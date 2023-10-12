---
title: Spring Boot에서 Not a Managed Type 오류 해결 방법
date: 2023-09-05 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot오류
---
## 오류 상황 및 원인

Spring Boot 프로젝트를 진행하다가 "Not a Managed Type" 이라는 오류가 발생할 경우가 있습니다. 이 오류는 주로 JPA(Entity 클래스와 Repository 인터페이스 사용시)에서 나타나곤 합니다. 'Managed Type'이라는 것은 JPA가 관리하는 객체, 즉 `@Entity` 어노테이션을 가진 클래스를 의미합니다. 이 오류가 발생하는 주된 원인은 Spring Boot가 JPA 엔터티를 제대로 인식하지 못하기 때문입니다.

## 해결 방법 1: 패키지 구조 확인

첫 번째로 확인해야 할 것은 패키지 구조입니다. `@SpringBootApplication` 어노테이션이 있는 클래스는 엔터티와 리포지토리가 있는 패키지와 같거나 그 상위에 위치해야 합니다. 예를 들어, `@SpringBootApplication`이 `com.example`에 위치한다면, 엔터티 클래스와 리포지토리 인터페이스는 `com.example` 혹은 `com.example.[하위패키지]`에 위치해야 합니다.

## 해결 방법 2: 어노테이션 확인

두 번째로 확인할 사항은 클래스에 적용된 어노테이션입니다. Entity 클래스 위에는 반드시 `@Entity` 어노테이션이 있어야 합니다. 또한, Repository 인터페이스 위에는 `@Repository` 어노테이션이 있어야 할 수도 있습니다.

## 해결 방법 3: 의존성 확인

세 번째로 확인해야 할 것은 Maven이나 Gradle 설정입니다. `pom.xml` 또는 `build.gradle` 파일에 Spring Data JPA 관련 의존성이 제대로 추가되어 있는지 확인하세요. 다음과 같은 코드가 있어야 합니다.

- Maven: `spring-boot-starter-data-jpa`
- Gradle: `implementation 'org.springframework.boot:spring-boot-starter-data-jpa'`

이 세 가지 해결 방법을 적용하면 대부분의 "Not a Managed Type" 오류를 해결할 수 있습니다. 이 외에도 문제가 계속된다면, IDE 재시작 혹은 빌드 캐시 삭제를 시도해보는 것도 좋습니다.