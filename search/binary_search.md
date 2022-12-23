# 이진 탐색

**이진 탐색(binary search)**을 **** 사전에서는 "검색 범위를 줄여 나가면서 원하는 데이터를 검색하는 알고리즘"이라고 정의하고 있습니다. 하지만 사전적 의미는 잘 와닿지 않으니, 한 가지 예시를 들어보겠습니다.

```python
import random
num = random.randrange(1, 101)
# num == 25 이라고 가정하겠습니다.
```

위는 1부터 100까지의 자연수 중 하나를 랜덤하게 생성하는 코드입니다.

그렇다면 우리는 이 num을 맞추는데 몇 번의 시도를 해야할까요?

**완전 탐색**을 기억해보면, 우리는 최악의 경우 100번의 시도를 해야합니다. 그렇기 때문에 시간 복잡도는 **O(N)**이죠.

하지만 이 고정된 num 값과 우리가 시도한 숫자의 대소 관계를 파악할 수 있다면 더 빠르게 num 값을 알아낼 수 있습니다. 업다운 게임을 생각하시면 됩니다.

50을 시도했을 때, num이 50보다 작다는 사실을 알 수 있다면 우리는 51부터 100까지의 수는 정답의 범위에서 배제됩니다.

이처럼, 평균적으로 약 절반씩 경우의 수가 줄어들기 때문에, 시간 복잡도는 **O(logN)**이라고 할 수 있습니다. 리스트의 정렬이 필요하다면, **O(NlogN)**의 시간 복잡도를 가집니다.



```python
num = 25
left = 1
right = 100
while left <= right:
    mid = (left + right) // 2

    if mid == num:
        break
    elif mid < num:
        left = mid + 1
    elif mid > num:
        right = mid - 1
```

이게 **이진 탐색**의 기본적인 틀입니다.&#x20;

처음 수의 범위를 **left \~ right**로 설정하고, 조건에 맞게 범위를 좁혀가는 방식으로 진행됩니다.

그러다 **left**가 **right**를 넘어설 경우에 반복문은 종료됩니다.





## 연습문제

### BOJ 13423

{% embed url="https://www.acmicpc.net/problem/13423" %}

바로 이전의 완전 탐색 파트에서 다뤘던 문제입니다.

완전 탐색으로도 가능하지만, **이진 탐색** 또한 풀이가 가능한 문제입니다.

참고로 해당 풀이는 pypy3에만 적용됨을 참고해주시기 바랍니다.

```python
t = int(input())
for _ in range(t):
    n = int(input())
    li = sorted(list(map(int, input().split())))
    ans = 0
    for i in range(n - 1):
        for j in range(i + 1, n):   # 중복되는 인덱스가 없도록 i+1부터 시작
            left = i
            right = j
            val = (li[left] + li[right]) / 2    # 원하는 값
            while left <= right:
                mid = (left + right) // 2
                if val == li[mid]:
                    ans += 1
                    break
                elif val > li[mid]:
                    left = mid + 1
                elif val < li[mid]:
                    right = mid - 1
    print(ans)
```

이전에 해당 문제를 **완전 탐색**으로 접근할 때의 컨셉을 그대로 따라해봅시다.

일단 마찬가지로 두 점을 반복문을 통해 고릅니다. **완전 탐색**에서는 첫 번째, 두 번째 점을 골랐으니 이번엔 첫 번째와 세 번째 점을 골라보도록 합시다.&#x20;

각 점의 인덱스를 left, right로 지정하고, 우리가 원하는 중앙 값(val)이 리스트에 있는지만 확인해주면 됩니다.



같은 문제를 여러 방식으로 푸는 것도 많은 도움이 되니, 꼭 풀어보시길 바랍니다.



### 풀어볼 문제

* [https://www.acmicpc.net/problem/16401](https://www.acmicpc.net/problem/16401)
* [https://www.acmicpc.net/problem/17951](https://www.acmicpc.net/problem/17951)&#x20;

(cf. 17951 문제처럼 정렬을 하지 않아야하는 **이진 탐색** 문제도 있습니다!)

