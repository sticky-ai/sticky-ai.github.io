---
title: Python. itertools.takewhile()
date: 2020-03-15
categories:
- Python
tags:
- Python
- itertools
- takewhile
---

> itertools.takewhile([Predicate, Iterable])

{% highlight python %}
from itertools import takewhile
{% endhighlight %}

`itertools` 모듈에 속해있는 `takewhile` 클래스는 요소를 필터링할 때 유용하게 사용됩니다. 조건과 반복자를 입력받아 조건이 최초로 **False**를 출력하는 시점 이전의 모든 요소들을 출력합니다. `dropwhile` 클래스와 반대의 특성을 가집니다.

## Examples
인자가 짝수인지 판별하는 함수를 정의하고 해당 함수를 첫 번째 인자로, 리스트를 두 번째 인자로 넣어주면 아래와 같은 결과를 출력하게 됩니다.
{% highlight python %}
def example(x):
    return x < 100

print(list(takewhile(is_even, [1, 10, 100, 1000, 10000])))
# [1, 10]
{% endhighlight %}

`lambda` 함수를 활용하여 코드를 조금 더 간결하게 표현할 수 있습니다. 
{% highlight python %}

print(list(takewhile(lambda x: x < 100, [1, 10, 100, 1000, 10000])))
# [1, 10]

`takewhile` 클래스와  `itertools` 모듈에 속해 있는 `count` 클래스를 동시에 사용하여 아래와 같이 응용할 수 있습니다. 

{% highlight python %}
start, stop, step = 1, 100, 12

def floatRange(start, stop, step):
    gen = takewhile(lambda x: x < stop, count(start, step))
    return list(gen)

print(floatRange(start, stop, step))
# [1, 13, 25, 37, 49, 61, 73, 85, 97]
{% endhighlight %}

## References
1. https://docs.python.org/2/library/itertools.html

