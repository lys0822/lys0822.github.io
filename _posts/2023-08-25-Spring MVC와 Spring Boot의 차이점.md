---
title: Spring MVC와 Spring Boot의 차이점
date: 2023-08-25 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringMVC
  - SpringBoot
---
## 서론

Spring MVC와 Spring Boot는 둘 다 자바 기반의 웹 애플리케이션 개발을 위한 프레임워크입니다. 하지만 이 둘은 다양한 면에서 차이가 있으며, 그 차이점을 이해하는 것이 중요합니다. 본 글에서는 이 두 프레임워크의 주요 차이점을 명확히 설명합니다.

## 설정의 복잡성

### Spring MVC
Spring MVC는 매우 유연하지만 설정이 복잡할 수 있습니다. 개발자는 XML 파일이나 Java 클래스를 사용해 수동으로 다양한 설정을 해야 합니다.

### Spring Boot
Spring Boot는 설정의 자동화가 장점입니다. 이 프레임워크는 'Convention over Configuration' 원칙을 따르며, 개발자가 따로 설정을 하지 않아도 자동으로 최적의 설정을 적용합니다.

## 프로젝트 구조

### Spring MVC
Spring MVC 프로젝트의 구조는 개발자가 직접 설정해야 합니다. 따라서 프로젝트의 구조는 개발자의 의도와 요구사항에 따라 달라질 수 있습니다.

### Spring Boot
Spring Boot는 일반적으로 일정한 프로젝트 구조를 제공합니다. 이러한 구조는 Spring Boot의 시작 페이지에서 제공되는 초기 설정을 통해 자동으로 생성됩니다.

## 의존성 관리

### Spring MVC
Spring MVC에서는 개발자가 필요한 라이브러리와 의존성을 직접 관리해야 합니다.

### Spring Boot
Spring Boot는 의존성 관리를 자동으로 해줍니다. 즉, `pom.xml` 파일에서 몇 가지 설정만으로 여러 라이브러리와 플러그인을 쉽게 추가할 수 있습니다.

## 내장 서버

### Spring MVC
Spring MVC에서는 내장 서버 기능이 없습니다. 별도의 웹 서버(Tomcat, Jetty 등)에 배포해야 합니다.

### Spring Boot
Spring Boot는 내장 Tomcat 서버를 제공합니다. 이로 인해 개발자는 웹 애플리케이션을 더 쉽게 실행하고 테스트할 수 있습니다.

## 결론

Spring MVC와 Spring Boot는 각각의 장단점과 사용 케이스가 있습니다. Spring MVC는 더 많은 유연성을 제공하지만, 설정이 복잡할 수 있습니다. 반면 Spring Boot는 빠르게 개발을 시작할 수 있게 해주지만, 일부 상세 설정은 제한될 수 있습니다. 이 두 프레임워크의 차이를 이해하고 자신의 프로젝트에 가장 적합한 것을 선택하는 것이 중요합니다.