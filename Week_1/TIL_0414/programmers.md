# 알고리즘 문제 풀기
- [힙 (heap)](#힙-heap) : 더 맵게
- [DFS/BFS](#깊이--너비-우선탐색-dfsbfs) : 여행경로
- [DP](#동적-계획법-dynamic-programming) : N으로 표현


# 힙 (heap)
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

### 깊이 우선 탐색 (DFS)
* 한 정점에서 인접한 모든(아직 방문하지 않은) 정점을 방문하되, 각 인접 정점 기준으로 깊이 우선 탐색을 모두 끝낸 후 다음 정점으로 진행
    * 재귀적인 구조 -> stack

### 너비 우선 탐색 (BFS)
* 한 정점에서 인접한 모든(아직 방문하지 않은) 정점을 방문하고, 방문한 각 인접 정점을 기준으로 (방문한 순서에 따라) 또 다시 너비 우선 탐색을 행함


### 여행경로 풀이
```python
def solution(tickets) :
    routes = {}
    for t in tickets :
        routes[t[0]] = routes.get(t[0], []) + [t[1]] # 출발 공항, 도착 공항 value
        
    # 도착 공항 계산하기 - 이름 역순 정렬
    for r in routes :   # 알고리즘 복잡도가 여기에서 지배된다. # `O(nlogn)`
        routes[r].sort(reverse = True)

    stack = ["ICN"]
    path = []
    # stack에 있는 것이 없어질 때 까지
    while len(stack) > 0 :      # `O(n)`
        top = stack[-1] # 마지막

        # 마지막이 route에 없거나, 아무것도 없을 때
        if top not in routes or len(route[top]) == 0:
            path.append(stack.pop())
        else :
            stack.append(routes[top][-1]) # 알파벳 순서 상 가장 앞에 있는 것
            routes[top] = routes[top][:-1]

    return path[::-1] # 리턴하는 리스트를 역순으로!
```
* `O(nlogn)`


# 동적 계획법 (Dynamic Programming)

* 주어진 최적화 문제를 
* 재귀적인 방식으로 보다 작은 부분 문제로 나누어
* 부분 문제의 풀어, 이 해를 조합하여
* 전체 문제의 해답에 이르는 방식
* 알고리즘의 진행에 따라 탐색해야 할 범위를 **동적으로 결정함**으로써 탐색 범위를 한정할 수 있음

* 피보나치 수열
    * 그 직전 두 항이 다음 항
    * 재귀함수로 구현한다면 ?
        *  f(4) = f(3) + f(2)
        *         f(2) + f(1) + f(1) + f(0)
        *         f(1) + f(0) + f(1) + f(1) + f(0)
        * 같은 함수를 재귀적으로 호출하는 맹점 존재
        * 복잡도 : 지수함수의 형태!!
    * 동적 계획법을 적용한다면?
        * 복잡도 : 선형함수의 형태 

### N으로 표현
N = 5
* N을 한 번 사용해서 만들 수 있는 수들 -> 1 : 5
* N을 두 번 사용해서 만들 수 있는 수들 -> 2 : 55
* N을 세 번 사용해서 만들 수 있는 수들 -> 3 : 555

```text
4 - 5555 : 1 (+, -, *, /) 3
         : 2 (+, -, *, /) 2
         : 3 (+, -, *, /) 1

5 - 55555 : 1 (+, -, *, /) 4
          : 2 (+, -, *, /) 3
          : 3 (+, -, *, /) 2
          : 4 (+, -, *, /) 1

N = x
n - x * n : 1 (+, -, *, /) n-1
          : 2 (+, -, *, /) n-2
          :     ...
          : n-1 (+, -, *, /) 1
```

* 요약 
    * 문제의 성질에 따라
    * 동적계획법으로 풀어냄으로써
    * 탐색해야 하는 범위를 효과적으로 줄일 수 있음


```python
def solution(N, number) :
    s = [set() for x in range(8)]

    # enumerate start = 1: index 1부터 시작
    for i, x in enumerate(s, start = 1) :
        x.add(int(str(N) * i))

    # 4겹으로 되어있지만, 중복 제거와 DP를 이용한다
    for i in range(len(s)) :
        for j in range(i) :
            for op1 in s[j] :
                for op2 in s[i - j - 1] :
                    s[i].add(op1 + op2)
                    s[i].add(op1 - op2)
                    s[i].add(op1 * op2)
                    # 뒤에 있는게 0이 아니여야 한다.
                    if op2 != 0 :
                        s[i].add(op1 // op2)

        if number in s[i]:
            answer = i + 1
            break

    # 8번 지정했는데도 안되는 경우
    else :
        answer = -1
        
    return answer

```



