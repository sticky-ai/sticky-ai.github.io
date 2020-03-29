---
title: Python. Iterator
date: 2020-03-29
categories:
- Python
tags:
- Python
- iter
- next
---

파이썬 내장 함수인 `iter`와 `next`는 Iterable한 객체를 다룰 때 사용됩니다. `iter`은 `__iter__` 함수를 호출하고, `next`는 `__next__` 함수를 호출합니다. `iter`는 Iterable한 객체에 대한 Iterator를 반환하고, `next`는 Iterator의 요소를 차례대로 반환합니다.

> iter(iterable or callable [, end]) 

`iter`는 iterable한 객체의 iterator를 반환합니다. 아래의 예제는 `A`라는 리스트와 `iter` 함수를 사용하여 `A`를 iterator로 변환한 `B`를 정의한 후 각 변수의 타입을 확인해보았습니다. `B`의 타입이 list_iterator를 반환하는 것을 확인할 수 있습니다.

{% highlight python %}
A = [1, 2, 3]
B = iter(A)

print(type(A)) # <class 'list'>
print(type(B)) # <class 'list_iterator'>
{% endhighlight %}

`iter` 함수에 반복을 끝내는 `end` 파라미터를 지정해주면 특정 값이 나올 때 반복을 멈출 수 있습니다. 다만, `end` 파라미터가 지정된 경우, 첫 번째 파라미터의 타입은 iterable이 아닌 **callable** 객체여야 합니다.

{% highlight python %}
import random

A = iter([1, 2, 3], 2) # TypeError: iter(v, w): v must be callable
B = iter(lambda : random.randint(0, 5), 3) 
print(B) # <callable_iterator object at 0x110d13dd8>
{% endhighlight %}

> next(iterator)

`next`는 iterator의 요소를 출력합니다. `next`의 파라미터는 iterator 객체여야 합니다. iterator에서 더 이상 반환할 요소가 없을 때에는 `StopIteration` 오류가 발생합니다.

{% highlight python %}
A = [1, 2, 3]
B = iter(A)

print(next(B)) # 1
print(next(B)) # 2
print(next(B)) # 3
print(next(B)) # StopIteration
{% endhighlight %}

## References
1. https://dojang.io/mod/page/view.php?id=2408
2. https://niceman.tistory.com/136
