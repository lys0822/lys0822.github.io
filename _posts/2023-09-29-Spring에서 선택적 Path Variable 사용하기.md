---
title: Spring에서 선택적 Path Variable 사용하기
date: 2023-09-29 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - PathVariable
---
## 소개
Spring Framework는 웹 개발에서 널리 사용되는 자바 프레임워크입니다. 본 글에서는 Spring의 @PathVariable 어노테이션을 사용해 선택적으로 경로 변수를 설정하는 방법에 대해 설명합니다.

## 기본적인 @PathVariable 사용법
Spring에서는 @PathVariable 어노테이션을 사용해 URL 경로의 일부를 메소드 매개변수로 쉽게 가져올 수 있습니다. 예를 들어, 아래와 같은 코드가 있을 경우:

```java
@RequestMapping("/greet/{name}")
public String greeting(@PathVariable String name) {
    return "Hello, " + name;
}
```

"/greet/John" URL에 대한 요청은 "Hello, John"을 반환합니다.

## 선택적 Path Variable 구현 방법
때로는 경로 변수가 선택적이어야 할 필요가 있습니다. 즉, URL에 경로 변수가 포함되지 않아도 코드가 실행되어야 합니다. 이를 위해 `@RequestMapping`과 `@PathVariable`의 속성을 적절히 조합하여 사용할 수 있습니다.

### 방법 1: 별도의 메소드 사용
두 개의 별도의 메소드를 정의하여 하나는 경로 변수를 포함하고, 하나는 포함하지 않습니다.

```java
@RequestMapping("/greet/{name}")
public String greetingWithVariable(@PathVariable String name) {
    return "Hello, " + name;
}

@RequestMapping("/greet/")
public String greetingWithoutVariable() {
    return "Hello, World";
}
```

### 방법 2: Optional 사용
Java 8 이상에서는 `Optional`을 사용해 선택적 경로 변수를 다룰 수 있습니다.

```java
@RequestMapping("/greet/{name}")
public String greeting(@PathVariable Optional<String> name) {
    return name.map(n -> "Hello, " + n).orElse("Hello, World");
}
```

## 주의사항
Optional을 사용할 경우, URL에서 경로 변수를 생략하면 `Optional.empty()`가 됩니다. 이를 처리하지 않으면 오류가 발생할 수 있으므로 주의해야 합니다.

## 정리
Spring Framework에서는 `@PathVariable` 어노테이션을 통해 URL 경로의 일부를 메소드 매개변수로 가져올 수 있습니다. 이때, 선택적으로 경로 변수를 다루기 위해서는 별도의 메소드를 사용하거나 Java의 `Optional`을 활용할 수 있습니다.