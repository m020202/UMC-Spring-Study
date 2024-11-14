# RestControllerAdvice

---

> **예외를 전역적으로 처리**하기 위해 사용되는 어노테이션.
>
- `@ControllerAdvice`와 유사하지만, `@RestController`와 함께 사용되며, JSON 형식의 응답을 반환하는 데에 중점을 둔다.

## ✅ 어노테이션 구성 요소

---

1. **@ControllerAdvice 기반**

   **@ControllerAdvice**는 스프링 애플리케이션의 특정 계층에 대해 예외 처리를 담당하는 클래스에서 사용된다. 즉, 지정된 컨트롤러 클래스에 예외가 발생했을 때 그 예외를 한 곳에서 일괄적으로 처리할 수 있다.

2. **@ResponseBody 기능 포함**

   `@RestControllerAdvice`는 자동으로 @ResponseBody가 포함되어 있어서, 예외 발생 시 JSON 또는 XML 형식으로 응답을 반환한다.

   `@ControllerAdvice`에 `@ResponseBody`를 추가한 형태라고 생각하기❗

3. **annotations 속성**

   `annotations = {RestController.class}` 부분은 **@RestControllerAdvice** 가 **@RestController**가 붙은 클래스에만 적용됨을 의미한다.


<aside>
🔑

예외 처리 흐름에 대해서 알아보기 전에 **@ExceptionHandler**부터 알아보자❗

</aside>

## ✅ @ExceptionHandler란❓

---

> `@ExceptionHandler`는 스프링 프레임워크에서 특정 예외를 처리하기 위해 사용되는 어노테이션이다.
>
- try-catch 구문 작성 없이 해당 어노테이션만으로 매우 유연하고 간단하게 예외처리를 할 수 있게 해준다.
- 이 어노테이션으로 특정 예외를 잡아서, 해당 예외가 발생했을 때 어떻게 응답할지를 정의하는 메서드를 지정할 수 있다.

### ✔️ 주요 기능 및 사용 방법

---

1. **특정 예외 처리**

   `@ExceptionHandler`는 메서드에 적용되어서 특정 예외 클래스를 처리하도록 지정한다.

   예외가 발생하면 컨트롤러 내부에서 스프링이 `@ExceptionHandler` 메서드를 찾아 예외를 처리한다.

2. **적용 범위**
    - 일반적으로는 `@Controller` 또는 `@RestController` 클래스 내부에서 사용된다.
    - `@ControllerAdvice` 혹은 `@RestControllerAdvice`와 함께 사용하면, 여러 컨트롤러에서 발생하는 예외를 전역적으로 처리할 수 있다.

### ✔️ 사용 예제

---

```java
@RestController
public class MyController {

    @GetMapping("/example")
    public String example() {
        if (true) {  // 예제에서 예외를 발생시키기 위해 항상 true로 설정
            throw new IllegalArgumentException("Invalid argument passed!");
        }
        return "Success!";
    }

    // 예외 처리 메서드
    @ExceptionHandler(IllegalArgumentException.class)
    public ResponseEntity<String> handleIllegalArgumentException(IllegalArgumentException ex) {
        return ResponseEntity.badRequest().body("Error: " + ex.getMessage());
    }
}
```

- 이렇게 컨트롤러 내부에서 정의해서 사용할 수 있다.

## ✅ 우리가 실습했던 코드에서 예외 처리 흐름 살펴보기

---

> 스프링에서 ExceptionAdvice가 @RestControllerAdvice로 등록되어 있다면,
GeneralException이 발생했을 때 이 예외가 ExceptionAdvice로 전달되는 구조는 다음과 같다.
>

### 1️⃣ 예외 발생

`throw new GeneralException(에러코드)`가 발생하면 스프링MVC는 이를 캐치하고, 해당 예외를 처리할 수 있는 핸들러를 찾기 위해서 **@ControllerAdvice(@RestControlllerAdvice)**로 선언된 클래스와 매핑을 시도한다.

- ExceptionAdvice 클래스가 @ControllerAdvice 어노테이션으로 등록되어 있다면, 전역 예외 처리기로 동작한다.

### 2️⃣ @ExceptionHandler 메서드 탐색

`ExceptionAdvice` 클래스 안에 `@ExceptionHandler(GeneralException.class)` 어노테이션으로 **GeneralException**을 처리하는 메서드를 정의하면, **GeneralException**이 발생할 때 해당 메서드가 자동으로 호출된다.

- 즉, 우리가 생성한 GeneralException 클래스 내에 onThrowException이 호출됨❗

```java
@ExceptionHandler(value = GeneralException.class)
public ResponseEntity onThrowException(GeneralException generalException, HttpServletRequest request) {
   ErrorReasonDTO errorReasonHttpStatus = generalException.getErrorReasonHttpStatus();
   return handleExceptionInternal(generalException,errorReasonHttpStatus,null,request);
}
```

**❓메서드 호출 시 의존성 주입**

- 적절한 메서드를 찾았다고 하자. **그런데 어떻게 매개변수로 우리가 throw new로 생성한 GeneralException을 넣어줄까❓**

  → **Spring이 해당 예외 객체를 메서드에 자동으로 주입하기 때문**❗


### 3️⃣ onThrowException 메서드

이 메서드는 `GeneralException` 타입의 예외와 `HttpServletRequest`를 매개변수로 받는다.

`GeneralException`에서 예외 상태 정보를 담고 있는 `ErrorReasonDTO` 객체를 가져온다.

이후 `handleExceptionInternal` 메서드를 호출해 실제 응답을 생성한다.

### 4️⃣ handleExceptionInternal 메서드

이 메서드는 `GeneralException` 발생 시 반환할 응답 본문과 상태 코드를 포함하는 `ResponseEntity`를 생성하는 역할을 한다.

- `ApiResponse.onFailure()` 메서드를 호출해서 응답 본문을 설정한다.
- `super.handleExceptionInternal` 메서드는 `ResponseEntityExceptionHandler` 클래스에서 제공되며, 에러 발생 시 기본적인 HTTP 응답을 생성하는 기능을 가지고 있다.