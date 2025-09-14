# SQL_BASIC 2주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_2nd_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**2주차 과제**는 1주차 과제처럼 SQL의 필요성이나 느낀점 위주가 아닌, **실제 강의 내용을 바탕으로 개념을 정리하고 학습한 내용을 집중적으로 기록**해주세요. 완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요. 

**👀(수행 인증샷은 필수입니다.)** 

## SQL_BASIC_2nd

### 섹션 3. 데이터 탐색 - 조건, 추출, 요약

### 2-3. 데이터 탐색 (SELECT, FROM, WHERE)

### 2-4. SELECT 연습문제

### 2-5. 집계 (Group By + Having + Sum/Count)



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | 🍽️         |
| 4주차 | 섹션 **3-4** ~ **4-4** | 🍽️         |
| 5주차 | 섹션 **4-4** ~ **4-9** | 🍽️         |
| 6주차 | 섹션 **5-1** ~ **5-7** | 🍽️         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 개념정리 

## 2-3. 데이터 탐색 (SELECT, FROM, WHERE)

~~~
✅ 학습 목표 :
* SQL 쿼리 구조를 이해할 수 있다. 
* SELECT, FROM, WHERE의 핵심 문법을 설명할 수 있다. 
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
SELECT  #테이블의 어떤 컬럼을 선택(출력)할 것인가?    
  COL1 AS new_name,  #별칭으로 바꾸겠다    
  COL2,    
  COL3    
FROM Dataset.Table  #어떤 테이블에서 데이터를 확인할 것인가?    
WHERE  #만약 원하는 조건이 있다면 어떤 조건인가?   
  Col1=1 : 조건문   

SQL 쿼리 구조: SELECT - FROM - WHERE    
실행 순서 : FROM - WHERE - SELECT    

SELECT    
'*' #모든 컬럼을 출력하겠다 /  *EXCEP(제외할 컬럼)   
FROM basic.pokemon   
WHERE   
  type1="Fire"   

빅쿼리인 경우 *을 처음부터 사용하지 않음. 비용이 많이 듦. 보통은 미리보기 기능을 활용해 데이터 확인함.   
 
FROM 'inflearn-bigquery.basic.pokemon'   
inflearn-bigquery: 프로젝트 id   
basic: dataset   
pokemon: table   
'<프로젝트 id>, <데이터셋>, <테이블>'   
프로젝트 id는 꼭 명시할 필요는 없을 수도 있음(프로젝트가 단일이라면!)   
프로젝트를 여러개 사용한다면 명시하는 것이 좋음 -> 쿼리를 실행할 때 어떤 프로젝트인지 확인하는 과정이 존재   
프로젝트 id 제외한다면 작성할 때 ' ' 없어도 괜찮음.   

*데이터를 활용하고 싶은 목적이 있어야, 어떤 컬럼을 선택할지 알 수 있게 됨.   

주석처리 -- 또는 #       
AS 컬럼 이름에 따옴표 " " 금지 !    
마지막에 ; 은 쿼리가 끝났음을 의미함    


## 2-5. 집계 (Group By / HAVING / SUM,COUNT)

~~~
✅ 학습 목표 :
* 데이터를 집계하고 그룹화하는 방법을 설명할 수 있다.
* GROUP BY, HAVING, ORDER BY, 집계함수(SUM/COUNT 등)을 활용하는 방법을 설명할 수 있다.
* having과 where의 차이에 대해서 설명할 수 있다.
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
[1] GROUP BY + 집계 함수(AVG, MAX): 집계하다= 모아서(그룹화해서) 계산하다   
계산   
-더하기, 빼기   
-최대값, 최소값   
-평균   
-갯수 세기   

SELECT   
 집계할_컬럼1   
 집계 함수(COUNT, MAX, MIN)   
FROM Table   
GROUP BY   
 집계할_컬럼1(기준컬럼)   

집계할 컬럼을 SELECT에 명시하고 그 컬럼을 꼭 GROUP BY에 작성   

[2] DISTINCT: 중복의 제거하고 unique한 것만 보여줌.   
1,2,3,3,4 => DISTINCT 하면 => 1,2,3,4   
COUNT(DISTINCT 컬럼) 형태로 많이 씀   
메인 페이지 VIEW 수는? COUNT(user_id)    
메인 페이지 VIEW한 유저의 수는? COUNT(DISTINCT user_id)   

-일자별 집계(원본 데이터는 특정 시간에 어떤 유저가 한 행동이 기록, 일자별로 집계)    
-연령대별 집계(특정 연령대에서 더 많이 구매했는가?)    
-특정 타입별 집계(특정 제품 타입을 많이 구매했는가?)    
-앱 화면별 집계(어떤 화면에 유저가 많이 접근했는가?)   
조합=> 일자별+제품 타입별 판매량 / 매출   
date, product_type => COUNT / SUM(revenue)   

[3] WHERE: 조건을 설정하고 싶은 경우 /HAVING 비교     

WHERE: Table에 바로 조건을 설정하고 싶을 때 사용    
HAVING: GROUP BY한 후 조건을 설정하고 싶은 경우 사용=집계를 하면서 생성된 컬럼에 조건을 달고 싶을 때 사용     (서브쿼리 사용 대신 간단하게 사용할 수 있음)   

서브쿼리: SELECT 문 안에 존재하는 SELECT쿼리   

[4] ORDER BY: 정렬하기    
쿼리의 맨 마지막에 작성   
ORDER BY <컬럼> <순서>    
순서: DESC(내림차순), OSC(오름차순-기본값)   

[5] LIMIT:  출력 개수 제한하기    
쿼리문 가장 마지막에 작성 (ORDER BY보다 마지막)    


# 2️⃣ 학습 인증란

<!-- 이 글을 지우고, 여기에 학습한 것을 인증해주세요.-->
![alt text](<학습인증 week2-2-1.PNG>)

![alt text](<학습인증 week2-1.PNG>)
<br><br>



---

# 3️⃣ 확인문제

## 문제 1

> **🧚Q. 포켓몬 마스터 승화는 포켓몬 데이터 조회하는 SQL문에 재미를 느껴서 혼자서 데이터를 조회하는 쿼리문을 짰습니다. 하지만 세 가지의 오류로 다음 코드가 실행이 안된다고 하는데, 각 오류의 위치와 이유를 설명하고, 올바른 쿼리문으로 수정해보세요.**

~~~sql
# 승화의 SQL Query문 
SELECT name AS '포켓몬 이름', ID;
WHERE type = 'Electric';
FROM pokemon;
~~~


~~~
SELECT   
 name AS 포켓몬 이름,   
 ID,
 type
FROM pokemon
WHERE type = 'Electric';

1. AS 컬럼명에 ' ' 없어야 함.
2. 쿼리문 마지막에만 ; 이 있어야 함.
3. SELECT - FROM - WHERE 순서로 작성해야함.
~~~



## 문제 2

> **🧚Q. 앞서 SQL Query의 오류를 해결한 승화는 기분 좋게 이번에는 포켓몬 데이터에서 타입별 평균 공격력이 60 이상인 타입만 조회하려는 쿼리를 작성하려고 했습니다. 하지만 이번에도 실수를 하여 쿼리문이 실행되지 않거나 잘못된 결과가 나오고 있는데, 쿼리에서 잘못된 부분이 무엇인지 설명하고, 올바르게 수정한 쿼리를 작성해보세요.**

~~~sql
SELECT type, AVG(attack) AS avg_attack
FROM pokemon
WHERE AVG(attack) >= 60
GROUP BY type;
~~~



~~~
SELECT
 type,
 AVG(attack) AS avg_attack
FROM pokemon
GROUP BY 
 type
HAVING avg_attack >=60

1. 집계한 후 조건을 설정하였으므로 GROUP BY가 아닌 HAVING을 써야함.
2. AVG(attack)을 avg_attack으로 정의하였으므로 avg_attack >=60 으로 표현해야함.
3. SELECT - FROM - GROUP BY - HAVING 순서로 작성해야함.
~~~



### 🎉 수고하셨습니다.