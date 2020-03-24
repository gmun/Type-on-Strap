---
layout: post
title: "Spring Data JPA의 Audit, Hibernate Envers의 @Audited"
tags: [Spring, JPA, Hibernate, Spring Data JPA, Envers]
categories: [Spring, Hibernate, Envers]
subtitle: "엔티티의 이력유형 데이터 모델링"
feature-img: "md/img/thumbnail/hibernate-envers.png"
thumbnail: "md/img/thumbnail/hibernate-envers.png"
excerpt_separator: <!--more-->
sitemap:
changefreq: daily

priority: 1.0
---

<!--more-->

# 엔티티의 데이터 이력관리
# 2. 엔티티의 이력유형 데이터 모델링

---

# 들어가기전

 데이터베이스에서 이력 데이터 모델링은 실무에서 중요한 부분이라 할 수 있습니다.

![그림]()

우선 위의 테이블 모델링을 살펴보시면 낯설지 않게 느끼실 수 있습니다. 아무래도 생성자, 생성일자, 수정자, 수정일자 컬럼들은 테이블을 구성할 때 관례적으로 배치하는 칼럼들이라 생각합니다. 이는 누가 테이블의 데이터를 저장하고 수정 또는 삭제 했는지에 대해 추적할 수 있는 밑걸음이라 생각합니다.

이러한 칼럼의 유형을 이력유형이라 합니다.

 



 
 JPA를 사용하는 프로젝트에선 이러한 

실무를 하다 중요한 데이터를 누가 삭제했는지 추적을 해야될 경우가 생겼지만 이러한 장치들의 부재로 


지난 [Hibernate Envers 이론편](https://gmoon92.github.io/spring/hibernate/envers/2020/01/02/hibernate-envers-concepts.html) 포스팅에서 엔티티의 이력 데이터에 대한 간략히 개념적인 부분들을 살펴보았습니다. 본 포스팅에선 개념적인 부분 보단 코드 중심으로 글을 작성했으며, 이력 데이터 관리에 대한 주제의 첫 걸음이라 생각하시면 되겠습니다.


다음 이력유형 컬럼들은 

 이력 데이터에 대한 관리 방법에 대해 설명드리도록 하겠습니다.

`엔티티의 이력유형 데이터 모델링`라는 주제에 대해 작성하려합니다.
 
 Hibernate Envers를 들어가기전에 엔티티의 이력유형 데이터 모델링이라는 주제에 대해 설명드리려합니다.

# 학습 목표

- Spring Data JPA의 Audit
- Hibernate Envers의 @Audited

## 1. Spring Data JPA의 Audit

우선 엔티티의 데이터를 누가 언제 생성/변경했는지에 대해 알 수 있도록 관리하는 방법을 소개해드리려 합니다.

Spring은 데이터를 쉽게 처리할 수 있도록 `org.springframework.data.annotation` 패지키를 제공하고 있습니다. 이 패키지에는 @CreatedBy, @CreatedDate, @LastModifiedBy, @LastModifiedDate라는 애노테이션이 존재하며 네이밍 그대로 생성자, 생성일자, 마지막 수정자, 마지막 수정일자를 의미합니다.

- org.springframework.data.annotation.CreatedBy
- org.springframework.data.annotation.CreatedDate
- org.springframework.data.annotation.LastModifiedBy
- org.springframework.data.annotation.LastModifiedDate

이제 Spring 데이터 애노테이션들을 활용하여 간단히 엔티티 데이터에 대한 이력을 관리할 수 있도록 구성해보도록 하겠습니다.

``` java
@Entity
public class Member {

    @Id
    @GeneratedValue
    private Long id;

    private String name;

    private int age;

    @ManyToOne
    private Team team;

    @CreatedBy
    private Long createdBy;

    @CreatedDate
    private LocalDateTime createdDt;

    @LastModifiedBy
    private Long modifiedBy;

    @LastModifiedDate
    private LocalDateTime modifiedDt;
}
```

예제 코드인 만큼 간단히 Member 엔티티를 구성해봤습니다.

하지만 해당 코드는 원했던 방향과 다르게 동작하지 않습니다. 해당 애노테이션을 활성화하기 위해선 몇 가지 작업들이 부가적으로 필요합니다.

![img](/md/img/hibernate/envers/spring-data-annotation-not-work.png)

다음 로그를 보시면 Member 테이블의 지정된 칼럼들이 null로 들어가는 걸 확인해보실 수 있습니다.

## 1.1. Audit Listener 등록 및 활성화

Spring Data 애노테이션을 활성화하기 위해선 javax.persistence.EntityListeners 애노테이션이 필요합니다.

참고로 @EntityListeners는 해당 패키지를 보시면 아시겠지만, Spring에서 지원하는 패키지가 아닌 JPA의 표준 규격 패키지입니다. 



## 1.2. mapped superclass 구성




## 2. Hibernate Envers의 @Audited


# 앞으로 진행될 내용

지금까지 Hibernate Envers에 대한 대략적인 개념과 동작 방식과 관련된 이론적인 설명 중심으로 작성했습니다.

물론, 이론적인 설명이라 하기엔 생략된 부분들이 많습니다. 예를 들어 이력 테이블에 존재하는 REVTYPE 컬럼은 무엇을 의미하는지, Audited Table은 어떻게 생성하고 관리되는지, Revision Number는 어느 시점에 생성되는지 등등 자세한 설명은 생략되었습니다. 앞으로 작성될 포스트를 통해 제기된 궁금증들을 풀어갈 예정이며, Hibernate Envers를 실무에 적용했던 사례를 통해 이론보다는 사용법과 주의사항에 대해 자세히 설명하겠습니다.

- Audited Entity
- Custom Revision Entity
- EntityTrackingRevisionListener
- EventListenerRegistry

# 참고

- [jboss-docs-hibernate-4.1-Envers](https://docs.jboss.org/hibernate/core/4.1/devguide/en-US/html/ch15.html#envers-tracking-modified-entities-queries)
- [Spring DOC - Spring data](https://docs.spring.io/spring-data/data-commons/docs/current/api/org/springframework/data/annotation/package-frame.html)
- [Baeldung - Spring data annotations](https://www.baeldung.com/spring-data-annotations)