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

이전 [Spring Data JPA의 이력 유형 데이터 관리](https://gmoon92.github.io/spring/hibernate/audited/2020/04/10/spring-data-audit.html) 포스팅에서 엔티티의 이력 유형 데이터 모델링 하는 방법을 소개해드렸습니다.

이때 삭제에 대한 데이터를 추적할 수 없다는 단점이 존재했습니다. 본 포스팅에선 삭제 데이터는 물론이거니와 

>- [Hibernate Envers를 활용한 이력관리](https://gmoon92.github.io/spring/hibernate/envers/2020/01/02/hibernate-envers-concepts.html) 
>- [Spring Data JPA의 이력 유형 데이터 관리](https://gmoon92.github.io/spring/hibernate/audited/2020/04/10/spring-data-audit.html)


# 앞으로 진행될 내용

지금까지 Hibernate Envers에 대한 대략적인 개념과 동작 방식과 관련된 이론적인 설명 중심으로 작성했습니다.

물론, 이론적인 설명이라 하기엔 생략된 부분들이 많습니다. 예를 들어 이력 테이블에 존재하는 REVTYPE 컬럼은 무엇을 의미하는지, Audited Table은 어떻게 생성하고 관리되는지, Revision Number는 어느 시점에 생성되는지 등등 자세한 설명은 생략되었습니다. 앞으로 작성될 포스트를 통해 제기된 궁금증들을 풀어갈 예정이며, Hibernate Envers를 실무에 적용했던 사례를 통해 이론보다는 사용법과 주의사항에 대해 자세히 설명하겠습니다.

- Audited Entity
- Custom Revision Entity
- EntityTrackingRevisionListener
- EventListenerRegistry


### 이력 테이블

### Envers 환경 구성

### 마무리


### 참고

- [jboss-docs-hibernate-4.1-Envers](https://docs.jboss.org/hibernate/core/4.1/devguide/en-US/html/ch15.html#envers-tracking-modified-entities-queries)
- [Spring DOC - Spring data](https://docs.spring.io/spring-data/data-commons/docs/current/api/org/springframework/data/annotation/package-frame.html)
- [Baeldung - Spring data annotations](https://www.baeldung.com/spring-data-annotations)
- [Hibernate-core - listeners](https://docs.jboss.org/hibernate/core/4.0/hem/en-US/html/listeners.html)