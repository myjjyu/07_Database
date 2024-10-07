# 📌 서브쿼리

1. 아이디가 jun123 인 학생과 같은 학년인 학생의 학번, 이름, 학년을 조회 

SELECT studno, name, grade FROM student s WHERE s.grade = (SELECT grade FROM student WHERE userid = 'jun123');

```
mysql> SELECT studno, name, grade FROM student s WHERE s.grade = (SELECT grade FROM student WHERE userid = 'jun123');
+--------+-----------+-------+
| studno | name      | grade |
+--------+-----------+-------+
|  10101 | 전인하    |     4 |
|  10107 | 이광훈    |     4 |
|  10202 | 오유석    |     4 |
+--------+-----------+-------+
```

2. 101번 학과 학생들의 평균 몸무게보다 몸무게가 적은 학생의 이름, 학과번호, 몸무게를 조회

SELECT name, deptno, weight FROM student s 
WHERE weight < 
(SELECT AVG(weight) FROM student WHERE deptno = 101);

```
mysql> SELECT name, deptno, weight FROM student s
    -> WHERE weight <
    -> (SELECT AVG(weight) FROM student WHERE deptno = 101);
+-----------+--------+--------+
| name      | deptno | weight |
+-----------+--------+--------+
| 박미경    |    101 |     52 |
| 지은경    |    101 |     42 |
| 임유진    |    101 |     54 |
| 김진영    |    102 |     48 |
| 이동훈    |    201 |     64 |
| 김진경    |    201 |     51 |
| 조명훈    |    201 |     62 |

```

3. 이광훈 학생 과 같은 학과의 학생들에 대한 평균 몸무게보다 몸무게가 적게 나가는 학생들의 이름, 몸무게, 소속학과이름, 담당교수 이름을 조회
- 담당교수가 없는 학생은 출력되지 않습니다

SELECT s.name, s.weight, d.dname, p.name 
FROM student s
INNER JOIN department d ON s.deptno = d.deptno
INNER JOIN professor p ON s.profno = p.profno
WHERE s.weight < (SELECT AVG(weight) FROM student 
WHERE deptno = (SELECT deptno FROM student WHERE name = '이광훈')
);

```
mysql> SELECT s.name, s.weight, d.dname, p.name
    -> FROM student s
    -> INNER JOIN department d ON s.deptno = d.deptno
    -> INNER JOIN professor p ON s.profno = p.profno
    -> WHERE s.weight < (SELECT AVG(weight) FROM student
    -> WHERE deptno = (SELECT deptno FROM student WHERE name = '이광훈')
    -> );
+-----------+--------+-----------------------+-----------+
| name      | weight | dname                 | name      |
+-----------+--------+-----------------------+-----------+
| 지은경    |     42 | 컴퓨터공학과          | 전은지    |
| 임유진    |     54 | 컴퓨터공학과          | 전은지    |
| 김진영    |     48 | 멀티미디어학과        | 권혁일    |
| 김진경    |     51 | 전자공학과            | 이재우    |
+-----------+--------+-----------------------+-----------+

```

4. 20101번 학생과 같은 학년이고, 20101번 학생의 키보다 큰키를 갖는 학생의 이름, 학년, 키를 조회하시오 

SELECT name, grade, height FROM student s 
WHERE s.grade = (SELECT grade FROM student WHERE studno = '20101')
AND s.height > (SELECT height FROM student WHERE studno = '20101');

```
mysql> SELECT name, grade, height FROM student s WHERE s.grade = (SELECT grade FROM student WHERE studno = '20101') AND s.height > (SELECT height FROM student WHERE studno = '20101');
+-----------+-------+--------+
| name      | grade | height |
+-----------+-------+--------+
| 서재진    |     1 |    186 |
| 박동진    |     1 |    182 |
| 조명훈    |     1 |    184 |
+-----------+-------+--------+
```

5. 학과이름에 공학 이라는 단어를 포함하고 있는 학과에 재학중인 학생의 학번, 학과이름, 학년, 학생이름을 조회 
   
SELECT s.studno, d.dname, s.grade, s.name 
FROM student s 
INNER JOIN department d ON s.deptno = d.deptno
WHERE d.dname LIKE '%공학%';

```
mysql> SELECT s.studno, d.dname, s.grade, s.name
    -> FROM student s
    -> INNER JOIN department d ON s.deptno = d.deptno
    -> WHERE d.dname LIKE '%공학%';
+--------+--------------------+-------+-----------+
| studno | dname              | grade | name      |
+--------+--------------------+-------+-----------+
|  10101 | 컴퓨터공학과       |     4 | 전인하    |
|  10102 | 컴퓨터공학과       |     1 | 박미경    |
|  10103 | 컴퓨터공학과       |     3 | 김영균    |
|  10104 | 컴퓨터공학과       |     2 | 지은경    |
|  10105 | 컴퓨터공학과       |     2 | 임유진    |
|  10106 | 컴퓨터공학과       |     1 | 서재진    |
|  10107 | 컴퓨터공학과       |     4 | 이광훈    |
|  10108 | 컴퓨터공학과       |     2 | 류민정    |
|  20101 | 전자공학과         |     1 | 이동훈    |
|  20102 | 전자공학과         |     1 | 박동진    |
|  20103 | 전자공학과         |     2 | 김진경    |
|  20104 | 전자공학과         |     1 | 조명훈    |
+--------+--------------------+-------+-----------+
```