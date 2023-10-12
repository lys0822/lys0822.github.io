---
title: Spring에서 ResponseEntity와 @RestController의 사용 시기
date: 2023-09-24 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - ResponseEntity
  - RestController
---
## ResponseEntity와 @RestController란 무엇인가?

`ResponseEntity`는 Spring Framework에서 HTTP 응답을 나타내는 클래스입니다. HTTP 상태 코드, 헤더, 본문 등을 모두 포함할 수 있습니다. 반면에 `@RestController`는 Spring MVC에서 RESTful 웹 서비스를 생성하기 위한 클래스 레벨의 어노테이션입니다. 이 어노테이션은 `@ResponseBody`와 `@Controller`를 결합한 것으로, 반환된 객체는 HTTP 응답 본문으로 자동 변환됩니다.

## ResponseEntity 사용의 장점

`ResponseEntity`를 사용하면 HTTP 상태 코드를 명시적으로 제어할 수 있습니다. 또한, 추가적인 HTTP 헤더를 설정하는 등 응답을 상세하게 조작할 수 있습니다. 예를 들어, 특정 조건에 따라 다른 상태 코드를 반환해야 할 때 유용합니다.

```java
public ResponseEntity<String> someMethod() {
    // 로직 수행
    return new ResponseEntity<>("Success", HttpStatus.OK);
}
```

## @RestController 사용의 장점

`@RestController`는 간결한 코드 작성을 가능하게 합니다. HTTP 상태 코드와 같은 추가 정보 없이도, 단순히 객체를 반환하면 JSON으로 자동 변환되어 응답됩니다. 일반적인 CRUD(Create, Read, Update, Delete) 작업에 적합하다고 할 수 있습니다.

```java
@RestController
public class SomeController {
    public String someMethod() {
        // 로직 수행
        return "Success";
    }
}
```

## 언제 어떤 것을 사용해야 하는가?

1. **단순한 응답이 필요한 경우**: `@RestController`를 사용하세요. 이는 코드를 간결하게 유지하며, 일반적인 웹 서비스에 적합합니다.
2. **응답을 상세하게 제어해야 하는 경우**: `ResponseEntity`를 사용하세요. HTTP 상태 코드, 헤더 등을 상세히 설정할 수 있습니다.

## 정리

`ResponseEntity`와 `@RestController` 각각은 특별한 케이스에 더 적합할 수 있습니다. 복잡한 로직 또는 HTTP 응답을 상세하게 제어해야 하는 상황에서는 `ResponseEntity`가 유용하며, 일반적인 RESTful 서비스에서는 `@RestController`가 더 적합합니다. 두 가지 방법을 적절히 혼합하여 사용하는 것도 가능합니다.