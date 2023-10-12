---
title: pring에서 여러 패키지 설정하기 context component-scan 이해하기
date: 2023-10-11 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - pring
---
# Spring에서 여러 패키지 설정하기: `context:component-scan` 이해하기

## 문제 상황

Spring 프레임워크를 사용하면서 `context:component-scan`을 이용해 자동으로 빈(bean)을 등록할 수 있습니다. 그러나 한 가지 어려운 점은 하나 이상의 패키지를 스캔해야 할 경우입니다. 이 글에서는 `context:component-scan`을 사용하여 여러 패키지를 어떻게 설정하는지 설명하겠습니다.

## 해결 방법 1: 쉼표로 구분하기

가장 간단한 방법은 `base-package` 속성에 여러 패키지를 쉼표(,)로 구분하여 나열하는 것입니다.

```xml
<context:component-scan base-package="com.example.package1, com.example.package2" />
```

이렇게 하면 `com.example.package1`과 `com.example.package2` 두 패키지 모두에서 스캔이 이루어집니다. XML 설정 파일에서 이 한 줄로 두 패키지를 손쉽게 설정할 수 있습니다.

## 해결 방법 2: 와일드카드 사용하기

와일드카드(*)를 사용하여 하위 패키지까지 스캔할 수 있습니다.

```xml
<context:component-scan base-package="com.example.*" />
```

이 설정은 `com.example` 패키지와 그 하위 패키지들을 모두 스캔합니다. 와일드카드는 '모든 것'을 의미하는 특수 문자입니다.

## 해결 방법 3: Java Config 사용하기

XML 대신 Java Config를 사용하는 방법도 있습니다. `@ComponentScan` 애노테이션을 이용하면 됩니다.

```java
@Configuration
@ComponentScan(basePackages = {"com.example.package1", "com.example.package2"})
public class AppConfig {}
```

이 방법은 Java 파일에서 애노테이션을 사용하여 여러 패키지를 설정하는 것입니다. 애노테이션은 코드에 메타데이터를 추가하는 방법입니다.

## 오류와 주의사항

- **Error creating bean**: 빈 생성 중 에러가 발생한 경우, 패키지명이 정확한지 확인해야 합니다.
- **ClassNotFoundException**: 이 오류는 클래스를 찾을 수 없을 때 발생합니다. 패키지명과 클래스명을 다시 확인하세요.

## 요약

Spring의 `context:component-scan`을 사용하여 여러 패키지를 설정하는 방법은 세 가지입니다. 첫째, XML 설정 파일에서 쉼표로 여러 패키지를 구분할 수 있습니다. 둘째, 와일드카드를 사용하여 하위 패키지까지 스캔할 수 있습니다. 셋째, Java Config를 사용하여 `@ComponentScan` 애노테이션으로 설정할 수 있습니다. 이러한 방법을 통해 복잡한 프로젝트에서도 효율적으로 빈을 관리할 수 있습니다.