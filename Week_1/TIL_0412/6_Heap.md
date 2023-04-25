## Heap

* 이진트리의 한 종류 (이진 힙 - Binary Heap)
(1) 루트(root) 노드가 언제나 최댓값 또는 최솟값을 가짐
    * 최대 힙 (max heap) , 최소 힙 (min heap)
(2) 완전 이진 트리여야 한다.

### 최대 힙의 예

* 재귀적으로 정의 됨
    * 어느 노드를 루트로 하는 서브트리도 모두 최대 힙
* parent 노드로 올라갈 수록 큰 값을 갖고 있다.
    * 하지만, left, right의 상대적인 순서는 정의되어 있지 않는다
* 느슨한 정렬

### 이진 트리와의 비교

(1) 원소들은 완전히 크기 순으로 정렬되어 있는가?

(2) 특정 키 값을 가지는 원소를 빠르게 검색할 수 있는가?

(3) 부가의 제약 조건은 어떤 것인가?

### 최대 힙의 추상적 자료구조
연산의 정의

* `__init__()` : 빈 최대 힙을 생성
* `insert(item)` : 새로운 원소 삽입
* `remove()` : 최대 원소 (root node)를 반환 / 그리고 동시에 이 노드를 삭제

### 데이터 표현의 설계
* 배열을 이용한 이진트리의 표현
    * 노드 번호 M을 기준으로
    * 왼쪽 자식의 번호 : `2*m`
    * 오른쪽 자식의 번호 : `2*m + 1`
    * 부모 노드의 번호 : `m//2`

* 완전 이진 트리이므로, 노드의 추가/삭제는 마지막 노드에서만
* 완전 이진트리라는 성질 때문에 배열로 구현하는게 적합하다

```python
class MaxHeap :
    def __init__(self) : 
        self.data = [None]
```

### 최대 힙에 원소 삽입
(1) 트리의 마지막 자리에 새로운 원소를 임시로 저장
(2) 부모 노드와 키 값을 비교하여 위로, 위로 이동

### 최대 힙에 원소 삽입 - 복잡도
* 원소의 개수가 n인 최대 힙에 새로운 원소 삽입
    * 부모 노드와의 대소 비교 최대 회수 : `log_2_n`
* 최악 복잡도 `O(logn)` 의 삽입 연산




```python
def insert(self, item) :
    m = len(self.data)
    self.data.append(item)

    # 0 = None 원소 한개라면 반환
    if m == 1 :
        return

    while self.data[m//2] < self.data[m] :
        self.data[m] , self.data[m//2] = self.data[m//2], self.data[m] # 치환
        m = m//2        # 상위 레벨
        
        # 루트 노드라면 종료
        if m == 1 :
            break

```


### 최대 힙에서 원소의 삭제

(1) 루트 노드의 제거 - 이것이 원소들 중 최댓값

(2) 트리 마지막 자리 노드를 임시로 루트 노드의 자리에 배치

(3) 자식 노드들과의 값 비교와 아래로, 아래로 이동
* 자식 노드는 왼쪽, 오른쪽 둘 있을 수도 있는데, 어느 쪽으로 이동?
* 더 큰 키 값을 가지는 쪽으로~

### 최대 힙으로부터 원소 삭제 - 복잡도

* 원소의 개수가 n인 최대 힙에서 최대 우너소 삭제
    * 자식 노드들과 대소 비교 최대 회수 : `2*log_2_n`
* 최악 복잡도 `O(logn)`의 삭제 연산

```python
class MaxHeap :
    def remove(self) :
        if len(self.data) > 1 :
            # 맨 마지막 데이터와 루트노드의 값을 교환
            self.data[1], self.data[-1] = self.data[-1], self.data[1]
            data = self.data.pop(-1)
            self.maxHeapify(1)
        else :
            data = None

        return data

    def maxHeapify(self, i) :
        left = 2*i          # 왼쪽 인덱스
        right = 2*i + 1     # 오른쪽 인덱스
        smallest = i

        if left < len(self.data)  and self.data[left] > self.data[smallest] :
            smallest = left

        if right < len(self.data) and slef.data[right] > self.data[smallest] :
            smallest = right

        if smallest != i :
            # 현재 노드와 최댓값 노드를 교처
            self.data[smallest] , self.data[i] = self.data[i], self.data[smallest]
            # 재귀적 호출을 이용해 최대 힙의 성질을 만족할 때까지 트리를 정리
            self.maxHeapify(smallest) 

    
```


### 최대 / 최소 힙의 응용
(1) 우선순위 큐 (priority queue)
* Enqueue 할 때, "느슨한 정렬"을 이루고 있도록 함 : `O(logn)`
* Dequeue를 할 때 최댓값을 순서대로 추출 : `O(logn)`
* 제 16강에서 양방향 연결 리스트 이용 구현과 효율성 비교!
(2) 힙 정렬 (heap sort)
* 정렬되지 않은 원소들을 아무 순서로나 최대 힙에 삽입 : `O(logn)
`
* 삽입이 끝나면, 힙이 비게 될 때까지 하나씩 삭제 : `O(logn)`
* 정렬 알고리즘 복잡도 : `O(nlogn)`

### 힙 정렬의 코드 구현
```python
def heapsort(unsorted) :
    H = MaxHeap()
    for item in unsorted :
        H.insert(item)

    sorted = []
    d = H.remove()
    while d :
        sorted.append(d) 
        d = H.remove()

    return sorted
```


