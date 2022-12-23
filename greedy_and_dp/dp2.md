---
description: 복잡한 문제를 간단한 여러 개의 문제로 나누어 푸는 방법
---

# 다이나믹 프로그래밍 2 O

DP를 활용하는 다양한 문제유형이 있는데요, 같이 한 번 알아볼까요?

📌**최장 증가 부분 수열(LIS, Longest Increasing Subsequence)**

원소가 n개인 배열의 일부 원소를 골라내서 만든 부분 수열 중, 각 원소가 이전 원소보다 크다는 조건을 만족하고, 그 길이가 최대인 부분 수열을 최장 증가 부분 수열이라고 합니다.

* 예를 들어, { 6, **2**, **5**, 1, **7**, 4, **8**, 3} 이라는 배열이 있을 경우, LIS는 { 2, 5, 7, 8 } 이 됩니다.
* { 2, 5 }, { 2, 7 } 등 증가하는 부분 수열은 많지만 그 중에서 가장 긴 것이 { 2, 5, 7, 8 } 입니다.

{% embed url="https://www.acmicpc.net/problem/11053" %}

첫번째 인덱스부터 수열의 길이의 최댓값을 저장해 나갑니다.\
수열 a = {10, 20, 10, 30, 20, 50}이 있을 때, 4번째 숫자(30)까지의 수열의 길이의 최댓값을 구해봅시다.

첫번째 숫자부터 검사를 해 나갑니다.\
자기 자신(30)보다 작은 숫자들 중 가장 큰 길이를 구하고 그 길이에 +1을 하면 됩니다.

| 수열 | 10 | 20 | 10 | 30 | 20 | 50 |
| -- | -- | -- | -- | -- | -- | -- |
| 길이 | 1  | 2  | 1  | 3  | 2  | 4  |

```python
x = int(input())

arr = list(map(int, input().split()))
dp = [1 for i in range(x)]

for i in range(x):
    for j in range(i):
        if arr[i] > arr[j]:
        #증가하기만 하면 일단 갱신시켜본다.
            dp[i] = max(dp[i], dp[j]+1)

print(max(dp))
```

위 LIS 성질을 이용해 아래 문제를 풀어봅시다.

{% embed url="https://www.acmicpc.net/problem/14002" %}

LIS 규칙에 따르면 가장 긴 길이는 앞에서 나온 수에 +1을 하였음을 알 수 있습니다. \
따라서 위 표에서 맨 뒤부터 추적하여 LIS 값인 4부터 시작하여 4, 3, 2, 1을 차례대로 추적하면 됩니다.

```python
n=int(input())
A=list(map(int,input().split()))
#LIS 로직
dp=[1]*n
for i in range(1,n):
    for j in range(i):
        if A[i]>A[j]: dp[i]=max(dp[i],dp[j]+1)


ans=[]

std=max(dp) 
print(std)

for i in range(n-1,-1,-1):
        if dp[i]==std:
            ans.append(A[i])
            std-=1

for i in ans[::-1]:
    print(i,end=' ')

```



📌**최장 공통 부분수열(LCS, Longest Common Subsequence)**

**공통 부분 문자열 중 가장 길이가 긴 문자열**을 말합니다. 이 때, 전체 문자열에서 **꼭 연속된 문자열일 필요는 없습니다.**

* 예를 들어 ABCDEF 와 ACDGHI 와의 **공통 Subsequence 중 가장 길이가 긴 것은 A**B**CD**EF / **A**ZG**CD**GHI 에서 **ACD** 입니다.

{% embed url="https://www.acmicpc.net/problem/9251" %}

문제에 나온 ACAYKP, CAPCAK의 예시를 들어봅시다..\
앞에 나온 문자를 S1, 뒤에 나온 문자를 S2라고 합시다.

일단 S1을 기준으로 비교합니다. S1의 A 과 S2의 C, CA, CAP, CAPC, CAPCA, CAPACAK 를 비교한 후 S1을 하나 늘려 비교하기 시작합니다. S1의 AC와 ...\
이 과정을 S1이 끝날 때까지 반복합니다.&#x20;

이 때 DP 테이블을 채우는 과정은 다음과 같습니다.\
S1의 A와 S2를 비교하는 과정을 볼까요?

\
S1\[0]과 S2\[0]은 달라 0입니다.

S1\[0]과 S2\[1]은 A로 같기 때문에 1을 증가해줍니다.

S1\[0]과 S2\[2]는 다릅니다. 이럴 경우에도 여전히 A와 CAP의 공통부분은 1개이므로, 1로 유지합니다.

|   | C | A | P | C | A | K |
| - | - | - | - | - | - | - |
| A | 0 | 1 | 1 | 1 | 1 | 1 |

...\
이런 규칙을 계속 따라 나가다 보면

다음 표와 같은 결과가 나옴을 알 수 있습니다.

|   | C | A | P | C | A | K |
| - | - | - | - | - | - | - |
| A | 0 | 1 | 1 | 1 | 1 | 1 |
| C | 1 | 1 | 1 | 2 | 2 | 2 |
| A | 1 | 2 | 2 | 2 | 3 | 3 |
| Y | 1 | 2 | 2 | 2 | 3 | 3 |
| K | 1 | 2 | 2 | 2 | 3 | 4 |
| P | 1 | 2 | 3 | 3 | 3 | 4 |

```python
A=input()
B=input()
dp=[[0]*1001 for _ in range(1001)]

ans=0
for i in range(1, len(A)+1):
    for j in range(1, len(B)+1):
        if A[i-1]==B[j-1]: dp[i][j]=dp[i-1][j-1]+1
        else: dp[i][j]=max(dp[i-1][j],dp[i][j-1])
        ans=max(ans, dp[i][j])
print(ans)
```



📌**KNAPSACK(14863)** 보류 -고난이도 토스에서 한 번
