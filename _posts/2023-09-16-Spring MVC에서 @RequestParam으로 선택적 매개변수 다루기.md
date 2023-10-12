---
title: Spring MVC에서 @RequestParam으로 선택적 매개변수 다루기
date: 2023-09-16 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringMVC
  - RequestParam
---
## @RequestParam의 기본 사용법

Spring MVC에서는 컨트롤러 메서드의 매개변수로 클라이언트로부터 전달된 데이터를 수집할 수 있습니다. 이 때 자주 사용되는 어노테이션(annotation)이 `@RequestParam`입니다. `@RequestParam`을 사용하면 HTTP 요청의 쿼리 문자열이나 폼 데이터에서 값을 가져와 메서드 매개변수에 바인딩할 수 있습니다. 

```java
@RequestMapping("/greeting")
public String greeting(@RequestParam String name) {
    return "Hello, " + name + "!";
}
```

위 코드는 `name` 이라는 키로 전달된 값을 가져와서 인사 메시지를 생성합니다.

## 선택적 매개변수 설정하기

필수 매개변수가 아닌 선택적 매개변수를 다룰 때도 `@RequestParam`을 사용할 수 있습니다. 이때 `required` 속성을 `false`로 설정하면 됩니다. 또한 `defaultValue` 속성을 사용하면 매개변수가 전달되지 않았을 때 기본 값을 설정할 수 있습니다.

```java
@RequestMapping("/greeting")
public String greeting(@RequestParam(required=false, defaultValue="World") String name) {
    return "Hello, " + name + "!";
}
```

이 코드에서는 `name` 매개변수가 선택적입니다. 값이 전달되지 않으면 "World"가 기본값으로 사용됩니다.

## 에러 상황과 해결책

`@RequestParam`을 사용하면서 자주 발생하는 에러는 `MissingServletRequestParameterException` 입니다. 이 에러는 필수 매개변수가 전달되지 않았을 때 발생합니다. 이를 해결하기 위해서는 `required` 속성을 `false`로 설정하거나, `defaultValue`를 지정해줄 수 있습니다.

## 정리

Spring MVC에서 `@RequestParam`을 통해 선택적 매개변수를 쉽게 다룰 수 있습니다. 필수가 아닌 매개변수를 사용할 때에는 `required=false` 설정을 통해 더 유연한 코드를 작성할 수 있으며, `defaultValue`를 통해 안전한 기본 값을 설정할 수 있습니다. 이렇게 하면 사용자로부터 다양한 입력을 쉽고 안전하게 처리할 수 있습니다.