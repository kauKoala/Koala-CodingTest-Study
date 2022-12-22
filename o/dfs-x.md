---
description: 깊이 우선 탐색, 그래프에서 깊은 부분을 우선적으로 탐색하는 알고리즘
---

# DFS X

<figure><img src="../.gitbook/assets/dfs.gif" alt=""><figcaption></figcaption></figure>

로직은 아래와 같습니다.

* 동영상에서 보이듯 시작 노드를 방문하고 해당 노드에 연결된 다음 노드에 방문, 그 다음 연결된 노드에 방문을 반복합니다.
* 그러다 (연결이 안되어 있으면) or (모두 방문한 노드라면) 이전 노드로 이동 후 연결된 노드(방문이 안된 노드)에 대해 다시 DFS를 수행합니다.



구현은 재귀함수를 사용합니다. 이 때 방문처리를 위한 visited 배열을 주의합시다.

```python
#DFS 메소드 정의
def dfs(graph, v, visited):
    #현재 노드를 방문처리
    visited[v] = True
    print(v, end=' ')
    #현재 노드와 연결된 다른 노드를 재귀적으로 방문
    for i in graph[v]:
        if not visited[i]:
            dfs(graph, i, visited)

#각 노드가 연결된 정보를 표현 (2차원 리스트)
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

#각 노드가 방문된 정보를 표현 (1차원 리스트)
visited = [False] * 9 

dfs(graph, 0, visited)   #출력 : 0 1 3 8 4 5 2 6 7

```





