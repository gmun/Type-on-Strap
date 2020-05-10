---
layout: post
title: "Hibernate Second Level Cache"
tags: [Spring, JPA, Hibernate, Spring Data JPA,Second-Level-Cache]
categories: [Spring, Hibernate, Cache]
subtitle: "로컬 메모리를 활용한 성능 개선"
feature-img: "md/img/thumbnail/hibernate-envers.png"
thumbnail: "md/img/thumbnail/hibernate-envers.png"
excerpt_separator: <!--more-->
sitemap:
changefreq: daily

priority: 1.0
---

<!--more-->

# 하이버네이트 2차 캐시(Second-Level Cahche, L2 Cache)

---

## 들어가기전

다른 ORM 프레임워크와 마찬가지로, 하이버네이트는 1차 캐시 개념이 있다.

1차 캐시는 영속성 컨텍스트에서 엔티티 객체가 한번만 로드 되도록 하는 세션 범위를 의미한다. 따라서 세션이 닫히면 1차 캐시도 종료됨으로 엔티티 인스턴스와 상호 독립적으로 작업할 수 있는 이유이기도 하다. 하지만 1차 캐시는 일반적인 웹 어플리케이션에선 트랜잭션이 시작하고 종료할 때까지만 유효하기 때문에, 어플리케이션 전체적인 관점에선 데이터베이스의 접근 회수를 획기적으로 줄이지는 못한다.

네트워크를 통해 데이터베이스에 접근하는 시간 비용은 애플리케이션 서버에서 내부 메모리에 접근하는 시간 비용보다 수만에서 수십만 배 이상 비싸다. 따라서 데이터베이스 접근 횟수를 줄이면 애플리케이션 성능을 획기적으로 개선할 수 있게 된다.

# 학습 목표

- Hibernate 2차 캐시의 이해
- Hibernate 2차 캐시의 사용법

### 동작 방식

하이버네이트에선 공유 캐시(Shared Cache) 또는 2차 캐시(Second-Level Cache, L2 Cache)라는 애플리케이션 범위의 캐시를 지원한다. 2차 캐시 범위는 SessionFactory-scoped이며, 2차 캐시에 저장된 데이터를 동일한 세션 팩토리의 모든 세션과 공유하게 된다. 만약 2차 캐시가 활성화 된 경우, 엔터티를 조회할 때 다음과 같은 동작 방식으로 진행한다.

1. 엔티티가 1차 캐시에 있으면, 1차 캐시에서 반환한다.
2. 1차 캐시에 엔티티가 없다면, 2차 캐시에서 찾고 엔티티를 반환한다.
3. 2차 캐시에 엔티티가 없다면, 데이터베이스에 접근하여 데이터 조회 후 결과를 2차 캐시에 저장한다. 2차 캐시에 저장된 데이터 결과를 1차 캐시에 복사하고, 복사된 데이터를 반환한다.

> 2차 캐시가 캐시한 데이터를 직접반환하지 않고 복사하는 이유는 동시성을 극대화하기 위함이다. 만약 직접 캐시한 데이터를 여러군데에서 수정할 경우 락을 걸어야 하는데 이러한 경우 동시성이 떨어질 수 있다.

### 특징

2차 캐시는 애플리케이션 범위 캐시로써 애플리케이션이 종료될 때까지 캐시를 유지하는 특징을 지니고 있다. 그 외 2차 캐시의 특징은 다음과 같다.

- 영속성 유닛 범위의 캐시다.
- 조회한 엔티티 객체를 반환하는것이 아닌 복사본을 생성하여 반환한다.
- 영속성 컨텍스트가 다르면 객체 동일성(a == b)를 보장하지 않는다.
- JPA 2.0부터 2차 캐시 표준을 정의했다.

### 2차 캐시 구현

2차 캐시를 사용하려면 javax.persistence.Cacheable 애노테이션을 사용하면 된다.

``` java
package javax.persistence;
@Target( { TYPE })
@Retention(RUNTIME)
public @interface Cacheable {
    boolean value() default true;
}
```

다음 엔티티 객체에 @Cacheable 애노테이션을 선언해주자.

``` java
@Cacheable
@Entity
public class Member {
	
	@Id @GeneratedValue
	private Long id;
	...
}
```

스프링 프레임워크에서 XML 캐시 설정은 다음과 같다.

``` xml
<bean id="entityManagerFactory" class="org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean">
	<property name="sharedCacheMode" value="ENABLE_SELECTIVE"/>
	...
```

캐시 모드는 아래 객체에서 확인해볼 수 있다.

``` java
package javax.persistence;

// 캐시 모드
public enum SharedCacheMode {
    ALL, // 모든 엔티티에 캐시 적용
    NONE, // 캐시 미적용
    ENABLE_SELECTIVE, // Cacheable(true)로 설정된 엔티티만 캐시 적용
    DISABLE_SELECTIVE, // 모든 엔티티 캐시 적용, 단 Cacheable(false)인 엔티티는 미적용
    UNSPECIFIED; // JPA 구현체가 정의한 설정에 의해 캐시 적용

    private SharedCacheMode() {
    }
}
```

### 캐시 조회 모드와 보관 모드

캐시를 무시하고 직접 데이터베이스에서 조회 또는 캐시를 갱신하려면 캐시 조회 모드와 캐시 보관 모드를 사용하면 된다.

``` java
em.setProperty("javax.persistence.cache.retrieveMode", CacheRetrieveMode.BYPASS);
```

- javax.persistence.cache.retrieveMode : 캐시 조회 모드 프로퍼티 이름
- javax.persistence.cache.stroeMode : 캐시 보관 모드 프로퍼티 이름

옵션 클래스들은 다음과 같다.

``` java
package javax.persistence;

public enum CacheRetrieveMode {
    USE,
    BYPASS;

    private CacheRetrieveMode() {
    }
}
```

캐시 조회 모드 설정 옵션

- USE : 캐시에서 조회한다. 기본값
- BYPASS : 캐시를 무시하고 데이터베이스에 직접 접근한다.

``` java
package javax.persistence;

public enum CacheStoreMode {
    USE,
    BYPASS,
    REFRESH;

    private CacheStoreMode() {
    }
}
```

캐시 보관 모드 설정 옵션

- USE : 조회한 데이터를 캐시에 저장한다. 조회한 데이터가 이미 캐시에 있으면 캐시 데이터를 최신상태로 갱신하지 않는다. 트랜잭션을 커밋하면 등록/수정한 엔티티도 캐시에 저장한다. 기본값
- BYPASS : 캐시에 저장하지 않는다.
- REFRESH : USE 전략에 추가로 데이터베이스에서 조회한 엔티티를 최신 상태로 다시 캐시한다.

### 설정 범위

캐시 모드는 엔티티 매니저 단위로 설정하거나, EntityManager.find(), EntityManager.reflesh()에 설정할 수 있다. 

- 엔티티 매니저
- find(), reflesh()
- Query.setHint() (TypeQuery 포함)

``` java
// 엔티티 매니저 설정 범위
em.setProperty("javax.persistence.cache.retrieveMode", CacheRetrieveMode.BYPASS);
em.setProperty("javax.persistence.cache.storeMode", CacheRetrieveMode.BYPASS);

// find()
Map<String, Object> param = new HashMap<String, Object>();
param.put("javax.persistence.cache.retrieveMode", CacheRetrieveMode.BYPASS);
param.put("javax.persistence.cache.storeMode", CacheRetrieveMode.BYPASS);

em.find(Member.class, id. param);

// JPQL
em.createQuery("select m from Member m where m.id = :id", Member.class)
	.setParameter("id", id)
	.setHint("javax.persistence.cache.retrieveMode", CacheRetrieveMode.BYPASS)
	.setHint("javax.persistence.cache.storeMode", CacheRetrieveMode.BYPASS)
	.getSingleResult();
```

### JPA Cache API

JPA에선 캐시를 관리하기 위해 Cache 인터페이스를 제공하고 있다. Cache는 EntityManagerFactory에서 구할 수 있다.

``` java
Cache cache = emf.getCache();
boolean contains = cache.contains(Member.class, member.getId);
log.debug("contains = {}", contains);
```

JPA 표준 Cache 인터페이스 기능은 다음과 같다.

``` java
package javax.persistence;

public interface Cache {

		// 해당 엔티티가 캐시에 있는지 여부 확인
    public boolean contains(Class cls, Object primaryKey);

		// 해당 엔티티중 특정 식별자를 가진 엔티티를 캐시에서 제거
    public void evict(Class cls, Object primaryKey);

		// 해당 엔티티 전체를 캐시에서 제거
    public void evict(Class cls);

		// 모든 캐시 데이터 제거
    public void evictAll();

		//JPA Cache 구현체 조회
    public <T> T unwrap(Class<T> cls);
```


### & EHCAHE

### 마무리

### 참고

- [jboss-docs-hibernate-4.1-Envers](https://docs.jboss.org/hibernate/core/4.1/devguide/en-US/html/ch15.html#envers-tracking-modified-entities-queries)
- [Spring DOC - Spring data](https://docs.spring.io/spring-data/data-commons/docs/current/api/org/springframework/data/annotation/package-frame.html)
- [Baeldung - Spring data annotations](https://www.baeldung.com/spring-data-annotations)
- [Hibernate-core - listeners](https://docs.jboss.org/hibernate/core/4.0/hem/en-US/html/listeners.html)