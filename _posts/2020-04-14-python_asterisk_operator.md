---
title: Python. Asterisk(*) Operator
date: 2020-04-14
categories:
- Python
tags:
- Python
- Asterisk
---

Python은 타 언어에 비해 다양한 연산을 지원합니다. 그 중에서도 `Asterisk(*) Operator`는 단순 연산을 포함한 여러 기능을 포함하고 있습니다. 

* 곱셈 및 거듭제곱 연산
* 컨테이너형 데이터 확장
* 가변인자(Variadic Parameters) 사용
* 컨테이너형 데이터 언패킹(Unpacking) 

각 항목에 대한 예제를 통해 어떻게 `Asterisk(*)`가 활용되는지 확인해보겠습니다. 

## 곱셈 및 거듭제곱 연산
Python에서는 `Asterisk(*)`를 활용한 다양한 연산자를 내장하고 있습니다. 기본적인 곱셈 연산과 거듭제곱 연산 또한 가능합니다.

{% highlight python %}
print(2 * 3) # 6
print(2 ** 3) # 8
{% endhighlight %}

## 컨테이너형 데이터 확장

`Asterisk(*)`를 활용하여 **컨테이너형 데이터**를 손쉽게 확장할 수 있습니다. 여기서 **컨테이너형 데이터**란, `__contains__` 객체를 상속받는 데이터 타입을 의미합니다. 대표적으로 `str`, `dict`, `list`, `tuple`, `dict`가 컨테이너형 데이터에 속합니다. 

`dir` 함수를 활용하여 각 데이터 타입이 진짜 컨테이너 객체를 상속받고 있는지 확인해보겠습니다. 

{% highlight python %}
print(dir(int)[:5]) # ['__abs__', '__add__', '__and__', '__bool__', '__ceil__']
print(dir(str)[:5]) # ['__add__', '__class__', '__contains__', '__delattr__', '__dir__']
print(dir(dict)[:5]) # ['__class__', '__contains__', '__delattr__', '__delitem__', '__dir__']
print(dir(list)[:5]) # ['__add__', '__class__', '__contains__', '__delattr__', '__dir__']
print(dir(tuple)[:5]) # ['__add__', '__class__', '__contains__', '__delattr__', '__dir__']
{% endhighlight %}

`int` 자료형을 제외한 나머지 자료형은 모두 `__contains__` 객체를 상속받고 있는 것을 확인할 수 있었습니다. 따라서, `int`를 제외한 나머지 자료형은 `Asterisk(*)`를 활용하여 데이터 확장이 가능합니다. 

{% highlight python %}
a = [0] * 10
print(a) # [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]

b = [1, 2] * 5
print(b) # [1, 2, 1, 2, 1, 2, 1, 2, 1, 2]

c = [[1, 2]] * 5
print(c) # [[1, 2], [1, 2], [1, 2], [1, 2], [1, 2]]

e = (1, 2) * 5
print(d) # (1, 2, 1, 2, 1, 2, 1, 2, 1, 2)
{% endhighlight %}

## 가변인자(Variadic Paramter) 사용

**가변인자(Variadic Parameter)**란, 넘어오는 인자(argument)의 수를 모르거나 어떠한 형태의 자료형이 넘어오더라도 처리할 수 있는 인자를 의미합니다. Python에서는 크게 **Positional Arguments**와 **Keyword Arguments**로 구분됩니다. Positional Arguments는 인자의 위치와 이름이 정해져 있지 않으며, Keyword Arguments는 인자의 위치와 이름이 정해져 있습니다. 관례적으로, Positional Arguments는  `*args`로, Keyword Arguments는 인자의  `*kwargs`로 표기합니다. 

만약, 5명의 학생 이름을 전달받아 출력하는 함수는 아래와 같이 정의할 수 있습니다.
{% highlight python %}
def get_names(first, second, third, fourth, fifth):
    print(first, second, third, fourth, fifth)

get_names('Kim', 'Lee', 'Park', 'Choi', 'Jeong') # Kim Lee Park Choi Jeong
{% endhighlight %}

하지만, 학생의 수가 10명, 20명이 넘는 경우에는 하나 하나 정의하기가 번거로우며, 학생의 수를 모르는 경우에는 처리할 수 없습니다. 이러한 상황에서 적용할 수 있는 것이 가변인자입니다.
{% highlight python %}
def get_names(*args, **kwargs):
    print(args)
    print(kwargs)
    
get_names('Park', 'Lee', 'Choi', first = 'Kim', second = 'Jeong') # ('Park', 'Lee', 'Choi') {'first': 'Kim', 'second': 'Jeong'}
{% endhighlight %}

## 컨테이너형 데이터 언패킹(Unpacking)
어떠한 함수가 가변 인자를 요구하는 경우, `Asterisk(*)`를 데이터 언패킹에 활용할 수 있습니다. **언패킹(Unpacking)**이란, 패킹(Packing)의 반대되는 개념으로, 여러 값을 가지고 있는 컨테이너형 데이터에서 값을 꺼내 분리하는 작업을 의미합니다. 아래의 예제를 통해 Packing과 Unpacking을 이해할 수 있습니다.

{% highlight python %}
'''Packing'''
a = 'a', 'b', 'c'
print(a) # ['a', 'b', 'c']

'''Unpacking'''
print(*a) # a b c

foo, bar, dgs = a
print(foo, bar, dgs) # a b c
{% endhighlight %}

다음 예제에서는 가변 인자를 요구하는 함수 `product`에 `Asterisk(*)`를 활용해보곘습니다. `product` 함수는 데카르드 곱을 반환하는 함수로, 가변인자를 받아 결과를 출력합니다. 2차원 리스트 `c`에 포함된 1차원 리스트 `[1, 2, 3]`과 `[4, 5, 6]`을 언패킹하여 값을 전달합니다. 
{% highlight python %}
from itertools import product

c = [[1, 2, 3], [4, 5, 6]]
print(list(product(*c))) # [(1, 4), (1, 5), (1, 6), (2, 4), (2, 5), (2, 6), (3, 4), (3, 5), (3, 6)]
{% endhighlight %}

## References 
1. https://mingrammer.com/understanding-the-asterisk-of-python/
2. https://dpdpwl.tistory.com/88

