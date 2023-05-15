# 개요

## SQL Injection이란?
- 임의의 SQL문을 주입하여 데이터 베이스의 비정상적 동작을 유도하는 것을 말함
- 악의적인 사용자가 보안상 취약점을 이용하여 데이터베이스를 공격할 때 주로 사용
- 공격이 쉬운 편에 속하는 데에 비해, 피해가 큰 편
>2017.3에 일어난 여기어때의 대규모 개인 정보 유출 또한 SQL Injection으로 발생

<br><br>

# SQL Injection의 종류

## Error based SQL Injection
- 논리적 에러를 이용한 SQL Injection
- 가장 많이 쓰이고 대중적인 공격 기법
```SQL
-- 원래 구문
SELECT * FROM Users WHERE id = 'INPUT1' AND password = 'INPUT2'

-- 공격자가 추가하는 구문
OR 1-1 --

-- 결과물
SELECT * FROM Users WHERE id = 'INPUT1' OR 1=1 -- AND password = 'INPUT2'
```
>`AND password = 'INPUT2'`부분은 주석처리  
>OR 1=1로 인해 `WHERE`절은 무조건 `TRUE` 처리  
>결과적으로 Users 테이블에 있는 모든 정보를 조회하게 됨
<br>

## Union based SQL Injection
- Union 명령어를 이용한 SQL Injection
- 두 개의 쿼리문에 대한 결과르 통합해서 하나의 테이블로 보여주게 하는 키워드
```SQL
-- 원래 구문
SELECT * FROM Board WHERE title LIKE '%INPUT%'

-- 공격자가 추가하는 구문
'UNION SELECT null, id, password FROM Users-- 

-- 결과물
SELECT * FROM Board WHERE title LIKE '%' UNION SELECT null, id, password FROM Users -- INPUT%'
```
>`INPUT%'`부분은 주석처리  
>`LIKE '%'` 로 인해 title 조건 없이 모두 조회  
>`UNION SELECT null, id, password FROM Users`로 인해 유저 정보 또한 같이 조회
<br>

## Blind SQL Injection
- 서버로부터 특정한 응답 대신 참, 거짓 응답만을 알 수 있을 때 데이터 베이스 정보를 유추하는 기법

### Boolean based SQL
- 로그인 성공과 로그인 실패 메시지 같은 부가 정보를 이용
- 테이블 정보등 데이터 베이스 관련 정보들을 유추 혹은 추출
```SQL
-- 원래 구문
SELECT * FROM Users WHERE id = 'INPUT1' AND password = 'INPUT2'

-- 공격자가 추가하는 구문 
abc123' and { 테이블명의 첫번째 글자가 임의의 알파벳과 같은지 확인하는 코드 } -- 

-- 결과물
SELECT * FROM Users WHERE id = 'abc123' and { 테이블명의 첫번째 글자가 임의의 알파벳과 같은지 확인하는 코드 } -- INPUT1' AND password = 'INPUT2'
```
>공격자가 임의의 ID로 회원가입한 후 공격에 사용  
>로그인 될 때까지 임의의 알파벳을 교체  
>만약 `U`에서 로그인이 되었다면 테이블명의 첫번째 글자는 U

### Time Based Injection
- 참, 거짓값을 명시적으로 반환받을 수 없을 때 사용
- 참, 거짓에 따른 특정 함수를 시행 후 결과를 보고 참 거짓을 유추
- 대표적으로 `SLEEP()` 같은 함수를 사용
```SQL
-- 원래 구문
SELECT * FROM Users WHERE id = 'INPUT1' AND password = 'INPUT2'

-- 공격자가 추가하는 구문 
abc123' and (LENGTH(DATABASE())=1 AND SLEEP(2)) --

-- 결과물
SELECT * FROM Users WHERE id = 'abc123' and (LENGTH(DATABASE())=1 AND SLEEP(2)) -- INPUT1' AND password = 'INPUT2'
```
>공격자가 데이터베이스 길이를 추측할 수 있는 코드  
>`--`뒤의 구문은 주석 처리  
>만약 `=1`부분의 숫자를 바꿔가며 true, false를 반환받음  
>만약 true라면 `SLEEP(2)` 함수가 실행됨

<br><br>

# 대응 방안

## 입력 값에 대한 검증
- SQL Injection에서 사용되는 기법과 키워드는 그 종류가 매우 많음
- 서버쪽에서 화이트리스트 기반 검증이 필요
- 공백 치환 : 많이 쓰이지만 취약한 방법
>예를 들면 SESELECTLECT란 커맨드가 입력되었다고 치자  
>여기서 중간 SELECT를 공백으로 치환해도 SELECT가 됨  
>그러므로 공격키워드와 의미없는 단어로 치환할 필요가 존재

## Prepared Statement 구문 사용
- 바인드 변수 부분을 DBMS의 캐시에 준비되어있는 쿼리를 사용
>여기서 바인드 변수부분을 파라미터라고 이해해도 좋을 것 같습니다.
- 공격 쿼리가 들어간다 해도, 사용자의 입력은 이미 의미없는 단순 문자열
- 전체 쿼리문도 공격자의 의도대로 작동 X

## Error Message 노출 금지
- SQL Injection 수행을 위해선 데이터베이스 정보가 필요
- 에러 발생 처리를 따로 하지 않으면 에러 내용 반환에서 테이블명, 컬럼명, 쿼리문이 노출 가능

## 웹 방화벽 사용
- 웹 공격 방어에 특화되어있는 웹 방화벽 사용

<br><br>

## 참고 문서
[NoirStar Space](https://noirstar.tistory.com/264)
[익스플로의 아카이브](https://iksflow.tistory.com/127)
[shionista의 보안블로그](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=is_king&logNo=221402635339)
