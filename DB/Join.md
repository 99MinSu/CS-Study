# Join

### 조인의 종류

### 내부 조인 (Inner Join)

- 두 테이블에서 공통된 데이터만 선택합니다.
- 공통된 값이 없는 행은 결과에 포함되지 않습니다.
- 예: `SELECT * FROM A INNER JOIN B ON A.id = B.id;`

### 왼쪽 조인 (Left Join)

- 왼쪽 테이블의 모든 데이터와 오른쪽 테이블의 공통된 데이터를 선택합니다.
- 왼쪽 테이블에만 있는 데이터도 결과에 포함되며, 오른쪽 테이블에 해당 데이터가 없으면 NULL로 채워집니다.
- 예: `SELECT * FROM A LEFT JOIN B ON A.id = B.id;`

### 오른쪽 조인 (Right Join)

- 오른쪽 테이블의 모든 데이터와 왼쪽 테이블의 공통된 데이터를 선택합니다.
- 오른쪽 테이블에만 있는 데이터도 결과에 포함되며, 왼쪽 테이블에 해당 데이터가 없으면 NULL로 채워집니다.
- 예: `SELECT * FROM A RIGHT JOIN B ON A.id = B.id;`

### 합집합 조인 (Full Outer Join)

- 두 테이블의 모든 데이터를 선택합니다.
- 공통된 데이터는 한 줄로 합쳐지고, 각 테이블에만 있는 데이터는 NULL로 채워집니다.
- 예: `SELECT * FROM A FULL OUTER JOIN B ON A.id = B.id;`
  ![image](https://github.com/Minsu17/CS-Study/assets/89891511/b9e5cbe8-a75a-472d-802d-1ec1ef2d7fc9)

### 4.7 조인의 원리

### 중첩 루프 조인 (Nested Loop Join)

- 두 테이블을 중첩 루프를 사용하여 비교합니다.
- 외부 루프에서 첫 번째 테이블의 각 행을 선택하고, 내부 루프에서 두 번째 테이블의 각 행과 비교합니다.
- 작은 테이블과 큰 테이블을 비교할 때 유리합니다.
- 한 번에 많은 양의 데이터를 메모리에 로드하지 않고, 한 번에 하나의 행을 처리할 수 있습니다. 따라서 메모리 사용량이 정렬병합이나 해시조인보다 상대적으로 적습니다.

### 예시

```sql
INSERT INTO departments (dept_id, dept_name) VALUES
(1, 'Engineering'),
(2, 'Sales'),
(3, 'Marketing');

INSERT INTO employees (emp_id, emp_name, dept_id) VALUES
(101, 'Alice', 1),
(102, 'Bob', 2),
(103, 'Charlie', 1),
(104, 'David', 3);

SELECT d.dept_name, e.emp_name
FROM departments d
JOIN (
    SELECT emp_name, dept_id
    FROM employees
) AS e ON d.dept_id = e.dept_id;
```

출력

```lua
| dept_name   | emp_name |
|-------------|----------|
| Engineering | Alice    |
| Sales       | Bob      |
| Engineering | Charlie  |
| Marketing   | David    |
```

### 정렬 병합 조인 (Sort Merge Join)

- 두 테이블을 조인 조건에 따라 정렬한 후, 정렬된 순서에 따라 병합합니다.
- 정렬된 상태의 큰 테이블들에 적합합니다.
- 성능이 좋지만, 정렬하는 데 시간이 걸릴 수 있습니다.
- NL(중첩루프조인)은 인덱스가 없다면 Inner 테이블을 탐색할 때마다 반복적으로 Full Scan을 수행하므로 매우 비효율적이므로 그럴 때 정렬 병합 조인이나 해시 조인을 고려한다.

### 예시

```sql
CREATE TABLE table1 (
    id INT PRIMARY KEY,
    name VARCHAR(50)
);

CREATE TABLE table2 (
    id INT PRIMARY KEY,
    category VARCHAR(50)
);

INSERT INTO table1 (id, name) VALUES
(1, 'Alice'),
(2, 'Bob'),
(3, 'Charlie');

INSERT INTO table2 (id, category) VALUES
(1, 'A'),
(2, 'B'),
(3, 'C');

-- 정렬 병합 조인을 사용하여 두 테이블을 조인하고 결과를 출력
SELECT t1.id, t1.name, t2.category
FROM table1 t1
JOIN table2 t2 ON t1.id = t2.id
ORDER BY t1.id;
```

출력

```lua
| id | name    | category |
|----|---------|----------|
| 1  | Alice   | A        |
| 2  | Bob     | B        |
| 3  | Charlie | C        |
```

### 해시 조인 (Hash Join)

- 한 테이블에 해시 테이블을 만들고, 다른 테이블의 데이터를 해시 테이블과 비교합니다.
- 작은 테이블을 해시 테이블로 변환한 후, 이를 메모리에 적재하여 사용하기 때문에 메모리 사용이 효율적입니다. 이는 정렬 병합 조인과 비교하여 메모리 부담이 적다는 장점을 가집니다
- 메모리를 많이 사용하지만 성능이 뛰어납니다.
- 해시테이블을 이용하여 빠르게 검색하기때문에 속도가 빠른 장점이 있습니다.
- 동등조인에 효과적이고 큰 테이블과 작은 테이블 사이에서 효과적

### 예시

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(50),
    department_id INT
);

CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(50)
);

INSERT INTO employees (employee_id, employee_name, department_id) VALUES
(1, 'Alice', 1),
(2, 'Bob', 2),
(3, 'Charlie', 1),
(4, 'David', 3);

INSERT INTO departments (department_id, department_name) VALUES
(1, 'HR'),
(2, 'Finance'),
(3, 'IT');

-- 해시 조인을 사용하여 employees와 departments 테이블을 조인하는 쿼리
SELECT e.employee_id, e.employee_name, d.department_name
FROM employees e
JOIN departments d ON e.department_id = d.department_id;
```

출력

```lua
| employee_id | employee_name | department_name |
|-------------|---------------|-----------------|
| 1           | Alice         | HR              |
| 2           | Bob           | Finance         |
| 3           | Charlie       | HR              |
| 4           | David         | IT              |
```

## Reference

[https://hongong.hanbit.co.kr/sql-기본-문법-joininner-outer-cross-self-join/](https://hongong.hanbit.co.kr/sql-%EA%B8%B0%EB%B3%B8-%EB%AC%B8%EB%B2%95-joininner-outer-cross-self-join/)

[https://bebeya.tistory.com/entry/MSSQL-중첩루프-머지-해시조인-3가지-설명](https://bebeya.tistory.com/entry/MSSQL-%EC%A4%91%EC%B2%A9%EB%A3%A8%ED%94%84-%EB%A8%B8%EC%A7%80-%ED%95%B4%EC%8B%9C%EC%A1%B0%EC%9D%B8-3%EA%B0%80%EC%A7%80-%EC%84%A4%EB%AA%85)
