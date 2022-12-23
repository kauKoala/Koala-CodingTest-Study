# 스택

**스택(stack)**이란 **LIFO**(Last In First Out, 후입선출)의 특징을 가지는 자료구조입니다.

후입선출 즉, '나중에 들어온게 먼저 나간다'를 그림으로 그려봅시다.

<figure><img src="../.gitbook/assets/image (15) (1).png" alt=""><figcaption></figcaption></figure>

1, 2, 3을 순서대로 넣은 후, 1을 빼내고 싶을 땐 어떻게 해야할까요?

어쩔 수 없이 3과 2를 차례로 뺀 후에야 1을 빼낼 수 있습니다.&#x20;

이것이 바로 스택입니다. 가장 나중에 들어온 3이 가장 먼저 나가는 후입선출의 구조죠.

나갈 구멍이 한 쪽밖에 없다고 생각하시면 편합니다. 리스트에서는 마지막 인덱스에 해당합니다.



스택은 리스트로 구현할 수 있고, 상황에 따라서는 뒤에서 배울 덱(deque)으로 구현하기도 합니다.

리스트를 사용할 경우, 내장 함수를 사용하여 쉽게 삽입/삭제 등의 연산을 할 수 있습니다.

```python
li = []
li.append(1)    # li == [1]
li.append(2)    # li == [1, 2]
li.pop()        # li == [1]
li.pop()        # li == []
```

**append(값)**은 원소 삽입시에, **pop()**은 삭제시에 사용하는 함수입니다.

이 두 함수를 사용하여 바로 문제를 풀어보도록 합시다.



## 연습문제

### BOJ 1874

{% embed url="https://www.acmicpc.net/problem/1874" %}

처음에 배열에 들어갈 원소를 하나씩 입력받게 됩니다. 하지만 모든 원소를 배열에 미리 넣어두는 방식 말고 하나씩 넣을지 말지 판단하는 방식으로 진행해보도록 하겠습니다.

```python
li = []      
ans = []    # '+', '-'를 담을 배열
cnt = 0
flag = True # 불가능한 경우를 위한 flag
```

li 배열을 사용하여 문제의 과정을 진행하고, ans 배열은 삽입/삭제의 여부에 따라 '+', '-'를 넣어줄 용도로 사용합니다.

입력받은 수열을 만들어 낼 수 없을 때 flag를 통해 예외처리를 해줄 예정입니다.



```python
n = int(input())
li = []     
ans = []    
cnt = 0
flag = True
for _ in range(n):
    val = int(input())

    while cnt < val:
        cnt += 1
        li.append(cnt)
        ans.append('+')
    if li[-1] == val:
        li.pop()
        ans.append('-')
    else:
        flag = False
        break

if flag == True:
    print('\n'.join(ans))
else:
    print('NO')
```

cnt 변수는 append() 할지 말지를 결정하는 지표가 됩니다.

입력값이 나올 때까지 수를 삽입하다가, 그 수가 나오면 삭제하는 과정을 반복하면 됩니다.

