# 🗄️ Database Schema: Student Semester Planner & GPA Calculator

This document provides a technical breakdown of the `[DB] Backend` databases.

---

## Database 1: Courses

| Property Name | Type | Purpose |
| --- | --- | --- |
| **Course Name** | `Title` | Name of the course (e.g., "Linear Algebra"). |
| **Professor** | `Text` | Instructor's name. |
| **Credits** | `Number` | Credit hours for the course. |
| **Grade (%)** | `Number` | Current or final percentage grade (0–100). |
| **GPA Points** | `Formula` | Converts percentage to GPA scale (0.0–4.0). |
| **Letter Grade** | `Formula` | Converts percentage to letter grade (A, B, C...). |
| **Status** | `Select` | `In Progress`, `Completed`, `Dropped`. |
| **Assignments** | `Relation` | Links to the Assignments database. |
| **Semester** | `Select` | e.g., `Fall 2025`, `Spring 2026`. |
| **Room / Time** | `Text` | Class schedule info. |

## Formula 2.0 Logic — GPA Points
```javascript
if(prop("Grade (%)") >= 90, 4.0,
  if(prop("Grade (%)") >= 80, 3.0,
    if(prop("Grade (%)") >= 70, 2.0,
      if(prop("Grade (%)") >= 60, 1.0, 0.0)
    )
  )
)
```

## Formula 2.0 Logic — Letter Grade
```javascript
ifs(
  prop("Grade (%)") >= 90, "A",
  prop("Grade (%)") >= 80, "B",
  prop("Grade (%)") >= 70, "C",
  prop("Grade (%)") >= 60, "D",
  "F"
)
```

---

## Database 2: Assignments

| Property Name | Type | Purpose |
| --- | --- | --- |
| **Assignment Name** | `Title` | Name of the assignment or exam. |
| **Course** | `Relation` | Links back to the Courses database. |
| **Type** | `Select` | `Homework`, `Quiz`, `Midterm`, `Final`, `Project`. |
| **Due Date** | `Date` | Deadline for submission. |
| **Status** | `Select` | `Not Started`, `In Progress`, `Submitted`, `Graded`. |
| **Grade (%)** | `Number` | Score received on this assignment. |
| **Weight (%)** | `Number` | How much this assignment counts toward the final grade. |
| **Progress Bar** | `Formula` | Visual progress bar for assignment completion. |
| **Notes** | `Text` | Study notes or submission instructions. |

## Formula 2.0 Logic — Progress Bar
```javascript
slice("▓▓▓▓▓▓▓▓▓▓", 0, round(prop("Grade (%)") / 10))
```

## Architectural Notes
- **Vault Method:** Both databases reside in `[DB] Backend`. The dashboard uses Linked Views.
- **GPA Calculator:** A summary section on the dashboard uses a Rollup on the Courses database to calculate the weighted semester GPA.
