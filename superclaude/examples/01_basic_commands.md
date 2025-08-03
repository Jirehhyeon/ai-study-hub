# SuperClaude 기본 명령어 예제

## 1. 프로젝트 설계 (`/sc design`)

### 예제 1: 웹 스크래퍼 설계

```bash
/sc design 웹사이트에서 뉴스 기사를 수집하는 Python 스크래퍼를 만들어주세요. 
다음 기능이 필요합니다:
- 여러 뉴스 사이트 지원
- 제목, 본문, 날짜 추출
- CSV/JSON 형식으로 저장
- 중복 제거 기능
```

**SuperClaude가 수행하는 작업:**
1. 프로젝트 구조 설계
2. 필요한 라이브러리 선정 (BeautifulSoup, requests 등)
3. 클래스 다이어그램 생성
4. 기본 코드 스켈레톤 작성

### 예제 2: REST API 서버 설계

```bash
/sc design 사용자 인증 기능이 있는 Todo List REST API 서버를 설계해주세요.
요구사항:
- JWT 인증
- CRUD 기능
- 사용자별 Todo 관리
- PostgreSQL 데이터베이스
```

---

## 2. 기능 구현 (`/sc implement`)

### 예제 1: 특정 기능 추가

```bash
/sc implement 위에서 만든 웹 스크래퍼에 다음 기능을 추가해주세요:
- 프록시 서버 지원
- User-Agent 로테이션
- 재시도 로직 (3회까지)
- 로깅 시스템
```

### 예제 2: UI 컴포넌트 구현

```bash
/sc implement React로 다크모드 토글 버튼을 구현해주세요.
- 시스템 설정 감지
- localStorage에 설정 저장
- 부드러운 전환 애니메이션
- 접근성 고려 (ARIA 속성)
```

---

## 3. 체크포인트 관리 (`/sc checkpoint` & `/sc rollback`)

### 체크포인트 생성

```bash
# 기본 기능 구현 후
/sc checkpoint "기본 CRUD 구현 완료"

# 인증 기능 추가 후
/sc checkpoint "JWT 인증 시스템 추가"

# UI 개선 후
/sc checkpoint "반응형 디자인 적용"
```

### 롤백 사용

```bash
# 이전 체크포인트로 되돌리기
/sc rollback

# 특정 체크포인트로 되돌리기
/sc rollback "기본 CRUD 구현 완료"
```

---

## 4. 코드 개선 (`/sc improve`)

### 예제 1: 성능 최적화

```bash
/sc improve 현재 코드의 성능을 개선해주세요.
특히 다음 부분에 집중해주세요:
- 데이터베이스 쿼리 최적화
- 캐싱 전략 구현
- 비동기 처리 개선
```

### 예제 2: 코드 품질 향상

```bash
/sc improve --focus readability
- 함수명과 변수명 개선
- 복잡한 로직 분리
- 주석 추가
- 타입 힌트 추가 (Python)
```

---

## 5. 분석 (`/sc analyze`)

### 예제 1: 전체 프로젝트 분석

```bash
/sc analyze --comprehensive
```

**분석 결과 예시:**
- 코드 복잡도 측정
- 보안 취약점 검사
- 성능 병목 지점 식별
- 의존성 분석
- 테스트 커버리지

### 예제 2: 특정 측면 분석

```bash
/sc analyze --focus security
# 보안 중심 분석

/sc analyze --focus performance
# 성능 중심 분석
```

---

## 6. 문제 해결 (`/sc troubleshoot`)

### 예제 1: 오류 해결

```bash
/sc troubleshoot 
"TypeError: Cannot read property 'map' of undefined 오류가 발생합니다.
UserList 컴포넌트에서 발생하는 것 같습니다."
```

### 예제 2: 성능 문제 해결

```bash
/sc troubleshoot
"API 응답이 너무 느립니다. 평균 3초 이상 걸리고 있습니다.
특히 사용자 목록을 불러올 때 문제가 심합니다."
```

---

## 7. 코드 정리 (`/sc cleanup`)

### 사용 예시

```bash
/sc cleanup
```

**정리 작업:**
- 사용하지 않는 import 제거
- 죽은 코드 제거
- 콘솔 로그 제거
- 포맷팅 정리
- 중복 코드 제거

---

## 8. 설명 요청 (`/sc explain`)

### 예제 1: 기술 개념 설명

```bash
/sc explain "React의 useEffect와 useLayoutEffect의 차이점"
```

### 예제 2: 코드 설명

```bash
/sc explain "현재 프로젝트의 인증 플로우를 설명해주세요"
```

---

## 9. 빌드 및 배포 (`/sc build`)

### 예제 1: Python 애플리케이션

```bash
/sc build --target exe
# Windows 실행 파일 생성

/sc build --target docker
# Docker 이미지 생성
```

### 예제 2: 웹 애플리케이션

```bash
/sc build --production
# 프로덕션 빌드 생성
# - 코드 최소화
# - 환경 변수 설정
# - 빌드 최적화
```

---

## 10. 문서화 (`/sc document`)

### 예제 1: API 문서 생성

```bash
/sc document --type api
# OpenAPI/Swagger 문서 생성
```

### 예제 2: 사용자 가이드 생성

```bash
/sc document --type user-guide --lang ko
# 한국어 사용자 가이드 생성
```

---

## 💡 고급 사용 팁

### 1. 연속 명령어 사용

```bash
# 프로젝트 생성부터 배포까지
/sc design "이미지 압축 도구"
/sc implement "드래그 앤 드롭 기능"
/sc checkpoint "MVP 완성"
/sc improve --focus performance
/sc analyze
/sc build --target exe
```

### 2. 플래그 활용

```bash
# 상세 모드
/sc analyze --verbose

# 특정 파일만 대상
/sc improve --files "src/utils/*.py"

# 언어 지정
/sc document --lang en
```

### 3. 워크플로우 최적화

```bash
# 개발 사이클
1. /sc design [프로젝트 설명]
2. /sc implement [기능]
3. /sc checkpoint [마일스톤]
4. /sc analyze --focus quality
5. /sc improve
6. /sc troubleshoot [문제]
7. /sc cleanup
8. /sc document
9. /sc build
```

---

## 🚨 주의사항

1. **체크포인트는 자주**: 큰 변경 전후로 체크포인트 생성
2. **분석 먼저**: improve 전에 analyze로 문제 파악
3. **단계별 진행**: 한 번에 너무 많은 변경 피하기
4. **백업 중요**: 중요한 코드는 별도 백업

---

## 📚 추가 예제 시나리오

### 시나리오 1: 풀스택 웹 앱 개발

```bash
# 1. 설계
/sc design "온라인 도서 관리 시스템 (React + Node.js + MongoDB)"

# 2. 백엔드 구현
/sc implement "Express.js REST API 서버 구조"
/sc implement "MongoDB 스키마 및 모델"
/sc implement "JWT 인증 미들웨어"

# 3. 프론트엔드 구현
/sc implement "React 라우터 설정"
/sc implement "도서 목록 컴포넌트"
/sc implement "도서 추가/수정 폼"

# 4. 통합 및 최적화
/sc improve --focus integration
/sc analyze --comprehensive
/sc troubleshoot "CORS 오류 해결"

# 5. 배포 준비
/sc cleanup
/sc document --type api
/sc build --production
```

### 시나리오 2: 데이터 분석 도구 개발

```bash
# 1. 초기 설계
/sc design "CSV 파일 분석 및 시각화 도구 (Python)"

# 2. 핵심 기능 구현
/sc implement "CSV 파일 읽기 및 검증"
/sc implement "통계 분석 함수 (평균, 중앙값, 표준편차)"
/sc implement "matplotlib 차트 생성"

# 3. UI 추가
/sc implement "Tkinter GUI 인터페이스"
/sc checkpoint "GUI 버전 1.0"

# 4. 기능 확장
/sc implement "Excel 파일 지원"
/sc implement "PDF 리포트 생성"

# 5. 최종 마무리
/sc improve --focus usability
/sc analyze --focus performance
/sc build --target exe
```

---

**이 예제들을 참고하여 SuperClaude를 최대한 활용해보세요!** 🚀