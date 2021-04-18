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
