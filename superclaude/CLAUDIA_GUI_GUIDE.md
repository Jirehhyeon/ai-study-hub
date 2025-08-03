# Claudia - Claude Code GUI 도구 완벽 가이드

## 🎨 Claudia란?

**Claudia**는 Claude Code를 그래픽 인터페이스(GUI)로 사용할 수 있게 해주는 오픈소스 프로그램입니다. 터미널 환경이 어려운 사용자도 쉽게 Claude Code의 강력한 기능을 활용할 수 있습니다.

### 주요 특징
- ✨ **직관적인 UI**: 프로젝트와 대화 내역을 시각적으로 관리
- 🆓 **오픈소스**: 완전 무료로 사용 가능
- 🚀 **에이전트 기능**: 여러 Claude를 동시에 실행 (Max 플랜)
- 🕒 **타임라인**: Git 기반 세이브/로드 시스템
- 🔧 **후크 시스템**: 도구 실행 전후 자동화

---

## 🛠️ 설치 가이드

### 시스템 요구사항
- **권장**: macOS, Linux
- **가능**: Windows (WSL 또는 Docker 환경)
- **주의**: Windows 네이티브 버전은 개발 중

### WSL 환경 설치 (Windows)

```bash
# 1. WSL 환경에서 Node.js 설치 확인
node --version

# 2. Claudia 설치
npm install -g claudia

# 3. 실행
claudia
```

**⚠️ WSL 설치 시 주의사항:**
- 한글 인코딩 문제 발생 가능
- 일부 기능(에이전트, 타임라인) 제한
- Docker 환경 사용 시 더 안정적

### macOS/Linux 설치

```bash
# 더 간단하고 안정적인 설치
npm install -g claudia
claudia
```

---

## 📱 기본 사용법

### 1. 프로젝트 관리

#### 기존 프로젝트 열기
1. Claudia 실행 → **Projects** 메뉴 클릭
2. 프로젝트 목록에서 원하는 프로젝트 선택
3. 과거 대화 내역 확인 및 이어서 작업

#### 새 프로젝트 생성
1. **New Chat** 클릭
2. 작업 폴더 선택
3. 대화 시작
4. `"CLAUDE.md 파일 만들어줘"` 요청으로 지침 파일 생성

### 2. 프로젝트 지침 설정

```markdown
# CLAUDE.md 편집 예시

## 프로젝트 설명
이 프로젝트는 웹 크롤러 개발입니다.

## 기술 스택
- Python 3.9+
- BeautifulSoup4
- Selenium

## 코딩 규칙
- PEP 8 준수
- 타입 힌트 사용
- 예외 처리 필수
```

**편집 방법**: Claudia에서 CLAUDE.md 파일 클릭 → 직접 편집

### 3. 사고 깊이 설정

**Options** 메뉴에서 선택:
- **Think**: 기본 사고 수준
- **Think Hard**: 더 깊은 분석 (토큰 사용량 증가)
- **Ultra Think**: 최대 깊이 분석 (토큰 대량 사용)

---

## 🤖 고급 기능

### 1. 에이전트 기능 (Agent)

백그라운드에서 추가 Claude Code 인스턴스 실행

```bash
# 에이전트 메뉴에서 설정
- 동시 작업 수행
- 병렬 처리로 속도 향상
- Max 플랜 권장
```

**주의**: WSL 환경에서는 오류 발생 가능

### 2. 후크(Hook) 시스템

도구 실행 전후에 자동으로 스크립트 실행

#### Pre Tool Use (도구 실행 전)
```bash
# 예: 터미널 명령 로깅
Pattern: bash
Command: echo "[$(date)] Executing: $1" >> tool_log.txt
```

#### Post Tool Use (도구 실행 후)
```bash
# 예: 실행 결과 로깅
Pattern: bash
Command: echo "[$(date)] Result: $?" >> tool_log.txt
```

### 활용 예시

#### 1. 디버깅 로그 자동화
```bash
# MCP 실행 결과 자동 저장
Pattern: mcp
Command: echo "$OUTPUT" >> mcp_results.log
```

#### 2. 자동 백업
```bash
# 파일 편집 후 자동 백업
Pattern: edit
Command: git add -A && git commit -m "Auto-backup: $(date)"
```

#### 3. 알림 시스템
```bash
# 작업 완료 시 알림
Hook Type: on-stop
Command: notify-send "Claude Code" "작업이 완료되었습니다"
```

### 3. 타임라인 기능

Git 기반 버전 관리 시스템

```bash
# 세이브 포인트 생성
Timeline → Create Checkpoint

# 이전 상태로 복원
Timeline → Restore to Checkpoint
```

**장점**:
- 실험적 변경 안전하게 시도
- 문제 발생 시 즉시 롤백
- 여러 브랜치 관리 가능

---

## 🎯 실전 활용 팁

### 1. 외부 도구 연동

#### 다른 AI 도구 활용
```bash
# 프로젝트 지침에 추가
## 외부 도구 사용법
- 코딩: Claude Code
- 문서 분석: [외부 AI 도구] --ro-mode
- 데이터 처리: Python 스크립트
```

### 2. 코드맵 생성

대규모 프로젝트 구조 파악을 위한 코드맵:

```bash
"전체 프로젝트 파일을 분석해서 다음 형식의 코드맵을 만들어줘:
1. 주요 기능별 파일 위치
2. 함수/클래스 간 의존성
3. 데이터 흐름도
4. 모듈 간 연결 관계"
```

### 3. 커스텀 슬래시 명령어

`~/.claude/settings.json`에 추가:

```json
{
  "commands": {
    "my-planner": {
      "description": "프로젝트 계획 수립",
      "prompt": "다음 요구사항에 대한 상세한 개발 계획을 수립해주세요:\n1. 기술 스택 선정\n2. 아키텍처 설계\n3. 일정 계획\n4. 리스크 분석"
    },
    "code-review": {
      "description": "코드 리뷰 수행",
      "prompt": "다음 관점에서 코드를 리뷰해주세요:\n- 버그 가능성\n- 성능 최적화\n- 보안 취약점\n- 코드 품질"
    }
  }
}
```

사용법: `/my-planner`, `/code-review`

---

## ⚠️ 알려진 문제와 해결법

### WSL 환경 문제

1. **한글 깨짐**
   ```bash
   export LANG=ko_KR.UTF-8
   export LC_ALL=ko_KR.UTF-8
   ```

2. **에이전트 기능 오류**
   - Docker 환경 사용 권장
   - 또는 native Linux/macOS 사용

3. **타임라인 기능 미작동**
   - Git 설정 확인
   - 권한 문제 해결: `chmod -R 755 .git`

### 일반적인 문제

1. **설치 실패**
   - Node.js 버전 확인 (16.x 이상)
   - npm 캐시 정리: `npm cache clean --force`

2. **GUI 렌더링 문제**
   - WSL2 + WSLg 설정 확인
   - X11 포워딩 설정

---

## 🚀 향후 업데이트 예정

- ✅ Windows 네이티브 버전
- ✅ 플랜 모드 지원
- ✅ 더 많은 MCP 통합
- ✅ 성능 최적화
- ✅ 다국어 지원

---

## 📚 추가 리소스

- [Claudia GitHub 저장소](https://github.com/claudia/claudia)
- [Claude Code 공식 문서](https://docs.anthropic.com/claude/docs)
- [WSL 설정 가이드](https://docs.microsoft.com/windows/wsl)

---

## 💡 프로 팁

### 1. 워크플로우 최적화
```bash
# 아침 루틴 자동화
Hook: on-start
Command: git pull && npm install && echo "프로젝트 준비 완료"
```

### 2. 협업 설정
```bash
# 팀원과 공유할 설정
.claudia/
├── hooks/
├── settings.json
└── templates/
```

### 3. 성능 모니터링
```bash
# 토큰 사용량 추적
Hook: post-tool-use
Command: echo "Tokens used: $TOKENS" >> usage.log
```

---

**Claudia**를 사용하면 Claude Code의 강력한 기능을 더욱 쉽고 효율적으로 활용할 수 있습니다. GUI의 편리함과 고급 기능들을 조합하여 생산성을 극대화하세요! 🎨✨