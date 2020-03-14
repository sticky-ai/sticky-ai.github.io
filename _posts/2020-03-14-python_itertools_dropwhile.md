---
title: Python. itertools.dropwhile()
date: 2020-03-14
categories:
- Python
tags:
- Python
- itertools
- dropwhile
---

> itertools.dropwhile([Predicate, Iterable])

{% highlight python %}
from itertools import dropwhile
{% endhighlight %}

`itertools` 모듈에 속해있는 `dropwhile` 클래스는 요소를 필터링할 때 유용하게 사용됩니다. 조건과 반복자를 입력받아 조건이 최초로 **False**를 반환하는 시점에 해당하는 요소들을 반환합니다.

## Examples
인자가 짝수인지 판별하는 함수를 정의하고 해당 함수를 첫 번째 인자로, 리스트를 두 번째 인자로 넣어주면 아래와 같은 결과를 출력하게 됩니다.
{% highlight python %}
def is_even(x): # x가 짝수인지 판별
    return x % 2 != 0

print(list(dropwhile(is_even, [1, 10, 100, 1000, 10000])))
# [10, 100, 1000, 10000]
{% endhighlight %}

`lambda` 함수를 활용하여 코드를 조금 더 간결하게 표현할 수 있습니다. 
{% highlight python %}

print(list(dropwhile(lambda x: x < 100, [1, 10, 100, 1000, 10000])))
# [100, 1000, 10000]

print(list(dropwhile(lambda x: len(x) < 5, ['a', 'aaa', 'aaaaa', 'aaaaaaa'])))
# ['aaaaa', 'aaaaaaa']
{% endhighlight %}

`dropwhile` 클래스를 아래와 같이 응용할 수 있습니다. 아래의 예시는 이름의 길이에 대한 조건문과 이름으로 구성된 리스트를 입력으로 받아 결과를 최대 3개까지 출력하도록 하는 예시입니다.

{% highlight python %}
names = ['James', 'May', 'Salen', 'Paul', 'Tom']
gen = dropwhile(lambda s: len(s) == 5, names)
print([next(gen) for _ in range(3)])
# ['May', 'Salen', 'Paul']
{% endhighlight %}

## References
1. https://docs.python.org/2/library/itertools.html