# 📌 조인

1. EQUI JOIN을 사용하여 학생 테이블과 부서 테이블의 학번, 이름, 학과번호, 소속학과 이름, 학과 위치 출력 

SELECT name, CONCAT(SUBSTRING(name, 1, 1), '*', SUBSTRING(name, 3, 1)) `newname` FROM student;

```
```

2. 102번 학과에 다니는 학생들에 대한 학번, 이름, 학과번호, 소속학과이름, 학년을 EQUI JOIN으로 조회하여 학년 순으로 출력

SELECT name, CONCAT(SUBSTRING(idnum, 1, 6), '-' , '*******') `newidnum` FROM student;
```

```

3. 학생이름, 학년, 담당교수이름, 담당교수의 직급을 EQUI JOIN으로 조회


```

```

4. 학생이름, 학년, 담당교수이름, 담당교수의 직급을 INNER JOIN을 사용하여 조회

SELECT max(height), min(height) FROM student where deptno = 101;

```
```