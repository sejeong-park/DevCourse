## 23.04.19

- [1 : Beautiful Soup 에 대하여](1_beautifulsoup.ipynb)
- [2 : 동적 웹사이트에서 고려해야 할 사항](2_dynamic_website.ipynb)


크롤링 실습을 통해, html 파싱하는 방법을 배웠다.
배운 내용을 차주 프로젝트에서 어떻게 효율적으로 쓸 지 고민해봐야겠다.!



> 배운 내용 중, 오래 기억해야 할 사항들

## HTML의 Locator로 원하는 요소 찾기
* `id`, `class` 를 이용해 특정 요소 지정 후 정보를 가져온다.
* `tagname` : 태그의 이름
* `id` : 하나의 고유 태그를 가리키는 라벨
* `class` : 여러 태그를 묶는 라벨

```html
<p>This element has only tagname</p>
<p id="target">This element has tagname and id</p>
<p class="targets">This element has tagname and class</p>
```

### ID
* id는 요소 하나를 지칭하는 별명 - 겹칠 수 없다.
* id를 이용하면, 해당하는 태그 단 한개를 쉽게 가져올 수 있다.

### Class
* class는 유사한 요소들을 구분짓는 별명
* class 이용 시, 해당하는 태그 하나 혹은 여러개를 쉽게 가져올 수 있다.

## 스크래핑의 2가지 원칙
1. 과도한 요청 보내지 않기
2. 받아온 정보 활용에 유의하기


## 페이지네이션 - 페이지는 어떻게 넘길까?

* 스크래핑 관점에서는 굉장히 단점 
    * 왜? 페이지네이션 된 각 페이지들을 각각 접근해서 가져와야 하기 때문
    * 모든 View에서 접근 & 모든 로직 적용
    * 1,2,3, ... 반복
    * 한번에 요청을 한다면 서버에 부하를 주는가?를 위배할 수 있다.
        * 어느정도 시간차를 두자!

## 정적 웹 사이트와 동적 웹 사이트

* 정적(static) 웹 사이트 : HTML 내용이 고정된 것 : 같은 주소 & 같은 응답
    * html 문서가 완전하게 응답한다.
* 동적(dynamic) 웹 사이트 : HTML 내용이 변하는 것
    * 응답 후 HTML이 렌더링이 될 때까지 지연시간이 존재
    * requests를 보낸 후에 바로 파싱 하면 안돼 & 구조가 바뀔 수 있다.

### 동적 웹 사이트의 동작 방식
* 웹 브라우저에선 JavaScript라는 프로그래밍 언어가 동작한다.

* 비동기 처리를 통해서 필요한 데이터를 채운다

* 동기 처리 : 요청에 따른 응답을 기다린다.
    * 렌더링과 데이터 처리 : 렌더링을 다 해야만 데이터 처리를 진행하는 !
    * 동기 처리된 후, HTML 로딩에 문제가 발생하지 않는다.
* 비동기 처리 : 요청에 따른 응답을 기다리지 않는다.
    * 렌더링을 시켜놓고 데이터 처리를 하는 ! (기다리지 않는다.)
    * 상황에 따라서 데이터가 완전하지 않은 경우가 발생한다.


### 어떻게 해결할 수 있을까? & 비동기 상황에서 데이터가 불완전하다면?

* 임의로 시간을 지연한 후, 데이터 처리가 끝난 후 정보를 가져오면 된다.
* 키보드 입력, 마우스 클릭 등을 프로그래밍할 순 없을까? (UI Action)

응답이 온 후에 요소들에 접근하는 환경
1. 웹 브라우저를 파이썬으로 조작하자!!!
2. 웹 브라우저를 자동화하는 라이브러리 : Selenium