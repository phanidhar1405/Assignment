```sql
create database college;
```

```sql
use college;
```

```sql
create table students(
      student_id int primary key,
      first_name varchar(30),
      last_name varchar(30),
      date_of_birth date,
      email varchar(30),
      phone_number bigint
);
```

## Courses table

```sql
CREATE TABLE courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(15),
    credits INT,
    teacher_id INT ,
    FOREIGN KEY (teacher_id) REFERENCES teachers(teacher_id)
);
```

## Enrollments table

```sql
CREATE TABLE enrollments (
    enrollment_id INT PRIMARY KEY,
    student_id INT,
    course_id INT,
    enrollment_date DATE,
    FOREIGN KEY (student_id) REFERENCES students(student_id),
    FOREIGN KEY (course_id) REFERENCES courses(course_id)
);
```

## Teachers table

```sql
CREATE TABLE teachers (
    teacher_id INT PRIMARY KEY,
    first_name VARCHAR(20),
    last_name VARCHAR(20),
    email VARCHAR(30)
);
```

## Payments table

```sql
CREATE TABLE payments (
    payment_id INT PRIMARY KEY,
    student_id INT,
    amount DECIMAL(10,3),
    payment_date DATE,
    FOREIGN KEY (student_id) REFERENCES students(student_id)
);
```

## Insert into Students table

```sql
INSERT INTO Students (student_id, first_name, last_name, date_of_birth, email, phone_number)
VALUES
    (101, 'Lohith', 'Kumar', '2000-05-15', 'lohith.kumar@example.com', '9876543210'),
    (102, 'Varun', 'Sharma', '2002-08-25', 'varun.sharma@example.com', '8765432109'),
    (103, 'Pavan', 'Reddy', '2003-02-10', 'pavan.reddy@example.com', '7654321098'),
    (104, 'Guna', 'Shekhar', '2002-11-30', 'guna.shekhar@example.com', '8543210987'),
    (105, 'Nikil', 'Raja', '2001-04-05', 'nikil.raju@example.com', '9932109876');
```

## Insert into Courses table

```sql
INSERT INTO Courses (course_id, course_name, credits, teacher_id)
VALUES
    (201, 'Mathematics',4, 401),
    (202, 'Physics',3, 402),
    (203, 'English', 3, 403),
    (204, 'Computer', 4, 401),
    (205, 'History', 3, 404),
    (206, 'Biology', 4, 402),
    (207, 'Economics', 3,403),
    (208, 'Chemistry', 4, 404);
```

## Insert into Enrollments table

```sql
INSERT INTO Enrollments (enrollment_id, student_id, course_id, enrollment_date)
VALUES
    (301, 101,201, '2023-01-05'),
    (302, 102,202, '2023-01-06'),
    (303, 103, 203, '2023-01-07'),
    (304, 104, 201, '2023-01-08'),
    (305, 101, 203, '2023-01-09'),
    (306, 102, null, '2023-01-10'),
    (307, 105, 203, '2023-01-11'),
    (308, 103, 202, '2023-01-12');
```

## Insert into Teachers table

```sql
INSERT INTO Teachers (teacher_id, first_name, last_name, email)
VALUES
    (401, 'Krishna', 'Mukul', 'krishna.mukul@school.edu'),
    (402, 'Sneha','Krupa', 'sneha.krupa@school.edu'),
    (403, 'Ashok','Gupta', 'ashok.gupta@school.edu'),
    (404, 'Preeti','Singh', 'preeti.singh@school.edu');
```

## Insert into Payments table

```sql
INSERT INTO Payments (payment_id, student_id, amount, payment_date)
VALUES
    (901, 101, 1500.00, '2023-02-01'),
    (902, 102, 1200.00, '2023-02-02'),
    (903, 102, 1300.00, '2023-02-03'),
    (904, 101, 1400.00, '2023-02-04'),
    (905, 104, 1100.00, '2023-02-05'),
    (906, 103, 1600.00, '2023-02-06'),
    (907, 102, 1700.00, '2023-02-07'),
	(908, 102, 1100.00, '2023-02-05'),
    (909, 105, 1600.00, '2023-02-06'),
    (910, 102, 1700.00, '2023-02-07'),
    (911, 105, 1800.00, '2023-02-08'),
    (912, 103, 1800.00, '2023-02-08');
```

1. Write an SQL query to insert a new student named John Doe into the "Students" table.

![alt text](image.png)

```sql
insert into students values(106 , 'Abhay','Romeo' , '2001-02-04','abhay.romeo@example.com',8797587952);
```

2. Write an SQL query to enroll an existing student in a course, specifying the enrollment date.

![alt text](image-1.png)

```sql
insert into enrollments values(309,103,201,'2023-02-01');
```

3. Update the email address of a teacher in the "Teachers" table.

![alt text](image-2.png)

```sql
update teachers
set email = 'preeti.singh300@school.edu'
where teacher_id = 404;
```

4. Write an SQL query to delete a specific enrollment record, choosing based on the student and course.

![alt text](image-3.png)

```sql
delete from enrollments where student_id = 103 and course_id = 201;
```

5. Update a course to assign a specific teacher using the "Courses" table.

![alt text](image-4.png)

```sql
update courses
set teacher_id = 402
where course_id = 204;
```

6. Write an SQL query to calculate the total payments made by a specific student.

![alt text](image-5.png)

```sql
select SUM(amount) from payments
where student_id = 102;
```

7. Retrieve a list of courses along with the count of students enrolled in each.

![alt text](image-6.png)

```sql
select course_id , count(student_id) from enrollments where course_id is not null group by course_id;
```

8. Find the names of students who have not enrolled in any course.

![alt text](image-7.png)

```sql
select first_name , last_name from enrollments as e
inner join students as s
on e.student_id = s.student_id
where course_id IS null
```

9. Retrieve the first name and last name of students, along with the names of the courses they are enrolled in.

![alt text](image-8.png)

```sql
select s.first_name,s.last_name,c.course_name from enrollments as e
inner join students as s on e.student_id = s.student_id
inner join courses as c on e.course_id = c.course_id;
```

10. List names of teachers and the courses they are assigned to.

![alt text](image-9.png)

```sql
select t.first_name , t.last_name , c.course_name from courses as c
inner join teachers as t
on c.teacher_id = t.teacher_id
```

11. Calculate the average number of students enrolled in each course using aggregate functions.

![alt text](image-10.png)

```sql
select c.course_name ,count(s.student_id)%7  as total from enrollments as e
inner join students as s on e.student_id = s.student_id
inner join courses as c on e.course_id = c.course_id
group by c.course_name;
```

12. Identify the student(s) who made the highest payment using a subquery.

![alt text](image-11.png)

```sql
SELECT top 2 s.student_id, s.first_name, s.last_name, SUM(p.amount)  AS total_payments
FROM students s
JOIN payments p ON s.student_id = p.student_id
GROUP BY s.student_id, s.first_name, s.last_name
ORDER BY total_payments DESC;
```

13. Retrieve a list of courses with the highest number of enrollments using subqueries.

![alt text](image-12.png)

```sql
SELECT course_id, course_name, num_enrollments
FROM (
    SELECT
        c.course_id,
        c.course_name,
        (
            SELECT COUNT(*)
            FROM enrollments e
            WHERE e.course_id = c.course_id
        ) AS num_enrollments
    FROM courses c
) AS course_enrollments
WHERE num_enrollments = (
    SELECT MAX(num_enrollments)
    FROM (
        SELECT COUNT(*) AS num_enrollments
        FROM enrollments
        GROUP BY course_id
    ) AS max_enrollments
);
```

14. Calculate the total payments made to courses taught by each teacher using subqueries.

![alt text](image-13.png)

```sql
SELECT
    t.teacher_id,
    t.first_name,
    t.last_name,
    (
        SELECT SUM(p.amount)
        FROM payments p
        inner join enrollments e ON p.student_id = e.student_id
        inner join courses c ON e.course_id = c.course_id
        WHERE c.teacher_id = t.teacher_id
    ) AS total_payments
FROM teachers t;
```

15. Identify students who are enrolled in more than one course.

![alt text](image-14.png)

```sql
SELECT s.student_id, s.first_name, s.last_name, COUNT(e.course_id) AS courses_enrolled
FROM students s
JOIN enrollments e ON s.student_id = e.student_id
GROUP BY s.student_id, s.first_name, s.last_name
HAVING COUNT(e.course_id) > 1;
```
