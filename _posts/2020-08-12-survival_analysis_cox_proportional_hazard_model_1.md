---
title: Survival Analysis. Cox 비례 위험 모형(Cox Proportional Hazard Model) - 1
date: 2020-08-12
categories:
- Survival Analysis
tags:
- Survival Analysis
- Cox Proportional Hazard Model
- Survival Function
- Hazard Function
- Hazard Ratio
---

앞선 `Kaplan-Meier`와 `Log-Rank Test` 방법은 생존율을 추정하는 가장 단순한 방법입니다. **시간(Time)**과 **사건(Event)**만을 고려하여 생존율을 추정하기 때문입니다. 이러한 측면에서 앞선 두 방법은 데이터의 특성을 전혀 반영하지 못하는 **Non-Parametric**한 분석 방법이라고 합니다. 이와 반대로, **Parametric** 방법은 생존 시간 분포(예를 들어 정규분포)가 존재한다고 가정하고 회귀 모델로 생존 기간을 예측하는 방법입니다. 대표적으로 `Linear Regression`이 있으며, 그 외에도 `Accelerated Failure Time Model`이 존재합니다.

앞으로의 포스팅에서 다루게 될 `Cox Proportional Hazard Model (이하 Cox 모형)`은 모델이 데이터의 특성은 반영하지만, 생존 시간 분포를 반영하지 않습니다. 다시 말하면, 생존 시간에 대한 특정한 가정이 필요 없다는 점에서 비모수적인 특징을 가지고 있으나, 공변량이 주어졌을 때 특정한 식으로 데이터의 특징을 표현할 수 있기에 모수적인 특징도 가지고 있습니다. 이러한 관점에서 `Cox 모형`은 **Semi-Parametric**한 생존 분석 방법이라고 할 수 있습니다.

## Cox Proportional Hazard Model의 개념
`Cox 모형`은 시간(Time) - 사건(Event) 데이터를 기반으로 예측 모형을 만드는 통계분석 혹은 생존분석 방법 중 하나입니다. Cox 모형은 Parametric 분석 방법인 회귀분석을 활용하여 **중도절단자료(Censored Data)**의 처리가 가능하며, 앞서 언급한 Kaplan-Meier 방법과 달리 사건 발생에 영향을 줄 수 있는 변수들의 특징을 반영한 모델을 구축할 수 있습니다. 

Cox 모형은 생존함수가 `지수함수(Exponential Function)`을 따른다는 것과 두 군의 위험비가 연구기간동안 일정하게 유지된다는 **비례위험가정**, 이 두 가지 가정이 요구됩니다. 특정 시점에서의 생존함수는 위험비에 대한 지수함수로 표현될 수 있어야 하며, `위험비`는 연구기간 내 일정하게 유지되어야 합니다. 

Cox 모형을 제대로 이해하기 위해서는 위험비를 포함한 여러 개념들에 대한 선행적 이해가 필요합니다. 이번 포스팅에서는 Cox 모형의 가정을 이해하기 위한 선행 개념들에 대해 설명드리겠습니다.

## 생존함수(Survival Function)
Cox 모형의 2가지 가정 중 하나에 해당하는 비례위험가정은 위험비가 일정하게 유지되어야 한다는 것을 의미합니다. 그렇다는 위험비는 무엇일까요? `위험비`는 집단 A와 집단 B의 위험함수의 비율입니다. 위험비를 이해하기 위해서는 먼저 `생존함수`와 `위험함수`에 대한 개념이 선행되어야 합니다. 

먼저, **생존함수**는 측정 시점부터 특정 시점까지 사건이 발생하지 않을 확률을 함수로 나타낸 것입니다. 즉, 관찰대상이 특정시간보다 오래 생존할 확률을 함수로 나타낸 것입니다. 생존함수는 일반적으로 $S(t)$로 표현합니다. 

$$ S(t) = P(T > t) $$

$P$는 확률(Probability), $t$는 시간, $T$는 사건이 발생하는 시간입니다. 시작 시점$(t = 0)$에는 어떠한 사건도 발생하지 않았기 때문에 생존함수는 1을 반환합니다. 관찰대상은 시간이 지남에 따라 사건이 발생하기 때문에 생존함수는 점차 감소하는 형태를 띄게됩니다. 만약, 관찰기간을 특정 시점으로 통제하지 않고 무한대로 늘리게 된다면 결국 생존함수는 0을 반환할 것입니다. 

생존함수를 통해 `생애분포함수(Lifetime Distribution Function)`를 산출할 수 있습니다. 생애분포함수는 생존함수의 정반대 개념이며, 관찰 대상의 사건이 특정 시간 안에 발생할 확률을 나타내며, $F(t)$로 표현됩니다. 

$$ F(t) = P(T \le t) = l - S(t) \\ f(t) = F\prime(t) = \frac{d}{dt}F(t)$$

생애분포함수를 미분하면 특정 시간에서의 사건발생률을 의미하는 `생존밀도함수(Survival Event Density Function)`을 구할 수 있습니다. 생존밀도함수는 $f(t)$로 나타냅니다. 

$$ S(t) = P(T > t) = \int_t^{\infty} f(u)du = 1 - F(t)$$ 

결국 생존함수는 시간 $t$ 이후에 사건이 발생할 확률을 적분(모두 더한 것)한 것입니다.

## 위험함수(Survival Function)
생존함수와 반대되는 개념인 **위험함수**는 임의의 시점에서의 사건이 발생할 확률을 함수로 나타낸 것으로 $h(t)$로 표현합니다. 다시 말하면, 위험함수는 특정 시간까지 사건이 발생하지 않은 케이스에 대해 사건이 발생할 확률(조건부 확률)을 나타냅니다. 위험함수 $h(t)$는 $\frac{f(t)}{S(t)}$로 산출할 수 있습니다. 여기서 $f(t)$는 특정시점 $t$에서 사건이 발생할 확률을 나타냅니다. 

$$ h(t) = \lim_{dt \rightarrow 0} \frac{P(t \le T < t + dt)}{dt \cdot S(t)} = \frac{f(t)}{S(t)} = -\frac{S\prime(t)}{S(t)} = -\frac{d}{dt}\log{S(t)} $$

위험함수는 시간 $t$에 사건이 발생할 확률을 시간 $t$보다 더 오래 생존한 확률로 나눈 결과로, 생존함수에 로그를 적용하여 미분한 것과 같습니다. 따라서, 위험함수가 반환하는 값은 항상 양수이며, 시간이 갈수록 늘어나거나 줄어들 수도 있습니다.

위험함수를 0부터 시간 $t$까지 적분하면 `누적위험함수(Cumulative Hazard Function)`를 얻을 수 있습니다. 누적위험함수는 시간 $t$까지 사건이 발생할 확률을 모두 더한 것입니다.

$$ H(t) = \int_0^t h(u)du = -\log{S(t)} \\ $$ 

## 위험함수(Survival Function)와 생존함수(Survival Function)의 관계

앞선 개념들을 통해 위험함수와 생존함수에 대해 알아보았습니다. 결과적으로 위험함수와 생존함수는 서로 관계를 가지는 것을 확인할 수 있었습니다.

$$ S(t) = \exp[-H(t)] = 1 - F(t), t > 0 $$

## 위험비(Hazard Ratio, HR)와 비례위험가정(Proportional Hazards Assumption)
앞서 Cox 모형은 비례위험가정이 수반되어야 모형을 구축할 수 있다고 설명했습니다. 그렇다면 위험비가 일정하게 유지되어야 한다는 것은 어떠한 의미일까요? 이에 대한 예시를 들어보겠습니다. 대장암 환자에 대한 수술방법 A와 새롭게 개발된 수술방법 B에 대한 생존분석을 진행한다고 가정하고, 수술방법 A에 비해 수술방법 B의 생존율이 1.5배 정도 높다면, 모든 시점에서 항상 1.5배여야 한다는 것이며, 이를 `비례위험가정`이라고 합니다. 
`위험비`는 각 집단의 위험함수 비를 통해 산출되며, 수식으로는 아래와 같습니다. $h_1(t)$와 $h_2(t)$는 집단 A와 집단 B에 대한 위험 함수이며, $t$는 시간을 나타냅니다. 

$$ HR = \frac{h_{2}(t)}{h_{1}(t)} $$ 


## References
1. Survival analysis: Part I — analysis of time-to-event, Junyong In et al., Korean Journal of Anesthesiology, 2018
2. Survival Analysis - 3, [Internet] https://3months.tistory.com/349
3. 생존분석 - 생존분석의 목적과 생존함수, 위험함수의 정의, [Internet] https://hyperconnect.github.io/2019/10/03/survival-analysis-part3.html
