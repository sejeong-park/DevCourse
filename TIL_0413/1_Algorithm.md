## 알고리즘 문제 풀이

## 체육복 문제 (Greedy)
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

## 가장 큰 수  - Sort 문제

문제의 해결 방법
(1) 빈 문자열로 수를 초기화 한다
(2) 수의 목록을 **(크게 만드는 것 우선으로)** 정렬 한다
(3) 목록에서 하나씩 꺼내어 현재 수에 이어 붙인다.
(4) 모든 수를 다 사용할 때까지 반복한다.


* 3 vs 32
    * 332 , 323 -> 3 > 32
* 3 vs 33
    *  333 , 333 -> 3 = 33
* 3 vs 34
    * 334 , 343 -> 3 < 34

### 크게 만드는 수의 기준 
* 34 vs 343
    * 34343 , 34334 -> 34 > 343

알고리즘 설계 방법 
* 대소 관계 비교를 위한 기준을 마련
* 이것을 이용하여 주어진 배열을 정렬
* 정렬된 배열을 이용하여 문자열 표현을 완성

### 가장 큰 수 문제 구현

```python
def solution(numbers) :
    numbers = [str(x) for x in numbers] # 문자열로 변환 ->  `O(n)`

    numbers.sort(key = lambda x : (x * 4)[:4], reverse = True)  # O(nlogn)
    if numbers[0] == '0' :
        # test 11번은 0만 여러개 들어있는 케이스일 수 있다.
        answer = '0'
    else :
        answer = ''.join(numbers)       # O(n)
    return answer
```

## 큰 수 만들기

### 큰 수 만들기 원칙 
* 앞 자리에 큰 수가 오는 것이 전체를 크게 만든다.
    * 따라서, 큰 것을 우선해서 골라 담고 싶다.
* 주어진 숫자로부터 하나씩 꺼내 모으되
    * 이 때 이미 모아둔 것 중 지금 등장한 것 보다 작은 것들은 빼낸다
    * 이것은 어디서 어떻게 살펴보아야하나? (오른쪽)
        * 아직 뺄 개수 (k)를 채우지 못한 경우
        * 자릿수는 어떻게 계산하는 가?

### 알고리즘의 복잡도 
* 가장 단순 (무식)한 방법은 어떤 것일까?
* 우리가 설계한 알고리즘의 복잡도는?
    * ~~`O(n^2)`~~ -> `O(n)`


### 탐욕법(Greedy)

* **앞 단계에서의 선택 (앞자리에 큰 수!)이 이후 단계에서의 동작에 의한 해의 최적성에 영향을 주지 않음**


```python
def solution(number, k ):
    collected = []

    # 이중 순환문
    for i, num in enumerate(number) :
        while len(collected) > 0 and collected[-1] < num and k > 0 :
            collected.pop()
            k -= 1
        if k == 0:
            collected += list(number[i:])
            break
        collected.append(num)
    
    # k가 남아 있다면 K 만큼 떼어낸다
    collected = collected[:-k] if k > 0 else collected
    answer = ''.join(collected)
    return answer
```