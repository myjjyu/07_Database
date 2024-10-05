# 📌 서브쿼리

1. 아이디가 jun123 인 학생과 같은 학년인 학생의 학번, 이름, 학년을 조회 

SELECT name, CONCAT(SUBSTRING(name, 1, 1), '*', SUBSTRING(name, 3, 1)) `newname` FROM student;

```
```

2. 101번 학과 학생들의 평균 몸무게보다 몸무게가 적은 학생의 이름, 학과번호, 몸무게를 조회
SELECT name, CONCAT(SUBSTRING(idnum, 1, 6), '-' , '*******') `newidnum` FROM student;
```

```

3. 이광훈 학생 과 같은 학과의 학생들에 대한 평균 몸무게보다 몸무게가 적게 나가는 학생들의 이름, 몸무게, 소속학과이름, 담당교수 이름을 조회
- 담당교수가 없는 학생은 출력되지 않습니다


```

```

4. 20101번 학생과 같은 학년이고, 20101번 학생의 키보다 큰키를 갖는 학생의 이름, 학년, 키를 조회하시오 

SELECT max(height), min(height) FROM student where deptno = 101;

```
```

5. 학생이름에 공학 이라는 단어를 포함하고 있는 학과에 재학중인 학생의 학번, 학과이름, 학년, 학생이름을 조회 

SELECT max(height), min(height) FROM student where deptno = 101;

```
```