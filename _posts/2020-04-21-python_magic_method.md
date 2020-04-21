---
title: Python. 매직 메소드(Magic Method)
date: 2020-04-21
categories:
- Python
tags:
- Python
- Magic Method
---

**매직 메소드(Magic Method or Special Method)**는 클래스 내에 정의할 수 있는 특별한 메소드를 의미합니다. 매직 메소드를 사용하여 미리 정의되어 있는 메소드를 재정의하여 데이터 객체를 만들거나, 연산하는데 사용합니다. 다시 말하면, 다양한 **빌트인(Built-in) 함수**들이 처리할 연산을 원하는대로 다시 정의할 수 있습니다. 

매직 메소드는 언더스코어(_)가 두 개씩 붙어 있는 것이 특징입니다. 이 언더스코어는 언더스코어가 2개씩 있다고 하여 던더(Double UNDERscore)라고 부릅니다. 대표적인 매직 메소드로 클래스를 생성할 때 정의하는 생성자인 `__init__`이나 소멸자 `__del__`가 있습니다. 물론 이 두 개의 매직 메소드 이외에도 수 많은 매직 메소드가 존재합니다.

## 매직 메소드 실습
예제를 통해 매직 메소드가 무엇이고 어떻게 사용되는지 살펴보겠습니다. 아래의 예제는 `Person` 클래스에서 생성자 `__init__` 매직 메소드를 정의하여 객체가 생성될 때 이름과 나이를 출력되게 하였습니다.

{% highlight python %}
class Person(object):
    def __init__(self, name, age):
        self.name = name
        self.age = age
        print('이름 : {} / 나이 : {}'.format(name, age))
    
person_1 = Person('Kim', 20) # 이름 : Kim / 나이 : 20
person_2 = Person('Lee', 25) # 이름 : Lee / 나이 : 25
{% endhighlight %}

우리에게 익숙한 덧셈 혹은 뺄셈과 같은 연산자 또한 매직 메소드로 다시 정의할 수 있습니다. x + y를 실행하면 x가 가지고 있는 매직 메소드인 `__add__`가 자동적으로 실행됩니다. 이는 덧셈 오퍼레이터 `+`가 자료형 `int`로부터 전달받은 매직 메소드 `__add__`를 상속받고 있기 때문입니다. 

{% highlight python %}
class MyAdd(int):
    def __init__(self, number):
        self.number = number

my_add = MyAdd(5)
print(num.__add__(10)) # 15
print(dir(my_add)) # '__abs__', '__add__', '__and__', '__bool__', '__ceil__', '__class__' ..
{% endhighlight %}

`int` 자료형을 상속받는 `MyInt` 클래스의 객체를 생성하고 해당 객체가 상속받고 있는 메소드를 확인해 보았더니 여러 매직 메소드들을 상속받고 있음을 확인할 수 있었습니다. 또한, `__add__` 매직 메소드를 직접 호출하여 덧셈을 수행했더니 정상적인 덧셈 결과가 나오는 것을 확인할 수 있었습니다.

그렇다면 이번에는 이 `__add__` 매직 메소드를 오버로딩하여 일반적인 덧셈과는 다른 결과가 나오도록 해보겠습니다.

{% highlight python %}
class MyAdd(object):
    def __init__(self, number):
        self.number = number

    def __add__(self, other):
        return self.number + other + 100
    
my_add = MyAdd(5) # 5
my_add.__add__(10) # 115
{% endhighlight %}

`MyAdd` 클래스의 `__add__` 메소드를 오버로딩하여 원래 덧셈 결과에 100을 추가적으로 더한 값을 출력하도록 하였습니다. 실제로 `__add__` 메소드를 직접 출력하여 덧셈 결과를 확인해보았더니 원래 15가 나와야 하지만, 115가 출력된 것을 확인할 수 있습니다.

## 다양한 매직 메소드
앞서 살펴본 `__add__` 매직 메소드 이외에도 여러가지 매직 메소드들이 존재합니다. 

**객체 생성 및 초기화**
* `__new__(cls[, ...])` : 새로운 클래스 인스턴스를 만들 때 가장 먼저 실행되는 메소드
* `__init__(self[, ...])` : 새로운 클래스 인스턴스가 생성된 이후 호출되는 메소드
* `__del__(self)` : 클래스 인스턴스가 소멸 될 때 호출되는 메소드

**속성(Attribute) 관리**
* `__getattr__(self, name)` : 객체에 없는 속성을 참조할 때 호출되는 메소드
* `__getattribute__(self, name)` : 객체의 속성을 참조할 때 호출되는 메소드
* `__setattr__(self, name, value)` : 객체의 속성을 변경할 때 호출되는 메소드
* `__delattr__(self, name)` : 객체의 속성을 `del` 키워드로 지울 때 호출되는 메소드
* `__dir__(self)` : 객체가 가지고 있는 모든 속성을 출력할 때 호출되는 메소드

**컨테이너 관리**
* `__len__(self)` : 객체의 길이를 반환할 때 호출되는 메소드
* `__getitem__(self)` : 객체의 인덱스를 통해 값을 조회할 때 호출되는 메소드
* `__iter__(self)` : 컨테이너의 이터레이터를 반환할 때 호출되는 메소드
* `__reversed__(self)` : 컨테이너의 순서를 반대로 바꿀 때 호출되는 메소드

**단항 연산자**
* `__neg__(self)` : `-object` 정의
* `__pos__(self)` : `+object` 정의
* `__abs__(self)` : `abs()` 정의

**비교 연산자**
* `__lt__(self, other)` : less than, $x < y$ 정의
* `__le__(self, other)` : less equal, $x <= y$ 정의
* `__gt__(self, other)` : greater than, $x > y$ 정의
* `__ge__(self, other)` : greater equal, $x >= y$ 정의
* `__eq__(self, other)` : equal, $x == y$ 정의
* `__ne__(self, other)` : not equal, $x != y$ 정의

**산술 연산자**
* `__add__(self, other)` : $x + y$ 정의
* `__sub__(self, other)` : $x - y$ 정의
* `__mul__(self, other)` : $x * y$ 정의
* `__matmul__(self, other)` : $x @ y$ 정의
* `__truediv__(self, other)` : $x / y$ 정의
* `__floordiv__(self, other)` : $x // y$ 정의
* `__mod__(self, other)` : $x % y$ 정의
* `__pow__(self, other[, modulo])` : $x ** y$ 정의
* `__round__(self[, n])` : 반올림 함수 `round()` 정의

**논리 연산자**
* `__and__(self, other)` : $x & y$ 정의
* `__or__(self, other)` : $x | y$ 정의
* `__xor__(self, other)` : $x \^ y$ 정의

**타입 변환**
* `__int__(self)` : `int()` 정의
* `__float__(self)` : `float()` 정의
* `__bool__(self)` : `bool()` 정의

## References 
1. https://corikachu.github.io/articles/python/python-magic-method

