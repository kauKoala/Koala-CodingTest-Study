---
description: 깊이 우선 탐색, 그래프에서 깊은 부분을 우선적으로 탐색하는 알고리즘
---

# DFS X

<figure><img src="../.gitbook/assets/dfs.gif" alt=""><figcaption></figcaption></figure>

로직은 아래와 같습니다.

* 그림에서 보이듯 시작 노드를 방문하고 연결된 다음 노드에 방문, 그 다음 연결된 노드에 방문...
* 그러다 (연결이 안되어 있으면) or (모두 방문한 노드라면) 이전 노드로 이동 후 연결된 노드(방문이 안된 노드)에 대해 다시 DFS를 수행합니다.
*

재귀함수 사용



