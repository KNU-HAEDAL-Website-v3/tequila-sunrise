# 아키텍처

## 1. 레이어드 아키텍처

### 가. 계층 구성
1) Presentation 계층
가) Controller
나) HTTP 요청 수신
다) 응답 형식 반환

2) Business 계층
가) Service
나) 핵심 비즈니스 로직 처리
다) 트랜잭션 관리

3) Persistence 계층
가) Repository
나) 데이터 접근
다) 쿼리 실행

4) Domain 계층
가) Entity
나) 도메인 모델
다) 비즈니스 상태 보유

### 나. 의존성 방향
1) 단방향 의존성 유지
가) Controller → Service 참조
나) Service → Repository 참조
다) 역방향 참조 금지
라) 순환 참조 금지

2) Domain 계층 독립
가) 상위 계층 참조 불가
나) 모든 계층에서 참조 가능

---

## 2. 패키지 구조

### 가. 도메인 기반 구성
1) 기능별 패키지 분리
가) user 패키지
나) product 패키지
다) order 패키지

2) 각 패키지 내 구성
가) controller
나) service
다) repository
라) dto
마) entity

### 나. 공통 패키지 구성
1) common 패키지
가) exception
나) config
다) util

---

## 3. DTO와 Entity 분리

### 가. Entity 규칙
1) DB 테이블 대응
2) 외부 직접 노출 금지
3) 비즈니스 메서드 포함

### 나. DTO 규칙
1) 요청: RequestDto
2) 응답: ResponseDto
3) Entity 래핑
4) 계층 간 데이터 전달

| 구분 | 위치 | 역할 | 비고 |
| --- | --- | --- | --- |
| Entity | Domain 계층 | DB 매핑 | 외부 노출 금지 |
| RequestDto | Presentation 계층 | 요청 수신 | 입력 검증 포함 |
| ResponseDto | Presentation 계층 | 응답 전달 | 필요 필드만 포함 |

---

## 4. 예외 처리 구조

### 가. 공통 예외 클래스
1) CustomException 정의
2) ErrorCode enum 작성
3) 코드·메시지 포함

### 나. GlobalExceptionHandler
1) @ControllerAdvice 적용
2) 전체 예외 일괄 처리
3) 통일된 응답 형식 반환

### 다. 응답 형식
```json
{
  "success": false,
  "errorCode": "USER_NOT_FOUND",
  "message": "사용자를 찾을 수 없습니다."
}
```

---

## 5. API 설계 규칙

### 가. REST 원칙
1) 리소스 중심 URL 설계
2) HTTP 메서드 구분
가) GET: 조회
나) POST: 생성
다) PUT: 전체 수정
라) PATCH: 부분 수정
마) DELETE: 삭제

### 나. URL 규칙
1) 소문자·하이픈 사용
2) 복수형 명사 사용
3) 동사 사용 금지

| 구분 | 좋은 예 | 나쁜 예 |
| --- | --- | --- |
| 리소스 URL | /users | /getUser |
| 단어 구분 | /user-profiles | /userProfiles |
| 중첩 리소스 | /users/{id}/orders | /getUserOrders |
