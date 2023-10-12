---
title: Spring Boot에서 실행할 Main 클래스 지정하기
date: 2023-09-30 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
  - Main클래스
---
## 문제 상황: `NoUniqueBeanDefinitionException` 오류

Spring Boot 프로젝트에서 여러 개의 `@SpringBootApplication` 클래스가 있다면, 실행 시 `NoUniqueBeanDefinitionException` 오류가 발생할 수 있습니다. 이 오류는 Spring Boot가 어떤 클래스를 애플리케이션의 시작점으로 사용해야 할지 모르기 때문에 발생합니다.

## 해결 방법 1: 명령어에 `--main-class` 옵션 추가

가장 간단한 방법은 명령어를 실행할 때 `--main-class` 옵션을 통해 Main 클래스를 명시적으로 지정하는 것입니다. 예를 들어, `MyApplication` 클래스를 실행하려면 아래와 같이 명령어를 입력합니다.

```bash
java -jar your-app.jar --main-class=com.example.MyApplication
```

## 해결 방법 2: `SpringApplication.setDefaultProperties` 메서드 사용

`SpringApplication` 클래스의 `setDefaultProperties` 메서드를 사용하면, 프로그램 코드 내에서 Main 클래스를 설정할 수 있습니다. 아래는 코드 예시입니다.

```java
public static void main(String[] args) {
    SpringApplication app = new SpringApplication(MyApplication.class);
    app.setDefaultProperties(Collections
      .singletonMap("spring.main.default-main-class", "com.example.MyApplication"));
    app.run(args);
}
```

## 해결 방법 3: `MANIFEST.MF` 파일 수정

JAR 파일 내의 `META-INF/MANIFEST.MF` 파일을 수정하여 `Start-Class` 속성을 지정하는 방법도 있습니다. 이 파일에서 `Start-Class` 키의 값을 원하는 Main 클래스로 설정하면 됩니다.

```text
Start-Class: com.example.MyApplication
```

## 주의사항: 다양한 설정 간의 우선순위

위에서 설명한 방법들은 동시에 적용될 수 있으나, `--main-class` 옵션은 가장 높은 우선순위를 가집니다. 다음으로 `SpringApplication.setDefaultProperties` 메서드, 그리고 마지막으로 `MANIFEST.MF` 파일이 적용됩니다.

## 결론

여러 개의 Main 클래스가 있는 Spring Boot 애플리케이션에서 `NoUniqueBeanDefinitionException` 오류를 해결하는 방법은 여러 가지입니다. 명령어 옵션, 코드 내 설정, 또는 `MANIFEST.MF` 파일을 통해 원하는 Main 클래스를 지정할 수 있습니다. 이러한 방법들을 통해 애플리케이션을 원활하게 실행할 수 있습니다.