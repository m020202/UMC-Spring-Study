## ✅ 제네릭 (Generics)

---

> 제네릭은 클래스, 인터페이스 또는 메서드에 **타입 매개변수 <T>**를 도입하는 기능이다.
>
- 즉, 타입이 클래스 내부에서 지정되는 것이 아닌 **외부에서 사용자에 의해 지정된다.**
- 이를 통해, **데이터 타입을 일반화**하여 **코드의 재사용성을 높이고**, **컴파일 타임에 타입 체크를 통해 타입 안전성을 제공**한다.

### ✔️ 예시 코드

---

> 만약, 리스트를 사용할 때 `Integer` 하나만 받을 수 있는 리스트와 `String`만 받을 수 있는 리스트를 따로 만들지 않고, 다음과 같이 제네릭을 사용하여 하나의 리스트로 다양한 타입을 처리할 수 있다.
>

```java
import java.util.ArrayList;
import java.util.List;

public class GenericExample<T> {
    private List<T> list = new ArrayList<>();

    public void add(T element) {
        list.add(element);
    }

    public T get(int index) {
        return list.get(index);
    }
}
```

- list 변수는 속성 타입이 아직 가지지 않고, **실제 컴파일 시점에 add() 되는 값에 따라서 정해진다.**

## ✅ 래퍼 클래스

---

> 자바의 **기본형(primitive type)을 객체로 다루기 위해** 제공되는 클래스.
>
- 자바의 기본형은 값만 저장하지만, 객체로 다루어야 하는 경우(컬렉션, 제네릭 등)에 래퍼 클래스를 활용하여 해당 기본형을 객체로 감쌀 수 있다.

### ✔️ 자바에서 제공하는 주요 기본형과 래퍼 클래스

---

| 기본형 (Primitive Type) | 래퍼 클래스 (Wrapper Class) |
| --- | --- |
| `byte` | `Byte` |
| `short` | `Short` |
| `int` | `Integer` |
| `long` | `Long` |
| `float` | `Float` |
| `double` | `Double` |
| `char` | `Character` |
| `boolean` | `Boolean` |

### ✔️ 래퍼 클래스를 사용하는 주요 이유

---

1. **컬렉션 (Collection) 사용**
    - 자바의 컬렉션 (List, Set, Map 등)은 객체만 다룰 수 있기 떄문에, 기본형을 객체로 변환해야 한다.

        ```java
        List<Integer> list = new ArrayList<>();
        list.add(1); 
        ```

      → 위에처럼 래퍼 클래스 대신 기본형 값만 넣어도, **자동으로 변환해준다(오토 박싱)**

2. **유틸리티 메서드 제공**
    - 래퍼 클래스는 기본형을 다룰 때 추가적인 기능을 제공한다.
    - `Integer.parseInt(String s)`

      : 문자열을 기본형 `int`로 변환해주는 메서드.

    - `Boolean.valueOf(String s)`

      : 문자열을 `Boolean`으로 변환해주는 메서드.


### ✔️ 오토 박싱과 언박싱

---

**오토 박싱이란❓**

: **기본형을 래퍼 클래스의 객체로 자동 변환**하는 과정이다.

- 개발자가 명시적으로 객체 변환을 하지 않아도 기본형을 래퍼 클래스로 자동 감싸서 객체로 변환한다.

```java
int num = 10;
Integer wrapperNum = num; <- 기본형 int가 Integer 객체로 자동 변환
```

**오토 언박싱이란❓**

: **래퍼 클래스의 객체를 다시 기본형으로 자동 변환**하는 과정이다.

```java
Integer wrapperNum = Integer.valueOf(1);
int num = wrapperNum; <- Integer 객체가 기본형 int로 자동 변환
```

## ✅ Optional

---

> Optional은 **null 값으로 인해 발생할 수 있는 문제를 방지**하기 위해 사용되는 클래스이다.
>
- 주로 값이 있을 수도, 없을 수도 있는 상황에서 이를 안전하게 처리할 수 있도록 도와준다.

### ✔️ 주요 메서드

---

**1️⃣ Optional.of(T value)**

: null이 아닌 값을 가진 Optional 객체를 생성한다. (값이 null이면 `NullPointerException` 던진다)

```java
Optional<String> optional = Optional.of("Hello");
```

**2️⃣ Optional.orElse(T other)**

: 값이 있으면 그 값을 반환하고, 값이 없으면 **다른 대체 값을 반환**한다.

```java
String result = optional.orElse("Default Value");
```

**3️⃣ Optional.orElseThrow(Supplier<? extends X> exceptionSupplier)**

: 값이 없을 때 예외를 던진다. (다양한 의미있는 예외 가능)

```java
String result = optional.orElseThrow(() -> new IllegalArgumentException("값이 없음"));
```

### ✔️ Optional 사용 이유

---

1. **NullPointerException 예방**

   : 자바에서 null은 매우 흔한 원인으로 예기치 않은 예외를 발생시킬 수 있다.

    - Optional을 사용하면, null 값을 명시적으로 다루게 되어서 더욱 안전하다.
2. **명확한 의미 전달**

   : 메서드의 반환 값이 null 일 수도 있음을 명시적으로 나타낼 수 있다.

    - 예를 들어, DB 조회 시 값이 없을 수 있음을 Optional로 반환하여, 이 상황을 명확히 처리하도록 유도할 수 있다.