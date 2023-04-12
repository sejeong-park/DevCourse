##Circular Queue

### 큐의 활용
* 자료를 생성하는 작업과 그 자료를 이용하는 작업이 **비동기적**으로 일어나는 경우
* 자료를 생성하는 작업이 여러 곳에서 일어나는 경우
* 자료를 이용하는 작업이 여러 곳에서 일어나는 경우
* 자료를 생성사는 작업과 그 자료를 이용하는 작업이 양쪽 다 여러 곳에서 일어나는 경우
* consumer, producer

## 환형 큐 (Circular Queue) 
* 정해진 개수의 저장 공간을 빙 돌려가며 이용

### 환형 큐의 추상적 자료구조 구현
연산의 정의
* `size()` : 현재 큐에 들어 있는 데이터 원소의 수를 구함
* `isEmpty()` : 현재 큐가 비어 있는 지를 판단
* `isFull()` : **큐에 데이터 원소가 꽉 차 있는지를 판단** -> 선형 큐와 차이점
* `enqueue(x)` : 데이터 원소 x를 큐에 추가
* `dequeue()` : 큐의 맨 앞에 저장된 데이터 원소를 제거 (또한 반환)
* `peek()` : 큐의 맨 앞에 저장된 데이터 원소를 반환 (제거하지 않음)

### 환형 큐의 특징
- front 와 rear을 적절히 계산하여, 배열을 환형으로 재활용

### 배열로 구현한 환형 큐
```python
class CircularQueue :

    def __init__(self, n) :
        self.maxCount = n
        self.data = [None] * n
        self.count = 0
        self.front = -1
        self.rear = -1

    def size(self) :
        # 현재 큐 길이 반환
        return self.count

    def isEmpty(self) :
        # 큐가 비어있는가?
        return self.count == 0

    def isFull(self) :
        # 큐가 꽉 차 있는가?
        return self.count == self.maxCount

    def enqueue(self, x) :
        # 입력을 해야하는 데 Queue가 가득 차있으면 error 반환
        if self.isFull() :
            raise IndexError('Queue full')
        self.rear = (self.rear + 1) % self.maxCount     # rear 포인터 + 1
        self.data[self.rear] = x # 처음 들어가면 rear이 -1 -> 0이므로 data[0]에 들어갔을 것
        self.count += 1

    def dequeue(self) :
        if self.isEmpty() :
            # Queue에서 원소를 빼야하는데, 뺄 것이 없으면 Error 발생
            raise IndexError('Queue empty')

        self.front = (self.front + 1) % self.maxCount
        x = self.data[self.front] # front는 뒤에서부터 카운트 해줄 것
        self.count -= 1
        return x

    def peek(self) :
        if self.isEmpty():
            raise IndexError('Queue empty')
        return self.data[(self.front + 1) % self.maxCount] # 현재 자기가 마지막을 가르키고 있는데, 원형큐이니, +1이 0번째 원소
```

