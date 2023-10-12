---
title: Spring MVC에서 모든 요청 매개변수를 Map으로 얻는 방법
date: 2023-09-18 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringMVC
  - 매개변수
  - Map
---
## 개요

Spring MVC에서는 컨트롤러에서 HTTP 요청의 모든 매개변수를 쉽게 가져올 수 있습니다. 이 글에서는 그 과정을 자세하게 설명합니다. 'HTTP 요청'이란 사용자가 웹 페이지에 접속할 때 서버에 보내는 정보입니다. '매개변수'란 이 정보 중에서 특별한 데이터를 의미합니다.

## `@RequestParam` 애너테이션 사용

Spring에서 가장 간단한 방법은 `@RequestParam` 애너테이션을 사용하는 것입니다. 이 애너테이션은 컨트롤러 메서드의 매개변수 앞에 붙여 사용됩니다.

```java
@RequestMapping("/somePath")
public String someMethod(@RequestParam Map<String, String> allParams) {
    // 코드 구현
}
```

`@RequestParam` 애너테이션을 `Map`과 함께 사용하면, 모든 요청 매개변수가 이 `Map`에 저장됩니다.

## `HttpServletRequest` 객체 사용

또 다른 방법은 `HttpServletRequest` 객체를 직접 사용하는 것입니다.

```java
@RequestMapping("/anotherPath")
public String anotherMethod(HttpServletRequest request) {
    Map<String, String[]> allParams = request.getParameterMap();
    // 코드 구현
}
```

`HttpServletRequest` 객체에서 `getParameterMap` 메서드를 호출하면, 매개변수가 `Map` 형태로 반환됩니다. 단, 값은 문자열 배열(`String[]`) 형태로 반환됩니다.

## 주의사항

- `@RequestParam`은 요청 매개변수가 없을 경우 `400 Bad Request` 오류를 발생시킵니다. 이를 피하려면 `required=false` 옵션을 설정할 수 있습니다.
- `HttpServletRequest`를 사용하면, 옵셔널한 매개변수를 처리하기 더 유연할 수 있습니다.

## 결론

Spring MVC에서는 여러 방법으로 HTTP 요청의 모든 매개변수를 쉽게 가져올 수 있습니다. 개발자의 요구에 따라 `@RequestParam` 애너테이션을 사용하거나 `HttpServletRequest` 객체를 직접 사용할 수 있습니다.