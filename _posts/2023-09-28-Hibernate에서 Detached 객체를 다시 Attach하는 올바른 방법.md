---
title: Hibernate에서 Detached 객체를 다시 Attach하는 올바른 방법
date: 2023-09-28 20:00:00 +0900
categories:
  - Spring
tags:
  - Hibernate
  - Detached객체
---
## Detached 객체란 무엇인가?

Hibernate에서 `Detached 객체`라고 부르는 것은 영속성 컨텍스트(Persistence Context)와 연결이 끊긴 객체를 말합니다. 영속성 컨텍스트는 데이터베이스와 객체 사이에 있는 캐시와 같은 것입니다. Detached 상태가 되면 Hibernate는 이 객체의 변경을 데이터베이스에 반영하지 않습니다.

## 왜 Detached 객체를 Attach해야 하는가?

Detached 객체는 데이터베이스와 동기화되지 않기 때문에, 객체를 수정했을 경우 해당 변경이 데이터베이스에 반영되지 않습니다. 따라서 필요한 수정을 한 후에는 반드시 이 객체를 다시 Attach 상태로 만들어 데이터베이스와 동기화해야 합니다.

## 올바른 Attach 방법

### `Session.merge()`

`Session.merge()` 메서드를 사용하면 Detached 객체를 다시 Attach 상태로 만들 수 있습니다. 이 방법은 Detached 객체와 현재 세션(Session)에 존재하는 객체를 병합(merge)합니다.

```java
Session session = sessionFactory.openSession();
session.beginTransaction();
YourClass detachedObject = /* 가져온 Detached 객체 */;
YourClass attachedObject = (YourClass) session.merge(detachedObject);
session.getTransaction().commit();
session.close();
```

### `Session.update()`

`Session.update()` 메서드를 사용할 수도 있습니다. 그러나 이 방법은 조심해야 할 점이 있습니다. 만약 같은 식별자(ID)를 가진 객체가 이미 세션에서 관리되고 있다면 `NonUniqueObjectException` 에러가 발생합니다.

```java
Session session = sessionFactory.openSession();
session.beginTransaction();
YourClass detachedObject = /* 가져온 Detached 객체 */;
session.update(detachedObject);
session.getTransaction().commit();
session.close();
```

## 결론

Detached 객체를 다시 Attach 상태로 만드는 것은 객체와 데이터베이스의 동기화를 위해 중요합니다. 이를 위해 `Session.merge()` 또는 `Session.update()` 메서드를 사용할 수 있으며, 각 방법에는 그에 맞는 사용 시나리오와 주의점이 있습니다.