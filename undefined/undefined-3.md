# 우선순위 큐

**우선순위 큐(priority queue)**란 **FIFO**의 특징을 가진 **큐(queue)**에 **우선순위** 방식을 접목시킨 자료구조입니다.

즉, 먼저 들어온 원소가 아닌 **우선순위가 높은 원소가 먼저 나가는** 특징을 가집니다.

우선순위 큐는 힙(heap)이라는 자료구조를 통해 구현할 수 있습니다.

그렇다면 힙은 무엇일까요?



**힙(heap)**이란 우선순위 큐를 위해 고안된 **완전 이진트리** 형태의 자료구조입니다. 트리에 대해 모르신다면, 뒤쪽의 트리 파트를 먼저 보시고 오시길 바랍니다.

힙의 종류에는

**1️⃣ 최대 힙**: 부모 노드의 키 값이 자식 노드보다 크거나 같은 완전 이진트리

**2️⃣ 최소 힙**: 부모 노드의 키 값이 자식 노드보다 작거나 같은 완전 이진트리

가 있습니다.



**최대 힙**이 default인 C++과는 다르게, **python**에서 heap은 **최소 힙**이 default입니다.&#x20;

이는 뒤의 연습문제에서 다시 한 번 확인해보도록 하겠습니다.



**힙**은 앞서 배웠던 덱과는 다르게 모듈에서 자료구조 자체를 제공해주진 않습니다.

하지만 리스트를 힙처럼 사용할 수 있도록, 모듈에서 여러가지 함수를 제공합니다.

```python
from heapq import heappush, heappop
```

대표적으로 **heappush()**와 **heappop()** 함수가 있습니다.

이름 그대로 **heappush()**는 원소 삽입시에, **heappop()**은 원소 삭제시에 사용하게 됩니다.

자세한 사용법은 아래의 예시와 함께 설명하겠습니다.



```python
from heapq import heappush
hq = []
heappush(hq, 4) # hq == [4]
heappush(hq, 2) # hq == [2, 4]
heappush(hq, 3) # hq == [2, 4, 3]
heappush(hq, 1) # hq == [1, 2, 3, 4]
```

위처럼 **heappush(리스트명, 값)**의 방식으로 사용할 수 있습니다.

원소가 삽입되기만 하는게 아니라, **최소 힙**으로 새롭게 정렬되는 모습을 주석을 통해 확인할 수 있습니다.



```python
from heapq import heappop
hq = [1, 2, 3, 4]
print(heappop(hq)) # 1 출력
print(hq)          # [2, 4, 3] 출력
```

삭제는 **heappop(리스트명)**의 방식으로 사용하면 됩니다.

**heappop()**은 실행 시에 부모 노드의 값이 삭제되고, 그 값을 반환하게 됩니다.

heappush와 마찬가지로 **최소 힙**으로 새롭게 정렬된 모습을 확인해볼 수 있습니다.



그렇다면 빈 리스트에 값을 하나씩 넣는(heappush) 작업 대신, **이미 원소가 정해진 리스트**를 힙으로 바꿀 순 없을까요?

```python
from heapq import heapify
hq = [4, 2, 3, 1]
heapify(hq)
print(hq)   # [1, 2, 3, 4] 출력
```

**heapify()**를 사용하면 위와 같이, 리스트 내부의 원소들이 힙 구조에 맞게 재배치됩니다.&#x20;

하지만 원본 리스트가 변경되므로, 기존의 형태가 필요한 경우에는 미리 복제를 해두어야 한다는 점을 유념하시길 바랍니다.



## 연습문제

### BOJ 1927

{% embed url="https://www.acmicpc.net/problem/1927" %}

```python
from heapq import heappush, heappop

n = int(input())
hq = []
for _ in range(n):
    val = int(input())
    if val != 0:
        heappush(hq, val)
        continue
    if not hq:
        print(0)
    else:
        print(heappop(hq))
```





### BOJ 11279

{% embed url="https://www.acmicpc.net/problem/11279" %}

```python
from heapq import heappush, heappop

n = int(input())
hq = []
for _ in range(n):
    val = int(input())
    if val != 0:
        heappush(hq, -val)
        continue
    if not hq:
        print(0)
    else:
        print(-heappop(hq))
```





```python
from heapq import heappush, heappop

n = int(input())
hq = []
for _ in range(n):
    val = int(input())
    if val != 0:
        heappush(hq, (-val, val))
        continue
    if not hq:
        print(0)
    else:
        print(heappop(hq)[1])
```

###

### BOJ11286

{% embed url="https://www.acmicpc.net/problem/11286" %}

```python
from heapq import heappush, heappop

n = int(input())
hq = []
for _ in range(n):
    val = int(input())
    if val != 0:
        heappush(hq, (abs(val), val))
        continue
    if not hq:
        print(0)
    else:
        print(heappop(hq)[1])
```

