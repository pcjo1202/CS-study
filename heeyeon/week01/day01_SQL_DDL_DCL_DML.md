<link rel="stylesheet" href="../style.css">

# SQL

<details>
<summary>1. DDL</summary>

<br/>

> Data Define Language, 데이터 정의어
>
> 개념 : DB를 구축하거나 수정할 목적으로 사용하는 언어 (DB 구조, 데이터 형식 등)

<br/>

### 1) CREATE

```sql
CREATE SCHEMA 대학교 AUTHORIZATION 홍길동;
```
**스키마**
- DB 구조, 제약 조건에 대한 전반 명세를 기술한 것
- 개체(Entity), 속성(Attribute), 관계(Relationship) 등

<br/>

```sql
CREATE DOMAIN SEX CHAR(1)
        DEFAULT '남'
        CONSTRAINT VALID-SEX CHECK(VALUE IN('남', '여'));
```

**도메인**
- 하나의 속성이 취할 수 있는 동일한 유형의 원자 값 집합 (사용자 정의 데이터 타입)

<br/>

```sql
CREATE TABLE 학생
    (이름 VARCHAR(15) DEFAULT 홍길동 NOT NULL,
    학번 CHAR(8) PRIMARY KEY,
    전공 CHAR(5),
    성별 SEX,
    생년월일 DATE, 
    UNIQUE(대체키_속성명),
    CONSTRAINT fk_전공 FOREIGN KEY(전공) REFERENCES 학과(학과코드)
        ON DELETE SET NULL
        ON UPDATE CASCADE,
    CONSTRAINT 생년월일제약
        CHECK(생년월일 >= '1980-01-01'));
```

<br/>

```sql
CREATE VIEW CC(ccid, ccname)
AS SELECT Course.id, Instructor.name
FROM Course, Instructor
WHERE Course.instructor = Instructor.id;
```

<br/>

```sql
CREATE UNIQUE INDEX 고객번호_idx
ON 고객(고객번호 DESC, 주문번호 ASC);
```

<br/>

### 2) ALTER

```sql
ALTER TABLE 학생 ADD 학년 VARCHAR(3) DEFAULT '기본값';

ALTER TABLE 학생 ALTER 학번 VARCHAR(10) NOT NULL;

ALTER TABLE 학생 ALTER 학번 SET DEFAULT '기본값';

ALTER TABLE 학생 DROP COLUMN 학번 CASCADE;
```

<br/>

### 3) DROP

```sql
DROP SCHEMA 스키마명 [CASCADE | RESTRICT];

DROP DOMAIN 도메인명 [CASCADE | RESTRICT];

DROP TABLE 테이블명 [CASCADE | RESTRICT];

DROP VIEW 뷰명 [CASCADE | RESTRICT];

DROP INDEX 인덱스명 [CASCADE | RESTRICT];

DROP CONSTRAINT 제약조건명;
```

<br/>

</details>



<details>
<summary>2. DCL</summary>

<br/>

> Data Control Language, 데이터 제어어
>
> 개념 : 데이터 보안, 무결성, 회복, 병행 제어 등 정의하는 데 사용하는 언어

<br/>

### 1) COMMIT

> 개념 : 트랜잭션 처리 정상 완료 후, 트랜잭션이 수행한 내용을 DB에 반영하는 명령어
>
> **Auto Commit** : DML문이 성공하면 자동 COMMIT / 실패하면 자동 ROLLBACK

<br/>

### 2) ROLLBACK

> 개념 : 변경되었으나 아직 COMMIT 되지 않은 모든 내용 취소, DB를 이전 상태로 복구하는 명령어
>
> **SAVE POINT** : 트랜잭션 내에 ROLLBACK 할 위치인 저장점을 지정하는 명령어

```sql
DELETE FROM 사원 WHERE 사원번호 = 30;
SAVEPOINT S1;

DELETE FROM 사원 WHERE 사원번호 = 20;
ROLLBACK TO S1;
```

<br/>
<br/>

> 💡 **TCL(Transaction Control Language, 트랜잭션 제어 명령어)**
>
> `COMMIT`, `ROLLBACK`, `SAVEPOINT`
>
> 트랜잭션 단위로 데이터 변경을 제어하는 명령어로, 데이터 일관성과 복구 가능성을 보장
>
> - `COMMIT` : 작업 확정하여 DB에 반영
> - `ROLLBACK` : 변경 내용을 취소하고 이전 상태로 복원
> - `SAVEPOINT` : 트랜잭션 내 되돌릴 지점을 임시로 저장

<br/>

### 3) GRANT / REVOKE

**사용자등급 지정/해제**
```sql
GRANT 사용자등급 TO 사용자_ID_리스트;
GRANT RESOURCE TO NABI;

REVOKE 사용자등급 FROM 사용자_ID_리스트;
REVOKE RESOURCE FROM NABI;
```

> **사용자등급**
> - DBA : DB 관리자
> - RESOURCE : DB 및 테이블 생성 가능자
> - CONNECT : 단순 사용자

<br/>

**테이블/속성 권한 부여/취소**
```sql
GRANT 권한_리스트 ON 개체 TO 사용자 [WITH GRANT OPTION];
GRANT ALL ON 고객 TO NABI WITH GRANT OPTION;

REVOKE [GRANT OPTION FOR] 권한_리스트 ON 개체 FROM 사용자 [CASCADE];
REVOKE GRANT OPTION FOR UPDATE ON 고객 FROM NABI;
```

> **권한 리스트**
> - ALL / SELECT / INSERT / UPDATE / DELETE

<br/>

</details>



<details>
<summary>3. DML</summary>

<br/>

> Data Manipulation Language, 데이터 조작어
>
> 개념 : DB 사용자가 저장된 데이터를 실질적으로 관리하는 데 사용되는 언어 (데이터 조작)

<br/>

### 1) INSERT

```sql
INSERT INTO 사원(이름, 부서)
VALUES ('홍승현', '인터넷');

INSERT INTO 편집부원(이름, 생일, 주소, 기본급)
SELECT 이름, 생일, 주소, 기본급
FROM 사원
WHERE 부서 = '편집';
```

<br/>

### 2) DELETE

```sql
DELETE FROM 사원
WHERE 이름 = '임꺽정';
```

<br/>

### 3) UPDATE

```sql
UPDATE 사원
SET 부서 = '기획', 기본급 = 기본급 + 5
WHERE 이름 = '황진이';
```

<br/>

### 4) INSERT

**일반 형식**

```sql
SELECT [DISTINCT | TOP 2] 테이블명.속성명 AS 별칭, 그룹함수(속성명) AS 별칭, 
        Window 함수 OVER (PARTITION BY 속성명 ORDER BY 속성명 DESC)
FROM 테이블명, 테이블명
WHERE 조건
GROUP BY 속성명, 속성명
HAVING 조건
ORDER BY 속성명 [ASC | DESC];
```

<br/>

**(1) 조건 연산자**
> - 비교 연산자 : =, >, >=, <, <=, <>
> - 논리 연산자 : NOT, AND, OR
> - LIKE 연산자 : %, _, #

<br/>

**(2) 기본 검색**

```sql
SELECT * FROM 사원;

SELECT 이름, 사원.부서 AS 소속부서, 사원.생일
FROM 사원;

SELECT DISTINCT 주소
FROM 사원;
```

<br/>

**(3) 조건 지정 검색, WHERE**

```sql
WHERE 부서 IN ('기획', '인터넷');
WHERE 부서 = '기획' OR 부서 = '인터넷';

WHERE 이름 LIKT '김%';

WHERE 생일 BETWEEN #01/01/69# AND #12/31/73#;

WHERE 주소 IS NOT NULL;
```

<br/>

**(4) 정렬 검색, ORDER BY**

```sql
SELECT TOP 2 *
FROM 사원
ORDER BY 부서 ASC, 이름 DESC;
```

<br/>

**(5) 하위 질의**

```sql
WHERE 이름 = (SELECT 이름 FROM 여가활동 WHERE 취미 = '나이트댄스');

WHERE 이름 NOT IN (SELECT 이름 FROM 여가활동);

WHERE 기본급 < ALL(SELECT 기본급 FROM 사원 WHERE 주소 = '망원동');
```

<br/>

**(6) 복수 테이블 검색**

```sql
SELECT 사원.이름, 사원.부서, 여가활동.취미, 여가활동.경력
FROM 사원, 여가활동
WHERE 여가활동.경력 >= 10 AND 사원.이름 = 여가활동.이름;
```

<br/>

**(7) 그룹 함수 & 그룹 지정 검색**

> - COUNT, SUM, AVG, MAX, MIN, STDDEV, VARIANCE
> - ROLLUP(속성명1, 속성명2) => 순서 중요 / 속성 수 n이면, n+1 레벨 까지
> - CUBE(속성명1, 속성명2) => 2의 n승 레벨 까지

```sql
SELECT 부서, COUNT(*) AS 사원수
FROM 상여금
WHERE 상여금 >= 100
GROUP BY 부서
HAVING COUNT(*) >= 2;

-- ROLLUP : 부서 + 상여내역 -> 부서 -> 전체
SELECT 부서, 상여내역, SUM(상여금) AS 상여금합계
FROM 상여금
GROUP BY ROLLUP(부서, 상여내역);

-- CUBE : 전체 -> 상여내역 -> 부서 -> 부서 + 상여내역
GROUP BY CUBE(부서, 상여내역);
```

<br/>

**(8) WINDOW 함수 이용 검색**

> - ROW_NUMBER(), RANK(), DENSE_RANK()

```sql
-- ROW_NUMBER() : 일련번호
SELECT 상여내역, 상여금, ROW_NUMBER() OVER (PARTITION BY 상여내역 ORDER BY 상여금 DESC) AS NO
FROM 상여금;

-- RANK() : 공동 순위 반영 1 2 2 4
SELECT 상여내역, 상여금, RANK() OVER (PARTITION BY 상여내역 ORDER BY 상여금 DESC) AS 상여금순위
FROM 상여금;

-- DENSE_RANK() : 공동 순위 무시 1 2 3 4
```

<br/>

**(9) 집합 연산자를 이용한 통합 질의**

> - UNION, UNION ALL, INTERSECT, EXCEPT

```sql
SELECT 속성명, 속성명
FROM 테이블명
UNION | UNION ALL | INTERSECT | EXCEPT
SELECT 속성명, 속성명
FROM 테이블명;
```

<br/>

**(10) JOIN**

> - INNER JOIN
>    - EQUI JOIN
>        - WHERE 이용
>        - NATURAL JOIN
>        - USING 이용
>    - NON-EQUI JOIN
>
>    - 조건 없는 INNER JOIN = CROSS JOIN
>
> - OUTER JOIN
>    - LEFT OUTER JOIN
>    - RIGHT OUTER JOIN
>    - FULL OUTER JOIN


```sql
-- INNER JOIN - WHERE 이용
SELECT 학번, 이름, 학생.학과코드, 학과명
FROM 학생, 학과
WHERE 학생.학과코드 = 학과.학과코드;

-- INNER JOIN - NATURAL JOIN (이름과 도메인이 같은 속성 반드시 있어야 함)
SELECT 학번, 이름, 학생.학과코드, 학과명
FROM 학생 NATURAL JOIN 학과;

-- INNER JOIN - USING 이용
SELECT 학번, 이름, 학생.학과코드, 학과명
FROM 학생 JOIN 학과 USING(학과코드);

-- INNER JOIN - NON-EQUI JOIN
SELECT 학번, 이름, 성적, 등급
FROM 학생, 성적등급
WHERE 학생.성적 BETWEEN 성적등급.최저 AND 성적등급.최고;
```

```sql
-- OUTER JOIN - LEFT OUTER JOIN
SELECT 학번, 이름, 학생.학과코드, 학과명
FROM 학생 LEFT OUTER JOIN 학과
ON 학생.학과코드 = 학과.학과코드;

SELECT 학번, 이름, 학생.학과코드, 학과명
FROM 학생, 학과
WHERE 학생.학과코드 = 학과.학과코드(+); -- INNER JOIN 처럼 WHERE 절 사용 가능


-- OUTER JOIN - RIGHT OUTER JOIN
SELECT 학번, 이름, 학생.학과코드, 학과명
FROM 학과 RIGHT OUTER JOIN 학생
ON 학과.학과코드 = 학생.학과코드;

SELECT 학번, 이름, 학생.학과코드, 학과명
FROM 학과, 학생
WHERE 학과.학과코드(+) = 학생.학과코드; -- INNER JOIN 처럼 WHERE 절 사용 가능


-- OUTER JOIN - FULL OUTER JOIN
SELECT 학번, 이름, 학생.학과코드, 학과명
FROM 학생 FULL OUTER JOIN 학과
ON 학생.학과코드 = 학과.학과코드;
```
</details>























