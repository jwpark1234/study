## 1. Server Component
 - useState 안씀
 - DB 접근. axios, fetch 등
 - 이벤트 없음
 - 서버에서 실행
## 2. Client Component
 - useState, useEffect 사용
 - DB 접근 없음
 - 이벤트 사용가능
 - 브라우저에서 실행
## 3. use client
 - next.js는 기본이 server component라 서버에서 실행되는데 use client를 붙이면 브라우저에서 실행되게 강제할 수 있음
 - 이벤트 처리, useState, 브라우저 API 쓸때 use client 사용해야됨
## 4. 파일 기반 라우팅
```
app/
 ├─ page.tsx        👈 메인 페이지
 ├─ layout.tsx      👈 공통 레이아웃
 ├─ users/
 │   ├─ page.tsx    👈 /users
```
```
/       -> /app/page.tsx 연결
/users  -> /app/users/page.tsx 연결
```
