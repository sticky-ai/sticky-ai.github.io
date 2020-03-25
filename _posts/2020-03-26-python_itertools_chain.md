---
title: Python. itertools.chain()
date: 2020-03-26
categories:
- Python
tags:
- Python
- itertools
- chain
---

> itertools.chain(*iterables)

{% highlight python %}
from itertools import chain
{% endhighlight %}

`itertools` 모듈에 속해있는 `chain` 클래스는 주어진 N차원 오브젝트를 연결한 결과를 N차원으로 반환합니다. 이와 비슷한 결과를 내는 방법으로 `itertools.chain.from_iterable()` 함수,  `sum()` 함수가 있고, `numpy` 모듈에 속해 있는 `flatten()`과 `reshape()`이 동일한 결과를 나타낼 수 있습니다. 다만, `reshape()`과 `flatten()`이 `itertools`가 제공하는 함수들에 비해 약 100배 가량 연산 속도가 빠릅니다.

## Examples
1차원 리스트 `A`와 `B`를 정의하고 `chain()` 함수로 연결시켰습니다. 1차원 + 1차원의 결과로 1차원 리스트를 반환하는 것을 확인할 수 있습니다.
{% highlight python %}
A = [1, 2, 3]
B = [4, 5, 6]
print(list(chain(A, B)))
# [1, 2, 3, 4, 5, 6]
{% endhighlight %}

2차원 리스트 `C`와 `D`를 정의하고 연결시켰습니다. 결과적으로 2차원 리스트를 반환하는 것을 확인할 수 있었습니다.
{% highlight python %}
C = [[1, 2], [3, 4], [5, 6]]
D = [[7, 8], [9, 10], [11, 12]]
print(list(chain(C)))
# [[1, 2], [3, 4], [5, 6], [7, 8], [9, 10], [11, 12]]
{% endhighlight %}

1차원 리스트 `A`와 2차원 리스트 `C`를 연결시켜보았습니다. 2차원 리스트를 반환하나, 1차원 리스트에 있던 요소들은 하나의 인덱스를 차지한 것을 확인할 수 있었습니다.
{% highlight python %}
A = [1, 2, 3]
C = [[1, 2], [3, 4], [5, 6]]
print(list(chain(A, C)))
# [1, 2, 3, [1, 2], [3, 4], [5, 6]]
{% endhighlight %}