## 우선순위 큐 구현

* 큐가 FIFO(First-In First-Out) 방식을 따르지 않고, 원소들의 우선순위에 따라 큐에서 빠져나오는 방식

우선 순위 큐가 어디서 사용될까?
* 운영체제의 CPU 스케줄러

서로 다른 두 가지 방식이 가능할 듯
(1) Enqueue 할 때 우선순위 순서를 유지하도록
(2) Dequeue할 때 우선순위 높은 것을 선택
-> 어느것이 유리할까? -> 1번이 조금 더 유리

우선 순위 큐를 구현하는 방법
(1) 선형 배열 이용
(2) 연결 리스트 이용
-> 어느것이 유리할까?
* 시간을 기준으로 하면 연결 리스트가 유리 (중간에 삽입하는 경우에서 시간적 측면에서 유리)
* 링크드리스트가 무조건 유리할까? -> 공간 복잡도 측면에서 선형 배열이 유리

### 우선순위 큐를 추상적 자료 구조를 이용해 해결하기
```python
class PriorityQueue :
    def __init__(self, x) :
        self.queue = DoublyLinkedList()

    def size(self) :
        return self.queue.getLength()

    def isEmpty(self) :
        return self.size() == 0
    
    # 데이터 삽입 연산
    def enqueue(self, x) :
        newNode = Node(x) # 새로 삽입할 노드

        # 처음 시작하는 위치는 head
        curr = self.queue.head

        # (1) 끝까지 가지 않을 조건 
        # (2) 우선순위를 비교하는 조건
        while curr.next != self.queue.tail and x < curr.next.data :
            curr = curr.next 

        # 양방향 연결 리스트 이용해 삽입
        self.queue.insertAfter(curr, newNode)
```

