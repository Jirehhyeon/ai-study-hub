# LangChain 기초 - LLM 애플리케이션 개발의 시작

## 🔗 LangChain이란?

LangChain은 대규모 언어 모델(LLM)을 활용한 애플리케이션을 쉽게 만들 수 있게 해주는 프레임워크입니다.

### 핵심 개념
- **🔗 Chains**: 여러 컴포넌트를 연결하여 복잡한 작업 수행
- **📝 Prompts**: 효과적인 프롬프트 관리 및 최적화
- **🧠 Memory**: 대화 맥락 유지 및 상태 관리
- **🔍 Retrieval**: RAG를 위한 문서 검색 및 처리
- **🤖 Agents**: 도구를 사용하여 작업을 수행하는 자율 에이전트

---

## 1. 설치 및 환경 설정

```bash
# LangChain 설치
pip install langchain langchain-openai langchain-community

# 추가 패키지
pip install chromadb  # 벡터 데이터베이스
pip install tiktoken  # 토큰 카운팅
pip install python-dotenv  # 환경 변수 관리
```

### 환경 변수 설정

```python
# .env 파일 생성
"""
OPENAI_API_KEY=your_api_key_here
LANGCHAIN_TRACING_V2=true
LANGCHAIN_API_KEY=your_langsmith_key
"""

# Python에서 로드
from dotenv import load_dotenv
import os

load_dotenv()
api_key = os.getenv("OPENAI_API_KEY")
```

---

## 2. 기본 사용법

### LLM 초기화

```python
from langchain_openai import ChatOpenAI
from langchain.schema import HumanMessage, SystemMessage

# LLM 모델 초기화
llm = ChatOpenAI(
    model="gpt-3.5-turbo",
    temperature=0.7,
    max_tokens=1000
)

# 간단한 대화
response = llm.invoke([
    SystemMessage(content="당신은 친절한 AI 어시스턴트입니다."),
    HumanMessage(content="LangChain에 대해 설명해주세요.")
])
print(response.content)
```

### 프롬프트 템플릿

```python
from langchain.prompts import ChatPromptTemplate, MessagesPlaceholder

# 프롬프트 템플릿 생성
prompt = ChatPromptTemplate.from_messages([
    ("system", "당신은 {role}입니다. {style}하게 대답해주세요."),
    ("user", "{input}")
])

# 체인 생성
chain = prompt | llm

# 실행
result = chain.invoke({
    "role": "Python 전문가",
    "style": "친절하고 상세",
    "input": "리스트 컴프리헨션을 설명해주세요."
})
print(result.content)
```

---

## 3. 체인(Chains) 활용하기

### 기본 체인

```python
from langchain.chains import LLMChain
from langchain.prompts import PromptTemplate

# 프롬프트 템플릿
prompt_template = PromptTemplate(
    input_variables=["topic"],
    template="""
    주제: {topic}
    
    위 주제에 대해 다음을 포함하여 설명해주세요:
    1. 정의
    2. 주요 특징
    3. 실제 활용 예시
    """
)

# 체인 생성
chain = LLMChain(llm=llm, prompt=prompt_template)

# 실행
result = chain.run(topic="머신러닝")
print(result)
```

### 순차적 체인

```python
from langchain.chains import SimpleSequentialChain

# 첫 번째 체인: 주제에 대한 설명 생성
explain_chain = LLMChain(
    llm=llm,
    prompt=PromptTemplate(
        input_variables=["topic"],
        template="다음 주제를 초보자도 이해할 수 있게 설명해주세요: {topic}"
    )
)

# 두 번째 체인: 설명을 바탕으로 퀴즈 생성
quiz_chain = LLMChain(
    llm=llm,
    prompt=PromptTemplate(
        input_variables=["explanation"],
        template="다음 설명을 바탕으로 3개의 퀴즈를 만들어주세요:\n\n{explanation}"
    )
)

# 순차적 체인 생성
sequential_chain = SimpleSequentialChain(
    chains=[explain_chain, quiz_chain],
    verbose=True
)

# 실행
result = sequential_chain.run("딥러닝")
print(result)
```

---

## 4. 메모리(Memory) 관리

### 대화 메모리

```python
from langchain.memory import ConversationBufferMemory
from langchain.chains import ConversationChain

# 메모리 초기화
memory = ConversationBufferMemory()

# 대화 체인 생성
conversation = ConversationChain(
    llm=llm,
    memory=memory,
    verbose=True
)

# 대화 진행
print(conversation.predict(input="안녕하세요! 저는 AI를 공부하고 있습니다."))
print(conversation.predict(input="특히 자연어처리에 관심이 많아요."))
print(conversation.predict(input="제가 뭘 공부한다고 했죠?"))  # 이전 대화 기억
```

### 요약 메모리

```python
from langchain.memory import ConversationSummaryMemory

# 요약 메모리 (긴 대화를 요약하여 저장)
summary_memory = ConversationSummaryMemory(llm=llm)

conversation_with_summary = ConversationChain(
    llm=llm,
    memory=summary_memory,
    verbose=True
)

# 긴 대화를 진행하면 자동으로 요약됨
for i in range(5):
    response = conversation_with_summary.predict(
        input=f"머신러닝의 {i+1}번째 중요한 개념을 설명해주세요."
    )
    print(f"Turn {i+1}: {response[:100]}...")
```

---

## 5. 문서 로더와 텍스트 분할

### 문서 로딩

```python
from langchain.document_loaders import TextLoader, PyPDFLoader
from langchain.text_splitter import RecursiveCharacterTextSplitter

# 텍스트 파일 로드
# loader = TextLoader("example.txt", encoding="utf-8")
# documents = loader.load()

# PDF 파일 로드 (예시)
# pdf_loader = PyPDFLoader("example.pdf")
# pdf_documents = pdf_loader.load()

# 샘플 문서 생성
sample_text = """
인공지능(AI)은 인간의 지능을 모방하여 작업을 수행하는 시스템입니다.
머신러닝은 AI의 한 분야로, 데이터로부터 패턴을 학습합니다.
딥러닝은 머신러닝의 한 종류로, 인공 신경망을 사용합니다.
자연어처리(NLP)는 컴퓨터가 인간의 언어를 이해하고 처리하는 기술입니다.
"""

# 텍스트 분할
text_splitter = RecursiveCharacterTextSplitter(
    chunk_size=50,
    chunk_overlap=10,
    length_function=len,
)

chunks = text_splitter.split_text(sample_text)
for i, chunk in enumerate(chunks):
    print(f"Chunk {i+1}: {chunk}")
```

---

## 6. 벡터 스토어와 검색

### 벡터 데이터베이스 구축

```python
from langchain.embeddings import OpenAIEmbeddings
from langchain.vectorstores import Chroma
from langchain.schema import Document

# 임베딩 모델 초기화
embeddings = OpenAIEmbeddings()

# 문서 준비
documents = [
    Document(page_content="Python은 배우기 쉬운 프로그래밍 언어입니다.", metadata={"topic": "programming"}),
    Document(page_content="머신러닝은 데이터로부터 패턴을 학습합니다.", metadata={"topic": "ml"}),
    Document(page_content="딥러닝은 인공 신경망을 사용하는 머신러닝입니다.", metadata={"topic": "dl"}),
    Document(page_content="자연어처리는 텍스트 데이터를 다룹니다.", metadata={"topic": "nlp"}),
]

# 벡터 스토어 생성
vector_store = Chroma.from_documents(
    documents=documents,
    embedding=embeddings,
    persist_directory="./chroma_db"
)

# 유사도 검색
query = "신경망을 사용하는 AI 기술"
results = vector_store.similarity_search(query, k=2)

for i, doc in enumerate(results):
    print(f"Result {i+1}: {doc.page_content}")
    print(f"Metadata: {doc.metadata}\n")
```

---

## 7. RAG (Retrieval-Augmented Generation) 구현

```python
from langchain.chains import RetrievalQA

# QA 체인 생성
qa_chain = RetrievalQA.from_chain_type(
    llm=llm,
    chain_type="stuff",
    retriever=vector_store.as_retriever(search_kwargs={"k": 2}),
    return_source_documents=True
)

# 질문하기
question = "딥러닝과 머신러닝의 관계는 무엇인가요?"
result = qa_chain({"query": question})

print(f"질문: {question}")
print(f"답변: {result['result']}")
print("\n참조한 문서:")
for doc in result['source_documents']:
    print(f"- {doc.page_content}")
```

---

## 8. 에이전트(Agents) 활용

### 도구를 사용하는 에이전트

```python
from langchain.agents import create_react_agent, AgentExecutor
from langchain.tools import Tool
from langchain import hub

# 간단한 도구 정의
def calculate(expression: str) -> str:
    """수학 계산을 수행합니다."""
    try:
        result = eval(expression)
        return f"계산 결과: {result}"
    except:
        return "계산할 수 없는 표현식입니다."

def get_current_time() -> str:
    """현재 시간을 반환합니다."""
    from datetime import datetime
    return f"현재 시간: {datetime.now().strftime('%Y-%m-%d %H:%M:%S')}"

# 도구 리스트
tools = [
    Tool(
        name="Calculator",
        func=calculate,
        description="수학 계산을 수행합니다. 입력: 수식"
    ),
    Tool(
        name="Clock",
        func=get_current_time,
        description="현재 시간을 알려줍니다."
    )
]

# 에이전트 프롬프트 (ReAct 방식)
prompt = hub.pull("hwchase17/react")

# 에이전트 생성
agent = create_react_agent(llm, tools, prompt)
agent_executor = AgentExecutor(agent=agent, tools=tools, verbose=True)

# 에이전트 실행
response = agent_executor.invoke({
    "input": "현재 시간을 알려주고, 3시간 45분 후는 몇 시인지 계산해주세요."
})
print(response["output"])
```

---

## 9. 실전 프로젝트: PDF 문서 기반 Q&A 시스템

```python
# 전체 시스템 구현
class PDFQuestionAnswering:
    def __init__(self, pdf_path=None):
        self.llm = ChatOpenAI(temperature=0)
        self.embeddings = OpenAIEmbeddings()
        self.vector_store = None
        
    def load_pdf(self, pdf_path):
        """PDF 파일을 로드하고 처리합니다."""
        # 실제로는 PyPDFLoader를 사용
        # loader = PyPDFLoader(pdf_path)
        # documents = loader.load()
        
        # 샘플 데이터로 대체
        documents = [
            Document(page_content="LangChain은 LLM 애플리케이션 개발 프레임워크입니다."),
            Document(page_content="체인을 통해 여러 작업을 연결할 수 있습니다."),
            Document(page_content="RAG는 검색 증강 생성 기술입니다."),
        ]
        
        # 텍스트 분할
        text_splitter = RecursiveCharacterTextSplitter(
            chunk_size=1000,
            chunk_overlap=200
        )
        splits = text_splitter.split_documents(documents)
        
        # 벡터 스토어 생성
        self.vector_store = Chroma.from_documents(
            documents=splits,
            embedding=self.embeddings
        )
        
    def ask_question(self, question):
        """질문에 대한 답변을 생성합니다."""
        if not self.vector_store:
            return "먼저 문서를 로드해주세요."
        
        # QA 체인 생성
        qa_chain = RetrievalQA.from_chain_type(
            llm=self.llm,
            chain_type="stuff",
            retriever=self.vector_store.as_retriever(),
            return_source_documents=True
        )
        
        # 질문 처리
        result = qa_chain({"query": question})
        return result['result']

# 시스템 사용
qa_system = PDFQuestionAnswering()
qa_system.load_pdf("dummy_path.pdf")  # 실제로는 PDF 경로

# 질문하기
questions = [
    "LangChain이 무엇인가요?",
    "체인의 역할은 무엇인가요?",
    "RAG란 무엇인가요?"
]

for q in questions:
    answer = qa_system.ask_question(q)
    print(f"\nQ: {q}")
    print(f"A: {answer}")
```

---

## 10. 베스트 프랙티스

### 1. 에러 처리
```python
from langchain.callbacks import StdOutCallbackHandler
from tenacity import retry, stop_after_attempt, wait_exponential

@retry(stop=stop_after_attempt(3), wait=wait_exponential(multiplier=1, min=4, max=10))
def safe_llm_call(chain, input_data):
    try:
        return chain.invoke(input_data)
    except Exception as e:
        print(f"Error: {e}")
        raise
```

### 2. 토큰 관리
```python
import tiktoken

def count_tokens(text, model="gpt-3.5-turbo"):
    encoding = tiktoken.encoding_for_model(model)
    return len(encoding.encode(text))

# 사용 예
text = "이것은 토큰 카운팅 예시입니다."
token_count = count_tokens(text)
print(f"토큰 수: {token_count}")
```

### 3. 스트리밍 응답
```python
from langchain.callbacks.streaming_stdout import StreamingStdOutCallbackHandler

# 스트리밍 LLM
streaming_llm = ChatOpenAI(
    streaming=True,
    callbacks=[StreamingStdOutCallbackHandler()]
)

# 실시간 응답
streaming_llm.invoke("파이썬의 장점을 설명해주세요.")
```

---

## 🎯 연습 문제

1. **채팅봇 만들기**: 메모리를 가진 대화형 챗봇 구현
2. **문서 요약기**: 긴 문서를 요약하는 체인 구현
3. **다국어 번역기**: 여러 언어로 번역하는 순차 체인
4. **코드 리뷰어**: 코드를 분석하고 개선점을 제안하는 에이전트

---

## 📚 추가 학습 자료

- [LangChain 공식 문서](https://python.langchain.com/)
- [LangChain 예제 갤러리](https://github.com/langchain-ai/langchain/tree/master/cookbook)
- [LangSmith (디버깅 도구)](https://smith.langchain.com/)
- [LangChain 커뮤니티](https://github.com/langchain-ai/langchain/discussions)

---

## 🚀 다음 단계

1. **고급 RAG**: 하이브리드 검색, 리랭킹
2. **프로덕션 배포**: API 서버 구축, 스케일링
3. **고급 에이전트**: 멀티 에이전트 시스템
4. **최적화**: 비용 절감, 성능 향상 기법

**실습이 핵심입니다! 작은 프로젝트부터 시작해보세요.** 🔨