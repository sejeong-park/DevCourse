## Queue

#### Queue
* 자료를 보관할 수 있는 선형 구조
* 단, 넣을 때에는 한쪽 끝에서 밀어넣어야 하고,
* 꺼낼 때에는 반대 쪽에서 뽑아 꺼내야 하는 제약이 있음
* 선입 선출(FIFO) 특징을 가지는 선형 구조

#### 큐의 동작

* 초기 상태 : 비어있는 큐 (empty Queue)
```python
Q = Queue()
Q.enqueue(A)
Q.enqueue(B)
r1 = dequeue()  # r1 = A
```
* 추상적 자료구조에 enqueue를 통해 넣는다.
* 데이터 원소를 꺼내기 위해, 반대방향에서 꺼낸다.
* 먼저 들어간 데이터가 먼저 나온다!

### 큐의 추상적 자료구조 구현
(1) 배열(array)을 이용하여 구현
* Python 리스트와 메서드들을 이용
(2) 연결 리스트(linked list)를 이용하여 구현
* 양방향 연결 리스트를 이용

### 연산의 정의
* `size()` - 현재 큐에 들어있는 데이터 원소의 수를 구함
* `isEmpty()` - 현재 큐가 비어 있는 지를 판단
* `enqueue(x)` - 데이터 원소 x를 큐에 추가
* `dequeue()` - 큐의 맨 앞에 저장된 데이터 원소를 제거 (또한, 반환)
* `peek()` - 큐의 맨 앞에 저장된 데이터 원소를 반환 (제거하지 않음)

> 스택과 큐
> 큐는 선입 선출
> 스택은 나중에 들어갔던 것이 먼저 나온다.

### 배열로 구현한 큐
```python
class ArrayQueue :
    def __init__(self) :        # 큐의 크기를 리턴
        self.data = []
    def isEmpty(self) :
        return self.size() == 0
    def enqueue(self, item) :
        self.data.append(item)  # 데이터 원소를 추가
    def dequeue(self) :
        return self.data.pop(0) # 맨 앞에 있는 것을 꺼내 리턴
    def peek(self) :
        return self.data[0] # 0번 원소가 무엇인지 확인하는 것
```
* 배열로 구현한 큐의 연산 복잡도
|연산| 복잡도 | 
|---|---|
|size()| O(1) |
|isEmpty() | O(1) |
| enqueue() | O(1) | 
| dequeue() | O(n) | 
| peek() | O(1) |

* dequeue 는 Queue의 길이에 비례하는 복잡도를 가진다.
    * dequeue는 배열의 맨 앞 원소를 꺼내야 한다.
    * 리스트로 구현을 하다보면, 1번째 원소를 꺼내므로 배열을 index-1씩 줄어드는 연산
        * Queue의 길이에 비례하는 연산 (Queue의 길이가 길어질 수록 연산이 느려진다.)

### 이중 연결 리스트로 큐를 구현
* 코드의 구현을 할 때 "연산 복잡도"에 대해 꼭 생각을 해볼 것!

### Double-Linked-List로 큐를 구현
<!-- <details>
<summary>Double-Linked-List</summary>
<div markdown = "1"> -->
```python
class Node :
    def __init__(self, item) :
        self.data = item
        self.prev = None
        self.next = None

class DoublyLinkedList :
    def __init__(self) :
        self.nodeCount = 0
        self.head = Node(None)
        self.tail = Node(None) 
        self.head.prev = None 
        self.head.next = self.tail
        self.tail.prev = self.head
        self.tail.next = None

    # 연결 리스트 표현해주기
    def __repr__(self) :
        if self.nodeCount == 0:
            return 'LinkedList : empty'

        s = ''
        curr = self.head
        # 현재 head의 ->-> 노드가 유효할 때까지 (dummy 존재하기 때문)
        while curr.next.next :
            curr = curr.next
            s += repr(curr.data)
            # dummy가 없을 때까지 -> 표시해주기
            if curr.next.next is not None :
                s += '->'
        return s 

    def getLength(self) :
        return self.nodeCount

    # 순회
    def traverse(self) :
        result = []
        curr = self.head
        while curr.next.next :
            curr = curr.next
            result.append(curr.data)
        return result

    # 역순
    def reverse(self) :
        result = []
        curr = self.tail    # 끝부터 탐색
        while curr.prev.prev :
            curr = curr.prev
            result.append(curr.data)
        return result


    def getAt(self, pos) :
        if pos < 0 or pos > self.nodeCount :
            return None

        # 현재 위치가 끝에서 더 가까울때
        if pos > self.nodeCount // 2 :
            i = 0
            curr = self.tail    # 뒤어서부터 탐색
            while i < self.nodeCount - pos + 1 :
                curr = curr.prev
                i += 1

        else :
            i = 0
            curr = self.head    # 앞에서부터 탐색
            while i < pos :
                curr = curr.next
                i += 1

        return curr

    def insertAfter(self, prev, newNode) :
        next = prev.next    # curr
        newNode.prev = prev
        newNode.next = next
        prev.next = newNode # insert
        next.prev = newNode
        self.nodeCount += 1
        return True

    def insertAt(self, pos, newNode) :
        if pos < 1 or pos > self.nodeCount :
            return False

        prev = self.getAt(pos-1) # pos -> 현재의 위치 구하기(새로 삽입하면서 현재 위치는 prev가 된다.)
        return self.insertAfter(prev, newNode)
    
    def popAfter(self, prev) :
        curr = prev.next
        next = curr.next
        prev.next = next
        next.prev = prev
        self.nodeCount -= 1
        return curr.data

    def popAt(self, pos) :
        if pos < 1 or pos > self.nodeCount :
            raise IndexError('Index out of range')

        prev = self.getAt(pos - 1)
        return self.popAfter(prev)

    def concat(self, L) :
        self.tail.prev.next = L.head.next
        L.head.next.prev = self.tail.prev
        self.tail = L.tail

        self.nodeCount += L.nodeCount
```
<!-- </div>
</details> -->


```python
class LinkedListQueue :

    def __init__(self) :
        self.data = DoublyLinkedList()

    def size(self) :
        return self.data.getLength()

    def isEmpty(self) :
        return self.data.getLength() == 0
    
    def enqueue(self, item) :
        node = Node(item)
        self.data.insertAt(self.data.nodeCount + 1, node)

    def dequeue(self) :
        return self.data.popAt(1)

    def peek(self) :
        return self.data.getAt(1).data
```





