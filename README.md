# AI Study Hub 🤖

AI와 머신러닝을 체계적으로 학습하기 위한 종합 가이드 레포지토리입니다.

## 📚 목차

1. [시작하기](#시작하기)
2. [학습 로드맵](#학습-로드맵)
3. [프로젝트 구조](#프로젝트-구조)
4. [주요 도구](#주요-도구)
5. [실습 프로젝트](#실습-프로젝트)
6. [리소스](#리소스)

---

## 🚀 시작하기

### 환경 설정

```bash
# Python 가상환경 생성
python -m venv venv

# 가상환경 활성화 (Windows)
venv\Scripts\activate

# 가상환경 활성화 (Mac/Linux)
source venv/bin/activate

# 기본 패키지 설치
pip install -r requirements.txt
```

### 필수 도구 설치

1. **Python 3.8+**: [다운로드](https://www.python.org/downloads/)
2. **Git**: [다운로드](https://git-scm.com/)
3. **VSCode**: [다운로드](https://code.visualstudio.com/)
4. **Jupyter Notebook**: `pip install jupyter`

---

## 🗺️ 학습 로드맵

### 1단계: AI 기초 (2-4주)
- [ ] Python 기초 문법
- [ ] NumPy, Pandas 기초
- [ ] 데이터 시각화 (Matplotlib, Seaborn)
- [ ] 통계학 기초

### 2단계: 머신러닝 기초 (4-6주)
- [ ] Scikit-learn 입문
- [ ] 지도학습 (분류, 회귀)
- [ ] 비지도학습 (클러스터링, 차원축소)
- [ ] 모델 평가 및 개선

### 3단계: 딥러닝 기초 (4-6주)
- [ ] 신경망 이론
- [ ] TensorFlow/PyTorch 기초
- [ ] CNN (컴퓨터 비전)
- [ ] RNN/LSTM (시계열 데이터)

### 4단계: 고급 주제 (6-8주)
- [ ] Transformers & NLP
- [ ] LangChain & RAG
- [ ] MLOps 기초
- [ ] 프로덕션 배포

### 5단계: 프로젝트 & 포트폴리오 (지속적)
- [ ] 개인 프로젝트 3개 이상
- [ ] 오픈소스 기여
- [ ] 블로그 작성

---

## 📁 프로젝트 구조

```
ai-study-hub/
├── fundamentals/          # AI/ML 기초 개념
│   ├── python-basics/     # Python 기초
│   ├── math-stats/        # 수학/통계
│   └── ml-basics/         # ML 기초 이론
├── tools/                 # AI 도구 학습
│   ├── langchain/         # LangChain 튜토리얼
│   ├── openai/            # OpenAI API 활용
│   └── huggingface/       # Hugging Face 모델
├── projects/              # 실습 프로젝트
│   ├── nlp/               # 자연어처리 프로젝트
│   ├── computer-vision/   # 컴퓨터 비전 프로젝트
│   └── ml-ops/            # MLOps 프로젝트
├── resources/             # 학습 자료
│   ├── papers/            # 주요 논문
│   ├── datasets/          # 데이터셋
│   └── tutorials/         # 튜토리얼 링크
└── superclaude/           # SuperClaude 관련
    ├── examples/          # 예제 코드
    └── templates/         # 프로젝트 템플릿
```

---

## 🛠️ 주요 도구

### 1. SuperClaude
AI 개발을 가속화하는 강력한 도구입니다.
- [설치 가이드](./superclaude/INSTALLATION_GUIDE_KO.md)
- [사용 예제](./superclaude/examples/)

### 2. LangChain
LLM 애플리케이션 개발 프레임워크
- [기초 튜토리얼](./tools/langchain/basics.md)
- [RAG 구현하기](./tools/langchain/rag-tutorial.md)

### 3. OpenAI API
GPT 모델 활용하기
- [API 시작하기](./tools/openai/getting-started.md)
- [프롬프트 엔지니어링](./tools/openai/prompt-engineering.md)

### 4. Hugging Face
사전학습 모델 활용
- [모델 허브 사용법](./tools/huggingface/model-hub.md)
- [파인튜닝 가이드](./tools/huggingface/fine-tuning.md)

---

## 💻 실습 프로젝트

### 초급 프로젝트
1. **감정 분석 챗봇**: 텍스트 감정 분석 및 응답 생성
2. **이미지 분류기**: 간단한 CNN 모델로 이미지 분류
3. **주가 예측 모델**: LSTM을 활용한 시계열 예측

### 중급 프로젝트
1. **질문-답변 시스템**: RAG를 활용한 문서 기반 QA
2. **음성 인식 앱**: Whisper API를 활용한 STT 구현
3. **추천 시스템**: 협업 필터링 기반 추천 엔진

### 고급 프로젝트
1. **멀티모달 AI**: 텍스트-이미지 통합 모델
2. **자동 코드 생성기**: LLM 기반 코드 생성 도구
3. **AI 에이전트**: 자율적으로 작업을 수행하는 에이전트

---

## 📚 리소스

### 필독 논문
- [Attention Is All You Need](./resources/papers/attention.md)
- [BERT: Pre-training of Deep Bidirectional Transformers](./resources/papers/bert.md)
- [GPT-3: Language Models are Few-Shot Learners](./resources/papers/gpt3.md)

### 추천 강의
- **Andrew Ng의 Machine Learning**: [Coursera](https://www.coursera.org/learn/machine-learning)
- **Fast.ai**: [실용적인 딥러닝](https://www.fast.ai/)
- **CS231n**: [스탠포드 컴퓨터 비전](http://cs231n.stanford.edu/)

### 유용한 데이터셋
- [Kaggle Datasets](https://www.kaggle.com/datasets)
- [Google Dataset Search](https://datasetsearch.research.google.com/)
- [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/index.php)

### 커뮤니티
- [Reddit r/MachineLearning](https://www.reddit.com/r/MachineLearning/)
- [AI 연구 Slack](https://join.slack.com/t/ai-research)
- [Papers with Code](https://paperswithcode.com/)

---

## 🎯 학습 팁

### 1. 실습 중심 학습
- 이론 20%, 실습 80% 비율 유지
- 매일 코드 작성하기
- 작은 프로젝트부터 시작

### 2. 커뮤니티 활용
- 질문하기를 두려워하지 않기
- 다른 사람의 코드 리뷰하기
- 블로그나 포럼에 학습 내용 공유

### 3. 지속적인 학습
- 최신 논문 팔로우
- 새로운 도구와 프레임워크 시도
- 실패를 학습의 기회로 활용

---

## 🤝 기여하기

이 레포지토리는 함께 만들어가는 학습 공간입니다.

1. Fork 하기
2. Feature 브랜치 생성 (`git checkout -b feature/AmazingFeature`)
3. 변경사항 커밋 (`git commit -m 'Add some AmazingFeature'`)
4. 브랜치에 Push (`git push origin feature/AmazingFeature`)
5. Pull Request 생성

---

## 📝 라이센스

이 프로젝트는 MIT 라이센스를 따릅니다. 자세한 내용은 [LICENSE](LICENSE) 파일을 참조하세요.

---

## ✨ 다음 단계

1. **오늘 시작하기**: Python 기초부터 차근차근
2. **일일 학습 계획**: 매일 1-2시간씩 꾸준히
3. **프로젝트 만들기**: 배운 내용을 바로 적용
4. **공유하기**: 학습 과정을 기록하고 공유

**함께 AI의 미래를 만들어갑시다! 🚀**