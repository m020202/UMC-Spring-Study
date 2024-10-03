### ✅ 내가 진행 중, 진행 완료한 미션 모아서 보는 쿼리

```sql
SELECT m.reward, m.deadline, mission_spec 
FROM mission as m
JOIN member_mission as mm ON m.id = mm.mission_id
JOIN member as mem ON mm.member_id = mem.id
WHERE mm.status = 'IN_PROGRESS' OR mm.status = 'DONE'
LIMIT 15 OFFSET 0 * 15; 
```

### ✅ 리뷰 작성하는 쿼리

```sql
INSERT INTO review VALUES ('{member_id}', '{store_id}', '{body}', '{score}');
```

### ✅ 홈 화면 쿼리

```sql
SELECT s.name, m.mission_spec, m.deadline
FROM mission as m
         JOIN store as s ON m.store_id = s.id
         JOIN region as r ON s.region_id = r.id
         JOIN member_mission as mm ON m.id = mm.mission_id
WHERE r.name = '미추홀구'
  AND mm.member_id = '{해당 멤버 id}'
  AND mm.status = 'NOT_STARTED';
AND m.deadline > NOW()
ORDER BY m.deadline
LIMIT 15 OFFSET 0;
```

### ✅ 마이페이지 화면 쿼리

```sql
// 이름, 이메일 휴대폰 번호, 포인트 조회 쿼리
SELECT
    name,
    email,
    COALESCE(phone_num, '미인증') as phone_num,
    point
FROM member;
WHERE id = '{해당 멤버 id}';
```