---
title: ML4NLP. PART 1. Text Classification & Sentence Representation 2 
date: 2020-02-19
categories:
- Natural Language Processing
tags:
- ML4NLP
- Word2Vec
- CBoW
- Continuous bag-of-words
- Relation Network
- Skip Gram
- CNN
- Convolutional Neural Network
---

앞선 포스팅 [ML4NLP. Part 1. Text Classification & Sentence Representation][ml4nlp_part1_1]에서 Text Classification을 진행하기 위한 사전 작업에 대해 살펴보았습니다. 원-핫 인코딩 방식이 단어간의 의미를 전혀 표현할 수 없다는 한계점을 해결하기 위해 Word Embedding 방법을 사용했었습니다. Word Embedding 방법은 문장을 수치화 하는 데 성공했지만, 단어간 유사도를 나타내기에는 적절하지 않다는 한계점이 드러났습니다. 따라서, 이번 포스팅에서는 문장의 의미를 파악하기 위한 여러가지 방법 중 Word2Vec 모델과 CNN 모델을 살펴보겠습니다.

## Word2Vec - CBoW(Continuous Bag-of-Words)
**CBoW**의 기본 아이디어는 여러 개의 단어로부터 이와 관련된 단어를 추정하는 것입니다. 예를 들어, 'The fat cat sat on the mat' 라는 문장이 있을 때, 이 문장은 {'The', 'cat', 'sat', 'on', 'the', 'mat'}와 같이 토큰화 할 수 있습니다. 만약, 'sat'이 예측해야 하는 단어라면 'football'을 **중심 단어(Center Word)** 라 하며, 예측에 사용되는 주변 단어들을 **주변 단어(Context Word)** 라 합니다.

중심 단어를 예측하기 위해 중심 단어 주변에 분포하는 주변 단어들을 살펴보아야 하는데, 몇 개의 주변 단어를 볼지 결정하는 것이 윈도우(Window)입니다. 윈도우의 크기가 $n$이라면, 중심 단어를 예측하기 위해 사용하는 주변 단어의 개수는 $2n$이 됩니다. 이러한 개념은 아래의 그림을 통해 쉽게 이해할 수 있습니다.

![IMAGE]({{ "assets/resources/2020-02-19-ml4nlp_text_classification_sentence_representation_2/cbow_example.jpg" | absolute_url }}){: width="70%" height="70%"}

위의 그림처럼, 예측하고자 하는 중심 단어를 바꾸어가면서 학습을 위한 데이터셋을 구축합니다. 위 그림을 통해윈도우가 움직이면서 CBoW 학습을 위한 데이터셋이 어떻게 구축되어지는지 확인할 수 있습니다. CBoW는 아래 그림과 같은 신경망 구조를 가집니다. Input Layer에는 중심 단어와 중심 단어 주변에 분포하는 주변 단어들의 원-핫 벡터가 들어가게 됩니다. 은닉층은 하나의 층으로 구성되어 있으며, 은닉층을 투사하는 가중치 행렬은 모든 단어에 공통적으로 적용합니다. 이는 일반적인 은닉층과는 달리 활성화 함수가 존재하지 않으며, 이전 포스팅에서 언급했던 바와 같이 Look-up Table 연산만을 진행합니다. 

![IMAGE]({{ "assets/resources/2020-02-19-ml4nlp_text_classification_sentence_representation_2/cbow_neural_nets.jpg" | absolute_url }}){: width="70%" height="70%"}

위 그림에서 $x$는 원-핫 인코딩 된 단어 벡터이며, $W$는 가중치, $M$은 임베딩 이후의 벡터의 차원, $V$는 단어 집합의 크기를 의미합니다. 입력층과 은닉층 사이의 가중치 행렬은 $W_{V*N}$이며, 모든 단어에 대해 동일하게 적용됩니다. 은닉층와 출력층 사이의 가중치 $W'_{N * V}$는 마치 입력층과 은닉층 사이의 가중치 행렬을 전치(Transpose)시킨 것 처럼 보이지만, 다른 행렬이라는 점을 유의해야 합니다. $W$와 $W'$의 가중치는 최초 아주 작은 랜덤값으로 세팅되어 있으며, 학습을 진행하면서 가중치를 조정해 나갑니다. 아래의 그림은 입력층과 은닉층 사이의 가중치 행렬 연산이 어떻게 일어나는지 확인할 수 있습니다.

![IMAGE]({{ "assets/resources/2020-02-19-ml4nlp_text_classification_sentence_representation_2/cbow_neural_nets_calculation_1.jpg" | absolute_url }}){: width="70%" height="70%"}

중심 단어가 'sat'이고, 윈도우의 크기가 1일 때, Input Layer에는 주변 단어 'cat'과 'on'이 원-핫 벡터의 형태로 들어오게 됩니다. 앞서 언급한대로, Input Layer와 Hidden Layer의 가중치 연산은 입력 벡터가 값이 1인  $i$번째 인덱스를 확인하여, $W$ 행렬의 $i$번 째 행을 그대로 읽어옵니다. 이러한 연산을 Table Look-up이라고 합니다. Table Look-up이 끝난 벡터들은 가중치 연산을 통해 Hidden Layer의 각 노드로 위치하게 됩니다.

![IMAGE]({{ "assets/resources/2020-02-19-ml4nlp_text_classification_sentence_representation_2/cbow_neural_nets_calculation_2.jpg" | absolute_url }}){: width="70%" height="70%"}

Hidden node들, 즉 가중치 연산을 마친 벡터들을 평균 내어 평균 벡터를 산출합니다. 윈도우의 크기가 1이면, 입력 벡터의 총 개수는 n이므로 중간 단어를 예측하기 위해서는 총 2개가 입력 벡터로 사용됩니다. 그렇기 떄문에, 평균을 구할 때에는 2개의 결과 벡터에 대한 평균을 산출합니다. 위의 그림은 윈도우의 크기가 2일 때의 연산 과정을 도식화 한 것입니다.

$$ v = \frac{V_{cat} + V_{on}}{2 * window\ size} $$

![IMAGE]({{ "assets/resources/2020-02-19-ml4nlp_text_classification_sentence_representation_2/cbow_neural_nets_calculation_3.jpg" | absolute_url }}){: width="70%" height="70%"}

최종적으로, 소프트맥스 함수를 취하여 예측 단어에 대한 Distribution을 출력합니다. 이러한 과정을 간단하게 정리하면 아래와 같습니다.

1. 원-핫 인코딩 된 벡터를 입력 변수로 구성
2. 가중치 연산을 통해 Table Look-up 수행
3. 연산된 벡터들의 평균값을 산출
4. Arbitrary Sub-graph를 통해 학습
5. Softmax 함수를 사용하여 예측값에 대한 Distribution 출력

![IMAGE]({{ "assets/resources/2020-02-19-ml4nlp_text_classification_sentence_representation_2/cbow_dag_final.jpg" | absolute_url }}){: width="70%" height="70%"}

## Word2Vec - RN(Relation Network)
**RN**은 Skip-gram이라고 표현하기도 하며, CBoW와 메커니즘이 거의 유사합니다. 다만, RN은 문장안에 존재하는 모든 토큰의 쌍을 보고, 각 쌍에 대한 신경망을 구축하는 것이 주요 아이디어입니다. CBoW가 Input Vector로 중심 단어를 제외한 주변 단어들을 사용하였다면, RN은 중심 단어만을 Input Vector로 활용합니다. 이를 도식화하면 아래의 그림과 같습니다.

![IMAGE]({{ "assets/resources/2020-02-19-ml4nlp_text_classification_sentence_representation_2/rn_neural_nets.jpg" | absolute_url }}){: width="70%" height="70%"}

RN의 세부 프로세스는 다음과 같습니다. 먼저, 문장에서 가능한 토큰들의 쌍$(x_i, x_j)$을 모두 추출합니다. 추출된 쌍을 기반으로 학습을 순차적으로 진행합니다. 만약, 중심 단어로 'sat'를 선정했다면, 'on'을 주변 단어 정답으로 두고 학습을 진행합니다. 이후에는 'on'을 중심 단어로, 'sat'를 주변 단어로 설정하여 학습을 진행합니다. 

![IMAGE]({{ "assets/resources/2020-02-19-ml4nlp_text_classification_sentence_representation_2/rn_dag_final.jpg" | absolute_url }}){: width="70%" height="70%"}

존재하는 모든 토큰 쌍에 대해 Relation Network Sub-graph를 계산합니다. Relation Network는 하나의 벡터를 반환하며, 산출된 모든 벡터들의 평균값을 산출하고, 산출된 값을 다시 한 번 Arbitrary Sub Graph를 통해 연산을 진행하고, 결과적으로 Softmax 함수를 통해 가능한 모든 쌍에 대한 Distribution을 출력합니다.

$$ f(x_i, x_j) = W\phi(U_{left}e_i + U_{right}e_j) \\RN(X) = \frac{1}{2N(N-1)} \sum_{i=1}^{T-1} \sum_{j=i+1}^{T} f(x_i, x_j) $$

Skip-Gram은 CBoW에 비해 중심 단어를 업데이트 할 수 있는 기회가 더 많기 때문에 상대적으로 성능이 좋게 나타납니다. 따라서, 최근에는 대부분의 Text Classification 및 Sentence Representation 문제에서 CBoW에 비해 Skip-Gram을 더 많이 사용하는 추세입니다.

## References
1. **Machine Learning for Natural Language Proceesing**의 모든 포스팅은 뉴욕대 조경현 교수님의 '딥러닝을 이용한 자연어 처리' MOOC 강의를 정리한 것입니다. (https://www.edwith.org/deepnlp/joinLectures/17363)

2. CBoW 개념 이해를 위해 '딥러닝을 이용한 자연어 처리 입문' 문헌을 참고 및 정리하였습니다. (https://wikidocs.net/22660)

3. Skip-Gram 개념 이해를 위해 'Word2Vec Tutorial - The Skip-Gram Model' 사이트를 참고 및 정리하였습니다. (http://mccormickml.com/2016/04/19/word2vec-tutorial-the-skip-gram-model/)

[ml4nlp_part1_1]: {{ site.baseurl }}{% link _posts/2020-02-18-ml4nlp_text_classification_sentence_representation_1.md %}