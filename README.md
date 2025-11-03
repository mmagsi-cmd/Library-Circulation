# 📚 Library Circulation Analytics  
**Project 2** | Professor Montalvo  
**By Muhammad Jawad Magsi**  
*Completed: October 24, 2025*

A **complete SQLite-based library management and analytics system** built over 6 weeks.  
Includes ERD, schema creation, data import with staging fixes, analytical SQL queries, database views, data quality checks, and performance optimization.

---

## 🧠 Project Overview
This project simulates a **Library Circulation System** to track and analyze:
- Books, Authors, Members, Staff, Loans, and Fines  
- Circulation patterns, overdue rates, and fine collections  
- Staff performance and member activity  
- Data quality and indexing for performance improvement  

The project was implemented using **SQLite** and **dbdiagram.io** with structured weekly milestones.

---

## 🗂️ Week 1 – ERD Design
Created an **Entity Relationship Diagram (ERD)** using **dbdiagram.io** to define relationships between:
- Author  
- Book  
- Member  
- Staff  
- Loan  
- Fine  

📄 *Deliverables:* `ERD.png` + dbdiagram.io link  

---

## 🧱 Week 2 – Schema Creation
Designed normalized database tables with:
- Primary Keys and Foreign Keys  
- Unique and Check Constraints  
- Referential Integrity  

Example:
```sql
CHECK (Status IN ('Available', 'CheckedOut', 'Lost', 'Damaged'));
CHECK (DueDate > LoanDate);
```

---

## 💾 Week 3 – Sample Data Import

Built datasets in **Google Sheets**, exported as **CSV**, and imported into **SQLite**.  
Used **staging tables** and `INSERT ... SELECT` commands to resolve import errors and ensure clean data loading.

📄 **Deliverables:**  
`authors.csv`, `books.csv`, `members.csv`, `loans.csv`, `fines.csv`

---

## 📊 Week 4 – First Reports (Queries #1–#8)

Analytical SQL queries for core library operations:

1. List all books with their authors  
2. Count books per author  
3. List members with overdue books  
4. Total fines collected (paid only)  
5. Books currently checked out  
6. Top 5 members with most loans  
7. Average fine amount by status  
8. Loans processed by each staff member  

📄 **Deliverable:** `reports.sql`

---

## 📈 Week 5 – Final Reports & Views (Queries #9–#15)

Advanced analytical queries providing deeper insights:

- Loans per genre  
- Average loan duration  
- Members with unpaid fines  
- Most active staff  
- Monthly loan summary  
- Overdue rate (%)  
- Top 5 most borrowed books  

### 📘 Database Views
| View | Description |
|------|--------------|
| `v_patron_activity` | Member activity summary (loans, fines, durations) |
| `v_branch_performance` | Staff performance (loans handled, fines collected) |
| `v_catalog_status` | Book availability and genre breakdown |

📄 **Deliverables:**  
`final_reports.sql`, `views.sql`

---

## 🧩 Week 6 – Data Quality & Performance

### ✅ Data Quality Checks (`dq_checks.sql`)
Ensured data accuracy and consistency with 5 validation queries:

1. Missing member emails  
2. Books without valid authors  
3. Loans with invalid dates  
4. Fines linked to nonexistent loans  
5. Duplicate ISBNs  

✅ All checks passed successfully — no data errors found.

---

### ⚡ Performance Optimization (`performance.md`)
Used **EXPLAIN QUERY PLAN** to compare execution **before and after indexing**.

**Example 1 – Member Loan Lookup**
```sql
CREATE INDEX idx_member_name ON Member(Name);
```
**Example 2 – Book Genre Filter**
```sql
CREATE INDEX idx_book_genre ON Book(Genre);
```
📈 **Result:** Significant reduction in table scans and improved query speed.

---

## 🧾 Deliverables Summary

| Week | Deliverables | Files |
|------|---------------|-------|
| 1 | ERD | `ERD.png` |
| 2 | Schema | `library_schema.sql` |
| 3 | Sample Data | `*.csv` |
| 4 | Reports | `reports.sql` |
| 5 | Final Reports & Views | `final_reports.sql`, `views.sql` |
| 6 | Data Quality & Performance | `dq_checks.sql`, `performance.md` |

---

## ⚙️ Tools & Technologies
- **SQLite Online**  
- **dbdiagram.io**  
- **Google Sheets**  
- **VS Code / SQL Editor**  
- **GitHub**

---

## 💡 Key Insights
- Identified top genres and most borrowed books  
- Measured staff performance and member activity  
- Analyzed overdue rate and fine collection trends  
- Ensured clean, validated, and indexed database for optimized performance  

---

## ✍️ Author
**Muhammad Jawad Magsi**  
📧 mmagsi@saintpeters.edu





