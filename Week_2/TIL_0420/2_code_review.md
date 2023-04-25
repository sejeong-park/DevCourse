# 코드 리뷰

- [좋은 코드 리뷰 방법](#좋은-코드-리뷰-방법)
- [Unit Test의 이해](#어떤-테스트들이-존재하는가)
    - [Unit Test의 예시](#숫자를-받아서-평균-계산-스크립트)
- [소스버전 컨트롤](#소스-버전-컨트롤)

## 좋은 코드 리뷰 방법

* 코드 리뷰를 요청하는 사람
    * 요청 시 되도록이면, 조금씩 자주 요청
        * Unit test와 같이 요청하면 최상
    * 주석을 최대한 추가하고, 무슨 이유에서 뭘 하려는 것인지 설명
    * 리뷰에 대한 피드백을 너무 감정적으로 받아들이지 않기

* 코드 리뷰를 하는 이
    * 코딩 스타일에 대한 것보다는 코드 자체에 대해 이야기
    * 객관적으로 쓰고, 비판하는 어조 피하기
    * 충분히 시간을 들여 도움이 되는 리뷰를 제공

* 코드 리뷰에 편리한 툴 사용
    * Github


### 코드 리뷰
* 새로운 코드 추가나, 기능 추가가 진행된다면, 그에 상응하는 **TestCode**가 필요하다.

## 어떤 테스트들이 존재하는가?
* **Unit Test**
    * 모듈의 특정 기능(함수)테스트
    * 보통 하나의 함수를 테스트
    * 자신이 만든 소프트웨어의 특정 기능을 테스트 하는 것

* **Integration Test**
    * 여러 모듈을 통합하여 하는 한 차원 위의 테스트

* **Acceptance Test**
    * 트래픽 등 생성하여 시스템에 로드를 주고, 견디는 지 보는 테스트

* **UI Test**
    * Selenium 등의 툴을 이용해, 웹 페이지 자체의 기능을 테스트하는 것이 대세

### 테스트가 왜 중요할까?
- Unit Test를 의무적으로 요구 : 테스트 없으면 코드 체크인 실패
- 테스트가 많을 수록
    - 시스템의 안정성 증대
    - Refactoring할 경우 혹은 새로 들어온 신입 엔지니어가 코드 수정할 때 굉장히 편리
- 어떤 경우에는 테스트를 작성하기가 너무 힘든 경우들이 있음

### Unit Test의 정의
* 자신이 만든 소프트웨어의 특정 기능을 테스트 하는 것
    * 많은 경우 특정 함수를 테스트 하는 것
    * 특정 입력에 대해 예상되는 특정 출력이 나오면 성공 아니면 실패
* Integration Test나 Functional Test에 비해 가장 낮은 레벨의 기본 테스트


### Test Coverage
* 실행 가능 경로 중 몇 퍼센트나 테스트가 되어있는지 그 퍼센트를 나타낸다.
* Test Coverage가 높을 수록 시스템이 안정됨은 물론, 부수적인 효과가 존재
    * 해당 모듈을 재작성 시 굉장히 유용
    새 엔지니어가 들어와서 작업 시 유용
* 100% Test Coverage를 갖기 위해 적어도 3개의 Unit Test가 필요 (if 조건을 모두 테스트 하기 위해)

* test code를 만들고 싶다면, 별도의 test file을 만든다.
    * `python3 -m unittest test.py`

### Python에서 Unit Test
* 이런 함수들은 각기 하나의 기능을 테스트
    * 하나의 메소드에 대해 정해진 입력을 주고 정해진 출력이 나오는 지 확인
* 출력의 타입에 따라 다른 함수들을 사용해서 테스트 성공여부를 결정
    * `assertEqual(a,b)` : a와 b 두개의 객체가 같으면 True, Flas
    * `assertTrue(a)` : a 가 True 이면 성공, False이면 실패
    * `assertRaises` : 주어진 입력에 대해 예상한 Exception이 나는지 확인

### 숫자를 받아서 평균 계산 스크립트
```python
import sys

def compute_average(numbers) :
    if not numbers :
        return None

    sum = 0
    for number in numbers :
        sum += number

    return sum / len(numbers)

def main() :
    list = []
    for argv in sys.argv[1:] :
        list.append(int(argv))
    print("Average : " + str(compute_average(list)))

if __name__ == "__main__" :
    main()
```

```python
import unittest
import avg

class averageTetstCase(uniitest.TestCase) :

    def test_average(self) : 
        answer = avg.compute_average([1,2,3,4,5])
        self.assertEqual(answer, 3.0)

    def test_empty_input_average(self) :
        answer = avg.compute_average([])
        self.assertEqual(answer, None)

if __name__ == "__main__" :
    unittest.main()
```


## 소스 버전 컨트롤
### 소스 버전 컨트롤
* 개발자들이 자신이 개발하는 소프트웨어의 소스코드에 발생하는 변경사항들을 관리할 수 있도록 해주는 프로그램

### 왜 소스 버전 컨트롤을 사용하나?
* 코드에 생기는 변경 사항들을 쉽게 추적 가능
    * 에러 시 이전 버전으로 Rollback
* 두 사람 이상이 공동 개발시 코드의 공유와 변경 용이
* 최근 시스템들은 코드리뷰도 지원
* 코드 백업의 역할 수행


### CI/CD 프로세스 만들기
* build -> test -> deploy -> monitor

### BUILD(Package)란 ?
* 자신 (혹은 팀)이 개발한 소프트웨어를 최종적으로 배포하기 위한 형태로 만드는 것을 의미
* 이를 위해 충분한 테스트 필요

### CI/CD 프로세스를 구현하려면
* SWE Pracice의 하나
1. 하나의 코드 repository 유지
2. 코드 변경을 계속해서 위의 코드 repository에 반영
3. 유닛 테스트를 추가
    * Repository의 Test Coverage를 70% 이상으로 유지
4. 안정적인 테스트 환경 준비
5. 빌드 생성 자동화  (테스트 포함)
    * Commit Build vs Nightly Build
6. 빌드 배포 자동화  (CD)

## 질문
* 테스트코드를 작성하는데도 자원이 들텐데 테스트코드를 작성하는데 타이밍이 있을까요?
    * Production / Test 환경을 구분한다.
        * 자원을 구분한다.
        * CI/CD의 중요성 -> DevOps가 필요하고,, 서버가 필요하고... 등등
    * 면접 할 때, 개발환경이 따로 있나?
        * Staging 환경 & Test 환경 유무에 따라 회사의 환경을 파악할 수 있다.

* Java에서는 moskito 나 junit, spring test 같은 것을 쓰는데 파이썬은 주로 사용하는 라이브러리가 있을까요?
    * unittest 모듈
    * markup object를 만들어서 쓴다.

