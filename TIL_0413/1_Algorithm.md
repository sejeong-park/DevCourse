## 알고리즘 문제 풀이

### 체육복 문제 (Greedy)
* 여벌의 체육복을 가져온 학생들의 번호(reverse)를 정렬 -> `O(klogk)`
* 체육복을 빌려줄 수 있는 학생을 찾아 처리 -> `O(k)*O(1)`
* 전체 알고리즘의 시간 복잡도 -> `O(klogk)`

### 방법 1
```python
def solution(n, lost, reserve) :
    uni = [1] * (n+2) 

    # 여벌의 체육복 = `O(n)`
    for i in reserve :
        uni[i] += 1
    # 분실 체육복 -1 = `O(n)`
    for i in lost :
        uni[i] -= 1

    for i in range(1, n + 1) :
        # 앞사람은 빌려야하고, 나는 여유본을 가지구 있을때
        if uni[i-1] == 0 and uni[i] == 2 :
            u[i-1:i+1] = [1,1]
        # 뒷 사람은 빌려야하고, 나는 여유본을 2개 가지고 있을 때
        elif uni[u] == 2 and uni[i+1] == 0  :
            u[i:i+2] = [1,1]

    # 체육 수업을 들을 수 있는 최대 학생 수
    return len([x for x in u[1:-1] if x > 0])

         
```

### 방법 2
```python
def solution(n, lost, reserve) :
    s = set(lost) & set(reserve) # 교집합
    l = set(lost) - s           # 체육복을 빌려야 하는 학생
    r = set(reserve) - s        #체육복을 빌려줄 수 있는 학생

    for x in sorted(r) :
        if x - 1 in l :
            l.remove(x - 1)
        elif x + 1 in l :
            l.remove(x + 1)

    return n - len(l)   # 전체 학생에서 빌려야 하는데 빌리지 못한 학생 반환
```