---
title: Python. List Comprehension
date: 2020-04-15
categories:
- Python
tags:
- Python
- List Comprehension
---

**List Comprehension**은 리스트를 생성하는 파이썬의 독특한 코드 형태를 의미합니다. List Comprehension을 활용하면 리스트를 생성하고 값을 하나씩 넣어줘야 하는 번거로운 과정을 단 몇 줄로 간단하게 표현할 수 있다는 장점을 가지고 있습니다.

# List Comprehension
기존 리스트 생성 방법과 List Comprehension을 활용한 방법을 비교해보겠습니다. 일반적으로, 0부터 9까지의 숫자를 포함하는 리스트를 생성한다면 다음과 같이 변수를 정의하고, `for` 반복문을 활용하여 생성되는 값을 `append` 함수를 통해 넣어주어야 합니다. 
{% highlight python %}
foo = []
for i in range(10):
    foo.append(i)
print(foo) # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
{% endhighlight %}

List Comprehension을 활용하면 한 줄로 간단하게 표현할 수 있습니다.
{% highlight python %}
foo = [i for i in range(10)]
print(foo) # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

bar = [i*10 for i in range(10)]
print(bar) # [0, 10, 20, 30, 40, 50, 60, 70, 80, 90]
{% endhighlight %}

## 조건문을 활용한 List Comprehension
List Comprehension에 조건을 추가할 수 있습니다. 아래의 예제는 조건을 추가하여 홀수만을 원소로 가지도록 하였습니다.
{% highlight python %}
foo = [i for i in range(10) if i%2 != 0]
print(foo) # [1, 3, 5, 7, 9]
{% endhighlight %}

만약, 조건문에서 `if` 뿐만 아니라 `else`까지 활용하고자 한다면 구문의 순서가 약간 달라집니다. 아래의 예제는 홀수만 출력하도록 함과 동시에 0을 포함한 짝수에 해당하는 원소를 모두 0으로 치환하였습니다.
{% highlight python %}
bar = [i if i%2 != 0 else 0 for i in range(10)]
print(bar) # [0, 1, 0, 3, 0, 5, 0, 7, 0, 9]
{% endhighlight %}

## List Comprehension 응용
List Comprehension을 활용하여 2중 `for` 반복문을 효과적으로 표현할 수 있습니다. 먼저, 기존의 2중 `for` 반복문을 활용하여 구구단을 출력해보도록 하겠습니다.
{% highlight python %}
foo = []
for i in range(1, 10):
    for j in range(1, 10):
        foo.append(i * j)
print(foo) # [1, 2, 3, 4, 5, 6, 7, 8, 9, 2, 4, 6, 8, 10, 12, 14, 16, 18, 3, 6, 9, 12, 15, 18, 21, 24, 27, ...]
{% endhighlight %}

List Comprehension을 활용하면 간단하게 나타낼 수 있습니다.
{% highlight python %}
bar = [i * j for i in range(1, 10) for j in range(1, 10)]
print(bar) # [1, 2, 3, 4, 5, 6, 7, 8, 9, 2, 4, 6, 8, 10, 12, 14, 16, 18, 3, 6, 9, 12, 15, 18, 21, 24, 27, ...]
{% endhighlight %}



