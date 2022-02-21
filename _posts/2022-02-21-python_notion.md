---
layout: post
title: "[python] set과 list 사소한 차이??"
tags: 
- python
math: true
date: 2022-02-21 20:00 +0800
---

### set vs list

---

문자열 관련 코딩 테스트 문제를 풀다가 당연스럽게 생각했던 문제에서 시간 초과로 실패했다.
복잡도를 생각해보다가 절대 성공할 수 없다고 생각되어, 문제가 될 것 같은 부분을 찾기 시작했다.
다른 사람들의 코드도 참고하던 중 이상한 부분을 발견했다. 

list
```python
arr = list()
result = list()
for i in range(n):
    temp = sys.stdin.readline().strip()
    if temp in arr:
        result.append(temp)
```

set
```python
arr = set()
result = list()
for i in range(n):
    temp = sys.stdin.readline().strip()
    if temp in arr:
        result.append(temp)
```

차이는 set과 list 차이만 존재했다. 
두 코드에서 시간 복잡도 차이가 난 이유는 set과 list의 a in b 연산 차이다.

- list의 a in b 평균 시간 복잡도 : O(n)
- set의 a in b 평균 시간 복잡도 : O(1)

이유는 python에서 set를 해시 테이블로 구현하기 때문이다. 
접근 자체가 다르기 때문에 드라마틱한 시간 차이가 존재한다.
