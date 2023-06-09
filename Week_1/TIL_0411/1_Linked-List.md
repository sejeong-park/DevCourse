### 연결리스트 (Linked List)

기본적인 연결 리스트
Node 
- data
- Link (next)

Node 내의 데이터는 다르 데이터를 가르킬 수 있음

Head와 Tail이 존재함

왜 Tail이 필요할까 ? 
-> 뒤에 삽입이 필요한다 할 때 앞에서부터 탐색하는 것 보다 tail에 하나를 더 붙이는게 효율적

연결 리스트의 추상적 자료구조

```python
class Node :
    def __init__(self, item) :
        self.data = item
        self.next = None
```

```python
class LinkedList :
    def __init__(self) :
        self.nodeCount = 0
        self.head = None
        self.tail = None
```
* 비어있는 연결리스트가 생성자에 의할 수 있도록

### 연산의 정의
1. 특정 원소 참조 (k번째)
2. 리스트 순회
3. 길이 얻어내기
4. 원소 삽입
5. 원소 삭제
6. 두 리스트 합치기

```python
# 특정 원소 참조
def getAt(self, pos) :
    if pos <= 0 or pos > self.nodeCount :
        return None

    i = 1
    curr = self.head
    while i < pos :
        curr = curr.next
        i += 1

    return curr
```

### 배열과 비교한 연결 리스트

| | 배열 | 연결 리스트 |
|---|---|---|
| 저장공간 | 연속한 위치 | 임의의 위치 |
| 특정 원소 지칭 | 매우 간편 | 선형탐색과 유사 |
| 시간 복잡도 | O(1) | O(n) |


### 리스트 순회 
```python
class Node :
    def __init__(self, item) :
        self.data = item
        self.next = None

class LinkedList :
    def __init__(self) :
        self.nodeCount = 0
        self.head = None
        self.tail = None
    
    def getAt(self, pos) :
        if pos < 1 or pos > self.nodeCount :
            return None

        i = 1
        curr = self.head
        while i < pose :
            curr = curr.next
            i += 1

        return curr

    def traverse(self) :
        result = []
        tmp = self.head # head는 현재의 머리
        while tmp != None :
            result.append(tmp.data)
            tmp = tmp.next  # 다음 차례로 넘어가
        return result
```

### 연결 리스트 연산 - 원소의 삽입

```python
def insertAt(self, pos, newNode) :
    prev = self.getAt(pos - 1)
    newNode.next = prev.next
    prev.next = newNode
    self.nodeCount += 1
```
중간에 노드를 삽입한다고 가정을 한다면, newNode의 뒤쪽 링크를 조정하고 next 링크도 조정을 한다.

(1) 삽입하려는 위치가 리스트의 맨 앞일 때
* prev 없음
* Head 조정 필요

(2) 삽입하려는 위치가 리스트의 맨 끝이면
* Tail을 재조정해야한다.

(3) 빈 리스트를 삽입할 때는?
* 두 조건에 의해 알아서 처리됨


```python
class LinkedList :


    def insertAt(self, pos, newNode) :
        # 조건 1. Pos 가 올바른 위치인가?
        if pos < 1 or pos > self.nodeCount + 1 :
            return False

        # pos가 1이면, prev는 없고, head가 새로운 노드를 가르키게해야한다.
        if pos == 1 :
            newNode.next = self.head
            self.haed = newNode 

        else :
            prev = self.getAt(pos - 1)
            newNode.next = prev.next
            prev.next = newNode 

        # 맨 마지막에 삽입하면, tail을 새로운 노드로 조정한다.
        if pos == self.nodeCount + 1 :
            self.tail = newNode 

        self.nodeCount += 1
        return True
```
### 연결 리스트 원소 삽입의 복잡도
* 맨 앞에 삽입하는 경우 : O(1)
* 중간에 삽입하는 경우 : O(n)
* 맨 끝에 삽입하는 경우 : O(1)

### 연결 리스트 연산 - 원소의 삭제
* 코드 구현 주의 사항
    * 삭제 하려는 node 가 맨 앞의 것일 때
        * prev 없음
        * head 조정 필요

    * 리스트의 맨 끝의 node를 삭제할 때
        * Tail 조정 필요

    * 유일한 노드를 삭제할 때?
        *  두 조건에 의해 삭제를 할까?


```python
class Node :
    def __init__(self, item) :
        self.data = item
        self.next = None

class LinkedList :

    def __init__(self) :
        self.nodeCount = 0
        self.head = None
        self.tail = None

    def getAt(self, pos) :
        if pos < 1 or pos > self.nodeCount :
            return None
        i = 1
        curr = self.head
        while i < pos :
            curr = curr.next
            i += 1

        return curr

    def insertAt(self, pos, newNode) :
        if pos < 1 or pos > self.nodeCount + 1 :
            return False
        
        if pos == 1 :
            newNode.next = self.head
            self.head = newNode
        
        else :
            if pos == self.nodeCount + 1 :
                prev = self.tail
            else :
                prev = self.getAt(pos - 1)
            newNode.next = prev.next
            prev.next = newNode 

        if pos == self.nodeCount + 1 :
            self.tail = newNode 
        
        self.nodeCount += 1
        return True
    
    def popAt(self, pos) :
        if pos < 1 or pos > self.nodeCount :
            return False
        if pos == 1 :
            curr = self.head
            self.head = curr.next

            if self.nodeCount == 1 :
                self.tail = self.head

        else :
            prev = self.getAt(pos - 1)
            curr = prev.next
            prev.next = curr.next
            if pos == self.nodeCount :
                self.tail = prev

        self.nodeCount -= 1
        return curr.data

    def traverse(self) :
        result = []
        curr = self.head

        while curr is not None :
            result.append(curr.data)
            curr = curr.next
        return result
```
### ConCat

```python
def concat(self, L) :
    self.tail.next = L.head
    if L.tail :
        self.tail = L.tail
    self.nodeCount += L.nodeCount
```

### 연결 리스트가 힘을 발휘할 때
* 아이폰 작업에서 앱 뺄때! & 끼워넣을 때
* 삽입과 삭제가 유연하다는 것이 가장 큰 장점
* 새로운 메서드들을 만들자
    * insertAfter(prev, newNode) -> 맨 앞에서는 어떻게?
    * popAfter(prev) -> 맨 앞에서는 어떻게?