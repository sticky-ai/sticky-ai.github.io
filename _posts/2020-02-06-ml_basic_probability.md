---
title: ML-BASIC. PART 3. Probability
date: 2020-02-06
categories:
- Machine Learning
tags:
- Machine Learning
- Probability
---

## 사건집합(Event Set)
`사건집합(Event Set)`은 가능한 모든 사건$(e)$들의 집합을 의미하며, $\Omega$(오메가)로 표현합니다. 예를 들어, 동전 던지기 게임을 한다고 가정하면, 가능한 모든 사건은 앞면이 나오는 경우와 뒷면이 나오는 경우 2가지가 존재합니다. 이는 가능한 모든 사건의 개수가 유한하기 때문에 이산(Discrete) 이라고 하며, 사건의 개수가 무한할 때는 연속(Continuous)라고 합니다.
  * 사건집합 : $$\Omega = \{e_1, e_2, \cdots, e_D\}$$
  * 이산 : $\| \Omega \| < \infty$
  * 연속 : $\| \Omega $\| = \infty$


## 확률변수(Random Variable)
사건집합 안에 속하지만 정의되지 않은 값입니다. 값이 정해지지 않은 변수이며, 사건 집합 안에서 어떠한 값도 될 수 있습니다. 확률 변수를 $X$라 정의하면, 확률 변수는 다음과 같이 표현할 수 있습니다. 

$$X \in \Omega$$

## 확률(Probability)
사건 집합 안에 속한 확률변수에 특정 값을 지정해줍니다. 동전 던지기 게임에서 앞면이 나올 사건을 $e_0$, 뒷면이 나올 사건을 $e_1$라고 정의하면 사건집합 $\Omega$는 $\{e_0, e_1\}$로 구성됩니다. 여기서, 앞면이 나올 확률은 $p(X = e_0)$, 뒷면이 나올 확률은 $p(X = e_1)$와 같이 나타냅니다. 이를 일반화하여 표현하면
다음과 같습니다.

$$ p(X = e_i) $$

## 확률의 특성(Properties)
1. Non-negatives : $p(X=e_i) \geq 0$, 확률은 음수가 될 수 없습니다. 확률은 0에서 100 범위로 존재하며, 100이 - 값을 가지는 확률은 존재하지 않습니다.
  
2. Unit Volume : $\sum_{e \in \Omega}p(X = e) = 1$, 모든 확률의 합은 1이 되어야 합니다. 동전 던지기 게임에서 사건 집합은 동전 앞면이 나오는 경우와 동전 뒷면이 나오는 2가지 경우가 존재하며, 앞면이 나올 확률과 뒷면이 나올 확률은 각각 0.5이기에, 이를 모두 더하면 1이라는 값이 나오게 됩니다.

## 다중확률변수(Multiple Random Variable)
확률 변수가 여러개의 벡터 형태로 구성될 때, 이를 `다중확률변수(Multiple Random Variable)`이라 합니다. 동전 던지기 게임을 독립적으로 2번 시행했을 때 각각의 확률 변수를 $X$와 $Y$로 표현할 수 있습니다. 

### 결합확률(Joint Probability) / 주변확률(Marginal Probability) / 조건부확률(Conditional Probability)
`결합확률(Joint Probability)`은 사건 X와 사건 Y가 동시에 발생할 확률입니다. 이는 $p(X, Y)$와 같이 나타냅니다. 결합확률과 대비되는 개념으로 `주변확률(Marginal Probability)`이 있습니다. 주변확률은 개별 사건의 확률 $p(X)$, $p(Y)$와 같이 나타냅니다. `조건부확률(Conditional Probability)`는 사건 Y가 특정 확률변수값을 가질 때, 사건 X에 대한 확률을 의미하며, $p(X|Y)$와 같이 표현합니다. 조건부확률의 값은 다음과 같이 정의될 수 있습니다.

$$ p(X|Y) = \frac{P(X, Y)}{p(Y)}$$

## Keyword
`확률(Probability)` `사건집합(Event Set)` `확률변수(Random Variable)` `다중확률변수(Multiple Random Variable)` `결합확률(Joint Probability)` `주변확률(Marginal Probability)` `조건부확률(Conditional Probability)`

## References
**Machine Learning for NLP**의 모든 포스팅은 뉴욕대 조경현 교수님의 '딥러닝을 이용한 자연어 처리' MOOC 강의를 정리한 것입니다. (https://www.edwith.org/deepnlp/joinLectures/17363)
