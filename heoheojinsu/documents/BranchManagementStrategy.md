# 브랜치 관리 전략

## 1. Git Flow 전략

### 가. 브랜치 종류

| 브랜치 | 역할 | 삭제 여부 |
| --- | --- | --- |
| main | 운영 배포용 브랜치 | 영구 유지 |
| develop | 개발 통합 브랜치 | 영구 유지 |
| feature/* | 기능 개발 브랜치 | 머지 후 삭제 |
| hotfix/* | 긴급 버그 수정 브랜치 | 머지 후 삭제 |
| release/* | 배포 준비 브랜치 | 머지 후 삭제 |

### 나. 브랜치 보호 규칙
1) main 보호 규칙
가) 직접 push 금지
나) PR만 허용
다) 리뷰 1인 이상 필수
라) CI 통과 후 머지

2) develop 보호 규칙
가) 직접 push 금지
나) PR만 허용

---

## 2. 브랜치 네이밍 규칙

### 가. 접두사 규칙

| 접두사 | 설명 | 예시 |
| --- | --- | --- |
| feat/ | 기능 추가 | feat/user-login |
| fix/ | 버그 수정 | fix/token-null-error |
| hotfix/ | 긴급 수정 | hotfix/payment-crash |
| refactor/ | 리팩토링 | refactor/user-service |
| docs/ | 문서 작업 | docs/api-guide |
| chore/ | 설정·빌드 작업 | chore/gradle-update |
| test/ | 테스트 작성 | test/user-service |

### 나. 명명 규칙
1) 소문자·하이픈 사용
2) 이슈 번호 포함
가) 예: feat/23-user-login
3) 30자 이내
4) 한글 사용 금지

---

## 3. 커밋 메시지 규칙

### 가. 구조
```
<type>(<scope>): <subject>

<body>

<footer>
```

### 나. type 종류

| type | 설명 |
| --- | --- |
| feat | 새로운 기능 추가 |
| fix | 버그 수정 |
| docs | 문서 수정 |
| style | 포맷·공백 등 코드 무관 변경 |
| refactor | 리팩토링 (기능 변경 없음) |
| test | 테스트 추가·수정 |
| chore | 빌드·설정 변경 |

### 다. 커밋 메시지 규칙
1) subject 50자 이내
2) 명령형 현재 시제
3) 마침표 금지
4) 영어 작성

### 라. 예시
```
feat(auth): add JWT refresh token

- 리프레시 토큰 생성 로직 추가
- 토큰 만료 시 자동 갱신 처리

Closes #42
```

---

## 4. Pull Request 규칙

### 가. PR 생성 기준
1) 기능 단위 PR 생성
2) 단일 목적 유지
3) 변경 파일 10개 이내

### 나. PR 제목 규칙
1) 커밋 type 접두사 부착
2) 이슈 번호 포함
가) 예: [feat] #23 로그인 기능 추가

### 다. PR 설명 항목
1) 변경 내용 기술
2) 테스트 방법 기술
3) 스크린샷 첨부
4) 관련 이슈 링크

### 라. 코드 리뷰 규칙
1) 승인자 1인 이상 필수
2) 요청 후 24시간 내 리뷰
3) 이유 명시 필수
4) 비난 금지

---

## 5. 머지 전략

### 가. develop으로 머지
1) Squash and Merge
가) 커밋 단일화
나) 히스토리 간결화

### 나. main으로 머지
1) Merge Commit
가) 배포 이력 보존

### 다. 머지 후 처리
1) feature 브랜치 삭제
2) 이슈 종료
