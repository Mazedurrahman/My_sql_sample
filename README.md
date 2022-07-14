use employees;
show tables;

select * from departments_dup order by dept_no ;
select * from dept_manager_dup order by dept_no ;

commit;

SELECT 
    m.dept_no, m.emp_no, d.dept_name
FROM
    dept_manager_dup m
        INNER JOIN
    departments_dup d ON m.dept_no = d.dept_no
GROUP BY m.emp_no
ORDER BY m.dept_no; 

show tables;
select * from employees;
select * from dept_manager;

SELECT 
    m.emp_no, m.dept_no, e.first_name, e.last_name, e.hire_date
FROM
    dept_manager m
        INNER JOIN
    employees e ON m.emp_no = e.emp_no
ORDER BY m.emp_no;

use employees;
select * from employees;
select * from dept_manager;

SELECT 
    e.emp_no, e.first_name, e.last_name, m.dept_no, m.from_date
FROM
    employees e
        LEFT JOIN
    dept_manager m ON m.emp_no = m.emp_no
WHERE
    last_name = 'Markovitch'
ORDER BY m.dept_no DESC , e.emp_no;


use employees;
select * from employees;
select * from dept_manager;

SELECT 
    e.emp_no, e.first_name, e.last_name, m.dept_no, e.hire_date
FROM
    dept_manager m
        INNER JOIN
    employees e ON m.emp_no = e.emp_no;
    
SELECT 
    e.emp_no, e.first_name, e.last_name, s.salary
FROM
    salaries s
        INNER JOIN
    employees e ON e.emp_no = s.emp_no
WHERE
    salary > 145000;
    
SELECT 
    e.emp_no, e.first_name, e.last_name
FROM
    dept_manager m
        INNER JOIN
    employees e ON m.emp_no = e.emp_no;
    
    
SELECT 
    e.emp_no, e.first_name, e.last_name
FROM
    employees e
WHERE
    e.emp_no IN (SELECT 
            dm.emp_no
        FROM
            dept_manager dm);
            
select * from dept_manager;

SELECT 
    *
FROM
    employees e
WHERE
    e.emp_no IN (SELECT 
            emp_no
        FROM
            dept_manager
        WHERE
            hire_date IN ('1990-01-01' , '1095-01-01'));
            
SELECT 
    *
FROM
    dept_manager 
WHERE
    emp_no IN (SELECT 
            emp_no
        FROM
            employees 
        WHERE
            hire_date BETWEEN '1990-01-01' AND '1095-01-01');

SELECT 
    m.emp_no,
    m.dept_no,
    e.first_name,
    e.last_name,
    m.from_date,
    m.to_date
FROM
    employees e
        INNER JOIN
    dept_manager m ON e.emp_no = m.emp_no
WHERE
    e.hire_date BETWEEN '1990-01-01' AND '1095-01-01';
   
   show tables;
   select * from titles;
   
SELECT 
    *
FROM
    employees e
        INNER JOIN
    title t ON e.emp_no = t.emp_no
WHERE
    title = 'Assistant Engineer';
    
    
SELECT 
    emp_no, title
FROM
    titles
WHERE
    title = 'Assistant Engineer';
    
SELECT 
    *
FROM
    employees e
WHERE
    EXISTS( SELECT 
            *
        FROM
            titles t
        WHERE
            t.emp_no = e.emp_no
                AND title = 'assistant engineeer');

use employees;
show tables;

select * from dept_manager;
select * from dept_emp;

select emp_no from dept_manager where emp_no = '110022';
SELECT 
    A.*
FROM
    (SELECT 
        e.emp_no AS employees_id,
            MIN(de.dept_no) AS department_code,
            (SELECT 
                    emp_no
                FROM
                    dept_manager
                WHERE
                    emp_no = '110022') AS manager_id
    FROM
        employees e
    JOIN dept_emp de ON e.emp_no = de.emp_no
    WHERE
        e.emp_no <= 10020
    GROUP BY e.emp_no
    ORDER BY e.emp_no) AS A 
UNION SELECT 
    B.*
FROM
    (SELECT 
        e.emp_no AS employees_id,
            MIN(de.dept_no) AS department_code,
            (SELECT 
                    emp_no
                FROM
                    dept_manager
                WHERE
                    emp_no = '110039') AS manager_id
    FROM
        employees e
    JOIN dept_emp de ON e.emp_no = de.emp_no
    WHERE
        e.emp_no >= 10020
    GROUP BY e.emp_no
    ORDER BY e.emp_no
    LIMIT 20) AS B;
    
    Drop table if exists emp_manager;
    CREATE TABLE emp_manager (
    emp_no INT(11) NOT NULL,
    dept_no CHAR(4) NULL,
    manager_no INT(11) NOT NULL
);

select * from  emp_manager;
