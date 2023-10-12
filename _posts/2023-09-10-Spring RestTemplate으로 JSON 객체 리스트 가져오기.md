---
title: Spring RestTemplate으로 JSON 객체 리스트 가져오기
date: 2023-09-10 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - RestTemplate
  - JSON
---
## 문제 상황 설명

Spring Framework에서 RestTemplate을 사용해 외부 API로부터 JSON 객체의 리스트를 가져오고 싶다는 것이 문제입니다. 특히, Stack Overflow에서 제기된 이 문제는 `RestTemplate` 객체의 `exchange` 메소드를 사용하려는 것과 관련이 있습니다.

## 에러 메시지

에러 메시지는 보통 "Could not extract response: no suitable HttpMessageConverter found for response type [...]" 등으로 나타납니다.

## 해결 방법

### 자바 타입으로 매핑

RestTemplate의 `exchange` 메소드를 사용할 때, 응답을 매핑할 자바 타입을 지정해야 합니다. 이것은 제네릭을 사용하여 수행됩니다. 예를 들어, 반환될 객체가 `List<User>` 타입이라면, 다음과 같이 코드를 작성할 수 있습니다.

```java
ParameterizedTypeReference<List<User>> typeRef = new ParameterizedTypeReference<List<User>>() {};
ResponseEntity<List<User>> response = restTemplate.exchange(url, HttpMethod.GET, null, typeRef);
List<User> users = response.getBody();
```

### 헤더 설정

필요한 경우, 헤더를 설정할 수 있습니다. 대표적인 예는 `Accept` 헤더입니다.

```java
HttpHeaders headers = new HttpHeaders();
headers.setAccept(Collections.singletonList(MediaType.APPLICATION_JSON));
HttpEntity<String> entity = new HttpEntity<>("parameters", headers);
```

이 헤더를 `exchange` 메소드의 매개변수로 전달할 수 있습니다.

### 주의사항

- `exchange` 메소드는 네트워크 통신을 수행하므로 예외 처리가 필요합니다.
- 매핑할 타입이 복잡한 경우, 커스텀 `HttpMessageConverter`를 등록할 수 있습니다.

## 결론

Spring의 `RestTemplate`을 사용하여 JSON 객체 리스트를 가져오는 것은 매우 편리합니다. 단지 반환될 객체의 타입을 정확히 지정하고 필요한 헤더를 설정하는 것이 중요합니다. 이렇게 해서 문제를 해결할 수 있을 것입니다.