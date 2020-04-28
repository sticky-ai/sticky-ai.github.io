---
title: Python. 정규 표현식(Regular Expression) - 1
date: 2020-04-28
categories:
- Python
tags:
- Python
- Regular Expression
---

**정규 표현식(Regular Expression)**은 복잡한 문자열을 손쉽게 처리할 수 있도록 하는 프로그래밍 방법 중 하나입니다. 파이썬을 포함한 대부분의 프로그래밍 언어에서 정규 표현식(이하 정규식)을 지원합니다. 문자열을 처리해야 하는 코드를 작성할 때 정규식을 사용하면 간단하게 나타낼 수 있습니다. 만약, 사용자의 이메일에서 아이디 부분을 모자이크 처리해야 하는 코드가 필요하다고 할 때, 일반적으로 다음과 같은 맥락으로 코드가 구성됩니다.

{% highlight python %}
def check_mail_pattern(mail): # 이메일 유효성 검사 함수 작성
    if '@' not in mail: # 문자열에 '@'가 들어있지 않으면 에러 발생
        raise ValueError
    else:
        split = mail.split('@')
        if len(split[0]) == 0 or len(split[1]) == 0: # '@'를 기준으로 구분한 문자열 앞뒤의 길이가 0이면 에러 발생
            raise ValueError


mail = ['Kim@naver.com', 'Lee@gmail.com', 'Park@hanmail.com', 'abcde', 'asd@']

result = []
for i in mail:
    try:
        check_mail_pattern(i) # 메일 유효성 검사
        split = i.split('@') 
        result.append('*****' + '@' + split[1]) # 아이디 모자이크
    except:
        result.append('i') # 메일 유효성 검사 실패 시 그대로 반환
            
print(result) # ['*****@naver.com', '*****@gmail.com', '*****@hanmail.com', 'Not Applicable', 'Not Applicable']
{% endhighlight %}

이메일 유효성을 검사하는 함수를 별도로 만들어 올바른 이메일 형식인지 확인하고, 올바른 이메일 형식이라면 모자이크를 진행하도록 하였습니다. 20줄에 육박하는 코드가 작성되었습니다. 하지만, 정규식을 사용하면 간단하게 나타낼 수 있습니다.

{% highlight python %}
import re # 정규표현식 라이브러리 호출

mail = ['Kim@naver.com', 'Lee@gmail.com', 'Park@hanmail.com', 'abcde', 'asd@']

p = re.compile('(\w+)[@](\w+[.]\w+)') # 정규표현식 정의
result = [p.sub('*****@\g<2>', i) for i in mail] # 결과 반환

print(result) # ['*****@naver.com', '*****@gmail.com', '*****@hanmail.com', 'abcde', 'asd@']
{% endhighlight %}

정규 표현식을 사용하여 복잡한 코드를 2줄로 간결하게 나타낼 수 있다는 것을 확인할 수 있었습니다. 이처럼 정규식은 복잡한 문자열을 처리할 때 엄청난 힘을 발휘합니다. 다음 포스팅에서는 이러한 정규식을 어떻게 사용하는지에 대해 더욱 자세히 알아보겠습니다.



