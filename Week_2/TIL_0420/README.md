# 23.04.20 (목)

### 두가지 내용에 대해서는 주기적으로 자주 보자. 
👉 좋은 코드란 무엇인가?
* [좋은 코드란 무엇일까?](./1_code_style_guide.md)
* [코드 리뷰](./2_code_review.md)
* [셀레니움](./3_Selenium.ipynb)

### 생각 정리

오늘 한기용 멘토님의 말씀들은 앞으로도 계속 기억했으면 좋은 말들이여서, 주기적으로 자주 보고 회고 하고 싶은 말씀들이였다. 
* TIL의 일부로 남기에는 너무 소중했다. -> 노션에다가도 기록해두자.

코드 리뷰를 받아본 적이 없어, 다른 개발자들이 코드 리뷰를 어떻게 진행하는지 궁금했고, 아직 python에 대한 기능이나, class 등 조금 더 가독성과 Python 특성을 이용하는 기술이 부족하다고 생각해서, 코드 리뷰를 받으며 성장하고 싶었다.

git에서 예시를 보여주시면서, 예시 코드에 대해 리뷰할 점에 대해 설명해주셔서, 시니어 관점에서 이런 부분을 피드백 해주시는구나 알 수 있어서 좋았다. 피드백을 받으면서 설계 방법을 더 고려한다면 확장성 있는 부분을 고민하고, 잘 성장해나갈 수 있을 것 같다..🥲

UnitTest 측면에서는 Spring 강의를 잠깐 들었을 때, JAVA 특성 상 TestCode의 중요성과 방법들을 이해하고, 작성하는 방법을 배웠었다. 하지만, 내가 들었던 Python - Flask, FastAPI 강의들에서는 UnitTest까지 하는 방법에 대한 설명이 없기도 했고, 간단한 서버만 띄우는 용이였어서 그런가.. 무지로, 중요성을 이해하지 못했는데, python 환경에서 unitTest의 중요도에 대해 다뤄서 좋았다.
- 주말에 UnitTest에 대해 한번 더 공부를 해야겠다.


### 좋은 개발자의 시작은? - 나에 대한 생각 정리
* 긍정적인 자세 & 남과 비교하지 않기
    * 본체는 긍정적인 편이지만, 아무래도 공부에 전념하고, 취업 시장 빙하기에 다시 취준생으로 뛰어든 이후로부터는 자신감이 많이 줄어들었다.. 🥲 나는 긍정적인 걸까, 부정적인 걸까 ㅎㅎ
    * 그러면서 먼저 취업한 주변과 비교되는 것도 사실.,
        * 내 가치관을 지키고, 발전에 중심을 두지만, 어쩔 수 없이 비교되는 요즘이다.
        * 내가 선택한 준비 기간이니, 여유로움을 가지고, 조바심 내지 말기
            * 기술적으로 폭넓게 많이 성장하기
            * 데이터가 많고, 신입 프로세스가 존재하고, 업무를 배울 수 있는 회사로 가기 위한 준비 기간 !
* 커리어를 길게 보기
    * 취준생이라는 것이 생각보다 더 조급함이 생기는데, .. 길게 보자!
    * 인생은 사진 아니고 동영상이라고 했다.
* 질문 잘하기
    * 왜 사용하는가?
    * 무슨 목적인가?
    * 혼자 해결하지 못하는 부분인가?
* 의사 소통 잘하기
    * 나는 의사소통에는 자신있다! ㅎㅎ
* 문제 정의 잘하기
    * 문제 정의도 잘한다!ㅎㅎ 
        - 개발로 이어질 수 있도록 문제를 해결하는 방법에 대해 고민해보자
* 결과 내기
    * 결과 내기에 부족한듯? - 5개월동안 결과도 잘내는 개발자로 성장하자!

### 좋은 코드란 무엇일까?
* 깔끔한 코드는 읽고, 이해하고, 수정하기 쉬움
* 코드는 명확한 이름, 일관된 형식, 의미 있는 주석으로 체계적으로 구성
* 좋은 코드는 테스트가 가능하며, 코드와 함께 유닛 테스트를 작성해야 함
* 클래스와 함수는 분명한 하나의 일을 하도록 구현해야 함
* 코드는 모듈화되어야 하며, 중복을 피해야 함
* 오류처리는 코드베이스 전체에서 철저하고, 일관성 있게 이루어져야 함 -> 로깅
    * 운영관점에서 중요함
* 코드는 작성자가 아닌 사용자를 염두에 두고 설계해야 함
* 단 중요한 일에 더 완벽을 기할 것 


#### 다음주(Git 특강) 준비 사항
* 2인 1조로 팀짜기
* Git Account 만들기


### 알게된 사항
`sys.argv` : `python3 avg.py 10 20 30 40 50` : 실행 cmd에서 입력

`assertEqual` : JAVA에서 `Assertions.assertThat(avg()).isEqualTo(30);`

