## ✅ Stream API란❓

---

> Stream API는 컬렉션, 배열 등 데이터 소스를 **연속적인 처리**와 **함수형 프로그래밍 스타일**로 처리할 수 있게 해주는 API이다.
>

### ✔️ 주요 개념

---

1. **Stream**
    - 스트림은 데이터의 흐름을 의미하며, 컬렉션이나 배열 같은 데이터를 연속적으로 처리하는 데 사용된다.
    - 스트림을 통해 데이터 요소들을 일련의 연산으로 필터링, 매핑, 정렬 등의 작업을 수행할 수 있다.
2. **함수형 프로그래밍**
    - Stream API는 람다 표현식과 함께 사용하며, 코드가 간결하고 가독성이 높아진다.
    - 데이터 처릴의 각 단계를 쉽게 읽고 이해할 수 있는 형태로 표현할 수 있다.
3. **중간 연산과 최종 연산**
    - **중간 연산**: 스트림의 요소를 가공하는 단계로, 연산이 바로 수행되지 않고 최종 연산이 호출될 때까지 지연된다.
        - ex, `filter()`, `map()`, `sorted()`
    - **최종 연산**: 스트림을 종료하고, 실제로 연산을 수행하여 결과를 반환한다.
        - ex, `collect()`, `forEach()`, `reduce()`

### ✔️코드로 구현해보기

---

> 1부터 10까지 있는 정수 배열을 stream으로 다루는 코드 작성❗
>

**1️⃣ 배열을 stream으로 만들어 요소를 모두 2배로 만든 배열을 반 후 원본 배열과 스트림 배열을 비교하기**

```java
List<Integer> arr = IntStream.range(1, 11).boxed().collect(Collectors.toList());
// 각 요소 2배씩
List<Integer> newArr = arr.stream().map(
  i -> i * 2
  ).collect(Collectors.toList());

arr.stream().forEach(num -> System.out.print(num + " "));
System.out.println();
newArr.stream().forEach(num -> System.out.print(num + " "));
>>> 1 2 3 4 5 6 7 8 9 10
    2 4 6 8 10 12 14 16 18 20 출력
```

**2️⃣ 배열 중 짝수만 4 + “is even number”와 같이 String으로 변환한 배열을 만들어 출력하기**

```java
List<Integer> arr = IntStream.range(1, 11).boxed().collect(Collectors.toList());
// 짝수만 뽑아서 조건에 맞게 변환
List<Integer> newArr = arr.stream()
	.filter(i -> i % 2 == 0)
	.map(i -> i + " is even number")
	.collect(Collectors.toList());

newArr.stream().forEach(str -> System.out.println(str));
>>> 2 is even number
		4 is even number
		6 is even number
		8 is even number
	 10 is even number 출력
```