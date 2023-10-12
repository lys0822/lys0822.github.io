---
title: Spring에서 Mockito를 사용하여 Autowired 필드를 Mock하는 방법
date: 2023-09-03 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - Mockito
  - PrivateAutowired
---
## 문제 상황: Autowired 필드 Mock 실패

Spring 프레임워크에서 테스트를 진행할 때, 종종 `@Autowired` 어노테이션이 붙은 필드를 가진 클래스를 테스트해야 하는 경우가 있습니다. 이때, 해당 필드를 모의 객체(Mock Object)로 만들어야 할 필요가 있습니다. 그러나 실제로 이를 실행하려고 하면 `NullPointerExeption` 이라는 에러가 발생하는 경우가 있습니다.

## Mockito를 사용한 해결 방법

### @InjectMocks와 @Mock 사용

Mockito 라이브러리를 사용하면 `@InjectMocks`와 `@Mock` 어노테이션을 사용하여 이 문제를 해결할 수 있습니다. `@InjectMocks`는 테스트할 클래스에 사용되며, `@Mock`은 모의 객체로 만들 필드에 사용됩니다.

```java
@RunWith(MockitoJUnitRunner.class)
public class MyClassTest {
  
  @InjectMocks
  MyClass myClass;
  
  @Mock
  MyAutowiredField myAutowiredField;
  
  @Test
  public void testMethod() {
    // 테스트 코드 작성
  }
}
```

### @MockBean 사용

Spring Boot를 사용하는 경우 `@MockBean` 어노테이션을 사용할 수도 있습니다. 이 어노테이션은 Spring ApplicationContext에 모의 객체를 추가합니다.

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class MyClassTest {

  @Autowired
  MyClass myClass;
  
  @MockBean
  MyAutowiredField myAutowiredField;
  
  @Test
  public void testMethod() {
    // 테스트 코드 작성
  }
}
```

## 주의 사항

이렇게 Mock 객체를 사용하면 실제 객체가 하는 일을 모방할 수 있습니다. 그러나 Mock 객체는 실제 객체의 상태를 가지고 있지 않기 때문에, 상태를 체크하는 로직에 대한 테스트는 신중하게 진행해야 합니다.

## 결론

`@Autowired` 필드를 테스트하려면 Mockito의 `@InjectMocks`, `@Mock` 또는 Spring Boot의 `@MockBean`을 사용하여 문제를 해결할 수 있습니다. 이를 통해 안정적인 단위 테스트를 진행할 수 있습니다.