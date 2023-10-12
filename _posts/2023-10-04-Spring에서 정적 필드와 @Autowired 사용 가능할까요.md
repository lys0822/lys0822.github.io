---
title: Spring에서 정적 필드와 @Autowired 사용 가능할까요
date: 2023-10-04 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - Autowired
---
## 정적 필드와 `@Autowired` 애너테이션

Spring 프레임워크에서 `@Autowired` 애너테이션을 사용하면 자동으로 의존성을 주입할 수 있습니다. 하지만 많은 개발자가 이 기능을 정적 필드에 적용할 수 있는지 의문을 가집니다. 정답은 **아니요**, Spring에서 `@Autowired`를 정적 필드에 직접 사용할 수 없습니다. 정적 필드는 클래스 레벨에서 공유되므로 인스턴스 생성과 독립적입니다. 따라서 Spring 컨테이너가 관리하는 빈을 정적 필드에 주입할 수 없습니다.

## 대안 방법: `@PostConstruct`

정적 필드에 의존성을 주입하려면 몇 가지 방법이 있습니다. `@PostConstruct` 애너테이션을 사용하는 것이 일반적인 방법입니다. 이 애너테이션은 빈이 완전히 초기화된 후에 실행되는 메서드를 표시합니다. 이 메서드 내에서 정적 필드를 설정할 수 있습니다.

```java
@Component
public class MyBean {
    @Autowired
    private SomeDependency someDependency;

    private static SomeDependency staticSomeDependency;

    @PostConstruct
    public void init() {
        staticSomeDependency = someDependency;
    }
}
```

여기서 `@PostConstruct`가 붙은 `init` 메서드가 빈 초기화 후에 실행되어 정적 필드 `staticSomeDependency`에 `someDependency` 빈을 주입합니다.

## 왜 이렇게 복잡한가?

Spring은 주로 인스턴스 레벨에서 작동하도록 설계되었습니다. 정적 필드는 클래스 레벨에서 작동하므로 이 두 개념은 잘 맞지 않습니다. 이러한 이유로 Spring에서는 `@Autowired`를 이용한 정적 필드에 대한 직접적인 의존성 주입을 지원하지 않습니다.

## 결론

정적 필드에 Spring 빈을 주입하려면 직접적인 방법은 없습니다. 대신 `@PostConstruct`를 사용하여 간접적으로 의존성을 주입할 수 있습니다. 이 방법을 이용하면 정적 필드에도 Spring 빈을 사용할 수 있게 됩니다.