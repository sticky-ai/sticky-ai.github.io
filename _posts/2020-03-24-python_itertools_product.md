---
title: Python. itertools.product()
date: 2020-03-24
categories:
- Python
tags:
- Python
- itertools
- product
---

> itertools.product(*args(iterator), repeat)

{% highlight python %}
from itertools import product
{% endhighlight %}

`itertools` 모듈에 속해있는 `product` 클래스는 주어진 반복자에 대한 **데카르트 곱(Cartesian Product)**을 반환합니다. **데카르트 곱**이란, 두 집합으로부터 각 원소를 하나씩 선택하여 구성한 집합을 의미합니다. 이를 수식으로 나타내면 다음과 같습니다.

$$ A*B = \{(a, b) \ | \ a \in A,  b \in B \} $$

데카르트 곱이 반환하는 결과를 코드로 나타내면 `(x,y) for x in A for y in B`와 같습니다.

## Examples

### Input :: Iterator(List), repeat = Integer
`List` 형태의 반복자만 Parameter로 지정하여 출력한 결과입니다.

{% highlight python %}
print(product([1,2,3],repeat = 2))
# <itertools.product object at 0x110bf4c60>
{% endhighlight %}

`List` 형태의 반복자만 Parameter로 지정하고, 결과를 `List`로 변환하여 출력한 결과입니다. Combination된 각각의 요소들을 확인하기 위해 `List`로 변환하여 출력하였습니다.

{% highlight python %}
print(list(product([1,2,3],repeat = 2)))
# [(1, 1), (1, 2), (1, 3), (2, 1), (2, 2), (2, 3), (3, 1), (3, 2), (3, 3)]
{% endhighlight %}

### Input :: Iterator(List), Iterator(List)
2개의 리스트 반복자를 파라미터로 지정할 수도 있습니다.
{% highlight python %}
print(list(product([1,2,3],[4,5])))
# [(1, 4), (1, 5), (2, 4), (2, 5), (3, 4), (3, 5)]
{% endhighlight %}


### Input :: Iterator(String), Iterator(String)
문자열에도 동일하게 적용 가능합니다.
{% highlight python %}
print(list(product('abc', 'de')))
# [('a', 'd'), ('a', 'e'), ('b', 'd'), ('b', 'e'), ('c', 'd'), ('c', 'e')]
{% endhighlight %}


### Input :: *args(Iterator)
2차원 리스트에도 동일하게 적용할 수 있습니다.
{% highlight python %}
A = [[1,2,3],[4,5]]
print(list(product(*A)))
# [(1, 4), (1, 5), (2, 4), (2, 5), (3, 4), (3, 5)]

B = [[1,2,3],[4,5], [6, 7]]
print(list(product(*B)))
# [(1, 4, 6), (1, 4, 7), (1, 5, 6), (1, 5, 7), (2, 4, 6), (2, 4, 7), (2, 5, 6), (2, 5, 7), (3, 4, 6), (3, 4, 7), (3, 5, 6), (3, 5, 7)]
{% endhighlight %}

## References
1. https://www.hackerrank.com/challenges/itertools-product/problem
