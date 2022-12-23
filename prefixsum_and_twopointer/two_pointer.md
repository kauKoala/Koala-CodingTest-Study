# 투포인터

**투 포인터**도 이진 탐색과 마찬가지로, 시간 초과의 문제로 완전 탐색을 채택할 수 없을 때 사용합니다.

길이가 N인 배열에서&#x20;

## 연습문제

###

###

###

###

### BOJ 2467

{% embed url="https://www.acmicpc.net/problem/2467" %}

첫 번째 문제보다는 확실히 까다로운 문제입니다.

이 문제에서는 두 개의 포인터가 꼭 동일한 방향으로 이동하지 않아도 된다는 점을 캐치하는 것이 중요합니다.



배열에서 두 원소의 합의 절댓값이 가장 작은 쌍을 찾으면 되는 문제입니다.

다만 유의할 점은, 절댓값이 가장 작은 값이 꼭 (음수, 양수)의 쌍일 필요는 없습니다.

배열에 따라서 (음수, 음수) 혹은 (양수, 양수)가 정답이 될 수 있습니다.&#x20;



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

