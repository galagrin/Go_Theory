# 📚 Моя база знаний по Go & Architecture

Добро пожаловать в личную шпаргалку! Ниже приведена навигация по всем разделам и темам.

---

## 📌 1. Основы языка

### Мапы

-   [Map основы](./01_Language_Basics/Map_basics.md)
-   [Map под капотом](./01_Language_Basics/Map_DeepDive.md)
-   [Map коллизии и переполнение](./01_Language_Basics/Map_hashCollision.md)
-   [Map под капотом простыми словами](./01_Language_Basics/Map_hashCollision.md)

---

### Изменения Go

-   [Go 1.22: изменение семантики переменных цикла](./01_Language_Basics/go1.22_LoopVariables.md)

---

## 📌 2. Конкурентность

-   [Горутины основы](./02_Concurrency/Goroutines.md)
-   [Планировщик Go](./02_Concurrency/Scheduler.md)
-   [Планировщик: до Go 1.14 и после + Стек горутины](./02_Concurrency/Stack_Goroutines.md)
-   [Состязание мьютексов (lock contention)](./02_Concurrency/Contention.md)
-   [Race Detector](./02_Concurrency/Race_Detector.md)
-   ***

### Каналы

-   [Каналы внутреннее устройство](./02_Concurrency/Go_Channels.md)
-   [Select](./02_Concurrency/Select.md)
-   [Правила пользования каналами](./02_Concurrency/Channels_Rules.md)

---

### Примитивы синхронизации

-   [sync.WaitGroup](./02_Concurrency/WaitGroup.md)
-   [Mutex и RWMutex](./02_Concurrence/Mutex_RWMutex.md)
-   [Атомики](./02_Concurrence/Atomic.md)
-   [Мбютексы VS Атомики](./02_Concurrence/MutexvsAtomic.md)
-   [sync.Once или Однократное выполнение](./02_Concurrence/syncOnce.md)
-   [sync.Cond (Условные переменные)](./02_Concurrence/Cond_Pool.md)

---

## 📌 3. Рантайм и GC

### Стек и куча

-   [Стек и куча: основы](./03_Runtime_and_GC/Stack_and_Heap.md)
-   [Устройства стека](./03_Runtime_and_GC/Stack_Go.md)
-   [Устройства кучи](./03_Runtime_and_GC/Heap_Go.md)
-   [Escape Analysis](./03_Runtime_and_GC/EscapeAnalysis.md)

## 📌 4. Архитектура и паттерны

-   [Паттерн Merge (Fan-In)](./04_Architecture_and_Patterns/Fan-In.md).
-   [Worker Pool vs Pipeline в Go](./04_Architecture_and_Patterns/pipeline_vs_workerPool.md).
