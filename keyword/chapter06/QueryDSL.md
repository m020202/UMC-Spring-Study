# QueryDSL

---

> **QueryDSL**은 자바에서 타입 안전한 쿼리를 작성할 수 있도록 지원하는 라이브러리이다.
>
- SQL, JPQL, HQL 등을 동적으로 작성하는 데 도움이 되며, 특히 **JPA**와 **Hibernate**와 함께 많이 사용된다.
- **QueryDSL**의 주된 목적은 쿼리 생성 및 실행을 **타입 안전**(compile-time 검사를 통한 오류 예방)하게 만들어주는 것이다.
  이를 통해 쿼리 작성 시 발생할 수 있는 오류를 컴파일 시점에 미리 검출할 수 있다.

## ✅ 주요 특징

---

1. **타입 안전성 (Type Safety)**:
    - QueryDSL은 SQL이나 JPQL을 문자열로 직접 작성하는 대신, **자바 코드**로 쿼리를 작성할 수 있도록 한다. 이로 인해 컴파일 시점에서 쿼리의 오류를 미리 발견할 수 있다.
2. **자바 기반 쿼리 생성**:
    - QueryDSL을 사용하면 자바 객체를 기반으로 쿼리를 작성할 수 있다. 이로 인해 **동적 쿼리**를 작성하거나 복잡한 조건을 생성하는 것이 용이해진다.
3. **SQL, JPQL, JQL 등 지원**:
    - QueryDSL은 SQL, JPQL, HQL 등 다양한 쿼리 언어를 지원하며, 사용자가 선택한 데이터베이스와 기술 스택에 맞게 쿼리를 작성할 수 있다.
4. **단일 쿼리 인터페이스**:
    - SQL, JPQL 등의 쿼리 문법을 통합하여 **단일 인터페이스**에서 처리할 수 있도록 도와준다. 즉, 쿼리 언어에 관계없이 동일한 방식으로 쿼리를 작성하고 할 수 있다.

## ✅ **QueryDSL 쿼리 작성 예시**

---

**기본 SELECT 쿼리**:

```java
JPAQueryFactory queryFactory = new JPAQueryFactory(entityManager);
QMember member = QMember.member;

List<Member> members = queryFactory
    .selectFrom(member)          // `select * from Member`
    .fetch();                    // 쿼리 실행

```

**WHERE 조건을 포함한 쿼리**:

```java
List<Member> members = queryFactory
    .selectFrom(member)
    .where(member.name.eq("John")) // `WHERE name = 'John'`
    .fetch();

```

**동적 쿼리 작성**:

```java
BooleanBuilder builder = new BooleanBuilder();

if (name != null) {
    builder.and(member.name.eq(name));
}
if (email != null) {
    builder.and(member.email.eq(email));
}

List<Member> members = queryFactory
    .selectFrom(member)
    .where(builder)
    .fetch();

```

**JOIN 쿼리**:

```java
QOrder order = QOrder.order;

List<Member> members = queryFactory
    .select(member)
    .from(member)
    .join(member.orders, order)  // `JOIN member.orders`
    .where(order.status.eq(OrderStatus.DELIVERED))
    .fetch();

```

**GROUP BY, HAVING 쿼리**:

```java
List<Tuple> result = queryFactory
    .select(member.name, member.email.count())
    .from(member)
    .groupBy(member.name)
    .having(member.email.count().gt(1))
    .fetch();

```

## ✅ **동적 쿼리** (`BooleanBuilder` 사용)

---

동적 쿼리를 작성할 때 `BooleanBuilder`를 사용하여 조건을 동적으로 추가할 수 있다.

```java
BooleanBuilder builder = new BooleanBuilder();

if (status != null) {
    builder.and(order.status.eq(status));
}
if (minPrice != null) {
    builder.and(order.price.goe(minPrice));
}

List<Order> orders = queryFactory
    .selectFrom(order)
    .where(builder)
    .fetch();

```

## ✅ **Pageable을 사용한 페이징 쿼리**

---

`QueryDSL`은 `Pageable`을 활용한 페이징 기능도 쉽게 지원한다.

```java
Pageable pageable = PageRequest.of(0, 10);

List<Member> members = queryFactory
    .selectFrom(member)
    .offset(pageable.getOffset())   // OFFSET 설정
    .limit(pageable.getPageSize())  // LIMIT 설정
    .fetch();

```