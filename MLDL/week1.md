# 머신러닝+딥러닝 CH 01-02


## MLDL_1st_TIL

### 1장 나의 첫 머신러닝
#### 01. 인공지능과 머신러닝, 딥러닝
#### 02. 코랩과 주피터 노트북
#### 03. 마켓과 머신러닝

### 2장 데이터 다루기
#### 01. 훈련 세트와 테스트 세트
#### 02. 데이터 전처리


## Study Schedule

| 주차  | 공부 범위     | 완료 여부 |
| ----- | ------------- | --------- |
| 1주차 | p.26~111    | ✅         |
| 2주차 | p.114~173   | 🍽️         |
| 3주차 | p.176~217  | 🍽️         |
| 4주차 | p.220~283 | 🍽️         |
| 5주차 | p.286~337 | 🍽️         |
| 6주차 | p.340~420 | 🍽️         |
| 7주차 | p.423~483 | 🍽️         |
| 8줓   | p.486~558 | 🍽️         |
<br>

<!-- 여기까진 그대로 둬 주세요-->


# 1️⃣ 개념 정리 

## 01-1. 인공지능과 머신러닝, 딥러닝

### 인공지능이란
\- `인공지능` : 사람처럼 학습하고 추론할 수 있는 지능을 가진 컴퓨터 시스템을 만드는 기술    
\- `강인공지능`(인공일반지능) : 영화 속 인공지능처럼 사람과 구분하기 어려운 지능을 가짐    
\- `약인공지능` : 특정 분야에서 사람의 일을 도와주는 보조 역할 (음성 비서, 자율 주행 자동차, 음악 추천 기계 번역 등)

### 머신러닝이란
\- `머신러닝` : 규칙을 일일이 프로그래밍 하지 않아도 자동으로 데이터에서 규칙을 학습하고 알고리즘을 연구하는 분야    
\- `사이킷런` : 대표적인 머신러닝 라이브러리

### 딥러닝이란
\- `딥러닝` : 머신러닝 알고리즘 중에 **인공 신경망**을 기반으로한 방법   
_이미지 분류 작업에 **합성곱 신경망**이 널리 사용되기 시작함_   
\- `텐서플로` : 구글이 공개한 딥러닝 라이브러리 오픈소스   
\- `파이토치` : 페이스북이 공개한 딥러닝 라이브러리   


## 01-2. 코랩과 주피터 노트북

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
> **이미 코랩 노트북이 5개 실행중이라면**

[런타임] → [세션 관리] 메뉴 선택하여 실행 중인 노트북을 종료할 수 있음.

## 01-3. 마켓과 머신러닝

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
### [k-최근접 이웃]
### 실습   
**1. 도미 데이터, 방어 데이터를 하나의 데이터로 합침.**  
~~~python
length = bream_length + smelt_length
weight = bream_weight + smelt_weight
~~~
**2. `사이킷럿` 패키지 사용, 그 전에 2차원 리스트를 만들어야 함.**  
~~~python
fish_data = [[l,w] for l, w in zip(length, weight)]
~~~
**3. 정답 데이터 준비하기**   
: 도미 데이터는 1, 빙어 데이터는 0으로 표현   
~~~python
fish_target = [1] * 35 + [0] * 14
print(fish_target)
~~~
**4. 알고리즘 준비**   
~~~python
from sklearn.neighbors improt KNeighborsClassifier
kn=KNeighborsClassifier()
kn.fit(fish_data, fish_target) # fit()메서드는 주어진 데이터로 알고리즘을 훈련시킨 뒤 훈련함.
kn.score(fish_data, fish_target) # score() 매서드는 모델을 평가하며 0과 1 사이의 값을 반환함. 즉 이 값을 정확도라고 부름.
~~~   
**5. k-최근접 이웃 알고리즘 실행**
~~~python
plt.scatter(bream_length, bream_weight)
plt.scatter(smelt_length, smelt_weight)
plt.scatter(30, 600, marker='^')
plt.xlabel('length')
plt.ylabel('weight')
plt.show()
~~~
~~~python
kn.predict([[30, 600]]) # predict() 매서드는 새로운 데이터의 정답을 예측함.
# 길이가 30, 무게가 600인 점(세모 점)의 정답을 예측함.
print(kn._fit_X)
print(kn._y)
kn49 = KNeighborsClassifier(n_neighbors=49) # 기본적으로 가까운 5개 데이터를 참고하지만, 해당 코드는 참고 데이터를 49개로 한 kn49모델

kn49.fit(fish_data, fish_target)
kn49.score(fish_data, fish_target) # 정확도 0.715
# 처음에 5개로 실행했을 때는 정확도가 1.0인 것을 비교하면 kn49보다 기본값이 좋음.
pritn(35/49)
~~~

## 02-1 훈련 세트와 테스트 세트
### [지도 학습과 비지도 학습]
\* `지도 학습` : 입력(데이터)과 타깃(정답)으로 이뤄진 훈련 데이터가 필요.   
$\rightarrow$ 지도 학습은 정답(타깃)이 있으니 알고리즘이 정답을 맞히는 것을 학습함.    
\* `비지도 학습` : 타깃 없이 입력 데이터만 사용, 데이터를 잘 파악하거나 변형하는 데 도움을 줌.    
_k-최근점 이웃 알고리즘 : 지도 학습 (입력 데이터와 타깃(정답)을 사용했으므로)


### [훈련 세트와 테스트 세트]
\* 이미 준비된 데이터 중에서 일부를 떼어 내어 훈련/테스트 세트를 만듦.   
\- `훈련 세트` : 훈련에 사용되는 데이터    
\- `테스트 세트` : 평가에 사용하는 데이터   

<br>

\* 전체 데이터에서 처음 35개 셈플을 선택함.   
\* 일반적으로 리스트 처럼 배열의 요소를 선택할 때는 배열의 위치, 즉 `인덱스`를 지정함.    
~~~python
print(fish_data[4])
print(fish_data[0:5]) # 슬라이싱 연산자는 인덱스의 범위를 지정해 여러개 원소를 선택할 수 있음.
# *이때 마지막 인덱스의 원소는 포함되지 않음. 0~4까지의 5개 원소만 선택됨.
print(fish_data[44:]) # 44번째부터 5개의 샘플을 추출함
~~~
~~~python
train_input = fish_data[:35]
train_target = fish_target[:35]
test_input = fish_data[35:]
test_target = fish_target[35:]
~~~

### [샘플링 편향]
: 훈련 세트와 테스트 세트에 샘플이 골고루 섞여 있지 않으면 샘플링이 한쪽으로 치우침.

### [넘파이]
: 파이썬의 대표적인 **배열** 라이브러리
~~~python
import numpy as np
input_arr = np.array(fish_data)
target_arr = np.array(fish_target)
print(input_arr)
~~~
$\rightarrow$ 이 배열에서 랜덤하게 샘플을 선택해 훈련/테스트 세트를 만듦.   
*주의할 점 : input_arr과 target_arr에서 같은 위치는 함께 선택되어야 함*   
~~~python
np.random.seed(42) # 실행할 때마다 일정한 결과 얻음
index=np.arange(49)
np.random.shuffle(index)
~~~

### [k-최근접 알고리즘 다시]
~~~python
kn = kn.fit(train_input, train_target)
kn.score(test_input, test_target)
kn.predict(test_input)
test_target
~~~

## 02-2 데이터 전처리
### [넘파이로 데이터 준비하기]
\- **np.`column_stack`(([1,2,3], [4,5,6]))**
: 전달받은 리스트를 일렬로 세운 다음 차례대로 나란히 연결함.
~~~python
import numpy as np
fish_data = np.column)stack((fish_length, fish_weight))
print(fish_data[:5])
~~~
\-**`np.ones()`, `np.zeros()`** : 각각 원하는 개수의 1과 0을 채운 배열을 만들어 줌.   
\-**`np.concatenate()`** : 첫 번째 차원을 따라 배열을 연결함.   
~~~python
fish_target = np.concatenate((np.ones(35), np.zeros(14)))
~~~

### [사이킷런으로 훈련 세트와 테스트 세트 나누기]
\-**`train_test_split()`** : 전달되는 리스트나 배열을 비율에 맞게 훈련/테스트 세트로 나누어 줌.   
*기본적으로 25%를 테스트 세트로 떼어냄*    
~~~python
from sklearn.model_selection import train_test_split
train_input, test_input, train_target, test_target= `train_test_split`(fish_data, fish_target, random_state=42)

# 무작위로 잘 섞이지 않았을 경우
train_input, test_input, train_target, test_target= train_test_split(fish_data, fish_target, `stratify=fish_target`, random_state=42)
~~~

### [기준 맞춰라]
\- 산점도의 x축, y축 범위를 비슷하게 맞춰야 함.     
\- `xlim()` : 맷플롯립에서 x축 범위를 지정할 때    
\- `ylim()` : 맷플롯립에서 y축 범위를 지정할 때    
~~~
- 대부분의 알고리즘들은 샘플 간의 거리에 영향을 많이 받으므로 특성값을 일정한 기준으로 맞춰야 한다.
- 이러한 작업을 **데이터 전처리** 라고 부름.
~~~

### [스케일이 다른 특성 처리]

> **표준점수(z 점수)**
각 특성값이 0에서 표준편차의 몇 배만큼 떨어져 있는지를 나타냄. 

~~~python
mean=np.mean(train_input, axis=0) # np.mean() 평균 계산
std=np.std(train_input, asxis=0) # np.std() 표준편차 계산
train_scaled = (train_input - mean) / std
~~~

\* **훈련 세트를 변환한 방식 그대로 테스트 세트를 변환해야 함!!!**

