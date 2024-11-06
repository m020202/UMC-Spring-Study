# @EntityGraph

---

연관관계가 있는 엔티티를 조회할 경우 지연 로딩으로 설정되어 있으면 연관관계에서 종속된 엔티티는 쿼리 실행 시 select 되지 않고, proxy 객체를 만들어 엔티티가 적용시킨다. 그 후 해당 프록시 객체를 호출할 때마다 그때그때 select 쿼리가 실행된다.

위와 같은 연관관계가 지연 로딩으로 되어 있을 경우 fetch 조인을 사용하여 여러 번의 쿼리를 한 번에 해결할 수 있다.

<aside>
🔑

**@EntityGraph**는 Spring Data JPA에서 fetch 조인을 **어노테이션**으로 사용할 수 있도록 만들어준 기능이다❗

</aside>

```java
public interface MemberRepository extends JpaRepository<Member, Long> {
	@EntityGraph(attributePaths = {"review"}) // 페치 조인 설정하기
    List<Member> findAll();
}
```

## ✅ @EntityGraph 사용 시 주의 사항

---

1. **필요한 경우에만 사용**

   모든 연관 엔티티를 즉시 로딩하면 성능에 영향을 줄 수 있으므로, 정말 필요한 경우에만 즉시 로딩을 적용해야 한다.

2. **복잡한 엔티티 그래프에 주의**

   다중 레벨의 연관관계에서 너무 많은 엔티티를 즉시 로딩하면 쿼리가 복잡해지고 성능이 저하될 수 있다.


## ✅ 정리

---

@EntityGraph는 페치 조인과 달리 선언만으로 간편하게 사용할 수 있고 페이징 쿼리와의 호환성에서도 더 유연하기에 유용한 도구이다