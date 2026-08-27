# 📚 Моя база знаний по Go & Architecture

Добро пожаловать в личную шпаргалку! Ниже приведена навигация по всем разделам и темам.

---

## 📌 1. Основы языка

-   [Map основы](./01_Language_Basics/Map_basics.md)
-   [Map под капотом](./01_Language_Basics/Map_DeepDive.md)
-   [Map коллизии и переполнение](./01_Language_Basics/Map_hashCollision.md)
-   [Map под капотом простыми словами](./01_Language_Basics/Map_hashCollision.md)

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

-   [Паттерн Merge (Fan-In)](./01_Concurrency/.md).

## 📌 4. Архитектура и паттерны
