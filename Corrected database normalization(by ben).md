### Scenario

Conside the following data from a school:

| Student Name  | Fees Paid | Date of Birth | Address                             | Subject 1              | Subject 2                 | Subject 3          | Subject 4 | Teacher Name   | Teacher Address               | Course Name      |
|---------------|-----------|---------------|-------------------------------------|------------------------|---------------------------|--------------------|-----------|----------------|-------------------------------|------------------|
| John Smith    | 18-Jul-00 | 04-Aug-91     | 3 Main Street, North Boston 56125   | Economics 1 (Business) | Biology 1 (Science)       |                    |           | James Peterson | 44 March Way, Glebe 56100     | Economics        |
| Maria Griffin | 14-May-01 | 10-Sep-92     | 16 Leeds Road, South Boston 56128   | Biology 1 (Science)    | Business Intro (Business) | Programming 2 (IT) |           | James Peterson | 44 March Way, Glebe 56100     | Computer Science |
| Susan Johnson | 03-Feb-01 | 13-Jan-91     | 21 Arrow Street, South Boston 56128 | Biology 2 (Science)    |                           |                    |           | Sarah Francis  |                               | Medicine         |
| Matt Long     | 29-Apr-02 | 25-Apr-92     | 14 Milk Lane,Â South Boston 56128   |                        |                           |                    |           | Shane Cobson   | 105 Mist Road, Faulkner 56410 | Dentistry        |

## Tasks

1. Normalize this table up to **3NF** [(see slides from class here)](https://https://docs.google.com/presentation/d/1sADUiD8YFt88YvV8UyHVhhPe7ks8K8Xpp3y-WPDJ2zc/edit#slide=id.p)

**Table 1: Student information**

| id | Student Name  | Fees Paid | Date of Birth | Address                             | Course Name      |
|----|---------------|-----------|---------------|-------------------------------------|------------------|
| 1  | John Smith    | 18-Jul-00 | 04-Aug-91     | 3 Main Street, North Boston 56125   | Economics        |
| 2  | Maria Griffin | 14-May-01 | 10-Sep-92     | 16 Leeds Road, South Boston 56128   | Computer Science |
| 3  | Susan Johnson | 03-Feb-01 | 13-Jan-91     | 21 Arrow Street, South Boston 56128 | Medicine         |
| 4  | Matt Long     | 29-Apr-02 | 25-Apr-92     | 14 Milk Lane,Â South Boston 56128   | Dentistry        |




**Table 2: Subjects**

| id | Subject         | Type     |
|----|-----------------|----------|
| 1  | Biology 1       | Science  |
| 2  | Biology 2       | Science  |
| 3  | Business Intro  | Business |
| 4  | Economics 1     | Business |
| 5  t| Programming 2   | IT       |



**Table 3: Teacher information**

| id | Teacher Name   | Teacher Address               |
|----|----------------|-------------------------------|
| 1  | James Peterson | 44 March Way, Glebe 56100     |
| 2  | Sarah Francis  |                               |
| 3  | Shane Cobson   | 105 Mist Road, Faulkner 56410 |



**Table 4: Student-Subject relationship**

| id | student_id | subject_id |
|----|------------|------------|
| 1  | 1          | 4          |
| 2  | 1          | 1          |
| 3  | 2          | 1          |
| 4  | 2          | 3          |
| 5  | 2          | 5          |
| 6  | 3          | 2          |
| 7  | 4          |            |



**Table 5: Teacher-Subject relationship**

| id | teacher_id | subject_id |
|----|------------|------------|
| 1  | 1          | 1          |
| 2  | 1          | 3          |
| 3  | 1          | 4          |
| 4  | 1          | 5          |
| 5  | 2          | 2          |
| 6  | 3          |            |




2. Create the ER diagram for the normalized database.
