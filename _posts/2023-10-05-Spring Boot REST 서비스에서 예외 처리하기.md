---
title: Spring Boot REST 서비스에서 예외 처리하기
date: 2023-10-05 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
  - REST
---
## 예외 처리란 무엇인가?
예외 처리는 프로그램에서 문제가 발생했을 때, 그 문제를 적절하게 다루는 방법입니다. 이는 사용자에게 친절한 메시지를 제공하거나, 오류를 로그에 기록하는 등의 작업을 포함할 수 있습니다. Spring Boot에서 REST 서비스를 구현할 때도 예외 처리는 중요한 부분입니다.

## `ControllerAdvice` 클래스 사용하기
Spring Boot에서는 `@ControllerAdvice` 어노테이션을 사용하여 전역 예외 처리를 할 수 있습니다. 이 클래스는 애플리케이션의 모든 컨트롤러에서 발생하는 예외를 한 곳에서 처리합니다.

```java
@ControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(value = Exception.class)
    public ResponseEntity<Object> handleException(Exception e) {
        return new ResponseEntity<>("오류가 발생했습니다.", HttpStatus.INTERNAL_SERVER_ERROR);
    }
}
```

## `ExceptionHandler` 메서드를 컨트롤러에 추가하기
특정 컨트롤러에서만 발생하는 예외를 처리하려면 `@ExceptionHandler` 어노테이션을 사용하여 그 컨트롤러 내에 메서드를 추가할 수 있습니다.

```java
@RestController
public class MyController {
    @ExceptionHandler(value = MyException.class)
    public ResponseEntity<Object> handleMyException(MyException e) {
        return new ResponseEntity<>("MyException이 발생했습니다.", HttpStatus.BAD_REQUEST);
    }
}
```

## `ResponseStatusException` 사용하기
`ResponseStatusException`은 상태 코드와 오류 메시지를 함께 반환할 수 있는 예외 클래스입니다. 이를 사용하면 간단한 예외 처리가 가능합니다.

```java
@GetMapping("/some-endpoint")
public String someEndpoint() {
    throw new ResponseStatusException(HttpStatus.NOT_FOUND, "이 리소스는 존재하지 않습니다.");
}
```

## 정리
Spring Boot에서는 여러 가지 방법으로 REST 서비스의 예외를 처리할 수 있습니다. `ControllerAdvice` 클래스를 사용하면 전역 예외 처리가 가능하고, `ExceptionHandler` 메서드를 통해 특정 컨트롤러에서 예외를 처리할 수 있습니다. 또한, `ResponseStatusException`을 사용하면 더 간단하게 예외를 처리할 수 있습니다. 이러한 방법들을 적절히 활용하여 사용자에게 더 나은 서비스를 제공해보세요.