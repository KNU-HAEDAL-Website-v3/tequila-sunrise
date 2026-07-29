# 기술 스택

## 1. 프론트엔드

### 가. 핵심 프레임워크

| 기술 | 버전 | 역할 |
| --- | --- | --- |
| React | 18.x | UI 컴포넌트 |
| TypeScript | 5.x | 타입 안전성 |
| Vite | 5.x | 번들러·개발 서버 |

### 나. 상태 관리

| 기술 | 용도 |
| --- | --- |
| Zustand | 전역 클라이언트 상태 |
| TanStack Query | 서버 상태·캐싱·동기화 |

### 다. UI 라이브러리

| 기술 | 역할 |
| --- | --- |
| Tailwind CSS | 유틸리티 CSS |
| shadcn/ui | 기본 UI 컴포넌트 |

### 라. 개발 도구

| 기술 | 역할 |
| --- | --- |
| ESLint | 코드 정적 분석 |
| Prettier | 코드 포맷 |
| Vitest | 단위 테스트 |

---

## 2. 백엔드

### 가. 핵심 프레임워크

| 기술 | 버전 | 역할 |
| --- | --- | --- |
| Java | 21 (LTS) | 언어 |
| Spring Boot | 3.3.x | 웹 프레임워크 |
| Spring Security | 6.x | 인증·인가 |
| Spring Data JPA | 3.x | ORM |

### 나. 인증·인가

| 기술 | 역할 |
| --- | --- |
| JWT (jjwt 0.12.x) | 액세스·리프레시 토큰 |
| Spring Security | 필터 체인 관리 |

### 다. 빌드 도구
1) Gradle
2) Kotlin DSL
3) build.gradle.kts

---

## 3. 데이터베이스

### 가. 주 데이터베이스

| 기술 | 버전 | 역할 |
| --- | --- | --- |
| MySQL | 8.0.x | 메인 RDB |
| HikariCP | (Spring Boot 내장) | 커넥션 풀 |
| Flyway | 9.x | 스키마 버전 관리 |

### 나. 보조 데이터베이스

| 기술 | 역할 |
| --- | --- |
| Redis | 세션·캐시·토큰 블랙리스트 |

### 다. ORM 규칙
1) JPA 사용
가) 쿼리메서드 우선 적용
나) 복잡 쿼리: JPQL
다) 성능 최적화 쿼리: QueryDSL
라) 직접 SQL: 최후 수단

2) N+1 문제 방지
가) FetchType.LAZY 기본 설정
나) 필요 시 fetch join 적용
다) Batch Size 설정

---

## 4. 인프라·배포

### 가. 컨테이너

| 기술 | 역할 |
| --- | --- |
| Docker | 컨테이너 패키징 |
| Docker Compose | 로컬 개발 환경 구성 |

### 나. CI/CD

| 기술 | 역할 |
| --- | --- |
| GitHub Actions | 빌드·테스트 자동화 |
| Docker Hub | 컨테이너 이미지 저장소 |

### 다. 클라우드

| 기술 | 역할 |
| --- | --- |
| AWS EC2 | 애플리케이션 서버 |
| AWS RDS | 관리형 MySQL |
| AWS S3 | 파일 저장 |
| AWS CloudFront | CDN |

---

## 5. 협업·문서화

### 가. API 문서

| 기술 | 역할 |
| --- | --- |
| Swagger (SpringDoc) | API 명세 자동 생성 |

1) /api-docs 경로 확인
2) @Operation 어노테이션 적용
3) 전체 엔드포인트 등록 필수

### 나. 형상 관리

| 기술 | 역할 |
| --- | --- |
| GitHub | 코드 저장소·PR 관리 |
| GitHub Projects | 이슈 트래킹 |

### 다. 테스트

| 기술 | 역할 |
| --- | --- |
| JUnit 5 | 백엔드 단위·통합 테스트 |
| Mockito | Mock 객체 |
| Testcontainers | DB 통합 테스트 |
| Vitest | 프론트엔드 단위 테스트 |

---

## 6. 버전 선택 기준

### 가. 원칙
1) LTS 버전 사용
2) 보안 패치 반영
3) 팀 합의 후 업그레이드
4) 주요 변경 사항 문서화
