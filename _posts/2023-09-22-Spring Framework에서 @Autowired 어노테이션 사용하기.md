---
title: Spring Framework에서 @Autowired 어노테이션 사용하기
date: 2023-09-22 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - 프레임워크
  - PrivateAutowired
---
## 무엇이 @Autowired 어노테이션인가?

@Autowired 어노테이션은 Spring Framework에서 의존성 주입(Dependency Injection)을 단순화하기 위해 사용됩니다. 의존성 주입이란, 하나의 객체가 다른 객체의 서비스를 사용할 수 있도록 연결해주는 기술을 말합니다. @Autowired는 개발자가 직접 객체를 생성하거나 관리하지 않아도, Spring 컨테이너가 자동으로 관리해줍니다.

## 어떻게 사용하나요?

@Autowired 어노테이션은 클래스의 필드, 생성자, 또는 메소드에 적용할 수 있습니다. 다음은 각 경우에 대한 간단한 예시입니다.

### 필드 주입(Field Injection)

```java
@Autowired
private MyService myService;
```

### 생성자 주입(Constructor Injection)

```java
@Autowired
public MyClass(MyService myService) {
  this.myService = myService;
}
```

### 메소드 주입(Method Injection)

```java
@Autowired
public void setMyService(MyService myService) {
  this.myService = myService;
}
```

## 주의사항은 무엇인가요?

@Autowired 어노테이션 사용 시에는 몇 가지 주의사항이 있습니다.

### No qualifying bean of type 에러

만약 적절한 빈(bean)이 없을 경우, `No qualifying bean of type` 에러가 발생할 수 있습니다. 이는 Spring 컨테이너가 필요한 타입의 빈을 찾지 못했음을 의미합니다.

### 주입 받을 빈이 여러 개인 경우

하나의 타입에 여러 빈이 존재하는 경우, `@Primary` 어노테이션을 사용하여 주요 빈을 지정할 수 있습니다.

## 정리

@Autowired 어노테이션은 Spring에서 의존성 주입을 쉽고 효율적으로 관리할 수 있게 도와줍니다. 주의사항을 잘 이해하고 사용한다면, 코드의 품질과 가독성을 높일 수 있습니다.