# Spring Data JPA의 페이징

---

> 페이징 기능은 대량의 데이터를 효율적으로 처리하고, 
데이터 조회 결과를 페이지 단위로 나누어 클라이언트에게 제공하는 기능이다.
> 

Spring Data JPA는 이를 위해 다양한 인터페이스와 클래스를 제공한다.

# ✅ Page

---

- **페이징 처리된 결과를 담고 있는** 인터페이스
- 페이지의 내용, 총 페이지 수, 현재 페이지 번호, 총 요소 수 등의 정보를 포함한다.

### ✔️ Page 인터페이스의 주요 기능

- **`getContent()`**: 현재 페이지에 포함된 엔티티의 리스트를 반환
- **`getNumber()`**: 현재 페이지 번호를 반환 (0부터 시작)
- **`getSize()`**: 페이지당 항목 수를 반환
- **`getTotalElements()`**: 전체 엔티티의 개수를 반환
- **`getTotalPages()`**: 전체 페이지 수를 반환
- **`hasContent()`**: 현재 페이지에 엔티티가 포함되어 있는지 여부를 반환
- **`hasNext()`**: 다음 페이지가 있는지 여부를 반환
- **`hasPrevious()`**: 이전 페이지가 있는지 여부를 반환
- **`isFirst()`**: 현재 페이지가 첫 번째 페이지인지 여부를 반환
- **`isLast()`**: 현재 페이지가 마지막 페이지인지 여부를 반환

### ✔️ **사용 예시**

```java
Page<Product> productsPage = productRepository.findAll(PageRequest.of(0, 10));

List<Product> products = productsPage.getContent(); // 현재 페이지의 엔티티 리스트
int currentPageNumber = productsPage.getNumber(); // 현재 페이지 번호
int pageSize = productsPage.getSize(); // 페이지당 항목 수
long totalElements = productsPage.getTotalElements(); // 전체 엔티티 개수
int totalPages = productsPage.getTotalPages(); // 전체 페이지 수
boolean hasNextPage = productsPage.hasNext(); // 다음 페이지 여부
boolean hasPreviousPage = productsPage.hasPrevious(); // 이전 페이지 여부
boolean isFirstPage = productsPage.isFirst(); // 첫 번째 페이지 여부
boolean isLastPage = productsPage.isLast(); // 마지막 페이지 여부
```

## ✅ Slice

- Page 인터페이스와 유사하게 페이징 처리된 결과를 표현하는데 사용하는 인터페이스
    
    하지만 Page와는 일부 차이점이 존재한다.
    

### ✔️ **Page 인터페이스와의 차이점**

1. 전체 페이지 수를 알 필요가 없는 경우.
2. 다음 페이지가 있는지 여부만 파악하고자 하는 경우

### ✔️ **주요 기능**

- **`getContent()`**: 현재 페이지에 포함된 엔티티의 리스트를 반환
- **`getNumber()`**: 현재 페이지 번호를 반환 (0부터 시작)
- **`getSize()`**: 페이지당 항목 수를 반환
- **`hasContent()`**: 현재 페이지에 엔티티가 포함되어 있는지 여부를 반환
- **`hasNext()`**: 다음 페이지가 있는지 여부를 반환
- **`isFirst()`**: 현재 페이지가 첫 번째 페이지인지 여부를 반환
- **`isLast()`**: 현재 페이지가 마지막 페이지인지 여부를 반환

→ Page 인터페이스에서 전체 페이지 or 엔티티 개수를 담고 있는 기능, 이전 페이지 존재 여부에 대한 기능만 빠졌다고 생각하면 된다.