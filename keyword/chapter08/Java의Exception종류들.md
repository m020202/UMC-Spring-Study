# Java의 Exception 종류들

---

> 자바에서 예외는 프로그램 실행 중에 발생하는 문제를 나타내며, 이를 처리하여 프로그램의 비정상 종료를 방지할 수 있다. 예외는 크게 두가지로 분류된다.
>

## ✅ **Checked Exception (체크드 예외)**

체크드 예외는 **컴파일 타임**에 반드시 처리해야 하는 예외로, 메서드 시그니처에 **throws** 키워드로 명시해야 한다. 컴파일러가 이러한 예외의 처리를 강제한다.

### ✔️ **주요 체크드 예외:**

1. **IOException** : 입출력 작업 중 발생하는 예외
2. **SQLException** : 데이터베이스 작업 중 발생하는 예외
3. **ClassNotFoundException** : 클래스 찾을 수 없을 때 발생하는 예외

## ✅ **Unchecked Exception (언체크드 예외)**

언체크드 예외는 **런타임**에 발생하며, 컴파일러가 이러한 예외의 처리를 강제하지 않다. 대부분의 언체크드 예외는 프로그래밍 오류로 인해 발생한다.

### ✔️ **주요 언체크드 예외:**

1. **NullPointerException** : null 객체에 접근할 때 발생
2. **ArrayIndexOutOfBoundException** : 배열의 인덱스 범위를 벗어날 때 발생
3. **ArithmeticException** : 수학적 오류가 발생할 때 (ex, ZeroDivision)
4. **IllegalArgumentException** : 잘못된 인자가 메소드에 전달될 때 발생