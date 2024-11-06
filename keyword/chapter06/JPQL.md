# JPQL

---

> JPQL 은 JPA에서 사용되는 **객체 지향 쿼리 언어**이다. JPQL은 SQL과 비슷하지만, SQL은 데이터베이스 테이블을 대상으로 하는 반면, JPQL은 **JPA 엔티티**(즉, 자바 클래스) 및 해당 엔티티의 **속성**(필드)을 대상으로 쿼리한다.
>

JPQL을 사용하면 SQL의 기능을 객체지향 방식으로 수행할 수 있으며, **데이터베이스 독립적인 쿼리**를 작성할 수 있다.

## ✅ 주요 특징

---

1. **객체 지향 쿼리**

   JPQL은 데이터베이스 테이블 대신 자바 엔티티 객체를 대상으로 쿼리한다. 예를 들어, SQL에서는 `SELECT * FROM Member`처럼 테이블을 조회하지만, JPQL에서는 `SELECT m FROM Member m`과 같이 엔티티 클래스를 조회한다.

2. **SQL과 유사**

   JPQL의 문법은 SQL과 매우 유사하지만, JPQL은 데이터베이스에 직접적으로 존재하는 테이블이 아니라 JPA 엔티티에 매핑된 객체를 대상으로 작업한다. 이는 JPA가 관리하는 객체를 기반으로 쿼리를 작성하는 방식이다.

3. **쿼리의 결과는 엔티티 객체**

   JPQL은 `SELECT`문을 통해 결과를 조회할 때, **엔티티 객체**를 반환한다. 즉, SQL에서 결과를 `ResultSet` 형태로 받는 것과 달리, JPQL은 **자바 객체**를 반환한다.


## ✅ JPQL 문법

---

### 1. 기본 SELECT 쿼리

```java
SELECT m FROM Member m
```

- `SELECT m`은 `Member` 엔티티 객체 `m`을 조회하는 쿼리이다.
- `FROM Member m`은 `Member` 엔티티로부터 데이터를 조회하고, `m`은 엔티티의 별칭이다.

### 2. WHERE 조건을 사용하는 쿼리

```java
SELECT m FROM Member m WHERE m.name = :name
```

- `m.name = :name`은 `name` 필드가 주어진 파라미터와 일치하는 `Member` 엔티티를 조회하는 조건이다.

### 3. JPQL의 JOIN

JPQL에서도 SQL과 유사하게 **조인**을 사용할 수 있다. 하지만 SQL의 `JOIN`과 다르게, JPQL에서는 **엔티티 관계**를 기준으로 조인을 한다.

```java
SELECT m FROM Member m JOIN m.reviews r WHERE r.score > 80
```

- `JOIN m.reviews r`은 `Member` 엔티티와 연관된 `reviews` 컬렉션을 조인한다. 즉, `Member`와 `Review` 엔티티 간의 관계를 기준으로 데이터를 조회한다.

### 4. SELECT 절에서 특정 필드만 조회

```java
SELECT m.name, m.age FROM Member m
```

- 위 쿼리는 `Member` 엔티티에서 `name`과 `age` 필드만 조회한다. 반환되는 값은 **결과 목록**으로, 각 항목은 `Object[]` 배열이다.

### 5. ORDER BY, GROUP BY

```java
SELECT m FROM Member m ORDER BY m.name ASC
```

- `ORDER BY`는 쿼리 결과를 특정 속성에 의해 정렬할 때 사용된다. 위 예제는 `Member` 엔티티를 `name` 속성에 따라 오름차순으로 정렬한다.

```java
SELECT m.country, COUNT(m) FROM Member m GROUP BY m.country
```

- `GROUP BY`는 데이터를 그룹화하여 통계 정보를 조회할 때 사용한다.

## ✅ JPQL의 제한 사항

---

- **테이블 조작**

  JPQL은 데이터베이스 테이블을 직접 조작하지 않는다. 즉, `INSERT`, `UPDATE`, `DELETE`와 같은 작업은 `JPQL` 대신 **JPA 메서드**(예: `EntityManager.persist()`, `EntityManager.remove()`, `EntityManager.merge()`를 사용한다.

- **기본 제공되는 집합 함수**

  `COUNT()`, `AVG()`, `SUM()`, `MAX()`, `MIN()` 등의 집합 함수는 지원하지만, SQL에서처럼 복잡한 집합 연산이나 특정 데이터베이스에서만 지원하는 기능은 JPQL에서 사용할 수 없다.


## ✅ JPQL과 SQL의 차이점

---

| **특징** | **JPQL** | **SQL** |
| --- | --- | --- |
| **대상** | 엔티티 클래스 (자바 객체) | 데이터베이스 테이블 |
| **쿼리 결과** | 엔티티 객체 또는 DTO | 테이블의 행 (Row) |
| **필드/속성** | 엔티티의 속성 (필드) | 테이블의 컬럼 |
| **동작 대상** | 자바 객체와 객체 관계 | 데이터베이스 테이블과 관계 |
| **집합 함수** | `COUNT`, `AVG`, `SUM`, `MAX`, `MIN` 등 지원 | SQL 표준 함수들 지원 |