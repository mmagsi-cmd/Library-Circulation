# Library Circulation Analytics
**Project 2** | *Professor Montalvo*  
**By Muhammad Jawad Magsi**

A **SQLite-powered library analytics system** tracking books, loans, fines, and staff performance. Built with ERD, schema, data import, 15 analytical queries, 3 views, data quality checks, and performance optimization.

---

## Project Summary

| Week | Deliverable | Status |
|------|-----------|--------|
| **1** | ERD (dbdiagram.io) | Done |
| **2** | `library_schema.sql` | Done |
| **3** | CSV → SQLite Import | Done |
| **4** | Queries #1–#8 | Done |
| **5** | Queries #9–#15 + Views | Done |
| **6** | DQ Checks + Index Tuning | Done |

---

## ERD (Designed in dbdiagram.io)

```dbml
Table Author { AuthorID int [pk], Name varchar, Nationality varchar, BirthYear int }
Table Book { BookID int [pk], Title varchar, AuthorID int [ref: > Author.AuthorID], ISBN varchar [unique], Genre varchar, YearPublished int, Status varchar }
Table Member { MemberID int [pk], Name varchar, Email varchar [unique], Phone varchar, Address varchar, MembershipDate date }
Table Staff { StaffID int [pk], Name varchar, Role varchar, Email varchar [unique] }
Table Loan { LoanID int [pk], BookID int [ref: > Book.BookID], MemberID int [ref: > Member.MemberID], StaffID int [ref: > Staff.StaffID], LoanDate date, DueDate date, ReturnDate date }
Table Fine { FineID int [pk], LoanID int [ref: > Loan.LoanID], Amount decimal, Status varchar, Date date }

PRAGMA foreign_keys = ON;

CREATE TABLE Author (AuthorID INTEGER PRIMARY KEY, Name TEXT NOT NULL, Nationality TEXT, BirthYear INTEGER);
CREATE TABLE Book (BookID INTEGER PRIMARY KEY, Title TEXT NOT NULL, AuthorID INTEGER NOT NULL, ISBN TEXT UNIQUE, Genre TEXT, YearPublished INTEGER CHECK (YearPublished > 0), Status TEXT CHECK (Status IN ('Available','CheckedOut','Lost','Damaged')), FOREIGN KEY (AuthorID) REFERENCES Author(AuthorID));
CREATE TABLE Member (MemberID INTEGER PRIMARY KEY, Name TEXT NOT NULL, Email TEXT UNIQUE NOT NULL, Phone TEXT, Address TEXT, MembershipDate TEXT NOT NULL);
CREATE TABLE Staff (StaffID INTEGER PRIMARY KEY, Name TEXT NOT NULL, Role TEXT CHECK (Role IN ('Librarian','Assistant','Admin')), Email TEXT UNIQUE);
CREATE TABLE Loan (LoanID INTEGER PRIMARY KEY, BookID INTEGER NOT NULL, MemberID INTEGER NOT NULL, StaffID INTEGER NOT NULL, LoanDate TEXT NOT NULL, DueDate TEXT NOT NULL, ReturnDate TEXT, FOREIGN KEY (BookID) REFERENCES Book(BookID), FOREIGN KEY (MemberID) REFERENCES Member(MemberID), FOREIGN KEY (StaffID) REFERENCES Staff(StaffID), CHECK (DueDate > LoanDate));
CREATE TABLE Fine (FineID INTEGER PRIMARY KEY, LoanID INTEGER NOT NULL, Amount NUMERIC CHECK (Amount >= 0), Status TEXT CHECK (Status IN ('Unpaid','Paid','Waived')), Date TEXT NOT NULL, FOREIGN KEY (LoanID) REFERENCES Loan(LoanID));

INSERT INTO Author SELECT * FROM Author_stagging;
INSERT INTO Book SELECT BookID, Title, AuthorID, ISBN, Genre, YearPublished, Status FROM Book_stagging;
INSERT INTO Member SELECT * FROM Member_stagging;
INSERT INTO Staff SELECT * FROM Staff_stagging;
INSERT INTO Loan SELECT * FROM Loan_stagging;
INSERT INTO Fine SELECT * FROM Fine_stagging;

