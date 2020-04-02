---
title: Python. Generator
date: 2020-04-03
categories:
- Python
tags:
- Python
- Generator
---

**Generator**는 Iterator를 반환하는 함수이며, `yield` 키워드를 사용하여 생성할 수 있습니다. 함수 내에서 `yield`를 사용하면 함수는 제너레이터를 반환합니다. 

{% highlight python %}
def generator(): # 제너레이터 생성
    yield 1
    yield 2
    yield 3

g = generator()

print(g) # <generator object generator at 0x110bcbca8>
{% endhighlight %}

Generator의 함수 목록을 확인해보면, Iterator에서 볼 수 있는 `__iter__`와 `__next__` 함수가 포함되어 있는 것을 확인할 수 있습니다. `__next__` 함수가 포함되어 있기 때문에 `next()` 함수를 사용하여 제너레이터의 각 요소에 접근할 수 있습니다.

{% highlight python %}
print(g) # ['__class__', '__del__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__lt__', '__name__', '__ne__', '__new__', '__next__', '__qualname__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'close',
 'gi_code', 'gi_frame', 'gi_running', 'gi_yieldfrom', 'send', 'throw']
 
print(next(g)) # 1
print(next(g)) # 2
print(next(g)) # 3
{% endhighlight %}

`for` 반복문을 활용하여 Generator의 요소에 접근할 수 있습니다. 
{% highlight python %}
for i in generator():
    print(i) 
# 1
# 2
# 3
{% endhighlight %}

Iterator와는 달리, Generator에 더 이상 출력할 요소가 없으면 `StopIteration` 에러가 자동적으로 발생합니다. 

{% highlight python %}
print(next(g)) # 1
print(next(g)) # 2
print(next(g)) # 3
print(next(g)) # StopIteration:
{% endhighlight %}

## References
1. https://dojang.io/mod/page/view.php?id=2412





