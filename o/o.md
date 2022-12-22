---
description: 노드들이 나무 가지처럼 연결된 비선형 계층적 자료구조
---

# 트리 O

![](<../.gitbook/assets/image (15).png>)왼쪽 그림이 바로 TREE 입니다.

트리의 가장 큰 특징 두 가지는 다음과 같습니다.&#x20;

① 연결 그래프입니다. (컴포넌트가 하나이다.)\
② 방향을 무시하였을 때, 싸이클(특정 정점에서 시작해 어떠한 경로를 지나 다시 그 정점으로 돌아오는 경로)이 존재하지 않습니다.

엇? 이거 그래프 아닙니까??\
네 맞습니다! 트리는 그래프의 하위 개념입니다.





📌트리의 개념

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

* 트리의 루트 노드(root)는 트리의 가장 위에 있는 노드를 말합니다. 따라서 'A'입니다.
* 노드 'D'의 부모 노드 (parent)는 해당 노드를 가리키는 상위 level 노드를 말한다. 따라서 'B'입니다.
* 노드 'D'의 자식 노드 (child)는 해당 노드가 가리키는 하위 level 노드들을 말한다. 따라서 'H'와 'I'입니다.
* 트리의 높이는 root 노드부터 한 level씩 count 해주면 됩니다. 따라서 이 트리의 depth는 '4'입니다.
* 노드 'D'는 level 3에 위치합니다.
* 말단 노드 (leaf node)는 자식 노드를 가지고 있지 않은 노드를 의미합니다. 따라서 'F', 'G', 'H', 'I'입니다.



📌트리를 탐색하는 방법

트리의 순회 중 중위(inorder) 순회, 전위(preorder) 순회, 후위 순회(postorder) 순회에 대해 알아봅시다.&#x20;

{% embed url="https://www.acmicpc.net/problem/1991" %}

* **전위 순회(preorder traverse) : 뿌리(root)를 먼저 방문**
* **중위 순회(inorder traverse) : 왼쪽 하위 트리를 방문 후 뿌리(root)를 방문**
* **후위 순회(postorder traverse) : 하위 트리 모두 방문 후 뿌리(root)를 방문**

<figure><img src="../.gitbook/assets/image (2) (4).png" alt=""><figcaption></figcaption></figure>

* 전위 순회 : 0->1->3->7->8->4->9->10->2->5->11->6
* 중위 순회 : 7->3->8->1->9->4->10->0->11->5->2->6
* 후위 순회 : 7->8->3->9->10->4->1->11->5->6->2->0

트리순회는 재귀함수로 구현할 수 있는데요, \
아래 코드에서 어디를 먼저 방문하느냐에 따라 함수 형태가 달라지는 것을 확인해보세요.

```python
import sys
 
N = int(sys.stdin.readline().strip())
tree = {}
 
for n in range(N):
    root, left, right = sys.stdin.readline().strip().split()
    tree[root] = [left, right]
 
 
def preorder(root):
    if root != '.':
        print(root, end='')  # root
        preorder(tree[root][0])  # left
        preorder(tree[root][1])  # right
 
 
def inorder(root):
    if root != '.':
        inorder(tree[root][0])  # left
        print(root, end='')  # root
        inorder(tree[root][1])  # right
 
 
def postorder(root):
    if root != '.':
        postorder(tree[root][0])  # left
        postorder(tree[root][1])  # right
        print(root, end='')  # root
 
 
preorder('A')
print()
inorder('A')
print()
postorder('A')
```



📌이진 탐색 트리(BST, Binary Search Tree)\
트리의 가장 대표적인 유형 중 하나인 이진 탐색트리에 대해 추가로 알아봅시다.

![](<../.gitbook/assets/image (5) (2).png>)

이진 트리 (binary tree)는 알다시피  각노드가 최대 두 개의 자식 노드를 가지는 트리 자료 구조 로, 자식 노드를 각각 왼쪽 자식 노드 와 오른쪽 자식 노드로 가지고 있습니다.

BST는 이진트리의 성질을 가지면서 다음과 같은 특징이 있습니다.

① 왼쪽 자식이 있다면, 왼쪽 자식의 key 값보다 자신의 key 값이 커야 한다.\
② 오른쪽 자식이 있다면, 오른쪽 자식의 key 값보다 자신의 key 값이 작아야 한다.

이러한 특징 덕택에 우리는 위 BST에서 67이라는 숫자를 찾을 때 단 4번의 접근만으로 67을 찾을 수 있다는 장점이 있습니다. 따라서 이진탐색 트리는 탐색 시간복잡도가 O(log N)에 해당합니다. (두 갈래로 나눠지며 탐색하므로log 밑은 2입니다.)



사실 BST에 가해지는 중요한 연산은 2개 더 있습니다. 삽입(insertion)과 삭제(deletion). 두 연산 역시 평균 시간 복잡도 O(logN)을 갖게 됩니다.



<figure><img src="../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

* 삽입과정

삽입과정은 이러합니다. 루트에서 시작하고, 삽입하려는 key값 K가 있을 때, 현재 정점의 key보다 K가 작으면 왼쪽 서브트리에 삽입해야 합니다. 만약 현재 정점의 왼쪽 자식이 없다면 key가 K인 새 노드를 만들어 현재 정점의 왼쪽 자식으로 만들고 연산을 종료하고, 자식이 또 있다면 위 연산을 반복합니다.

반대로 현재 정점의 key보다 K가 크면 오른쪽 서브트리에 대해 위와 같은 연산을 합니다.

* 삭제과정

삭제과정이 조금 까다로운데요, 경우가 세 가지로 나뉩니다.

\
1\. 지워야 할 노드가 리프 노드일 때\
그냥 똑 떼어주면 됩니다.

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

2\. 지워야 할 노드가 자식이 하나만 있을 때\
자신을 떼어내고 자식을 그 자리로 갖다 놓으면 됩니다.

<figure><img src="../.gitbook/assets/image (4) (2).png" alt=""><figcaption></figcaption></figure>

3\. 지워야 할 노드가 자식이 2개일 때\
이 경우가 가장 까다로운데요, 해당 노드 왼쪽에 있는 노드들 중 가장 큰 leaf노드 가져오거나 / 해당 노드 오른쪽에 있는 노드들 중 가장 작은 leaf노드를 가져오면 됩니다.

<figure><img src="../.gitbook/assets/image (1) (2).png" alt=""><figcaption></figcaption></figure>

이렇게 BST의 검색, 삽입, 삭제에 대해 알아보았는데요.\
이번에는BST의 특징을 이용하여 다음 5639 문제를 풀어봅시다.\
앞에서 배운 전위 후위 순회를 활용하여 푸시면 됩니다.

{% embed url="https://www.acmicpc.net/problem/5639" %}

```python
import sys
sys.setrecursionlimit(10**6)
num_list = []
while True:
    try:
        num = int(input())
        num_list.append(num)
    except:
        break

def postorder(first,end):
    if first > end:
        return
    mid = end+1   # 루트보다 큰 값이 존재하지 않을 경우를 대비   
    for i in range(first+1,end+1):
        if num_list[first] < num_list[i]:
            mid = i
            break
    
    postorder(first+1, mid-1)
    postorder(mid, end)
    print(num_list[first])

postorder(0,len(num_list)-1)
```
