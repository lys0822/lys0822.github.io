---
title: IntelliJ에서 No beans of type found for Autowired repository 오류 해결하기
date: 2023-09-02 20:00:00 +0900
categories:
  - Spring
tags:
  - IntelliJ
---
## 오류 개요

IntelliJ IDEA에서 Spring 프로젝트를 작업할 때, `@Autowired` 어노테이션을 사용하여 의존성을 주입하려고 할 때가 있습니다. 그러나 가끔 이 과정에서 "No beans of type found for Autowired repository"라는 오류가 발생할 수 있습니다. 이 오류는 보통 스프링 빈(Bean)을 정상적으로 생성하지 못했을 때 나타납니다. 이 글에서는 이 문제를 어떻게 해결할 수 있는지에 대해 자세히 알아보겠습니다.

## 오류 원인 파악

이 오류가 나타나는 주요 원인은 다음과 같습니다:

1. **컴포넌트 스캔 범위**: 해당 클래스가 스프링의 컴포넌트 스캔 범위에 없을 경우
2. **어노테이션 누락**: `@Repository`, `@Service`, `@Controller` 등의 어노테이션이 빠져 있을 경우
3. **설정 파일 오류**: `applicationContext.xml` 또는 `application.properties` 파일에 오류가 있는 경우

## 해결 방법

### 컴포넌트 스캔 범위 조정

스프링 부트에서는 `@SpringBootApplication` 어노테이션이 있는 클래스가 컴포넌트 스캔의 시작점입니다. 이 클래스가 있는 패키지와 그 하위 패키지에 있는 빈들만 스캔합니다. 따라서 빈을 찾을 수 없는 문제가 생기면, 이 점을 확인해보세요.

### 필요한 어노테이션 추가

`@Repository`, `@Service`, `@Controller` 등의 어노테이션은 스프링이 빈을 생성할 때 참조하는 표시입니다. 이러한 어노테이션을 빠뜨렸다면, 해당 클래스에 적절한 어노테이션을 추가해주세요.

### 설정 파일 검토

`applicationContext.xml` 파일에서 `<context:component-scan>` 태그를 사용하여 스캔 범위를 지정할 수 있습니다. 이 설정이 올바른지 확인하세요. 또한, `application.properties` 파일에서도 빈 설정에 영향을 줄 수 있는 여러 설정값이 있으니 이 부분도 살펴보세요.

## 정리

IntelliJ에서 "No beans of type found for Autowired repository" 오류는 주로 스프링 빈 생성과 관련된 문제에서 발생합니다. 이를 해결하기 위해서는 컴포넌트 스캔 범위, 필요한 어노테이션, 설정 파일을 철저히 검토해야 합니다. 이러한 점들을 주의 깊게 살펴보면 대부분의 문제를 쉽게 해결할 수 있을 것입니다.