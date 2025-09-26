# SQL_BASIC 4주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_4th_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**4주차 과제부터는 강의 내용을 정리하는 것과 함께, 프로그래머스에서 제공하는 SQL 문제를 직접 풀어보는 실습도 병행합니다.** 강의에서는 **배운 내용을 정리하고 주요 쿼리 예제를 정리**하며, 프로그래머스 문제는 **직접 풀어본 뒤 풀이 과정과 결과, 배운 점을 함께 기록**해주세요. 완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**(수행 인증샷은 필수입니다.)** 

## SQL_BASIC_4th

### 섹션 4. 쿼리 잘 작성하기, 쿼리 작성 템플릿 및 오류를 잘 디버깅하기

### 3-4. 오류를 잘 디버깅하는 방법



## 섹션 5. 데이터 탐색 - 변환

### 4-1. INTRO

### 4-2. 데이터 타입과 데이터 변환(CAST, SAFE_CAST)

### 4-3. 문자열 함수(CONCAT, SPLIT, REPLACE, TRIM, UPPER)

### 4-4. 날짜 및 시간 데이터 이해하기(1) (타임존, UTC, Millisecond, TIMESTAMP/DATETIME)



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | ✅         |
| 4주차 | 섹션 **3-4** ~ **4-4** | ✅         |
| 5주차 | 섹션 **4-4** ~ **4-9** | 🍽️         |
| 6주차 | 섹션 **5-1** ~ **5-7** | 🍽️         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 개념정리

## 3-4. 오류를 디버깅하는 방법

~~~
✅ 학습 목표 :
* 오류의 정의에 대해 설명할 수 있다. 
* 오류 메시지를 보고 디버깅이라는 과정을 수행할 수 있다. 
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->

### Syntax Error
문법을 지키지 않아 생기는 오류   

1. 
~~~
SELECT
 col => 이 부분이 비어있기에 생기는 오류
FROM
~~~
Syntax Error: SELECT list must not be empty at [10:1]    
SELECT 목록은 [10:1] 에서 비어 있으면 안된다.    
**[10:1] : [줄:칸]**

2.
~~~
SELECT
 COUNT(id, kor_name)
FROM basic.pokemon
~~~
Syntax Error: Number of arguments does not match for aggregate function COUNT   
집계함수 COUNT의 인자 수가 일치하지 않습니다.   
**COUNT(1개)**

3.
~~~
SELECT
 type1,
 COUNT(id) AS cnt
FROM basic. pokemon
~~~

Syntax Error: SELECT list expression references column tpe1 a which is neither grouped nor aggregated    
SELECT 목록 식은 다음에서 그룹화되거나 집계되지 않은 열을 참조합니다.    
**GROUP BY에 적절한 컬럼을 명시하지 않았을 경우 발생하는 오류**

4.
~~~
SELECT
 type1,
 COUNT(id) AS cnt
FROM basic.pokemon
GROUP BY
 type1

SELECT
 *
FROM basic. trainer
~~~
Syntax error: Expected end of input but got keyword SELECT    
입력이 끝날것으로 예상되었지만 SELECT 키워드가 입력되었습니다.    
**쿼리가 끝나는 부분에 ; 붙이고 실행할 부분만 드래그 앤 드랍해서 실행하기**

5.
~~~
SELECT
 *
FROM basic.trainer LIMIT 1000
WHERE 
 id=3
~~~
Syntax error: Expected end of input ut got keyword WHERE at [5:1]    
입력이 끝날 것으로 예상되었지만 [5:1]에서 키워드 WHERE 을 얻었습니다.    
**LIMIT 1000 은 맨 마지막에 위치**

6.
~~~
SELECT
 name,
FROM(
 SELECT
  *
 FROM basic.trainer
 WHERE
  id=3
~~~
Syntax error: Expexted ")" but got end of script at [8: 11]    
")"가 예상되지만 [8:11]에 스크립트가 끝났습니다.     
**(괄호) 열고 닫고 확인하기**


## 4-2. 데이터 타입과 데이터 변환(CAST, SAFE_CAST)

~~~
✅ 학습 목표 :
* 데이터 타입의 종류를 설명할 수 있다. 
* 데이터 타입을 변환하는 방법을 설명할 수 있다. 
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
### 변환을 위한 함수

#### 데이터 타입
숫자   
문자   
시간/날짜      
부울(Bool): 참/거짓 *(*TRUE/FALSE가 문자타입인 경우가 있으니 주의*)*

#### 데이터 타입이 중요한 이유
- 엑셀의 빈 값이 "", NULL 일수도 있음   
- 1이라는 값이 숫자1, 문자1일 수도 있음   
- 2023-12-31 라는 값이 시간/날짜 일수도 있고 문자일수도 있음     

**=> 데이터 타입이 내 생각과 다른 경우 CAST (SAFE_CAST) 함수 사용**
~~~
SELECT
 CAST(1 AS STRING) #숫자 1을 문자 1로 변경
~~~
~~~
SELECT
 SAFE_CAST("카일스쿨" AS INT64)

#결과값은 null     
#카일스쿨이 숫자가 될 수 없기 때문
~~~




#### 수학함수(평균, 표준편차, 코사인 등)
Tip!   
x/y 대신 **SAFE_DIVIDE(x, y)**   
x, y중 하나라도 0인 경우 나누면 zero error가 발생하기 때문에 SAFE_DIVIDE 함수 사용하기



## 4-3. 문자열 함수(CONCAT, SPLIT, REPLACE, TRIM, UPPER)

~~~
✅ 학습 목표 :
* 문자열 함수들의 종류를 이해하고 어떠한 상황에서 사용하는지 설명할 수 있다. 
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->

### 1. 문자열 붙이기 => CONCAT
~~~
SELECT
 CONCAT("안녕", "하세요", "!") AS result;
~~~
=> 안녕하세요!   
=> FROM 없이도 실행   

### 2. 문자열 쪼개기 => SPLIT
~~~
SELECT
 SPLIT("가, 나, 다, 라", ", ") AS result
~~~
=> 가 나 다 라
(배열 ARRAY)

### 3. 특정 단어 수정하기 => REPLACE
~~~
SELECT
 REPLACE("안녕하세요", "안녕", "실천") AS result
 ~~~
=> 실천하세요

### 4. 문자열 자르기=> TRIM
~~~
SELECT
 TRIM("안녕하세요", "하세요") AS result
~~~
=> 안녕

 
### 5. 영어 소문자를 대문자로 변경 => UPPER
~~~
SELECT
 UPPER("abc") AS result
 ~~~
=>ABC



## 4-4. 날짜 및 시간 데이터 이해하기(1) (타임존, UTC, Millisecond, TIMESTAMP/DATETIME)

~~~
✅ 학습 목표 :
* 날짜 및 시간 데이터 타입과 UTC의 개념을 설명할 수 있다. 
* DATE, DATETIME, TIMESTAMP 에 대해서 설명할 수 있다.
* 시간함수들의 종류와 시간의 차이를 추출하는 방법을 설명할 수 있다. 
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
### 날짜 및 시간데이터
- 날짜 및 시간 데이터 타입 파악하기   
: DATE, DATETIME(시간만), TIMESTAMP
- 날짜 및 시간 데이터 관련 알면 좋은 내용   
: UTC, Millisecond
- 날짜 및 시간 데이터 타입 변환하기   
- 시간 함수(두 시간의 차이, 특정 부분 추출하기)   

### 타임존
1. GMT: Greenwich Mean Time(한국 시간:GMT+9)   

2. UTC: Universal TIme Coordinated (한국시간: UTC +9)   
- 타임 존이 존재한다 = 특정 지역의 표준 시간대   

### TIMESTAMP
- 시간 도장
- UTC부터 경과한 시간을 나타내는 값
- Time Zone 정보 있음
~~~
SELECT
 TIMESTAMP_MILLIS(1704176819711) AS milli_to_timestamp_value,
 TIMESTAMP_MICROS(1704176819711000) AS micro_to_timestamp_value,
 ~~~
 ~~~
DATETIME(TIMESTAMP_MIRCROS(1704176819711000) AS datetime_value,
DATETIME(TIMESTAMP_MILLIS(1704176819711) AS datetime_value;
~~~

#### TIMESTAMP와 DATETIME 비교
**DATETIME에는 타임존이 들어가 있어야함.**
~~~
DATETIME(TIMESTAMP_MIRCROS(1704176819711000), 'Asia/Seoul') datetime_value;
~~~
=> 결과: 시차가 보정된 시각을 보여줌.

##### EX)24년 1월 18일 20시 55분(한국시간)에 실행
~~~
SELECT
 CURRENT_TIMESTAMP() AS timestamp_col,
 DATETIME(CURRENT_TIMESTAMP(), 'ASIA/SEOUL") AS datetime_col
~~~

| 구분  | TIMESTAMP              | DATETIME |
| ------- | ---------------------| --------- |
| 타임존   | UTC가 나옴  | T가 나옴(TIME의미)|
| 시간차이 | 결과로 나온 시각에 -9시간 해야함| 한국시간과 동일  |
<br>

<br>

---

# 2️⃣ 확인문제 & 문제 인증

## 학습 인증
![alt text](<SQL 4week 학습인증.PNG>)   

## 프로그래머스 문제 

> 조건에 맞는 회원 수 구하기 (SELECT, COUNT) 
>
> **먼저 문제를 풀고 난 이후에 확인 문제를 확인해주세요**
>
> 문제 링크 
>
> :  https://school.programmers.co.kr/learn/courses/30/lessons/131535#

<!-- 문제를 풀기 위하여 로그인이  필요합니다. -->

<!-- 정답을 맞추게 되면, 정답입니다. 라는 칸이 생성되는데 이 부분을 캡처해서 이 주석을 지우시고 첨부해주시면 됩니다. --> 

![alt text](<SQL 4week 정답.PNG>)

## 문제 1

> **🧚Q. 프로그래머스 문제를 풀던 서현이는 여러 번의 시행착오 끝에 결국 혼자 해결하기 어려워 오류 메시지를 공유하며 도움을 요청했습니다. 여러분들이 오류 메시지를 확인하고, 해당 SQL 쿼리에서 어떤 부분이 잘못되었는지 오류 메시지를 해석하고 찾아 설명해주세요.**

~~~sql
# 조건에 맞는 회원 수 구하기 (SELECT, COUNT) 
# 서현이의 SQL 첫 번째 풀이
SELECT COUNT(AGE, JOINED)
FROM USER_INFO
WHERE AGE BETWEEN 20 AND 29
  AND JOINED BETWEEN '2021-01-01' AND '2021-12-31';
  
오류 메시지 : Error: Number of arguments does not match for aggregate function COUNT
 
# 수정하고 난 이후 두 번째 풀이
SELECT AGE, COUNT(*)
FROM USER_INFO
WHERE AGE BETWEEN 20 AND 29
  AND JOINED BETWEEN '2021-01-01' AND '2021-12-31';
  
오류 메시지 : SELECT list expression references column AGE which is neither grouped nor aggregated
~~~



~~~
1. 집계함수 COUNT의 인자 수가 일치하지 않습니다.   
=> COUNT(1개) 
2. SELECT 목록 식은 다음에서 그룹화되거나 집계되지 않은 열을 참조합니다.   
=> SELECT 문에 AGE를 작성했다면 GROUP BY문으로 AGE를 어떻게 그룹지을지 설정해주어야한다. 이 쿼리문의 SELECT에는 AGE를 포함시킬 이유가 없다.
~~~



### 🎉 수고하셨습니다.