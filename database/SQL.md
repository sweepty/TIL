# SQL

### 단일 SQL 문 실행 순서

```flow
st=>start: Start
from=>operation: FROM: JOIN을 통하여 큰 테이블을 만든다. 
where=>operation: WHERE: 테이블로부터 한 Row씩 읽어 조건을 만족하는 결과만 뽑는다.
groupby=>operation: GROUP BY: 원하는 그룹별로 행들을 Grouping한다.
having=>operation: HAVING: 원하는 조건을 만족하는 그룹만 남긴다.
orderby=>operation: ORDER BY: 주어진 조건에 따라 정렬 한다.
select=>operation: SELECT: 원하는 결과만 Projection한다.
e=>end
st->from->where->groupby->having->orderby->select->e

```



## Join

#### Cartesian product 

```sql
select * from emp, dept;
select * from emp cross join dept;
```



#### Equi join

```sql
SELECT * 
FROM emp e, dept d 
WHERE e.deptno = d.deptno;

-- 이렇게 쓰기도 함.
SELECT * 
FROM emp JOIN dept USING (deptno);
```



#### Natural join

```sql
select *
from dept natural join emp;
```

두 테이블에 이름이 같은 컬럼이 있을 때 사용가능함.



> Q. 그럼 equi join이랑 natrual join이랑 뭐가 다른가?
>
> A. natural join은 중복되는 컬럼 값을 없애줌.
>
> 위의 예제처럼 equi join을 수행하는 경우에는 deptno가 두개가 나오지만 natural join의 경우에는 중복되는 값인 deptno가 한번만 나옴.



#### Outer join

Left outer join -  

```sql
-- left outer join 
select *
from emp left outer join dept on emp.deptno = dept.deptno;

-- right outer join
select *
from emp right outer join dept on emp.deptno = dept.deptno;

-- full outer join
select *
from emp full outer join dept on emp.deptno = dept.deptno;
```





## Group & Aggregation

### Aggregation function

결과값 하나만 반환한다.

- 종류
  - AVG
  - COUNT
  - MAX
  - MIN
  - SUM
  - ....

```sql
-- 직원들의 연봉평균 구하기
select avg(salary) from emp;
```



Q. 부서별 평균 연봉을 구하고 싶어요! 이렇게 하면 되나요? (부서번호, 평균 연봉)으로 출력할건데 😃

```sql
select deptno, avg(salary) from emp;
-- ERROR 이렇게 하면 안됨!!!!!!!
```

=> aggregation을 사용하면 컬럼이 하나만 나오기 때문에 다른 컬럼을 더 select하고 싶다면 group by를 이용해야한다.



### Group

- **group by** : 그룹으로 묶은 결과를 확인해야할 때 사용한다.

ex) 

```sql
-- 부서별 인원 찾기 (부서명, 인원)으로 출력
select dname, count(empno)
from emp e left outer join dept d on e.deptno = d.deptno
group by dname;
```

- having: group by를 사용하여 그룹으로 묶은 결과에 조건을 주고 싶을 때 사용한다. (where와 같은 역할)

*where 과 having을 잘 구분해서 하자 (중요중요)*



#### 연습

부서별 인원을 부서명과 출력해보자^*^

```sql
-- 근데 부서에 인원이 하나도 없는 경우를 대비해서 left outer join을 해야하는거 아닐까?
-- 맞는거 같다..ㅎㅎ 잘했어 하지만 처음부터 생각해냈어야지
select dname, count(empno)
from emp e left outer join dept d on e.deptno = d.deptno
group by dname;
```



```sql
-- 틀림^*^ 주의하자
select dname, count(empno)
from emp e join dept d on e.deptno = d.deptno
group by dname;
```



self join으로 scott의 연봉보다 높은 사람 찾기 self join 근데 그냥 from emp e, emp e2해도 됨.(cartesian join)

```sql
select e.ename
from emp e join emp e2 on e.empno= e2.empno
where e2.ename = 'SCOTT' and e2.sal < e.sal;
```



rownum을 이용해서 상위 3개 이런거 빠르게 뽑기: top-k





## Subquery

하나의 SQL 질의문 속에 다른 SQL 질의문이 포함되어 있는 형태 



###Single-row subquery 

Subquery의 결과가 **한 개** ROW인 경우 

= , > , >=, < , <=, <> 를 사용한다.

ex)

```sql
SELECT ename, deptno 
FROM emp 
WHERE deptno = (SELECT deptno FROM dept WHERE dname = 'SALES');
```



###Multi-row subquery

Subquery의 결과가 **둘 이상**의 Row 일 때

ANY, ALL, IN, EXIST…  를 사용한다.

ex)

```sql
SELECT ename, sal, deptno 
FROM emp 
WHERE ename IN (SELECT MIN(ename) FROM emp GROUP BY deptno);
```



굳이 JOIN이 필요없는 곳에서는 JOIN을 하지말고 subquery를 이용해서 조인값을 줄이자.