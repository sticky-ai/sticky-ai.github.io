---
title: Python. itertools.accumulate()
date: 2020-03-26
categories:
- Python
tags:
- Python
- itertools
- accumulate
---

> itertools.permutations(iterable: Iterable[, func)

{% highlight python %}
from itertools import accumulate()
{% endhighlight %}

`itertools` 모듈에 속해있는 `accumulate` 클래스는 주어진 반복자에 대한 **축적 합**을 반환합니다. **축적 합**이란, 주어진 오브젝트에 대해 각 인덱스 이전의 값들을 모두 더한 값을 의미합니다. 만약 `[1, 2, 3]`의 리스트가 입력되었다면, 이를 accumulate한 결과값은 `[1, 3, 6]`입니다. 이를 풀어서 표현하면 `[1, 1 + 2, 1 + 2 + 3]`과 같습니다.

## Examples

`List` 형태의 반복자를 지정하였습니다. 정상적으로 accumulate된 결과를 확인할 수 있습니다.
{% highlight python %}
A = [1, 2, 3, 4]
print(list(accumulate(A)))
# [1, 3, 6, 10]
{% endhighlight %}

문자열에도 동일하게 적용 가능합니다.
{% highlight python %}
B = 'abcd'
print(list(accumulate(B)))
# ['a', 'ab', 'abc', 'abcd']
{% endhighlight %}

