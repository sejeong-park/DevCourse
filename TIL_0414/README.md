## 0414

오늘은 코딩테스트 대비 강의를 보았다.
heapq 관련하여, 문제 풀이를 봤는데, 그동안은 문제를 접근할 때 heapq에 대한 이해가 부족했어서, heap 관련한 문제를 다른 방법으로 풀어왔다 -> Greedy 혹은 완탐으로 풀었던 것 같다.

다른 사람들의 코드를 참고하지 않으면, heapq에 대한 설계를 못했었는데, 이번 기회에 heapq를 이용해 풀어야 하는 알고리즘 문제가 나올 때, 왜 힙을 써야할까, 한 차례 사고 후 문제를 해결할 수 있을 것 같다.
연습을 통해 어떻게 적용해나갈지 고민 해야겠다.


### heap 관련 모듈 과 최대 힙
python에서 heapq 모듈은 `최소 힙` 으로 구현되어 있다.

[힙관련 모듈 참고](https://www.daleseo.com/python-heapq/)
* 힙 원소 추가 : `heapq.heappush(heap_list, data)`
* 힙 원소 삭제 : `heapq.heappop(heap)`    
    * heappop() 함수 호출은 원소를 삭제할 때마다 이진 트리의 재배치를 통해 새로운 최소값을 인덱스 0에 위치 시킨다.
* 최소값 삭제하지 않고, 얻기 : `heap[0]`
* 기존 리스트를 힙으로 변환 : `heapq.heapify(heap)`

* python에서 최대 힙은 어떻게 구현할까?
    * 최대 힙을 만드려면, 입력 값들에 음수를 씌운다.   
```python
nums = [4, 1, 7, 3, 8, 5]
heap = []
for num in nums :
    heapq.heappush(heap, (-num, num)) # (우선순위, 값)
while heap :
    print(heappop(heap)[1]) # index 1

```
```text
8, 7, 5, 4, 3, 2, 1
```

### n번째 최소값 / 최대값
* 최소 힙이나 최대 힙을 사용하면, n번째로 작은 값이나, n번째로 큰 값 구하는 데 효과적
```python
def nth_smallest(nums, n) :
    heapq.heapify(nums)
    nth_min = None
    # n 까지 탐색
    for _ in range(n) :
        nth_min = heapq.heappop(heap)

    return nth_min

print(nth_smallest([4, 1, 7, 3, 8, 5], 3))
```
* 이러한 용도로 사용할 수 있는 `nsmallest()`, `nlargest()`라는 함수 존재 !!!
    * 이 결과 리스트의 마지막 값이 n번째 작은 값 혹은 큰값이 된다!! 
    * `heapq.nsmallest(3, [4, 1, 7, 3, 8, 5])[-1]`
    * `heapq.nlargest(3, [4, 1, 7, 3, 8, 5])[-1]`



