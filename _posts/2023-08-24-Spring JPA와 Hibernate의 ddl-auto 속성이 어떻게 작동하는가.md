---
title: Spring JPA와 Hibernate의 ddl-auto 속성이 어떻게 작동하는가
date: 2023-08-24 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - JupyterLab오류
  - Hibernate
  - ddl-auto
---
## 소개

Spring JPA와 Hibernate를 사용할 때 주목해야 할 중요한 설정 중 하나는 `ddl-auto` 속성입니다. 이 설정은 데이터베이스 스키마(Database Schema)를 어떻게 처리할지를 결정합니다. 여기에서는 `ddl-auto`의 다양한 옵션과 그 작동 방식에 대해 자세히 알아보겠습니다.

## 'ddl-auto' 속성의 다양한 옵션

`ddl-auto` 속성은 주로 `application.properties` 또는 `application.yml` 파일에 설정됩니다. 이 설정에는 여러 가지 옵션값이 있습니다.

- **none**: 아무런 작동을 하지 않습니다.
- **validate**: 데이터베이스 스키마와 엔터티 클래스가 일치하는지 검증합니다.
- **update**: 필요한 경우 데이터베이스 스키마를 업데이트합니다.
- **create**: 실행할 때마다 테이블을 새로 생성합니다.
- **create-drop**: 애플리케이션 종료시 테이블을 삭제합니다.

## 'none' 옵션

이 옵션을 설정하면 Hibernate는 데이터베이스에 대한 어떤 DDL(Data Definition Language) 작업도 수행하지 않습니다. DDL이란 데이터베이스 스키마를 정의하거나 변경하는 언어입니다.

## 'validate' 옵션

`validate`를 설정하면, 애플리케이션 실행 시 Hibernate는 엔터티 클래스와 데이터베이스 스키마가 일치하는지 검사합니다. 일치하지 않으면 `Schema-validation: wrong column type encountered`와 같은 오류를 발생시킵니다.

## 'update' 옵션

이 옵션을 사용하면 Hibernate는 데이터베이스 스키마를 필요에 따라 자동으로 업데이트합니다. 새로운 엔터티가 추가되거나 기존 엔터티가 변경된 경우, 이 변경사항을 데이터베이스에 반영합니다.

## 'create'와 'create-drop' 옵션

`create` 옵션은 애플리케이션을 실행할 때마다 데이터베이스 테이블을 새로 생성합니다. 기존 테이블은 삭제됩니다. `create-drop`은 `create` 옵션과 유사하지만, 애플리케이션 종료시에 생성한 테이블을 삭제합니다.

## 정리

`ddl-auto` 속성은 Spring JPA와 Hibernate에서 데이터베이스 스키마를 어떻게 관리할지 결정하는 중요한 설정입니다. 옵션에 따라 다양한 작동 방식이 있으므로, 상황에 따라 적절한 값을 설정해야 합니다. 이로써 개발 과정이 더욱 효율적이고 안정적으로 진행될 수 있습니다.