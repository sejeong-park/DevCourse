# Tree

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

```python
class Node :
    def __init__(self, item) :
        self.data = item
        self.left = None
        self.right = None

    def size(self) :
        l = self.left.size() if self.left else 0
        r = self.right.size() if self.right else 0
        return l + r + 1

    def depth(self) :
        l = self.left.depth() if self.left else 0
        r = self.right.size() if self.right else 0
        return max(l, r) + 1
```
```python
class BinaryTree :
    def __init__(self, r) :
        self.root = r

    def size(self) :
        if self.root : 
            return self.root.size()
        else :
            return 0

    def depth(self) :
        if self.root : 
            return self.root.depth()
        else:
            return 0

```


## 이진 트리의 순회
### 깊이 우선 순회

(1) 중위 순회

* 순회의 순서 : Left -> 자기자신 -> Right

```python
class Node :
    def inorder(self) :
        traversal = []
        if self.left :
            traversal += self.left.inorder()
        traversal.append(self.data)
        if self.right : 
            traversal += self.right.inorder()
        return traversal
```

(2) 전위 순회

* 순회의 순서 : 자기 자신 -> Left -> Right

```python
class Node :
    def preorder(self) :
        traversal = []
        traversal.append(self.data)
        if self.left :
            traversal += self.left.preorder()
        if self.right :
            traversal += self.right.preorder()
        return traversal
```

(3) 후위 순회

* 순회의 순서 : Left -> Right -> 자기 자신


```python
class Node :
    def postorder(self) :
        traversal = []
        if self.left :
            traversal += self.left.preorder()
        if self.right :
            traversal += self.right.preorder()
        traversal.append(self.data)
        return traversal
```

## 넓이 우선 순회 (BFS)

* 원칙
    * 수준(level)이 낮은 노드를 우선으로 방문
    * 같은 수준의 노드들 사이에는
        * 부모 노드의 방문 순서에 따라 방문
        * 왼쪽 자식 노드를 오른쪽 자식보다 먼저 방문

    * 재귀적 방법이 적합한가?
        * 적합하지 않다!!

* 한 노드를 방문했을 때
    * 나중에 방문할 노드들을 순서대로 기록해두어야 한다
    * 큐(Queue)를 이용하자!

### 넓이 우선 순회 알고리즘 궇현
(1) (초기화) traversal : 빈 리스트, q : 빈 큐
(2) 빈 트리가 아니면, root node를 큐에 추가 (enqueue)
(3) q가 비어있지 않은 동안
    * node <- queue에서 원소 추출 (dequeue)
    * node를 방문
    * node의 왼쪽, 오른쪽 자식 (있으면) 들을 queue에 추가
(4) queue가 빈 큐가 되면 모든 노드 방문 완료

```python
class BinaryTree :
    
    def __init__(self, r) :
        self.root = r

    def bft(self) :
        
        queue = ArrayQueue()
        traversal = []

        # root가 존재할 때
        if self.root :
            
            queue.enqueue(self.root) 

            while not queue.isEmpty() :
                node = queue.deque()
                if node.left :
                    queue.enqueue(node.left)
                if node.right :
                    queue.enqueue(node.right)
                traversal.append(node.data)
            
        return traversal
```

