DROP TABLE IF EXISTS StudentEnrollments;

CREATE TABLE StudentEnrollments (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(100) NOT NULL,
    course_id VARCHAR(10) NOT NULL,
    enrollment_date DATE NOT NULL
);

INSERT INTO StudentEnrollments (student_id, student_name, course_id, enrollment_date)
VALUES 
(1, 'John', 'CSE101', '2024-06-01'),
(2, 'Alice', 'CSE102', '2024-06-02'),
(3, 'Bob', 'CSE103', '2024-06-03');

SELECT * FROM StudentEnrollments;

START TRANSACTION;

UPDATE StudentEnrollments 
SET enrollment_date = '2024-07-01' 
WHERE student_id = 1;

UPDATE StudentEnrollments 
SET enrollment_date = '2024-07-02' 
WHERE student_id = 2;

COMMIT;

SELECT * FROM StudentEnrollments;

START TRANSACTION;

UPDATE StudentEnrollments 
SET enrollment_date = '2024-08-02' 
WHERE student_id = 2;

UPDATE StudentEnrollments 
SET enrollment_date = '2024-08-01' 
WHERE student_id = 1;

COMMIT;

SELECT * FROM StudentEnrollments;

SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;

START TRANSACTION;

SELECT student_id, student_name, course_id, enrollment_date 
FROM StudentEnrollments 
WHERE student_id = 1;

SELECT SLEEP(5);

SELECT student_id, student_name, course_id, enrollment_date 
FROM StudentEnrollments 
WHERE student_id = 1;

COMMIT;

START TRANSACTION;

UPDATE StudentEnrollments 
SET enrollment_date = '2024-09-15' 
WHERE student_id = 1;

COMMIT;

SELECT * FROM StudentEnrollments;

START TRANSACTION;

SELECT * FROM StudentEnrollments 
WHERE student_id = 1 
FOR UPDATE;

UPDATE StudentEnrollments 
SET enrollment_date = '2024-10-01' 
WHERE student_id = 1;

COMMIT;

SELECT * FROM StudentEnrollments;

START TRANSACTION;

SELECT * FROM StudentEnrollments 
WHERE student_id = 2;

COMMIT;

START TRANSACTION;

UPDATE StudentEnrollments 
SET enrollment_date = '2024-10-15' 
WHERE student_id = 2;

COMMIT;

SELECT * FROM StudentEnrollments ORDER BY student_id;
