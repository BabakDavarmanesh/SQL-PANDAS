# Students' Exam Attendance

Find the number of times each student attended each exam.

Return the result ordered by `student_id` and `subject_name`.

---

## Schema

**Table: `Students`**
```
student_id INT PRIMARY KEY
student_name VARCHAR
```

**Table: `Subjects`**
```
subject_name VARCHAR PRIMARY KEY
```

**Table: `Examinations`**
```
student_id INT
subject_name VARCHAR
-- (May contain duplicates; no primary key)
-- Each student takes every course; each row is an attendance record for an exam.
```

---

## Example

**Input**  

**Students**
| student_id | student_name |
|------------|---------------|
| 1          | Alice         |
| 2          | Bob           |
| 13         | John          |
| 6          | Alex          |

**Subjects**
| subject_name |
|--------------|
| Math         |
| Physics      |
| Programming  |

**Examinations**
| student_id | subject_name |
|------------|--------------|
| 1          | Math         |
| 1          | Physics      |
| 1          | Programming  |
| 2          | Programming  |
| 1          | Physics      |
| 1          | Math         |
| 13         | Math         |
| 13          | Programming  |
| 13         | Physics      |
| 2          | Math         |
| 1          | Math         |

**Output**
| student_id | student_name | subject_name | attended_exams |
|------------|--------------|--------------|----------------|
| 1          | Alice        | Math         | 3              |
| 1          | Alice        | Physics      | 2              |
| 1          | Alice        | Programming  | 1              |
| 2          | Bob          | Math         | 1              |
| 2          | Bob          | Physics      | 0              |
| 2          | Bob          | Programming  | 1              |
| 6          | Alex         | Math         | 0              |
| 6          | Alex         | Physics      | 0              |
| 6          | Alex         | Programming  | 0              |
| 13         | John         | Math         | 1              |
| 13         | John         | Physics      | 1              |
| 13         | John         | Programming  | 1              |

---
