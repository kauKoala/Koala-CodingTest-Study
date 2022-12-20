# 덱

**덱(deque)**은 double-ended queue의 줄임말로서, **큐(queue)**의 전단(front)과 후단(rear)에서 모두 삽입과 삭제가 가능한 큐를 의미합니다. 큐에서 발전된 자료구조라고 봐도 좋으며, 데크라고 불리기도 합니다.

```python
from collections import deque
dq = deque()
```

덱은 collections에서 불러와 사용할 수 있으며, 위와 같은 형태로 빈 덱을 선언합니다.

그렇다면 큐와는 다른 덱의 특징으로는 무엇이 있을까요?



**1️⃣ 전단(front)에 삽입이 가능하다**

덱의 정의에서 언급했듯이, 전단에서는 삭제만 가능한 큐와 달리 덱은 삽입도 가능합니다.

```python
from collections import deque
dq = deque([1, 2, 3])
dq.appendleft(0)
print(dq[0])  # 0 출력
```

**appendleft**를 사용하여 전단에 삽입할 수 있습니다.



2️⃣ **전단(front)의 원소를 삭제할 땐, pop(0)이 아닌 popleft() 사용**

모듈을 불러와 사용하다보니, 기존 리스트를 통해 구현하던 pop과는 함수의 차이가 존재합니다.

```python
from collections import deque
q = [1, 2, 3]
q.pop(0) # 1 
dq = deque([1, 2, 3])
dq.pop(0) # TypeError: deque.pop() takes no arguments (1 given)
```

큐와 동일하게 **pop(0)**을 사용하여 원소를 삭제하려고 하면 pop() 안에는 argument가 들어갈 수 없다는 error를 맞게 됩니다.

나아가서, 특정 인덱스의 원소를 삭제하는 **pop(n)**의 방식도 덱에서는 사용할 수 없겠죠?

이처럼, 덱만의 적절한 함수를 잘 찾아서 사용하셔야 합니다.

아래에 덱의 기본적인 함수 4개(append(), appendleft(), pop(), popleft())를 첨부합니다.

```python
from collections import deque
dq = deque([1, 2, 3])
dq.append(4)     # deque([1, 2, 3, 4])
dq.appendleft(0) # deque([0, 1, 2, 3, 4])
dq.pop()         # deque([0, 1, 2, 3])
dq.popleft()     # deque([1, 2, 3])
```



**3️⃣ 연산 속도가 빠르다**

덱의 가장 큰 장점이자, 큐 대신 덱을 쓰는 가장 큰 이유인데요.

큐로는 시간 초과가 나지만, 덱으로는 통과할 수 있는 문제가 가끔 존재합니다.



## 연습문제

### BOJ 5397

{% embed url="https://www.acmicpc.net/problem/5397" %}
