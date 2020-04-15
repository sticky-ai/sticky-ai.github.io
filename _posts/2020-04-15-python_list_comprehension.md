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

List Comprehension의 사용 방법은 기존의 `for` 반복문과 크게 다르지 않으며, 다음과 같은 형태를 가집니다. `[{변수} for {변수} in {iterable} if {조건}]` 변수와 iterable은 반드시 필요하며, 조건은 Option 입니다. 위와 같은 코드를 `대괄호[]`로 감싸주어야 List Comprehension이 완성됩니다.

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

# 그 외 다양한 Comprehension

## Dictionary Comprehension
List Comprehension과 유사한 문법으로 Dictionary를 효과적으로 생성할 수 있습니다. 차이점이라면 Comprehension 구문을 `대괄호[]`가 아닌 `중괄호{}`로 감싸준다는 것과 `Key`와 `Value`로 구성되어야 한다는 점입니다.

{% highlight python %}
number = [101, 102, 103, 104, 105]
name = ['Kim', 'Lee', 'Park', 'Choi', 'Jeong']

dict_comp = {key: value for key, value in zip(number, name)}
print(dict_comp) # {101: 'Kim', 102: 'Lee', 103: 'Park', 104: 'Choi', 105: 'Jeong'}
{% endhighlight %}

## Generator Comprehension (Expression)
`Generator`도 Comprehension 구문을 사용하여 손쉽게 생성할 수 있습니다. `소괄호()`를 사용하면 됩니다.

{% highlight python %}
gen_comp = (i for i in range(10))
print(next(gen_comp)) # 0
print(next(gen_comp)) # 1
{% endhighlight %}





