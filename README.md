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

