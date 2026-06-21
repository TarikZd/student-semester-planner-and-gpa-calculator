# 📖 Start Here: Student Semester Planner & GPA Calculator

Welcome to the **Student Semester Planner & GPA Calculator** by **Moorish Dev**. Get organized and start calculating your GPA in under 60 seconds.

---

## ⚡ Quick Start (60 Seconds)

1. **Duplicate this template** → Click `Duplicate` in the top-right corner.
2. **Add your courses** → Click "📚 New Course", enter the course name, semester, and credit hours.
3. **Add assignments** → Click "📝 New Assignment", link it to a course, and set the due date.
4. **Update your grades** → As results come in, update the `Grade (%)` field on each assignment.

---

## 🏗️ Architecture Overview

| Location | What's Here |
| --- | --- |
| **Main Dashboard** | GPA Summary + Linked Views of Courses & Assignments |
| **`[DB] Backend`** | Raw `Courses` and `Assignments` databases |

---

## ✍️ Manual Setup Steps (Required)

### Step 1: Convert GPA Points to a Formula
1. Open `[DB] Backend` → Open the `Courses` database.
2. Click `Grade Points` column → **Edit Property** → Change type to `Formula`.
3. Paste this formula:
```javascript
if(prop("Grade (%)") >= 90, 4.0,
  if(prop("Grade (%)") >= 80, 3.0,
    if(prop("Grade (%)") >= 70, 2.0,
      if(prop("Grade (%)") >= 60, 1.0, 0.0)
    )
  )
)
```

### Step 2: Set Up the Assignment Calendar View
1. On the dashboard's Assignments Linked View → click `+ Add a view` → Choose `Calendar`.
2. Set the calendar date to `Due Date`.
3. Name this view `📅 Deadlines`.

### Step 3: Create Button Blocks
1. On the main dashboard, type `/button`.
2. Create two buttons: `📚 New Course` (adds to Courses DB) and `📝 New Assignment` (adds to Assignments DB).

---

## 🎨 Customization Tips

- **Set your semester** by filtering the Courses Linked View by `Semester = Fall 2025` (or your current term).
- **Color-code by status** — use Notion's color options on the `Status` select property.
- **Export to PDF** — Share your Notion page publicly for professors or advisors to view.

---

*Built by Moorish Dev | Last Updated: June 2026*
