---
layout: post
title: [프로그래머스] 무지의 먹방 라이브
date: 2022-01-24 20:00 +0800
last_modified_at: 2022-01-24 20:00:00 +0800
tags: [programmers, binary_search]
toc:  true
---
해당 문제는 "이것이 코딩 테스트다"에서 그리디 문제로 분류 되어 있었고, 따라서 그리디로 해결하려 노력했던 문제이다. 

## 풀기 전 생각 정리
1) 시간 k를 기준으로 while문을 반복적으로 돌려, k가 1씩 증가함에 따라 food_times를 갱신하자.
==> 효율성 테스트에서 k의 범위는 1 <= k <= 2*10^13 이므로 불가능한 아이디어

2) 원소의 크기 범위가 1 <= 원소 크기 <= 100,000,000이므로 k와 가까운 값을 찾기 위해 기준이 되는 원소 크기를 구해보자. 
==> 이분 탐색을 통해 구현해보는 것으로 채택


### Code

{% highlight js %}
def solution(food_times, k):
    ft_len = len(food_times)

    if k >= sum(food_times):    # 방송이 정지 되기전에 다 먹어 더이상 먹을 것이 없는 경우
        return -1
    if k < ft_len:              # 원소 크기가 최소 1이니까, 한바퀴도 못 돌았을 때 정전이 나는 경우
        return k+1
    if k == ft_len:             # 정확히 한바퀴 돌고, 정전이 난 경우
        return 1

    # 이분 탐색으로 어느 숫자가 k에 가깝게 만들어 주는지 찾음
    start = 1
    end = 100000000

    while start <= end:
        mid = int((start+end)/2)
        count = 0
        for i in range(ft_len):
            if food_times[i] < mid:
                count += food_times[i]
            else:
                count += mid
        if count > k:
            end = mid -1
        else:
            start = mid + 1

    # 여기서 찾은 크기로 list 초기화
    mid = int((start + end) / 2)
    remain = 0
    for i in range(ft_len):
        if food_times[i] <= mid:
            remain += food_times[i]
            food_times[i] = 0
        else:
            food_times[i] -= mid
            remain += mid

    # 먹을 것이 남아 있는 음식들을 확인해서 최종적으로 먹기 시작해야할 음식의 position을 찾음
    k -= remain
    for i in range(ft_len):
        if food_times[i] != 0:
            k -= 1
        if k == -1:
            return i+1


{% endhighlight %}