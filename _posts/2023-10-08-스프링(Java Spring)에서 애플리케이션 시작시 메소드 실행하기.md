---
title: 스프링(Java Spring)에서 애플리케이션 시작시 메소드 실행하기
date: 2023-10-08 20:00:00 +0900
categories:
  - Spring
tags:
  - Java
  - Spring
---
## `@PostConstruct`를 이용한 방법

`@PostConstruct`는 Java에서 제공하는 어노테이션 중 하나입니다. 이 어노테이션은 스프링 빈이 초기화될 때 실행되는 메소드에 붙일 수 있습니다.

```java
import javax.annotation.PostConstruct;

public class MyBean {

    @PostConstruct
    public void init() {
        // 여기에 시작시 실행될 코드를 넣습니다.
    }
}
```

이 방법은 간단하고 편리하며, 메소드가 빈 초기화 직후에 실행되기 때문에 다른 빈과의 의존성 문제를 쉽게 해결할 수 있습니다.

## `CommandLineRunner`나 `ApplicationRunner` 인터페이스 사용

`CommandLineRunner`나 `ApplicationRunner`는 스프링 부트에서 제공하는 인터페이스입니다. 이 인터페이스를 구현하여 `run` 메소드를 오버라이딩하면, 애플리케이션 시작 후에 원하는 로직을 실행할 수 있습니다.

```java
import org.springframework.boot.CommandLineRunner;
import org.springframework.stereotype.Component;

@Component
public class MyStartupRunner implements CommandLineRunner {

    @Override
    public void run(String... args) {
        // 여기에 시작시 실행될 코드를 넣습니다.
    }
}
```

이 방법은 스프링 부트에서만 사용할 수 있으며, 애플리케이션 시작 후에 코드를 실행할 때 유용합니다.

## `@EventListener` 사용

스프링 4.2 이상에서는 `@EventListener` 어노테이션을 사용하여 애플리케이션 이벤트를 듣고 그에 따라 메소드를 실행할 수 있습니다.

```java
import org.springframework.context.event.ContextRefreshedEvent;
import org.springframework.context.event.EventListener;

public class MyBean {

    @EventListener(ContextRefreshedEvent.class)
    public void onApplicationEvent(ContextRefreshedEvent event) {
        // 여기에 시작시 실행될 코드를 넣습니다.
    }
}
```

이 방법은 더 복잡한 이벤트 조건에 따라 메소드를 실행할 때 유용합니다.

## 요약

여러 방법이 있지만, 각 방법은 사용 케이스에 따라 장단점이 있습니다. `@PostConstruct`는 빈 초기화시, `CommandLineRunner`와 `ApplicationRunner`는 애플리케이션 시작 후, `@EventListener`는 특정 이벤트 발생시에 메소드를 실행할 수 있습니다. 본인의 상황에 맞는 방법을 선택하면 됩니다.