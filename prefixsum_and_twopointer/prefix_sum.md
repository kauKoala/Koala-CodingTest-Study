---
description: 나열된 수의 구간 합을 빠르게 구하는 알고리즘
---

# 누적합

📌누적합을 언제 사용할까?

아래 문제를 함께 봅시다.

{% embed url="https://www.acmicpc.net/problem/11659" %}

직관적으로 우리가 짤 수 있는 코드는 다음과 같습니다.\
그냥 l과 r을 입력받아서 arr에서 차례대로 원소를 가져와 sum에 더하면 되겠죠?

```python
import sys
input=sys.stdin.readline

n,m=map(int,input().split())
arr = [*map(int,input().split())]

for i in range(m):
    l, r=map(int,input().split())
    ans=0
    for j in range(l-1,r):
        ans+=arr[j]
    print(ans)
```

그런데 11659가 요구하는 시간제한은 1초로 1억번의 연산 안에 통과해야 합니다.\
극단적인 경우 위 연산은 O(NM)일텐데 N과 M 모두 100,000이므로 통과할 수 없습니다.

이럴 때 누적합을 사용합니다.

📌  1차원 누적합\
아이디어만 중요할 뿐 그리 어려운 로직은 아닙니다.

![](<../.gitbook/assets/image (13).png>)고등학교 때 많이 본 이 로직과 비슷합니다.

일단 기존 arr가 있다면 피보나치 수열 형태로 prefix\_sum을 만듭니다.

![](<../.gitbook/assets/image (3).png>)![](<../.gitbook/assets/image (25).png>)

만약 arr\[2]+arr\[3]을 하고 싶다면 prefix\_sum\[3]-prefix\_sum\[1]을 하면 자동적으로 구해지는 것을 증명할 수 있습니다.

```python
#누적합
#완전탐색은 O(NM)인데 누적합은 O(N+M)이다
import sys
input=sys.stdin.readline

n,m=map(int,input().split())
arr = [*map(int,input().split())]

psum=[0]*(n+1)
for i in range(1,n+1):
    psum[i]=psum[i-1]+arr[i-1]

for i in range(m):
    l, r=map(int,input().split())
    print(psum[r]-psum[l-1])
```

📌2차원 - 2167

{% embed url="https://www.acmicpc.net/problem/2167" %}

공식처럼 외우고 응용에 써먹는 게 중요하다.\
누적합을 다른 곳에서 쓰기도 함.\
그 일례로 문제 2571이 좋은 것 같음.
