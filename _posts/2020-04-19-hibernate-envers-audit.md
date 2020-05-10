---
layout: post
title: "Hibernate Envers의 @Audited"
tags: [Spring, JPA, Hibernate, Spring Data JPA, Envers, Audit]
categories: [Spring, Hibernate, Envers]
subtitle: "엔티티의 이력 테이블"
feature-img: "md/img/thumbnail/hibernate-envers.png"
thumbnail: "md/img/thumbnail/hibernate-envers.png"
excerpt_separator: <!--more-->
sitemap:
changefreq: daily

priority: 1.0
---

<!--more-->

# 엔티티의 이력 테이블

---

# 들어가기전

이전 [Spring Data JPA의 이력 유형 데이터 관리](https://gmoon92.github.io/spring/hibernate/audited/2020/04/10/spring-data-audit.html) 포스팅에서 Spring Data 애노테이션을 활용하여 엔티티의 이력 유형 데이터 모델링하는 방법에 대해 작성했습니다.

글을 보다보면 Spring Data 애노테이션으로 이력 유형 데이터를 관리할 수 있지만, 이전의 데이터 또는 삭제한 데이터를 추적할 수 없다는 단점이 있습니다.

- 이전 이력 데이터 관리
- 삭제 데이터 관리

다음 문제점들을 해결하기 위해선 이력 데이터를 추적할 테이블을 관리한다면 해결할 수 있지만, 기존의 테이블 외에 별도의 테이블을 생성하여 관리한다는 건 쉽지 않습니다. Hibernate에선 이러한 상황들을 고려하여 Hibernate Envers 패키지를 제공해주고 있습니다. 이를 사용한다면 더욱 쉽게 이력 데이터를 관리할 수 있습니다. 본 포스팅에선 Hibernate Envers를 활용하여 이력 데이터를 관리하는 방법에 대해 소개해드리겠습니다.

>- [Hibernate Envers를 활용한 이력관리](https://gmoon92.github.io/spring/hibernate/envers/2020/01/02/hibernate-envers-concepts.html) 
>- [Spring Data JPA의 이력 유형 데이터 관리](https://gmoon92.github.io/spring/hibernate/audited/2020/04/10/spring-data-audit.html)


# 학습 목표

- Hibernate Envers 사용법과 이해
- Audited Entity

## 1. Hibernate Envers
## Audited Entity

Hibernate Envers는 

## 2. Envers Config Properties

## 3. Revision Table 구성

## 4. Revision Table 조회


- Audited Entity
- Custom Revision Entity
- EntityTrackingRevisionListener
- EventListenerRegistry

### 마무리

### 참고

- [jboss-docs-hibernate-4.1-Envers](https://docs.jboss.org/hibernate/core/4.1/devguide/en-US/html/ch15.html#envers-tracking-modified-entities-queries)
- [Spring DOC - Spring data](https://docs.spring.io/spring-data/data-commons/docs/current/api/org/springframework/data/annotation/package-frame.html)
- [Baeldung - Spring data annotations](https://www.baeldung.com/spring-data-annotations)
- [Hibernate-core - listeners](https://docs.jboss.org/hibernate/core/4.0/hem/en-US/html/listeners.html)