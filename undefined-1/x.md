---
description: >-
  모든 경우의 수를 탐색하다 만약 조건에 맞지 않으면 그 즉시 중단하고 이전으로 돌아가여 다시 확인하는 것을 반복하면서 원하는 조건을 찾는
  알고리즘
---

# 완전탐색 (백트래킹) X

백트래킹 유형을 가장  잘 보여주는 백준 온라인 저지의 9663번 N-Queen 문제를 함께 살펴봅시다.\
[https://www.acmicpc.net/problem/9663](https://www.acmicpc.net/problem/9663)

N-Queens 문제의 규칙은 퀸이 놓였을 때 퀸 자신을 기준으로 일직선상(가로 및 세로)과 대각선 방향에는 아무것도 놓여있으면 안 된다는 것이고, 우리는 **4번째 줄까지 퀸을 놓는 경우의 수**를 구하고 싶습니다.

예를 들어 아래와 같이 퀸의 가로에 퀸을 놓을 수 없습니다.

![](<../.gitbook/assets/image (1).png>)

우리가 어떤 과정을 거쳐 판단을 내릴 수 있을지 봅시다.\


<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>



코드로 백트래킹을 구현할 시, 재귀함수가 많이 쓰입니다. dfs

```
import sys
input=sys.stdin.readline
def check(x):
    for i in range(x):
        if col[x]==col[i] or abs(col[i]-col[x])==x-i: 
        #+ 모양이나 X 모양 중 해당하는 게 있으면 안된다.
            return False
    return True

def dfs(x):
    global res #전역변수로 할당
    if x==n: #마지막 행에 도달하면
        res+=1 #오키 잘했어 하면서 경우의 수 하나를 찾은 거임
    else:
        for i in range(n):
            col[x]=i #x열의 행은 i라고 하면
            if check(x):
                dfs(x+1)
n=int(input())
res=0
col=[0]*n


dfs(0)
print(res)
```

N과 M 시리즈

15684
