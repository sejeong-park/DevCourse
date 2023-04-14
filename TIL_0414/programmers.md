# 힙 (Heap)
## 더 맵게
* 효울성 테스트도 포함되어 있다.

문제의 해결 - 예제
[1, 2, 3, 9, 10, 12]  (k = 7)
1. 1 + 2*2 -> 5 (3, 9 사이) -> [3, 5, 9, 12]
2. 3 + 5*2 -> 13 (12 뒤에) -> [9, 10, 12, 13]
3. 9 -> k= 7 이상이니, 더 탐색할 필요가 없다. (지금까지 몇번 확인했는 지)

### 알고리즘 복잡도
* 최악의 경우 : 모든 음식을 제일 안매운거랑 그다음안매운거 계속 섞어 배열의 끝까지 갈때
    * 수가 하나 남을때까지 섞어야 하는 경우 (n-1회)
* 각 단계 ("섞는 일")에서 요구되는 계산량
    * 정렬된 리스트에 순서 맞추어 원소 삽입 
    * `O(n)` = 목록의 길이에 비례
* 전체 문제 풀이의 복잡도 : `O(n^2)`
    * 지나치게 높다.
* 보다 좋은 방법은 없나?
    * 최소, 최대 원소를 빠르게 꺼낼 수 있으면 좋겠다!
    * max heap, min heap


### 힙
* 성질 : 최대/최소 원소를 빠르게 찾을 수 있다. (상수 시간에)
* 연산
    * 힙 구성 (heapify) - `O(NlogN)`
    * 삽입 (insert) - `O(logN)`
    * 삭제 (remove) - `O(logN)`
* 완전 이진 트리 -> 배열을 이용해서 응용 가능

### 힙의 응용
* 정렬 (heapsort)
* 우선순위 큐 (priority queue) 

### 더 맵게
* python에서 힙 적용
    * `import heapq`
    * `heapq.heapify(L)` # 리스트 L로부터 min heap 구성
    * `m = heapq.heappop(L)` # min heap L에서 최소값 삭제 (반환)
    * `heapq.heappush(L, x)`


```python
import heapq

def solution(scoville, K) :
    answer = 0 

    heapq.heapify(scoville)
    while True :        # O(n)
        min1 = heapq.heappop(scoville)  
        if min1 >= K :
            # 제일 안매운 음식이 K이상일 때
            break
        elif len(scoville) == 0 :
            # 제일 작은 수 하나를 뺐더니, 아무것도 남아있지 않은 경우
            answer = -1
            break

        min2 = heapq.heappop(scoville)  # 두번째로 음식이 안매운 경우
        new_scoville = min1 + 2 * min2  # 제일 안매운맛 + 2 * 두번째로 음식이 안매운 맛
        heapq.heappush(scoville, new_scoville)  # 새로 추가될 원소를 넣는다.
        answer += 1         # 한번 음식을 섞었다.

    return answer
```
* 전체 알고리즘 복잡도 : `O(nlogn)`

# 깊이 / 너비 우선탐색 (DFS/BFS)

## 여행 경로

* 배경 지식
    * 그래프
        * 정점과 간선
        * 유향 (directed) 그래프와 무향 (undirected) 그래프
    * 스택  (stack)
    * 큐    (queue)

## 깊이 우선 탐색 (DFS)
* 한 정점에서 인접한 모든(아직 방문하지 않은) 정점을 방문하되, 각 인접 정점 기준으로 깊이 우선 탐색을 모두 끝낸 후 다음 정점으로 진행


