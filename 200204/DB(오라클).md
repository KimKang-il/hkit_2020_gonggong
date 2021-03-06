## 마이그레이션
* Sqlines
  - http://www.sqlines.com/online
  
## JOIN
### CROSS JOIN
* CROSS JOIN(교차 조인) 
  - 특징 : 카디사안 곱(Cartesian Product)
  ```sql
  - SELECT * FROM department CROSS JOIN employee;  
  - SELECT * FROM department, employee;
  ```
### INNER JOIN
* INNER JOIN(내부 조인) 
  - 특징 : 모든 비교자(=, <, >, <=, >=) 사용 가능
  ```sql
  - SELECT * FROM employee INNER JOIN department ON employee.DNO=department.DNO;
  - SELECT * FROM employee JOIN department ON employee.DNO=department.DNO;
  - SELECT * FROM employee, department WHERE employee.DNO=department.DNO;
  ```
* EQUI JOIN(동일 조인) 
  - 특징 : 조건으로 동등 비교(=)만 사용 가능
  ```sql
  - SELECT * FROM employee JOIN department WHERE employee.DNO=department.DNO;  
  - SELECT * FROM employee, department WHERE employee.DNO=department.DNO;  
  - SELECT * FROM employee INNER JOIN department USING (DNO);
  ```
* NATURAL JOIN(자연 조인) - 자동으로 동일한 컬럼이 있는지를 조사해서 조인함
  - SELECT * FROM employee NATURAL JOIN department;
### OUTER JOIN
* 특징 : 무조건 INNER JOIN 보다는 검색 결과가 같거나 많음
* FULL OUTER JOIN(완전 외부 조인)
  ```sql
  - SELECT * FROM employee FULL OUTER JOIN department ON employee.DNO = department.DNO;  
  ```
* LEFT OUTER JOIN(왼쪽 외부 조인)
  ```sql
  - SELECT * FROM employee LEFT OUTER JOIN department ON employee.DNO = department.DNO;  
  ```
* RIGHT OUTER JOIN(오른쪽 외부 조인)
  ```sql
  - SELECT * FROM employee RIGHT OUTER JOIN department ON employee.DNO = department.DNO;
  ```
### SELF JOIN
* SELF JOIN(자가 조인)
  ```sql
  - SELECT a.ENAME AS '사원이름', b.ENAME AS '직속상관이름' FROM employee a INNER JOIN employee b ON a.MANAGER=b.DNO
  - SELECT a.ENAME AS '사원이름', b.ENAME AS '직속상관이름' FROM employee a JOIN employee b ON a.MANAGER=b.DNO
  - SELECT a.ENAME AS '사원이름', b.ENAME AS '직속상관이름' FROM employee a INNER JOIN employee b WHERE a.MANAGER=b.DNO
  - SELECT a.ENAME AS '사원이름', b.ENAME AS '직속상관이름' FROM employee a JOIN employee b WHERE a.MANAGER=b.DNO
  - SELECT a.ENAME AS '사원이름', b.ENAME AS '직속상관이름' FROM employee a, employee b WHERE a.MANAGER=b.DNO
  ```

## 명시적, 암묵적 조인 비교
  ```sql
  - SELECT * FROM employee CROSS JOIN department;
  - SELECT * FROM employee INNER JOIN department;
  - SELECT * FROM employee JOIN department;
  - SELECT * FROM employee, department;
  ```

## 연습문제

1. EQUI 조인을 사용하여 SCOTT 사원의 부서번호와 부서 이름을 출력하시오.
```console
ENAME                       DNO DNAME
-------------------- ---------- ----------------------------
SCOTT                        20 RESEARCH
```

2. INNER JOIN과 ON 연산자를 사용하여 사원이름과 함께 그 사원이 소속된 부서이름과 지역명을 출력하시오.
```console
ENAME                DNAME                        LOC
-------------------- ---------------------------- --------------------------
CLARK                ACCOUNTING                   NEW YORK
KING                 ACCOUNTING                   NEW YORK
MILLER               ACCOUNTING                   NEW YORK
JONES                RESEARCH                     DALLAS
FORD                 RESEARCH                     DALLAS
ADAMS                RESEARCH                     DALLAS
SMITH                RESEARCH                     DALLAS
SCOTT                RESEARCH                     DALLAS
WARD                 SALES                        CHICAGO
TURNER               SALES                        CHICAGO
ALLEN                SALES                        CHICAGO

ENAME                DNAME                        LOC
-------------------- ---------------------------- --------------------------
JAMES                SALES                        CHICAGO
BLAKE                SALES                        CHICAGO
MARTIN               SALES                        CHICAGO

14 rows selected.
```

3. INNER JOIN과 USING 연산자를 사용하여 10번 부서에 속하는 모든 담당 업무의 고유 목록(한번씩만 표시)을 부서의 지역명을 포함하여 출력하시오.
```console
       DNO JOB                LOC
---------- ------------------ --------------------------
        10 MANAGER            NEW YORK
        10 PRESIDENT          NEW YORK
        10 CLERK              NEW YORK
```

4. NATURAL JOIN을 사용하여 커미션을 받는 모든 사원의 이름, 부서이름, 지역명을 출력하시오.
```console
ENAME                DNAME                        LOC
-------------------- ---------------------------- --------------------------
ALLEN                SALES                        CHICAGO
MARTIN               SALES                        CHICAGO
WARD                 SALES                        CHICAGO
```


5. EQUI 조인과 WildCard를 사용하여 이름에 A가 포함된 모든 사원의 부서명을 출력하시오.
```console
ENAME                DNAME
-------------------- ----------------------------
ALLEN                SALES
WARD                 SALES
MARTIN               SALES
BLAKE                SALES
CLARK                ACCOUNTING
ADAMS                RESEARCH
JAMES                SALES

7 rows selected.
```


6. NATURAL JOIN을 사용하여 NEW YORK에 근무하는 모든 사원의 이름, 업무, 부서번호 및 부서명을 출력하시오.
```console
ENAME                JOB                       DNO DNAME
-------------------- ------------------ ---------- ----------------------------
CLARK                MANAGER                    10 ACCOUNTING
KING                 PRESIDENT                  10 ACCOUNTING
MILLER               CLERK                      10 ACCOUNTING
```

7. SELF JOIN을 사용하여 사원의 이름 및 사원번호를 관리자 이름 및 관리자 번호와 함께 출력하시오. 단 각 열의 별칭은 결과 화면과 같이 하시오.
```console
EMPLOYEE                   EMP#    MANAGER MRG#
-------------------- ---------- ---------- --------------------
FORD                       7566       7566 JONES
SCOTT                      7566       7566 JONES
TURNER                     7698       7698 BLAKE
ALLEN                      7698       7698 BLAKE
WARD                       7698       7698 BLAKE
JAMES                      7698       7698 BLAKE
MARTIN                     7698       7698 BLAKE
MILLER                     7782       7782 CLARK
ADAMS                      7788       7788 SCOTT
BLAKE                      7839       7839 KING
JONES                      7839       7839 KING

EMPLOYEE                   EMP#    MANAGER MRG#
-------------------- ---------- ---------- --------------------
CLARK                      7839       7839 KING
SMITH                      7902       7902 FORD

13 rows selected.
```

<!--
8. OUTER JOIN, SELF JOIN을 사용하여 관리자가 없는 사원을 포함하여 사원번호를 기준으로 내림차순 정렬을 하여 출력하시오.
```console
EMPLOYEE                   EMP#    MANAGER MGR#
-------------------- ---------- ---------- --------------------
MILLER                     7782       7782 CLARK
FORD                       7566       7566 JONES
JAMES                      7698       7698 BLAKE
ADAMS                      7788       7788 SCOTT
TURNER                     7698       7698 BLAKE
KING
SCOTT                      7566       7566 JONES
CLARK                      7839       7839 KING
BLAKE                      7839       7839 KING
MARTIN                     7698       7698 BLAKE
JONES                      7839       7839 KING

EMPLOYEE                   EMP#    MANAGER MGR#
-------------------- ---------- ---------- --------------------
WARD                       7698       7698 BLAKE
ALLEN                      7698       7698 BLAKE
SMITH                      7902       7902 FORD

14 rows selected.
```

-->
9. SELF JOIN을 사용하여 지정한 사원의 이름, 부서번호, 지정한 사원과 동일한 부서에서 근무하는 사원을 출력하시오. 단, 각 열의 별칭은 이름, 부서번호, 동료로 하시오.
```console
이름                   부서번호 동료
-------------------- ---------- --------------------
SCOTT                        20 SMITH
SCOTT                        20 JONES
SCOTT                        20 ADAMS
SCOTT                        20 FORD
```

10. SELF JOIN을 사용하여 WARD사원보다 늦게 입사한 사원의 이름과 입사일을 출력하시오.
```console
ENAME                HIREDATE
-------------------- --------
JONES                81/04/02
BLAKE                81/05/01
CLARK                81/06/09
TURNER               81/09/08
MARTIN               81/09/28
KING                 81/11/17
JAMES                81/12/03
FORD                 81/12/03
MILLER               82/01/23
SCOTT                87/07/13
ADAMS                87/07/13

11 rows selected.
```

11. SELF JOIN을 사용하여 관리자보다 먼저 입사한 모든 사원의 이름 및 입사일을 관리자의 이름 및 입사일과 함께 출력하시오, 단 각 열의 별칭은 결과 화면과 같도록 하시오.
```console
ENAME                HIREDATE ENAME                HIREDATE
-------------------- -------- -------------------- --------
ALLEN                81/02/20 BLAKE                81/05/01
WARD                 81/02/22 BLAKE                81/05/01
ADAMS                87/07/13 SCOTT                87/07/13
BLAKE                81/05/01 KING                 81/11/17
JONES                81/04/02 KING                 81/11/17
CLARK                81/06/09 KING                 81/11/17
SMITH                80/12/17 FORD                 81/12/03

7 rows selected.
```

## 참고 링크
* 위키백과 - Join (SQL)
  - https://ko.wikipedia.org/wiki/Join_(SQL)
* 11_JOIN
  - https://routines77.tistory.com/entry/11JOIN
    
    
