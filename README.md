# Java 8 Features – Complete Guide

A comprehensive guide to Java 8 features with examples, explanations, and interview questions. This repository covers functional programming, Lambda Expressions, Stream API, and other important enhancements introduced in Java 8.

## Table of Contents

1. [Introduction](#introduction)
2. [Lambda Expressions](#1-lambda-expressions)
3. [Functional Interfaces](#2-functional-interfaces)
4. [Method References](#3-method-references)
5. [Stream API](#4-stream-api)
6. [forEach() Method](#5-foreach-method)
7. [Optional Class](#6-optional-class)
8. [Default and Static Methods in Interfaces](#7-default-and-static-methods-in-interfaces)
9. [Predefined Functional Interfaces](#8-predefined-functional-interfaces)
10. [Collectors](#9-collectors)
11. [Date and Time API](#10-date-and-time-api)
12. [CompletableFuture](#11-completablefuture)
13. [Base64 API](#12-base64-api)
14. [StringJoiner](#13-stringjoiner)
15. [Parallel Streams](#14-parallel-streams)
16. [Interview Questions](#interview-questions)

## Introduction

Java 8 was released in March 2014 and introduced several features that made Java programming more expressive and functional.

### Major Features

- Lambda Expressions
- Functional Interfaces
- Method References
- Stream API
- Optional Class
- Default and Static Interface Methods
- New Date and Time API
- CompletableFuture
- Base64 API
- Collection API enhancements

## 1. Lambda Expressions

Lambda expressions provide a concise way to implement a functional interface.

**Syntax:**

```java
(parameters) -> expression
```

**Example:**

```java
public class LambdaExample {
    public static void main(String[] args) {
        Runnable task = () ->
            System.out.println("Executing task");

        task.run();
    }
}
```

**Benefits:**
- Reduces boilerplate code.
- Supports functional programming.
- Works with functional interfaces.

## 2. Functional Interfaces

A functional interface contains exactly one abstract method. It can have multiple default and static methods.

The `@FunctionalInterface` annotation helps the compiler validate the interface.

```java
@FunctionalInterface
interface Calculator {
    int add(int a, int b);
}

public class FunctionalInterfaceExample {
    public static void main(String[] args) {
        Calculator calculator = (a, b) -> a + b;

        System.out.println(calculator.add(10, 20));
    }
}
```

**Output:**

```text
30
```

Common examples include `Runnable`, `Comparator`, `Predicate`, `Function`, `Consumer`, and `Supplier`.

## 3. Method References

Method references provide a shorter way to refer to an existing method using `::`.

**Example:**

```java
import java.util.Arrays;
import java.util.List;

public class MethodReferenceExample {
    public static void main(String[] args) {
        List<String> names =
            Arrays.asList("Arun", "Bala", "Chitra");

        names.forEach(System.out::println);
    }
}
```

### Types of Method References

1. Static method reference — `ClassName::staticMethod`
2. Instance method of a particular object — `object::instanceMethod`
3. Instance method of an arbitrary object — `ClassName::instanceMethod`
4. Constructor reference — `ClassName::new`

## 4. Stream API

The Stream API processes collections of data using operations such as filtering, mapping, sorting, and reducing.

**Example: Filter even numbers**

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class StreamExample {
    public static void main(String[] args) {
        List<Integer> numbers =
            Arrays.asList(1, 2, 3, 4, 5, 6);

        List<Integer> evenNumbers = numbers.stream()
            .filter(n -> n % 2 == 0)
            .collect(Collectors.toList());

        System.out.println(evenNumbers);
    }
}
```

**Output:**

```text
[2, 4, 6]
```

### Important Stream Operations

| Operation | Purpose |
|---|---|
| `filter()` | Select elements matching a condition |
| `map()` | Transform elements |
| `flatMap()` | Flatten nested streams |
| `sorted()` | Sort elements |
| `distinct()` | Remove duplicates |
| `limit()` | Limit the number of elements |
| `skip()` | Skip the first N elements |
| `reduce()` | Combine elements into one result |
| `collect()` | Accumulate results into a collection or another container |
| `count()` | Count elements |
| `findFirst()` | Return the first element, if present |
| `anyMatch()` | Check whether any element matches a condition |

### Intermediate vs Terminal Operations

**Intermediate operations:** `filter()`, `map()`, `sorted()`, `distinct()`

**Terminal operations:** `collect()`, `forEach()`, `count()`, `reduce()`

Intermediate operations are generally lazy and execute when a terminal operation triggers the stream pipeline.

## 5. forEach() Method

The `forEach()` method performs an action for each element.

```java
List<String> names =
    Arrays.asList("Java", "Spring", "Hibernate");

names.forEach(name -> System.out.println(name));
```

Using a method reference:

```java
names.forEach(System.out::println);
```

## 6. Optional Class

`Optional` represents a value that may or may not be present. It helps express potentially absent values and reduces some common null-handling errors.

```java
import java.util.Optional;

public class OptionalExample {
    public static void main(String[] args) {
        String name = null;

        String result = Optional.ofNullable(name)
            .orElse("Default Name");

        System.out.println(result);
    }
}
```

**Output:**

```text
Default Name
```

### Important Methods

- `Optional.of(value)` — creates an Optional for a non-null value.
- `Optional.ofNullable(value)` — supports a nullable value.
- `isPresent()` — checks whether a value exists.
- `ifPresent()` — executes an action when a value exists.
- `orElse()` — returns a fallback value when empty.
- `orElseGet()` — obtains a fallback value from a supplier when empty.
- `orElseThrow()` — returns the value or throws an exception.

## 7. Default and Static Methods in Interfaces

Java 8 allows interfaces to define default and static methods.

```java
interface Vehicle {
    default void start() {
        System.out.println("Vehicle started");
    }

    static void serviceInfo() {
        System.out.println("Vehicle service information");
    }
}

public class InterfaceExample implements Vehicle {
    public static void main(String[] args) {
        InterfaceExample vehicle = new InterfaceExample();

        vehicle.start();
        Vehicle.serviceInfo();
    }
}
```

**Key points:**
- Default methods can be inherited and overridden by implementing classes.
- Static interface methods are called using the interface name.
- These features helped evolve interfaces without forcing every existing implementation to add new methods.

## 8. Predefined Functional Interfaces

Java 8 provides reusable functional interfaces in `java.util.function`.

### Predicate<T>

Accepts a value and returns a boolean.

```java
Predicate<Integer> isEven = n -> n % 2 == 0;

System.out.println(isEven.test(10)); // true
```

### Function<T, R>

Accepts a value and returns a transformed result.

```java
Function<String, Integer> length = String::length;

System.out.println(length.apply("Java")); // 4
```

### Consumer<T>

Accepts a value and performs an action without returning a result.

```java
Consumer<String> printer = System.out::println;

printer.accept("Hello Java");
```

### Supplier<T>

Supplies a value without accepting an input.

```java
Supplier<Double> randomValue = Math::random;

System.out.println(randomValue.get());
```

### Other Important Interfaces

- `BiPredicate<T, U>` — accepts two inputs and returns a boolean.
- `BiFunction<T, U, R>` — accepts two inputs and returns a result.
- `BiConsumer<T, U>` — accepts two inputs and performs an action.
- `UnaryOperator<T>` — transforms a value into the same type.
- `BinaryOperator<T>` — combines two values of the same type into that type.

## 9. Collectors

Collectors are used with streams to accumulate or group results.

### Grouping By

```java
Map<Integer, List<String>> groupedNames =
    names.stream()
        .collect(Collectors.groupingBy(String::length));
```

### Counting Frequency

```java
Map<String, Long> frequency =
    names.stream()
        .collect(Collectors.groupingBy(
            name -> name,
            Collectors.counting()
        ));
```

### Joining Strings

```java
String result = names.stream()
    .collect(Collectors.joining(", "));

System.out.println(result);
```

Other useful collectors include `toList()`, `toSet()`, `partitioningBy()`, `mapping()`, `counting()`, and `summarizingInt()`.

## 10. Date and Time API

Java 8 introduced the `java.time` package to provide a modern date and time API.

```java
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.LocalTime;
import java.time.format.DateTimeFormatter;

public class DateTimeExample {
    public static void main(String[] args) {
        LocalDate date = LocalDate.now();
        LocalTime time = LocalTime.now();
        LocalDateTime dateTime = LocalDateTime.now();

        DateTimeFormatter formatter =
            DateTimeFormatter.ofPattern("dd-MM-yyyy");

        System.out.println(date.format(formatter));
        System.out.println(time);
        System.out.println(dateTime);
    }
}
```

### Important Classes

- `LocalDate` — date without a time zone.
- `LocalTime` — time without a date or time zone.
- `LocalDateTime` — date and time without a time zone.
- `ZonedDateTime` — date and time with a time zone.
- `Instant` — a point on the timeline.
- `Period` — date-based amount of time.
- `Duration` — time-based amount of time.
- `DateTimeFormatter` — formats and parses dates and times.

## 11. CompletableFuture

`CompletableFuture` supports asynchronous computations and combining dependent tasks.

```java
import java.util.concurrent.CompletableFuture;

public class CompletableFutureExample {
    public static void main(String[] args) {
        CompletableFuture<String> future =
            CompletableFuture.supplyAsync(() -> "Hello")
                .thenApply(message -> message + " Java 8");

        System.out.println(future.join());
    }
}
```

**Output:**

```text
Hello Java 8
```

Important methods include `supplyAsync()`, `runAsync()`, `thenApply()`, `thenCompose()`, `thenCombine()`, `exceptionally()`, and `allOf()`.

## 12. Base64 API

Java 8 introduced built-in Base64 encoding and decoding.

```java
import java.util.Base64;

public class Base64Example {
    public static void main(String[] args) {
        String input = "Java 8";

        String encoded = Base64.getEncoder()
            .encodeToString(input.getBytes());

        byte[] decodedBytes = Base64.getDecoder()
            .decode(encoded);

        System.out.println(encoded);
        System.out.println(new String(decodedBytes));
    }
}
```

**Note:** Base64 is an encoding mechanism, not encryption.

## 13. StringJoiner

`StringJoiner` joins multiple strings with a delimiter and optional prefix and suffix.

```java
import java.util.StringJoiner;

public class StringJoinerExample {
    public static void main(String[] args) {
        StringJoiner joiner =
            new StringJoiner(", ", "[", "]");

        joiner.add("Java");
        joiner.add("Spring Boot");
        joiner.add("PostgreSQL");

        System.out.println(joiner);
    }
}
```

**Output:**

```text
[Java, Spring Boot, PostgreSQL]
```

## 14. Parallel Streams

Parallel streams can process stream elements concurrently using multiple threads, commonly through the common ForkJoinPool.

```java
import java.util.Arrays;
import java.util.List;

public class ParallelStreamExample {
    public static void main(String[] args) {
        List<Integer> numbers =
            Arrays.asList(1, 2, 3, 4, 5);

        numbers.parallelStream()
            .forEach(System.out::println);
    }
}
```

**Important:** Output order is not guaranteed when using `forEach()` with a parallel stream. Parallel processing is not always faster; benchmark performance and consider thread safety, data size, and task cost.

## Interview Questions

1. What are the major features introduced in Java 8?
2. What is a lambda expression?
3. What is a functional interface?
4. What is the difference between `map()` and `flatMap()`?
5. What is the difference between intermediate and terminal operations?
6. What is the difference between `findFirst()` and `findAny()`?
7. What is the difference between `orElse()` and `orElseGet()`?
8. What is the difference between `Predicate`, `Function`, `Consumer`, and `Supplier`?
9. How does `Collectors.groupingBy()` work?
10. What is the difference between `Stream` and `parallelStream()`?
11. What is the difference between `thenApply()` and `thenCompose()`?
12. What are default methods in interfaces?
13. How does the Java 8 Date and Time API differ from `Date` and `Calendar`?
14. What is the difference between `reduce()` and `collect()`?
15. How can duplicate elements be identified using the Stream API?
16. How can we preserve insertion order while collecting stream results?
17. How can exceptions be handled in `CompletableFuture`?
18. Can a functional interface contain default and static methods?

## Practice Programs

- Find even and odd numbers using streams.
- Find duplicate elements in a list.
- Find the frequency of each character in a string.
- Find the first non-repeated character.
- Find the second-highest number in a list.
- Sort employees by salary and name.
- Group employees by department.
- Find the highest-paid employee in each department.
- Partition employees based on salary.
- Convert a list of objects into a map.
- Find the top three highest-paid employees.
- Flatten a list of lists using `flatMap()`.
- Find duplicate words in a sentence.
- Find the sum and average of numbers using streams.

## References

- [Oracle Java Tutorials](https://docs.oracle.com/javase/8/docs/)
- [Java 8 Stream API](https://docs.oracle.com/javase/8/docs/api/java/util/stream/package-summary.html)
- [Java 8 Functional Interfaces](https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html)
- [Java 8 Date and Time API](https://docs.oracle.com/javase/8/docs/api/java/time/package-summary.html)

---

**Author:** Saranya Sakthivel

**Technologies:** Java 8, Functional Programming, Stream API, Collections, Concurrency
