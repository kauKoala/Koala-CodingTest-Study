---
description: 리스트에 순차적으로 접근해야 할 때 두 개의 점의 위치를 기록하면서 처리하는 알고리즘
---

# 투포인터

**투 포인터**도 이진 탐색과 마찬가지로, 시간 초과의 문제로 완전 탐색을 채택할 수 없을 때 사용합니다.

<figure><img src="../.gitbook/assets/image (16) (2).png" alt=""><figcaption></figcaption></figure>

위와 같은 배열이 있습니다. 우리는 연속된 원소의 합이 5인 부분 배열의 개수를 찾고 싶다고 가정합시다.

그렇다면 우리는 배열의 크기와 인덱스를 모두 바꿔가며 **완전 탐색**을 해야할까요? 이는 너무 비효율적입니다.

<figure><img src="../.gitbook/assets/image (3) (5).png" alt=""><figcaption></figcaption></figure>

효율성을 위해, 그리고 시간 초과를 방지하기 위해 우리는 **투 포인터** 기법을 사용할 수 있습니다.

해당 원소를 가리키는 두 개의 포인터를 두고, 조건에 맞게 이동시키는거죠.

합이 5임을 찾고 싶으니 '5보다 작을 땐 아래 쪽 포인터를 이동시키고, 5보다 클 땐 위 쪽 포인터를 이동시키기' 와 같은 규칙을 두면서 말이죠. 하지만 모든 문제가 그렇듯, 응용되면 조건식이 달라지므로 컨셉만 이해하시고 문제로 익히시는게 좋습니다.

완전 탐색으로는 O(N^2)의 시간 복잡도를 가지지만, 투 포인터를 사용하면 **O(N)**까지 줄일 수 있습니다.



문제를 풀어보며 익혀봅시다.



## 연습문제

### BOJ 2467

{% embed url="https://www.acmicpc.net/problem/2467" %}

두 포인터의 시작점이 왼쪽에 위치했던 위 설명에 반해, 이 문제의 두 포인터는 양 끝에 위치합니다.&#x20;

이 문제에서는 두 개의 포인터가 꼭 동일한 방향으로 이동하지 않아도 된다는 점을 캐치하는 것이 중요합니다.



배열에서 두 원소의 합의 절댓값이 가장 작은 쌍을 찾으면 되는 문제입니다.

다만 유의할 점은, 절댓값이 가장 작은 값이 꼭 (음수, 양수)의 쌍일 필요는 없습니다.

배열에 따라서 (음수, 음수) 혹은 (양수, 양수)도 정답이 될 수 있습니다.&#x20;



```python
left, right = 0, n - 1
minVal = abs(li[left] + li[right])
ans = [li[left], li[right]]
```

left와 right가 배열의 양 끝에서 시작하면, 두 원소의 합의 절댓값을 점점 줄여나갈 수 있습니다.

또한, 두 원소의 합의 절댓값을 저장할 minVal 변수와 정답이 될 두 원소의 배열을 초기화해줍시다.

계속해서 진행을 하다가 left와 right가 만날 때 탐색이 종료되어야 하기 때문에,

```python
left, right = 0, n - 1
minVal = abs(li[left] + li[right])
ans = [li[left], li[right]]

while left != right:
    # blah blah
```

위와 같은 while문을 작성할 수 있습니다.



이후에 left 포인터는 오른쪽으로, right 포인터는 왼쪽으로 향하면서 탐색을 하게 됩니다.

left 입장에서는 오른쪽으로 향할 수록 값이 커지고, right 입장에서는 왼쪽으로 향할수록 값이 작아집니다.

그렇기 때문에, 두 포인터가 가리키는 값의 합이 0에 가장 가까운 쌍을 골라주면 됩니다.



```python
n = int(input())
li = list(map(int, input().split()))
left, right = 0, n - 1
minVal = abs(li[left] + li[right])
ans = [li[left], li[right]]

while left != right:
    if minVal > abs(li[left] + li[right]):  # 최솟값 갱신 조건
        minVal = abs(li[left] + li[right])
        ans = [li[left], li[right]]

    if li[left] + li[right] >= 0:
        right -= 1
    elif li[left] + li[right] < 0:
        left += 1

print(*ans)
```

전체 코드입니다.

**li\[left] + li\[right] == 0**일 경우에 **break**를 하셔도 무방합니다.

두 가지의 경우를 소개해드렸지만, 다른 방식으로도 사용될 수 있으니 상황에 맞게 판단하셔서 설정하시면 됩니다.

