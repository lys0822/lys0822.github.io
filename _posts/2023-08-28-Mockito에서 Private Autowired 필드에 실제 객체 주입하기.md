---
title: Mockito에서 Private Autowired 필드에 실제 객체 주입하기
date: 2023-08-28 20:00:00 +0900
categories:
  - Spring
tags:
  - Mockito
  - PrivateAutowired
---
## 문제 상황: Private Autowired 필드가 있는 경우 Mockito 사용법

개발자들이 테스트를 작성할 때 종종 사용하는 도구 중 하나가 Mockito라는 테스트 프레임워크입니다. Mockito를 사용하면, 개발자는 실제 객체 대신 가상 객체(Mock Object)를 쉽게 생성하여 테스트할 수 있습니다. 그런데 이러한 가상 객체를 `@Autowired` 어노테이션이 붙은 **private 필드**에 주입하려고 할 때 문제가 생기곤 합니다.

## 해결책: Private Autowired 필드에 실제 객체를 어떻게 주입할까?

### Reflection API 활용하기

Reflection API는 자바에서 객체의 클래스 정보를 취득하고, 그 정보를 활용하여 메소드를 실행하거나 필드에 접근할 수 있게 도와주는 API입니다. 이를 활용하면 private 필드에도 접근이 가능합니다.

1. **Field 객체 가져오기**: 먼저 `Class` 객체의 `getDeclaredField` 메소드를 사용하여 접근하려는 필드의 `Field` 객체를 얻습니다.
2. **접근 권한 부여**: `Field` 객체의 `setAccessible` 메소드를 true로 설정하여 접근 권한을 부여합니다.
3. **객체 주입**: `Field` 객체의 `set` 메소드를 사용하여 실제 객체를 주입합니다.

```java
Field field = myClass.getDeclaredField("myField");
field.setAccessible(true);
field.set(myObject, realObject);
```

### Mockito의 `@InjectMocks`와 `@Spy` 활용하기

Mockito에는 `@InjectMocks` 어노테이션이 있는데, 이 어노테이션은 테스트 대상 클래스의 인스턴스를 생성하면서 실제 객체 또는 Mock 객체를 자동으로 주입해줍니다. 여기서 `@Spy`를 같이 사용하면 실제 객체를 주입할 수 있습니다.

```java
@InjectMocks
MyClass myClass;

@Spy
RealObject realObject;

@Before
public void setUp() {
    MockitoAnnotations.initMocks(this);
}
```

## 결론: Mockito와 Private Autowired 필드

`Reflection API`를 사용하거나 Mockito의 `@InjectMocks`와 `@Spy` 어노테이션을 활용하면 private 필드에도 실제 객체를 쉽게 주입할 수 있습니다. 이로써 Mockito를 사용한 유닛 테스트 작성에서도 더 다양한 상황에 대응할 수 있게 됩니다.