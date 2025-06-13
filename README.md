# 🎓 University Examination System Database

This project implements a **relational database schema** for managing a University Examination System. It covers core components such as **students**, **faculty members**, **departments**, **courses**, **exams**, and **exam attempts**. The schema ensures all key relationships are captured, including course enrollments, exam creation, coordination, teaching assignments, and student performance tracking.

---

## 🔍 Key Features

- Faculty members can act as department heads, course coordinators, and exam creators.
- Each student is enrolled in a department and can take multiple courses.
- Course enrollments include attendance tracking.
- Exams are tied to courses and created by faculty.
- Each student may have multiple attempts per exam with marks and dates recorded.
- Real-world academic roles and relationships reflected using foreign keys.

---

## 🧱 Database Schema & Table Definitions

### 1. `Faculty` Table

```sql
CREATE TABLE Faculty (
    Faculty_ID INT PRIMARY KEY,
    Emp_Name VARCHAR(100),
    Designation VARCHAR(50)
);
```

### 2. `Department` Table

```sql
CREATE TABLE Department (
    Dept_ID INT PRIMARY KEY,
    Dept_Name VARCHAR(100),
    Head_Faculty_ID INT,
    FOREIGN KEY (Head_Faculty_ID) REFERENCES Faculty(Faculty_ID)
);
```

### 3. `Course` Table

```sql
CREATE TABLE Course (
    Course_Code VARCHAR(10) PRIMARY KEY,
    Title VARCHAR(100),
    Dept_ID INT,
    Coordinator_ID INT,
    FOREIGN KEY (Dept_ID) REFERENCES Department(Dept_ID),
    FOREIGN KEY (Coordinator_ID) REFERENCES Faculty(Faculty_ID)
);
```

### 4. `Student` Table

```sql
CREATE TABLE Student (
    Roll_No INT PRIMARY KEY,
    Student_Name VARCHAR(100),
    Dept_ID INT,
    FOREIGN KEY (Dept_ID) REFERENCES Department(Dept_ID)
);
```

### 5. `Student_Course` (Enrollment) Table

```sql
CREATE TABLE Student_Course (
    Roll_No INT,
    Course_Code VARCHAR(10),
    Attendance_Percentage DECIMAL(5,2),
    PRIMARY KEY (Roll_No, Course_Code),
    FOREIGN KEY (Roll_No) REFERENCES Student(Roll_No),
    FOREIGN KEY (Course_Code) REFERENCES Course(Course_Code)
);
```

### 6. `Exam` Table

```sql
CREATE TABLE Exam (
    Exam_ID INT PRIMARY KEY,
    Title VARCHAR(100),
    Subject_Name VARCHAR(100),
    Duration INT,
    Exam_Date DATE,
    Exam_Type VARCHAR(20),
    Course_Code VARCHAR(10),
    Created_By INT,
    FOREIGN KEY (Course_Code) REFERENCES Course(Course_Code),
    FOREIGN KEY (Created_By) REFERENCES Faculty(Faculty_ID)
);
```

### 7. `Exam_Attempt` Table

```sql
CREATE TABLE Exam_Attempt (
    Attempt_ID INT PRIMARY KEY,
    Exam_ID INT,
    Roll_No INT,
    Attempt_Number INT,
    Marks INT,
    FOREIGN KEY (Exam_ID) REFERENCES Exam(Exam_ID),
    FOREIGN KEY (Roll_No) REFERENCES Student(Roll_No)
);
```

---

## 🔗 Relationships Summary

- **Faculty–Department**: A department is headed by one faculty member.
- **Faculty–Course**: A faculty can coordinate and teach multiple courses.
- **Department–Course**: One department offers many courses.
- **Student–Department**: A student belongs to one department.
- **Student–Course**: Many-to-many relationship via `Student_Course`.
- **Exam–Course**: Each exam belongs to a specific course.
- **Exam–Faculty**: Created by a faculty member.
- **Exam_Attempt**: Records all student attempts for exams.

---

## 📌 Notes

- All primary and foreign keys are enforced to maintain referential integrity.
- Attendance and exam records allow tracking of student performance.
- This schema can be easily extended with grading systems, notifications, or online assessment tools.

![image](https://github.com/user-attachments/assets/bda982a2-bd50-445f-a868-ece5a89b7841)

![image](https://github.com/user-attachments/assets/00c7c00c-7fa2-4e8d-8a66-4a35e061ae3c)






