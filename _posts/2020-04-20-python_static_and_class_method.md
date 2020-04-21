---
title: Python. 정적 메소드(@classmethod & @staticmethod)
date: 2020-04-20
categories:
- Python
tags:
- Python
- Instance Method
- Static Method
- Class Method
---

파이썬에서 클래스 안에서 정의되는 메소드는 크게 인스턴스 메소드, 스태틱 메소드, 클래스 메소드가 있습니다. 스태틱 메소드와 클래스 메소드를 **정적 메소드**라 표현합니다. **정적 메소드**는 클래스를 통해 직접 접근할 수 있는 메소드를 의미합니다. 기존에는 클래스 속 정의된 인스턴스 메소드를 호출하기 위해 1)클래스 정의 2)객체 생성 3)함수 호출의 과정을 거쳐야 했으나, 정적 메소드를 활용하면 객체를 생성하지 않고 클래스 이름 뒤에 마침표(.)를 찍어 직접 호출이 가능합니다. 

**인스턴스 메소드**는 인스턴스를 통해 호출이 되며, 첫 번째 인자 `self`로 인스턴스 자신을 전달합니다. **클래스 메소드**는 첫 번째 인자로 클래스 자신인 `cls`를 전달합니다. **스태틱 메소드**는 인스턴스나 클래스를 인자로 받지 않으며, 클래스 안에서는 일반 함수와 동일한 기능을 합니다. 다만, 정적 메소드는 함수 앞에 `데코레이터(@)`를 사용하여 해당 함수가 정적 메소드임을 나타냅니다. 아래의 예제를 통해 인스턴스 메소드와 정적 메소드가 코드에서 어떻게 정의되는지 살펴보겠습니다.

{% highlight python %}
class ClassName:
    def func(arg1, arg2, ..):
        code ..

    @staticmethod
    def func(arg1, arg2, ..): 
        code ..
        
    @classmethod
    def func(cls, arg1, arg2, ..): 
        code ..
{% endhighlight %}

그렇다면, 예제를 통해 정적 메소드를 언제 사용해야 하는지 알아보겠습니다. 아래의 예제는 물가상승률을 반영하여 직원들의 급여를 인상해주는 코드입니다. 먼저, 일반적인 클래스와 인스턴스 메소드만으로 코드를 구성해보겠습니다.

{% highlight python %}
class Employee(object):
    inf_rate = 1.2
    
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary
        
    def raise_salary(self):
        self.salary = int(self.salary * self.inf_rate)
    
    def get_salary(self):
        return '{}의 급여는 {}원 입니다.'.format(self.name, self.salary)
    
emp_1 = Employee('Kim', 10000)
emp_2 = Employee('Lee', 20000)

# 급여 인상 전
print(emp_1.get_salary()) # Kim의 급여는 10000원 입니다.
print(emp_2.get_salary()) # Lee의 급여는 20000원 입니다.

emp_1.raise_salary()
emp_2.raise_salary()

# 급여 인상 후 
print(emp_1.get_salary()) # Kim의 급여는 12000원 입니다.
print(emp_2.get_salary()) # Lee의 급여는 24000원 입니다.
{% endhighlight %}

## @classmethod

`Employee` 클래스에 정의된 클래스 변수인 물가상승률 `inf_rate`를 변경하는 방식으로 급여 인상 코드를 구성할 수 있지만, 다른 부가적인 기능 등을 추가할 때 **클래스 메소드**를 사용하면 편리합니다. 클래스 내부에 `change_inf_rate` 클래스 메소드를 정의하여 `Employee` 클래스의 클래스 변수 `inf_rate`를 조정할 수 있도록 하였습니다. `change_inf_rate` 함수에서는 물가상승률이 1 이하가 되는 경우, 원래 급여를 유지하도록 하는 예외처리 코드를 삽입하였습니다.

{% highlight python %}
class Employee(object):
    inf_rate = 1.2
    
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary
        
    def raise_salary(self):
        self.salary = int(self.salary * self.inf_rate)
    
    def get_salary(self):
        return '{}의 급여는 {}원 입니다.'.format(self.name, self.salary)
    
    @classmethod
    def change_inf_rate(cls, rate):
        if rate < 1:
            rate = 1.0
            cls.inf_rate = 1.0
            print('급여를 삭감할 수 없습니다.')
            print('자동적으로 {}%가 반영되었습니다.'.format(rate))
        else:
            cls.inf_rate = rate
            print('물가상승률 {}%가 반영되었습니다.'.format(rate))
    
emp_1 = Employee('Kim', 10000)
emp_2 = Employee('Lee', 20000)

# 급여 인상 전
print(emp_1.get_salary()) # Kim의 급여는 10000원 입니다.
print(emp_2.get_salary()) # Lee의 급여는 20000원 입니다.

Employee.change_inf_rate(2.0) # 물가상승률 2.0%가 반영되었습니다.
emp_1.raise_salary()
emp_2.raise_salary()

# 급여 인상 후 
print(emp_1.get_salary()) # Kim의 급여는 20000원 입니다.
print(emp_2.get_salary()) # Lee의 급여는 40000원 입니다.
{% endhighlight %}

정상적으로 물가상승률이 조정되어 급여가 인상되었음을 확인할 수 있습니다.

## @staticmethod
스태틱 메소드는 클래스 안에서 정의될 때 인스턴스 메소드와 크게 다를 바 없습니다. 이러한 이유로 스태틱 메소드는 잘 안쓰이는 편이지만, 클래스와 연관성 있는 함수를 클래스 내에 위치시켜 코드 파악이 쉽고, 조금 더 쉽게 호출하여 사용할 수 있다는 장점을 가지고 있습니다.

{% highlight python %}
class Employee(object):
    inf_rate = 1.2
    
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary
        
    def raise_salary(self):
        self.salary = int(self.salary * self.inf_rate)
    
    def get_salary(self):
        return '{}의 급여는 {}원 입니다.'.format(self.name, self.salary)
    
    @classmethod
    def change_inf_rate(cls, rate):
        if rate < 1:
            rate = 1.0
            cls.inf_rate = 1.0
            print('급여를 삭감할 수 없습니다.')
            print('자동적으로 {}%가 반영되었습니다.'.format(rate))
        else:
            cls.inf_rate = rate
            print('물가상승률 {}%가 반영되었습니다.'.format(rate))

    @staticmethod
    def is_gt_50000(salary):
        return salary > 50000

emp_1 = Employee('Kim', 10000)
emp_2 = Employee('Lee', 20000)

# 급여 인상 전
print(emp_1.get_salary()) # Kim의 급여는 10000원 입니다.
print(emp_2.get_salary()) # Lee의 급여는 20000원 입니다.

Employee.change_inf_rate(3.0) # 물가상승률 3.0%가 반영되었습니다.
emp_1.raise_salary()
emp_2.raise_salary()

# 급여 인상 후 
print(emp_1.get_salary()) # Kim의 급여는 30000원 입니다.
print(emp_2.get_salary()) # Lee의 급여는 60000원 입니다.

# 급여가 50000을 넘는지 확인 
print(emp_1.is_gt_50000(emp_1.salary)) # False
print(emp_2.is_gt_50000(emp_2.salary)) # True
{% endhighlight %}

## References
1. http://schoolofweb.net/blog/posts/%ED%8C%8C%EC%9D%B4%EC%8D%AC-oop-part-4-%ED%81%B4%EB%9E%98%EC%8A%A4-%EB%A9%94%EC%86%8C%EB%93%9C%EC%99%80-%EC%8A%A4%ED%83%9C%ED%8B%B1-%EB%A9%94%EC%86%8C%EB%93%9C-class-method-and-static-method/







