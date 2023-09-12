# 목차 
[1. 프로그램 성능평가](#1-프로그램-성능평가) <br>
[1-1. 점근적 표기법](#1-1-점근적-표기법-asymptotic-notation) <br>
[2. 시간 복잡도](#2-시간-복잡도-time-complexity) <br>
[2-1. 빅 오 함수의 종류](#2-1-시간복잡도-빅-오-표기법-함수의-종류) <br>
[3. 공간 복잡도](#3-공간-복잡도-space-complexity) <br>

# 1. SQL 이란? 

SQL이란 데이터베이스에서 데이터를 정의, 조작, 제어하기 위해 사용되는 명령어입니다. SQL의 구성요소로는 크게 3가지 데이터 정의어(DDL), 데이터 조작어(DML), 데이터 제어어(DCL)으로 구성됩니다. 

데이터 정의어(DDL) : 데이터 베이스를 생성하거나 테이블을 만드는 언어 

데이터 조작어(DML) : 데이터베이스에 저장된 데이터를 조회하거나 수정, 삭제하는 등의 역할을 하는 언어 

데이터 제어어(DCL) : 사용자의 권한을 설정하는 언어 

<img src="assets/DML의예시.PNG" width="300" height="300"><br/>

테이블이란 항상 이름을 가지고 있는 리스트로 데이터가 저장되어있는 공간을 의미. 테이블은 행(ROW)과 열(COLUMN) 그리고 거기에 대응하는 값(FIELD)으로 구성되어 있다. 

<img src="assets/테이블.PNG" width="300" height="300"><br/>

# 2. 검색 - SELECT 

SELECT는 테이블에 저장된 데이터를 검색하는 명령어입니다. 예를들어, 아래의 그림처럼 book 테이블에서 책의 제목과 저자만을 검색하는 것을 말할 수 있습니다. 

<img src="assets/select.PNG" width="300" height="300"><br/>

기본적인 문법은 아래와 같이 구성되는데, 검색할 컬럼 부분에 *라는 명령어를 입력시에 전체 컬럼을 가져올 수도 있습니다. 

<img src="assets/select문법.PNG" width="300" height="300"><br/>

# 3. 조건 - WHERE

WHERE 절이란 검색하고자 하는 데이터의 조건을 설정할 수 있는 명령으로서 테이블의 특정 데이터를 검색하려고 할 때 사용된다. 예를 들어, 책 정보를 저장하는 book 테이블에서 제목이 '돈키호테'인 책을 검색해보자고 할 때 WHERE 절이 사용된다. 

<img src="assets/where.PNG" width="300" height="300"><br/>

WHERE 문의 기본 문법은 FROM 테이블 뒤에 비교 연산자와 함께 조건을 달아줌으로써 사용된다. 

<img src="assets/where문법.PNG" width="300" height="300"><br/>

# 4. 다양한 조건 - WHERE

위에서 배운 WHERE을 좀 더 심화해서 사용하는 것으로 하나의 조건뿐 아니라 여러 개의 조건을 사용할 수 있다. 

<img src="assets/다양한where.PNG" width="300" height="300"><br/>

비교연산자

<img src="assets/비교연산자.PNG" width="300" height="300"><br/>

복합 조건 연산자

<img src="assets/복합조건연산자.PNG" width="300" height="300"><br/>

기타 연산자

<img src="assets/기타연산자.PNG" width="300" height="300"><br/>

