# Python for AI - 기초부터 시작하기

## 📌 왜 Python인가?

AI/ML 분야에서 Python이 선호되는 이유:
- 🎯 간단하고 읽기 쉬운 문법
- 📚 풍부한 AI/ML 라이브러리 생태계
- 🚀 빠른 프로토타이핑
- 🤝 활발한 커뮤니티 지원

---

## 1. Python 기초 문법

### 변수와 데이터 타입

```python
# 숫자형
integer_num = 42
float_num = 3.14

# 문자열
name = "AI Study"
multiline = """여러 줄
문자열도
가능합니다"""

# 불린
is_learning = True

# 리스트 (순서가 있고 변경 가능)
scores = [95, 87, 92, 88]

# 튜플 (순서가 있고 변경 불가)
coordinates = (10, 20)

# 딕셔너리 (키-값 쌍)
student = {
    "name": "김철수",
    "age": 25,
    "major": "AI"
}

# 집합 (중복 없음, 순서 없음)
unique_numbers = {1, 2, 3, 3, 4}  # {1, 2, 3, 4}
```

### 조건문과 반복문

```python
# if-elif-else
score = 85
if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
else:
    grade = "C"

# for 반복문
for i in range(5):
    print(f"반복 {i}번째")

# while 반복문
count = 0
while count < 5:
    print(f"카운트: {count}")
    count += 1

# 리스트 컴프리헨션 (파이썬다운 방식)
squares = [x**2 for x in range(10)]
even_squares = [x**2 for x in range(10) if x % 2 == 0]
```

### 함수

```python
# 기본 함수
def greet(name):
    return f"안녕하세요, {name}님!"

# 기본값이 있는 매개변수
def power(base, exponent=2):
    return base ** exponent

# 가변 인자
def sum_all(*args):
    return sum(args)

# 키워드 가변 인자
def print_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

# 람다 함수 (익명 함수)
square = lambda x: x**2
```

---

## 2. AI/ML을 위한 필수 라이브러리

### NumPy - 수치 계산의 기초

```python
import numpy as np

# 배열 생성
arr = np.array([1, 2, 3, 4, 5])
matrix = np.array([[1, 2], [3, 4]])

# 기본 연산
print(arr * 2)  # [2, 4, 6, 8, 10]
print(arr.mean())  # 평균
print(arr.std())   # 표준편차

# 행렬 연산
a = np.array([[1, 2], [3, 4]])
b = np.array([[5, 6], [7, 8]])
print(np.dot(a, b))  # 행렬 곱셈

# 유용한 함수들
zeros = np.zeros((3, 3))  # 0으로 채워진 3x3 행렬
ones = np.ones((2, 4))    # 1로 채워진 2x4 행렬
random = np.random.rand(3, 3)  # 0~1 사이 랜덤 값
```

### Pandas - 데이터 처리의 핵심

```python
import pandas as pd

# DataFrame 생성
data = {
    'name': ['김철수', '이영희', '박민수'],
    'age': [25, 27, 24],
    'score': [85, 92, 88]
}
df = pd.DataFrame(data)

# 데이터 탐색
print(df.head())      # 상위 5개 행
print(df.info())      # 데이터 정보
print(df.describe())  # 통계 요약

# 데이터 선택
print(df['name'])     # 특정 열 선택
print(df[df['age'] > 25])  # 조건부 선택

# 데이터 처리
df['grade'] = df['score'].apply(lambda x: 'A' if x >= 90 else 'B')
df_sorted = df.sort_values('score', ascending=False)
```

### Matplotlib - 데이터 시각화

```python
import matplotlib.pyplot as plt

# 선 그래프
x = np.linspace(0, 10, 100)
y = np.sin(x)
plt.plot(x, y)
plt.title('Sine Wave')
plt.xlabel('X')
plt.ylabel('Y')
plt.show()

# 산점도
x = np.random.rand(50)
y = np.random.rand(50)
plt.scatter(x, y)
plt.title('Random Scatter Plot')
plt.show()

# 히스토그램
data = np.random.normal(100, 15, 1000)
plt.hist(data, bins=30)
plt.title('Normal Distribution')
plt.show()
```

---

## 3. 실습 프로젝트: 간단한 데이터 분석

### 프로젝트: 학생 성적 분석 시스템

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# 1. 데이터 생성
np.random.seed(42)
students = 100

data = {
    'student_id': [f'S{i:03d}' for i in range(1, students + 1)],
    'math': np.random.normal(75, 15, students).clip(0, 100),
    'science': np.random.normal(80, 12, students).clip(0, 100),
    'english': np.random.normal(70, 18, students).clip(0, 100)
}

df = pd.DataFrame(data)

# 2. 총점과 평균 계산
df['total'] = df[['math', 'science', 'english']].sum(axis=1)
df['average'] = df['total'] / 3

# 3. 등급 부여
def assign_grade(avg):
    if avg >= 90: return 'A'
    elif avg >= 80: return 'B'
    elif avg >= 70: return 'C'
    elif avg >= 60: return 'D'
    else: return 'F'

df['grade'] = df['average'].apply(assign_grade)

# 4. 통계 분석
print("=== 과목별 통계 ===")
print(df[['math', 'science', 'english']].describe())

print("\n=== 등급 분포 ===")
print(df['grade'].value_counts().sort_index())

# 5. 시각화
fig, axes = plt.subplots(2, 2, figsize=(12, 10))

# 과목별 점수 분포
subjects = ['math', 'science', 'english']
for i, subject in enumerate(subjects):
    axes[0, 0].hist(df[subject], bins=20, alpha=0.6, label=subject)
axes[0, 0].set_title('Subject Score Distribution')
axes[0, 0].legend()

# 평균 점수 분포
axes[0, 1].hist(df['average'], bins=20, color='green')
axes[0, 1].set_title('Average Score Distribution')

# 등급 분포
grade_counts = df['grade'].value_counts().sort_index()
axes[1, 0].bar(grade_counts.index, grade_counts.values)
axes[1, 0].set_title('Grade Distribution')

# 과목 간 상관관계
axes[1, 1].scatter(df['math'], df['science'], alpha=0.5)
axes[1, 1].set_xlabel('Math')
axes[1, 1].set_ylabel('Science')
axes[1, 1].set_title('Math vs Science Correlation')

plt.tight_layout()
plt.show()

# 6. 상위 10명 학생
print("\n=== 상위 10명 학생 ===")
top_students = df.nlargest(10, 'average')[['student_id', 'average', 'grade']]
print(top_students)
```

---

## 4. AI/ML을 위한 고급 Python 기법

### 클래스와 객체지향 프로그래밍

```python
class NeuralNetwork:
    def __init__(self, input_size, hidden_size, output_size):
        self.input_size = input_size
        self.hidden_size = hidden_size
        self.output_size = output_size
        self.weights = self._initialize_weights()
    
    def _initialize_weights(self):
        # 가중치 초기화 (실제로는 더 복잡함)
        return {
            'W1': np.random.randn(self.input_size, self.hidden_size),
            'W2': np.random.randn(self.hidden_size, self.output_size)
        }
    
    def forward(self, X):
        # 순전파 (간단한 예시)
        self.z1 = np.dot(X, self.weights['W1'])
        self.a1 = self._sigmoid(self.z1)
        self.z2 = np.dot(self.a1, self.weights['W2'])
        output = self._sigmoid(self.z2)
        return output
    
    @staticmethod
    def _sigmoid(x):
        return 1 / (1 + np.exp(-x))

# 사용 예시
nn = NeuralNetwork(input_size=3, hidden_size=4, output_size=1)
input_data = np.array([[1, 2, 3]])
output = nn.forward(input_data)
print(f"Output: {output}")
```

### 데코레이터

```python
import time

# 실행 시간 측정 데코레이터
def measure_time(func):
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} 실행 시간: {end - start:.4f}초")
        return result
    return wrapper

@measure_time
def train_model(epochs):
    # 모델 학습 시뮬레이션
    time.sleep(0.1 * epochs)
    return "학습 완료"

result = train_model(5)
```

### 제너레이터 (메모리 효율적인 데이터 처리)

```python
# 대용량 데이터를 메모리 효율적으로 처리
def data_generator(file_path, batch_size=32):
    """배치 단위로 데이터를 읽어오는 제너레이터"""
    with open(file_path, 'r') as f:
        batch = []
        for line in f:
            batch.append(line.strip())
            if len(batch) == batch_size:
                yield batch
                batch = []
        if batch:  # 마지막 배치
            yield batch

# 사용 예시 (파일이 있다고 가정)
# for batch in data_generator('large_dataset.txt'):
#     process_batch(batch)
```

---

## 5. 연습 문제

### 문제 1: 데이터 전처리
```python
# 주어진 데이터에서 이상치를 제거하고 정규화하세요
data = [1, 2, 3, 100, 4, 5, 6, -50, 7, 8, 9]

# 힌트: IQR(사분위수 범위)를 사용하여 이상치 제거
# 정규화: (x - min) / (max - min)
```

### 문제 2: 간단한 분류기
```python
# K-최근접 이웃(KNN) 분류기를 구현하세요
class SimpleKNN:
    def __init__(self, k=3):
        self.k = k
        
    def fit(self, X, y):
        # 학습 데이터 저장
        pass
    
    def predict(self, X):
        # 예측 구현
        pass
```

### 문제 3: 데이터 시각화
```python
# 주어진 데이터로 다양한 차트를 그리세요
# 1. 시계열 데이터 라인 차트
# 2. 카테고리별 막대 그래프
# 3. 상관관계 히트맵
```

---

## 🎯 다음 단계

1. **NumPy 심화**: 브로드캐스팅, 고급 인덱싱
2. **Pandas 심화**: GroupBy, Merge, Pivot
3. **시각화 심화**: Seaborn, Plotly
4. **ML 라이브러리**: Scikit-learn 시작하기

---

## 📚 추가 학습 자료

- [Python 공식 튜토리얼](https://docs.python.org/ko/3/tutorial/)
- [NumPy 공식 문서](https://numpy.org/doc/stable/)
- [Pandas 공식 문서](https://pandas.pydata.org/docs/)
- [Matplotlib 갤러리](https://matplotlib.org/stable/gallery/index.html)

**기억하세요**: 코드는 직접 작성하면서 배우는 것이 가장 효과적입니다! 💪