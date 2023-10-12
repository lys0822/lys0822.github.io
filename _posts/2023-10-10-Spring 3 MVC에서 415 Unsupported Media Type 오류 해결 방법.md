---
title: Spring 3 MVC에서 415 Unsupported Media Type 오류 해결 방법
date: 2023-10-10 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring3MVC
---
## 오류 개요

Spring 3 MVC에서 RESTful API를 구현하다 보면, 클라이언트로부터 JSON 데이터를 받을 때 "415 Unsupported Media Type"이라는 오류에 직면할 수 있습니다. 이 문제는 서버가 클라이언트로부터 보내진 요청의 '미디어 타입'을 지원하지 않을 때 발생합니다.

## 오류 원인과 해결 방안

### 원인 1: `@RequestBody` 어노테이션 누락

`@RequestBody` 어노테이션은 메서드의 파라미터가 HTTP 요청의 본문(body)으로부터 값을 읽어야 함을 명시합니다. 이 어노테이션이 누락되면, 스프링은 클라이언트의 요청을 제대로 처리할 수 없어 "415 Unsupported Media Type" 오류를 반환합니다.

#### 해결 방안

컨트롤러 메서드의 파라미터에 `@RequestBody` 어노테이션을 추가합니다.

```java
@RequestMapping(value = "/someEndpoint", method = RequestMethod.POST)
public ResponseEntity<String> someMethod(@RequestBody SomeClass someObject) {
  // 로직 구현
}
```

### 원인 2: `Content-Type` 헤더 누락 또는 잘못 설정

HTTP 요청에서 `Content-Type` 헤더는 요청 본문의 미디어 타입을 명시합니다. 이 헤더가 누락되거나 잘못 설정되면, 서버는 어떻게 요청을 처리해야 할지 알 수 없어 해당 오류를 반환할 수 있습니다.

#### 해결 방안

HTTP 요청에서 `Content-Type` 헤더를 `application/json`으로 명시적으로 설정합니다.

```http
POST /someEndpoint HTTP/1.1
Host: example.com
Content-Type: application/json
```

## 프로그래밍 언어 라이브러리의 활용

Java, Python, JavaScript 등 다양한 프로그래밍 언어에서 HTTP 요청을 보낼 때, 해당 언어의 라이브러리를 활용하여 `Content-Type` 헤더와 `@RequestBody`를 올바르게 설정할 수 있습니다. 이렇게 하면 "415 Unsupported Media Type" 오류를 피할 수 있습니다.

## 요약

"415 Unsupported Media Type" 오류는 주로 두 가지 원인으로 발생합니다. 첫째는 `@RequestBody` 어노테이션의 누락, 둘째는 `Content-Type` 헤더의 누락 또는 잘못된 설정입니다. 이 두 가지 원인을 정확히 파악하고 해결 방안을 적용하면, 이 오류를 성공적으로 해결할 수 있습니다.