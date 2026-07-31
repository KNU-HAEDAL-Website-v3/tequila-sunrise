# 코딩 컨벤션

## 1. 명명 규칙

### 가. 표기법 기준

| 구분 | 표기법 | 예시 |
| --- | --- | --- |
| 클래스 | PascalCase | UserService, OrderController |
| 인터페이스 | PascalCase | UserRepository, Pageable |
| 메서드 | camelCase | getUserById(), createOrder() |
| 변수 | camelCase | userName, totalPrice |
| 상수 | UPPER_SNAKE_CASE | MAX_RETRY_COUNT, DEFAULT_PAGE_SIZE |
| 패키지 | 소문자 | com.haedal.user |
| DB 컬럼 | snake_case | user_name, created_at |

### 나. 명명 원칙
1) 의미 있는 이름 사용
가) data, info, temp 사용 금지
나) getUserList() 형태 권장

2) 약어 최소화
가) usr → user
나) 잘 알려진 약어 허용
다) URL, HTTP 등 허용

3) 불리언 접두사: is/has/can
가) isActive
나) hasPermission

---

## 2. 코드 구조 규칙

### 가. 클래스 구조 순서
1) 상수 필드
2) 인스턴스 필드
3) 생성자
4) public 메서드
5) private 메서드

### 나. 메서드 규칙
1) 단일 책임 원칙
2) 50줄 이내
3) 인자 3개 이하
가) 초과 시 객체로 묶기

### 다. 들여쓰기·공백 규칙
1) 들여쓰기 4칸
2) 탭 대신 스페이스
3) 줄 길이 120자 이내
4) 연산자 앞뒤 공백

---

## 3. 주석 규칙

### 가. 주석 작성 원칙
1) 코드 자체 설명 우선
2) 주석 의존 지양
3) '무엇'보다 '왜' 기술

### 나. Javadoc 규칙
1) public API 필수 작성
2) @param, @return 포함
3) @throws 포함

```java
/**
 * 사용자 ID로 사용자를 조회합니다.
 *
 * @param userId 조회할 사용자의 ID
 * @return 사용자 정보 DTO
 * @throws UserNotFoundException 사용자가 없을 때
 */
public UserResponseDto getUserById(Long userId) { ... }
```

### 다. 인라인 주석 규칙
1) 복잡한 로직에만 적용
2) 코드 옆에 위치
3) 2칸 띄고 // 형식

---

## 4. 린터·포맷터 설정

### 가. Java 프로젝트
1) Checkstyle
가) Google Style 적용
나) 빌드 시 자동 검사

2) IntelliJ 설정
가) 저장 시 자동 포맷
나) Import 자동 정렬

### 나. JavaScript/TypeScript 프로젝트
1) ESLint
가) airbnb 규칙 적용
2) Prettier
가) 저장 시 자동 포맷

### 다. .editorconfig 공통 설정
```ini
root = true

[*]
indent_style = space
indent_size = 4
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
```

---

## 5. 금지 사항

### 가. 코드 작성 금지 사항

| 금지 항목 | 이유 | 대안 |
| --- | --- | --- |
| System.out.println | 운영 로그 혼재 | Logger 사용 |
| 매직 넘버 사용 | 의미 불명확 | 상수 정의 |
| null 직접 반환 | NPE 유발 | Optional 또는 빈 컬렉션 반환 |
| catch (Exception e) 빈 블록 | 예외 묵살 | 로그 출력 또는 재처리 |
| 불필요한 주석 | 혼란 유발 | 삭제 |
