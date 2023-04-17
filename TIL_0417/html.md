## HTML
웹 페이지의 구조를 정의하며, 텍스트, 이미지, 비디오 등의 다양한 콘텐츠를 표시할 수 있다. 

```html
<!DOCTYPE html>    <!-- 문서 버전 -->
<html lang="ko">    <!-- HTML문서 시작 선언 및 문서 기본 언어 설정 -->
  <head>    <!-- 문서에 필요한 정보가 기입되는 곳 -->
    <title>문서 제목</title>    <!-- 문서의 제목 -->
  <head>
    
  <body>    <!-- 실제 사용자가 눈으로 볼 수 있는 문서의 내용이 입력되는 곳 -->
    안녕하세요!
  </body>
</html>
```
### HEAD
* 사람 눈에 보이지 않는 문서의 정보 담기는 영역
1. title
2. meta data
3. css, script

### BODY
* 사용자 눈에 실제로 보이는 콘텐츠


#### info check 방법
* 주석 : 개발자가 코드 내에 입력한 메모
    * <!--Content-->
    * 주석 내 주석은 사용 불가능
    * 사용자에게는 보이지 않는 주석이지만, 소스보기나 개발자 도구로 보면 코드가 보이니 주의하기!

* 메타 데이터 - 인코딩
    - charset은 문서에서 허용하는 문자의 집합
    - charset에 선언

#### block 레벌 요소 
    * 레고 블록 처럼 차곡차곡 쌓이고, 화면의 너비가 꽉차는 요소
    * 일반적으로 페이지의 구조적 요소를 나타낸다.
    * `<div></div>`
    * 파티션을 나눈다.


#### inline 레벨 요소
    * 블록 요소 내 포함하는 요소
    * 크기 조절 불가능 & 좌/우 여백만 허용
    * `<span>, <a>, <strong>`

#### inline-block
    * 글자처럼 취급되나, block태그의 성질을 가지는 요소
    * block과 마찬가지로 크기와 내/외부 여백을 지정할 수 있다.
    * css로 성질을 바꾼 것이기 때문에 의미상 인라인 레벨 요소이다.

### 레이아웃 태그를 왜 알아야 할까?
* HTML5부터 태그를 의미있게 사용하기 위해 Semantic 태그를 사용하여 문서 구조 작성
* 단순히 의미 구분자인 `<div>`를 남발하지 않고, 적절한 태그를 사용하여 웹 문서가 담은 구조를 의미 있게 전달
* 시멘틱 하게 마크업을 함으로써 검색엔진의 검색 순위에 가산점을 얻거나, 홈페이지의 로딩 속도를 높인다.

#### 레이아웃 ㅌ태그
* `<div>`    :  가장 흔히 사용되는 레이아웃 태그로 단순히 구역을 나눔
* `<headers>`   : 블로그의 글 제목, 작성일 등 주요 정보
* `<footer>`    : 페이지의 바닥줄에 사용 - 저작권 정보, 연락처 등
* `<main>`  : 페이지의 가장 큰 부분, 주요 콘텐츠를 담는 태그
* `<section>`   : 콘텐츠 구역을 나누는 태그 - 신문지에서 여러 기사 & 각 구역
* `<article>`   : 블로그 포스트 & 뉴스 기사와 같은 독립적인 문서 전달
* `<aside>`     : 문서의 주요 내용에 간접적인 정보를 전달하는 태그 -> 쇼핑몰 오른쪽에 따라다니는 "오늘 본 상품" 같은 것으로 사용


### 자주 사용하는 태그
`<h1> ~ <h6>`
* 문서의 구획 제목 Heading 태그
    * h1은 페이지 내 한번만 사용되어야 하고, 구획의 순서는 지켜져야 함

`<p>`
* 문서에서 하나의 문단을 나타냄
    * 제목 태그와 함께 사용되기도 하고, 단독으로 사용되기도 함

`<b>, <strong>`
* 글씨 두깨 조절
    * `<b>` 의미X, 단순 굵은 글씨
    * `<strong>` 강조의 의미, 굵은 글씨
* 두 태그는 시각적으로 굵은 효과는 동일하지만, 의미가 다르다.

`<i>, <em>`
* 글씨의 기울기를 조절할 수 있다.
    * `<i>` 태그는 기울임과 동시에 텍스트가 문단의 내용과 구분 필요
    * `<em>` 태그는 기울임과 동시에 "강조" 를 나타냄

`<u>`
* 글씨에 밑줄을 넣고 주석을 가지는 단어
    * css로 스타일링 하여, 빨간 밑줄을 넣는 것으로 오타를 나타낸 것 처럼 사용 가능
    * 단순하게 밑줄만 긋는 용도로 사용하면 안됨

`<s>, <del>`
* 글씨에 취소선 추가 가능
    * `<s>` 태그는 단순히 시각적인 취소선 추가, 접근성 기기에 취소에 대한 안내는 하지 않음
    * `<del>` 태그는 문서에서 제거된 텍스트, `<ins>` 태그와 함께 사용되면 제거된 텍스트 옆에 추가된 텍스트 표현 가능

`<a>`
* 클릭하면 페이지 이동 -> 링크 요소
    * href 속성 사용해 이동하고자 하는 파일 혹은 url 작성
    * target 속성을 사용해 이동해야 할 링크를 새창 (_blank), 현재 창(_self) 등 원하는 타겟을 지정 가능 

### 멀티미디어 태그
* `<img>`
* `<figure>, <figcaption>`
* `<video>`
* `<audio>`
* `<svg>`

### 리스트 태그
* `<ul>, <li>`
* `<ol>, <li>`
* `<dl>, <dt>, <dd>`

### 표 태그
* `<table>`
* `<th>`
* `<thed>`
* `<tbody>`
* `<tfoot>`
* `<caption>`

### 외부 콘텐츠 관련 태그
* `<iframe>`

### form 태그
정보를 제출하기 위한 태그
* input, selectbox, textarea 등을 가질 수 있다.
* 정보를 제출하기 위한 button을 가진다.
* action 속성으로 정보가 제출되었을 때, 페이지를 이동시킬 수 있다.
* method 속성으로 정보가 제출될 때 처리 방식을 결정할 수 있다.
* GET 방식 : 도메인 뒤에 모든 input의 정보가 표시된다.
    * 검색할 때 주로 사용
* POST 방식 : (개발자도구) network의 payload - 양식데이터에서 확인 가능
    * 로그인 할 때 주로 사용 ; 보안이 중요할때 사용한다.


### label 테그
* input, textarea, selecbox의 설명을 작성할 수 있는 태그
* id 속성이 절대로 중복되면 안된다.

### 자주 사용되는 input 태그
1. checkbox : input을 체크박스 형태로 만든다.
2. radio : 라디오 버튼으로 만든다.
3. file : 파일을 첨부할 수 있게 만든다.
4. buttom : value 속성에 입력된 값을 이름으로 갖는 버튼으로 만든다.
5. hidden : input을 시각적으로 숨겨준다. 정보 제출 시 value 속성에 입력된 값은 전송된다

### select 태그
* 옵션 메뉴를 제공하는 태그
    * option 태그를 사용해 옵션을 정의한다.

### textarea
* 여러 줄을 입력할 수 있다.

### 알아두면 좋은 속성
* readonly : 사용자가 수정할 수 없는 "읽기 전용"으로 만든다.
* required : form이 제출될 때 "필수 입력 사항"으로 만든다.
* placeholder : input, textarea에 부가 설명을 입력해둘 수 있다 `<select>` 태그에서 사용할 수 없다.
* disabled : 요소가 비활성화 되며 정보 제출 시 값이 제출되지 않는다. 

### HTML 작성 시 주의 사항
* 대소문자 주의 -> 소문자 작성
* 닫는 태그 생략 주의
* 한글 사용 지양
* ID 중복 사용 주의
* 계층 구조 유지
* 동일 의미의 태그 중첩 금지 