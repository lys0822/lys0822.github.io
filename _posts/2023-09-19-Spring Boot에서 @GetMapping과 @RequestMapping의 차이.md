---
title: Spring Boot에서 @GetMapping과 @RequestMapping의 차이
date: 2023-09-19 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
  - GetMapping
  - RequestMapping
---
## 개요

Spring Boot에서 웹 요청을 처리할 때 자주 사용되는 애너테이션에는 `@GetMapping`과 `@RequestMapping`이 있습니다. 이 두 애너테이션은 비슷해 보이지만 몇 가지 중요한 차이점이 있습니다. 이 글에서는 이 두 애너테이션의 차이점을 자세하게 알아보겠습니다.

## @GetMapping 애너테이션

`@GetMapping`은 HTTP GET 요청을 처리하는 메서드에 사용됩니다. 이 애너테이션은 Spring 4.3 이상에서 제공되며, 주로 조회 작업에 사용됩니다.

### 특징

1. 코드가 간결하다.
2. GET 방식만 지원한다.
3. URL 패턴과 함께 추가적인 설정을 쉽게 할 수 있다.

### 예시 코드

```java
@GetMapping("/hello")
public String sayHello() {
  return "Hello, World!";
}
```

## @RequestMapping 애너테이션

`@RequestMapping`은 HTTP 요청을 처리하는 메서드에 사용됩니다. 여기서 중요한 것은 **모든** HTTP 메서드(GET, POST, PUT, DELETE 등)를 지원한다는 점입니다.

### 특징

1. 다양한 설정 옵션을 제공한다.
2. 모든 HTTP 메서드를 지원한다.
3. `method` 속성을 사용하여 특정 HTTP 메서드로 제한할 수 있다.

### 예시 코드

```java
@RequestMapping(value = "/hello", method = RequestMethod.GET)
public String sayHello() {
  return "Hello, World!";
}
```

## 주요 차이점

1. **지원하는 HTTP 메서드**: `@GetMapping`은 GET 메서드만 지원하는 반면, `@RequestMapping`은 모든 HTTP 메서드를 지원합니다.
2. **코드 간결성**: `@GetMapping`은 코드가 더 간결하고 직관적입니다.
3. **버전**: `@GetMapping`은 Spring 4.3 이상에서만 사용할 수 있습니다.

## 결론

두 애너테이션 모두 웹 요청을 처리하는 데 유용하지만, 사용 사례와 필요한 기능에 따라 적절한 애너테이션을 선택해야 합니다. `@GetMapping`은 간단하고 명확한 GET 요청에 적합하며, `@RequestMapping`은 다양한 설정과 HTTP 메서드를 지원해야 할 때 유용합니다.