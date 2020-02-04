---
title: ML-BASIC. Part 1. Overview
description: 
categories:
 - Machine Learning
tags:
 - Machine Learning
 - Supervised Learning
---

## Keyword
* 알고리즘 (Algorithm)
* 머신러닝 (Machine Learning)
* 지도학습 (Supervised Learning)
* 훈련샘플 (Training Examples)
* 가설집합 (Hypothesis Sets)
* 검정세트 (Validation Set)
* 테스트셋 (Test Set)
* 비용함수 (Loss Function)
* 최적화 알고리즘 (Optimization Algorithm)

`알고리즘(Algorithm)`은 어떠한 문제를 해결하기 위한 일련의 명령을 의미합니다. 머신러닝 기술이 적용되기 이전에는 1) 문제에 대한 자세한 설명이 주어지고 2) 해당 문제를 해결하기 위한 알고리즘을 설계하는 방식으로 진행되었습니다.

시대가 변화하면서 머신러닝 기술이 발달하게 되면서 문제의 해결 방식이 달라지게 되었습니다. `머신러닝(Machine Learning)`을 활용한 문제 해결 방법은 1) 대략적인 문제에 대한 설명이 주어지고 2) `훈련샘플(Training Examples)`이 제공되며 3) 문제 해결을 위한 **학습**을 진행합니다.

## Machine Learning Algorithm
머신러닝 알고리즘은 크게 `지도학습(Supervised Learning)`과 `비지도학습(Unsupervised Learning)`으로 구분됩니다. 지도학습은 주어진 데이터셋에 학습 데이터 $x$와 결과값 $y$가 동시에 주어지는 경우를 의미하며, 비지도학습은 $x$만 주어집니다. 다만, $y$값이 존재하지 않는 비지도학습 문제인 경우 실무에서는 거의 사용되지 않으며, 레이블링을 진행하여 지도학습 문제로 바꾸어 진행하는 경우가 많습니다.

### Supervised Learning
지도학습 기반의 머신러닝 모델을 구축하기 위해서는 아래 3가지가 제공되어야 하며, 2가지를 결정해야 합니다. 

* **Provided**
  * Dataset : 주어진 데이터셋을 $D$라고 하면, $N$개의 Input과 Output으로 구성됩니다.
  * Loss Function : 머신러닝 모델을 함수 $M$이라고 하면, $M(x)$의 값과 실제 값인 $y$를 평가하기 위한 지표입니다. 
  * Validation Set($D_{val}$) & Test Set($D_{test}$) : 검정 세트와 테스트 세트를 활용하여 구축된 모델의 성능을 평가하며, 만들어진 모델이 기존에 보지 않았던 데이터 샘플을 올바르게 분류할 수 있는지 검정합니다.

* **Decide** 
  * 가설집합(Hypothesis Sets) : 문제를 해결하기 위한 알고리즘을 결정해야 합니다.
  * 최적화 알고리즘(Optimization Algorithm) : 모델의 Loss값을 낮출 수 있는 학습 방법을 결정해야 합니다.
  
앞서 주어지고 결정했던 것들을 정리하여 수식으로 나타내면 다음과 같습니다.

* 훈련 데이터셋 : $D_{train} = \{(x_1, y_1), \cdots, (x_N, y_N)\}$
* 평가 및 테스트셋 : $D_{val}, D_{test}$
* 손실 함수 : $ L(M(x), y) \ge 0 $
* 가설 집합 : $H_1, \cdots, H_M$
* 최적화 알고리즘

모든 조건이 충족되면, 각 가설집합 $H_m$에 최적화 알고리즘을 적용하여 가장 성능이 좋은 모델을 찾습니다. 

1. Model Training : 각 가설(알고리즘)마다, Training Set을 사용하여 성능이 가장 좋은 모델을 찾습니다.
$$ \hat{M}_m = arg\min_{M \in H_m} \sum_{(x, y) \in D} L(M(x), y) $$

2. Model Selection : 검정 세트를 사용하여 훈련된 모델 중 가장 성능이 좋은 모델을 선택합니다.
$$ \hat{M}_m = arg\min_{M \in H_m} \sum_{(x, y) \in D_{val}} L(M(x), y) $$

3. Reporting : 테스트 세트를 사용하여 제일 좋은 모델의 성능을 측정합니다.
$$ R(\hat{M}) \approx \frac{1}{|D_{test}|} \sum_{(x,y) \in D_{test}} L(\hat{M}(x), y)$$


## References
**ML-BASIC**의 모든 포스팅은 뉴욕대 조경현 교수님의 '딥러닝을 이용한 자연어 처리' MOOC 강의를 정리한 것입니다. (https://www.edwith.org/deepnlp/joinLectures/17363)

