# 📚 Constraint-Based Exam Scheduling Engine

Live Demo: https://examscheduler.streamlit.app

## 🚀 Overview

This project implements a constraint-based exam scheduling system using Google OR-Tools (CP-SAT solver) and real enrollment-style data (~1000 students, ~100 courses).

The goal is to generate a clash-free exam timetable while respecting student-centric fairness constraints.

The optimization engine is wrapped in a Streamlit web app that allows:

- Viewing the full global exam timetable
- Inspecting personalized schedules per student
- Analyzing fairness and exam load metrics

---

## 🧠 Problem Formulation

The scheduling problem is modeled as a Constraint Satisfaction / Optimization Problem.

### Decision Variables
- `x[c, t] = 1` if course `c` is assigned to time slot `t`

### Hard Constraints
- Each course must be assigned to exactly one time slot.
- No student can have two exams in the same time slot.
- Each student may have at most **2 exams per day**.

### Objective
- Minimize the total number of time slots used, compressing the exam period while satisfying all constraints.

The model is solved using Google OR-Tools CP-SAT solver.

---

## 📊 Data

The dataset consists of student-course interactions (rating = 1 indicates enrollment).

From the full dataset:
- Students filtered to those enrolled in 5–8 courses
- 1000 students randomly sampled
- ~100 unique courses scheduled

---

## 📈 Results

The solver consistently returns **OPTIMAL** solutions under the specified constraints.

Example properties of generated schedules:

- No exam conflicts per student
- Max 2 exams per day per student
- Balanced distribution of exams across days
- Compressed time horizon via slot minimization

---

## 🖥️ UI

Built using Streamlit.

Features:
- Global timetable view
- Per-student personalized schedule view
- Fairness metrics:
  - Maximum exams per day (any student)
  - Average exam span per student
  - Exams per day distribution chart

---

## 🛠 Tech Stack

- Python
- Google OR-Tools (CP-SAT)
- Pandas
- Streamlit
- Git + GitHub
- Streamlit Community Cloud (deployment)

---

## 🔮 Future Improvements

- Add room capacity constraints
- Add instructor availability constraints
- Treat consecutive-day exams as soft penalties
- Allow dynamic re-solving via UI controls
- Support multi-campus scheduling

---

## 📌 Why This Matters

Exam scheduling is a real-world NP-hard timetabling problem.

This project demonstrates:
- Constraint modeling
- Optimization reasoning
- Feasibility and stress testing
- System design thinking
- Lightweight productization with a live UI
- ## 📚 Dataset

The dataset used in this project originates from a publicly available student-course interaction dataset (via Kaggle).

It contains anonymized user–course enrollment records. For this project:
- Only enrollments (rating = 1) were used.
- Students with 5–8 enrolled courses were selected.
- A subset of 1000 students was sampled to construct the scheduling instance.

Original dataset source:https://www.kaggle.com/datasets/ddatad/course-enrollments-dataset?resource=download
