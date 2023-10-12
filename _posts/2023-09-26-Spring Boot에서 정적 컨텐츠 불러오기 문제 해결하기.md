---
title: Spring Boot에서 정적 컨텐츠 불러오기 문제 해결하기
date: 2023-09-26 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
---
## 문제 상황 및 대응 전략

Spring Boot에서는 웹 애플리케이션을 개발할 때 종종 HTML, CSS, JavaScript와 같은 정적 컨텐츠를 불러오는 작업이 필요합니다. 그러나 개발자들이 `Spring Boot not serving static content`라는 에러에 직면하는 경우가 있습니다. 이 문제는 보통 Spring Boot 프로젝트 구조나 설정에서 발생합니다.

## 원인과 해결 방법 1: 디렉토리 구조

Spring Boot에서는 `/src/main/resources/static` 디렉토리를 기본으로 정적 파일을 찾습니다. 따라서 이 경로에 파일이 올바르게 위치해 있는지 확인해야 합니다. 만약 파일이 다른 위치에 있다면, 정적 파일을 올바른 디렉토리로 옮기세요.

## 원인과 해결 방법 2: 의존성 문제

프로젝트의 `pom.xml` 파일이나 `build.gradle` 파일에서 웹 관련 의존성이 올바르게 설정되어 있는지 확인하세요. 예를 들어, Spring Boot Starter Web을 추가해야 할 수 있습니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

## 원인과 해결 방법 3: 캐시 및 브라우저 이슈

웹 브라우저의 캐시 문제로 인해 새로운 정적 파일이 로드되지 않을 수 있습니다. 이 경우, 브라우저의 캐시를 지우고 다시 시도하세요.

## 원인과 해결 방법 4: 스프링 부트 설정

`application.properties` 또는 `application.yml` 파일에서 정적 리소스 관련 설정을 확인하세요. 예를 들어, `spring.resources.static-locations`를 사용하여 정적 리소스의 위치를 지정할 수 있습니다.

```properties
spring.resources.static-locations=classpath:/custom/
```

## 에러 코드 분석: `Spring Boot not serving static content`

이 에러 메시지는 Spring Boot가 정적 컨텐츠를 올바르게 불러오지 못했을 때 나타납니다. 이 문제를 해결하기 위해 위의 방법을 순차적으로 적용해보세요.

## 요약

Spring Boot에서 정적 컨텐츠를 불러오지 못하는 문제는 다양한 원인에 기인할 수 있습니다. 디렉토리 구조, 의존성 설정, 캐시 및 브라우저 이슈, 그리고 Spring Boot의 설정을 체크하여 문제를 해결할 수 있습니다.