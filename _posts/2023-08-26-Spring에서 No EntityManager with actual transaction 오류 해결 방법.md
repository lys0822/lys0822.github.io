---
title: Spring에서 No EntityManager with actual transaction 오류 해결 방법
date: 2023-08-26 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring오류
---
## 오류 개요

Spring 프레임워크에서 개발을 하다 보면 다양한 오류에 직면할 수 있습니다. 이 중 하나가 "No EntityManager with actual transaction available for current thread"라는 오류 메시지입니다. 이 오류는 데이터베이스와 관련된 작업을 할 때 흔히 발생합니다.

## 원인 파악

이 오류는 주로 Spring의 JPA(Java Persistence API)를 사용할 때 발생합니다. JPA는 자바 어플리케이션에서 관계형 데이터베이스를 쉽게 다루기 위한 API입니다. 오류 메시지가 나타나는 주요 원인은 트랜잭션이 제대로 설정되지 않았거나, 현재 스레드에 대한 트랜잭션이 존재하지 않을 때입니다.

## 해결 방안

### @Transactional 어노테이션 확인

이 오류를 해결하는 가장 간단한 방법은 `@Transactional` 어노테이션을 메서드나 클래스에 추가하는 것입니다. 이 어노테이션은 메서드가 실행되는 동안 데이터베이스의 트랜잭션을 관리해줍니다.

```java
@Service
public class YourService {
    @Transactional
    public void yourMethod() {
        // your code here
    }
}
```

### EntityManager 주입

또 다른 방법은 `EntityManager`를 직접 주입하여 사용하는 것입니다. 이 방법은 복잡한 트랜잭션 로직이 필요한 경우 유용합니다.

```java
@Service
public class YourService {
    @PersistenceContext
    private EntityManager entityManager;
    
    public void yourMethod() {
        // your code here
        entityManager.flush();
    }
}
```

## 마무리

"No EntityManager with actual transaction available for current thread" 오류는 주로 트랜잭션 설정이 잘못되었을 때 발생합니다. 이 문제를 해결하기 위해 `@Transactional` 어노테이션을 적용하거나, 필요한 경우 `EntityManager`를 직접 사용할 수 있습니다. 이러한 접근 방식을 통해 오류를 해결하고 더 안정적인 애플리케이션을 개발할 수 있습니다.