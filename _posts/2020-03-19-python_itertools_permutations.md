---
title: Python. itertools.permutations()
date: 2020-03-19
categories:
- Python
tags:
- Python
- itertools
- permutations
---

> itertools.permutations(iterators, r)

{% highlight python %}
from itertools import permutations
{% endhighlight %}

`itertools` 모듈에 속해있는 `permutations` 클래스는 반복 가능한 모든 요소들의 순열을 반환합니다. Parameter를 지정하지 않거나, 입력값이 None이면 기본값은 반복자의 길이가 됩니다.

## Examples
{% highlight python %}

### Input :: Iterator(List), r = None)
print(permutations(['1','2','3']))
# <itertools.permutations object at 0x02A45210>

print(list(permutations(['1','2','3'])))
# [('1', '2', '3'), ('1', '3', '2'), ('2', '1', '3'), ('2', '3', '1'), ('3', '1', '2'), ('3', '2', '1')]

### Input :: Iterator, r = Integer)
print(list(permutations(['1','2','3'], 2)))
# [('1', '2'), ('1', '3'), ('2', '1'), ('2', '3'), ('3', '1'), ('3', '2')]

### Input :: Iterator(String), r = Integer)
print(list(permutations('abc', 3)))
[('a', 'b', 'c'), ('a', 'c', 'b'), ('b', 'a', 'c'), ('b', 'c', 'a'), ('c', 'a', 'b'), ('c', 'b', 'a')]

{% endhighlight %}

## References
1. https://www.hackerrank.com/challenges/itertools-permutations/problem
2. https://docs.python.org/2/library/itertools.html



