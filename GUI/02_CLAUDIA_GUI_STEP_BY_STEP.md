# 🎨 Claudia GUI 완벽 설치 및 사용 가이드

## 📌 Claudia란?

Claude Code를 **그래픽 인터페이스(GUI)**로 사용할 수 있게 해주는 **무료 오픈소스** 프로그램입니다.
터미널이 어려운 분들도 마우스 클릭만으로 Claude Code의 모든 기능을 사용할 수 있습니다!

---

## 🖥️ 주요 기능

### 1. 직관적인 인터페이스
- 프로젝트 목록을 한눈에 확인
- 대화 내역을 시각적으로 관리
- 마우스 클릭으로 모든 기능 사용

### 2. 고급 기능
- **Think 레벨 조정**: 토큰 사용량과 사고 깊이 조절
- **에이전트 기능**: 여러 Claude를 동시 실행 (Max 플랜)
- **Hook 시스템**: 자동화 스크립트 실행
- **타임라인**: Git 기반 코드 버전 관리

---

## 🛠️ 설치 가이드

### Windows (WSL) 설치

**주의**: Windows 네이티브 버전은 개발 중. WSL 사용 필요

#### 1단계: WSL 설치 확인
```bash
# WSL 버전 확인
wsl --version
```

#### 2단계: Claudia 설치
```bash
# WSL 터미널에서 실행
npm install -g claudia
```

#### 3단계: 실행
```bash
# Claudia 실행
claudia
```

### Mac/Linux 설치 (권장)
```bash
# 더 간단하고 안정적
npm install -g claudia
claudia
```

---

## 📱 기본 사용법

### 1. 프로젝트 관리

#### 기존 프로젝트 열기
1. Claudia 실행
2. **Projects** 메뉴 클릭
3. 프로젝트 목록에서 선택
4. 과거 대화 내역이 자동으로 표시됨

#### 새 프로젝트 만들기
1. **New Chat** 클릭
2. 작업 폴더 선택
3. 대화 시작
4. "CLAUDE.md 파일 만들어줘"로 지침 파일 생성

### 2. 프로젝트 지침 설정

CLAUDE.md 파일을 클릭해서 바로 편집:

```markdown
# 프로젝트 설명
웹 크롤러 개발 프로젝트

# 기술 스택
- Python 3.9+
- BeautifulSoup4
- Selenium

# 코딩 규칙
- PEP 8 준수
- 타입 힌트 사용
- 예외 처리 필수
```

### 3. Think 레벨 설정

Options 메뉴에서 선택:
- **Think**: 기본 사고 (빠름, 토큰 적게 사용)
- **Think Hard**: 깊은 사고 (중간 속도, 토큰 중간 사용)
- **Ultra Think**: 최대 깊이 (느림, 토큰 많이 사용, 최고 품질)

---

## 🚀 고급 기능

### 1. Hook 시스템 설정

Hook은 도구 실행 전후에 자동으로 스크립트를 실행하는 기능입니다.

#### Hook 설정 방법
1. 프로젝트에서 **Hooks** 클릭
2. **Pre Tool Use** 또는 **Post Tool Use** 선택
3. **Add Hook** 클릭

#### 예제 1: 터미널 명령 로깅

**Pre Tool Use** (실행 전):
```bash
Pattern: bash
Command: echo "[$(date)] 실행: $1" >> tool_log.txt
```

**Post Tool Use** (실행 후):
```bash
Pattern: bash
Command: echo "[$(date)] 결과: $?" >> tool_log.txt
```

#### 예제 2: MCP 실행 결과 저장
```bash
Pattern: mcp
Command: echo "$OUTPUT" >> mcp_results.log
```

#### 예제 3: 작업 완료 시 자동 커밋
```bash
Hook Type: on-stop
Command: git add -A && git commit -m "자동 저장: $(date)"
```

### 2. 에이전트 기능 (Max 플랜)

백그라운드에서 추가 Claude Code 실행:
1. **Agent** 메뉴 클릭
2. 동시 실행할 작업 설정
3. 병렬 처리로 작업 속도 향상

**주의**: WSL에서는 오류 발생 가능. Mac/Linux 권장

### 3. 타임라인 기능

Git 기반 세이브/로드 시스템:
1. **Timeline** 메뉴
2. **Create Checkpoint**: 현재 상태 저장
3. **Restore**: 이전 상태로 복원

**장점**:
- 실험적 변경 안전하게 시도
- 문제 발생 시 즉시 롤백
- 여러 버전 관리

---

## 💡 실전 활용 팁

### 1. 외부 도구 연동

프로젝트 지침에 추가:
```markdown
## 외부 도구 사용법
- 코딩: Claude Code
- 문서 분석: [다른 AI 도구] --ro-mode
- 대량 처리: Python 스크립트
```

### 2. 코드맵 생성

전체 프로젝트 구조 파악:
```
"전체 파일을 분석해서 코드맵을 만들어줘:
1. 기능별 파일 위치
2. 함수/클래스 의존성
3. 데이터 흐름
4. 모듈 간 연결"
```

### 3. 커스텀 명령어 만들기

`~/.claude/settings.json` 편집:
```json
{
  "commands": {
    "my-planner": {
      "prompt": "프로젝트 계획을 수립해주세요"
    }
  }
}
```

사용: `/my-planner`

---

## ⚠️ 알려진 문제와 해결법

### WSL 환경 문제

#### 1. 한글 깨짐
```bash
export LANG=ko_KR.UTF-8
export LC_ALL=ko_KR.UTF-8
```

#### 2. 에이전트 기능 오류
- Docker 사용 권장
- 또는 native Linux/Mac 사용

#### 3. 타임라인 미작동
```bash
# Git 권한 설정
chmod -R 755 .git
```

### 일반 문제

#### 설치 실패
```bash
# Node.js 버전 확인 (16.x 이상)
node --version

# npm 캐시 정리
npm cache clean --force
```

---

## 🎯 Claudia vs 터미널 비교

| 기능 | Claudia GUI | 터미널 |
|------|-------------|---------|
| 사용 편의성 | ⭐⭐⭐⭐⭐ | ⭐⭐ |
| 프로젝트 관리 | 시각적 | 명령어 |
| 대화 내역 | 한눈에 확인 | 스크롤 필요 |
| 설정 변경 | 클릭 | 파일 편집 |
| Hook 설정 | GUI | 수동 설정 |
| 학습 곡선 | 낮음 | 높음 |

---

## 🚀 추천 워크플로우

### 1. 프로젝트 시작
```
1. Claudia 실행
2. New Chat → 폴더 선택
3. "CLAUDE.md 만들어줘"
4. 프로젝트 설명 작성
```

### 2. 개발 작업
```
1. Think Hard 설정
2. SuperClaude 명령어 사용
3. Hook으로 자동 로깅
4. Timeline으로 버전 관리
```

### 3. 디버깅
```
1. Hook 로그 확인
2. "로그 파일 분석해줘"
3. 문제 해결
```

---

## 📈 향후 업데이트 예정

- ✅ Windows 네이티브 버전
- ✅ Plan Mode 지원
- ✅ 더 많은 GUI 기능
- ✅ 한글 완벽 지원

---

## 🎉 결론

Claudia를 사용하면:
- 터미널 없이 Claude Code 사용
- 마우스 클릭으로 모든 기능 활용
- 시각적으로 프로젝트 관리
- Hook으로 작업 자동화

이제 누구나 쉽게 Claude Code를 마스터할 수 있습니다! 🚀