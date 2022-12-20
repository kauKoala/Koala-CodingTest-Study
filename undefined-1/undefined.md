# 완전 탐색

모든 문제는 완전 탐색부터 고민 (랑이집사님)

그 후에 다른 방법을 생각하는 방향으로!



## 연습문제

###

###

### BOJ 13423

{% embed url="https://www.acmicpc.net/problem/13423" %}

간단히 말해서, 입력받은 N개의 점 중 간격이 동일한 세 개의 점의 **조합**이 총 몇 개인지 구하는 문제입니다.

가장 먼저 기초 스터디에서 다룬 itertools의 combinations를 생각해 볼 수 있습니다.

```python
from itertools import combinations as cb
input = __import__('sys').stdin.readline
t = int(input())
for _ in range(t):
    n = int(input())
    li = list(map(int, input().split()))
    li.sort()
    ans = 0
    for i in cb(li, 3):
        if abs(i[2] - i[1]) == abs(i[1] - i[0]):
            ans += 1
    print(ans)
```

하지만 점이 최대 1,000개이기 때문에, 이 방식으로 풀면 **시간 초과**를 받을 수 밖에 없습니다.

그렇다면 다른 방법을 생각해야 합니다.



동일하게 완전 탐색 풀이지만, **defaultdict**을 사용하면 시간 초과에서 자유로워질 수 있습니다.

```python
from collections import defaultdict
input = __import__('sys').stdin.readline
t = int(input())
for _ in range(t):
    n = int(input())
    li = sorted(list(map(int, input().split())))
    spotList = defaultdict(int)
    for i in range(len(li)):              # 모든 점을 defaultdict에 담기
        spotList[li[i]] = 1

    ans = 0
    for i in range(n-1):
        for j in range(i+1, n):
            first = li[i]
            second = li[j]
            third = li[j] + (li[j]-li[i]) # 임의의 세번 째 점
            if spotList[third] == 1:      # 임의의 세번 째 점이 존재하는지 확인
                ans += 1
    print(ans)
```

일단, defaultdict(int)을 하나 생성하여 모든 점을 담아줍니다.&#x20;

'점이 존재한다'는 의미로 defaultdict을 사용할 것이므로, 존재하는 점(key)의 값(value)은 모두 임의의 값 1로 넣어줍니다.

그 후에 이중 반복문을 통해 defaultdict에 담긴 두 점을 선택합니다.

first와 second를 선택하고, 이 두 점 사이의 거리와 동일한 third를 임의로 설정합니다.

임의의 third가 만약 defaultdict에 존재한다면 동일한 거리의 세 점이 모두 존재한다는 의미가 됩니다.

위와 같은 경우에 ans의 값을 1씩 올리면서 반복문을 돌리면, 최종 정답을 받을 수 있습니다.



















