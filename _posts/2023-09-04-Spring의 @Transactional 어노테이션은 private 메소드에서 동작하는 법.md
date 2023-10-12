---
title: Spring의 Transactional 어노테이션은 private 메소드에서 동작하는 법
date: 2023-09-04 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - Transactional
  - 어노테이션
---
## 동작 원리와 제약사항

Spring 프레임워크의 `@Transactional` 어노테이션은 트랜잭션을 관리하는 매우 유용한 도구입니다. 하지만 이 어노테이션을 제대로 활용하려면 몇 가지 중요한 제약사항을 알아야 합니다. 특히, `@Transactional` 어노테이션이 private 메소드에서 동작하지 않는 이유는 Spring AOP(Aspect Oriented Programming)의 작동 방식 때문입니다.

Spring AOP는 프록시 기반으로 동작합니다. 이 말은, 어노테이션이 붙은 메소드가 호출될 때 실제로는 프록시 객체가 그 메소드를 대신 호출한다는 것을 의미합니다. 이 프록시 객체는 원래의 메소드를 호출하기 전후로 트랜잭션을 관리합니다. 그러나 프록시는 오직 public 메소드에만 적용될 수 있습니다. 따라서 `@Transactional` 어노테이션이 붙은 private 메소드는 프록시를 통해 접근할 수 없으므로 트랜잭션 관리가 이루어지지 않습니다.

## 코드 오류 예시

만약 `@Transactional` 어노테이션이 붙은 private 메소드를 사용하게 되면, 트랜잭션 처리가 예상대로 이루어지지 않을 것입니다. 이 경우 코드에서 특별한 에러 메시지는 나타나지 않겠지만, 예를 들어 `RuntimeException`이 발생했을 때 롤백(Rollback)이 이루어지지 않을 수 있습니다.

## 대안과 해결책

이 문제를 해결하기 위한 가장 간단한 방법은 해당 메소드를 public으로 변경하는 것입니다. 그 외에도 내부적으로 private 메소드를 호출하는 public 메소드를 하나 더 만들어 해당 public 메소드에 `@Transactional` 어노테이션을 붙이는 방법도 있습니다.

결론적으로, Spring의 `@Transactional` 어노테이션은 private 메소드에서는 동작하지 않습니다. 이를 이해하고 올바르게 적용하면 더 효과적인 트랜잭션 관리가 가능합니다.