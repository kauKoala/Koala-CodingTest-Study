---
description: 그래프 내의 모든 정점들을 가장 적은 비용으로 연결하는 알고리즘
---

# 크루스칼 O

크루스칼을 이해하기 전에 일단 **MST**(**Minimum Spanning Tree)**라는 개념부터 이해해야 합니다.\


📌Spanning Tree(신장트리)란 ??\
![](<../.gitbook/assets/image (7).png>)

**그래프에서** \
****①**모든 정점을 포함하고 정점 간 서로 연결이 되며** \
****②**싸이클이 존재하지 않는(tree의 기본 조건) 부분그래프**\
**입니다.**

위에 그림에서도, a 연결그래프에서 만들어진 부분그래프 b 3개 모두 정점끼리 모두 하나로 연결되어 있고 사이클이 존재하지 않는 것을 볼 수 있죠?

📌Minimum Spanning Tree?\
이 중 MST는 이 그래프들 중 **가중치의 합이 최소가 되는 신장 트리**를 의미합니다.\
MST의 특징은 자연스럽게 정점이 N개라면 간선은 N-1개가 됩니다.

📌로직\
구하는 로직은 어렵지 않습니다. 위 특징을 이용하면 됩니다.

① 간선들을 가중치 순으로 오름차순 정렬하고 정점들을 각 컴포넌트로 초기화합니다.\
② 간선들을 훑으면서 양쪽 정점을 포함한 컴포넌트가 연결되어 있지 않으면(**사이클이 형성되지 않는다면**) 간선을 뽑고 연결합니다.\
③ 간선 V-1개가 뽑혔을 때, 그 간선들과 정점들이 이루는 그래프가 MST입니다.

'사이클이 형성되지 않는다면'의 구현은 앞에서 본 유니온파인드로 해결할 수 있겠죠?

그럼 다음 그래프로 크루스칼을 구현해봅시다. 아래 그래프는 노드가 총 5개니까 4개의 간선을 선택해내면 됩니다!

![](<../.gitbook/assets/image (21).png>)

일단 간선들 사이에서 가장 가중치가 작은 2 가중치의 간선을 선택합니다.

![](<../.gitbook/assets/image (24).png>)

다음으로 가중치가 작은 4를 선택하고,

![](<../.gitbook/assets/image (5) (5).png>)

그 다음으로 가중치가 작은 4를 선택하고 싶은데 아차차! 이렇게 하면 사이클이 만들어져서 안되겠죠?

![](<../.gitbook/assets/image (12).png>)X

그래서 다음으로 가중치가 작은 6인 간선을 또 하나 선택합니다.

![](<../.gitbook/assets/image (9).png>)

이제 지금까지 간선 3개를 선택했으니 남은 한 개만 선택하면 됩니다! 남은 간선들 중 가중치가 가장 작은 6을 선택하면 더 이상 사이클을 형성하는 일 없이 크루스칼 알고리즘이 완성됩니다!!

![](<../.gitbook/assets/image (22) (1).png>)

{% embed url="https://www.acmicpc.net/problem/1922" %}

크루스칼의 가장 대표적인 문제를 풀어봅시다.\
유니온파인드로 사이클이 이루어지는지 판단해나가면서 가장 가중치가 작은 간선들을 (노드-1)개의 갯수만큼 찾으면 됩니다.

```python
import sys
input = sys.stdin.readline

def find(a):
    if a == parent[a]: 
        return a
    parent[a] = find(parent[a])  
    return parent[a]

def union(a, b):
    a = find(a)
    b = find(b)
    # a , b의 루트노드를 찾아줌
    if b < a:
        parent[a] = b
    else:
        parent[b] = a

n = int(input())
m = int(input())
arr = []
parent = [i for i in range(n + 1)]
res = 0
for i in range(m):
    a, b, c = map(int, input().split())
    arr.append([c,a,b,])

arr.sort(key=lambda x: x[0])
for dis, a, b in arr:
    if find(a) != find(b):  # 루트가 같으면 할 필요가 없음
        union(a, b)
        res += dis
print(res)
```

\[참고] 아래는크루스칼 알고리즘을 구하는 전체적인 동영상입니다.

![](../.gitbook/assets/크루스칼.gif)

