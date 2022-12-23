---
description: 깊이 우선 탐색, 그래프에서 깊은 부분을 우선적으로 탐색하는 알고리즘
---

# DFS O

<figure><img src="../.gitbook/assets/dfs.gif" alt=""><figcaption></figcaption></figure>

로직은 아래와 같습니다.

* 동영상에서 보이듯 시작 노드를 방문하고 해당 노드에 연결된 다음 노드에 방문, 그 다음 연결된 노드에 방문을 반복합니다.
* 그러다 (연결이 안되어 있으면) or (모두 방문한 노드라면) 이전 노드로 이동 후 연결된 노드(방문이 안된 노드)에 대해 다시 DFS를 수행합니다.



구현은 재귀함수를 사용합니다. 이 때 방문처리를 위한 visited 배열을 주의합시다.\
앞에 트리 순환에서 봤던 재귀 방식을 사용하여 노드를 불러오는 로직을 이해하며 다음 코드를 봅시다.

for문에서 노드를 재귀함수로 넘기고, 또 다시 해당 노드에서 이어지는 다른 노드들을 재귀함수로 넘기는 과정에서 자연스럽게 DFS가 구현됨을 알 수 있습니다.

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

다음 문제를 함께 봅시다!

{% embed url="https://www.acmicpc.net/problem/13023" %}

이 문제는 의도 이해가 조금 어려울 수 있는데, 쉽게 말해 친구관계 그래프의 깊이가 5가 될 수 있는지를 증명하면 됩니다.

dfs에서 들어갔다가 다시 나오는 로직이므로 방문표시를 풀어주는 것에 유의합시다.\
이는 백트래킹 문제에서 봤던 로직과 같습니다.

```python
N,M=map(int,input().split())
arr=[[] for _ in range(N)]
for _ in range(M):
    a,b=map(int,input().split())
    arr[a].append(b)
    arr[b].append(a)

def dfs(index,num):
    if num==4: print(1); exit();
    for i in arr[index]:
        if not visited[i]:
            visited[i]=1
            dfs(i,num+1)
            visited[i]=0
visited=[0]*N
for i in range(N):
    #방문표시
    visited[i]=1
    dfs(i,0)
    #방문표시 해제
    visited[i]=0
print(0)
```



