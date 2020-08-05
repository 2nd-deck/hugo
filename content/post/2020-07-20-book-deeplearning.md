---
title: Book - 딥러닝 입문 / 박해선
date: 2020-07-20
categories: ["No.1 Hold"]
---

딥러닝 입문 - 박해선

## 기본정보

*   이지스퍼블리싱 2020

## 감상
AI, 머신러닝, 딥러닝, 강화학습등 말만 어려운데 그 안에 있는 선형회귀, 경사 하강법, 에포크등은 도저히 감이 잡히지 않았다. 딥러닝 관련 책 중 가장 쉬운걸로 빌린 것이 이 책! 구글 코랩으로 설치 압박이 적어 누구나 실습하면서 개념을 이해하기 쉬울 것 같다.  

## 주요내용
### 파이썬 패키지
1. 넘파이 : 딥러닝 분야에서 이것을 사용하는 이유는 '저수준 언어로 다차원 배열을 구현 했기 때문에 다차원 배열의 크기가 커져도 높은 성능을 보장한다.'는 점이다. (import numpy as np)
2. 맷플롯립 : 파이썬 과학 생태계의 표준 그래프 패키지 (import matplotlib.pyplot as plt)


### 수치 예측
1. 선형 회귀 : 딥러닝의 기초이며 1차 함수로 표현. 
일정을 적어두면 자연스럽게 우선순위가 올라간다. 매주 같은 시간으로 꾸준한 일정을 짜는 게 좋다. 프로젝트 기간을 결정한다. 마지막으로 이 모든 정보를 달력에 써 넣어라.
2. 경사하강법 : 모델이 데이터를 잘표현할 수 있도록 기울기를 사용하여 모델을 조금씩 조정하는 최적화 알고리즘
3. 오차역전파 : y와 y_hat의 차이를 이용하여 w와 b를 업데이트
```
err = y[0] - y_hat
w_new = w + w_rate * err
b_new = b + 1 * err
print(w_new, b_new)
```
이렇게 x[1]에 대한 값으로 전체 데이터를 모두 이용하는 한 단위의 작업을 에포크라고 한다.   
4. 손실 함수 : 제곱 오차의 최소값을 알아내기 위해 가중치나 절편에 대해 미분을 한다. SE = 1/2 * (y-y_hat)^2을 미분하면 오차역전파와 동일하다.
```
err = y_i - y_hat
b = b + 1 * err
```
5. 경사하강법으로 간단한 뉴런 만들기
```
class Neuron;
    def__init__(self):
        self.w = 1.0    # 가중치 초기화
        self.b = 1.0    # 절편 초기화
    def forpass(self, x):
        y_hat = x * self.w + self.b     # 직선 방정식을 계산
        return y_hat
    def backprop(self,x, err):
        w_grad = x * err    # 가중치에 대한 그레디언트 계산
        b_grad = 1 * err    # 절편에 대한 그레디언트 계산
        return w_grad, b_grad
    def fit(self, x, y, epochs=100):
        for x_i, y_i in zip(x,y):   # 모든 샘플에 대해 반복
            y_hat = self.forpass(x_i)   # 정방향 계산
            err = -(y_i - y_hat)        # 오차계산
            w_grad, b_grad = self.backprop(x_i, err)    # 역방향 계산
            self.w -=w_grad # 가중치 업데이트
            self.b -=b_grad # 가중치 업데이트

```
neuron = Neuron()   
neuron.fit(x, y)

### 이진 분류
1. 퍼셉트론 : 선형함수에 계단함수(z>0 여부에 따라 y = 1 or -1)를 더해 결과 판단 z = w1x1 + ... + wnxn + b
![perceptron](/img/perceptron.jpg)
2. 아달린 : 적응형 선형 뉴런. 선형함수의 결과를 학습에 사용
![adalin](/img/adalin.jpg)
3. 로지스틱 회귀 : 선형 함수를 통과시켜 얻은 z를 임계 함수에 보내기 전에 변형 시키는데 이런 함수를 활성화 함수라고 부른다. 이때 활성화 함수를 시그모이드 함수라고 한다. 
![logistic](/img/logistic.jpg)
4. 시그모이드 함수 : ( p = 1 / (1+e^(-z)))
![sigmoid](/img/sigmoid.jpg)
![logistic2](/img/logistic2.jpg)
5. 로지스틱 손실 함수 : L = -(y log(a) + (1-y) log(1-a))   
    - y가 1인 경우(양성클래스) = -log(a)
    - y가 0인 경우(양성클래스) = -log(1-a)
이것을 미분하면   
    - 가중치에 대한 미분 = -(y-a)xi
    - 절편에 대한 미분 = -(y-a)1

+ 선형 회귀나 로지스틱 회귀는 모두 경사 하강법 사용. 경사 하강법은 손실 함수의 결과값을 최소화하는 경향으로 가중치를 업데이트
+ 경사 하강법의 종류
    - 확률적 경사 하강법 : 샘플 데이터 1개에 대한 그레디언트 계산. 계산 비용은 적은 대신 가중치가 최적값에 수렴하는 과정이 불안정.
    - 배치 경사 하강법 :  전체 훈련 세트를 사용하여 한 번에 그레디언트를 계산하는 방식. 가중치가 최적값에 수렵하는 과정은 안정적이지만 계산 비용이 많이 듦.
    - 미니 배치 경사 하강법 :  배치 크기를 작게 하여(훈련 세트를 여러번 나누어) 처리하는 방식. 두 방법의 장점을 절충한 방식. 
    ![descent](/img/descent.jpg)
+ 에포크마다 훈련 세트를 무작위로 섞어 손실 함수의 값을 줄이면 정확도를 높일 수 있다.



### 훈련 노하우
+ 실전에서 수집된 데이터는 잘 가공되어 있지 않으므로 데이터 전처리가 필요.   
훈련세트에서 스케일링 된 값을 검증세트에 반영.

+ 과대적합, 과소적합
    - 과대적합이란 모델이 훈련 세트에서는 좋은 성능을 내지만 검증 세트에서는 낮은 성능을 내는 것. 과소적합은 훈련세트와 검증 세트의 성능에는 차이가 크지 않지만 모두 낮은 성능을 내는 것.
    - 과대적합(분산이 크다)의 주요 원인 중 하나는 훈련 세트에 충분히 다양한 패턴의 샘플이 포함되지 않은 경우이다. 더 많은 훈련 샘플을 모은다. 또는 모델이 훈련 세트에 집착하지 않도록 가중치를 제한할 수 있다.(모델의 복잡도를 낮춘다.)
    - 과소적합(편향이 크다)은 모델이 충분히 복잡하지 않아 훈련 데이터에 있는 패턴을 모두 잡아내지 못하는 현상. 해결하는 방법은 복잡도가 더 높은 모델을 사용하거나 가중치의 규제를 완화하는 것이다.
    - 에포크와 손실 함수의 그래프, 모델 복잡도와 손실 함수의 그래프로 과대/소적합을 분석할 수 있다. 지금은 훈련 세트의 크기나 모델의 복잡도를 변화시키기 어려우므로 적절한 에포크 횟수를 찾아본다.
+ 적절한 편향-분산 트레이드 오프 선택
+ 과대적합을 해결하는 대표적인 방법 중 하나로 가중치 규제가 있다. 규제를 사용하여 가중치를 제한하면 모델이 몇 개의 데이이터에 집착하지 않게 되므로 일반화 성능을 높일 수 있다.
    - L1 규제: 손실 함수의 가중치의 절댓값인 L1 norm을 추가한다. 회귀 모델에 L1 규제를 추가한 것을 라쏘 모델이라 한다. (w_grad += alpah * np.sign(w)) 사이킷런에서 sklearn.linear_model.Lasso 클래스에서 라쏘 모델을 제공한다. L1 규제는 규제 하이퍼파라미터 a에 많이 의존한다.
    - L2 규제: 손실 함수에 가중치에 대한 L2 norm의 제곱을 더한다.(w_grad += alpha * w) 회귀 모델에 L2 규제를 적용한 것을 릿지 모델이라고 한다. 사이킷런에서 sklearn.linear_model.Ridge 클래스를 제공한다. SGDClassifier 클래스에서는 penalty 매개변수를 l2로 지정하여 L2 규제를 추가할 수 있다. 두 클래스 모두 규제의 강도는 alpha 매개변수로 제어한다.
+ 교차검증 
    - 검증 세트를 훈련 세트에서 분리하느라 훈련 세트의 샘플 개수가 줄어든다.
    - 교차 검증은 훈련 세트를 k개의 작은 덩어리(폴드)로 나누고 그중 하나를 검증에 사용하고 나머지를 훈련에 사용한다. 검증에 사용하는 하나의 폴드는 k개가 번갈아 가면서 수행한다. k-폴드 교차 검증 
    - 사이킷런 model_selection 모듈의 cross_validate()함수로 교차 검증이 가능하다.






## 실습 5장
```
import numpy as np
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
cancer = load_breast_cancer()
x = cancer.data
y = cancer.target
x_train_all, x_test, y_train_all, y_test = train_test_split(x, y, stratify=y, test_size=0.2, random_state=42)
x_train, x_val, y_train, y_val = train_test_split(x_train_all, y_train_all, stratify=y_train_all, test_size=0.2, random_state=42)

from sklearn.linear_model import SGDClassifier
sgd = SGDClassifier(loss='log', random_state=42)
sgd.fit(x_train, y_train)
sgd.score(x_val, y_val)

```
하이퍼파라미터 : loss와 같은 매개변수의 값은 가중치나 절편처럼 알아서 학습되지 않음. 사용자가 직접 선택.
loss를 log로 했을떄 score는 0.8333, hinge로 했을때 score는 0.93859
이러한 작업을 '모델을 튜닝한다'라고 함.
테스트 모델로 모델을 튜닝하면 실전에서 좋은 성능을 기대하기 어렵다. 그러므로 검증 세트를 따로 준비 한다.
train과 test를 8:2로 나눈뒤, train을 다시 검증세트와 8:2로 나눈다. 대략 6:2:2 = train : val : test
```
import matplotlib.pyplot as plt
print(cancer.feature_names[[2,3]])
plt.boxplot(x_train[:,2:4])
plt.xlabel('feature')
plt.ylabel('value')
plt.show()
```
두 특성의 스케일 차이가 크다. mean perimeter는 주로 100~200에 값들이 위치한 반면에 mean area는 200~2,000 사이에 값들이 집중되어 있다
```
class SingleLayer:
  def __init__(self, learning_rate=0.1):
    self.w = None
    self.b = None
    self.losses = []
    self.val_losses = [] # 검증 세트의 손실 변수 추가
    self.w_history = []
    self.lr = learning_rate
  def forpass(self, x):
    z = np.sum(x * self.w) + self.b
    return z

  def backprop(self, x, err):
    w_grad = x * err
    b_grad = 1 * err
    return w_grad, b_grad

  def fit(self, x, y, epochs=100, x_val= None, y_val=None):
    self.w = np.ones(x.shape[1])
    self.b = 0
    self.w_history.append(self.w.copy())
    np.random.seed(42)
    for i in range(epochs):
      loss = 0
      indexes = np.random.permutation(np.arange(len(x)))
      for i in indexes:
        z = self.forpass(x[i])
        a = self.activation(z)
        err = -(y[i] - a)
        w_grad, b_grad = self.backprop(x[i], err)
        self.w -= self.lr * w_grad  # 가중치 업데이트(학습률 적용)
        self.b -= b_grad            # 절편 업데이트
        # 가중치 기록
        self.w_history.append(self.w.copy())
        # 안전한 로그 계산을 위해 클리핑한 후 손실을 누적
        a = np.clip(a, 1e-10, 1-1e-10)
        loss += -(y[i]*np.log(a)+(1-y[i])*np.log(1-a))

      # 에포크마다 평균 손실을 저장
      self.losses.append(loss/len(y))
      # 검증 세트에 대한 손실을 계산
      self.update_val_loss(x_val, y_val)

  def update_val_loss(self, x_val, y_val):
    if x_val is None:
      return
    val_loss = 0
    for i in range(len(x_val)):
      z = self.forpass(len(x_val))
      a = self.activation(z)
      a = np.clip(a, 1e-10, 1-1e-10)
      val_loss += -(y_val[i]*np.log(a)+(1-y_val[i])*np.log(1-a))
    self.val_losses.append(val_loss/len(y_val))
  #활성화함수
  def activation(self, z):
    a = 1 / (1 + np.exp(-z))                    # 시그모이드 계산
    return a

  #예측 수행
  def predict(self, x):
    z = [self.forpass(x_i) for x_i in x]
    #a = self.activation(np.array(z))
    return np.array(z) > 0  # 계단함수 사용.
  
  def score(self, x, y):
    return np.mean(self.predict(x) == y)
```
learning rate는 학습률로 하이퍼파라미터이다. 이 값으로 가중치의 업데이트 양을 조절 (보통 0.001, 0.01)등의 로그 스케일로 학습률을 지정하여 테스트.
가중치가 바뀔 떄마다 w_history 리스트에 가중치를 기록한다.넘파이 배열을 리스트에 추가하면 실제 값이 복사되는 것이 아니라 배열을 참조하기 때문에 가중치 변수 self.w의 값이 바뀔 때마다 그 값을 복사하여 w_history에 추가해야 한다. 또 w_grad에 학습률 self.lr을 곱하는 연산이 추가되어 가중치 업데이트 양을 조절.
```
layer1 = SingleLayer()
layer1.fit(x_train, y_train)
layer1.score(x_val, y_val)
```
```
w2 = []
w3 = []
for w in layer1.w_history:
  w2.append(w[2])
  w3.append(w[3])
plt.plot(w2, w3)
plt.plot(w[-1], w3[-1], 'ro')
plt.xlabel('w[2]')
plt.ylabel('w[3]')
plt.show()
```
세번째, 네번째 요소 w[2], w[3]은 각각 mean perimeter와 mean area 특성에 대한 가중치이다.
mean perimeter에 비해 mean area의 스케일이 크므로 w3 값이 학습 과정에서 큰 폭으로 흔들리며 변화하고 있다. 반면에 w2 값은 0부터 시작하여 조금씩 최적값에 가까워진다. 이 그래프의 현상을 'w3에 대한 그레이디언트가 크기 때문에 w3축을 따라 가중치가 크게 요동치고 있다.'라고 말한다. 이러한 현상을 줄이기 위해 스케일을 조정한다.
신경망에서 자주 사용하는 스케일 조정 방벙중 하나는 표준화(standardization)이다. 표준화는 특성값에서 평균을 뺴고 표준 편차로 나눈다. 표준화를 하면 평균이 0이고 분산이 1인 특성이 만들어진다.  x=(x−μ)/s 
사이킷런에는 StandardScaler 클래스가 있다. 여기서는 직접 표준화 구현
```
train_mean = np.mean(x_train, axis=0)
train_std = np.std(x_train, axis=0)
x_train_scaled = (x_train - train_mean) / train_std
```
넘파이의 mean(), std()함수로 평균과 표준 편차를 계산
표준화를 구현한 다음에 특성별로 스케일을 조정
```
layer2 = SingleLayer()
layer2.fit(x_train_scaled, y_train)
w2 = []
w3 = []
for w in layer2.w_history:
  w2.append(w[2])
  w3.append(w[3])
plt.plot(w2,w3)
plt.plot(w2[-1], w3[-1], 'ro')
```
검증 결과가 좋지 않다. 검증세트도 표준화 전처리를 적용해야함
```
val_mean = np.mean(x_val, axis=0)
val_std = np.std(x_val, axis=0)
x_val_scaled = (x_val - val_mean) / val_std
layer2.score(x_val_scaled, y_val)
```
```
plt.plot(x_train[:50,0], x_train[:50, 1],'bo')
plt.plot(x_val[:50,0],x_val[:50,1], 'ro')
plt.xlabel('fature 1')
plt.ylabel('fature 2')
plt.legend(['train set', 'val. set'])
plt.show()
```
```
plt.plot(x_train_scaled[:50,0], x_train_scaled[:50, 1],'bo')
plt.plot(x_val_scaled[:50,0],x_val_scaled[:50,1], 'ro')
plt.xlabel('fature 1')
plt.ylabel('fature 2')
plt.legend(['train set', 'val. set'])
plt.show()
```
훈련 세트와 검증 세트가 다른 비율로 스케일이 조정된 경우, 훈련 세트와 검증 세트의 점과 점 사이의 거리가 변환된 이후에 그대로 유지되지 않음. 데이터를 제대로 전처리 했다면 훈련 세트와 검증 세트의 거리가 그대로 유지되어야 함. 점과 점사이 거리가 달라지 ㄴ이유는 훈련 세트와 검증 세트를 각각 다른 비율로 전처리했기 떄문이다.
```
x_val_scaled = (x_val - train_mean) / train_std
plt.plot(x_train_scaled[:50,0], x_train_scaled[:50, 1],'bo')
plt.plot(x_val_scaled[:50,0],x_val_scaled[:50,1], 'ro')
plt.xlabel('fature 1')
plt.ylabel('fature 2')
plt.legend(['train set', 'val. set'])
plt.show()
```

```
layer3 = SingleLayer()
layer3.fit(x_train_scaled, y_train, x_val=x_val_scaled, y_val=y_val)
layer3.update_val_loss(x_val_scaled, y_val)
```
훈련세트와 검증세트의 에포크당 손실률을 그래프로 그려본다
```
plt.ylim(0, 0.3)
plt.plot(layer3.losses)
plt.plot(layer3.val_losses)
plt.xlabel('loss')
plt.ylabel('epoch')
plt.legend(['train loss', 'val_loss'])
plt.show()
```
#20번의 에포크까지 모델을 훈련
layer4 = SingleLayer()
layer4.fit(x_train_scaled, y_train, epochs=20)
layer4.score(x_val_scaled, y_val)

## 5장 규제


