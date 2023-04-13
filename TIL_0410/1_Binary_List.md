##  선형 배열 Point

####  List.insert(index, 대상 값)

```
 L.index(3, 65)
```
* index 3번째 위치에 65를 삽입해라

#### 궁금증
* append 메소드와 insert 메소드의 차이는 무엇일까?

* del 과 pop의 차이는 무엇일까?

---

## 정렬
* `sorted()`
    
    * 내장 함수 (built-in function)
    * 정렬된 새로운 리스트를 얻어냄
    * 역순 방법 -> ```L2 = sorted(L, reverse = True)```

* `sort()`

    * 리스트의 메서드 (method)
    * 해당 리스트를 정렬함
    * 역순 방법 -> ```L.sort(reverse=True)```

#### 정렬에 조건 주는 방법
```
L = ['abcd' , 'xyz' , 'spam']
sorted(L, key = lambda x: len(x))
```
* 결과 : `['xyz', 'abcd', 'spam']

```python
L = [{'name' : 'John', 'score' : 83}, {'name' : 'Paul', 'score' : 92}]
L.sort(key = lambda x : x['score'], reverse = True)
```
* 레코드들을 점수 높은 순으로 정렬

## 탐색 알고리즘

### 선형 탐색 알고리즘 (Linear Search)
* 리스트의 길이에 비례하는 시간 소요 : `O(n)`
    * 최악의 경우 : 모든 원소를 다 비교해야 한다

### 이진 탐색 알고리즘 (Binary Serach)
* 탐색하려는 리스트가 이미 정렬되어 있는 경우에만 적용 가능
* 크기 순으로 정렬되어 있다는 성질을 이용
* 한 번 비교가 일어날 때마다 리스트를 반씩 줄임
    * `O(logn)`
```python
def solution(L, x):
    answer = 0
    
    start, end = 0, len(L)-1
    
    while start <= end :
        middle = (start + end) // 2         # 중간값 찾기
        
        if L[middle] == x :
            return middle
        elif L[middle] < x: 
            # start보다 작으면
            start = middle +1
        else :
            end = middle - 1
    
    return -1
```