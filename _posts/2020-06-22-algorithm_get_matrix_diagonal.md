---
title: Algorithm. 행렬의 대각 성분을 출력하는 방법
date: 2020-06-22
categories:
- Algorithm
tags:
- Python
- Diagonal
---

파이썬에서 행렬(Matrix) 데이터 타입을 다룰 때, 대각 성분을 출력하고자 하는 경우가 있습니다. `NUMPY`등의 라이브러리를 사용하면 손쉽게 대각 성분을 출력할 수 있지만, 본 포스팅에서는 각 인덱스에 접근하여 출력하는 방법을 소개하고자 합니다.

## 좌표 초기값이 지정되어 있지 않을 때
{% highlight python %}
def get_matrix(n): # n * n 행렬을 생성
    m = []
    c = 0
    for i in range(n):
        temp = []
        for j in range(n):
            temp.append(c)
            c += 1
        m.append(temp)
    return m

m = get_matrix(5) # [[0, 1, 2, 3, 4], [5, 6, 7, 8, 9], [10, 11, 12, 13, 14], [15, 16, 17, 18, 19], [20, 21, 22, 23, 24]]
{% endhighlight %}

{% highlight python %}
def get_diag(m):
    return [m[i][i] for i in range(len(m))]
    
def get_diag_reverse(m):
    return [m[idx][i] for idx, i in enumerate(range(len(m)-1, -1, -1))]

diag = get_diag(m)
diag # [0, 6, 12, 18, 24]

diag_rev = get_diag_reverse(m)
diag_rev # [4, 8, 12, 16, 20]
{% endhighlight %}

## 좌표 초기값이 지정되어 있을 때
{% highlight python %}
def get_pos_diag(m, x, y):
    l = len(m)
    e = set()
    for i in range(l):
        if x+i < l and y+i < l:
            e.add(m[x+i][y+i])
        if x-i >= 0 and y-i >=0:
            e.add(m[x-i][y-i])
    return sorted(list(e))
    
def get_pos_diag_reverse(m, x, y):
    l = len(m)
    e = set()
    for i in range(l):
        if x+i < l and y-i >=0:
            e.add(m[x+i][y-i])
        if x-i >= 0 and y+i < l:
            e.add(m[x-i][y+i])
    return sorted(list(e))
    
pos_diag = get_pos_diag(m, 2, 3)
pos_diag # [1, 7, 13, 19]

pos_diag_rev = get_pos_diag_reverse(m, 2, 3)
pos_diag_rev # [9, 13, 17, 21]
{% endhighlight %}