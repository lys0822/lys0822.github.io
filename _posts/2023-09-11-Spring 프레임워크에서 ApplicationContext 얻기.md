---
title: Spring 프레임워크에서 ApplicationContext 얻기
date: 2023-09-11 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - ApplicationContext
---
## ApplicationContext란 무엇인가?

`ApplicationContext`는 Spring 프레임워크에서 중요한 구성 요소입니다. 이것은 빈(bean) 설정, 이벤트 전파, 리소스 로딩 등 다양한 역할을 합니다. 빈은 Spring에서 관리하는 객체를 의미하며, `ApplicationContext`는 이러한 빈들의 라이프사이클을 관리합니다.

## `ApplicationContext` 얻기의 일반적인 방법

1. **어노테이션을 이용한 방법**: `@Autowired` 어노테이션을 사용하여 자동으로 주입합니다.
    ```java
    @Autowired
    private ApplicationContext applicationContext;
    ```

2. **`ApplicationContextAware` 인터페이스 구현**: 이 인터페이스를 구현하고 `setApplicationContext` 메서드를 오버라이딩합니다.
    ```java
    public class MyClass implements ApplicationContextAware {
        private ApplicationContext applicationContext;

        @Override
        public void setApplicationContext(ApplicationContext applicationContext) {
            this.applicationContext = applicationContext;
        }
    }
    ```

3. **`SpringApplication.run()` 반환 값 활용**: 이 메서드는 `ConfigurableApplicationContext` 타입의 객체를 반환합니다.
    ```java
    ConfigurableApplicationContext context = SpringApplication.run(MyApplication.class, args);
    ```

4. **`WebApplicationContextUtils`를 사용한 방법**: 웹 애플리케이션에서 사용할 경우, `WebApplicationContextUtils`를 사용할 수 있습니다.
    ```java
    ApplicationContext ctx = WebApplicationContextUtils.getWebApplicationContext(servletContext);
    ```

## 각 방법의 적절한 활용 시기

- **어노테이션을 이용한 방법**: 코드가 Spring 컨테이너에 의해 관리되고 있을 때 가장 간단하고 적합합니다.
- **`ApplicationContextAware` 인터페이스 구현**: 빈의 라이프사이클에 더 깊게 관여해야 할 때 사용합니다.
- **`SpringApplication.run()` 반환 값 활용**: 애플리케이션의 시작점에서 `ApplicationContext`를 얻고 싶을 때 사용합니다.
- **`WebApplicationContextUtils`를 사용한 방법**: 웹 애플리케이션과 연동되는 경우에만 사용할 수 있습니다.

## 주의사항

- `ApplicationContext`는 애플리케이션의 중심적인 역할을 하므로, 무턱대고 얻어서 사용하는 것은 좋지 않습니다.
- 싱글톤 빈으로만 작동하므로, 여러 번 얻어도 동일한 객체를 반환합니다.

이 글을 통해 Spring의 `ApplicationContext`를 어떻게 얻을 수 있는지, 언제 어떤 방법을 사용하는 것이 좋은지에 대한 명확한 이해를 하셨길 바랍니다.