---
title: Python. Property
date: 2020-04-20
categories:
- Python
tags:
- Python
- Property
- Getter
- Setter
---

클래스에서 함수를 사용하여 값을 가져오거나 저장하는 경우가 있습니다. 일반적으로 `getter`, `setter`라고 명명합니다. 말 그대로 값을 가져오거나 저장하기 위해 만들어진 함수를 의미합니다. 아래의 예제는 `Person`이라는 클래스에 이름을 저장하는 setter `set_name` 함수와 이름을 가져오는 getter `get_name` 함수로 구성되어 있습니다. 

## 일반적인 Getter와 Setter

{% highlight python %}
class Person:
    def __init__(self, name):
        self.name = name
    
    def set_name(self, name):
        self.name = name
        
    def get_name(self):
        return self.name
        
p = Person('Kim')
print(p.get_name()) # Kim

p.set_name('Lee')
print(p.get_name()) # Lee
{% endhighlight %}

객체를 생성하면 `__init__` 함수에 의해 `name` 변수에 'Kim'이라는 이름이 저장되었습니다. 이후, `set_name` 함수를 통해 이름을 'Lee'로 변경하였고, 바뀐 이름으로 출력되는 것을 확인할 수 있습니다.

## @property와 @_.setter

파이썬에서 제공하는 `@property`와 `@_.setter` 데코레이터를 사용하면 더욱 손쉽게 값을 할당하고 호출할 수 있습니다.

{% highlight python %}
class Person:
    def __init__(self, name):
        self.__name = name
    
    @property
    def name(self):
        return self.__name
    
    @name.setter
    def name(self, name):
        self.__name = name
        
p = Person('Kim')
print(p.name) # Kim

p.name = 'Lee'
print(p.name) # Lee
{% endhighlight %}

동일한 함수명 `name`에 `@property`와 `@name.setter` 데코레이터를 추가하고 `인스턴스.속성` 형식으로 접근하여 값을 할당하고 불러오는 것을 확인할 수 있습니다.