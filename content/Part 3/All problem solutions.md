```sql
-- Part 3: DBMS Query Tasks 45pts total, 3pt for each

  

-- 1. Create a procedure 'sp_UpdateStock' that decreases product quantity. If quantity

-- drops below zero, it must ROLLBACK the transaction.

  

-- my (wrong) version

create procedure sp_UpdateStock(p_product_id int, p_amount) as $$

begin

update products set quantity=quantity-p_amount where product_id=p_product_id

if (select quantity from products) < 0

then rollback

end if

end;

$$ language plpgsql;

  

-- corrected version

create procedure sp_UpdateStock(p_product_id int, p_amount int) as $$

begin

update products set quantity=quantity-p_amount where product_id=p_product_id;

if (select quantity from products where product_id = p_product_id) < 0

then rollback;

end if;

end;

$$ language plpgsql;

  
  

-- 2. Write a function 'fn_CalcDiscount' that returns a 20% discount if a customer has spent

-- over $5000, and 10% otherwise.

  

create function fn_CalcDiscount(p_spent_amount numeric) returns numeric as $$

begin

if (p_spent_amount > 5000)

then return p_spent_amount * 0.2;

else return p_spent_amount * 0.1;

end if;

end;

$$ language plpgsql;

  
  

-- 3. Create a partial index on the 'Orders' table that only indexes records where 'status' is

-- 'Urgent'.

  

-- my wrong version

create index idx_urg on orders where status='Urgent';

  

-- corrected version

create index idx_urg on orders(order_id) where status='Urgent';

  

-- 4. Given R(A, B, C, D, E) and F = {A -> B, BC -> D, D -> A}. Find all candidate keys.

  

ACE, BCE, DCE

  

-- 5. Decompose R(A, B, C, D) with FDs {A -> B, B -> C} into 3NF. Ensure it is

-- dependency-preserving.

  

Candidate keys: AD

Decomposing: R1(A,B), R2(B,C), R3(A,D)

  

-- 6. Transform the following into an optimized Relational Algebra tree:

-- SELECT name FROM student, dept WHERE student.d_id = dept.d_id AND dept.budget > 50000.

π_name

   │

   ⨝ (student.d_id = dept.d_id)

   │                    │

student          σ_budget > 50000

                        │

                      dept

  
  
  
  
  
  

-- 7. Explain why a Hash Join might be selected by the optimizer over a Nested Loop Join

-- for two large tables.

hash join uses hash table to store values of one table and can access them quickly, so it has to only traverse first table once

and then it traverses second table once and joins.

In "nested loop join" for every row of first table we have to check every row of second table (or vice versa),

so it might be significantly slower

  
  

-- 8. Write a SQL block that demonstrates the 'Read Committed' isolation level compared

-- to 'Repeatable Read'.

In "Read Commited" non-repeatable read can occur, whereas in "repeatable read" it cannot.

-- Read Commited

-- Session A

SET TRANSACTION ISOLATION LEVEL READ COMMITTED;

BEGIN;

SELECT balance FROM accounts WHERE id = 1;   -- sees 1000

-- Session B

BEGIN;

UPDATE accounts SET balance = 900 WHERE id = 1;

COMMIT;

-- Session A (still inside the same transaction)

SELECT balance FROM accounts WHERE id = 1;   -- now sees 900

COMMIT;

  

-- Repeatable Read

-- Session A

SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;

BEGIN;

SELECT balance FROM accounts WHERE id = 1;   -- sees 1000

-- Session B

BEGIN;

UPDATE accounts SET balance = 800 WHERE id = 1;

COMMIT;

-- Session A (still inside the same transaction)

SELECT balance FROM accounts WHERE id = 1;   -- still sees 1000 (old snapshot)

COMMIT;

  
  

-- 9. Write a query to find the 3rd highest salary in each department using

-- DENSE_RANK().

  

WITH ranked_salaries AS (

    SELECT

        dept_name,

        salary,

        DENSE_RANK() OVER (PARTITION BY dept_name ORDER BY salary DESC) AS dr

    FROM instructor

)

SELECT dept_name, salary

FROM ranked_salaries

WHERE dr = 3;

-- we also have similar functions RANK(), ROW_NUMBER()

  
  

-- 10. Given an 'Employees' table with 'id' and 'manager_id', write a recursive query to

-- show the full hierarchy of a specific manager.

  

WITH RECURSIVE hierarchy AS (

    SELECT id, manager_id

    FROM employees

    WHERE id = 5 -- manager with id 5

  

    UNION ALL

  

    SELECT e.id, e.manager_id

    FROM employees e

    JOIN hierarchy h ON e.manager_id = h.id

)

SELECT * FROM hierarchy;

  

-- 11. Find the IDs of students who have enrolled in ALL courses offered by the 'Computer

-- Science' department.

  

SELECT t.ID

FROM takes t

JOIN course c ON t.course_id = c.course_id

WHERE c.dept_name = 'Computer Science'

GROUP BY t.ID

HAVING COUNT(DISTINCT t.course_id) = (

    SELECT COUNT(*) FROM course WHERE dept_name = 'Computer Science'

);

  
  

-- 12. Find product IDs that were sold in 'January' but NOT in 'February'.

  

SELECT DISTINCT product_id FROM sales WHERE month = 'January'

AND product_id NOT IN (SELECT product_id FROM sales WHERE month = 'February');

  
  

-- 13. Given a table 'Post' with a column 'tags' (text array), find all posts that contain the

-- tags 'sql' and 'database'.

  

SELECT *

FROM Post

WHERE ARRAY['sql', 'database'] <@ tags;

  
  

-- 14. Query a JSONB column 'data' to find records where the key 'active' is set to true.

  

SELECT * FROM tablename

WHERE data->>'active' = 'true';

  
  

-- 15. Find the names of employees whose salary is higher than the average salary of the

-- entire company.

  

SELECT name

FROM employees

WHERE salary > (SELECT AVG(salary) FROM employees);
```