#PostgreSQL
__개요__
1. PostgreSQL은 관계형 데이터베이스 시스템의 일종이다.
2. 가장 진보한 오픈소스 데이터베이스 시스템이라고 할 수 있다.
3. Unix/Linux, MAC OS, Soraris, Windows 등의 OS를 지원한다.
4. PostgreSQL은 완전 무료 소프트웨어이다.

__특징__
1. multi-version concurrency control(MVCC)의 완벽한 지원함
2. C/C++,Java 등의 프로그래밍 언어 연동을 완벽 지원함
3. 확장성에 매우 좋음(Data Types, Index Types, Function 등)
4. 커뮤니티 활성화(오픈소스 커뮤니티가 있고 많은 기업들이 기술지원 서비스를 하고있음)


__select 문법__
<pre>
<code>
    select : --추출 재상 컬럼, 만약 테이블의 모든 컬럼을 다 보고 싶다면 '*'
    from : --추출 대상 테이블명 입력
    
</code>
</pre>

__SQL 실행순서__
<pre>
<code>
select --3
	A.first_name , --4 
	A.last_name , 
	A.email 
from --1 
	customer A --2  
;
</code>
</pre>

<pre>
<code>
--ALIAS -> 코드의 가독성 -> sql 성능
--DBMS -> 옵티마이저 -> 최적화기 -> sql -> 가장빠르게, 가장 저비용, 실행

--옵티마이저란?
--sql을 가장 빠르고 효율적으로 수행할 최적(최저비용)의 처리경로를 생성해 주는 DBMS 내부의 핵심엔진이다.
</code>
</pre>
-------------------------------------------------------------------------------------

__order by 문법__
<pre>
<code>
select 				--추출 대상 컬럼
	column_1,
	column_2
from 
	TBL_NAME		--추출 대상 테이블명 입력
	
 </code>
</pre>

<pre>
<code>
order by column_1 asc 	column_1 은 오름차순 정력(default는 asc)
order by column_2 desc	column_2 은 내림차순 정렬(default는 asc)

 </code>
</pre>

--------------------------------------------------------------------------------------
<pre>
<code>
select 
	FIRST_NAME,
	LAST_NAME
from 
	customer 
order by first_name asc
;
 </code>
</pre>

--------------------------------------------------------------------------------------
<pre>
<code>
select 
	first_name,
	last_name
from 
	customer 
order by first_name desc 
;
 </code>
</pre>
---------------------------------------------------------------------------------------
<pre>
<code>
select 
	first_name,
	last_name
from 
	customer 
order by firs_name asc, last_name desc 
;
 </code>
</pre>
---------------------------------------------------------------------------------------

__select distinct 문법__
<pre>
<code>
select distinct column_1		--COLUMN_1의 값이 중복 값 존재 시 중복 값을 제거
from TABLE_NAME;
 </code>
</pre>

---------------------------------------------------------------------------------------
<pre>
<code>
select distinct column_1, column_2			--COLUMN_1+COLUMN_2의 값이 중복 값 존재 시 중복 값을 제거
from TABLE_NAME;
 </code>
</pre>
---------------------------------------------------------------------------------------
<pre>
<code>
select distinct column_1, column_2			--COLUMN_1+COLUMN_2의 값이 중복 값 존재 시 중복 값을 제거
from TABLE_NAME								
order by column2, column2					--결과를 명확하게 하기 위해 order by 절 사용
 </code>
</pre>

---------------------------------------------------------------------------------------
__테이블 생성__
<pre>
<code>
create table T1(ID SERIAL not null primary key, BCOLOR VARCHAR, FCOLOR VARCHAR)
 </code>
</pre>

__데이터 삽입__
<pre>
<code>
insert 
into T1(BCOLOR, FCOLOR)
values
	('red','red')
   ,('red','red')
   ,('red',null)
   ,(NULL,'red')
   ,('red','green')
   ,('red','blue')
   ,('green','red')
   ,('green','blue')
   ,('green','green')
   ,('blue','red')
   ,('blue','green')
   ,('blue','blue')
  ;
  
 commit;
  </code>
</pre>

---------------------------------------------------------------------------------------
<pre>
<code>
select distinct BCOLOR
from t1 
order by BCOLOR 
;
 </code>
</pre>
---------------------------------------------------------------------------------------
<pre>
<code>
select distinct BCOLOR, FCOLOR
from t1 
order by BCOLOR, FCOLOR
;
 </code>
</pre>
---------------------------------------------------------------------------------------
<pre>
<code>
select distinct on(BCOLOR) BCOLOR		--BCOLOR 컬럼 값 기준 중복 제거함
	   ,FCOLOR							--FCOLOR 컬럼 값은 단 한 개 값 만은 보여줌
from t1 
order by
	BCOLOR, FCOLOR;
	 </code>
</pre>
---------------------------------------------------------------------------------------
<pre>
<code>
select distinct on(BCOLOR) BCOLOR		--BCOLOR 컬럼 값 기준 중복 제거함
		,FCOLOR							--FCOLOR 컬럼 값은 단 한개만 보여줌
from t1 
order by
	BCOLOR, FCOLOR desc;					--FCOLOR 컬럼 값을 보여 줄 때 내림차순 정렬함
 </code>
</pre>
----------------------------------------------------------------------------------------
__where 절 문법__

<pre>
<code>
select 
	COLUMN_1,
	COLUMN_2
from 
	TABLE_NAME
where	
	<조건>
;
 </code>
</pre>
----------------------------------------------------------------------------------------
<pre>
<code>
연산자
= : 같음
> : ~보다 큰
< : ~보다 작은
>= : ~보다 크거나 같은
<= : ~보다 작거나 같은
<>, != : ~가 아닌
and : 그리고
or : 혹은
 </code>
</pre>

----------------------------------------------------------------------------------------
<pre>
<code>
select 	
	LAST_NAME, --3
	FIRST_NAME
from 
	customer  --1
where
	FIRST_NAME='Jamie';			--2	-- FIRST_NAME아 'Jamie'인 행을 출력함
 </code>
</pre>
----------------------------------------------------------------------------------------
<pre>
<code>	
select 
	LAST_NAME,
	FIRST_NAME
from 
	customer 
where
	FIRST_NAME='Jamie'			--FIRST_NAME이 'Jamie'이면서
and LAST_NAME ='Rice';			--LAST_NAME이 'Rice'인 행을 출력함
 </code>
</pre>
-----------------------------------------------------------------------------------------
<pre>
<code>
select 
	CUSTOMER_ID,
	AMOUNT,
	PAYMENT_DATE
from 	
	PAYMENT 
where
	AMOUNT <= 1					--AMOUNT가 1이하 이거나
	or AMOUNT >=8 ;				--AMOUNT가 8이상인 행을 출력
 </code>
</pre>
------------------------------------------------------------------------------------------
	
__limit 절 문법__
<pre>
<code>
-- 특정 집합을 출력시 출력하는 행의 수를 한정하는 역할을 한다. 부분 범위 처리시 사용된다. PostgreSQL, MySQL 등에서 지원한다.
 </code>
</pre>

<pre>
<code>
select 
	*
from 	
	TABLE_NAME
limit N;			--출력하는 행의 수를 지정한다.
 </code>
</pre>
--------------------------------------------------------------------------------------------
<pre>
<code>
select 
	*
from 
	TABLE_NAME
limit N offset M;			--출력하는 행의 수를 지정하면서 시작위치를 지정한다. offset M 값의 시작위치는 0이다.
 </code>
</pre>
--------------------------------------------------------------------------------------------
<pre>
<code>
select 
	FILM_ID,
	TITLE,
	RELEASE_YEAR
from 	
	FILM								
order by FILM_ID			--FILM_ID로 정렬한다ㅣ
	limit 5;				--정렬한 값 중에서 결과 건수는 5건수로 제한한다.
 </code>
</pre>	
---------------------------------------------------------------------------------------------
<pre>
<code>	
select 
	FILM_ID,
	TITLE,
	RELEASE_YEAR
from 
	FILM
order by FILM_ID				--FILM_ID로 정렬한다.
	limit 4						--정렬한 값 중에서 결과 건수는 4건으로 제한한다.
	offset 3;					--FILM_ID로 정렬한 값 중에서 출력행의 시작위치는 3이다.(시작위치 3은 0,1,2,3 즉 4번째 행부터 시작)
 </code>
</pre>
----------------------------------------------------------------------------------------------
<pre>
<code>
select 
	FILM_ID,
	TITLE,
	RENTAL_RATE
from 
	FILM
order by RENTAL_RATE desc			-- RENTA_RATE를 내림차순으로 정렬한다.
limit 10;							-- 정렬한 값 중에서 최소 10건 만을 출력한다.
 </code>
</pre>
-----------------------------------------------------------------------------------------------

__fetch 절 문법__
<pre>
<code>
--특정 집합을 출력 시 출력하는 행의 수를 한정하는 역할을 한다. 부분 범위 처리시 사용된다.
 </code>
</pre>
<pre>
<code>
select 
	*
from 
	TABLE_NAME
fetch first [N] row only;	-- 출력하는 행의 수를 지정한다. N을 입력하지 않고 ROW ONLY만 입력하면 단 한건만 출력된다.
 </code>
</pre>
------------------------------------------------------------------------------------------------
<pre>
<code>
select 
	*
from 
	TABLE_NAME
offset [N] rows					--출력하는 행의 수를 지정하면서 시작위치를 지정한다. offset N 값의 시작위치는 0이다.
	fetch first [N] row only; 
 </code>
</pre>	
-------------------------------------------------------------------------------------------------
<pre>
<code>
select 
	FILM_ID,
	TITLE
from 
	FILM
order by TITLE				--TITLE로 정렬한 집합 중에서
fetch first row only;	--최초의 단 한 건의 행을 리턶나다.
 </code>
</pre>
-------------------------------------------------------------------------------------------------
<pre>
<code>
select 
	*
from 
	FILM
order by TITLE				--TITLE로 정렬한 집합중에서
fetch first 1 row only;		--최초의 단 한 건의 행을 리턴한다.
 </code>
</pre>
-------------------------------------------------------------------------------------------------
<pre>
<code>
select 	
	FILM_ID,
	TITLE
from 	
	FILM
order by TITLE				--TITLE로 정렬한 집합중에서
	offset 5 rows			--6번째 행부터
fetch first 5 row only;		--5건의 행을 리턴한다.
 </code>
</pre>
---------------------------------------------------------------------------------------------------
__IN 연산자 문법__
<pre>
<code>
--특정 집합(컬럼 혹은 리스트)에서 특정 집합 혹은 리스트가 존재하는지 판단하는 연산자
 </code>
</pre>
<pre>
<code>
select 	
	*
from 
	TABLE_NAME
where
	COLUMN_NAME in (VALUE1, VALUE2,...)		--COLUMN_NAME이 가지고 있는 집합에서 VALUE1, VALUE2등의 값이 존재하는지 확인
 </code>
</pre>	
-----------------------------------------------------------------------------------------------------
<pre>
<code>
select 
	*
from 
	TABLE_NAME
where COLUMN_NAME in 						--COLUMN_NAME이 가지고 있는 집합에서 TABLE_NAME2 테이블의 COLUMN_NAME2의 집합이 존재하는지 확인
(select COLUMN_NAME2 from TABLE_NAME2)
 </code>
</pre>
------------------------------------------------------------------------------------------------------
<pre>
<code>
select
	CUSTOMER_ID,
	RENTAL_ID,
	RETURN_DATE
from 
	RENTAL
where
	CUSTOMER_ID in (1,2)			--CUSTOMER_ID가 1혹은 2인 행을 출력한다.
order by RETURN_DATE desc;			--그 결과를 RETURN_DATE 컬럼 내림차순으로 출력한다.

-- 가독성, 알아보기 쉽다.
-- (DBMS 최적화기, SQL 최적화) 옵티마이저 특성상 IN조건이 OR 보다 성능상 유리할때가 많다.
 </code>
</pre>
-------------------------------------------------------------------------------------------------------
<pre>
<code>
select 
	CUSTOMER_ID,
	RENTAL_ID,
	RETURN_DATE
from 
	RENTAL
where
	CUSTOMER_ID =1 or CUSTOMER_ID=2			-- CUSTOEMR_ID가 1혹은 2인 행을 출력한다.
order by RETURN_DATE desc;					-- 그 결과를 RETURN_DATE 컬럼 내림차순으로 출려한다.
 </code>
</pre>
--------------------------------------------------------------------------------------------------------
<pre>
<code>
select 
	CUSTOMER_ID,
	RENTAL_ID,
	RETURN_DATE
from 
	RENTAL
where
	CUSTOMER_ID not in (1,2)			--1혹은 2가 아닌거 == 1과 2를 제외한 나머지 전부
order by RETURN_DATE desc;
 </code>
</pre>
----------------------------------------------------------------------------------------------------------
<pre>
<code>
-- NOT IN 연산자는 'AND' && '<>'과 같다.
select 
	CUSTOMER_ID,
	RENTAL_ID,
	RETURN_DATE
from 
	RENTAL
where 
	CUSTOMER_ID <> 1 and CUSTOMER_ID <>2
order by RETURN_DATE desc;
 </code>
</pre>
----------------------------------------------------------------------------------------------------------
<pre>
<code>
select 	
	CUSTOMER_ID
from 
	RENTAL
where
	cast (RETURN_DATE as DATE) ='2005-05-27'	--RETURN_DATE가 2005년 5월 27일인 CUSTOMER_ID를 출력한다.	
 </code>
</pre>
----------------------------------------------------------------------------------------------------------	
<pre>
<code>
select 	
	FIRST_NAME, LAST_NAME
from 
	CUSTOMER
where 
	CUSTOMER_ID IN(				--RETURN_DATE가 2005년 5월 27일인 CUSTOMER_ID의 FIRST_NAME, LAST_NAME을 출력한다.
					select 
						CUSTOMER_ID
					from
						RENTAL
					where
						cast(RETURN_DATE as DATE) ='2005-05-27');		--RETURN_DATE가 2005년 5월 27일인 CUSTOMER_ID를 출력함
 </code>
</pre>
----------------------------------------------------------------------------------------------------------						
__between 연산자 문법__
<pre>
<code>
--특정 집합에서 어떠한 컬럼의 값이 특정 범위안에 들어가는 집합을 출력하는 연산자
 </code>
</pre>
<pre>
<code>
select 
	*
from 
	TABLE_NAME
where 						--COLUMN_NAME 컬럼의 값이 VALUE_A와 VALUE_B 사이에 있는 집합을 출력한다.
	COLUMN_NAME						
between VALUE_A and VALUE_B;	--즉 COLUMN_NAME은 VALUE_A보다 크거나 같고 VALUE_B보다는 작거나 같다.
 </code>
</pre>
-----------------------------------------------------------------------------------------------------------
<pre>
<code>
select 
	*
from 
	TABLE_NAME
where 						--COLUMN_NAME 컬럼의 값이 VALUE_A와 VALUE_B 사이에 있지 않는 집합을 출력한다.
	COLUMN_NAME						
not between VALUE_A and VALUE_B;	--즉 COLUMN_NAME은 VALUE_A보다 작거나(혹은) VALUE_B보다는 크다.
 </code>
</pre>
-----------------------------------------------------------------------------------------------------------
<pre>
<code>
select 
	CUSTOMER_ID,
	PAYMENT_ID,
	AMOUNT
from 	
	PAYMENT
where AMOUNT between 8 and 9;   --AMOUNT가 8부터9사이인 집합을 출력한다.
 </code>
</pre>
-----------------------------------------------------------------------------------------------------------
<pre>
<code>
select 
	CUSTOMER_ID,
	PAYMENT_ID,
	AMOUNT
from 	
	PAYMENT
where AMOUNT not between 8 and 9;   --AMOUNT가 8부터9사이가 아닌 집합을 출력한다.
 </code>
</pre>
-----------------------------------------------------------------------------------------------------------
<pre>
<code>
select 
	CUSTOMER_ID,
	PAYMENT_ID,
	AMOUNT,
	PAYMENT_DATE
from 	
	PAYMENT
where
	CAST(PAYMENT_DATE as DATE)	-- = TO_CHAR(PAYMENT_DATE,'YYYY--MM--DD')   PAYMENT_DATE가 2007년 2월 7일부터 2007년 2월 15일 데이터를 추출함
	between '2007-02-07' and '2007-02-15';
 </code>
</pre>
------------------------------------------------------------------------------------------------------------
__like 연산자 문법__
<pre>
<code>
--특정 집합에서 어떠한 컬럼의 값이 특정 값과 유사한 패턴을 갖는 집합을 출력하는 연산자
 </code>
</pre>
<pre>
<code>
select 
	*
from 
	TABLE_NAME
where COLUMN_NAME

like 특정패턴			--COLUMN_NAME 컬럼의 값이 특정 패턴과 유사한 집합을 출력한다.
 </code>
</pre>
-------------------------------------------------------------------------------------------------------------
<pre>
<code>
select 
	*
from 
	TABLE_NAME
where COLUMN_NAME
not like 특정패턴			--COLU,N_NAME 컬럼의 값이 특정 패턴과 유사하지 않는 집합을 출력한다.

--특정 패턴에서 '%'는 어떤 문자 혹은 문자열이든지 매칭 되었다고 판단한다.
--특정 패턴에서 '_'는 한개의 문자가 어떤 문자이든지 매칭 되었다고 판단한다.
 </code>
</pre>
-------------------------------------------------------------------------------------------------------------
<pre>
<code>
select 
	FIRST_NAME,
	LAST_NAME
from 
	CUSTOMER
where
	FIRST_NAME like 'Jen%';
 </code>
</pre>
-------------------------------------------------------------------------------------------------------------
<pre>
<code>
select 
	'FOO' like 'FOO',	--true 'FOO'는 'FOO'이므로 참이다
	'FOO' like 'F%',	--'F%'는 'F'로 시작하면 모두 참이다
	'FOO' like '_O_',	--'_O_'는 3자리 문자열이고 가운데 문자가 'O'라면 모두 참이다.
	'BAR' like 'B_'	;	--'B_'는 2자리 문자열이고 'B'로 시작하기만 하면 두번째 문자는 무엇이든 간에 참이다. 하지만 'BAR'는 'B'로 시작하긴 했지만 3자리 이므로 거짓이다.
 </code>
</pre>
-------------------------------------------------------------------------------------------------------------
<pre>
<code>
select 
	FIRST_NAME,
	LAST_NAME
from 	
	CUSTOMER
where
	FIRST_NAME like '%er%'	--FIRST_NAME에 'er'이 존재하는 모든 집합을 출력한다.
</code>
</pre>
-------------------------------------------------------------------------------------------------------------	
<pre>
<code>
select 
	FIRST_NAME,
	LAST_NAME
from 
	CUSTOMER
where
	FIRST_NAME like '_her%'	--첫번째 문자가 어떠한 문자로 시작 가능하지만 그 다음이 'her'이어야 하고 그 다음에는 어떤 문자 혹은 문자열이어도 상관없는 집합이 출력된다.
 </code>
</pre>
--------------------------------------------------------------------------------------------------------------
__is null 연잔자 문법__
<pre>
<code>
-- 특정 컬럼 혹은 값이 널 값인지 아닌지를 판단하는 연산자이다. IS NULL 혹은 IS NOT NULL로 널 유무를 판단한다.

select 
	*
from TABLE_NAME
where COLUMN_NAME is null --COLUMN_NAME 컬럼의 값이 널인 집합을 출력한다.
 </code>
</pre>
----------------------------------------------------------------------------------------------------------------
<pre>
<code>
select 
	*
from TABLE_NAME
where COLUMN_NAME is not null --COLUMN_NAME 컬럼의 값이 널이 아닌 집합을 출력한다.
 </code>
</pre>
----------------------------------------------------------------------------------------------------------------
<pre>
<code>
create table CONTACTS
(
	ID INT generated by default as identity,
	FIRST_NAME VARCHAR(50) not null,
	LAST_NAME VARCHAR(50) not null,
	EMAIL VARCHAR(255) not null,
	PHONE VARCHAR(15),
	primary key (ID)

);

insert 
into
	CONTACTS(FIRST_NAME,LAST_NAME,EMAIL,PHONE)
values
	('Jhon','Doe','john.doe@example.com',NULL),
	('Lily','Bush','lily.bush@example.com','(408-234-2764');
commit;

select 	
	*
from 
	CONTACTS;
 </code>
</pre>
----------------------------------------------------------------------------------------------------------------
<pre>
<code>
select 
	ID,
	FIRST_NAME,
	LAST_NAME,
	EMAIL,
	PHONE
from 
	contacts
where PHONE is null --PHONE컬럼의 값이 NULL인 집합을 출력하고자 한다.
 </code>
</pre>
----------------------------------------------------------------------------------------------------------------
<pre>
<code>
select 
	ID,
	FIRST_NAME,
	LAST_NAME,
	EMAIL,
	PHONE
from 
	contacts
where PHONE is not null --PHONE컬럼의 값이 NULL이 아닌 집합을 출력하고자 한다.
 </code>
</pre>
