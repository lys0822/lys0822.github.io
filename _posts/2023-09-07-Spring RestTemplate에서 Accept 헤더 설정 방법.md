---
title: Spring RestTemplate에서 Accept 헤더 설정 방법
date: 2023-09-07 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - RestTemplate
---
## Accept 헤더란 무엇인가?

Accept 헤더는 HTTP 요청에서 클라이언트가 원하는 응답의 컨텐츠 유형을 서버에 알려주는 역할을 합니다. 예를 들어, 클라이언트가 JSON 형식의 데이터를 원한다면, Accept 헤더에 `application/json`을 명시할 수 있습니다.

## Spring의 RestTemplate에서 Accept 헤더 설정하는 방법

### HttpHeaders 클래스 사용

Java의 Spring 프레임워크에서는 `HttpHeaders` 클래스를 사용하여 HTTP 헤더를 설정할 수 있습니다. 이 클래스를 이용하면 Accept 헤더뿐만 아니라 다양한 HTTP 헤더를 쉽게 설정할 수 있습니다.

```java
HttpHeaders headers = new HttpHeaders();
headers.setAccept(Arrays.asList(MediaType.APPLICATION_JSON));
HttpEntity<String> entity = new HttpEntity<>("parameters", headers);

RestTemplate restTemplate = new RestTemplate();
ResponseEntity<String> response = restTemplate.exchange(url, HttpMethod.GET, entity, String.class);
```

### exchange 메소드 활용

`RestTemplate`의 `exchange` 메소드를 사용하면 HTTP 메소드와 헤더, 요청 본문 등을 상세히 설정할 수 있습니다. 이 메소드는 매우 유연해서 다양한 상황에서 활용 가능합니다.

### getForEntity 메소드를 이용한 간단한 방법

만약 GET 요청만을 보낼 예정이라면, `getForEntity` 메소드를 사용하는 것이 더 간단할 수 있습니다. 하지만 이 방법은 Accept 헤더 외의 다른 헤더를 설정할 수 없으므로, 상황에 따라 선택이 필요합니다.

```java
RestTemplate restTemplate = new RestTemplate();
ResponseEntity<String> response = restTemplate.getForEntity(url, String.class, headers);
```

## 주의사항

- `MediaType`은 데이터 유형을 나타내는 열거형(enum)입니다. 이를 통해 헤더에 들어갈 값들을 미리 정의해놓은 상수로 쉽게 사용할 수 있습니다.
- `HttpEntity` 클래스는 HTTP 요청 또는 응답에 대한 헤더와 본문을 캡슐화(encapsulation)합니다. 캡슐화란 데이터와 데이터를 처리하는 메소드를 하나로 묶는 것을 의미합니다.
  
이렇게 Spring의 RestTemplate를 사용하여 Accept 헤더를 설정할 수 있습니다. 이를 통해 서버와 더 정확하게 커뮤니케이션을 할 수 있게 됩니다.