# Полный курс Rust: От основ до Backend с Axum
**Интенсивный курс в стиле JavaRush**
**~300+ практических задач | 16 недель**
+
---

## 📚 Содержание

1. [Модуль 1: Основы синтаксиса и переменные](#модуль-1-основы-синтаксиса-и-переменные)
2. [Модуль 2: Управление потоком](#модуль-2-управление-потоком)
3. [Модуль 3: Циклы](#модуль-3-циклы)
4. [Модуль 4: Обработка ошибок](#модуль-4-обработка-ошибок-и-паники)
5. [Модуль 5: Ownership и Borrowing](#модуль-5-ownership-и-borrowing)
6. [Модуль 6: Структуры и методы](#модуль-6-структуры-и-методы)
7. [Модуль 7: Enums и Pattern Matching](#модуль-7-enums-и-pattern-matching)
8. [Модуль 8: Коллекции](#модуль-8-коллекции)
9. [Модуль 9: Обработка ошибок (Result)](#модуль-9-обработка-ошибок-result)
10. [Модуль 10: Generics и Traits](#модуль-10-generics-и-traits)
11. [Модуль 11: Iterators и Closures](#модуль-11-iterators-и-closures)
12. [Модуль 12: Тестирование](#модуль-12-тестирование)
13. [Модуль 13: Smart Pointers](#модуль-13-smart-pointers)
14. [Модуль 14: Concurrency](#модуль-14-concurrency)
15. [Модуль 15: Async/Await](#модуль-15-asyncawait)
16. [Модуль 16: Backend с Axum](#модуль-16-backend-с-axum)

---

# МОДУЛЬ 1: Основы синтаксиса и переменные
**Недели: 1-2 | Задачи: 20 | Rust Book: Главы 1-3**

## Теория

### 1.1 Установка и первая программа

**Основные концепции:**
- Rust - статически типизированный язык с упором на безопасность памяти без GC
- Cargo - менеджер пакетов и система сборки (аналог Maven в Java)
- Компилятор как "привратник" - не пропустит код с ошибками

**Команды:**
```bash
# Создание проекта
cargo new my_project
cd my_project

# Запуск (компиляция + выполнение)
cargo run

# Только компиляция
cargo build

# Компиляция с оптимизацией
cargo build --release

# Проверка без сборки (быстро!)
cargo check

# Запуск тестов
cargo test

# Форматирование кода
cargo fmt

# Линтер
cargo clippy
```

**Структура проекта:**
```
my_project/
├── Cargo.toml       # Манифест (как pom.xml)
├── Cargo.lock       # Зафиксированные версии
├── src/
│   ├── main.rs      # Точка входа для бинарника
│   └── lib.rs       # Библиотечный код
└── target/          # Скомпилированные артефакты
```

**Hello World:**
```rust
fn main() {
    println!("Hello, world!");
}
```

---

### 1.2 Переменные и типы

**Ключевые отличия от Java:**
| Java | Rust |
|------|------|
| Переменные мутабельны по умолчанию | Иммутабельны по умолчанию |
| `null` для отсутствия значения | `Option<T>` |
| Исключения для ошибок | `Result<T, E>` |
| GC управляет памятью | Система владения (ownership) |
| Примитивы и ссылки | Все типы единообразны |

**Целочисленные типы:**
| Разрядность | Знаковый | Беззнаковый | Диапазон (знаковый) |
|-------------|----------|-------------|---------------------|
| 8 бит | `i8` | `u8` | -128 до 127 |
| 16 бит | `i16` | `u16` | -32,768 до 32,767 |
| 32 бит | `i32` (по умолчанию) | `u32` | -2³¹ до 2³¹-1 |
| 64 бит | `i64` | `u64` | -2⁶³ до 2⁶³-1 |
| 128 бит | `i128` | `u128` | огромные числа |
| Размер указателя | `isize` | `usize` | зависит от архитектуры |

**Вещественные типы:**
- `f32` - одинарная точность
- `f64` - двойная точность (по умолчанию)

**Другие типы:**
- `bool` - true/false
- `char` - Unicode символ (4 байта!)

**Синтаксис переменных:**
```rust
// Иммутабельная (нельзя изменить)
let x = 5;
let y: u64 = 100;       // явный тип

// Мутабельная (можно изменить)
let mut z = 10;
z = 15;                  // OK

// Shadowing (затенение) - создание новой переменной
let x = 5;
let x = x + 1;           // новая переменная x = 6
let x = "строка";        // даже тип может измениться!

// Числовые литералы
let million = 1_000_000;     // подчеркивания для читаемости
let hex = 0xff;              // шестнадцатеричный
let binary = 0b1111_0000;    // двоичный
let byte = b'A';             // байт (только u8)
let suffix = 42u64;          // суффикс типа
```

**Константы:**
```rust
// Всегда иммутабельны, тип обязателен
const MAX_POINTS: u32 = 100_000;
const PI: f64 = 3.14159;
```

---

## Практические задачи

### Задача 1.1: Hello, Rust!
**Сложность:** 🌟
**Время:** 5 минут
**Теория:** Функции, возвращаемые значения

**Что нужно сделать:**
Измените функцию так, чтобы она возвращала строку "I'm ready to learn Rust!"

**Стартовый код:**
```rust
// src/lib.rs
fn greeting() -> &'static str {
    // TODO: исправьте строку
    "I'm ready to ___!"
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_greeting() {
        assert_eq!(greeting(), "I'm ready to learn Rust!");
    }
}
```

**Подсказки:**
- `&'static str` - ссылка на строку, существующую всё время работы программы
- Последнее выражение без `;` возвращается из функции
- Можно использовать `return`, но это не идиоматично

**Критерии:**
- ✅ Тест проходит
- ✅ Нет предупреждений компилятора

---

### Задача 1.2: Калькулятор скорости
**Сложность:** 🌟
**Время:** 10 минут
**Теория:** Функции, арифметические операции

**Что нужно сделать:**
Реализуйте функцию вычисления скорости: speed = distance / time

**Стартовый код:**
```rust
// src/lib.rs

/// Вычисляет скорость объекта
///
/// # Arguments
/// * `start` - начальная позиция (метры)
/// * `end` - конечная позиция (метры)
/// * `time_elapsed` - затраченное время (секунды)
///
/// # Returns
/// Скорость в метрах/секунду
fn speed(start: u32, end: u32, time_elapsed: u32) -> u32 {
    // TODO:
    // 1. Вычислите дистанцию (end - start)
    // 2. Разделите дистанцию на время
    todo!() // макрос todo!() вызывает панику
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_speed_basic() {
        assert_eq!(speed(0, 10, 2), 5);
    }

    #[test]
    fn test_speed_with_start() {
        assert_eq!(speed(10, 30, 4), 5);
    }

    #[test]
    fn test_speed_large() {
        assert_eq!(speed(0, 100, 10), 10);
    }
}
```

**Подсказки:**
- Целочисленное деление отбрасывает дробную часть: `5 / 2 == 2`
- Операторы: `+`, `-`, `*`, `/`, `%`
- Используйте скобки для контроля порядка операций

---

### Задача 1.3: Конвертер температур
**Сложность:** 🌟
**Время:** 15 минут
**Теория:** Типы данных, арифметика

**Что нужно сделать:**
Реализуйте конвертацию Цельсий ↔ Фаренгейт

Формулы:
- F = C × 9 / 5 + 32
- C = (F - 32) × 5 / 9

**Стартовый код:**
```rust
// src/lib.rs

fn celsius_to_fahrenheit(celsius: i32) -> i32 {
    // TODO: F = C * 9 / 5 + 32
    // ВАЖНО: порядок операций!
    todo!()
}

fn fahrenheit_to_celsius(fahrenheit: i32) -> i32 {
    // TODO: C = (F - 32) * 5 / 9
    todo!()
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_celsius_to_fahrenheit() {
        assert_eq!(celsius_to_fahrenheit(0), 32);
        assert_eq!(celsius_to_fahrenheit(100), 212);
        assert_eq!(celsius_to_fahrenheit(-40), -40);
        assert_eq!(celsius_to_fahrenheit(25), 77);
    }

    #[test]
    fn test_fahrenheit_to_celsius() {
        assert_eq!(fahrenheit_to_celsius(32), 0);
        assert_eq!(fahrenheit_to_celsius(212), 100);
        assert_eq!(fahrenheit_to_celsius(-40), -40);
    }
}
```

**Подсказки:**
- Используйте `i32` для отрицательных температур
- Скобки важны: `(a + b) * c`
- Целочисленное деление может быть неточным

---

### Задача 1.4: Приведение типов
**Сложность:** 🌟🌟
**Время:** 10 минут
**Теория:** Приведение типов, нет автокастинга

**Что нужно сделать:**
Исправьте ошибки компиляции, используя явное приведение типов

**Стартовый код (НЕ КОМПИЛИРУЕТСЯ!):**
```rust
// src/lib.rs

fn mix_types() -> u32 {
    let a: u8 = 100;
    let b: u16 = 200;
    let c: u32 = 300;

    // TODO: исправьте - нельзя складывать разные типы!
    let result = a + b + c;

    result
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_mix_types() {
        assert_eq!(mix_types(), 600);
    }
}
```

**Подсказки:**
- Используйте `as` для приведения: `a as u32`
- Rust НЕ делает автоматического приведения
- Приводите меньшие типы к большим

**Решение (не подглядывайте!):**
```rust
fn mix_types() -> u32 {
    let a: u8 = 100;
    let b: u16 = 200;
    let c: u32 = 300;
    let result = (a as u32) + (b as u32) + c;
    result
}
```

---

### Задача 1.5: Мутабельность
**Сложность:** 🌟🌟
**Время:** 10 минут
**Теория:** mut, иммутабельность по умолчанию

**Что нужно сделать:**
Исправьте код, добавив `mut` где необходимо

**Стартовый код (НЕ КОМПИЛИРУЕТСЯ!):**
```rust
// src/lib.rs

fn accumulate_sum(limit: u32) -> u32 {
    // TODO: добавьте mut где нужно
    let sum = 0;
    let i = 1;

    while i <= limit {
        sum = sum + i;
        i = i + 1;
    }

    sum
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_accumulate() {
        assert_eq!(accumulate_sum(5), 15); // 1+2+3+4+5
        assert_eq!(accumulate_sum(10), 55);
        assert_eq!(accumulate_sum(0), 0);
    }
}
```

**Подсказки:**
- Переменные иммутабельны по умолчанию
- `let mut x = 5;` для мутабельной переменной
- Подумайте, какие переменные изменяются

---

### Задача 1.6: Shadowing vs Mutation
**Сложность:** 🌟🌟
**Время:** 15 минут
**Теория:** Разница между shadowing и mut

**Что нужно сделать:**
Реализуйте две версии функции преобразования: через shadowing и через mut

**Стартовый код:**
```rust
// src/lib.rs

// Версия с shadowing
fn transform_shadowing(value: i32) -> i32 {
    // TODO: используя shadowing (let x = ...; let x = ...;)
    // 1. Удвойте value
    // 2. Прибавьте 10
    // 3. Умножьте на 3
    todo!()
}

// Версия с мутацией
fn transform_mutation(value: i32) -> i32 {
    // TODO: используя let mut
    // Те же операции
    todo!()
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_transform_shadowing() {
        assert_eq!(transform_shadowing(5), 60); // (5*2+10)*3
        assert_eq!(transform_shadowing(0), 30); // (0*2+10)*3
    }

    #[test]
    fn test_transform_mutation() {
        assert_eq!(transform_mutation(5), 60);
        assert_eq!(transform_mutation(0), 30);
    }
}
```

**Решение:**
```rust
fn transform_shadowing(value: i32) -> i32 {
    let value = value * 2;
    let value = value + 10;
    let value = value * 3;
    value
}

fn transform_mutation(value: i32) -> i32 {
    let mut result = value * 2;
    result = result + 10;
    result = result * 3;
    result
}
```

---

### Задачи 1.7-1.20: Дополнительные упражнения

**1.7: Проверка четности** 🌟
```rust
fn is_even(n: i32) -> bool {
    // TODO: верните true если n четное
    todo!()
}
```

**1.8: Абсолютное значение** 🌟
```rust
fn abs(n: i32) -> i32 {
    // TODO: верните |n|
    // Подсказка: используйте if
    todo!()
}
```

**1.9: Максимум из двух** 🌟
```rust
fn max(a: i32, b: i32) -> i32 {
    // TODO: верните наибольшее
    todo!()
}
```

**1.10: Площадь прямоугольника** 🌟
```rust
fn rectangle_area(width: u32, height: u32) -> u32 {
    todo!()
}
```

[Продолжение со всеми задачами...]

---

# МОДУЛЬ 2: Управление потоком
**Недели: 2 | Задачи: 15 | Rust Book: Глава 3**

## Теория

### 2.1 Условия if/else

**Синтаксис:**
```rust
let number = 7;

if number < 5 {
    println!("меньше 5");
} else if number < 10 {
    println!("от 5 до 9");
} else {
    println!("10 или больше");
}
```

**ВАЖНО:** Условие ОБЯЗАНО быть `bool`!
```rust
// ❌ НЕ компилируется
let x = 5;
if x {  // error: нет truthy/falsy
    println!("x не ноль");
}

// ✅ Правильно
if x != 0 {
    println!("x не ноль");
}
```

**if как выражение:**
```rust
let condition = true;
let number = if condition { 5 } else { 6 };
// number == 5

// Обе ветки должны возвращать ОДИНАКОВЫЙ тип!
// ❌ НЕ компилируется:
let bad = if true { 5 } else { "шесть" };
```

**Операторы сравнения:**
- `==` равно
- `!=` не равно
- `<` меньше
- `>` больше
- `<=` меньше или равно
- `>=` больше или равно

**Логические операторы:**
- `&&` И (AND)
- `||` ИЛИ (OR)
- `!` НЕ (NOT)

```rust
let age = 25;
let has_license = true;

// Можно ли водить?
if age >= 18 && has_license {
    println!("Можете водить");
}

// Сокращенное вычисление (short-circuit)
if false && expensive_function() {
    // expensive_function() НЕ вызовется
}
```

---

## Практические задачи

### Задача 2.1: FizzBuzz
**Сложность:** 🌟🌟
**Время:** 20 минут
**Теория:** Вложенные условия, операции с остатком

**Что нужно сделать:**
Классическая задача FizzBuzz:
- Делится на 3 → "Fizz"
- Делится на 5 → "Buzz"
- Делится на 3 И 5 → "FizzBuzz"
- Иначе → строковое представление числа

**Стартовый код:**
```rust
// src/lib.rs

fn fizzbuzz(n: u32) -> String {
    // TODO: реализуйте FizzBuzz
    // Подсказка: проверяйте деление на 15 ПЕРЕД 3 и 5!
    // Подсказка: используйте n % 3 == 0
    // Подсказка: n.to_string() конвертирует число в String
    todo!()
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_fizz() {
        assert_eq!(fizzbuzz(3), "Fizz");
        assert_eq!(fizzbuzz(6), "Fizz");
        assert_eq!(fizzbuzz(9), "Fizz");
    }

    #[test]
    fn test_buzz() {
        assert_eq!(fizzbuzz(5), "Buzz");
        assert_eq!(fizzbuzz(10), "Buzz");
    }

    #[test]
    fn test_fizzbuzz() {
        assert_eq!(fizzbuzz(15), "FizzBuzz");
        assert_eq!(fizzbuzz(30), "FizzBuzz");
        assert_eq!(fizzbuzz(45), "FizzBuzz");
    }

    #[test]
    fn test_number() {
        assert_eq!(fizzbuzz(1), "1");
        assert_eq!(fizzbuzz(2), "2");
        assert_eq!(fizzbuzz(7), "7");
    }
}
```

**Решение:**
```rust
fn fizzbuzz(n: u32) -> String {
    if n % 15 == 0 {
        String::from("FizzBuzz")
    } else if n % 3 == 0 {
        String::from("Fizz")
    } else if n % 5 == 0 {
        String::from("Buzz")
    } else {
        n.to_string()
    }
}
```

---

### Задача 2.2: Високосный год
**Сложность:** 🌟🌟
**Время:** 20 минут
**Теория:** Сложная логика, логические операторы

**Правила:**
1. Делится на 4 БЕЗ остатка → високосный
2. НО если делится на 100 → НЕ високосный
3. НО если делится на 400 → ВСЁ ЖЕ високосный

**Примеры:**
- 2000 → true (делится на 400)
- 1900 → false (делится на 100, но не на 400)
- 2004 → true (делится на 4, но не на 100)

**Стартовый код:**
```rust
// src/lib.rs

fn is_leap_year(year: u32) -> bool {
    // TODO: реализуйте проверку
    // Можно одним выражением или через if/else
    todo!()
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_divisible_by_400() {
        assert!(is_leap_year(2000));
        assert!(is_leap_year(2400));
    }

    #[test]
    fn test_divisible_by_100_not_400() {
        assert!(!is_leap_year(1900));
        assert!(!is_leap_year(2100));
    }

    #[test]
    fn test_divisible_by_4_not_100() {
        assert!(is_leap_year(2004));
        assert!(is_leap_year(2024));
    }

    #[test]
    fn test_not_divisible_by_4() {
        assert!(!is_leap_year(2001));
        assert!(!is_leap_year(2019));
    }
}
```

**Компактное решение:**
```rust
fn is_leap_year(year: u32) -> bool {
    (year % 4 == 0 && year % 100 != 0) || (year % 400 == 0)
}
```

---

[Задачи 2.3-2.15 продолжаются аналогично...]

---

# МОДУЛЬ 3: Циклы
**Недели: 2-3 | Задачи: 18 | Rust Book: Глава 3**

## Теория

### 3.1 Цикл loop (бесконечный)

```rust
let mut count = 0;
loop {
    count += 1;
    if count == 10 {
        break; // выход
    }
}

// Возврат значения из loop
let result = loop {
    count += 1;
    if count == 20 {
        break count * 2; // возвращаем значение
    }
};
```

### 3.2 Цикл while

```rust
let mut number = 3;

while number != 0 {
    println!("{}!", number);
    number -= 1;
}
```

### 3.3 Цикл for

```rust
// Диапазоны (ranges)
for i in 1..5 {      // 1, 2, 3, 4 (не включает 5)
    println!("{}", i);
}

for i in 1..=5 {     // 1, 2, 3, 4, 5 (включает 5)
    println!("{}", i);
}

// Обратный порядок
for i in (1..5).rev() {  // 4, 3, 2, 1
    println!("{}", i);
}

// С шагом
for i in (0..10).step_by(2) {  // 0, 2, 4, 6, 8
    println!("{}", i);
}
```

### 3.4 Метки циклов

```rust
'outer: for x in 0..5 {
    for y in 0..5 {
        if x == 2 && y == 2 {
            break 'outer; // выход из внешнего цикла
        }
    }
}
```

---

## Практические задачи

### Задача 3.1: Факториал (while)
**Сложность:** 🌟🌟
**Время:** 15 минут

**Стартовый код:**
```rust
fn factorial_while(n: u32) -> u32 {
    // TODO: вычислите n! используя while
    // 0! = 1, 5! = 1*2*3*4*5 = 120
    todo!()
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_factorial() {
        assert_eq!(factorial_while(0), 1);
        assert_eq!(factorial_while(1), 1);
        assert_eq!(factorial_while(5), 120);
        assert_eq!(factorial_while(10), 3_628_800);
    }
}
```

---

### Задача 3.2: Факториал (for)
**Сложность:** 🌟🌟
**Время:** 10 минут

**Стартовый код:**
```rust
fn factorial_for(n: u32) -> u32 {
    let mut result = 1;
    // TODO: используйте for с диапазоном 1..=n
    todo!()
}
```

**Решение:**
```rust
fn factorial_for(n: u32) -> u32 {
    let mut result = 1;
    for i in 1..=n {
        result *= i;
    }
    result
}
```

---

### Задача 3.3: Сумма чётных
**Сложность:** 🌟🌟
**Время:** 15 минут

**Стартовый код:**
```rust
fn sum_of_evens(n: u32) -> u32 {
    // TODO: просуммируйте все чётные от 1 до n
    todo!()
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_sum() {
        assert_eq!(sum_of_evens(10), 30); // 2+4+6+8+10
        assert_eq!(sum_of_evens(5), 6);   // 2+4
        assert_eq!(sum_of_evens(1), 0);
    }
}
```

---

### Задача 3.4: Фибоначчи
**Сложность:** 🌟🌟🌟
**Время:** 25 минут

**Стартовый код:**
```rust
fn fibonacci(n: u32) -> u64 {
    if n == 0 { return 0; }
    if n == 1 { return 1; }

    // TODO: используйте цикл с двумя переменными
    // prev, curr
    todo!()
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_fib() {
        assert_eq!(fibonacci(0), 0);
        assert_eq!(fibonacci(1), 1);
        assert_eq!(fibonacci(2), 1);
        assert_eq!(fibonacci(10), 55);
        assert_eq!(fibonacci(20), 6765);
    }
}
```

---

[Задачи 3.5-3.18: Реализация различных алгоритмов с циклами...]

---

# МОДУЛЬ 4: Обработка ошибок и паники
**Недели: 3 | Задачи: 12 | Rust Book: Глава 9**

## Теория

### 4.1 Panic! - неисправимые ошибки

```rust
fn divide(a: i32, b: i32) -> i32 {
    if b == 0 {
        panic!("Деление на ноль!");
    }
    a / b
}
```

### 4.2 Переполнение (Overflow)

В debug: переполнение → паника
В release: переполнение → wrapping (обертывание)

```rust
let x: u8 = 255;
// В debug: паника
// В release: x + 1 == 0
```

**Методы контроля:**
```rust
let x: u8 = 255;

// Wrapping - циклическое
assert_eq!(x.wrapping_add(1), 0);

// Saturating - насыщение
assert_eq!(x.saturating_add(1), 255);

// Checked - возвращает Option
assert_eq!(x.checked_add(1), None);
assert_eq!(x.checked_add(0), Some(255));

// Overflowing - (результат, флаг)
let (result, overflow) = x.overflowing_add(1);
assert_eq!(result, 0);
assert!(overflow);
```

---

## Практические задачи

### Задача 4.1: Безопасное деление
**Сложность:** 🌟🌟
**Стартовый код:**
```rust
fn safe_divide(dividend: i32, divisor: i32) -> i32 {
    // TODO: проверьте divisor != 0, иначе panic!
    todo!()
}

#[cfg(test)]
mod tests {
    #[test]
    #[should_panic(expected = "ноль")]
    fn test_panic() {
        safe_divide(10, 0);
    }
}
```

---

### Задача 4.2: Безопасный факториал
**Сложность:** 🌟🌟🌟
**Стартовый код:**
```rust
fn checked_factorial(n: u32) -> Option<u32> {
    let mut result = 1u32;
    for i in 2..=n {
        // TODO: используйте checked_mul
        result = todo!();
    }
    Some(result)
}

#[cfg(test)]
mod tests {
    #[test]
    fn test_overflow() {
        assert_eq!(checked_factorial(13), None); // переполнение
        assert_eq!(checked_factorial(12), Some(479_001_600));
    }
}
```

**Решение:**
```rust
fn checked_factorial(n: u32) -> Option<u32> {
    let mut result = 1u32;
    for i in 2..=n {
        result = result.checked_mul(i)?; // ? возвращает None
    }
    Some(result)
}
```

---

[Задачи 4.3-4.12...]

---

# МОДУЛЬ 5: Ownership и Borrowing
**Недели: 4-5 | Задачи: 30 | Rust Book: Глава 4**

## Теория

### 5.1 Три правила Ownership

1. **Каждое значение имеет владельца (owner)**
2. **У значения может быть только ОДИН владелец**
3. **Когда владелец выходит из scope, значение удаляется**

### 5.2 Move semantics

```rust
let s1 = String::from("hello");
let s2 = s1; // s1 ПЕРЕМЕЩЁН в s2

// ❌ ошибка: s1 больше не валиден!
println!("{}", s1);

// ✅ OK
println!("{}", s2);
```

**Почему нет Copy?**
- `String` хранит данные в куче
- Копирование было бы дорогим
- Move предотвращает double-free

**Copy types (примитивы):**
```rust
let x = 5;
let y = x; // копируется, не перемещается

// ✅ оба валидны
println!("{} {}", x, y);
```

Типы с trait `Copy`:
- Все целочисленные: `i32`, `u64`, etc
- `bool`, `char`, `f64`
- Кортежи из Copy типов: `(i32, i32)`

### 5.3 Borrowing (заимствование)

**Иммутабельная ссылка `&T`:**
```rust
fn calculate_length(s: &String) -> usize {
    s.len()
} // s выходит из scope, но ничего не удаляется

let s1 = String::from("hello");
let len = calculate_length(&s1); // передаём ссылку
println!("{} {}", s1, len); // s1 всё ещё валиден
```

**Мутабельная ссылка `&mut T`:**
```rust
fn append_world(s: &mut String) {
    s.push_str(", world");
}

let mut s = String::from("hello");
append_world(&mut s);
println!("{}", s); // "hello, world"
```

### 5.4 Правила заимствования

1. **В любой момент может быть:**
   - Одна мутабельная ссылка `&mut T`
   - ИЛИ любое кол-во иммутабельных `&T`

2. **Ссылки должны быть всегда валидны**

```rust
let mut s = String::from("hello");

let r1 = &s;     // OK
let r2 = &s;     // OK
// let r3 = &mut s; // ❌ ОШИБКА: уже есть иммутабельные

println!("{} {}", r1, r2);
// r1 и r2 больше не используются

let r3 = &mut s; // ✅ OK: предыдущие ссылки неактивны
r3.push_str("!");
```

### 5.5 Dangling references (висячие ссылки)

```rust
// ❌ НЕ компилируется
fn dangle() -> &String {
    let s = String::from("hello");
    &s // s удалится, ссылка станет невалидной!
}

// ✅ Правильно - передаём владение
fn no_dangle() -> String {
    let s = String::from("hello");
    s // перемещаем значение наружу
}
```

### 5.6 Slice type

**String slice `&str`:**
```rust
let s = String::from("hello world");

let hello = &s[0..5];   // "hello"
let world = &s[6..11];  // "world"

// Сокращения
let slice = &s[..5];    // от начала
let slice = &s[6..];    // до конца
let slice = &s[..];     // вся строка
```

**Array slice `&[T]`:**
```rust
let a = [1, 2, 3, 4, 5];
let slice = &a[1..3]; // [2, 3]
```

---

## Практические задачи

### Задача 5.1: Move vs Copy
**Сложность:** 🌟
**Время:** 10 минут

**Стартовый код:**
```rust
// TODO: исправьте ошибки компиляции
fn move_semantics1() {
    let s1 = String::from("hello");
    let s2 = s1;

    // ❌ ошибка - исправьте!
    println!("{}", s1);
}

fn copy_semantics() {
    let x = 5;
    let y = x;

    // ✅ это работает, почему?
    println!("{}", x);
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_move() {
        move_semantics1(); // должно компилироваться
    }
}
```

**Возможные решения:**
1. Использовать `s2` вместо `s1`
2. Клонировать: `let s2 = s1.clone();`
3. Использовать ссылку: `let s2 = &s1;`

---

### Задача 5.2: Функция с заимствованием
**Сложность:** 🌟🌟
**Время:** 15 минут

**Что нужно сделать:**
Исправьте функцию, чтобы она принимала ссылку

**Стартовый код:**
```rust
// ❌ эта функция забирает владение!
fn calculate_length(s: String) -> usize {
    s.len()
}

fn main() {
    let s1 = String::from("hello");
    let len = calculate_length(s1);

    // ❌ ошибка: s1 перемещён!
    println!("Length of '{}' is {}.", s1, len);
}

// TODO: исправьте сигнатуру calculate_length
// чтобы она заимствовала, а не забирала владение
```

**Решение:**
```rust
fn calculate_length(s: &String) -> usize {
    s.len()
}

fn main() {
    let s1 = String::from("hello");
    let len = calculate_length(&s1);
    println!("Length of '{}' is {}.", s1, len);
}
```

---

### Задача 5.3: Мутабельное заимствование
**Сложность:** 🌟🌟
**Время:** 20 минут

**Стартовый код:**
```rust
fn append_exclamation(s: /* TODO: тип? */) {
    // TODO: добавьте "!" к строке
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_append() {
        let mut s = String::from("hello");
        append_exclamation(/* TODO */);
        assert_eq!(s, "hello!");
    }
}
```

**Решение:**
```rust
fn append_exclamation(s: &mut String) {
    s.push('!');
}

#[test]
fn test_append() {
    let mut s = String::from("hello");
    append_exclamation(&mut s);
    assert_eq!(s, "hello!");
}
```

---

### Задача 5.4: Правила заимствования
**Сложность:** 🌟🌟🌟
**Время:** 25 минут

**Стартовый код (НЕ КОМПИЛИРУЕТСЯ!):**
```rust
fn borrowing_rules() {
    let mut s = String::from("hello");

    let r1 = &s;
    let r2 = &s;
    let r3 = &mut s; // ❌ ошибка!

    println!("{}, {}, {}", r1, r2, r3);
}

// TODO: исправьте три способами:
// 1. Используйте r3 после того как r1, r2 больше не нужны
// 2. Уберите r3
// 3. Сделайте r1, r2 мутабельными
```

---

### Задача 5.5: Первое слово (slices)
**Сложность:** 🌟🌟🌟
**Время:** 30 минут

**Что нужно сделать:**
Напишите функцию, возвращающую первое слово из строки

**Стартовый код:**
```rust
fn first_word(s: &String) -> &str {
    let bytes = s.as_bytes();

    for (i, &item) in bytes.iter().enumerate() {
        if item == b' ' {
            // TODO: верните slice от 0 до i
        }
    }

    // TODO: если пробела нет, верните всю строку
    todo!()
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_first_word() {
        let s = String::from("hello world");
        assert_eq!(first_word(&s), "hello");

        let s2 = String::from("hello");
        assert_eq!(first_word(&s2), "hello");
    }
}
```

**Решение:**
```rust
fn first_word(s: &String) -> &str {
    let bytes = s.as_bytes();

    for (i, &item) in bytes.iter().enumerate() {
        if item == b' ' {
            return &s[..i];
        }
    }

    &s[..]
}
```

**Улучшенная версия:**
```rust
// Принимаем &str вместо &String - работает с обоими!
fn first_word(s: &str) -> &str {
    let bytes = s.as_bytes();

    for (i, &item) in bytes.iter().enumerate() {
        if item == b' ' {
            return &s[..i];
        }
    }

    s
}
```

---

[Задачи 5.6-5.30: упражнения на ownership, borrowing, slices...]

---

# МОДУЛЬ 6: Структуры и методы
**Недели: 5-6 | Задачи: 25 | Rust Book: Глава 5**

## Теория

### 6.1 Определение структур

```rust
struct User {
    username: String,
    email: String,
    sign_in_count: u64,
    active: bool,
}

// Создание экземпляра
let user1 = User {
    email: String::from("user@example.com"),
    username: String::from("username123"),
    active: true,
    sign_in_count: 1,
};

// Доступ к полям
println!("{}", user1.email);

// Мутабельная структура
let mut user2 = User {
    email: String::from("another@example.com"),
    username: String::from("another"),
    active: true,
    sign_in_count: 1,
};

user2.email = String::from("newemail@example.com");
```

### 6.2 Field init shorthand

```rust
fn build_user(email: String, username: String) -> User {
    User {
        email,    // вместо email: email
        username, // вместо username: username
        active: true,
        sign_in_count: 1,
    }
}
```

### 6.3 Struct update syntax

```rust
let user2 = User {
    email: String::from("another@example.com"),
    ..user1  // остальные поля копируются из user1
};

// ВНИМАНИЕ: user1.username перемещён в user2!
// user1.username больше не валиден, но user1.active - валиден (Copy)
```

### 6.4 Tuple structs

```rust
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);

let black = Color(0, 0, 0);
let origin = Point(0, 0, 0);

// Разные типы, несмотря на одинаковые поля!
```

### 6.5 Unit-like structs

```rust
struct AlwaysEqual;

let subject = AlwaysEqual;
```

### 6.6 Методы

```rust
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    // Метод (принимает &self)
    fn area(&self) -> u32 {
        self.width * self.height
    }

    // Метод с мутацией
    fn double(&mut self) {
        self.width *= 2;
        self.height *= 2;
    }

    // Метод, забирающий ownership
    fn destroy(self) {
        // self удаляется
    }

    // Ассоциированная функция (конструктор)
    fn new(width: u32, height: u32) -> Rectangle {
        Rectangle { width, height }
    }

    // Ещё конструктор
    fn square(size: u32) -> Rectangle {
        Rectangle {
            width: size,
            height: size,
        }
    }
}

// Использование
let rect = Rectangle::new(30, 50);
let area = rect.area();

let sq = Rectangle::square(10);
```

### 6.7 Множественные impl блоки

```rust
impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

impl Rectangle {
    fn can_hold(&self, other: &Rectangle) -> bool {
        self.width > other.width && self.height > other.height
    }
}
```

### 6.8 Debug trait

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

let rect = Rectangle { width: 30, height: 50 };
println!("{:?}", rect);    // Debug format
println!("{:#?}", rect);   // Pretty-print
dbg!(&rect);               // Debug макрос
```

---

## Практические задачи

### Задача 6.1: Структура User
**Сложность:** 🌟
**Время:** 15 минут

**Стартовый код:**
```rust
// TODO: определите структуру User с полями:
// - username: String
// - email: String
// - age: u8
// - active: bool

// TODO: реализуйте функцию создания пользователя
fn build_user(username: String, email: String, age: u8) -> User {
    todo!()
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_user() {
        let user = build_user(
            String::from("alice"),
            String::from("alice@example.com"),
            25
        );
        assert_eq!(user.username, "alice");
        assert_eq!(user.age, 25);
        assert!(user.active);
    }
}
```

---

### Задача 6.2: Структура Rectangle
**Сложность:** 🌟🌟
**Время:** 20 минут

**Стартовый код:**
```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    // TODO: реализуйте метод area
    fn area(&self) -> u32 {
        todo!()
    }

    // TODO: реализуйте конструктор new
    fn new(width: u32, height: u32) -> Rectangle {
        todo!()
    }

    // TODO: реализуйте конструктор square
    fn square(size: u32) -> Rectangle {
        todo!()
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_area() {
        let rect = Rectangle::new(30, 50);
        assert_eq!(rect.area(), 1500);
    }

    #[test]
    fn test_square() {
        let sq = Rectangle::square(10);
        assert_eq!(sq.area(), 100);
    }
}
```

---

### Задача 6.3: Метод can_hold
**Сложность:** 🌟🌟
**Время:** 20 минут

**Что нужно сделать:**
Добавьте метод, проверяющий, может ли один прямоугольник поместиться в другой

**Стартовый код:**
```rust
impl Rectangle {
    fn can_hold(&self, other: &Rectangle) -> bool {
        // TODO: верните true если self больше other
        // по обеим dimensions
        todo!()
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_can_hold() {
        let rect1 = Rectangle::new(30, 50);
        let rect2 = Rectangle::new(10, 40);
        let rect3 = Rectangle::new(60, 45);

        assert!(rect1.can_hold(&rect2));
        assert!(!rect1.can_hold(&rect3));
    }
}
```

---

[Задачи 6.4-6.25: Point, Circle, Person, Car, etc...]

---

# МОДУЛЬ 7: Enums и Pattern Matching
**Недели: 6-7 | Задачи: 30 | Rust Book: Глава 6**

## Теория

### 7.1 Определение Enums

```rust
enum IpAddrKind {
    V4,
    V6,
}

let four = IpAddrKind::V4;
let six = IpAddrKind::V6;
```

### 7.2 Enums с данными

```rust
enum IpAddr {
    V4(u8, u8, u8, u8),
    V6(String),
}

let home = IpAddr::V4(127, 0, 0, 1);
let loopback = IpAddr::V6(String::from("::1"));

// Разные типы данных в вариантах!
enum Message {
    Quit,                       // нет данных
    Move { x: i32, y: i32 },    // анонимная структура
    Write(String),              // String
    ChangeColor(i32, i32, i32), // три i32
}
```

### 7.3 Методы для Enums

```rust
impl Message {
    fn call(&self) {
        // реализация...
    }
}

let m = Message::Write(String::from("hello"));
m.call();
```

### 7.4 Option<T>

**Нет null в Rust!** Вместо этого:
```rust
enum Option<T> {
    Some(T),
    None,
}

let some_number = Some(5);
let some_string = Some("a string");
let absent_number: Option<i32> = None;

// ❌ НЕ компилируется - нельзя смешивать T и Option<T>!
let x: i8 = 5;
let y: Option<i8> = Some(5);
let sum = x + y; // ошибка!

// ✅ Нужно обработать Option
let sum = x + y.unwrap_or(0);
```

### 7.5 match Expression

```rust
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}

// match должен быть исчерпывающим!
// ❌ ошибка - не все варианты покрыты
fn bad_match(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        // остальные?
    }
}
```

### 7.6 Patterns с данными

```rust
#[derive(Debug)]
enum UsState {
    Alabama,
    Alaska,
    // ...
}

enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter(UsState),
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter(state) => {
            println!("State quarter from {:?}!", state);
            25
        }
    }
}
```

### 7.7 Matching Option<T>

```rust
fn plus_one(x: Option<i32>) -> Option<i32> {
    match x {
        None => None,
        Some(i) => Some(i + 1),
    }
}

let five = Some(5);
let six = plus_one(five);
let none = plus_one(None);
```

### 7.8 Placeholder _

```rust
let some_u8_value = 0u8;
match some_u8_value {
    1 => println!("one"),
    3 => println!("three"),
    5 => println!("five"),
    7 => println!("seven"),
    _ => (), // все остальные
}
```

### 7.9 if let

```rust
let some_value = Some(3);

// Длинный способ
match some_value {
    Some(3) => println!("three"),
    _ => (),
}

// Короткий способ
if let Some(3) = some_value {
    println!("three");
}

// С else
if let Some(3) = some_value {
    println!("three");
} else {
    println!("not three");
}
```

---

## Практические задачи

### Задача 7.1: Enum Traffic Light
**Сложность:** 🌟
**Время:** 15 минут

**Стартовый код:**
```rust
// TODO: определите enum TrafficLight с вариантами:
// Red, Yellow, Green

// TODO: реализуйте функцию, возвращающую время в секундах
fn duration(light: TrafficLight) -> u8 {
    // Red: 60, Yellow: 5, Green: 45
    todo!()
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_duration() {
        assert_eq!(duration(TrafficLight::Red), 60);
        assert_eq!(duration(TrafficLight::Yellow), 5);
        assert_eq!(duration(TrafficLight::Green), 45);
    }
}
```

---

### Задача 7.2: Option - safe division
**Сложность:** 🌟🌟
**Время:** 20 минут

**Стартовый код:**
```rust
// TODO: верните Some(результат) или None при делении на 0
fn safe_divide(dividend: i32, divisor: i32) -> Option<i32> {
    todo!()
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_safe_divide() {
        assert_eq!(safe_divide(10, 2), Some(5));
        assert_eq!(safe_divide(10, 3), Some(3)); // целочисленное
        assert_eq!(safe_divide(10, 0), None);
    }
}
```

**Решение:**
```rust
fn safe_divide(dividend: i32, divisor: i32) -> Option<i32> {
    if divisor == 0 {
        None
    } else {
        Some(dividend / divisor)
    }
}
```

---

### Задача 7.3: Enum Message
**Сложность:** 🌟🌟🌟
**Время:** 30 минут

**Стартовый код:**
```rust
// TODO: определите enum Message с вариантами:
// - Quit
// - Move { x: i32, y: i32 }
// - Write(String)
// - ChangeColor(u8, u8, u8)

impl Message {
    fn call(&self) {
        // TODO: используйте match для обработки каждого варианта
        // и выведите соответствующее сообщение
        todo!()
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_message() {
        let messages = vec![
            Message::Quit,
            Message::Move { x: 10, y: 20 },
            Message::Write(String::from("hello")),
            Message::ChangeColor(255, 0, 0),
        ];

        for msg in messages {
            msg.call();
        }
    }
}
```

---

[Задачи 7.4-7.30: Result, сложные pattern matching, etc...]

---

# МОДУЛЬ 8: Коллекции
**Недели: 7-8 | Задачи: 35 | Rust Book: Глава 8**

## Теория

### 8.1 Vector

```rust
// Создание
let v: Vec<i32> = Vec::new();
let v = vec![1, 2, 3];

// Добавление
let mut v = Vec::new();
v.push(5);
v.push(6);

// Чтение
let third: &i32 = &v[2];
let third: Option<&i32> = v.get(2);

// Итерация
for i in &v {
    println!("{}", i);
}

// Мутабельная итерация
for i in &mut v {
    *i += 50;
}

// Vec с enum для разных типов
enum SpreadsheetCell {
    Int(i32),
    Float(f64),
    Text(String),
}

let row = vec![
    SpreadsheetCell::Int(3),
    SpreadsheetCell::Text(String::from("blue")),
    SpreadsheetCell::Float(10.12),
];
```

### 8.2 String

```rust
// Создание
let mut s = String::new();
let s = "initial contents".to_string();
let s = String::from("initial contents");

// Добавление
let mut s = String::from("foo");
s.push_str("bar");
s.push('!');

// Конкатенация
let s1 = String::from("Hello, ");
let s2 = String::from("world!");
let s3 = s1 + &s2; // s1 перемещён!

// format! макрос (не забирает владение)
let s1 = String::from("tic");
let s2 = String::from("tac");
let s3 = String::from("toe");
let s = format!("{}-{}-{}", s1, s2, s3);

// Индексация НЕ работает!
// ❌ let h = s[0];

// Итерация по символам
for c in "नमस्ते".chars() {
    println!("{}", c);
}

// Итерация по байтам
for b in "नमस्ते".bytes() {
    println!("{}", b);
}
```

### 8.3 HashMap

```rust
use std::collections::HashMap;

// Создание
let mut scores = HashMap::new();
scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Yellow"), 50);

// Создание из векторов
let teams = vec![String::from("Blue"), String::from("Yellow")];
let initial_scores = vec![10, 50];
let scores: HashMap<_, _> = teams.iter()
    .zip(initial_scores.iter())
    .collect();

// Чтение
let team_name = String::from("Blue");
let score = scores.get(&team_name); // Option<&V>

// Итерация
for (key, value) in &scores {
    println!("{}: {}", key, value);
}

// Обновление
scores.insert(String::from("Blue"), 25); // перезапись

// Вставка если нет
scores.entry(String::from("Blue")).or_insert(50);

// Обновление на основе старого значения
let text = "hello world wonderful world";
let mut map = HashMap::new();
for word in text.split_whitespace() {
    let count = map.entry(word).or_insert(0);
    *count += 1;
}
```

---

## Практические задачи

### Задача 8.1: Среднее, медиана, мода
**Сложность:** 🌟🌟🌟
**Время:** 45 минут

**Что нужно сделать:**
Для списка целых чисел вычислите:
1. Среднее (mean)
2. Медиану (median) - среднее значение после сортировки
3. Моду (mode) - значение, встречающееся чаще всего

**Стартовый код:**
```rust
use std::collections::HashMap;

fn mean(numbers: &[i32]) -> f64 {
    // TODO: вычислите среднее
    todo!()
}

fn median(numbers: &mut [i32]) -> f64 {
    // TODO: отсортируйте и найдите среднее значение
    // Подсказка: numbers.sort()
    // Для чётного кол-ва элементов - среднее двух центральных
    todo!()
}

fn mode(numbers: &[i32]) -> i32 {
    // TODO: используйте HashMap для подсчёта частоты
    // Верните число с наибольшей частотой
    todo!()
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_mean() {
        assert_eq!(mean(&[1, 2, 3, 4, 5]), 3.0);
        assert_eq!(mean(&[2, 4, 6]), 4.0);
    }

    #[test]
    fn test_median() {
        assert_eq!(median(&mut [1, 2, 3, 4, 5]), 3.0);
        assert_eq!(median(&mut [1, 2, 3, 4]), 2.5);
    }

    #[test]
    fn test_mode() {
        assert_eq!(mode(&[1, 2, 2, 3, 3, 3, 4]), 3);
        assert_eq!(mode(&[5, 5, 5, 1, 2]), 5);
    }
}
```

---

[Задачи 8.2-8.35: работа с Vec, String, HashMap...]

---

# МОДУЛЬ 9: Обработка ошибок (Result)
**Недели: 8-9 | Задачи: 20 | Rust Book: Глава 9**

## Теория

### 9.1 Result<T, E>

```rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}

use std::fs::File;

let f = File::open("hello.txt");

let f = match f {
    Ok(file) => file,
    Err(error) => panic!("Problem opening: {:?}", error),
};
```

### 9.2 Оператор ?

```rust
use std::io;
use std::io::Read;
use std::fs::File;

fn read_username_from_file() -> Result<String, io::Error> {
    let mut f = File::open("hello.txt")?; // если Err - вернёт его
    let mut s = String::new();
    f.read_to_string(&mut s)?;
    Ok(s)
}

// Ещё короче с chain
fn read_username_from_file() -> Result<String, io::Error> {
    let mut s = String::new();
    File::open("hello.txt")?.read_to_string(&mut s)?;
    Ok(s)
}
```

### 9.3 Кастомные типы ошибок

```rust
use std::fmt;

#[derive(Debug)]
enum MyError {
    IoError(std::io::Error),
    ParseError(std::num::ParseIntError),
    CustomError(String),
}

impl fmt::Display for MyError {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        match self {
            MyError::IoError(e) => write!(f, "IO error: {}", e),
            MyError::ParseError(e) => write!(f, "Parse error: {}", e),
            MyError::CustomError(msg) => write!(f, "Error: {}", msg),
        }
    }
}

impl std::error::Error for MyError {}
```

---

[Задачи 9.1-9.20...]

---

# МОДУЛЬ 10: Generics и Traits
**Недели: 9-10 | Задачи: 25 | Rust Book: Глава 10**

## Теория

### 10.1 Generic функции

```rust
fn largest<T: PartialOrd>(list: &[T]) -> &T {
    let mut largest = &list[0];
    for item in list {
        if item > largest {
            largest = item;
        }
    }
    largest
}
```

### 10.2 Generic структуры

```rust
struct Point<T> {
    x: T,
    y: T,
}

impl<T> Point<T> {
    fn new(x: T, y: T) -> Self {
        Point { x, y }
    }
}

// Множественные типы
struct Point<T, U> {
    x: T,
    y: U,
}
```

### 10.3 Traits

```rust
pub trait Summary {
    fn summarize(&self) -> String;

    // Default implementation
    fn default_summary(&self) -> String {
        String::from("(Read more...)")
    }
}

impl Summary for NewsArticle {
    fn summarize(&self) -> String {
        format!("{}, by {} ({})", self.headline, self.author, self.location)
    }
}
```

### 10.4 Trait bounds

```rust
pub fn notify<T: Summary>(item: &T) {
    println!("Breaking news! {}", item.summarize());
}

// Множественные bounds
pub fn notify<T: Summary + Display>(item: &T) {
    // ...
}

// where clause
fn some_function<T, U>(t: &T, u: &U) -> i32
where
    T: Display + Clone,
    U: Clone + Debug,
{
    // ...
}
```

---

[Задачи 10.1-10.25...]

---

# МОДУЛЬ 11-16 продолжаются аналогично...

# МОДУЛЬ 16: Backend с Axum
**Недели: 15-16 | Задачи: 50 | Финальный проект**

## Теория

### 16.1 Установка Axum

```toml
[dependencies]
axum = "0.7"
tokio = { version = "1", features = ["full"] }
serde = { version = "1", features = ["derive"] }
serde_json = "1"
```

### 16.2 Hello World API

```rust
use axum::{
    routing::get,
    Router,
};

#[tokio::main]
async fn main() {
    let app = Router::new()
        .route("/", get(handler));

    let listener = tokio::net::TcpListener::bind("127.0.0.1:3000")
        .await
        .unwrap();

    axum::serve(listener, app).await.unwrap();
}

async fn handler() -> &'static str {
    "Hello, Axum!"
}
```

### 16.3 JSON API

```rust
use axum::{Json, response::IntoResponse};
use serde::{Deserialize, Serialize};

#[derive(Serialize, Deserialize)]
struct User {
    id: u32,
    name: String,
}

async fn create_user(
    Json(payload): Json<User>,
) -> impl IntoResponse {
    Json(payload)
}

let app = Router::new()
    .route("/users", post(create_user));
```

---

## Финальный проект: Blog API

**Требования:**
- CRUD для постов
- Аутентификация JWT
- PostgreSQL
- Тесты

[Детальные задачи...]

---

# 🎓 Заключение

Вы прошли полный курс от основ до backend разработки!

**Следующие шаги:**
1. Изучите async patterns глубже
2. Попрактикуйтесь с real-world проектами
3. Изучите production deployment

**Ресурсы:**
- The Rust Book: https://doc.rust-lang.org/book/
- Rustlings: https://rustlings.cool/
- Rust by Example: https://doc.rust-lang.org/rust-by-example/

**Удачи в изучении Rust! 🦀**
