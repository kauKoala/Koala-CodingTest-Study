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
#가장 거리가 가까운 것부터 먼 것으로 순서대로 점차 탐색함
#큐를 이용
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
    [3, 4, 5], #1번 노드에 연결된 건 2,3,8 이다.
    [6,7], #2번 노드에 연결된 건 1,7이다.
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



\+위상정렬도 소개
