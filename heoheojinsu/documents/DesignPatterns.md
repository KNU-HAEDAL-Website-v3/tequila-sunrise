# 디자인 패턴

## 1. 생성 패턴

### 가. Builder 패턴
1) 복잡한 객체 생성 시 적용
2) 선택적 필드가 많은 경우
3) 불변 객체 생성
4) Lombok @Builder 활용

```java
// 좋은 예
User user = User.builder()
    .name("홍길동")
    .email("hong@example.com")
    .role(Role.USER)
    .build();

// 나쁜 예 (텔레스코핑 생성자)
User user = new User("홍길동", "hong@example.com", Role.USER, null, null);
```

### 나. Factory 패턴
1) 객체 생성 로직 은닉
2) 타입별 분기 처리

```java
// 알림 타입에 따라 생성
Notification notification = NotificationFactory.create(type, message);
```

### 다. Singleton 주의사항
1) 직접 구현 금지
2) Spring Bean으로 위임
3) @Component 적용
4) 무상태(Stateless) 유지
가) 상태 보유 시 멀티스레드 문제 발생

---

## 2. 구조 패턴

### 가. Repository 패턴
1) 데이터 접근 추상화
2) 인터페이스 정의
3) 구현체 분리
4) 테스트 용이성 확보

```java
// 인터페이스 정의
public interface UserRepository extends JpaRepository<User, Long> {
    Optional<User> findByEmail(String email);
}
```

### 나. DTO 패턴
1) 계층 간 데이터 전달
2) Entity 직접 노출 금지
3) 요청·응답 분리

| 클래스 | 방향 | 역할 |
| --- | --- | --- |
| UserCreateRequest | 클라이언트 → 서버 | 생성 요청 데이터 |
| UserResponse | 서버 → 클라이언트 | 응답 데이터 |

### 다. Facade 패턴
1) 복잡한 서브시스템 은닉
2) 단순한 인터페이스 제공
3) 여러 서비스 조합

---

## 3. 행동 패턴

### 가. Strategy 패턴
1) 알고리즘 교체 가능 구조
2) if-else 분기 최소화
3) 인터페이스로 전략 정의

```java
// 결제 전략 예시
PaymentStrategy strategy = PaymentStrategyFactory.of(paymentType);
strategy.pay(amount);
```

### 나. Observer 패턴
1) 이벤트 기반 처리
2) Spring ApplicationEvent 활용
3) 느슨한 결합 구조

```java
// 이벤트 발행
eventPublisher.publishEvent(new UserCreatedEvent(user));

// 이벤트 구독
@EventListener
public void onUserCreated(UserCreatedEvent event) { ... }
```

### 다. Template Method 패턴
1) 공통 흐름: 상위 클래스 정의
2) 세부 처리: 하위 클래스 구현

---

## 4. 예외 처리 패턴

### 가. 사용자 정의 예외
1) RuntimeException 상속
2) ErrorCode enum 활용
3) 도메인별 예외 분리

```java
public class UserNotFoundException extends BusinessException {
    public UserNotFoundException(Long userId) {
        super(ErrorCode.USER_NOT_FOUND, "userId: " + userId);
    }
}
```

### 나. ErrorCode 정의

| 코드 | HTTP 상태 | 메시지 |
| --- | --- | --- |
| USER_NOT_FOUND | 404 | 사용자를 찾을 수 없습니다. |
| INVALID_INPUT | 400 | 잘못된 입력값입니다. |
| UNAUTHORIZED | 401 | 인증이 필요합니다. |
| FORBIDDEN | 403 | 접근 권한이 없습니다. |
| DUPLICATE_EMAIL | 409 | 이미 사용 중인 이메일입니다. |

### 다. GlobalExceptionHandler
1) @RestControllerAdvice 적용
2) 공통 응답 형식 반환
3) 전체 예외 일괄 처리

---

## 5. 금지 패턴

### 가. 안티패턴

| 안티패턴 | 문제점 | 대안 |
| --- | --- | --- |
| God Object | 클래스가 너무 많은 역할 | 단일 책임 원칙 적용 |
| Magic Number | 의미 불명확 숫자 | 상수화 |
| Shotgun Surgery | 변경 시 여러 파일 수정 | 응집도 높이기 |
| 서비스에서 직접 HTTP 호출 | 계층 혼재 | FeignClient 또는 별도 클라이언트 |
| Controller에 비즈니스 로직 | 테스트 어려움 | Service로 이동 |
