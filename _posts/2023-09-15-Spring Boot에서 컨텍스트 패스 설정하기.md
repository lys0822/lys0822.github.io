---
title: Spring Boot에서 컨텍스트 패스 설정하기
date: 2023-09-15 20:00:00 +0900
categories:
  - Spring
tags:
---
## 개요

Spring Boot 애플리케이션에서 컨텍스트 패스(Context Path)를 설정하는 방법에 대해 자세히 알아보겠습니다. 컨텍스트 패스는 웹 애플리케이션에서 URL이 어떻게 구성되는지 정의하는 중요한 요소입니다.

## 무엇이 컨텍스트 패스인가?

컨텍스트 패스는 웹 서버에서 애플리케이션을 구분하기 위한 URL의 일부입니다. 예를 들어, `http://localhost:8080/myApp`에서 `myApp`가 컨텍스트 패스입니다. 이를 통해 같은 웹 서버에서 여러 애플리케이션을 운영할 수 있습니다.

## 컨텍스트 패스 설정 방법

### `application.properties` 파일에서 설정

가장 일반적인 방법은 `application.properties` 파일에서 `server.servlet.context-path` 속성을 설정하는 것입니다.

```properties
server.servlet.context-path=/myApp
```

### Java 코드에서 설정

`WebServerFactoryCustomizer` 인터페이스를 구현하여 Java 코드 내에서도 설정할 수 있습니다.

```java
@Bean
public WebServerFactoryCustomizer<ConfigurableServletWebServerFactory> webServerFactoryCustomizer() {
    return factory -> factory.setContextPath("/myApp");
}
```

## 주의사항

- 이 설정은 애플리케이션을 재시작해야 적용됩니다.
- 컨텍스트 패스가 변경되면, 모든 웹 리소스의 URL도 이에 따라 바뀌므로 주의가 필요합니다.

## `server.servlet.context-path` vs `spring.mvc.servlet.path`

Spring Boot에서는 `server.servlet.context-path` 외에도 `spring.mvc.servlet.path` 옵션도 있습니다. 그러나 `spring.mvc.servlet.path`는 컨트롤러 레벨에서만 적용되므로, 일반적으로는 `server.servlet.context-path`를 사용하는 것이 좋습니다.

## 오류와 해결

### `NoSuchBeanDefinitionException`

컨텍스트 패스 설정 시 `NoSuchBeanDefinitionException`이 발생할 수 있습니다. 이 경우, `WebServerFactoryCustomizer` 빈 등록이 제대로 되지 않은 것이므로 확인이 필요합니다.

## 결론

Spring Boot에서 컨텍스트 패스 설정은 상당히 간단하며, 주로 `application.properties` 파일 또는 Java 코드를 통해 설정할 수 있습니다. 이 설정은 웹 리소스의 URL을 결정하므로 중요한 작업입니다.