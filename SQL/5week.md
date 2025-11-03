# SQL_BASIC 5주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_5th_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**5주차 과제는 문제 풀이를 중심으로**, 강의에서 제시된 예제 문제 중 **3 문제 이상을 선택하여 직접 풀어본 뒤**, 강의 영상의 풀이와 비교해 **틀린 부분, 맞은 부분, 새롭게 배운 개념**을 구체적으로 정리해주세요. (적어도 4문제는 정리해야 합니다.) 완성된 과제는 Gihub에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**(수행 인증샷은 필수입니다.)** 



## SQL_BASIC_5th

### 섹션 5. 데이터 탐색 - 변환

### 4-4. 날짜 및 시간 데이터 이해하기(2) (EXTRACT, DATETIME_TRUNC, PARSE_DATETIME, FROMAT_DATETIME)

### 4-5. 시간 데이터 연습문제 1~2번

### 4-5. 시간 데이터 연습문제 3~5번

### 4-6. 조건문 (CASE WHEN, IF)

### 4-7. 조건문 연습 문제

### 4-8. 정리

### 4-9. BigQuery 공식 문서 확인하는 법

(강의에서 연습문제가 많아서 따로 프로그래머스 문제 과제는 없습니다.)



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | ✅         |
| 4주차 | 섹션 **3-4** ~ **4-4** | ✅         |
| 5주차 | 섹션 **4-4** ~ **4-9** | ✅         |
| 6주차 | 섹션 **5-1** ~ **5-7** | 🍽️         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<br>



<!-- 여기까진 그대로 둬 주세요-->

---

# 4-4. 날짜 및 시간 데이터 이해하기(2) (EXTRACT, DATETIME_TRUNC, PARSE_DATETIME, FROMAT_DATETIME)

~~~
✅ 학습 목표 :
* 날짜 및 시간 데이터에 대해서 더 자세히 설명할 수 있다. 
* CURRENT_TIME, EXTRACT, DATETIME_TRUNC, PARSE_DATETIME, FROMAT_DATETIME 을 설명할 수 있다. 
~~~

### 1. CURRENT_DATETIME
~~~sql
SELECT
 CURRENT_DATE() AS current_date
 CURRENT_DATETIME() AS current_datetime
~~~

### 2. EXTRACT
2024-01-02 14:00:00 중에서 일자별 주문을 뽑고 싶을 때, 일만 추출해서 집계할 수 있음.         
~~~sql     
EXTRACT(part FROM datetime_expression)
~~~
 => part에 시간표현이 들어감     

- week은 sunday부터 시작하는 것이 기본값           
- 요일(평일/주말)         
EXTRACT(DAYOFWEEK FROM datetime_col)              
주말이라면 [1,7] 범위의 값을 반환             
- DATE와 HOUR만 남기고 싶은 경우 => 시간 자르기               
DATETIME_TRUNC(datetime_col, HOUR) => 시간 뒤의 분은 전부 0분으로 바뀜

### 3. PARSE_DATETIME
문자열로 저장된 것을 DATETIME 타입으로 바꾸고 싶은 경우        
PARSE_DATETIME('문자열의 형태', 'DATETIME 문자열')        
~~~sql
SELECT
 PARSE_DATETIME('%Y-%m-%d %H:%M:%S', '2024-01-11 12:35:35') AS parse_datetime;
~~~

### 4. FORMAT_DATETIME
DATETIME 타입을 문자열 데이터로 변환하고 싶은 경우             

### 5. LAST_DAY
마지막 날을 알고 싶은 경우: 자동으로 월의 마지막 값을 계산해서 특정 연산을 할 경우           
~~~sql
LAST_DAY(DATETIME '2024-01-03 15:30:00', WEEK(MONDAY)) AS last_day_week_mon     
~~~

- 원래 디폴트 값은 WEEK(SUNDAY)         
- MONDAY로 바꾸었기 때문에 해당 날짜가 포함된 주의 일요일에 해당하는 날짜가 선택됨.       
*일요일이 기준으로 많이 사용됨.        

### 6. DATETIME_DIFF
두 DATETIME의 차이를 알고 싶은 경우  
~~~sql          
DATETIME_DIFF(첫번째, 두번째, 궁금한 차이)             
~~~




# 4-6. 조건문(CASE WHEN, IF)

~~~
✅ 학습 목표 :
* 조건문 함수의 기능을 이해하고, 설명할 수 있다. 
~~~

### 1. CASE WHEN
: 여러 조건이 있을 경우 사용. 조건의 순서에 주으

<문법>
~~~sql
SELECT
  CASE
    WHEN 조건1 THEN 조건 1이 참일 경우 결과
    WHEN 조건2 THEN 조건 2가 참일 경우 결과
    ELSE 그 외 조건일 경우 결과
  END AS 새로운 컬럼_이름
~~~

<예시>         
Rock(바위) 타입과 Ground(땅) 타입이 결국 비슷 "Rock&Ground"라는 타입을 새로 만들면 어떨까?
~~~sql
SELECT
  new_type1,
  COUNT(DISTINCT id) AS cnt
FROM(
   SELECT
      *,
      CASE
         WHEN (type1 IN ("Rock", "Ground")) OR (type2 IN ("Rock", "Ground")) THEN "Rock&Ground"
       ELSE AS new_type1
   FROM basic.pokemon
)
GROUP BY
 new_type1
~~~

#### *CASE WHEN 순서 
: 첫번째 조건을 먼저 보고 처리를 하기 때문에 중복되는 범위가 존재할 경우 주의해야함!
~~~sql
WHEN attack >= 100 THEN 'Very Strong'
WHEN attack >= 50 THEN 'Strong'
#해당 순서로 조건 작성해야함
~~~
### 2. IF
: 단일 조건일 경우 유용    

<문법>
~~~sql
IF(조건문, True일 때의 값, False일 때의 값) AS 새로운_컬럼_이름
~~~



 # 4-5. 시간 데이터 연습문제 & 4-7. 조건문 연습 문제

~~~
✅ 학습 목표 :
* 4-5, 4-7 각각에서 두 문제 이상 (최소 4문제) 푼 내용 정리하기
~~~

## 4-5 시간 데이터 연습문제

### #1 트레이너가가 포켓몬을 포획한 날짜(catch_date)를 기준으로, 2023년 1월에 포획한 포켓몬의 수를 계산해주세요.            

- 데이터특징             
-- catch_date : DATE 타입                
--catch_datetime : UTC. TIMESTAMP 타입                 
=> 컬럼 이름은 datetime인데 TIMESTAMP 타입으로 저장되어있다! => 컬럼명만 믿고 바로 쿼리 작성 금지                
--catch_date가 UTC 기준인지? KR 기준인지? 확인 필요  
--catch_date != DATE(DATETIME(catch_datetime, "Asia/Seoul")) 
있다면 catch_date는 사용하기 어려울 수 있음.                

### => catch_date, catch_datetime 검증
~~~sql
SELECT
 COUNT(*)
FROM(
SELECT
  id,
  catch_date,
  DATE(DATETIME(catch_datetime, "Asia/Seoul")) AS catch_datetime_kr_date
FROM basic.trainer_pokemon
)
WHERE
  catch_date != catch_datetime_kr_date
~~~
같지 않은 경우 141건, 같은 경우는 238건!     
따라서 catch_date 사용 불가능


### #1 문제풀이
~~~sql
SELECT
 COUNT(DISTINCT id) AS cnt
FROM basic. trainer_pokemon
WHERE
 EXTRACT(YEAR FROM DATETIEM(catch_datetiem, "Asia/Seoul")) = 2023 #catch_datetime은 TIMESTAMP로 저장되어 있으므로, DATETIME으로 변경해야 함
 AND EXTRACT(MONTH FROM DATETIME(catch_datetime, "Asia/Seoul")) =1
~~~

### #2 배틀이 일어난 시간을 기준으로, 오전 6시에서 오후 6시 사이에 일어난 배틀의 수를 계산해주세요.
- 데이터 특징          
--battle_date : battle_datetime 기반으로 만들어진 DATE                  
--battle_datetime : DATETIME           
--battle_timestamp : TIMESTAMP              
--battle_datetime이랑 DATETIME(battle_timestamp, "Asia/Seoul") 같은지 확인!
### => battle_datetime, battle_timestamp 검증
~~~sql
SELECT
 COUNTIF(battle_datetime = DATETIME(battle_timestamp, "Asia/Seoul")) AS same_timestamp_kr
 COUNTIF(battle_datetime != DATETIME(battle_timestamp, "Asia/Seoul")) AS not_same_timestamp_kr
FROM basic.battle
~~~
battle_datetime, battle_timestamp 같다!

### #2 첫번째 풀이
~~~sql
SELECT
 COUNT(DISTINCT id) AS battle_cnt
FROM basic.battle
WHERE
 EXTRACT(HOUR FROM battle_datetime) >=6
 AND EXTRACT(HOUR FROM battle_datetime) <= 18
~~~

### #2 두번째 풀이
~~~sql
SELECT
 COUNT(DISTINCT id) AS battle_cnt
FROM basic.battle
WHERE
 EXTRACT(HOUR FROM battle_datetime) BETWEEN 6 and 18
~~~

#### 시간대별로 몇 건이 있는가?
~~~sql
SELECT
 hour,
 COUNT(DISTINCT id) AS battle_cnt
FROM (
  SELECT
     *,
     EXTRACT(HOUR FROM battle_datetime) AS hour
  FROM basic.battle
)
GROUP BY
 hour
ORDER BY
 hour
~~~
## 4-7 조건문 연습 문제
### #1 포켓몬의 'Speed'가 70이상이면 '빠름', 그렇지 않으면 '느림'으로 표시하는 새로운 컬럼 'Speed_Category'를 만들어주세요.
~~~sql
SELECT
  *,
  IF (speed >=70, "빠름", "느림") AS Speed_Category
FROM basic.pokemon
~~~

### #3 각 포켓몬의 총점(total)을 기준으로, 300이하면 'Low', 301에서 500 사이면 'Medium', 501 이상이면 'High'로 분류해주세요.
~~~sql
SELECT
  *
FROM( 
SELECT
  id,
  kor_name,
  total,
  CASE
    WHEN total >=501 THEN "High"
    WHEN total BETWEEN 301 AND 500 THEN "Medium"
  ELSE "Low"
  END AS total_grade  
FROM basic.pokemon
)
WHERE
  total_grade = "Low"
~~~

#### 이렇게 적으면 오답이다.
~~~sql
SELECT
  id,
  kor_name,
  total,
  CASE
    WHEN total >=501 THEN "High"
    WHEN total BETWEEN 301 AND 500 THEN "Medium"
  ELSE "Low"
  END AS total_grade  
FROM basic.pokemon
WHERE
  total_grade = "Low"
#Unrecognized name : total_grade. 컬럼의 이름을 인지할 수 없다. 컬럼이 없다.
~~~
## 수행 인증샷
![alt text](<5week 수행인증.PNG>)
<br>

<br>

---

# 확인문제

## 문제 1

> **🧚Q. 광윤이는 사용자 로그 데이터에서, 2021년에 접속한 사용자 수를  집계하려고 했습니다. 그는 여러 SQL 쿼리들을 실행해봤지만, 그 중 일부는 문법적으로 잘못되어 실행되지 않았습니다. 다음 보기 중 틀린 쿼리를 모두 골라보세요 (복수 선택 가능)**

~~~sql
1. SELECT COUNT(*)  
   FROM user_log  
   WHERE EXTRACT(YEAR FROM login_date) = 2021;

2. SELECT EXTRACT(YEAR FROM login_date), COUNT(*)  
   FROM user_log  
   GROUP BY EXTRACT(YEAR FROM login_date);

3. SELECT COUNT(*)  
   FROM user_log  
   WHERE login_date = '2021';

4. SELECT COUNT(*)  
   FROM user_log  
   WHERE login_date BETWEEN '2021-01-01' AND '2021-12-31';
~~~

<!-- 틀린쿼리에 대한 오류의 원인도 같이 작성해주세요. 문제에서 제공된 login_data 컬럼은 DATE type의 데이터를 가지고 있다고 가정하시면 됩니다. -->

~~~
3번
이유 : '2021'은 DATE type이 아닌 문자열이기 때문이다.
~~~



## 문제 2

> **🧚Q. 혜성이는 포켓몬 타입에 따라 설명을 부여하는 쿼리를 작성했습니다. type 1 컬럼의 값에 따라 조건을 분기했으며, 다음 SQL 쿼리를 실행했습니다.**

~~~sql
SELECT name,
       CASE 
         WHEN type1 = 'Fire' THEN 'Hot'
         WHEN type1 = 'Water' THEN 'Cool'
         ELSE 'Normal'
       END AS type_description
FROM pokemon;
~~~

> **다음 중 type_description의 결과가 'Normal'로 출력될 포켓몬은?**

| **name**   | **type1** |
| ---------- | --------- |
| Pikachu    | Electric  |
| Charmander | Fire      |
| Squirtle   | Water     |
| Bulbasaur  | Grass     |

<!-- 근거와 함께 답을 작성해주세요 -->

~~~
Pikachu, Bulbasaur
이유 : CASE WHEN 문법에 따라 Charmander은 'Hot', Squirtle은 'Cool'로 출력되고 타입이 'Fire'나 'Water'이 아닌 경우에 'Normal'이 출력된다.
~~~



<br>

### 🎉 수고하셨습니다.