---
description: 컴퓨터의 빠른 계산 능력을 이용해 가능한 경우의 수를 일일이 나열하면서 답을 찾는 알고리즘
---

# 완전 탐색

**완전 탐색**이란 모든 경우의 수를 다 따져가며 정답을 찾는 방식을 의미합니다.

**브루트포스(brute-force) 알고리즘**이라고도 하며, "무식하게 푸는 방법"이라고 생각해도 좋습니다.

예를 들어, 사람이 4자리 수의 자물쇠를 푸는데는 오랜 시간이 걸립니다. 운이 좋지 않으면 총 10,000번의 시도를 해야합니다. 하지만 컴퓨터의 빠른 계산 능력을 빌린다면, 이러한 문제는 아주 적은 시간만에 풀어낼 수 있습니다.

이처럼 컴퓨터의 빠른 속도를 믿고 "전부" 해보는 방식이 바로 **완전 탐색**입니다.

즉, 완전 탐색은 **O(N)** 만큼의 시간 복잡도를 가집니다.



하지만, 대부분의 알고리즘 문제는 **시간 제한**이 있습니다. 안타깝게도 **완전 탐색**은 이러한 시간 문제에 자유롭지 못합니다.

백준 문제의 좌측 상단에서 **시간 제한**을 찾아볼 수 있는데, 보통 **1초**에 약 **1억 번**의 연산을 할 수 있다고 생각하시면 됩니다.



예를 들어 컴퓨터가 1부터 10억까지의 수 중 하나를 고르고, 제가 그 수를 **1초** 안에 맞춰야 하는 상황을 가정하겠습니다.

최악의 경우에는 10억 번의 시도가 필요합니다. 즉, 약 10초가 소요되는 이러한 경우에는 **완전 탐색**을 사용할 수 없습니다.



결론적으로 모든 문제를 풀 때는

1️⃣ **시간 복잡도를 계산하고**

**2️⃣ 이를 기반으로 완전 탐색 가능 여부를 판단한다**

의 순서로 접근하셔야 합니다.

시간 제한으로 완전탐색이 어렵다고 판단이 되면, 다른 알고리즘을 고안하시면 됩니다.



## 연습문제

### BOJ 13423

{% embed url="https://www.acmicpc.net/problem/13423" %}

간단히 말해서, 입력받은 N개의 점 중 간격이 동일한 세 개의 점의 **조합**이 총 몇 개인지 구하는 문제입니다.

3중 반복문을 통해 3개의 점을 골라내거나, itertools의 combinations을 생각해볼 수 있습니다.

여기서는 combinations를 사용해보도록 하겠습니다.

```python
from itertools import combinations as cb

t = int(input())
for _ in range(t):
    n = int(input())
    li = list(map(int, input().split()))
    li.sort()
    ans = 0
    for i in cb(li, 3):
        if i[2] - i[1] == i[1] - i[0]:
            ans += 1
    print(ans)
```

시간 제한이 없다면 이 방식으로 풀어도 문제가 없습니다.

하지만 점이 최대 1,000개이기 때문에, 약 1,000 \* 1,000 \* 1,000 만큼의 연산이 필요하고 이는 1초의 시간 제한을 훌쩍 넘어가게 됩니다.

그렇다면 다른 방법을 생각해야 합니다.



동일하게 완전 탐색 풀이지만, **defaultdict**을 사용하면 시간 초과에서 자유로워질 수 있습니다.

```python
from collections import defaultdict

t = int(input())
for _ in range(t):
    n = int(input())
    li = sorted(list(map(int, input().split())))
    spotList = defaultdict(int)
    for i in range(len(li)):              # 모든 점을 defaultdict에 담기
        spotList[li[i]] = 1               # True를 의미함

    ans = 0
    for i in range(n - 1):
        for j in range(i + 1, n):
            first = li[i]
            second = li[j]
            third = li[j] + (li[j] - li[i]) # 임의의 세번 째 점
            if spotList[third] == 1:      # 임의의 세번 째 점이 존재하는지 확인
                ans += 1
    print(ans)
```

일단, defaultdict(int)을 하나 생성하여 모든 점을 담아줍니다.&#x20;

'점이 존재한다'는 의미로 defaultdict을 사용할 것이므로, 존재하는 점(key)의 값(value)은 모두 임의의 값 1로 넣어줍니다.

그 후에 이중 반복문을 통해 defaultdict에 담긴 두 점을 선택합니다.

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>



first와 second를 선택하고, 이 두 점 사이의 거리와 동일한 third를 임의로 설정합니다.

임의의 third가 만약 defaultdict에 존재한다면 동일한 거리의 세 점이 모두 존재한다는 의미가 됩니다.

위와 같은 경우에 ans의 값을 1씩 올리면서 반복문을 돌면, 최종 정답을 구할 수 있습니다.



처음에, 나쁜 예로 **combinations** 활용 코드를 보여드렸습니다.

문제를 보고 **3중 반복문** 혹은 **combinations**을 사용해야겠다는 아이디어가 떠올랐다면 잘하신겁니다.&#x20;

하지만 코드를 작성하기 이전에 시간 복잡도 계산이 우선시 되었다면, 해당 코드를 작성하며 시간을 낭비하는 일이 없었겠죠?



다시 한 번 강조하겠습니다.

1️⃣ **시간 복잡도 계산**

**2️⃣** 이를 기반으로 **완전탐색** vs. **그 외 알고리즘** 선택



### 풀어볼 문제

* [https://www.acmicpc.net/problem/1436](https://www.acmicpc.net/problem/1436)
* [https://www.acmicpc.net/problem/1895](https://www.acmicpc.net/problem/1895)

