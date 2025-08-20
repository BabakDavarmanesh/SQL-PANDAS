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

## Pandas-ready data (dictionary format)

Use the following dictionaries to recreate the example inputs as pandas DataFrames:

```python
import pandas as pd

students_dict = {
    "student_id": [1, 2, 13, 6],
    "student_name": ["Alice", "Bob", "John", "Alex"],
}
students_df = pd.DataFrame(students_dict)

subjects_dict = {
    "subject_name": ["Math", "Physics", "Programming"],
}
subjects_df = pd.DataFrame(subjects_dict)

examinations_dict = {
    "student_id":   [1, 1, 1, 2, 1, 1, 13, 13, 13, 2, 1],
    "subject_name": ["Math", "Physics", "Programming", "Programming",
                     "Physics", "Math", "Math", "Programming", "Physics",
                     "Math", "Math"],
}
examinations_df = pd.DataFrame(examinations_dict)
```

---

## Example Pandas solution

```python
# Cartesian product of students and subjects to ensure all pairs are present
pairs = students_df.assign(key=1).merge(subjects_df.assign(key=1), on="key").drop(columns="key")

# Count exam attendances per (student_id, subject_name)
counts = (
    examinations_df
    .groupby(["student_id", "subject_name"])
    .size()
    .reset_index(name="attended_exams")
)

# Join counts to all pairs; fill missing with 0
result = (
    pairs
    .merge(counts, on=["student_id", "subject_name"], how="left")
    .fillna({"attended_exams": 0})
    .astype({"attended_exams": int})
    .merge(students_df, on="student_id")  # ensure student_name present (redundant if already in pairs)
    [["student_id", "student_name", "subject_name", "attended_exams"]]
    .sort_values(["student_id", "subject_name"])
    .reset_index(drop=True)
)
```

---

## Example SQL (portable idea)

```sql
-- Create all student/subject pairs, then left join counts from Examinations.
WITH pairs AS (
  SELECT s.student_id, s.student_name, sub.subject_name
  FROM Students s
  CROSS JOIN Subjects sub
),
counts AS (
  SELECT e.student_id, e.subject_name, COUNT(*) AS attended_exams
  FROM Examinations e
  GROUP BY e.student_id, e.subject_name
)
SELECT p.student_id, p.student_name, p.subject_name, COALESCE(c.attended_exams, 0) AS attended_exams
FROM pairs p
LEFT JOIN counts c
  ON p.student_id = c.student_id
 AND p.subject_name = c.subject_name
ORDER BY p.student_id, p.subject_name;
```