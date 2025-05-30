# postgres-assignment
``` bash
C:\Users\Minfy>psql -U akhilesh -d university_db
Password for user akhilesh:
psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

university_db=> create table students(
university_db(> student_id integer,
university_db(> first_name varchar(50),
university_db(> last_name varchar(50),
university_db(> email varchar(100),
university_db(> date_of_birth date
university_db(> );
CREATE TABLE
university_db=> select * from students;
 student_id | first_name | last_name | email | date_of_birth
------------+------------+-----------+-------+---------------
(0 rows)


university_db=> desc students;
ERROR:  syntax error at or near "desc"
LINE 1: desc students;
        ^
university_db=> describe students;
ERROR:  syntax error at or near "describe"
LINE 1: describe students;
        ^
university_db=> clear
university_db-> describe students;
ERROR:  syntax error at or near "clear"
LINE 1: clear
        ^
university_db=> \d
          List of relations
 Schema |   Name   | Type  |  Owner
--------+----------+-------+----------
 public | students | table | akhilesh
(1 row)


university_db=> \d students
                         Table "public.students"
    Column     |          Type          | Collation | Nullable | Default
---------------+------------------------+-----------+----------+---------
 student_id    | integer                |           |          |
 first_name    | character varying(50)  |           |          |
 last_name     | character varying(50)  |           |          |
 email         | character varying(100) |           |          |
 date_of_birth | date                   |           |          |


university_db=> alter table students add column enrollment_date date;
ALTER TABLE
university_db=> \d students
                          Table "public.students"
     Column      |          Type          | Collation | Nullable | Default
-----------------+------------------------+-----------+----------+---------
 student_id      | integer                |           |          |
 first_name      | character varying(50)  |           |          |
 last_name       | character varying(50)  |           |          |
 email           | character varying(100) |           |          |
 date_of_birth   | date                   |           |          |
 enrollment_date | date                   |           |          |


university_db=> alter table students drop column enrollment_date;
ALTER TABLE
university_db=> \d students
                         Table "public.students"
    Column     |          Type          | Collation | Nullable | Default
---------------+------------------------+-----------+----------+---------
 student_id    | integer                |           |          |
 first_name    | character varying(50)  |           |          |
 last_name     | character varying(50)  |           |          |
 email         | character varying(100) |           |          |
 date_of_birth | date                   |           |          |


university_db=> alter table students alter column email type varchar(150);
ALTER TABLE
university_db=> \d students
                         Table "public.students"
    Column     |          Type          | Collation | Nullable | Default
---------------+------------------------+-----------+----------+---------
 student_id    | integer                |           |          |
 first_name    | character varying(50)  |           |          |
 last_name     | character varying(50)  |           |          |
 email         | character varying(150) |           |          |
 date_of_birth | date                   |           |          |


university_db=> alterv table  students rename column date_of_birth to dob;
ERROR:  syntax error at or near "alterv"
LINE 1: alterv table  students rename column date_of_birth to dob;
        ^
university_db=> alter table  students rename column date_of_birth to dob;
ALTER TABLE
university_db=> \d students
                       Table "public.students"
   Column   |          Type          | Collation | Nullable | Default
------------+------------------------+-----------+----------+---------
 student_id | integer                |           |          |
 first_name | character varying(50)  |           |          |
 last_name  | character varying(50)  |           |          |
 email      | character varying(150) |           |          |
 dob        | date                   |           |          |


university_db=> alter table students add constraint unique_email unique(email);
ALTER TABLE
university_db=> alter table add column p.no varchar(4):
university_db-> ;
ERROR:  syntax error at or near "column"
LINE 1: alter table add column p.no varchar(4):
                        ^
university_db=> alter table add column p.no varchar(4);
ERROR:  syntax error at or near "column"
LINE 1: alter table add column p.no varchar(4);
                        ^
university_db=> alter table students add column p.no varchar(4);
ERROR:  syntax error at or near "."
LINE 1: alter table students add column p.no varchar(4);
                                         ^
university_db=> alter table students add column p-no varchar(4);
ERROR:  syntax error at or near "-"
LINE 1: alter table students add column p-no varchar(4);
                                         ^
university_db=> alter table students add column p_no varchar(4);
ALTER TABLE
university_db=> alter table students drop column p_no;
ALTER TABLE
university_db=> \d students
                       Table "public.students"
   Column   |          Type          | Collation | Nullable | Default
------------+------------------------+-----------+----------+---------
 student_id | integer                |           |          |
 first_name | character varying(50)  |           |          |
 last_name  | character varying(50)  |           |          |
 email      | character varying(150) |           |          |
 dob        | date                   |           |          |
Indexes:
    "unique_email" UNIQUE CONSTRAINT, btree (email)


university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob)
university_db-> VALUES (1, 'Alice', 'Smith', 'alice.smith@example.com', '2003-05-15');
INSERT 0 1
university_db=>
university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob)
university_db-> VALUES (2, 'Bob', 'Johnson', 'bob.johnson@example.com', '2002-08-22'),
university_db->        (3, 'Charlie', 'Brown', 'charlie.brown@example.com', '2003-01-10');
INSERT 0 2
university_db=> select * from students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(3 rows)


university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob) values(4,Rohit,sharma,hitman@gmail.com,30-04-1987),(5,Virat,kohli,king@gmail.com,2-11-1988);
ERROR:  column "rohit" does not exist
LINE 1: ...t_id, first_name, last_name, email, dob) values(4,Rohit,shar...
                                                             ^
university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob) values(4,"Rohit","sharma","hitman@gmail.com",30-04-1987),(5,"Virat","kohli","king@gmail.com",2-11-1988);
ERROR:  column "Rohit" does not exist
LINE 1: ...t_id, first_name, last_name, email, dob) values(4,"Rohit","s...
                                                             ^
university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob) values(4,"Rohit","sharma","hitman@gmail.com",'30-04-1987'),(5,"Virat","kohli","king@gmail.com",'2-11-1988');
ERROR:  column "Rohit" does not exist
LINE 1: ...t_id, first_name, last_name, email, dob) values(4,"Rohit","s...
                                                             ^
university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob) values(4,'Rohit','sharma','hitman@gmail.com','30-04-1987'),(5,'Virat','kohli','king@gmail.com','2-11-1988');
INSERT 0 2
university_db=> select * from students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | Rohit      | sharma    | hitman@gmail.com          | 1987-04-30
          5 | Virat      | kohli     | king@gmail.com            | 1988-11-02
(5 rows)


university_db=> select * from students where year(dob) between '1995' and '2002';
ERROR:  function year(date) does not exist
LINE 1: select * from students where year(dob) between '1995' and '2...                                     ^
HINT:  No function matches the given name and argument types. You might need to add explicit type casts.
university_db=> select * from students where dob between '1995-00-00' and '2002-00-00';
ERROR:  date/time field value out of range: "1995-00-00"
LINE 1: select * from students where dob between '1995-00-00' and '2...
                                                 ^
HINT:  Perhaps you need a different "datestyle" setting.
university_db=> select * from students where dob between '1995-01-01' and '2002-01-01';
 student_id | first_name | last_name | email | dob
------------+------------+-----------+-------+-----
(0 rows)


university_db=> select * from students where dob between '1995-01-01' and '2004-01-01';
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(3 rows)


university_db=> select * from students where first_name ilike '%a%;
university_db'> select * from students where first_name ilike '%a%';
university_db'> select * from students where first_name ILIKE '%a%';
university_db'> ;
university_db'>
university_db'>
university_db'>
university_db'> clear
university_db'> ;
university_db'>
university_db'> select * from students;
university_db'> \q

C:\Users\Minfy>psql -U akhilesh -d university_db
Password for user akhilesh:
psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

university_db=> select * from students where firts_name ilike '%a%' ;
ERROR:  column "firts_name" does not exist
LINE 1: select * from students where firts_name ilike '%a%' ;
                                     ^
HINT:  Perhaps you meant to reference the column "students.first_name".university_db=> select * from students where first_name ilike '%a%' ;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          5 | Virat      | kohli     | king@gmail.com            | 1988-11-02
(3 rows)


university_db=> select * from students where student_id=2;
 student_id | first_name | last_name |          email          |    dob
------------+------------+-----------+-------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com | 2002-08-22
(1 row)


university_db=> select * from students where dob<'2003-01-01';
 student_id | first_name | last_name |          email          |    dob
------------+------------+-----------+-------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com | 2002-08-22
          4 | Rohit      | sharma    | hitman@gmail.com        | 1987-04-30
          5 | Virat      | kohli     | king@gmail.com          | 1988-11-02
(3 rows)


university_db=> select * from students where first_name ilike '%a%'or '%c%' ;
ERROR:  invalid input syntax for type boolean: "%c%"
LINE 1: ...elect * from students where first_name ilike '%a%'or '%c%' ;                                                                ^
university_db=> select * from students where first_name ilike '%a%' or '%c%' ;
ERROR:  invalid input syntax for type boolean: "%c%"
LINE 1: ...lect * from students where first_name ilike '%a%' or '%c%' ;
                                                                ^
university_db=> select * from students where first_name ilike '%a%' or '%c%';
ERROR:  invalid input syntax for type boolean: "%c%"
LINE 1: ...elect * from students where first_name ilike '%a%' or '%c%';
                                                                 ^
university_db=> select * from students where first_name ilike '%a%' or ilike '%c%';
ERROR:  type "ilike" does not exist
LINE 1: ...t * from students where first_name ilike '%a%' or ilike '%c%...
                                                             ^
university_db=> select * from students where first_name ilike '%a%' or first_name ilike '%c%';
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          5 | Virat      | kohli     | king@gmail.com            | 1988-11-02
(3 rows)


university_db=> select * from students where first_name ilike '%c%' or first_name ilike '%c%';
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(2 rows)


university_db=> select * from students where email='example.com';
 student_id | first_name | last_name | email | dob
------------+------------+-----------+-------+-----
(0 rows)


university_db=> select * from students where email='example.com';
 student_id | first_name | last_name | email | dob
------------+------------+-----------+-------+-----
(0 rows)


university_db=> select * from students where email like '%example.com';
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(3 rows)


university_db=> select * from students where email is null;
 student_id | first_name | last_name | email | dob
------------+------------+-----------+-------+-----
(0 rows)


university_db=> update students set email='alice@gmail.com' where student_id=1;
UPDATE 1
university_db=> select * from students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | Rohit      | sharma    | hitman@gmail.com          | 1987-04-30
          5 | Virat      | kohli     | king@gmail.com            | 1988-11-02
          1 | Alice      | Smith     | alice@gmail.com           | 2003-05-15
(5 rows)


university_db=> select * from students order by student_id;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice@gmail.com           | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | Rohit      | sharma    | hitman@gmail.com          | 1987-04-30
          5 | Virat      | kohli     | king@gmail.com            | 1988-11-02
(5 rows)


university_db=> select * from students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | Rohit      | sharma    | hitman@gmail.com          | 1987-04-30
          5 | Virat      | kohli     | king@gmail.com            | 1988-11-02
          1 | Alice      | Smith     | alice@gmail.com           | 2003-05-15
(5 rows)


university_db=> update students set dob='2003-11-11' where last_name=sharma;
ERROR:  column "sharma" does not exist
LINE 1: update students set dob='2003-11-11' where last_name=sharma;
                                                             ^
university_db=> update students set dob='2003-11-11' where last_name='sharma';
UPDATE 1
university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob)
university_db-> VALUES (99, 'Temp', 'User', 'temp@example.com', '2000-01-01');
INSERT 0 1
university_db=> delete from students where student_id=99;
DELETE 1
university_db=> select * from students where student_id=99;
 student_id | first_name | last_name | email | dob
------------+------------+-----------+-------+-----
(0 rows)


university_db=> select * from students order by last_name;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          5 | Virat      | kohli     | king@gmail.com            | 1988-11-02
          4 | Rohit      | sharma    | hitman@gmail.com          | 2003-11-11
          1 | Alice      | Smith     | alice@gmail.com           | 2003-05-15
(5 rows)


university_db=> select * from students order by last_name desc ;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice@gmail.com           | 2003-05-15
          4 | Rohit      | sharma    | hitman@gmail.com          | 2003-11-11
          5 | Virat      | kohli     | king@gmail.com            | 1988-11-02
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(5 rows)


university_db=> select * from students order by dob desc;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          4 | Rohit      | sharma    | hitman@gmail.com          | 2003-11-11
          1 | Alice      | Smith     | alice@gmail.com           | 2003-05-15
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          5 | Virat      | kohli     | king@gmail.com            | 1988-11-02
(5 rows)


university_db=> select * from students order by first_name asc,last_name desc;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice@gmail.com           | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | Rohit      | sharma    | hitman@gmail.com          | 2003-11-11
          5 | Virat      | kohli     | king@gmail.com            | 1988-11-02
(5 rows)


university_db=> select * from students order by first_name offset1;
ERROR:  syntax error at or near "offset1"
LINE 1: select * from students order by first_name offset1;
                                                   ^
university_db=> select * from students order by first_name offset 1;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | Rohit      | sharma    | hitman@gmail.com          | 2003-11-11
          5 | Virat      | kohli     | king@gmail.com            | 1988-11-02
(4 rows)


university_db=> select * from students order by first_name offset 1,limit 2;
ERROR:  syntax error at or near ","
LINE 1: select * from students order by first_name offset 1,limit 2;
                                                           ^
university_db=> select * from students order by first_name offset 1,limit 2;
ERROR:  syntax error at or near ","
LINE 1: select * from students order by first_name offset 1,limit 2;
                                                           ^
university_db=> select * from students order by first_name offset 1 limit 2;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(2 rows)


university_db=> select * from students order by dob  limit 2;
 student_id | first_name | last_name |          email          |    dob
------------+------------+-----------+-------------------------+------------
          5 | Virat      | kohli     | king@gmail.com          | 1988-11-02
          2 | Bob        | Johnson   | bob.johnson@example.com | 2002-08-22
(2 rows)


university_db=> select * from students order by student_id offset 1 limit 2;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(2 rows)


university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob)
university_db-> VALUES (5, 'Eve', 'Smith', 'eve.smith@example.com', '2004-07-01');
INSERT 0 1
university_db=> select last_name from students;
 last_name
-----------
 Johnson
 Brown
 kohli
 Smith
 sharma
 Smith
(6 rows)


university_db=> select distinct last_name from students;
 last_name
-----------
 Smith
 kohli
 Johnson
 sharma
 Brown
(5 rows)


university_db=> select count(*) from students;
 count
-------
     6
(1 row)


university_db=> select count(email) from students;
 count
-------
     6
(1 row)


university_db=> select min(dob) from students;
    min
------------
 1988-11-02
(1 row)


university_db=> select count(email) from students;
 count
-------
     6
(1 row)


university_db=> select count(!email) from students;
ERROR:  operator does not exist: ! character varying
LINE 1: select count(!email) from students;
                     ^
HINT:  No operator matches the given name and argument type. You might need to add an explicit type cast.
university_db=> select count(distinct last_name) from students;
 count
-------
     5
(1 row)


university_db=> select  from students;
--
(6 rows)


university_db=> select * from students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          5 | Virat      | kohli     | king@gmail.com            | 1988-11-02
          1 | Alice      | Smith     | alice@gmail.com           | 2003-05-15
          4 | Rohit      | sharma    | hitman@gmail.com          | 2003-11-11
          5 | Eve        | Smith     | eve.smith@example.com     | 2004-07-01
(6 rows)


university_db=> select last_name,count(*) as last_name_count from students group by last_name;
 last_name | last_name_count
-----------+-----------------
 Smith     |               2
 kohli     |               1
 Johnson   |               1
 sharma    |               1
 Brown     |               1
(5 rows)


university_db=> select last_name,count(*) as last_name_count from students group by last_name having 2>2;
 last_name | last_name_count
-----------+-----------------
(0 rows)


university_db=> select last_name,count(*) as last_name_count from students group by last_name having 2=2;
 last_name | last_name_count
-----------+-----------------
 Smith     |               2
 kohli     |               1
 Johnson   |               1
 sharma    |               1
 Brown     |               1
(5 rows)


university_db=> select last_name,count(*) as last_name_count from students group by last_name having last_name_count=2;
ERROR:  column "last_name_count" does not exist
LINE 1: ...ame_count from students group by last_name having last_name_...
                                                             ^
university_db=> select last_name,count(*) as last_name_count from students group by last_name having count(*)=2;
 last_name | last_name_count
-----------+-----------------
 Smith     |               2
(1 row)


university_db=> drop table students;
DROP TABLE
university_db=> create table students(
university_db(> student_id integer primary_key auto_increment,
university_db(> first_name varchar(50) not null,
university_db(> last_name varchar(50) not null,
university_db(> email varchar(100) unique,
university_db(> dob date,
university_db(> enrollment_status varchar(10) check (enrollment_status
university_db(> in ('enrolled','graduated','dropped')));
ERROR:  syntax error at or near "primary_key"
LINE 2: student_id integer primary_key auto_increment,
                           ^
university_db=> create table students(
university_db(> student_id integer  auto_increment primary_key,
university_db(> first_name varchar(50) not null,
university_db(> last_name varchar(50) not null,
university_db(> email varchar(100) unique,
university_db(> dob date,
university_db(> enrollment_status varchar(10) check (enrollment_status
university_db(> in ('enrolled','graduated','dropped')));
ERROR:  syntax error at or near "auto_increment"
LINE 2: student_id integer  auto_increment primary_key,
                            ^
university_db=> create table students(
university_db(> student_id integer,
university_db(> first_name varchar(50) not null,
university_db(> last_name varchar(50) not null,
university_db(> email varchar(100) unique,
university_db(> dob date,
university_db(> enrollment_status varchar(10) check (enrollment_status
university_db(> in ('enrolled','graduated','dropped')));
CREATE TABLE
university_db=>  drop table students;
DROP TABLE
university_db=> create table students(
university_db(> student_id integer serial primary key,
university_db(> first_name varchar(50) not null,
university_db(> last_name varchar(50) not null,
university_db(> email varchar(100) unique,
university_db(> dob date,
university_db(> enrollment_status varchar(10) check (enrollment_status
university_db(> in ('enrolled','graduated','dropped')));
ERROR:  syntax error at or near "serial"
LINE 2: student_id integer serial primary key,
                           ^
university_db=> create table students(
university_db(> student_id serial primary key,
university_db(> first_name varchar(50) not null,
university_db(> last_name varchar(50) not null,
university_db(> email varchar(100) unique,
university_db(> dob date,
university_db(> enrollment_status varchar(10) check (enrollment_status
university_db(> in ('enrolled','graduated','dropped')));
CREATE TABLE
university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Alice', 'Smith', 'alice.smith@example.com', '2003-05-15', 'enrolled');
INSERT 0 1
university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Robert', 'Johnson', 'robert.j@example.com', '2002-08-22', 'enrolled');
INSERT 0 1
university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Charlie', 'Brown', 'charlie.brown@example.com', '2003-01-10', 'pending');
ERROR:  new row for relation "students" violates check constraint "students_enrollment_status_check"
DETAIL:  Failing row contains (3, Charlie, Brown, charlie.brown@example.com, 2003-01-10, pending).
university_db=> select * from students
university_db-> \q

C:\Users\Minfy>psql -U akhilesh -d university_db
Password for user akhilesh:
^C
C:\Users\Minfy>psql -U akhilesh -d university_db
Password for user akhilesh:
psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Alice', 'Smith', 'alice.smith@example.com', '2003-05-15', 'enrolled');
ERROR:  duplicate key value violates unique constraint "students_email_key"
DETAIL:  Key (email)=(alice.smith@example.com) already exists.
university_db=> select * from students;
 student_id | first_name | last_name |          email          |    dob     | enrollment_status
------------+------------+-----------+-------------------------+------------+-------------------
          1 | Alice      | Smith     | alice.smith@example.com | 2003-05-15 | enrolled
          2 | Robert     | Johnson   | robert.j@example.com    | 2002-08-22 | enrolled
(2 rows)


university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Robert', 'Johnson', 'robert.j@example.com', '2002-08-22', 'enrolled');
ERROR:  duplicate key value violates unique constraint "students_email_key"
DETAIL:  Key (email)=(robert.j@example.com) already exists.
university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Charlie', 'Brown', 'charlie.brown@example.com', '2003-01-10', 'pending');
ERROR:  new row for relation "students" violates check constraint "students_enrollment_status_check"
DETAIL:  Failing row contains (6, Charlie, Brown, charlie.brown@example.com, 2003-01-10, pending).
university_db=>
university_db=>
university_db=>
university_db=>
university_db=>
university_db=>
university_db=> CREATE TABLE courses (
university_db(>     course_id SERIAL PRIMARY KEY,
university_db(>     course_name VARCHAR(100) NOT NULL UNIQUE,
university_db(>     credits INTEGER CHECK (credits > 0 AND credits < 10) -- Example of CHECK
university_db(> );
CREATE TABLE
university_db=>
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Introduction to SQL', 3);
INSERT 0 1
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Database Design', 4);
INSERT 0 1
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Web Development', 3);
INSERT 0 1
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Data Structures', 4);
INSERT 0 1
university_db=> select * from students;
 student_id | first_name | last_name |          email          |    dob     | enrollment_status
------------+------------+-----------+-------------------------+------------+-------------------
          1 | Alice      | Smith     | alice.smith@example.com | 2003-05-15 | enrolled
          2 | Robert     | Johnson   | robert.j@example.com    | 2002-08-22 | enrolled
(2 rows)


university_db=> select * from courses;
 course_id |     course_name     | credits
-----------+---------------------+---------
         1 | Introduction to SQL |       3
         2 | Database Design     |       4
         3 | Web Development     |       3
         4 | Data Structures     |       4
(4 rows)


university_db=> CREATE TABLE enrollments (
university_db(>     enrollment_id SERIAL PRIMARY KEY,
university_db(>     student_id INTEGER NOT NULL,
university_db(>     course_id INTEGER NOT NULL,
university_db(>     enrollment_date DATE DEFAULT CURRENT_DATE, -- Sets default if not specified
university_db(>     grade CHAR(1) CHECK (grade IN ('A', 'B', 'C', 'D', 'F', 'W', NULL)), -- W for withdraw, NULL if not graded
university_db(>
university_db(>     -- Foreign Key constraint for student_id
university_db(>     CONSTRAINT fk_student
university_db(>         FOREIGN KEY (student_id)
university_db(>         REFERENCES students(student_id)
university_db(>         ON DELETE CASCADE, -- If a student is deleted, their enrollments are also deleted.
university_db(>                            -- Other options: ON DELETE RESTRICT, ON DELETE SET NULL, ON DELETE SET DEFAULT
university_db(>
university_db(>     -- Foreign Key constraint for course_id
university_db(>     CONSTRAINT fk_course
university_db(>         FOREIGN KEY (course_id)
university_db(>         REFERENCES courses(course_id)
university_db(>         ON DELETE RESTRICT, -- (Default if not specified) Prevent deleting a course if students are enrolled.
university_db(>
university_db(>     -- Ensure a student cannot enroll in the same course multiple times (if semester isn't a factor)
university_db(>     UNIQUE (student_id, course_id)
university_db(> );
CREATE TABLE
university_db=>
university_db=> INSERT INTO enrollments (student_id, course_id, grade) VALUES (1, 1, 'A');
INSERT 0 1
university_db=> INSERT INTO enrollments (student_id, course_id) VALUES (1, 2);
INSERT 0 1
university_db=> show tables;
ERROR:  unrecognized configuration parameter "tables"
university_db=> show tables();
ERROR:  syntax error at or near "("
LINE 1: show tables();
                   ^
university_db=> \dt
            List of relations
 Schema |    Name     | Type  |  Owner
--------+-------------+-------+----------
 public | courses     | table | akhilesh
 public | enrollments | table | akhilesh
 public | students    | table | akhilesh
(3 rows)


university_db=> select * from courses;
 course_id |     course_name     | credits
-----------+---------------------+---------
         1 | Introduction to SQL |       3
         2 | Database Design     |       4
         3 | Web Development     |       3
         4 | Data Structures     |       4
(4 rows)


university_db=> select * from enrollments;
 enrollment_id | student_id | course_id | enrollment_date | grade
---------------+------------+-----------+-----------------+-------
             1 |          1 |         1 | 2025-05-30      | A
             2 |          1 |         2 | 2025-05-30      |
(2 rows)

```
