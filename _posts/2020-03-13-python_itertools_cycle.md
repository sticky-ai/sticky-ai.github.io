---
title: Python. itertools.cycle()
date: 2020-03-13
categories:
- Python
tags:
- Python
- itertools
- cycle
---

> itertools.cycle([Iterable])

{% highlight python %}
from itertools import cycle
{% endhighlight %}

`itertools` 모듈에 속해있는 `cycle` 클래스는 Iterable한 오브젝트를 입력받아 요소를 반복적으로 생성합니다.

## Examples

`cycle` 객체를 출력하면 아래와 같은 결과가 나오게 됩니다. 생성된 `cycle` 객체인 `c`에 대한 인덱스 슬라이싱 접근은 오류를 발생시킵니다.
{% highlight python %}
c = cycle('Hello')) 
print(c) # <itertools.cycle object at 0x110bfbf30>
print(c[0]) # TypeError: 'itertools.cycle' object is not subscriptable
{% endhighlight %}

`cycle` 객체가 가지고 있는 요소를 출력해보겠습니다. 위에서 정의한 'Hello'라는 문자열이 순서대로, 반복적으로 출력되는 것을 확인할 수 있습니다.
{% highlight python %}
count = 0
for i in c:
    print(i)
    count += 1
    if count == 8:
        break
# H
# e
# l
# l
# o
# H
# e
# l
{% endhighlight %}

`next()` 함수를 사용하여 `cycle` 객체가 가지고 있는 원소들을 표현할 수 있습니다. `next()` 함수는 반복자를 입력받아 그 반복자가 다음에 출력해야 할 요소를 반환합니다. 

{% highlight python %}
c_lst = [next(c) for _ in range(n)]
# ['e', 'l', 'l', 'o', 'H', 'e', 'l', 'l']
{% endhighlight %}

## References
1. https://docs.python.org/2/library/itertools.html

