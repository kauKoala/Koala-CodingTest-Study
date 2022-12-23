---
description: 나열된 수의 구간 합을 빠르게 구하는 알고리즘
---

# 누적합

📌누적합이 언제 효과적일까요??

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

![](<../.gitbook/assets/image (3) (6).png>)![](<../.gitbook/assets/image (25).png>)

arr\[2]+arr\[3]에 해당하는 부분합은 prefix\_sum\[3]-prefix\_sum\[1]을 하면 자동적으로 구해지는 것을 증명할 수 있습니다.

<pre class="language-python"><code class="lang-python">#누적합
#완전탐색은 O(NM)인데 누적합은 O(N+M)이다
import sys
input=sys.stdin.readline

n,m=map(int,input().split())
arr = [*map(int,input().split())]

psum=[0]*(n+1)
for i in range(1,n+1):
    psum[i]=psum[i-1]+arr[i-1]

<strong>for i in range(m):
</strong>    l, r=map(int,input().split())
    print(psum[r]-psum[l-1])
</code></pre>

📌2차원 - 2167\
이번에는 누적합을 이차원으로 구현하는 방법에 대해 알아봅시다.

{% embed url="https://www.acmicpc.net/problem/2167" %}

이차원 누적합의 초기화 단계는 다음과 같습니다.

①A(i, j)에서 행방향으로 누적합을 구합니다\
****②행 누적합에 대해서 열방향으로 누적합을 구합니다.

이 때 우리가 고등학교 때 배웠던 세 집합의 합집합을 구하는 공식과 비슷한 로직이 들어갑니다.

![](<../.gitbook/assets/image (22).png>)A∪B∪C = A+B+C-A∩B-A∩C-B∩C+A∩B∩C 기억하죠?

다음과 같은 표 A의 누적합을 구하고 싶습니다.

|  1 | 4 | 4 | 9 |
| -- | - | - | - |
| 3  | 2 | 7 | 6 |
| 5  | 2 | 8 | 8 |

먼저표 A보다 행과 열이 각각 1개씩 많은 표 prefix\_sum를 만들고 0행과 0열을 모두 0으로 초기화시킵니다.

|   |   |   |   |   |
| - | - | - | - | - |
| 0 | 0 | 0 | 0 | 0 |
| 0 |   |   |   |   |
| 0 |   |   |   |   |
| 0 |   |   |   |   |

이후 **prefix\_sum\[i]\[ j]=prefix\_sum\[i-1]\[j]+prefix\_sum\[i]\[j-1]-prefix\_sum\[i-1]\[j-1]+A\[i]\[j]**를 for문으로 처리해주면 아래와 같이 우리가 의도한 대로 열 방향/행 방향 누적합이 모두 적용됩니다.

|   |   |    |    |    |
| - | - | -- | -- | -- |
| 0 | 0 | 0  | 0  | 0  |
| 0 | 1 | 5  | 9  | 18 |
| 0 | 4 | 10 | 12 | 36 |
| 0 | 9 | 17 | 36 | 59 |

그럼 이번에는 prefix\_sum 배열에서구간합을 구해볼까요?\
다아래2차원 배열에서 파란색에 해당하는 구간을 구하고 싶다고 합시다.

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

이 때 우리가 고등학교 때 배웠던 3개의 집합의 교집합을 구하는 공식과 비슷하게&#x20;

파란색 부분=  전체합 - 초록색1 - 초록색2 + 빨간색 \
으로 구할 수 있습니다.

```python
N,M=map(int,input().split())
A=[list(map(int,input().split())) for _ in range(N)]
prefix_sum=[[0 for i in range(0,M+1)] for _ in range(N+1)]

for i in range(1, N+1):
    for j in range(1, M+1):
        prefix_sum[i][j]=prefix_sum[i][j-1]+prefix_sum[i-1][j]
                            -prefix_sum[i-1][j-1]+A[i-1][j-1]

for _ in range(int(input())):
    i, j, x, y =map(int,input().split())
    print(prefix_sum[x][y]-prefix_sum[x][j-1]-prefix_sum[i-1][y]+prefix_sum[i-1][j-1])
```



사실 1,2차원 누적합은 이해한 후에, 공식처럼 외우고 응용에 써먹는 게 중요합니다. \
연속적인 어떤 구간에서 어떤 처리를 하고자 한다면 의심해보면 좋습니다.&#x20;

