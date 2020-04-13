---
title: Python. Lambda Expression
date: 2020-04-12
categories:
- Python
tags:
- Python
- Lambda
---

**Lambda Expression**는 코드가 식의 형태를 띄고 있어 '람다 표현식(이하 람다)'으로 표현되며, 익명 함수를 만들 때 사용됩니다. **익명 함수**란, 함수 선언 시 함수명을 정의해야 하는 기존 함수와는 달리, 함수명 없이도 정의할 수 있는 함수를 의미합니다. 기존의 함수는 함수가 정의되는 순간 메모리에 올라가 호출되기를 기다립니다. 반면, 람다는 실행 이후 메모리 영역에서 제거됩니다. 따라서, 한 번만 사용될 함수라면 람다로 정의하는 것이 좋습니다.

일반적인 함수는 아래와 같이 정의하고 호출합니다.

{% highlight python %}
def sum(x, y): 
    return x + y
  
print(sum(1, 2)) # 3
{% endhighlight %}

람다를 사용하면 코드를 더욱 간결하게 표현할 수 있습니다.

{% highlight python %}
l = lambda x, y: x+y
print(l) # <function <lambda> at 0x110bd9ea0>
print(l(1, 2)) # 3
{% endhighlight %}

람다 자체를 호출하는 방법도 있습니다. 람다 뒤에 `(*args)`를 붙여 사용합니다.

{% highlight python %}
print((lambda x, y: x + y)(1, 2))
{% endhighlight %}

매개변수가 없는 람다의 경우 람다 표현식 뒤에 `()`만 붙여 호출합니다.

{% highlight python %}
print((lambda : 1)()) # 1
{% endhighlight %}

람다 자체를 인수로 사용할 수 있습니다. 람다는 Callable한 객체를 인자로 요구하는 `map`, `filter`, `reduce` 등의 함수를 사용할 때 유용하게 사용됩니다.

{% highlight python %}
a = [1, 2, 3, 4, 5]
b = [6, 7, 8, 9, 10]

print(list(map(lambda x: x + 10, a))) # [11, 12, 13, 14, 15]
print(list(map(lambda x, y: x + y, a, b))) # [7, 9, 11, 13, 15]
{% endhighlight %}







