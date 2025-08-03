# 🔧 MCP 자동 설치 완벽 가이드 - "설치해줘"만 하면 끝!

## 📌 개요

MCP(Model Context Protocol) 설치가 복잡해서 하루 종일 걸렸던 경험이 있으신가요?
이제 **5분**이면 끝납니다! 대화하듯 "설치해줘"라고만 하면 됩니다.

---

## 🚀 사전 준비사항

### 필수 환경
- **WSL** (Windows Subsystem for Linux) 또는 Mac/Linux
- **Node.js** 설치됨
- **Claude Code** 설치됨

---

## 📋 단계별 설치 가이드

### 1단계: MCP Installer 설치

WSL 터미널에서 다음 명령어 실행:

```bash
# MCP Installer 설치 (--scope user로 모든 프로젝트에서 사용 가능)
npm install -g @modelcontextprotocol/installer --scope user
```

### 2단계: 자동 설치 지침 설정

#### 2-1. CLAUDE.md 파일 찾기
작업 폴더에서 `CLAUDE.md` 파일을 찾거나 생성

#### 2-2. 자동 설치 지침 추가
다음 내용을 `CLAUDE.md` 파일에 복사-붙여넣기:

```markdown
# MCP 자동 설치 지침

## MCP 설치 순서
1. 공식 홈페이지에서 설치 방법 확인
2. MCP Installer로 자동 설치 시도
3. 실패 시 `claude mcp add` 명령어 사용
4. 필요시 설정 파일 직접 편집

## 설치 확인 방법
- 서브 에이전트를 백그라운드에서 실행
- 디버그 모드로 에러 메시지 확인
- 재시작 없이 `claude mcp list`로 확인

## 자동화 스크립트
설치 요청 시 다음 순서로 진행:
1. MCP 공식 정보 검색
2. 작업 환경 확인 (WSL/Mac/Linux)
3. Node.js 버전 확인
4. MCP Installer 시도
5. 실패 시 대체 방법 자동 전환
6. 서브 에이전트로 설치 확인
```

### 3단계: Claude Code 실행

```bash
# 1. 작업 폴더로 이동
cd /your/project/folder

# 2. Claude Code 실행
claude
```

### 4단계: MCP 설치 요청

이제 대화하듯 설치를 요청하면 됩니다!

#### 4개 필수 MCP 설치

**1. Context7 MCP 설치** (약 6분)
```
"Context7 MCP를 설치해주세요"
```

**2. Sequential MCP 설치** (약 5분)
```
"Sequential MCP도 설치해주세요"
```

**3. Google Search MCP 설치** (약 5분)
```
"Google Search MCP 설치 부탁드립니다"
```

**4. Playwright MCP 설치** (약 5분)
```
"Playwright MCP도 설치해주세요"
```

---

## 🎯 특수 MCP 설치

### Magic MCP 설치 (UI 컴포넌트 생성용)

**주의**: API 키가 필요하며, 무료 플랜은 사용량 제한이 있습니다.

#### 1. API 키 발급
1. [visly.ai](https://visly.ai) 방문
2. 회원가입
3. 설정에서 API 키 발급

#### 2. 설치 요청
```
"Magic MCP를 설치해주세요"
```

#### 3. 설정 붙여넣기
Claude가 요청하면 발급받은 API 키와 설정을 붙여넣기

### MySQL/MariaDB MCP 설치

**사전 요구사항**: MySQL 서버가 실행 중이어야 함

```bash
# MySQL 서버 실행 확인
mysql --version

# 설치 요청
"MariaDB MCP를 설치해주세요"
```

### 까다로운 MCP 설치 (예: Shrimp Task Manager)

일부 MCP는 추가 요구사항이 있을 수 있습니다:
- Node.js 버전 업데이트 필요
- 관리자 권한 필요
- 약 20분 소요

```
"Shrimp Task Manager MCP를 설치해주세요"
```

---

## 🔍 설치 확인

### 방법 1: Claude Code 재시작 후 확인
```bash
# Claude Code 종료 후 재시작
claude

# MCP 목록 확인
claude mcp list
```

### 방법 2: 대화로 확인
```
"설치된 MCP 목록을 보여주세요"
```

---

## 🛡️ 보안 주의사항

### API 키 보호
CLAUDE.md 파일에 API 키나 비밀번호가 있다면:

```
"CLAUDE.md 파일을 .gitignore에 추가해주세요"
```

이렇게 하면 GitHub에 실수로 노출되는 것을 방지할 수 있습니다.

---

## 📊 설치 시간 비교

| MCP 이름 | 수동 설치 | 자동 설치 |
|----------|-----------|-----------|
| Context7 | 30분+ | 6분 |
| Sequential | 20분+ | 5분 |
| Google Search | 25분+ | 5분 |
| Playwright | 30분+ | 5분 |
| Magic | 40분+ | 10분 |
| 복잡한 MCP | 1시간+ | 20분 |

---

## 💡 문제 해결

### 설치 실패 시

1. **Node.js 버전 확인**
```bash
node --version
# 16.x 이상 필요
```

2. **권한 문제**
```bash
# 관리자 권한으로 실행
sudo npm install -g @modelcontextprotocol/installer
```

3. **수동 대체 방법**
```
"GitHub에서 직접 다운로드해서 설치해주세요"
```

### MCP가 인식되지 않을 때

1. Claude Code 완전히 종료 후 재시작
2. 설정 파일 확인: `~/.claude/mcp.json`
3. 캐시 정리: `npm cache clean --force`

---

## 🎉 완료!

이제 복잡한 MCP 설치 과정이 단 5분으로 단축되었습니다.
"설치해줘"라고만 하면 Claude가 알아서 다 해줍니다!

### 다음 단계
1. SuperClaude와 함께 사용하여 성능 극대화
2. Claudia GUI로 더 편리하게 사용
3. 각 MCP의 고유 기능 활용

**팁**: 여러 MCP를 한 번에 설치하려면:
```
"Context7, Sequential, Playwright MCP를 모두 설치해주세요"
```