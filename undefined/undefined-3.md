# 우선순위 큐

python은 최소힙이 default (C++은 최대힙)



## 연습문제

### BOJ 1927

{% embed url="https://www.acmicpc.net/problem/1927" %}

```python
from heapq import heappush, heappop
input = __import__('sys').stdin.readline
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
input = __import__('sys').stdin.readline
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
input = __import__('sys').stdin.readline
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
input = __import__('sys').stdin.readline
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

