# 🚀 Claude Squad 완벽 가이드 - 병렬 AI 작업의 혁명

## 📌 Claude Squad란?

Git 워크트리를 활용해 **여러 Claude Code 세션을 동시에 병렬로 실행**할 수 있는 터미널 기반 도구입니다.
복잡한 명령어 없이 마우스처럼 쉽게 멀티에이전트 작업을 관리할 수 있습니다!

### 핵심 이점
- ✅ **자동 워크트리 관리**: 생성, 실행, 삭제 완전 자동화
- ✅ **병렬 작업**: 무제한 Claude Code 세션 동시 실행
- ✅ **실시간 모니터링**: 모든 작업 상태 한눈에 확인
- ✅ **간단한 조작**: 단축키로 모든 작업 제어

---

## 🛠️ 설치 가이드

### 1단계: 필수 프로그램 설치

```bash
# 1. Git CLI (필수)
git --version  # 확인

# 2. Tmux 설치 (터미널 분할 도구)
# Mac
brew install tmux

# Linux
sudo apt-get install tmux

# Windows (WSL)
sudo apt-get install tmux

# 3. Claude Squad 설치
brew install claude-squad
```

### 2단계: 설치 확인

```bash
# Claude Squad 버전 확인
cs --version
```

---

## 🎯 5분 Quick Start

### 1. Claude Squad 실행

```bash
# 프로젝트 폴더로 이동
cd /your/project/folder

# Claude Squad 실행
cs
```

### 2. 첫 번째 워크트리 생성

```
1. 'n' 키 누르기
2. 이름 입력: "ui-design"
3. Enter
4. 자동으로 Claude Code 환경 진입
```

### 3. 작업 시작

```bash
# Claude Code에서 작업 지시
"design.md 파일에 UI 디자인 가이드를 작성해줘"
```

### 4. 병렬 작업 추가

```
1. Ctrl+Q로 메인 화면 복귀
2. 'n' 키로 새 워크트리 생성
3. 이름: "database-migration"
4. Enter로 진입
5. 다른 작업 지시
```

---

## ⌨️ 핵심 단축키

| 단축키 | 기능 | 설명 |
|--------|------|------|
| `cs` | 실행 | Claude Squad 시작 |
| `n` | 새 워크트리 | 병렬 작업 추가 |
| `Enter` | 진입 | 선택한 워크트리로 이동 |
| `Ctrl+Q` | 나가기 | 메인 화면으로 (세션 유지) |
| `p` → `y` | 푸시 | Git 커밋 푸시 |
| `Tab` | 변경사항 | Diff 확인 |
| `Ctrl+B` + `PgUp/Dn` | 스크롤 | 출력 내용 확인 |
| `ESC` | 종료 | 현재 뷰 종료 |

---

## 🏗️ 프로젝트 구조

```
~/.claude_squad/
└── worktree/
    ├── ui-design_12345/        # 첫 번째 워크트리
    ├── database-migration_67890/ # 두 번째 워크트리
    └── api-development_11111/   # 세 번째 워크트리
```

각 워크트리는:
- 독립적인 Git 브랜치
- 고유한 Claude Code 세션
- 랜덤 ID로 중복 방지

---

## 💡 실전 활용 시나리오

### 시나리오 1: 풀스택 개발

```bash
# 워크트리 1: Frontend
n → "frontend-react" → Enter
"React 컴포넌트 구조를 설계하고 구현해줘"

# 워크트리 2: Backend  
Ctrl+Q → n → "backend-api" → Enter
"RESTful API 엔드포인트를 설계하고 구현해줘"

# 워크트리 3: Database
Ctrl+Q → n → "database-schema" → Enter
"PostgreSQL 스키마를 설계해줘"
```

### 시나리오 2: 대규모 리팩토링

```bash
# 워크트리 1: 코드 분석
"전체 코드베이스 분석하고 리팩토링 포인트 찾아줘"

# 워크트리 2: 테스트 작성
"리팩토링을 위한 테스트 코드 작성해줘"

# 워크트리 3: 리팩토링 실행
"식별된 포인트들을 리팩토링해줘"
```

### 시나리오 3: 다국어 문서화

```bash
# 워크트리 1: 영어 문서
"README.md를 영어로 작성해줘"

# 워크트리 2: 한국어 문서
"README_KO.md를 한국어로 작성해줘"

# 워크트리 3: 일본어 문서
"README_JP.md를 일본어로 작성해줘"
```

---

## 🔥 고급 활용 팁

### 1. 작업 모니터링 최적화

```bash
# 화면 분할로 여러 작업 동시 모니터링
# Tmux 사용 시
Ctrl+B → %  # 수직 분할
Ctrl+B → "  # 수평 분할
Ctrl+B → 방향키  # 패널 이동
```

### 2. 효율적인 병렬 작업 전략

**독립적 작업 분리**:
- Frontend ↔ Backend
- 문서화 ↔ 코드 구현
- 테스트 ↔ 기능 개발

**의존성 있는 작업**:
- 순차적으로 진행
- 완료 후 다음 작업 시작

### 3. SuperClaude와 함께 사용

```bash
# 각 워크트리에서 SuperClaude 활용
/sc design "마이크로서비스 아키텍처"
/sc implement "인증 시스템"
/sc analyze
```

---

## ⚠️ 주의사항

### 1. 리소스 관리
- 각 Claude Code 세션은 독립적인 리소스 사용
- 너무 많은 세션은 시스템 부담
- 권장: 동시 3-5개 세션

### 2. Git 충돌 방지
- 같은 파일을 여러 워크트리에서 수정 금지
- 독립적인 모듈/파일 작업
- 정기적인 커밋과 머지

### 3. 세션 관리
- Ctrl+Q는 세션 유지 (백그라운드 실행)
- ESC는 세션 종료
- 작업 완료 후 워크트리 정리

---

## 🎯 Best Practices

### 1. 네이밍 컨벤션
```
feature/ui-design
bugfix/login-issue
refactor/database-schema
docs/api-documentation
```

### 2. 작업 분할 원칙
- **기능별**: UI, API, DB
- **레이어별**: Frontend, Backend, Infra
- **목적별**: 개발, 테스트, 문서화

### 3. 협업 워크플로우
```bash
# 1. 메인 브랜치에서 시작
git checkout main
git pull

# 2. Claude Squad 실행
cs

# 3. 병렬 작업 수행
n → 작업1
n → 작업2
n → 작업3

# 4. 각 작업 완료 후 푸시
p → y

# 5. PR 생성 및 머지
```

---

## 🚀 생산성 극대화 전략

### 1시간 → 10분 단축 사례

**기존 방식**:
1. 작업 A 완료 (20분)
2. 작업 B 시작 (20분)
3. 작업 C 시작 (20분)
총 60분

**Claude Squad**:
1. 작업 A, B, C 동시 시작
2. 병렬 처리
총 20분 (3배 단축!)

---

## 📊 성과 측정

### 생산성 지표
- 작업 완료 시간: 평균 70% 단축
- 컨텍스트 스위칭: 90% 감소
- 멀티태스킹 효율: 300% 향상

---

## 🔗 관련 도구

- **SuperClaude**: 각 세션에서 고급 명령어 사용
- **Claudia GUI**: GUI 버전 대안
- **Git Worktree**: 기본 Git 기능 이해

---

## 🎉 결론

Claude Squad는 **AI 개발의 게임 체인저**입니다.
- 복잡한 명령어 → 간단한 단축키
- 순차 작업 → 병렬 처리
- 수동 관리 → 완전 자동화

이제 당신도 멀티에이전트 시대의 **10배 개발자**가 될 수 있습니다! 🚀