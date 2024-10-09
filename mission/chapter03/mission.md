## ☑️ 홈 화면

---

### ✅ **API Endpoint**

<aside>
🔑

**GET /api/home**

</aside>

### **✅ Request Body**

- **없음**

### **✅ Request Header**

```yaml
Authorization: Bearer <access_token> // 인증 토큰 값
Accept: application/json // 서버가 클라이언트에게 응답할 데이터 형식
User-Agent: PostmanRuntime/7.41.1 // 요청을 보내는 클라이언트 정보
```

### **✅ Query String**

- **없음**

## ☑️ 마이페이지 리뷰 작성

---

### ✅ **API Endpoint**

<aside>
🔑

**POST /api/users/review**

</aside>

### **✅ Request Body**

```json
{
	 "body" : "너무 맛있어요!",
	 "score" : "4.5"
}
```

### **✅ Request Header**

```yaml
Authorization: Bearer <access_token> // 인증 토큰 값
Content-Type: application/json // 요청의 본문 데이터 형식
Accept: application/json // 서버가 클라이언트에게 응답할 데이터 형식
User-Agent: PostmanRuntime/7.41.1 // 요청을 보내는 클라이언트 정보
```

### **✅ Query String**

- **없음**

## ☑️ 미션 목록 조회

---

### ✅ **API Endpoint**

<aside>
🔑

**GET /api/users/missions**

</aside>

### **✅ Request Body**

- **없음**

### **✅ Request Header**

```yaml
Authorization: Bearer <access_token> // 인증 토큰 값
Accept: application/json // 서버가 클라이언트에게 응답할 데이터 형식
User-Agent: PostmanRuntime/7.41.1 // 요청을 보내는 클라이언트 정보
```

### **✅ Query String**

---

⏩ **진행 중인 미션 조회**

<aside>
🔑

**?status = IN_PROGRESS**

</aside>

⏩ **진행 완료한 미션 조회**

<aside>
🔑

**?status = DONE**

</aside>

## ☑️ 회원 가입

---

### ✅ **API Endpoint**

<aside>
🔑

**POST /api/users**

</aside>

### **✅ Request Body**

```json
{
	"name" : "J",
	"gender" : "MALE",
	"age" : 24,
	"address" : "미추홀구 용현동",
	"spec_address" : "177-12번지 3층",
	"email" : "m020202@naver.com"
}
```

### **✅ Request Header**

```yaml
Content-Type: application/json // 요청의 본문 데이터 형식
Accept: application/json // 서버가 클라이언트에게 응답할 데이터 형식
User-Agent: PostmanRuntime/7.41.1 // 요청을 보내는 클라이언트 정보
```

### **✅ Query String**

- **없음**