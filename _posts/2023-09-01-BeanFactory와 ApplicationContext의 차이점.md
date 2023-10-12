---
title: BeanFactory와 ApplicationContext의 차이점
date: 2023-09-01 20:00:00 +0900
categories:
  - Spring
tags:
  - BeanFactory
  - ApplicationContext
---
## 무엇이 Spring Framework인가?

Spring Framework는 Java 언어를 위한 다양한 기능을 제공하는 프레임워크입니다. 이 프레임워크에서는 빈(Bean)이라 불리는 객체를 생성하고 관리해주는 컨테이너가 존재합니다. 이러한 컨테이너는 크게 `BeanFactory`와 `ApplicationContext`로 나뉩니다. 두 컨테이너가 어떻게 다른지, 각각 어떤 상황에서 사용하는 것이 좋은지에 대해 알아보겠습니다.

## BeanFactory: 기본적인 빈 관리

`BeanFactory`는 Spring에서 가장 기본적인 형태의 빈 컨테이너입니다. 이 컨테이너는 빈을 생성, 설정, 관리 등의 역할을 합니다. 이 컨테이너는 별도의 설정 없이도 가장 단순한 형태의 빈 생성과 호출이 가능합니다.

- **지연 초기화(Lazy Initialization)**: `BeanFactory`는 빈을 처음으로 요청할 때까지 초기화를 지연시킵니다.
- **의존성 주입(Dependency Injection)**: 다른 객체와의 의존성을 자동으로 주입해 줍니다.
  
하지만, `BeanFactory`는 이벤트 전파, AOP 지원 등의 고급 기능을 제공하지 않습니다.

## ApplicationContext: 고급 빈 관리와 추가 기능

`ApplicationContext`는 `BeanFactory`의 확장된 형태로, 더 많은 기능을 제공합니다.

- **즉시 초기화(Eager Initialization)**: 컨테이너가 시작될 때 모든 싱글톤 빈을 초기화합니다.
- **이벤트 전파(Event Propagation)**: 애플리케이션 이벤트를 처리할 수 있습니다.
- **국제화(i18n) 지원**: 다국어를 지원하는 기능을 제공합니다.

`ApplicationContext`는 복잡한 애플리케이션에 적합하며, 여러 가지 부가 기능이 필요할 때 사용됩니다.

## 어떤 것을 사용해야 할까?

간단한 애플리케이션에서는 `BeanFactory`가 더 적합할 수 있습니다. 하지만 대부분의 상황에서 `ApplicationContext`를 사용하는 것이 더 나은 선택입니다. 이유는 다음과 같습니다.

- **기능성**: `ApplicationContext`가 제공하는 다양한 서비스가 대부분의 애플리케이션 개발에 유용합니다.
- **확장성**: 애플리케이션이 성장하면서 추가 기능이 필요할 때, `ApplicationContext`가 더 유연한 확장을 지원합니다.

## 정리

`BeanFactory`와 `ApplicationContext`는 Spring Framework에서 빈을 관리하는 두 가지 주요 컨테이너입니다. `BeanFactory`는 가장 기본적인 빈 관리를 제공하는 반면, `ApplicationContext`는 더 많은 기능과 편의성을 제공합니다. 따라서 애플리케이션의 요구 사항과 복잡성에 따라 적절한 컨테이너를 선택해야 합니다.