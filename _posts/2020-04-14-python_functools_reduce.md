---
title: Python. functools.reduce()
date: 2020-04-14
categories:
- Python
tags:
- Python
- functools
- reduce
---

> functools.reduce(function, iterator, initializer = None)

`functools` 모듈에 속해있는 `reduce`는 iterator의 요소들을 전달받은 함수에 대입하여 하나의 결과를 출력하는 함수입니다. `x`와 `y`를 인자로 받는 함수가 있고, 1차원 리스트 `[a1, a2, a3, a4]`가 있을 때 `reduce` 함수는 다음과 같은 과정을 걸쳐 결과를 반환합니다.

$$ {f} \cdot ({\ f} \cdot ({\ f}(a_1, \; a_2), \; a_3), \; a_4) $$

아래의 실습을 통해 `reduce`가 어떠한 입력을 받아 결과를 출력하는지 확인해보곘습니다.

## 함수 호출
{% highlight python %}
from functools import reduce 
{% endhighlight %}

## 함수 및 변수 정의
{% highlight python %}
def foo(x, y):
    return x * y
    
bar = [1, 2, 3, 4, 5]
{% endhighlight %}

## 결과 확인

{% highlight python %}
print(reduce(foo, bar)) # 120
{% endhighlight %}

`initializer` 인자를 활용하여 초기값을 지정할 수 있습니다.
{% highlight python %}
print(reduce(foo, bar, 100)) # 12000
{% endhighlight %}

## 응용

`lambda` 표현식을 활용하여 코드를 더욱 간결하게 표현할 수 있습니다.

{% highlight python %}
print(reduce(lambda x, y: x + y, bar)) # 15
{% endhighlight %}

`reduce` 함수를 응용하여 최대값을 출력하는 코드를 간결하게 짤 수 있습니다.

{% highlight python %}
print(reduce(lambda x, y: x if x > y else y, bar)) # 5
{% endhighlight %}





