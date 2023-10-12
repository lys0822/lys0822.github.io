---
title: Spring CRUDRepository에서 List<Long> 타입으로 검색하는 방법
date: 2023-08-31 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - CRUDReponsitory
---
## 문제 상황: findByInventoryIdsList 구현

Spring Framework에서 JPA와 함께 사용되는 `CrudRepository` 인터페이스는 매우 유용합니다. 그런데, 이 인터페이스를 사용하여 `List<Long>` 타입의 inventory ID를 가지고 데이터를 검색하려고 할 때 어떻게 해야 할까요? 이 글에서는 Stack Overflow의 해당 질문에 대한 해결책을 자세하게 설명합니다.

## 에러 코드: NoSuchMethodError

먼저, 이런 유형의 문제에서 가장 흔하게 발생하는 에러는 `NoSuchMethodError` 입니다. 이 에러는 원하는 메소드가 CrudRepository 인터페이스나 해당 구현 클래스에 없을 때 발생합니다.

## 사용 가능한 해결 방법

### 1. `@Query` 어노테이션 사용

이 문제를 해결하는 첫 번째 방법은 `@Query` 어노테이션을 사용하여 JPQL(Java Persistence Query Language) 쿼리를 작성하는 것입니다. 

```java
@Query("SELECT e FROM Entity e WHERE e.inventoryId IN :inventoryIds")
List<Entity> findByInventoryIdsList(@Param("inventoryIds") List<Long> inventoryIds);
```

### 2. 메소드 이름을 이용한 쿼리 생성

`CrudRepository` 인터페이스에서는 메소드 이름만으로도 쿼리를 생성할 수 있습니다. 이를 통해 아래와 같이 간단히 구현할 수 있습니다.

```java
List<Entity> findByInventoryIdIn(List<Long> inventoryIds);
```

### 3. Native Query 사용

이 방법은 데이터베이스에 직접 쿼리를 보내는 방법입니다. 이 방법은 다소 복잡할 수 있으나, 성능이 중요한 상황에서 유용하게 사용될 수 있습니다.

```java
@Query(value = "SELECT * FROM Entity WHERE inventory_id IN ?1", nativeQuery = true)
List<Entity> findByInventoryIdsList(List<Long> inventoryIds);
```

## 결론: 어떤 방법을 사용할까?

각 방법은 자신의 장단점이 있습니다. `@Query` 어노테이션을 사용하면 더 복잡한 쿼리를 작성할 수 있습니다. 메소드 이름을 이용한 방법은 간단하며, Native Query는 성능을 최적화할 수 있습니다. 상황에 따라 적절한 방법을 선택하면 됩니다.