# Паттерн merge (Fan-In)

Классическая задача на собеседованиях уровня Middle+/Senior: объединить $N$ каналов в один.

```go
func merge(cs ...<-chan int) <-chan int {
    out := make(chan int)
    var wg sync.WaitGroup

    // Функция-воркер для вычитывания отдельного канала
    output := func(c <-chan int) {
        defer wg.Done()
        for n := range c {
            out <- n
        }
    }

    wg.Add(len(cs))
    for _, c := range cs {
        go output(c)
    }

    // Фоновый контроллер: ждет завершения всех писателей и закрывает out
    go func() {
        wg.Wait()
        close(out)
    }()

    return out
}
```
