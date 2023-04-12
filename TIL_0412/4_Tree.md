## Tree

* 정점과 간선을 이용하여 데이터의 배치 형태를 추상화한 자료 구조

트리의 높이 (depth)
* 트리의 높이(height) = 최대 수준 (level) + 1
* 서브트리
* 노드의 차수 = 자식(서브트리)의 수
* degree가 0 인 노드 -> 마지막 자식노드(leaf node)

### 이진 트리 (Binary Tree)
* 모든 노드의 차수가 **2이하**인 트리
* 재귀적으로 정의할 수 있다.
    * 루트 노드 + 왼쪽 서브트리 + 오른쪽 서브트리
        * empty Tree도 이진트리이다.

### 포화 이진 트리 (Full Binary Tree)
* 모든 레벨에서 노드들이 모두 채워져 있는 이진트리
* 높이가 k이고 노드의 개수가 2^k-1 인 이진 트리

### 완전 이진 트리 (Complete Binary Tree)
* 높이 k 인 완전 이진 트리
* 레벨 k-2까지는 모든 노드가 2개의 자식을 가진 포화 이진 트리
* 레벨 k-1에서는 왼쪽부터 노드가 순차적으로 채워져 있는 이진 트리

## 이진 트리의 추상적 자료구조

연산의 정의
* size() - 현재 트리에 포함되어 있는 노드의 수를 구함
* depth() - 현재 트리의 깊이(또는 높이 ; height) 를 구함
* 순회 (traversal)

* Node
    * Data
    * Left Child
    * Right Child

```python
class Node :
    def __init__(self, item) :
        self.data = item
        self.left = None
        self.right = None
```

## 이진트리의 구현

### 이진트리의 구현 - size()

```python
class BinaryTree :
    def __init__(self, r) :
        self.root = r        
```

* 재귀적인 방법으로 쉽게 구할 수 있다.
    * 전체 이진 트리의 size() = left subtree의 size()  + right subtree의 size() + 1(자기 자신)

```python
class Node :
    def size(self) :
        left = self.left.size() if self.left else 0
        right = self.right.size() if self.right else 0

        return left + right + 1
```

```python
class BinaryTree : 
    def size(self) :
        if self.root :
            return self.root.size()
        else :
            return 0
```
### 이진 트리의 구현

* 전체 이진 트리의 depth() = left subtree의 depth()와 right subtree의 depth() 중 더 큰 것 + 1

~~~~연습문제~~~~


## 이진 트리의 순회
### 깊이 우선 순회
* 중위 순회
* 전위 순회
* 후위 순회

### 넓이 우선 순회