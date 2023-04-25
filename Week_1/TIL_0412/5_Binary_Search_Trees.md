## 이진 탐색 트리

모든 노드에 대해서
* 왼쪽 서브트리에 있는 데이터는 모두 현재 노드의 값보다 작고
* 오른쪽 서브트리에 있는 데이터는 모두 현재 노드의 값보다 큰
성질을 만족하는 이진트리

* 이진 탐색 트리는 데이터 검색에 유리하다
    * 배열을 이용한 이진탐색과 비슷하다!

### 이진탐색과 이진탐색트리를 비교해 볼까?
(장점) : 이진탐색트리는 트리의 구조를 띄고 있으므로, 데이터 원소의 추가와 삭제가 용이하다.
(단점) : 이진탐색트리는 공간 소요가 크다. -> 항상 `O(logn)`의 탐색 복잡도 ? (항상은 아님)

### 이진 탐색 트리의 추상적 자료 구조
* 데이터 표현 - 각 노드는 (key, value)의 쌍으로
    * 키를 이용해서 검색 가능
    * 보다 복잡한 데이터 레코드로 확장 가능

* 연산의 정의
    * insert(key, data) - 트리에 주어진 데이터 원소를 추가
    * remove(key) - 특정 원소를 트리로부터 삭제
    * lookup(key) - 특정 원소를 검색
    * inorder() - 키의 순서대로 데이터 원소를 나열



### 코드 구현
```python
class Node :
    def __init__(self, key, data) :
        self.key = key
        self.data = data
        self.left = None
        self.right = None

    def inorder(self) :
        traversal = []
        if self.left :
            traversal += self.left.inorder()
        traversal.append(self)
        if self.right : 
            traversal += self.right.inorder()

        return traversal
    
    # 찾으려는 값이 있나?
    def lookup(self, key, parent = None) :
        # parent 인자가 없으면 None으로 가정
        if key < self.key :
            if self.left :
                return self.left.lookup(key, self)
            else :
                return None, None

        elif key > self.key :
            if self.right : 
                return self.right.lookup(key, self)
            else :
                return None, None
        
        # 같다면?
        else :
            # 내 self 노드의 부모
            return self, parent

    def insert(self, key, data) :
        
        # 만약 키가 이미 있다면 (중복이라면)
        if self.key is key :
            raise KeyError
        
        # (1) 찾으려는 키가 해당 노드보다 작은 경우
        if key < self.key :
            if self.left :
                self.left.insert(key, data)
            else :
                self.left = Node(key, data)
        elif key > self.key :
            if self.right :
                self.right.insert(key, data)
            else :
                self.right = Node(key, data)
    
    
class BinSearchTree :
    def __init__(self) :
        self.root = None

    def inorder(self) :
        if self.root :
            return self.root.inorder()
        else :
            return []

    def min(self) :
        if self.root :
            return self.root.min()
        else :
            return None    

    def lookup(self, key) :
        if self.root :
            return self.root.lookup(key)
        else :
            return None, None

    def insert(self, key, data) :
        if self.root :
            self.root.insert(key, data)
        else :
            self.root = Node(key, data)
```

* lookup()
    * 입력 인자 : 찾으려는 대상 키
    * 리턴 : 찾은 노드와 그것의 "부모 노드"
        * 각 없으면 None 으로

* insert()
    * 입력 인자  : 키, 데이터 원소
    * 리턴 : 없음


### 이진 탐색 트리에서 원소 삭제
(1) key를 이용해서 노드를 찾는다.
* 해당 키의 노드가 없으면, 삭제할 것도 없음
* 찾은 노드의 부모 노드도 알고 잇어야 함

(2) 찾은 노드를 제거하고도 이진 탐색 트리 성질을 만족하도록 트리의 구조를 정리한다.

인터페이스 설계
* 입력 : 키 (key)
* 출력 : 삭제한 경우 True, 해당 키의 노드가 없는 경우 False

```python
class BinSearchTree :
    def remove(self, key) :
        node, parent = self.lookup(key)
        if node :

            ###
            return True

        else :
            return False

```

### 이진 탐색 트리 구조의 유지
삭제 되는 노드가 
(1) 말단(leaf) 노드인 경우
* 그냥 그 노드를 없애면 된다.
    - 부모 노드의 링크를 조절 (좌 ? 우 ?)
(2) 자식을 하나 가지고 있는 경우
* 삭제되는 노드 자리에 그 자식을 대신 배치
    - 자식이 왼쪽? 오른쪽 ?
    - 부모 노드의 링크를 조정 (좌 ? 우 ?)
(3) 자식을 둘 가지고 있는 경우
* 삭제되는 노드보다 바로 다음 키를 가지는 노드를 찾아 그 노드를 삭제되는 노드 자리에 대신 배치하고 이 노드를 대신 삭제

### 이진 탐색 트리가 별로 효율적이지 못한 경우
* 한쪽으로 치우쳐진 균형이 이루어지지 않은 이진탐색 트리 -> 선형 탐색과 동등한 복잡도를 가진 경우

### 보다 나은 성능을 보이는 이진 탐색 트리들 
* 높이의 균형을 유지함으로써 `O(logn)` 의 탐색 복잡도 보장
* 삽입과 삭제 연산이 보다 복잡
* AVL TREE, RED-Black Tree
