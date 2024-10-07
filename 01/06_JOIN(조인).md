# 📌 조인

1. EQUI JOIN을 사용하여 학생 테이블과 부서 테이블의 학번, 이름, 학과번호, 소속학과 이름, 학과 위치 출력 

SELECT s.studno, s.name, s.deptno, d.dname, d.loc
FROM student s, department d WHERE s.deptno = d.deptno;

```
mysql> SELECT s.studno, s.name, s.deptno, d.dname, d.loc
    -> FROM student s, department d WHERE s.deptno = d.deptno;
+--------+-----------+--------+-----------------------+---------+
| studno | name      | deptno | dname                 | loc     |
+--------+-----------+--------+-----------------------+---------+
|  10101 | 전인하    |    101 | 컴퓨터공학과          | 1호관   |
|  10102 | 박미경    |    101 | 컴퓨터공학과          | 1호관   |
|  10103 | 김영균    |    101 | 컴퓨터공학과          | 1호관   |
|  10104 | 지은경    |    101 | 컴퓨터공학과          | 1호관   |
|  10105 | 임유진    |    101 | 컴퓨터공학과          | 1호관   |
|  10106 | 서재진    |    101 | 컴퓨터공학과          | 1호관   |
|  10107 | 이광훈    |    101 | 컴퓨터공학과          | 1호관   |
|  10108 | 류민정    |    101 | 컴퓨터공학과          | 1호관   |
|  10201 | 김진영    |    102 | 멀티미디어학과        | 2호관   |
|  10202 | 오유석    |    102 | 멀티미디어학과        | 2호관   |
|  10203 | 하나리    |    102 | 멀티미디어학과        | 2호관   |
|  10204 | 윤진욱    |    102 | 멀티미디어학과        | 2호관   |
|  20101 | 이동훈    |    201 | 전자공학과            | 3호관   |
|  20102 | 박동진    |    201 | 전자공학과            | 3호관   |
|  20103 | 김진경    |    201 | 전자공학과            | 3호관   |
|  20104 | 조명훈    |    201 | 전자공학과            | 3호관   |
+--------+-----------+--------+-----------------------+---------+

```

2. 102번 학과에 다니는 학생들에 대한 학번, 이름, 학과번호, 소속학과이름, 학년을 EQUI JOIN으로 조회하여 학년 순으로 출력

SELECT s.studno, s.name, s.deptno, d.deptno, s.grade
FROM student s, department d 
WHERE s.deptno = d.deptno AND s.deptno = 102
ORDER BY s.grade;

```
mysql> SELECT s.studno, s.name, s.deptno, d.deptno, s.grade
    -> FROM student s, department d
    -> WHERE s.deptno = d.deptno AND s.deptno = 102
    -> ORDER BY s.grade;
+--------+-----------+--------+--------+-------+
| studno | name      | deptno | deptno | grade |
+--------+-----------+--------+--------+-------+
|  10203 | 하나리    |    102 |    102 |     1 |
|  10201 | 김진영    |    102 |    102 |     2 |
|  10204 | 윤진욱    |    102 |    102 |     3 |
|  10202 | 오유석    |    102 |    102 |     4 |
+--------+-----------+--------+--------+-------+
```

3. 학생이름, 학년, 담당교수이름, 담당교수의 직급을 EQUI JOIN으로 조회
   
SELECT s.name, s.grade, s.deptno, p.name, p.position
FROM student s, professor p 
WHERE s.profno = p.profno;

```
mysql> SELECT s.name, s.grade, s.deptno, p.name, p.position
    -> FROM student s, professor p
    -> WHERE s.profno = p.profno;
+-----------+-------+--------+-----------+--------------+
| name      | grade | deptno | name      | position     |
+-----------+-------+--------+-----------+--------------+
| 김진경    |     2 |    201 | 이재우    | 조교수       |
| 전인하    |     4 |    101 | 성연희    | 조교수       |
| 이광훈    |     4 |    101 | 성연희    | 조교수       |
| 김진영    |     2 |    102 | 권혁일    | 교수         |
| 오유석    |     4 |    102 | 권혁일    | 교수         |
| 윤진욱    |     3 |    102 | 권혁일    | 교수         |
| 김영균    |     3 |    101 | 이만식    | 부교수       |
| 지은경    |     2 |    101 | 전은지    | 전임강사     |
| 임유진    |     2 |    101 | 전은지    | 전임강사     |
| 류민정    |     2 |    101 | 전은지    | 전임강사     |
+-----------+-------+--------+-----------+--------------+
```

1. 학생이름, 학년, 담당교수이름, 담당교수의 직급을 INNER JOIN을 사용하여 조회

SELECT s.name, s.grade, p.name, p.position
FROM student s
INNER JOIN professor p
ON s.profno = p.profno;

```
mysql> SELECT s.name, s.grade, p.name, p.position
    -> FROM student s
    -> INNER JOIN professor p
    -> ON s.profno = p.profno;
+-----------+-------+-----------+--------------+
| name      | grade | name      | position     |
+-----------+-------+-----------+--------------+
| 김진경    |     2 | 이재우    | 조교수       |
| 전인하    |     4 | 성연희    | 조교수       |
| 이광훈    |     4 | 성연희    | 조교수       |
| 김진영    |     2 | 권혁일    | 교수         |
| 오유석    |     4 | 권혁일    | 교수         |
| 윤진욱    |     3 | 권혁일    | 교수         |
| 김영균    |     3 | 이만식    | 부교수       |
| 지은경    |     2 | 전은지    | 전임강사     |
| 임유진    |     2 | 전은지    | 전임강사     |
| 류민정    |     2 | 전은지    | 전임강사     |
+-----------+-------+-----------+--------------+

```