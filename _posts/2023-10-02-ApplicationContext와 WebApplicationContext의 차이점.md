---
title: ApplicationContext와 WebApplicationContext의 차이점
date: 2023-10-02 20:00:00 +0900
categories:
  - Spring
tags:
  - ApplicationContext
  - WebApplicationContext
---
## 서론
Spring Framework에서는 ApplicationContext와 WebApplicationContext라는 두 가지 중요한 컨테이너가 있습니다. 이 둘은 비슷해 보이지만 실제로는 목적과 활용도가 다릅니다. 이 글에서는 이 두 개념의 차이점을 자세히 알아보겠습니다.

## ApplicationContext의 역할
ApplicationContext는 Spring Framework의 핵심 컨테이너 중 하나로, 빈(Bean)의 생명 주기를 관리하고, 의존성 주입(Dependency Injection)을 처리합니다. 빈은 Spring에서 관리하는 객체를 의미하며, 의존성 주입은 필요한 객체를 자동으로 연결해 주는 것을 말합니다. ApplicationContext는 일반적인 자바 애플리케이션 또는 배치 프로세스, 데스크톱 애플리케이션에서도 사용될 수 있습니다.

## WebApplicationContext의 특징
WebApplicationContext는 ApplicationContext를 상속받아 웹 애플리케이션에서 필요한 기능을 추가로 제공합니다. 이 컨테이너는 웹 애플리케이션의 실행 환경을 고려하여, 서블릿(Servlet)과 같은 웹 관련 구성요소를 관리합니다. 즉, 웹 환경에서만 활용되는 빈들을 관리하고 있습니다.

## 둘 사이의 주요 차이점
ApplicationContext는 웹 환경과 무관하게 다양한 종류의 애플리케이션에서 사용되는 반면, WebApplicationContext는 웹 애플리케이션에 특화되어 있습니다. WebApplicationContext는 ServletContext에 접근할 수 있어 웹 애플리케이션의 환경 정보를 쉽게 얻을 수 있습니다.

또한, ApplicationContext는 단일 인스턴스만 생성할 수 있지만, WebApplicationContext는 각 웹 애플리케이션 별로 여러 인스턴스를 생성할 수 있습니다. 이로 인해 각 웹 애플리케이션은 독립적인 설정과 빈을 가질 수 있습니다.

## 정리
ApplicationContext와 WebApplicationContext는 Spring Framework에서 중요한 역할을 하는 컨테이너입니다. 둘은 유사하게 보일 수 있지만, ApplicationContext는 다양한 환경에서, WebApplicationContext는 웹 환경에서 사용되며, 웹 애플리케이션에 필요한 추가적인 기능을 제공합니다. 이를 이해하면 Spring Framework를 더 효과적으로 활용할 수 있습니다.