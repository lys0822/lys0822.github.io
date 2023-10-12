---
title: Spring Boot에서 리소스 폴더에서 파일 읽기
date: 2023-10-03 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
---
## 개요

Spring Boot에서 리소스 폴더에 있는 파일을 읽어들이는 방법에는 여러가지가 있습니다. 이 글에서는 주로 사용되는 방법 몇 가지를 상세하게 소개하겠습니다.

## ClassPathResource 사용하기

`ClassPathResource` 클래스를 사용하여 파일을 로드할 수 있습니다. 아래는 코드 예시입니다.

```java
ClassPathResource resource = new ClassPathResource("example.txt");
InputStream inputStream = resource.getInputStream();
```

이 방법은 `java.io.InputStream`을 반환합니다. 이 스트림은 파일의 내용을 읽어들일 수 있습니다.

## ResourceLoader 사용하기

`ResourceLoader` 인터페이스를 사용하여도 리소스 폴더에 접근할 수 있습니다.

```java
@Autowired
ResourceLoader resourceLoader;

public void readFile() {
    Resource resource = resourceLoader.getResource("classpath:example.txt");
    InputStream inputStream = resource.getInputStream();
}
```

여기서 `@Autowired`는 스프링 프레임워크가 자동으로 해당 객체를 주입해주는 어노테이션입니다.

## FileReader와 BufferedReader 사용하기

또한 Java의 기본 클래스인 `FileReader`와 `BufferedReader`를 사용하여도 파일을 읽을 수 있습니다.

```java
BufferedReader reader = new BufferedReader(new FileReader("src/main/resources/example.txt"));
```

하지만 이 방법은 파일 경로를 직접 명시해야하기 때문에, JAR 파일로 패키징할 때 문제가 될 수 있습니다.

## 주의사항

`FileNotFoundException`이 발생할 수 있으므로, 파일을 읽는 코드를 실행하기 전에 해당 파일이 정말로 존재하는지 확인해야 합니다.

## 결론

Spring Boot에서 리소스 폴더에 있는 파일을 읽는 방법은 다양합니다. 상황과 필요에 따라 적절한 방법을 선택하여 사용하면 됩니다. 이렇게 하면 파일을 효율적으로 관리할 수 있습니다.