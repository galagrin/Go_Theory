# Worker Pool vs Pipeline в Go

## 1. Главное отличие

|              | Worker Pool                          | Pipeline                             |
| ------------ | ------------------------------------ | ------------------------------------ |
| Структура    | Много **одинаковых** воркеров        | Несколько **разных стадий** подряд   |
| Поток данных | Задачи → одна очередь → воркеры      | Стадия 1 → Стадия 2 → Стадия 3 → ... |
| Цель         | Ограничить параллелизм               | Пошаговая обработка данных           |
| Каналы       | jobs + results                       | Цепочка каналов (ch1 → ch2 → ch3)    |
| Аналогия     | 3 кассы обслуживают очередь клиентов | Конвейер на заводе                   |

---

## 2. Worker Pool (пул воркеров)

### Когда использовать

-   Нужно ограничить количество одновременных горутин
-   Обработка фоновых задач, запросов к внешним API, очередей

### Схема

tasks → [jobs channel] → Worker 1
→ Worker 2 → [results channel] → результат
→ Worker 3

### Шаблон кода

```go
func workerPool(tasks []int, workers int) []int {
    jobs := make(chan int, len(tasks))
    results := make(chan int, len(tasks))

    // 1. Запускаем фиксированное количество воркеров
    for i := 0; i < workers; i++ {
        go func() {
            for task := range jobs {          // читаем, пока канал не закроют
                results <- task * 2           // обрабатываем
            }
        }()
    }

    // 2. Отправляем все задачи
    for _, task := range tasks {
        jobs <- task
    }
    close(jobs) // сигнал воркерам: задач больше нет

    // 3. Собираем результаты
    out := make([]int, 0, len(tasks))
    for i := 0; i < len(tasks); i++ {
        out = append(out, <-results)
    }
    return out
}
```

### Вариант с WaitGroup (если нужно закрывать results)

```go
var wg sync.WaitGroup

for i := 0; i < workers; i++ {
wg.Add(1)
go func() {
defer wg.Done()
for task := range jobs {
results <- task \* 2
}
}()
}

go func() {
wg.Wait()
close(results)
}()

// отправка задач + close(jobs)
// сбор через: for val := range results { ... }
```

## 3. Pipeline (конвейер)

### Когда использовать

-   Данные должны пройти несколько разных этапов обработки
-   Каждый этап делает свою работу и передаёт результат дальше

### Схема

Generator → numsChan → Multiply → multiplyChan → Filter → filterChan → результат

### Шаблон кода

```go
func pipeline(n int) []int {
    numsChan := make(chan int, n)
    multiplyChan := make(chan int, n)
    filterChan := make(chan int, n)

    // Стадия 1: Multiply
    go func() {
        for num := range numsChan {
            multiplyChan <- num * 2
        }
        close(multiplyChan) // закрываем следующий канал
    }()

    // Стадия 2: Filter
    go func() {
        for val := range multiplyChan {
            if val%2 == 0 {
                filterChan <- val
            }
        }
        close(filterChan)
    }()

    // Generator (источник данных)
    go func() {
        for i := 1; i <= n; i++ {
            numsChan <- i
        }
        close(numsChan) // запускает цепочку закрытий
    }()

    // Собираем результат
    result := make([]int, 0, n)
    for val := range filterChan {
        result = append(result, val)
    }
        return result
    }

```

---

## 4. Важные правила (для обоих паттернов)

1. **Кто пишет — тот и закрывает канал**
2. `for range` по каналу работает **до закрытия** канала
3. Закрытый канал можно читать (получишь zero value + false)
4. Писать в закрытый канал = panic
5. Не закрывай канал там, где ещё могут писать другие горутины
6. Буферизированные каналы уменьшают количество блокировок, но не обязательны

---

## 5. Как запомнить

-   **Worker Pool** = «ограниченное число одинаковых работников»
-   **Pipeline** = «конвейер из разных станков»

Worker Pool отвечает на вопрос: _«Сколько одновременно?»_  
Pipeline отвечает на вопрос: _«В каком порядке обрабатывать?»_
