## ✅ Valid란❓

---

> 자바에서 **Bean Validation**을 사용하여 **객체의 유효성을 검사**할 때 사용되는 어노테이션.
>
- `@Valid` 어노테이션을 이용하면, 객체 안에서 들어오는 값에 대해 검증이 가능해진다.
- 주로 **메서드의 파라미터**나 **클래스 필드**에 적용되어, 해당 객체나 필드의 **유효성을 검사**한다.

## ✅ 주요 사용 예시

---

### 1️⃣ **메소드 파라미터에 사용**

```java
@PostMapping("/user")
public ResponseEntity<String> createUser(@Valid @RequestBody User user, BindingResult result) {
    if (result.hasErrors()) {
        return ResponseEntity.badRequest().body("Invalid user data");
    }
    // 유효성 검사를 통과한 후의 로직
    return ResponseEntity.ok("User created");
}
```

- 여기서 `@Valid`는 ‘**User**’ 객체의 필드들이 정의된 유효성 조건을 만족하는지 검사
- 값이 올바르게 들어오지 않았다면 `MethodArgumentNotValidException` 예외와 `400 Bad Request` 상태코드를 반환하게 된다.

### 2️⃣ **클래스 필드에 사용**

```java
public class User {
    @NotNull(message = "Name cannot be null")
    private String name;

    @Min(value = 18, message = "Age should not be less than 18")
    private int age;

    // getters and setters
}
```

- `@NotNull` 및 `@Min` 등의 어노테이션이 적힌 필드의 유효성을 정의

## ✅ 검증 어노테이션 종류

---

### 1️⃣ 문자열 검증

- `@NotBlank` - null이 아니고 공백이 아닌 문자를 하나 이상 포함해야한다.
- `@NotEmpty` - null이거나 empty가 아니어야 한다.
- `@NotNull` - null이 아닌 어떤 타입이든 상관 없다.
- `@Null` - 타입 상관없으며 null 값 허용한다.

### 2️⃣ 최대 / 최소 검증

- `@DecimalMax` - 지정된 최댓값보다 작거나 같아야 한다.
- `@DecimalMin` - 지정된 최솟값보다 크거나 같아야 한다.

### 3️⃣ Boolean 검증

- `@AssertTrue` - 항상 True 여야 한다.
- `@AssertFalse` - 항상 False 여야 한다.