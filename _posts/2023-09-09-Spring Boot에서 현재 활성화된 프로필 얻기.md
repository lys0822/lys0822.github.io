---
title: Spring Boot에서 현재 활성화된 프로필 얻기
date: 2023-09-09 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
---
## Spring Boot란 무엇인가?

Spring Boot는 자바(Java)로 웹 애플리케이션을 개발하는 데 도움을 주는 프레임워크입니다. 프레임워크란 프로그램을 개발할 때 필요한 기본 구조를 제공하는 도구를 말합니다. Spring Boot는 빠른 개발과 간편한 설정을 위해 많이 사용됩니다.

## 환경 프로필(Environment Profile)이란?

환경 프로필이란 애플리케이션을 다른 환경(예: 개발, 테스트, 운영 등)에서 실행할 때 필요한 설정을 구분해 놓은 것입니다. 이렇게 하면 같은 애플리케이션 코드를 여러 환경에서 다르게 실행할 수 있습니다.

## 프로그래밍으로 현재 활성화된 프로필 얻는 방법

Spring Boot에서 현재 활성화된 환경 프로필을 프로그래밍적으로 얻으려면 `Environment` 인터페이스를 사용할 수 있습니다. `Environment` 인터페이스는 애플리케이션의 현재 환경 정보를 얻을 수 있는 메서드를 제공합니다.

### 코드 예시

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.core.env.Environment;
import org.springframework.stereotype.Component;

@Component
public class ProfileChecker {
  
  @Autowired
  private Environment environment;

  public void printActiveProfiles() {
    String[] activeProfiles = environment.getActiveProfiles();
    for (String profile : activeProfiles) {
      System.out.println("현재 활성화된 프로필: " + profile);
    }
  }
}
```

이 코드는 `Environment` 인터페이스를 통해 현재 활성화된 프로필을 배열 형태로 얻고, 그것을 콘솔에 출력합니다.

### 주의사항

- `@Autowired` 어노테이션은 Spring이 자동으로 `Environment` 객체를 주입해주기 위한 설정입니다. 주입이란 필요한 객체를 자동으로 생성하여 연결하는 것을 말합니다.
- `@Component` 어노테이션은 이 클래스가 Spring의 컴포넌트임을 나타냅니다.

이 글을 통해 Spring Boot에서 현재 활성화된 환경 프로필을 프로그래밍적으로 얻는 방법에 대해 알아보았습니다. 이 정보가 도움이 되길 바랍니다.