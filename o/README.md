---
description: 연결되어 있는 객체 간의 관계를 표현하는 비선형 자료구조
---

# 그래프 O

그래프는 우리에게 매우 친근합니다. 고등학교 때 데이터를 정리해 놓을 때나, 마인드맵을 그려가면서 공부할 때, 모두 유용하게 사용하였는데요. 우리는 어떻게 컴퓨터에게 그래프의 개념을 설명해줄 수 있을지  알아봅시다.

먼저 그래프의 특징에 대해 알아봅시다.

![](<../.gitbook/assets/image (16).png>)정점(V)과 간선(E)으로 이루어진 "그래프"!

그래프는 정점과 간선으로 이루어져 있습니다. 위 그림에서 볼 수 있듯이,

* vertex는 정점 또는 노드라고 말하며, 여러 가지 특성을 가질 수 있는 객체를 의미합니다.
* edge는 간선 또는 link라고 말하며 정점들 간의 관계를 의미합니다.

그래프의 종류는 크게 두 개로 나뉩니다.

![](<../.gitbook/assets/image (2) (3).png>)차례대로유향 그래프, 무향 그래프이다.

그림으로 볼 수 있듯이 유향그래프는 방향이 존재하고, 무향그래프는 방향이 존재하지 않습니다.\
노드 간 이동 시 유향 그래프에서는 해당 방향으로만 이동 가능하고, 무향그래프에서는 자유롭게 이동할 수 있다는 특징이 있습니다.



이번에는그래프를 나타내는 두 가지 표현 방법을 알아봅시다.

📌인접행렬

인접행렬이란 이름 그대로 그래프의 연결 관계를 행렬로 표현하여 이차원 배열로 나타내는 방식을 의미합니다.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

위 무향그래프를 보면 노드0에서 노드3으로 이동할 수 있으므로 (0,3) 값을 1로 할당하였습니다. \
0에서 2처럼 이동할 수 없는 경우에는 0으로 할당합니다.

\
📌인접리스트

그래프의 한 꼭짓점에서 연결되어 있는 꼭짓점들을 하나의 연결 리스트로 표현하는 방식을 의미합니다.\
파이썬에서는 dictionary로 구현하거나 또는 이차원 배열에 append하는 방식으로 구현할 수 있습니다.

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

위 그래프에서 우리는 노드 0에서는 노드 1,2,3으로 갈 수 있음을 알 수 있습니다.\
인접리스트 방법은 인접 행렬 방법보다 공간적 측면에서 낭비가 없어 효율적입니다.

아래와 같이 표현 가능합니다.

```python
graph = { 0: [1,2,3], 
	  1: [0,2], 
          2: [0,1,3],
          3: [0,2] }
graph = [[1,2,3], [0,2], [0,1,3], [0,2]]
```
