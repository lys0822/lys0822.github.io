---
title: 스프링 부트 Unable to find a @SpringBootConfiguration오류 해결 방법
date: 2023-09-13 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
---
## 문제 상황 및 원인

스프링 부트(Spring Boot)를 사용하다가 JPA 테스트를 실행할 때 `Unable to find a @SpringBootConfiguration`라는 오류 메시지가 나타난 경우, 이는 일반적으로 스프링 부트 설정 클래스를 찾을 수 없다는 것을 의미합니다. 스프링 부트 설정 클래스는 `@SpringBootConfiguration` 또는 `@SpringBootApplication` 어노테이션을 포함해야 합니다. 이러한 오류는 주로 테스트 클래스의 위치나 패키지 구조, 그리고 어노테이션의 사용에 문제가 있을 때 발생합니다.

## 해결책 1: 패키지 구조 확인

테스트 클래스는 메인 어플리케이션 클래스가 위치한 패키지 또는 그 하위 패키지에 위치해야 합니다. 이는 스프링 부트가 자동으로 설정 클래스를 찾을 수 있도록 도와줍니다. 만약 테스트 클래스가 메인 어플리케이션 클래스와 같은 패키지에 있지 않다면, 이를 같은 패키지 또는 하위 패키지로 이동시키세요.

## 해결책 2: 어노테이션 사용 확인

테스트 클래스에 `@SpringBootTest` 어노테이션을 붙여야 합니다. 이 어노테이션은 스프링 부트 테스트에 필요한 거의 모든 설정을 자동으로 로드합니다. 또한, `@AutoConfigureDataJpa` 어노테이션을 추가하여 JPA 관련 설정을 자동으로 로드할 수 있습니다.

```java
@SpringBootTest
@AutoConfigureDataJpa
class YourTestClass {
  // ...
}
```

## 해결책 3: 명시적 설정 클래스 지정

위의 방법들로 문제가 해결되지 않는 경우, `@ContextConfiguration` 어노테이션을 사용하여 설정 클래스를 명시적으로 지정할 수 있습니다.

```java
@SpringBootTest
@ContextConfiguration(classes = YourApp.class)
class YourTestClass {
  // ...
}
```

여기에서 `YourApp`은 메인 어플리케이션 클래스입니다. 이 클래스에는 `@SpringBootApplication` 또는 `@SpringBootConfiguration` 어노테이션을 포함해야 합니다.

## 요약

`Unable to find a @SpringBootConfiguration` 오류는 스프링 부트 설정 클래스를 찾을 수 없을 때 발생합니다. 이를 해결하기 위해서는 패키지 구조를 확인하고, 필요한 어노테이션을 올바르게 사용하거나, 설정 클래스를 명시적으로 지정해야 합니다. 이러한 방법들을 적용하면 대부분의 문제가 해결될 것입니다.