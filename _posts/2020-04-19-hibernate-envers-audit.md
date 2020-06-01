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

- 최근 이력 데이터에 대해서만 알 수 있다.
- 삭제된 데이터를 알 수 없다.

다음 문제점들을 해결하기 위해선 이력 데이터를 추적할 테이블을 관리해야 됩니다. 하지만 기존의 테이블 외에 별도의 테이블을 생성하여 관리한다는 건 쉽지 않습니다. Hibernate에선 이러한 상황들을 고려하여 별도로 Hibernate Envers 프로젝트를 제공해주고 있습니다. 우선 다음 프로젝트 더욱 쉽게 이력 데이터를 관리할 수 있습니다. 본 포스팅에선 Hibernate Envers를 활용하여 이력 데이터를 관리하는 방법에 대해 소개해드리겠습니다.

>- [Hibernate Envers를 활용한 이력관리](https://gmoon92.github.io/spring/hibernate/envers/2020/01/02/hibernate-envers-concepts.html) 
>- [Spring Data JPA의 이력 유형 데이터 관리](https://gmoon92.github.io/spring/hibernate/audited/2020/04/10/spring-data-audit.html)


# 학습 목표

- Hibernate Envers 사용법과 이해
    - 이력 테이블 생성 방법
- Audited Entity과 Revision Table 이해

## 1. Hibernate Envers
## Database Auditing 지원

Hibernate Envers는 [Database Auditing](https://docs.oracle.com/cd/B19306_01/network.102/b14266/auditing.htm#CHDJBDHJ)를 쉽게 대처하기 위해 고안된 프로젝트입니다.
 
Audit는 감사(監査)라는 의미로 무언가 감독하고 감시하다라는 의미를 지니고 있습니다.
 
 ORM 관점에서 Database Auditing는 영속성 컨텍스트에 관련된 엔티티들의 기록들을 추적하는것을 의미합니다. Hibernate Envers는 이러한 Database Auditing을 하기 위해, 엔티티의 버전 관리를 하기 위한 프로젝트라 생각하시면 됩니다. 이 프로젝트는 SQL 트리거에서 아이디어를 얻어 개발되었기 때문에, 엔티티의 삽입/수정/삭제 이벤트가 발생할 때 동작하게 됩니다. 따라서 Hibernate Envers는 Database Auditing의 이점을 소스 단위에서 제어할 수 있다는 장점이 있습니다.

## Audtied Table과 Revision Table

Hibernate Envers를 활성화하기 위해선, 가장 먼저 [hibernate-envers](https://mvnrepository.com/artifact/org.hibernate/hibernate-envers/5.4.16.Final) 라이브러리를 pom.xml 추가하여 프로젝트에 의존성을 주입시켜야 됩니다.

``` xml
<!-- https://mvnrepository.com/artifact/org.hibernate/hibernate-envers -->
<dependency>
    <groupId>org.hibernate</groupId>
    <artifactId>hibernate-envers</artifactId>
    <version>5.4.16.Final</version>
</dependency>
```

[1] 다음으로 엔티티 객체에 org.hibernate.envers.Audited 애노테이션을 선언해줍니다.

``` java
@Entity
@Audited //[1] 데이터 감사를 하겠다는 의미
public class Member {

    @Id
    @GeneratedValue
    private Long id;
    
    private String name;
}
```

그 다음 프로젝트를 실행하면, 아래 그림처럼 Hibernate Envers에 의해 이력 테이블(*_AUD)과 함께 REVINFO라는 개정 테이블(Revision Table)이 생성됩니다.

![img](/md/img/hibernate/envers/audited-table-in-hibernate-envers.png)

개정 테이블이란 엔티티의 이력 버전을 관리하는 테이블로 Envers를 설정하게 되면 필수적으로 생성되는 테이블입니다. 개정 테이블 정보는 다음과 같습니다.

- REV : 개정 번호(PK)
- REVTSMP : 생성일자

Member 테이블의 이력 테이블 정보는 다음과 같습니다.

- REV : 개정 테이블의 PK
- REVTYPE : 개정 유형
    - 삽입 : 0
    - 수정 : 1
    - 삭제 : 2

## 2. Envers Config Properties

기본적으로 이력 테이블은 *_AUD라는 규칙으로 생성됩니다. 만약 이력 테이블 명을 커스텀하고 싶다면, org.hibernate.envers.audit_table_suffix 프로퍼티 값을 설정하여 변경해주면 됩니다.

``` xml
# hibernate envers prop
org.hibernate.envers.audit_table_suffix=_h
```

이외에 Hibernate Envers의 프로퍼티 값은 다음과 같습니다.

|  Property | default | 비고 |
|:---:|:---:|:---:|
|org.hibernate.envers.audit_table_prefix| |엔티티 이름을 작성하기 위해 감사 된 엔티티 이름 앞에 추가되어 감사 정보를 보유 할 문자열입니다.|
|org.hibernate.envers.audit_table_suffix|_AUD|감사 정보를 보유 할 엔티티 이름을 작성하기 위해 감사 엔티티 이름에 추가 될 문자열입니다.|
|org.hibernate.envers.revision_field_name|REV|개정 번호를 보유 할 감사 엔티티의 필드 이름.|
|org.hibernate.envers.revision_type_field_name|REVTYPE|개정 유형을 보유 할 감사 엔티티의 필드 이름|
|org.hibernate.envers.revision_on_collection_change|true|mappedBy 속성을 사용하는 필드를 감사한다. (OneToMany 관계에서의 Collection 또는 OneToOne 관계)|
|org.hibernate.envers.do_not_audit_optimistic_locking_field|true|true 인 경우, 주석이 달린 낙관적 락 사용되는 속성 @Version은 자동으로 감사되지 않습니다 (이력은 저장되지 않으며 일반적으로 저장하는 것이 의미가 없습니다).|

## 3. 이력 데이터 조회
## AuditReader.find()

Hibernate Envers 프로젝트를 통해 이력 데이터를 조회할 수 있는 여러 방식중에 org.hibernate.envers.AuditReader를 사용하여 조회하는 방식을 살펴봅시다.

``` java
AuditReader auditReader = AuditReaderFactory.get(entityManager);
Member auditMember = auditReader.find(Member.class, entityId, revisionNumber);
```

- find(Class<T> entityClass, Object primaryKey, Number revision)

다음 메서드는 자동으로 삭제 개정 유형을 제외한 최신 이력 데이터를 조회하게 됩니다.

조건을 추가하여 조회하고 싶은 경우엔 AuditQuery를 사용해야 합니다. AuditQuery는 AuditReader 객체를 사용하여 반환받아 사용할 수 있습니다. 

## AuditQuery 질의문의 다양한 조건절

``` java
AuditReader auditReader = AuditReaderFactory.get(entityManager);
AuditQuery query = auditReader.createQuery()
                              .forRevisionsOfEntity(Member.class, false, true);
```

- forRevisionsOfEntity(Class<?> entityClass, boolean selectEntitiesOnly, boolean selectDeletedEntities)

일반적으로 AuditQuery 조건에 다음 3 가지 메서드를 사용하여 이력 데이터를 조회 조건을 추가할 수 있습니다.

1. AuditEntity.revisionNumber() : 개정 번호에 대한 조건
2. AuditEntity.revisionType() : 개정 유형(ADD, MOD, DEL) 조건
3. AuditEntity.property() : 엔티티 프로퍼티에 대한 조건

``` java
Number revisionNumber = (Number) getAuditReader().createQuery()
        .forRevisionsOfEntity(Member.class, true, false)
        .addProjection(AuditEntity.revisionNumber().max())
        .add(AuditEntity.id().eq(entityId))
        .add(AuditEntity.revisionType().eq(RevisionType.ADD))
        .add(AuditEntity.property("name").eq("gmoon"))
        .getSingleResult();
```

다음 개정 번호를 반환하는 코드를 해석하자면 최근 삽입된 개정 데이터 중에 사용자 이름이 gmoon인 개정 번호를 반환한다라고 해석할 수 있습니다. 보시다시피 Envers 쿼리는 Hibernate Criteria와 유사하기 때문에 다양한 조건을 어렵지 않게 추가할 수 있습니다.

## 4. 이력 데이터 저장

Hibernate Envers는 트랜잭션이 커밋을 하게 되면, 다음과 같은 동작 방식으로 데이터를 저장하게 됩니다.    

1. Entity 테이블 저장
2. REV 테이블 저장
3. AUD 테이블 저장

Envers의 저장하는 방식은 트랜잭션 단위로 개정 테이블에 저장하는 특징이 있습니다.

예를 들어 동일한 트랜잭션 범위에서 Member 테이블과 Team 테이블을 동시에 수정하게 된다면, 하나의 개정 번호로 데이터를 저장하게 됩니다. 

## 5. Revision Table 커스텀

이제 Revision Table를 소스 베이스에서 변경하는 방식에 대해 소개해드리겠습니다.

기본적으로 Envers를 설정하게 되면 Hibernate에 의해 REVINFO 라는 개정 테이블이 생성됩니다.

|Column|설명|
|---|---|
|REV|개정 테이블의 기본 키로써 int/Integer 또는 long/Long 타입만 설정 가능|
|REVTSTMP|long/Long 또는 java.util.Date 타입으로만 설정 가능|

> 왜 개정 생성 일자 타입엔 Time API(JDK8)를 사용할 수 없을까? 다음과 같은 의문이 있다면 아래 링크를 참고하자.
> - https://hibernate.atlassian.net/browse/HHH-10827
> - https://hibernate.atlassian.net/browse/HHH-10828
> - https://hibernate.atlassian.net/browse/HHH-10496

이러한 개정 테이블에 부가적인 데이터를 쌓기 위해선 org.hibernate.envers.RevisionEntity 애노테이션을 사용하면 됩니다. 

``` java
@Entity
@Table(name = "REVISION_HISTORY")
@RevisionEntity
public class RevisionHistory extends DefaultRevisionEntity {

    @Column(name = "username")
    private String username;
}
```

예를 들어 어느 회원이 엔티티를 변경했는지 알고 싶다면 다음 코드와 같이 @Column 애노테이션을 사용하여 지정만 해주시면 됩니다.

![img](/md/img/hibernate/envers/revision_entity_custom.png)

다음으로 누가 엔티티를 수

이벤트 리스너를 등록하여 개정 엔티티 



개정 테이블을 커스텀하기 위해 이벤트 리스너를 등록하면 




/**
 * life cycle
 * 1. @Audited @Entity save/update/delete
 * 2. EntityTrackingRevisionListener.newRevision()
 * 3. call next value for hibernate_sequence
 * 4. HistoryRevision.id 존재 -> entityChanged()
 * 5. @RevisionEntity save
 * 6. AUD Table save
 * 7. @HistoryRevisionDetail save
 */


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