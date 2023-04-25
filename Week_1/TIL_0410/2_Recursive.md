## 재귀 알고리즘 - 기초 (Recursive functions)

* 하나의 함수에서 자신을 다시 호출하여 작업을 수행하는 것
* 생각보다 많은 종류의 문제를 재귀적으로 해결 가능

* 이진트리
    * 노드 기준
    * 왼쪽 서브트리의 원소들은 모두 작거나 같을 것
    * 오른쪽 서브트리의 원소들은 모두 클 것
    * 이 원칙은 모두 노드들에 재귀적으로 적용 가능

* 수학 공식을 이용해서 생각해보기
```python
def sum(n) : 
    # 0 미만의 수는 자기 자신
    if n <= 1 :
        return n
    # 양수만
    else :
        return n + sum(n-1)
```
> 재귀 함수를 호출 할 때 종결 조건이 매우 중요하다!!    
알고리즘의 종결조건에 반드시 필요하다!!

## 피보나치 순열 구현하기
```python
def solution(x):
    answer = 0
    
    def fibo(x) :
        if x == 0 :
            return 0
        elif x == 1 : 
            return 1
        else :
            return fibo(x-1) + fibo(x-2)
    answer = fibo(x)
    return answer
```

## 재귀 알고리즘 응용

* 재귀적이 반복된다는 점에서 count 파트에서 약점을 갖는다.

### 조합의 수 계산
* n개의 서로 다른 원소에서 m개를 택하는 경우의 수
