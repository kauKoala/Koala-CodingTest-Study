---
description: 한 쪽에서는 삽입만, 다른 한 쪽에서는 삭제만 가능한 자료구조
---

# 큐

**큐(queue)**란 **FIFO**(First In First Out, 선입선출)의 특징을 가지는 자료구조입니다.

선입선출 즉, '먼저 들어온게 먼저 나간다'를 그림으로 그려봅시다.

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

스택과는 다르게 양 쪽이 모두 열려 있습니다.&#x20;

한 쪽에서만 삽입/삭제가 이루어졌던 스택과는 달리, 큐는 삽입과 삭제가 다른 쪽에서 일어납니다.

한 쪽으로만 들어올 수 있다는 것은 스택과 동일하지만, 다른 쪽으로 나가야 한다는 것이 스택과 차별화된 큐만의 특징입니다.&#x20;

그렇기 때문에 **선입선출**이 가능한 것이죠.



스택과 마찬가지로 리스트와 덱으로 구현이 가능합니다.

```python
li = []        
li.append(1)    # li == [1]
li.append(2)    # li == [1, 2]
li.pop(0)       # li == [2]
li.pop(0)       # li == []
```

스택처럼 **append(값)**과 **pop()** 함수를 모두 사용할 수 있습니다.

다만 스택과의 차이점인 **전단(front) 삭제**는 **pop(0)**를 사용하여 실행할 수 있습니다.

하지만 pop()과 달리 pop(0)은 인덱스를 지정해주는 만큼, 모든 원소를 전부 검색하는 **O(N)**의 시간 복잡도를 가집니다.

만약 pop(0) 때문에 문제를 시간 내에 풀 수 없다면, 바로 뒤에 나올 collections 모듈의 deque이 해결책이 될 수 있습니다.



## 연습문제

### BOJ 1966

{% embed url="https://www.acmicpc.net/problem/1966" %}

문제를 읽어보면, 전단(front)에서 원소를 삭제해야 하기 때문에, 큐를 사용해야 합니다.

하지만 삽입/삭제를 거치면서 원래 지정한 문서의 인덱스마저 바뀌게 됩니다.

때문에, 중요도를 담은 배열 이외에 **다른 배열**을 하나 더 만들어서, 지정한 문서의 위치를 동시에 저장하는 방식으로 하시면 됩니다.

```python
li = list(map(int, input().split()))
chk = [False for _ in range(n)]
chk[m] = True
```

위와 같이 중요도를 담은 배열 **li**와, 궁금한 문서의 위치를 저장해줄 배열 **chk**를 만들도록 합시다.

chk 배열의 원소를 모두 False로 만들되, 궁금한 문서는 True로 지정해줘야겠죠?



while문을 돌다가, 리스트의 0번 인덱스의 값이 최댓값이면서 처음 지정한 문서일 때 반복문을 종료해주시면 됩니다.

```python
t = int(input())
for i in range(t):
    n, m = map(int, input().split())
    li = list(map(int, input().split()))
    chk = [False for _ in range(n)]
    chk[m] = True
    cnt = 0
    while True:
        if li[0] == max(li):
            cnt += 1
            if chk[0] == True:
                print(cnt)
                break
            else:
                li.pop(0)
                chk.pop(0)
        else:
            li.append(li.pop(0))
            chk.append(chk.pop(0))
```









