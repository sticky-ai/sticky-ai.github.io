---
title: Python. collections.Counter()
date: 2020-03-13
categories:
- Python
tags:
- Python
- Collections
- Counter
---

## collections.Counter([Iterable-or-mapping])
`collection` 모듈에 속해있는 `Counter` 클래스는 주어진 컨테이너에 동일한 값이 몇 개씩 있는지 손쉽게 파악할 수 있도록 도와줍니다. Input으로 데이터를 입력받아 Dictionary 형태로 반환합니다. **Elements**가 Key로 저장되고 **Counts**가 Value로 저장됩니다. 아래의 코드를 통해 불러 올 수 있습니다.
{% highlight python %}
from collections import Counter
{% endhighlight %}



## Examples

### Input :: None
{% highlight python %}
print(Counter())
# Counter()
{% endhighlight %}

### Input :: List 
{% highlight python %}
lst = ['a', 'aa', 'aaa', 'aaaa', 'a', 'aa']
print(Counter(lst))
# Counter({'a': 2, 'aa': 2, 'aaa': 1, 'aaaa': 1})
{% endhighlight %}

### Input :: Dictionary
{% highlight python %}
dict = {'a': 1, 'b': 2, 'c': 3}
print(Counter(dict))
# Counter({'c': 3, 'b': 2, 'a': 1})
{% endhighlight %}

### Input :: String
{% highlight python %}
strs = 'Hello World!'
print(collections.Counter(strs))
# Counter({'l': 3, 'o': 2, 'H': 1, 'e': 1, ' ': 1, 'W': 1, 'r': 1, 'd': 1, '!': 1})
{% endhighlight %}

### Input :: Mapping
{% highlight python %}
mapped = Counter(a = 1, b = 2, c = 3)
print(mapped)
print(list(mapped.elements()))
# Counter({'c': 3, 'b': 2, 'a': 1})
# ['a', 'b', 'b', 'c', 'c', 'c']
{% endhighlight %}

## Methods

### elements()
Counter를 구성하고 있는 Element들을 출력합니다.
{% highlight python %}
mapped = Counter(a = 1, b = 2, c = 3)
print(list(mapped.elements()))
# ['a', 'b', 'b', 'c', 'c', 'c']
{% endhighlight %}

### most_common([n])
많이 등장한 `n`개 Element의 개수를 출력합니다. `n`이 `None`이거나 아무것도 입력하지 않으면 전체 Element의 개수를 출력합니다.
{% highlight python %}
print(Counter('abracadabra').most_common(3))
# [('a', 5), ('b', 2), ('r', 2)]
{% endhighlight %}

### substract([Iterable-or-mapping])
각 `Counter` 오브젝트 간 뺄셈 연산을 진행합니다.
{% highlight python %}
c = Counter(a=4, b=2, c=0, d=-2)
d = Counter(a=1, b=2, c=3, d=4)
c.subtract(d)
print(c)
# Counter({'a': 3, 'b': 0, 'c': -3, 'd': -6})
{% endhighlight %}

### update([Iterable-or-mapping])
`Counter` 오브젝트가 가지고 있는 Element를 갱신합니다.
{% highlight python %}
c = collections.Counter()
print(c)
c.update('Hello World')
print(c)
# Counter()
# Counter({'l': 3, 'o': 2, 'H': 1, 'e': 1, ' ': 1, 'W': 1, 'r': 1, 'd': 1})
{% endhighlight %}

## References
1. https://docs.python.org/3/library/collections.html

