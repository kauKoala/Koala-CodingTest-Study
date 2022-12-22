---
description: 넓이 우선 탐색, 그래프에서 인접한 노드를 우선적으로 탐색하는 방법
---

# BFS

<figure><img src="../.gitbook/assets/bfs.gif" alt=""><figcaption></figcaption></figure>

로직은 아래와 같습니다.

* 동영상에서 보이듯 시작 노드를 방문하고 해당 노드에 연결되어 있는 노드들을 전부 방문합니다.
* 다음으로 그 노드들에서 위 BFS를 다시 진행합니다.



구현은 큐를 사용합니다.

```python
from collections import deque

def bfs(graph, start, visited):
    queue=deque([start])
    visited[start] = True
    while queue:
        v = queue.popleft()
        print(v, end=' ')
        for i in graph[v]:
            if not visited[i]:
                queue.append(i)
                visited[i] = True

graph = [
    [1,2], #0번 노드에서 1과 2로 이동 가능하다.
    [3, 4, 5], #1번 노드에서 2,3,8로 이동 가능하다.
    [6,7], #2번 노드에서 1,7로 이동 가능하다.
    [8],
    [3],
    [],
    [],
    [],
    []
]

visited = [False] * 9

bfs(graph, 0, visited) #출력 : 0 1 2 3 4 5 6 7 8 
```

{% embed url="https://www.acmicpc.net/problem/2644" %}

```python
from collections import deque

def bfs(node):
    queue = deque()
    queue.append(node)
    while queue:
        node = queue.popleft()
        for n in graph[node]:
            if check[n] == 0:
                check[n] = check[node]+1
                queue.append(n)
            
n = int(input())
graph = [[] for _ in range(n+1)]
s, e = map(int, input().split())
for _ in range(int(input())):
    u, v = map(int, input().split())
    graph[u].append(v)
    graph[v].append(u)
check = [0]*(n+1)
bfs(s)
print(check[e] if check[e] > 0 else -1)
```

floodfill 관련 로직 설명
