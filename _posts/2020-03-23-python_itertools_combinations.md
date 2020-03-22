---
title: Python. itertools.combinations()
date: 2020-03-23
categories:
- Python
tags:
- Python
- itertools
- combinations
---

> itertools.permutations(iterators, r)

{% highlight python %}
from itertools import combinations
{% endhighlight %}

`itertools` 모듈에 속해있는 `combinations` 클래스는 반복 가능한 모든 요소들의 조합을 반환합니다.

## Examples

### Input :: Iterator(List), r = Integer)
`List` 형태의 반복자만 Parameter로 지정하여 출력한 결과입니다.
{% highlight python %}
print(combinations(['1','2','3'], 2))
# <itertools.combinations object at 0x110c4fe08>
{% endhighlight %}

`List` 형태의 반복자만 Parameter로 지정하고, 결과를 `List`로 변환하여 출력한 결과입니다.
Combination된 각각의 요소들을 확인하기 위해 `List`로 변환하여 출력하였습니다.
{% highlight python %}
print(list(combinations(['1','2','3'], 2)))
# [('1', '2'), ('1', '3'), ('2', '3')]
{% endhighlight %}

### Input :: Iterator(String), r = Integer)
`String` 형태의 반복자와 순열의 길이 `r`을 지정하여 출력한 결과입니다.
{% highlight python %}
print(list(combinations('abcd', 2)))
# [('a', 'b'), ('a', 'c'), ('a', 'd'), ('b', 'c'), ('b', 'd'), ('c', 'd')]
{% endhighlight %}

`sorted` 함수를 사용하여 출력 결과를 정렬할 수 있습니다.
{% highlight python %}
print(list(combinations(sorted('dcab'), 2)))
# [('a', 'b'), ('a', 'c'), ('a', 'd'), ('b', 'c'), ('b', 'd'), ('c', 'd')]
{% endhighlight %}


## References
1. https://www.hackerrank.com/challenges/itertools-combinations/problem
