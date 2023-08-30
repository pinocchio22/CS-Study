# 목차 
[1. DDL](#1-DDL) <br>
[2. DML](#2-DML) <br>
[3. SUBQUERY](#3-SUBQUERY) <b
[4. Join](#4-Join) <br>r>
[5. 내장 함수](#5-내장-함수) <br>
[6. NULL](#6-NULL) <br>


# 1. DDL(Data-Definition Language)
* 스키마를 정의 / 수정 / 삭제할 때 사용
## 테이블 생성
* create table 테이블명
* primary key - 기본키로 지정
* foreign key - 외래키로 지정

## 테이블 삭제/수정
* drop table 테이블명 - relation과 내부 튜플 모두 삭제
* delete from 테이블명 - relation은 보존하고 내부 튜플만 삭제
* alter table 테이블명 add 어트리뷰트 도메인 - Attribute 추가

# 2. DML(Data-Manipulation Language)
* 데이터를 검색/삽입/삭제/수정할 떄 사용
* select: 알고자 하는 Attribute 리스트
* from: 출처 Relation 리스트
* where: 튜플 필터링 조건

<br>
<img width="762" alt="image" src="https://github.com/pinocchio22/CS-Study/assets/61182499/afdb9c6e-f8dd-432c-bb24-7798d70d87f3">
<br>

# 3. SUBQUERY
##  메인 쿼리와 서브 쿼리
### 메인 쿼리
* 외부 질의를 의미
* 서브 쿼리가 반환한 값을 이용해서 메인 쿼리가 완성

### 서브 쿼리
* 내부 질의(내부 SELECT 문, 중첩된 SELECT 문)를 의미
* 메인 쿼리에서 사용할 값을 반환
* 하나의 SQL 문 안에 포함되어 있는 또 다른 SQL문

## 서브 쿼리의 사용
* 검색하고자 하는 자료의 형태 및 유무, 자료의 양 등의 조건에 따라 상황에 맞게 사용
* 잘못 사용할 경우 성능에 나쁜 영향을 줄 수 있으므로 주의를 요함 (예시)

### SELECT - 스칼라 서브쿼리
* 결과를 알고자하는 Attribute 리스트를 명시
* 코드, 계산 등에 사용
#### select / select all
* 중복을 허용하는 일반적인 select
#### select distinct
* 중복을 제거하는 select
#### select *
* 모든 Attribute. 즉, 테이블을 그대로 원하는 경우
#### select 사칙연산
* Attribute 값에 산술연산을 가미한 결과를 얻고 싶은 경우

```swift
SELECT 고객명, 지역, 
        (SELECT SUM(금액)
         FROM 주문
         WHERE 주문.고객번호=고객.고객번호) AS 구매액
FROM 고객
WHERE 직업='학생';

고객 테이블에서 학생이라는 직업을 가진 고객들을 정보를
가져오면 주문테이블에서 각 고객들의 구매액을 보여줌
```

### FROM - 인라인 서브쿼리
* 1차 가공하여 테이블을 결과로 보여주고 그 결과를 대상으로 쿼리를 할 때 사용
* 대상 Relation을 명시

```swift
SELECT *
FROM customer,
    (SELECT custid AS cid,
            SUM(saleprice) AS samt
     FROM orders
     GROUP BY custid) csales
WHERE customer.custid = csales.cid

고객별 주문 내역 출력
```

### WHERE - 서브쿼리
* 튜플 필터링 조건을 명시
* and / or / not과 같은 논리 연산자 사용 가능
* 서브쿼리로 공급될 결과 집합의 컬럼이 메인 쿼리의 조건에 기술된 타입, 수 등이 동일해야 함

```swift
SELECT *
FROM 주문
WHERE 고객번호 IN ( SELECT 고객번호
                  FROM 고객
                  WHERE 지역='제주도‘ );

고객 테이블에서 '제주도'에 거주하는 고객의 고객번호를 가져와서 주문 테이블에서
주문내역을 가져옴
```

# 4. Join 
* SQL에서 두 개 이상의 Relation을 함께 사용하여 원하는 데이터를 얻는 방법

join의 종류

## Aggregate Functions
### Group By
* 테이블에서 특정 Attribute의 값이 같은 튜플들을 모아 그룹을 만들고, 그렇게 만들어진 각 그룹별로 검색을 하는 기능
* 여러 튜플 집합으로 나누어 각각의 결과를 알고 싶을 때 사용

### Having
* group by를 사용할 때 having절을 사용
* group by로 만들어진 그룹에 대한 조건을 명시

# 5. 내장 함수
## 문자열 함수
### Ascii()
* 문자열의 제일 왼쪽 문자의 아스키 코드 값을 반환(Integer)
### Char()
* 정수 아스키 코드를 문자로 반환(Char)
### Charindex()
* 문자열에서 지정한 식의 위치를 반환
### Difference()
* 두 문자식에 SUONDEX 값 간의 차이를 정수로 반환

```swift
SELECT ASCII ('abcd')
SELECT CHAR(97)
SELECT Charindex('b','abcde')
SELECT Difference('a','b')

결과: 97
결과: a
결과: 2
결과: 3
```

### Left()
* 문자열에서 왼쪽에서부터 지정한 수만큼의 문자를 반환
### Len()
* 문자열의 길이 반환
### Lower()
* 대문자를 소문자로 반환

```swift
SELECT Left('abced','3')
SELECT Len('abced')
SELECT Lower('ABCDE')

결과: abc
결과: 5
결과: abcde
```

### Replace()
* 문자열에서 바꾸고 싶은 문자 다른 문자로 변환
### Reverse()
* 문자열을 역순으로 출력
### Space()
* 지정한 수만큼의 공백 문자 반환
### Substring()
* 문자, 이진, 텍스트 또는 이미지 식의 일부를 반환

```swift
SELECT Replace('abcde', 'a', '1')
SELECT Reverse('abcde')
SELECT Space(10)
SELECT Substring('abcde', 2, 3)

결과: 1bcde
결과: edcba
결과: '          '
결과: bcd
```

## 날짜 및 시간함수
### getdate()
* 오늘 날짜를 반환(datetime)
### Datename()
* 지정한 날짜의 특정 날짜부분을 나타내는 문자열을 반환
### Day()
* 지정한 날짜에 일 부분을 나타내는 정수를 반환 (Month, Year 동일)

```swift
SELECT GETDATE()
SELECT Detaname(d, getdate())
SELECT Day(getdate())

결과: 2012-01-06 16:39:09:620
결과: 6
결과: 6
```

## 기타 함수
### Isnumeric()
* 해당 문자열이 숫자형이면 1 아니면 0을 반환
### Isdate()
* 해당 문자열이 Datetime이면 1 아니면 0

```swift
SELECT Isnumeric('30')
SELECT Isnumeric('f2')
SELECT Isdate('20231231')
SELECT Isdate('aa')

결과: 1
결과: 0
결과: 1
결과: 0
```

# 6. NULL
* 아직 지정되지 않음
* 값을 알 수 없음
* 값을 적용 할 수 없음
* null은 공백과 같지 않음
* null은 0이 아님
