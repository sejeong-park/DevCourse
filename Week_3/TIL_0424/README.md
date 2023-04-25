## 23.04.24

### Django 시작하기

> 방법에 대한 학습과정은 노션 페이지에 정리 - 첨부한 사진이 많아서 ... 

* [Django 시작하기](https://evening-november-9ec.notion.site/Django-fe19a9d0c3d0472eba52cf801ac3b611)

* [Django Admin](https://evening-november-9ec.notion.site/Django-Admin-5cca3d0304be496b89c358a57d0c1986)

* [Django Shell](https://evening-november-9ec.notion.site/Django-Shell-2f7f055b5b6e43ab87645d2d493a4abb)


### 참고자료
[Django 공식 Document 페이지](https://docs.djangoproject.com/ko/4.2/)
* Filter Look UP 함수

### 관계형 데이터베이스 (RDB)

* 관계형 데이터베이스 
    * 데이터를 행과 열로 이루어진 테이블의 형태로 구성
    * 테이블 간의 관계를 정의하는 데이터베이스 

    * [전에 CS 공부하면서 정리했던 RDB vs NoSQL](https://evening-november-9ec.notion.site/SQL-RDB-vs-NoSQL-8f3aaea485494c1ea1236a2b8e615452)

* 테이블
    * 데이터베이스에서 행과 열로 구성되어 있는 데이터의 집합

* 열
    * 테이블에 존재하는 필드(field)
    * **primary key** : 각 행(row)을 고유하게 식별할 수 있는 열(column) 
    * **foregin key** : 다른 테이블의 primary key를 참조하는 열(column)을 의미
        * foregin key를 사용하면, **두 테이블 간의 관겨를 설정**할 수 있다.
        * foregin key에 대해서는 Django에서 항상 indexing을 한다.
            * index를 안하면, 테이블을 Full Scan 해야하기 때문

* 행
    * 테이블에 저장된 데이터 레코드(Record)
