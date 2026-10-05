# SAS for Data Analysts — Complete Course Notes

**Beginner → Intermediate → Advanced → Industry → Interview**

**Focus: Banking, Financial Services, Credit Risk, Fraud and Insurance**

These notes cover **every topic in your 8-session SAS syllabus**: all 151 items, nothing skipped. The
topics are put in the order that makes them easiest to learn. Each topic is linked to what you already
know from **MS SQL Server** and **Python/Pandas**.

**Who this is for:** a Data Analyst with 2+ years of experience in SQL Server, Python, Pandas, Excel,
Power BI and ETL, who wants to work as a SAS Data Analyst or SAS Developer in banking or financial
services, and to pass SAS technical interviews.

**How the writing works:** every idea is explained in short, simple sentences first. Where SAS uses a
special word, the plain meaning comes first and the SAS word comes after it, so you can still use the
right term in an interview. Code, procedure names and SAS keywords are never simplified.

**Symbols used in these notes**

| Symbol | Meaning |
| --- | --- |
| 🔥 | Very important. Do not skip. |
| ⭐ | Asked often in interviews. |
| ⚠️ | A common mistake or trap. |
| 💼 | How it is used in a real bank or insurer. |
| 🚀 | Makes programs faster or lighter. |
| 🧠 | What happens inside SAS. |
| 📌 | Remember this. |
| ✓ / ◐ / ○ | Completed / In progress / Not started (for your progress tracking) |

> **How to run the code:** every program in these notes is complete. You can run it in SAS Studio
> (free through SAS OnDemand for Academics), SAS Enterprise Guide or SAS for Windows. Programs that
> connect to outside systems (SQL Server, Oracle, Hadoop, remote servers) need your company's server
> names and credentials. Those places are clearly marked.

---

## Table of Contents

- [Part 0 — Syllabus Analysis and Learning Roadmap](#part-0--syllabus-analysis-and-learning-roadmap)
- [The SQL ↔ SAS ↔ Python/Pandas Concept Map](#the-sql--sas--pythonpandas-concept-map)
- [Part I — Getting Started with SAS (Modules 1–7)](#part-i--getting-started-with-sas-modules-17)
- [Part II — Getting Data In and Out (Modules 8–12)](#part-ii--getting-data-in-and-out-modules-812)
- [Part III — Core DATA Step Processing (Modules 13–20)](#part-iii--core-data-step-processing-modules-1320)
- [Part IV — SAS Functions (Modules 21–24)](#part-iv--sas-functions-modules-2124)
- [Part V — PROC SQL (Modules 25–32)](#part-v--proc-sql-modules-2532)
- [Part VI — Advanced DATA Step (Modules 33–39)](#part-vi--advanced-data-step-modules-3339)
- [Part VII — Reporting, Summary Statistics and Charts (Modules 40–46)](#part-vii--reporting-summary-statistics-and-charts-modules-4046)
- [Part VIII — Macros and Automation (Modules 47–55)](#part-viii--macros-and-automation-modules-4755)
- [Part IX — Production Skills (Modules 56–59)](#part-ix--production-skills-modules-5659)
- [Part X — Master References](#part-x--master-references)
- [Part XI — Interview Preparation](#part-xi--interview-preparation)
- [Part XII — Capstone Project, Career and Study Modes](#part-xii--capstone-project-career-and-study-modes)

---

# Part 0 — Syllabus Analysis and Learning Roadmap

Before teaching anything, your syllabus was checked as a whole. This part shows what was found and
how the course is organised as a result.

## 0.1 Overall Syllabus Assessment

**What is strong about the syllabus**

- It covers the whole of **Base SAS**: the DATA step, PROC SQL, the main reporting procedures and the
  macro language. Those four areas are what SAS interviews in banks test most.
- It starts from a **SQL ↔ SAS ↔ Pandas map**. That is the right way for someone who already knows
  SQL Server and Pandas to learn SAS quickly.
- It includes the topics that separate a beginner from a working SAS developer: the **PDV**, **@ and
  @@**, **RETAIN**, **FIRST./LAST.**, **PROC TRANSPOSE**, **CALL SYMPUT** and **macro debugging**.
- It covers getting data from real places: text files, Excel, Access, SQL Server, Oracle, remote
  servers and Hadoop.

**What needed fixing**

| Issue | Example in the syllabus | What these notes do |
| --- | --- | --- |
| The same topic appears in several sessions | Functions in Sessions 4 and 6; PROC SQL basics in Sessions 4 and 7; random observations in Sessions 3 and 5 | Each topic is taught once, in depth. Every repeat is still listed and marked as covered. |
| A key idea comes too late | The **PDV** is in Session 3, but you need it to understand Sessions 2, 3 and 5 | The PDV is taught in Module 7, straight after your first datasets. |
| Related topics are split up | Transposing in Sessions 4 and 5; MERGE (Session 7) far from SET (Session 2) | Related topics are grouped into one module. |
| Some items are named after things that do not exist as described | "PROC SQL stored procedures", "truncating tables" in PROC SQL | The notes explain what SAS really offers, and the closest equivalent. |
| Some products are retired | "SAS University Studio" (SAS University Edition) | Explained, with the current free option (SAS OnDemand for Academics). |
| Important industry skills are missing | Hash objects, PROC DATASETS, PROC APPEND, error handling, data quality checks, performance tuning, production scheduling | Added where they fit naturally (see 0.4). |

## 0.2 Topic Dependency Map

An arrow means "learn this first". Learning in this order means you never meet an idea that depends
on something you have not seen yet.

```text
                       What SAS is, interfaces, SAS PC windows
                                        |
                                        v
                 Program structure: DATA step, PROC step, statements
                                        |
                                        v
            Libraries, datasets, variables, naming rules, data types
                                        |
                                        v
                First datasets (DATALINES) ---> SET (dataset to dataset)
                                        |
                                        v
              PDV: how the DATA step compiles and executes   <-- the key idea
                  |                    |                         |
                  v                    v                         v
        Reading raw files     KEEP / DROP / RENAME /       Functions (character,
        INFILE, INPUT, @, @@  WHERE / IF / OUTPUT          numeric, date)
                  |                    |                         |
                  v                    v                         |
        PROC IMPORT/EXPORT,     PROC SORT, formats,              |
        databases, servers      sampling, row numbers            |
                  \                    |                         /
                   \                   v                        /
                    +------> PROC SQL (tables, queries, joins) <+
                                        |
                                        v
         MERGE, RETAIN, FIRST./LAST., PROC RANK, TRANSPOSE, loops, arrays
                                        |
                                        v
       Reporting: PRINT, ODS, MEANS, SUMMARY, UNIVARIATE, FREQ, REPORT, TABULATE, charts
                                        |
                                        v
       Macros: variables, parameters, INTO, CALL SYMPUT, %IF, %DO, debugging, storage
                                        |
                                        v
       Production: debugging, performance, data quality, scheduling, capstone project
```

## 0.3 Duplicate and Overlapping Topics

Every row below is taught **once**, in depth. Both syllabus items are marked as covered.

| Topic | Appears in your syllabus as | Taught in |
| --- | --- | --- |
| SAS programming steps | 1.16 and 2.2 | Module 3 |
| Character functions | 4.1 and 6.1 | Module 21 |
| Numeric functions | 4.2 and 6.2 | Module 22 |
| Datetime functions | 4.3 and 6.3 | Module 23 |
| Selecting random observations | 3.15 and 5.11 | Module 20 |
| Creating tables with PROC SQL | 4.6 and 7.1 | Module 25 |
| Inserting values with PROC SQL | 4.7 and 7.2 | Module 25 |
| New table from an existing table | 4.14 and 7.3 | Module 25 |
| Calculated columns | 4.21 and 7.19 | Module 27 |
| CASE WHEN | 4.18 and 7.10 | Module 28 |
| Summarising data | 4.16 and 7.12 | Module 29 |
| WHERE vs HAVING | 4.17 and 7.13 | Module 29 |
| COALESCE | 4.22 and 7.20 | Module 30 |
| Row numbers in PROC SQL | 7.5 and 7.6 | Module 30 |
| SQL functions | 4.23, 7.21 and 7.22 | Module 30 |
| SQL views | 4.24 and 7.23 | Module 32 |
| SQL stored procedures | 4.25 and 7.24 | Module 32 |
| Transposing | 4.19, 5.1 and 5.2 | Module 36 |
| Joining / merging tables | 4.20, 7.18 and concept map row 8 | Modules 31 and 33 |
| Reading TXT files | 1.17, 3.3 and 3.11 | Modules 8 and 10 |
| Reading CSV files | 1.18 and 3.4 | Module 10 |
| Reading Excel files | 1.19, 3.1 and 3.2 | Module 10 |

## 0.4 Missing Industry Topics (Added to These Notes)

These are not in your syllabus, but SAS jobs in banks expect them. They are added where they fit.

| Added topic | Why it matters at work | Where it is taught |
| --- | --- | --- |
| The SAS log: NOTE, WARNING, ERROR | You will spend more time reading logs than writing code | Modules 3 and 56 |
| LENGTH, LABEL, ATTRIB and truncation | The most common cause of silently cut-off text | Modules 4, 5 and 8 |
| Missing values in depth | Missing numbers sort lowest and pass `< 0` tests | Modules 4, 15 and 22 |
| SELECT / WHEN | A cleaner way to write long IF-ELSE chains | Module 15 |
| PROC DATASETS and PROC APPEND | Managing and adding to datasets without rewriting them | Modules 6 and 31 |
| Hash objects | Fast lookups without sorting; widely used in fraud rules | Modules 33 and 57 |
| LAG and DIF | Comparing with the previous row (e.g. time since last transaction) | Modules 22 and 34 |
| Perl regular expressions (PRXMATCH, PRXCHANGE) | Pulling patterns out of messy text | Module 9 |
| Explicit and implicit SQL pass-through | Making the database do the heavy work | Modules 11 and 57 |
| Dictionary tables | Programs that inspect libraries and build code | Modules 32 and 50 |
| Return codes (&SYSERR, &SYSCC) and error handling | Jobs that stop safely when something fails | Modules 55 and 59 |
| Data quality and reconciliation | Control totals, duplicate keys, orphan records | Module 58 |
| Performance tuning | Programs that finish on 100 million rows | Module 57 |
| Batch running and scheduling | How SAS jobs actually run every night | Modules 55 and 59 |
| SAS Viya awareness | Where modern SAS platforms are heading | Module 1 |

## 0.5 Recommended Learning Order

1. **Part I — Getting started.** What SAS is, its windows, how a program is built, libraries,
   datasets and variables, your first datasets, and the PDV.
2. **Part II — Getting data in and out.** Raw text files, @ and @@, PROC IMPORT and EXPORT, databases,
   remote servers and Hadoop.
3. **Part III — Core DATA step.** KEEP, DROP, RENAME, WHERE, IF, OUTPUT, sorting, formats, sampling
   and row numbers.
4. **Part IV — Functions.** Character, numeric and date functions.
5. **Part V — PROC SQL.** Everything from creating tables to joins and views.
6. **Part VI — Advanced DATA step.** MERGE, RETAIN, FIRST./LAST., PROC RANK, TRANSPOSE, loops, arrays,
   COMPARE and UPDATE.
7. **Part VII — Reporting.** PROC PRINT, ODS, MEANS, SUMMARY, UNIVARIATE, FREQ, REPORT, TABULATE and
   charts.
8. **Part VIII — Macros.** From %LET to scheduled, parameterised automation.
9. **Part IX — Production skills.** Debugging, performance, data quality and production workflows.
10. **Parts X–XII — References, interviews, projects and career.**

**Why this order:** the PDV is moved early because almost every later topic is easier once you know
it. PROC SQL comes after the DATA step basics so you can compare the two styles side by side. Macros
come last because they generate DATA step and PROC SQL code, so you must know that code first.

## 0.6 Complete Learning Roadmap

| Part | Modules | Suggested time (about 1.5 hours a day) |
| --- | --- | --- |
| I — Getting started | 1–7 | Week 1 |
| II — Data in and out | 8–12 | Week 2 |
| III — Core DATA step | 13–20 | Weeks 3–4 |
| IV — Functions | 21–24 | Week 4 |
| V — PROC SQL | 25–32 | Weeks 5–6 |
| VI — Advanced DATA step | 33–39 | Weeks 6–7 |
| VII — Reporting | 40–46 | Week 8 |
| VIII — Macros and automation | 47–55 | Weeks 9–10 |
| IX — Production skills | 56–59 | Week 11 |
| X–XII — Reference, interviews, capstone | — | Week 12 and ongoing |

## 0.7 Module-Wise Topic Mapping (Your Complete Syllabus Checklist)

Every one of your 151 syllabus items is listed here with the module that teaches it. Use the last
column to track your own progress: change ○ to ◐ when you start a topic and to ✓ when you finish it.

**Session 1 — SAS Fundamentals**

| # | Syllabus item | Taught in | Status |
| --- | --- | --- | --- |
| Map | SQL ↔ SAS ↔ Python/Pandas concept mapping (8 rows) | [Concept Map](#the-sql--sas--pythonpandas-concept-map) | ○ |
| 1.1 | What is SAS? | Module 1 | ○ |
| 1.2 | SAS Components | Module 1 | ○ |
| 1.3 | Introduction to SAS PC | Module 1 | ○ |
| 1.4 | Introduction to SAS University Studio | Module 1 | ○ |
| 1.5 | Introduction to SAS Enterprise Guide | Module 1 | ○ |
| 1.6 | SAS Programming | Module 3 | ○ |
| 1.7 | SAS Jargons | Module 3 | ○ |
| 1.8 | Creating the first SAS dataset | Module 5 | ○ |
| 1.9 | Explain SAS Programming | Module 3 | ○ |
| 1.10 | SAS PC Windows and its functionality | Module 2 | ○ |
| 1.11 | SAS Shortcut Keys | Module 2 | ○ |
| 1.12 | Creating SAS dataset from fixed-format text file | Module 8 | ○ |
| 1.13 | SAS Library and Library naming criteria | Module 4 | ○ |
| 1.14 | SAS Dataset and Variable naming criteria | Module 4 | ○ |
| 1.15 | SAS Variable types and values | Module 4 | ○ |
| 1.16 | SAS Programming Steps | Module 3 | ○ |
| 1.17 | Reading TXT file using PROC IMPORT | Module 10 | ○ |
| 1.18 | Reading CSV file using PROC IMPORT | Module 10 | ○ |
| 1.19 | Reading Excel file using PROC IMPORT | Module 10 | ○ |
| 1.20 | Describing a dataset and library | Module 6 | ○ |
| 1.21 | Creating a new dataset from an existing dataset | Module 5 | ○ |
| 1.22 | Copying datasets from one library to another | Module 6 | ○ |

**Session 2 — DATA Step Fundamentals**

| # | Syllabus item | Taught in | Status |
| --- | --- | --- | --- |
| 2.1 | SET statement | Module 5 | ○ |
| 2.2 | SAS Programming Steps (same as 1.16) | Module 3 | ○ |
| 2.3 | KEEP as a statement and option | Module 13 | ○ |
| 2.4 | DROP as a statement and option | Module 13 | ○ |
| 2.5 | RENAME as a statement and option | Module 13 | ○ |
| 2.6 | WHERE as a statement and option | Module 14 | ○ |
| 2.7 | WHERE statement with operators and operands | Module 14 | ○ |
| 2.8 | Sorting datasets | Module 18 | ○ |
| 2.9 | Removing duplicates using PROC SORT | Module 18 | ○ |
| 2.10 | List Report | Module 40 | ○ |
| 2.11 | ODS | Module 40 | ○ |
| 2.12 | IF THEN statement | Module 15 | ○ |
| 2.13 | IF THEN DO statement | Module 15 | ○ |
| 2.14 | Creating multiple datasets from an existing dataset | Module 17 | ○ |
| 2.15 | SAS FORMAT | Module 19 | ○ |
| 2.16 | Creating user-defined SAS formats | Module 19 | ○ |
| 2.17 | Storing and using SAS formats in a permanent library | Module 19 | ○ |
| 2.18 | Difference between IF and WHERE | Module 16 | ○ |

**Session 3 — Data Import, Export, Input, Output and PDV**

| # | Syllabus item | Taught in | Status |
| --- | --- | --- | --- |
| 3.1 | Reading and writing Excel files | Module 10 | ○ |
| 3.2 | Reading and writing Excel files with multiple sheets | Module 10 | ○ |
| 3.3 | Reading and writing TXT files | Module 8 | ○ |
| 3.4 | Reading and writing CSV files | Module 10 | ○ |
| 3.5 | Reading and writing Access databases | Module 11 | ○ |
| 3.6 | Reading from database servers such as SQL Server | Module 11 | ○ |
| 3.7 | Reading from Oracle database | Module 11 | ○ |
| 3.8 | PROC DOWNLOAD | Module 12 | ○ |
| 3.9 | PROC UPLOAD | Module 12 | ○ |
| 3.10 | HDFS connection | Module 12 | ○ |
| 3.11 | Reading/writing TXT delimited files | Module 8 | ○ |
| 3.12 | @ vs @@ while reading data | Module 9 | ○ |
| 3.13 | Reading unstructured data into structured datasets | Module 9 | ○ |
| 3.14 | PDV and PDV by example | Module 7 | ○ |
| 3.15 | Selecting random observations | Module 20 | ○ |
| 3.16 | Reading data from one dataset to another while selecting observations | Module 20 | ○ |

**Session 4 — SAS Functions and PROC SQL**

| # | Syllabus item | Taught in | Status |
| --- | --- | --- | --- |
| 4.1 | Character functions | Module 21 | ○ |
| 4.2 | Numeric functions | Module 22 | ○ |
| 4.3 | Datetime functions | Module 23 | ○ |
| 4.4 | SAS functions with examples | Module 24 | ○ |
| 4.5 | SAS SQL Programming | Module 25 | ○ |
| 4.6 | Creating a table using PROC SQL | Module 25 | ○ |
| 4.7 | Inserting values using PROC SQL | Module 25 | ○ |
| 4.8 | Adding columns using PROC SQL | Module 26 | ○ |
| 4.9 | Dropping columns using PROC SQL | Module 26 | ○ |
| 4.10 | Renaming columns using PROC SQL | Module 26 | ○ |
| 4.11 | Dropping tables | Module 26 | ○ |
| 4.12 | Deleting tables | Module 26 | ○ |
| 4.13 | Truncating tables | Module 26 | ○ |
| 4.14 | Creating a new table from an existing table | Module 25 | ○ |
| 4.15 | Creating a new table by limiting records | Module 25 | ○ |
| 4.16 | Sorting and summarizing a table | Module 29 | ○ |
| 4.17 | WHERE vs HAVING | Module 29 | ○ |
| 4.18 | CASE WHEN | Module 28 | ○ |
| 4.19 | Transposing a table | Module 36 | ○ |
| 4.20 | Joining tables vertically and horizontally | Module 31 | ○ |
| 4.21 | Creating calculated columns | Module 27 | ○ |
| 4.22 | COALESCE | Module 30 | ○ |
| 4.23 | SAS SQL functions | Module 30 | ○ |
| 4.24 | SAS SQL Views | Module 32 | ○ |
| 4.25 | SAS SQL Stored Procedures | Module 32 | ○ |

**Session 5 — Advanced DATA Step**

| # | Syllabus item | Taught in | Status |
| --- | --- | --- | --- |
| 5.1 | Transposing datasets from rows to columns and columns to rows | Module 36 | ○ |
| 5.2 | Transpose examples and challenges | Module 36 | ○ |
| 5.3 | RETAIN statement | Module 34 | ○ |
| 5.4 | Difference between SUM and addition | Module 22 | ○ |
| 5.5 | SAS COMPARE procedure | Module 39 | ○ |
| 5.6 | SAS UPDATE statement | Module 39 | ○ |
| 5.7 | FIRST. and LAST. | Module 34 | ○ |
| 5.8 | PROC RANK | Module 35 | ○ |
| 5.9 | FIRST./LAST. vs PROC RANK | Module 35 | ○ |
| 5.10 | Creating row numbers | Module 20 | ○ |
| 5.11 | Selecting random observations (same as 3.15) | Module 20 | ○ |
| 5.12 | Selecting every alternate observation | Module 20 | ○ |
| 5.13 | SAS loops | Module 37 | ○ |
| 5.14 | Loop examples | Module 37 | ○ |
| 5.15 | SAS arrays | Module 38 | ○ |
| 5.16 | Array examples | Module 38 | ○ |

**Session 6 — Reporting, Summary Statistics and Visualization**

| # | Syllabus item | Taught in | Status |
| --- | --- | --- | --- |
| 6.1 | Character functions (same as 4.1) | Module 21 | ○ |
| 6.2 | Numeric functions (same as 4.2) | Module 22 | ○ |
| 6.3 | Datetime functions (same as 4.3) | Module 23 | ○ |
| 6.4 | Summary reports | Module 41 | ○ |
| 6.5 | PROC MEANS | Module 41 | ○ |
| 6.6 | PROC SUMMARY | Module 41 | ○ |
| 6.7 | PROC UNIVARIATE | Module 42 | ○ |
| 6.8 | PROC FREQ | Module 43 | ○ |
| 6.9 | PROC REPORT | Module 44 | ○ |
| 6.10 | PROC TABULATE | Module 45 | ○ |
| 6.11 | SAS Charts | Module 46 | ○ |

**Session 7 — Advanced SAS SQL**

| # | Syllabus item | Taught in | Status |
| --- | --- | --- | --- |
| 7.1 | Creating tables using PROC SQL (same as 4.6) | Module 25 | ○ |
| 7.2 | Inserting values using PROC SQL (same as 4.7) | Module 25 | ○ |
| 7.3 | Creating a new table from an existing table (same as 4.14) | Module 25 | ○ |
| 7.4 | Selecting observations | Module 27 | ○ |
| 7.5 | Adding row numbers | Module 30 | ○ |
| 7.6 | Creating row numbers (same as 7.5) | Module 30 | ○ |
| 7.7 | Table aliases and column aliases | Module 27 | ○ |
| 7.8 | Expressions | Module 27 | ○ |
| 7.9 | WHERE clause with operators and operands | Module 27 | ○ |
| 7.10 | CASE WHEN (same as 4.18) | Module 28 | ○ |
| 7.11 | Nested CASE WHEN | Module 28 | ○ |
| 7.12 | Summarizing data (same as 4.16) | Module 29 | ○ |
| 7.13 | WHERE vs HAVING (same as 4.17) | Module 29 | ○ |
| 7.14 | Sequence of SQL clauses | Module 29 | ○ |
| 7.15 | UPDATE statement | Module 26 | ○ |
| 7.16 | DELETE statement | Module 26 | ○ |
| 7.17 | Appending tables | Module 31 | ○ |
| 7.18 | Merging tables | Modules 31 and 33 | ○ |
| 7.19 | Calculated fields (same as 4.21) | Module 27 | ○ |
| 7.20 | COALESCE (same as 4.22) | Module 30 | ○ |
| 7.21 | Character, numeric and datetime functions | Module 30 | ○ |
| 7.22 | SAS SQL functions with examples | Module 30 | ○ |
| 7.23 | SAS SQL Views (same as 4.24) | Module 32 | ○ |
| 7.24 | SAS SQL Stored Procedures (same as 4.25) | Module 32 | ○ |

**Session 8 — SAS Macros and Automation**

| # | Syllabus item | Taught in | Status |
| --- | --- | --- | --- |
| 8.1 | SAS automation program with an example | Module 47 | ○ |
| 8.2 | How a SAS macro program starts and ends | Module 47 | ○ |
| 8.3 | Defining SAS macro variables | Module 48 | ○ |
| 8.4 | Macro variables and practical uses | Module 48 | ○ |
| 8.5 | %LET and practical uses | Module 48 | ○ |
| 8.6 | Positional and keyword parameters | Module 49 | ○ |
| 8.7 | %GLOBAL macro variables | Module 48 | ○ |
| 8.8 | %LOCAL macro variables | Module 48 | ○ |
| 8.9 | PROC SQL INTO clause for creating macro variables | Module 50 | ○ |
| 8.10 | %DO loop for creating macro variables | Module 50 | ○ |
| 8.11 | CALL SYMPUT | Module 50 | ○ |
| 8.12 | SAS macro debugging options | Module 53 | ○ |
| 8.13 | Storing SAS macros in a permanent library | Module 54 | ○ |
| 8.14 | %INCLUDE | Module 54 | ○ |
| 8.15 | Viewing all defined macro variables | Module 48 | ○ |
| 8.16 | Conditional macro execution using %IF %THEN | Module 51 | ○ |
| 8.17 | SAS macro scheduling | Module 55 | ○ |
| 8.18 | SAS macro functions | Module 52 | ○ |
| 8.19 | SAS macro industry examples | Module 55 | ○ |

**Coverage check:** Session 1: 22 items · Session 2: 18 · Session 3: 16 · Session 4: 25 · Session 5:
16 · Session 6: 11 · Session 7: 24 · Session 8: 19 · **Total: 151 items, all covered.**

The deep-dive sections asked for in your prompt are covered too: the macro master section (Modules
47–55), functions master reference (Part X), reporting master (Part X), DATA step master (Part X),
SQL master (Part X), data quality (Module 58), production SAS (Module 59), SAS environments (Module
1), modern SAS versions (Module 1), naming rules (Module 4), the date/time model (Module 23), file
input (Modules 8–9), transpose (Module 36), merge/join (Modules 31 and 33), RETAIN/FIRST./LAST.
(Module 34), arrays and loops (Modules 37–38) and automation (Modules 47 and 55).

## 0.8 Beginner → Advanced Progression

| Level | Modules | You will be able to |
| --- | --- | --- |
| Beginner | 1–12 | Run SAS, create and read datasets, load files and database tables, and explain the PDV |
| Intermediate | 13–32 | Filter, sort, format, clean and summarise data; write any PROC SQL query a SQL Server analyst would |
| Advanced | 33–46 | Do BY-group processing, running totals, ranking, transposing, arrays and professional reports |
| Industry | 47–59 | Build parameterised macros, schedule jobs, debug logs, tune performance and validate data |
| Interview | Parts X–XII | Answer conceptual, coding, debugging and scenario questions with confidence |

## 0.9 Interview Preparation Roadmap

| Week | Focus | Practice |
| --- | --- | --- |
| 1–2 | PDV, DATA vs PROC step, libraries, INPUT styles, @ vs @@ | Explain the PDV out loud using a 3-row example |
| 3–4 | WHERE vs IF, KEEP/DROP/RENAME order, PROC SORT NODUPKEY, formats | Predict the output of small programs before running them |
| 5–6 | PROC SQL: joins, WHERE vs HAVING, CALCULATED, CASE, remerging | Rewrite 20 SQL Server queries as PROC SQL |
| 6–7 | MERGE vs JOIN, RETAIN, FIRST./LAST., TRANSPOSE, arrays | Solve the classic "running total by customer" and "latest record" problems |
| 8 | PROC MEANS vs SUMMARY, FREQ, REPORT, TABULATE | Build one monthly branch report end to end |
| 9–10 | Macros: scope, CALL SYMPUT timing, INTO, quoting, debugging | Explain why a CALL SYMPUT value is not available in the same step |
| 11–12 | Debugging, performance, data quality, production, capstone | Mock interviews using Part XI |

## 0.10 Industry Project Roadmap

| After | Project | What it proves |
| --- | --- | --- |
| Part III | **Mini Project 1** — Customer and transaction data intake | You can load, check, clean and de-duplicate real files |
| Part V | **Mini Project 2** — Branch performance analysis with PROC SQL | You can answer business questions with joins and summaries |
| Part VI | **Mini Project 3** — Bank transaction fraud analysis | You can apply BY-group logic and fraud rules at scale |
| Part VIII | **Mini Project 4** — Automated monthly risk report | You can turn a manual report into a scheduled macro job |
| Part XII | **Capstone** — End-to-end fraud analytics system | One resume-ready project covering the whole course |

## 0.11 Final Estimated Skill Progression

These are typical outcomes if you complete the modules and their exercises. Your own pace may be
faster because you already know SQL and Pandas well.

| Skill area | Start | After Part V | After Part VIII | After the capstone |
| --- | --- | --- | --- | --- |
| DATA step | New | Comfortable | Strong | Strong, production-ready |
| PROC SQL | Strong SQL, new to SAS SQL | Strong | Strong | Strong, with tuning |
| Reporting | New | Basic | Strong | Strong |
| Macros | New | New | Comfortable | Strong |
| Debugging and performance | New | Basic | Comfortable | Strong |
| Interview readiness | Low | Entry-level SAS analyst | Mid-level SAS analyst | Mid-level SAS developer |

---

# The SQL ↔ SAS ↔ Python/Pandas Concept Map

You already know SQL Server and Pandas. This map is your bridge into SAS.

## Your Session 1 Mapping

| # | SQL | SAS | Python / Pandas |
| --- | --- | --- | --- |
| 1 | DATABASE | LIBRARY | Database / Folder / Collection |
| 2 | TABLE | DATASET | DataFrame |
| 3 | COLUMNS or FIELDS | VARIABLES | Columns |
| 4 | ROWS or RECORDS | OBSERVATIONS | Rows / Records |
| 5 | Filter — `WHERE` | `WHERE` | `df[df["age"] > 30]` |
| 6 | Sort — `ORDER BY` | `PROC SORT` | `df.sort_values(by=['Col1','Col2'], ascending=[False, True])` |
| 7 | `GROUP BY` | `PROC SQL` / `PROC SUMMARY` | `df.groupby('Col1', as_index=False)` |
| 8 | `JOIN` | `PROC SQL` / `MERGE` | `df.merge()` or `df.join()` or `df.concat()` |

📌 Two small corrections to keep in mind for row 8. In Pandas the function is written `pd.concat()`,
not `df.concat()`. And it stacks tables (like SQL `UNION ALL`), so it is not a join. In SAS, stacking
is done with `SET a b;` or SQL `UNION ALL`. Joining is done with `MERGE` or SQL `JOIN`.

## The Growing Mental Map

This list grows as you go through the course. Each pair is explained in its own module.

| SAS | SQL Server | Pandas | Module |
| --- | --- | --- | --- |
| LIBRARY | Database / schema | Folder of files | 4 |
| DATASET | Table | DataFrame | 4 |
| OBSERVATION | Row | Row | 4 |
| VARIABLE | Column | Column | 4 |
| `SET` | Reading a table; `UNION ALL` when listing several | Reading a DataFrame; `pd.concat` when stacking | 5 |
| PDV | No real equivalent (SQL works on whole sets) | No real equivalent (Pandas works on whole columns) | 7 |
| `WHERE` | `WHERE` | Boolean filtering | 14 |
| `PROC SORT` | `ORDER BY` | `sort_values()` | 18 |
| `PROC SORT NODUPKEY` | `ROW_NUMBER() ... = 1` | `drop_duplicates()` | 18 |
| `FORMAT` | `FORMAT()`, `CONVERT()` (display only) | `.map()`, `.dt.strftime()` | 19 |
| `PROC SQL` | SQL | `pandasql`, `duckdb` (or the Pandas methods) | 25 |
| `MERGE` | `JOIN` | `merge()` | 33 |
| `PROC SUMMARY` | `GROUP BY` with aggregates | `groupby().agg()` | 41 |
| `PROC TRANSPOSE` | `PIVOT` / `UNPIVOT` | `pivot()` / `melt()` | 36 |
| `RETAIN` | Running totals with window functions | `cumsum()`, `shift()` | 34 |
| `FIRST.` / `LAST.` | `ROW_NUMBER()`, `LEAD`, `LAG` | `groupby().cumcount()`, `head(1)`, `tail(1)` | 34 |
| `PROC RANK` | `RANK()`, `DENSE_RANK()`, `NTILE()` | `rank()`, `qcut()` | 35 |
| `ARRAY` | No direct equivalent | Working on many columns at once | 38 |
| `MACRO` | Dynamic SQL / stored procedures | Python functions and f-strings | 47 |

⚠️ Do not force a comparison when the ideas are different. The biggest difference: **SQL and Pandas
work on the whole table at once. The SAS DATA step works on one row at a time, in a loop.** This is
why SAS has tools like RETAIN and FIRST./LAST. that SQL and Pandas do not need in the same form.

---

# Part I — Getting Started with SAS (Modules 1–7)

## MODULE 1 — What SAS Is: Products, Components and Environments

**Syllabus items:** 1.1 What is SAS? · 1.2 SAS Components · 1.3 Introduction to SAS PC · 1.4
Introduction to SAS University Studio · 1.5 Introduction to SAS Enterprise Guide

**You will learn:** what SAS is, what its main parts do, and the different screens you can use to run
it. **Why it matters:** interviewers often start with "What is SAS?" and "Which SAS tools have you
used?". A clear answer sets a good tone. **Before you start:** nothing.

### 🧠 What it is

SAS is software for working with data. You use it to read data, clean it, join it, analyse it and
report on it. SAS is also the name of the programming language you write to do this.

SAS began in the late 1960s as a university project for analysing farm research data. The company,
SAS Institute, was founded in 1976. The name first stood for "Statistical Analysis System". Today it
is simply "SAS".

**Formal definition:** SAS is an integrated software suite for data management, advanced analytics,
business intelligence and reporting, built around the SAS programming language.

**Why banks and insurers use SAS**

- **Trust and history.** Many risk and fraud systems were built in SAS over 20–30 years. That code
  still runs every day.
- **Regulation.** Banks must show regulators how a number was produced. SAS is validated, stable and
  has detailed logs. Credit-risk models (for example Basel and IFRS 9 models) are often built in SAS.
- **Large data on disk.** Pandas holds data in memory. SAS reads data from disk one row at a time, so
  it can process files much bigger than the computer's memory.
- **Support.** Companies pay for SAS and get vendor support, which risk teams value.

### SAS components

SAS is sold as a family of products. Each one adds a capability.

| Component | What it does | Typical user |
| --- | --- | --- |
| **Base SAS** | The core: DATA step, PROC SQL, macro language, basic procedures (SORT, PRINT, MEANS, FREQ, REPORT), ODS | Every SAS user |
| **SAS/STAT** | Statistics: regression, logistic regression, sampling (PROC REG, PROC LOGISTIC, PROC SURVEYSELECT) | Statisticians, model builders |
| **SAS/GRAPH** | Older-style charts and maps (PROC GCHART, PROC GPLOT) | Report writers on older systems |
| **SAS/ACCESS** | Connects SAS to databases and files: Oracle, SQL Server, Teradata, Hadoop, ODBC, Excel, Access | Anyone pulling data from a database |
| **SAS/CONNECT** | Runs code on a remote SAS server and moves data between machines (PROC UPLOAD, PROC DOWNLOAD) | Analysts working with central servers |
| **SAS/ETS** | Time series and forecasting | Economists, forecasting teams |
| **SAS Enterprise Guide** | A Windows program for writing code and building point-and-click projects | Most bank analysts |
| **SAS Studio** | A web-browser screen for writing and running SAS code | Learners, Viya users |
| **SAS Enterprise Miner** | Drag-and-drop predictive modelling | Data scientists on SAS 9 |
| **SAS Visual Analytics** | Dashboards and interactive reports | Business users, BI teams |
| **SAS Viya** | The modern cloud platform with an in-memory engine called CAS | Companies modernising their SAS estate |
| **SAS Data Integration Studio** | Builds ETL jobs as visual flows | ETL developers |
| **SAS Management Console** | Manages servers, users, libraries and schedules | SAS administrators |

### Do not mix up these four ideas

Interviewers like to check that you can tell these apart.

| Idea | What it means | Examples |
| --- | --- | --- |
| **Language** | The code you write | DATA step, PROC SQL, macro language |
| **Product** | Something SAS sells and licenses | Base SAS, SAS/STAT, SAS/ACCESS |
| **Execution environment** | Where the code actually runs | Your PC, a SAS 9.4 server, SAS Viya compute server, CAS |
| **Interface** | The screen you type into | SAS for Windows, Enterprise Guide, SAS Studio |

📌 Example of getting it right: "I write SAS code (language) in Enterprise Guide (interface). The code
runs on our SAS 9.4 server (environment). We license Base SAS and SAS/ACCESS to Oracle (products)."

### Introduction to SAS PC (1.3)

"SAS PC" means SAS installed on a Windows computer and used through its own windows. This screen is
also called the **SAS windowing environment** or **Display Manager**. You type code in an editor,
press a key to run it, and read the results in other windows. Module 2 covers each window.

- **Good for:** learning, small jobs, quick checks.
- **Limits:** it runs on one PC, so it is limited by that PC's power. Most banks now use a central
  server through Enterprise Guide or SAS Studio instead.

### Introduction to SAS University Studio (1.4)

**SAS University Edition** was a free version of SAS for learning. It ran inside a virtual machine
on your computer, and you used it through **SAS Studio** in your web browser.

⚠️ SAS University Edition has been **retired**. The free option today is **SAS OnDemand for
Academics**. It gives you SAS Studio in the browser, with SAS running on SAS's own cloud servers.
Nothing needs to be installed. The code you write there is the same SAS code used at work.

**SAS Studio** itself is very much alive. It is the browser interface used with SAS 9.4 servers and
with SAS Viya.

### Introduction to SAS Enterprise Guide (1.5)

**SAS Enterprise Guide (EG)** is a Windows program that connects to a SAS server. In most banks this
is the screen you will use every day.

- **Projects:** you keep programs, datasets and reports together in one project file (`.egp`).
- **Process flows:** you can see how steps link together, like a flowchart.
- **Tasks:** point-and-click tools write SAS code for you (for example a summary table).
- **Code:** you can write your own programs, just like in SAS PC.
- **Servers:** your code usually runs on a powerful server, not on your laptop.

### SAS 9.4, SAS Viya and modern SAS

| Platform | What it is | Why it matters to you |
| --- | --- | --- |
| **SAS 9.4** | The classic SAS platform, first released in 2013 and still updated | Most bank SAS code runs here today |
| **SAS Viya** | The cloud platform. Adds CAS, an in-memory engine that splits work across many machines | Banks are moving towards it. Your Base SAS skills still apply. |
| **CAS** | Cloud Analytic Services, the Viya engine | Uses CAS actions and in-memory tables. Some SAS 9 habits change. |

📌 The DATA step, PROC SQL and macros you learn here work in both SAS 9.4 and SAS Viya.

### Environments compared

| Environment | Interface | Typical users | Strengths | Limits | Relevance today |
| --- | --- | --- | --- | --- | --- |
| SAS PC (Windows) | Desktop windows | Learners, small teams | Simple, everything local | Limited to one PC | Still used, but less in banks |
| SAS University Edition | SAS Studio in a virtual machine | Learners | Was free | Retired | Replaced by SAS OnDemand for Academics |
| SAS Enterprise Guide | Windows client | Bank analysts, developers | Projects, flows, tasks, server power | Windows only | Very common in banks |
| SAS Studio | Web browser | Learners, Viya users | Nothing to install | Fewer project features than EG | Growing; standard in Viya |
| SAS Viya | SAS Studio and web apps | Modern analytics teams | Scales out, cloud, Python and R integration | Cost, migration effort | The direction SAS is heading |
| SAS Enterprise Miner | Drag-and-drop | Modellers | Fast model building | Older, SAS 9 only | Being replaced by Viya tools |
| SAS Visual Analytics | Web dashboards | Business users | Interactive reports | Not for data preparation | Common for SAS dashboards |

### 💼 Banking scenario

A credit-card fraud team receives 10 million transactions every day. A SAS job on the bank's server
reads them from Oracle using **SAS/ACCESS**. A DATA step in **Base SAS** applies fraud rules. **PROC
REPORT** builds the daily summary. Analysts look at results in **Enterprise Guide**, and managers see
a dashboard in **SAS Visual Analytics**. One business process uses five SAS components.

### ⚠️ Common mistakes

- Saying "SAS is a database". It is not. SAS stores data in files called SAS datasets, but it is an
  analytics tool, not a database server.
- Saying "Enterprise Guide is a different language". It is an interface. The code is the same SAS.
- Saying you used "SAS University Edition" as if it is current. Say SAS OnDemand for Academics or SAS
  Studio.

### Exercises

1. **Level 1 — Beginner:** List three SAS products and what each one does.
2. **Level 2 — Intermediate:** Explain the difference between SAS Studio and SAS Enterprise Guide.
3. **Level 3 — Advanced:** Explain why a bank might keep SAS 9.4 even after buying SAS Viya.
4. **Level 4 — Interview:** Answer "What is SAS and why do banks use it?" in under one minute.
5. **Level 5 — Real world:** Draw how a daily fraud report could flow through four SAS components.

### ⭐ Interview questions

**Q1. What is SAS?**
- *What they are testing:* whether you understand SAS beyond "a tool".
- *Strong answer:* "SAS is an analytics software suite and a programming language. I use Base SAS for
  the DATA step, PROC SQL and macros to prepare and analyse data, and procedures like PROC MEANS and
  PROC REPORT for reporting. In banking it is valued for reliability, audit trails and handling large
  data on disk."
- *Weak answer:* "It is a statistics tool."
- *Follow-up:* "What is the difference between Base SAS and SAS/ACCESS?"

**Q2. What is the difference between SAS Enterprise Guide and Base SAS?**
- *Strong answer:* "Base SAS is the product that contains the language and core procedures. Enterprise
  Guide is a Windows interface that sends that code to a SAS server and organises work into projects."

**Q3. What is SAS Viya?**
- *Strong answer:* "SAS Viya is SAS's cloud platform. It adds CAS, an in-memory engine that spreads
  work over many machines. Standard SAS code still runs on its compute server."

### Module wrap-up

- **I now know:** what SAS is, its main products, and the difference between language, product,
  environment and interface.
- **I can now:** describe the SAS tools used in a bank and choose the right one for a job.
- **Next:** Module 2 — the SAS PC windows and shortcut keys.

---

## MODULE 2 — The SAS PC Windows and Shortcut Keys

**Syllabus items:** 1.10 SAS PC Windows and its functionality · 1.11 SAS Shortcut Keys

**You will learn:** what each SAS window is for and the keys that save you time. **Why it matters:**
you will use these windows every few seconds. **Before you start:** Module 1.

### The main windows

```text
+-----------------------------------+-----------------------------------+
| EXPLORER                          | ENHANCED EDITOR                   |
|  Libraries                        |  data work.txn;                   |
|   - Work                          |     set bank.transactions;        |
|   - Sashelp                       |  run;                             |
|   - Bank                          |                                   |
|-----------------------------------+-----------------------------------|
| RESULTS                           | LOG                               |
|  - Print: WORK.TXN                |  NOTE: The data set WORK.TXN has  |
|  - Means: Summary statistics      |        6 observations and 5 ...   |
+-----------------------------------+-----------------------------------+
                         RESULTS VIEWER (HTML report)
```

| Window | What it is for | Tip |
| --- | --- | --- |
| **Enhanced Editor** | Where you write and run code. Colours keywords so mistakes are easy to spot. | Save programs as `.sas` files |
| **Program Editor** | The older editor. Clears your code when you run it. | Prefer the Enhanced Editor |
| **Log** | SAS writes what happened: NOTE, WARNING and ERROR messages, row counts, timings | 📌 Read it after **every** run |
| **Output** | Plain-text results (the LISTING destination) | Mostly replaced by the Results Viewer |
| **Results Viewer** | Shows procedure output as an HTML report | The default output since SAS 9.3 |
| **Results** | A tree of every output you produced in this session | Click to jump back to old output |
| **Explorer** | Browse libraries and datasets. Double-click a dataset to open it. | ⚠️ Close opened datasets, or other programs cannot change them |

**The normal workflow**

```text
Write code (Editor) -> Run (F3 / F8) -> Read the LOG -> Check results (Results Viewer)
        ^                                    |
        +---------- fix any problem ---------+
```

### Shortcut keys

These are common defaults in SAS 9.4 for Windows. **Keys can differ by version and by your settings.**
To see your real key list, press **F9** or type `KEYS` in the command bar.

| Key | What it does |
| --- | --- |
| **F3** or **F8** | Run (submit) the code. If text is selected, only that text runs. |
| **F4** | Bring back the last code you ran (in the Program Editor) |
| **F5** | Go to the Program Editor |
| **F6** | Go to the Log |
| **F7** | Go to the Output window |
| **F9** | Open the KEYS window (see and change key settings) |
| **Ctrl + /** | Comment out the selected lines |
| **Ctrl + Shift + /** | Remove comments from the selected lines |
| **Ctrl + Shift + U** | Change selected text to UPPERCASE |
| **Ctrl + Shift + L** | Change selected text to lowercase |
| **Ctrl + F** / **Ctrl + H** | Find / find and replace |
| **Ctrl + G** | Go to a line number |
| **Ctrl + Break** | Interrupt a running program |

**In SAS Studio and Enterprise Guide**, use the Run button or the keys shown in that tool's menu. In
SAS Studio, **F3** runs the code.

**A useful command:** this line clears the Log and Output windows before a fresh run.

```sas
dm "log; clear; output; clear;";
```

⚠️ `dm` statements work only in SAS for Windows (Display Manager). They do nothing useful in SAS
Studio or batch jobs.

### ⚠️ Common mistakes

- Not reading the Log. A program can "finish" and still be wrong. The Log is where SAS tells you.
- Leaving a dataset open in the Explorer viewer. Your next program then fails with
  `ERROR: A lock is not available for ...`.
- Using the old Program Editor, which clears your code each time you run it.

### Exercises

1. **Level 1:** Open SAS, run `proc print data=sashelp.class; run;` and find the output in three
   different windows.
2. **Level 2:** Comment out three lines with a shortcut, then remove the comments.
3. **Level 3:** Find your own key settings with F9 and write down any that differ from the table.
4. **Level 4 — Interview:** "Where do you look first when a program does not give the expected result?"
5. **Level 5:** Open a dataset in the viewer, try to overwrite it from code, and read the error.

### ⭐ Interview questions

**Q. Which window is most important and why?**
- *Strong answer:* "The Log. It tells me whether the program ran correctly: errors, warnings,
  uninitialized variables, type conversions and row counts. Output can look fine while the Log shows
  a problem."

### Module wrap-up

- **I now know:** the purpose of each SAS window and the main shortcut keys.
- **I can now:** write, run and check a program efficiently.
- **Next:** Module 3 — how a SAS program is built.

---

## MODULE 3 — How a SAS Program Is Built: Steps, Statements and Jargon

**Syllabus items:** 1.6 SAS Programming · 1.7 SAS Jargons · 1.9 Explain SAS Programming · 1.16 SAS
Programming Steps · 2.2 SAS Programming Steps (same topic)

**You will learn:** the building blocks of every SAS program, the words SAS people use, and how to
read the Log. **Why it matters:** everything else is built from these pieces. **Before you start:**
Module 2.

### 🧠 What it is

A SAS program is a list of **statements**. Each statement ends with a **semicolon** (`;`).

Statements are grouped into **steps**. There are only two kinds of step:

| Step | Starts with | Ends with | What it does |
| --- | --- | --- | --- |
| **DATA step** | `DATA` | `RUN;` | Creates or changes datasets. Reads files, cleans, calculates, filters. |
| **PROC step** | `PROC` | `RUN;` or `QUIT;` | Uses a dataset: sorts, prints, summarises, reports, runs SQL. |

Some statements live outside steps. They are called **global statements**. They take effect as soon
as SAS reads them.

| Global statement | What it does |
| --- | --- |
| `LIBNAME` | Points a short name at a folder or database |
| `FILENAME` | Points a short name at a file |
| `OPTIONS` | Changes system settings |
| `TITLE` / `FOOTNOTE` | Sets report titles and footnotes |
| `%LET` | Creates a macro variable |

📌 **RUN or QUIT?** Most procedures end with `RUN;`. A few stay open until `QUIT;`, because you can
send them several commands: `PROC SQL`, `PROC DATASETS`, and charting procedures such as `PROC
GPLOT`. If you forget `QUIT;`, the procedure keeps running and the Log says "PROC SQL is still
running".

### Your first complete program, explained (1.9)

```sas
/* Program: first_look.sas  - summarise a small loan file */
options nodate nonumber;                 /* global statement */
title "Loan Balances by Product";         /* global statement */

data work.loans;                          /* DATA step starts */
    input loan_id $ product $ balance;
    datalines;
L001 HOME 2500000
L002 AUTO 450000
L003 HOME 1800000
L004 PERSONAL 300000
;
run;                                      /* DATA step ends */

proc means data=work.loans n sum mean;    /* PROC step starts */
    class product;
    var balance;
run;                                      /* PROC step ends */
```

**Line by line**

| Code | What it does |
| --- | --- |
| `/* ... */` | A comment. SAS ignores it. |
| `options nodate nonumber;` | Global: do not print the date and page number on output |
| `title "...";` | Global: sets the title for all following output until changed |
| `data work.loans;` | Start a DATA step that will create a dataset called `loans` in the `WORK` library |
| `input loan_id $ product $ balance;` | Read three values from each line. `$` means "this is text". |
| `datalines;` | The data lines start on the next line |
| `;` (alone on a line) | The data lines end |
| `run;` | Run the DATA step |
| `proc means data=work.loans n sum mean;` | Start PROC MEANS on `work.loans`. Show count, sum and mean. |
| `class product;` | Give separate results for each product |
| `var balance;` | Calculate the statistics for `balance` |
| `run;` | Run the PROC step |

⚠️ `PERSONAL` has 8 characters. With this kind of input, text is cut to 8 characters by default, so
it just fits. A longer value would be cut off silently. Module 5 shows how to fix this with `LENGTH`.

**Expected output (Results Viewer)**

```text
                     Loan Balances by Product

                        The MEANS Procedure
                     Analysis Variable : balance

   product      N Obs     N             Sum            Mean
   ---------------------------------------------------------
   AUTO             1     1          450000          450000
   HOME             2     2         4300000         2150000
   PERSONAL         1     1          300000          300000
```

**Expected Log (simplified)**

```text
NOTE: The data set WORK.LOANS has 4 observations and 3 variables.
NOTE: DATA statement used (Total process time): real time 0.01 seconds
NOTE: There were 4 observations read from the data set WORK.LOANS.
NOTE: PROCEDURE MEANS used (Total process time): real time 0.03 seconds
```

### Rules of SAS syntax

- **Every statement ends with `;`.** A missing semicolon is the most common beginner error.
- **Free format.** Statements can span lines, and you can put several on one line. Spacing does not
  matter.
- **Not case-sensitive.** `DATA`, `data` and `Data` are the same. Variable names keep the case you
  first gave them for display, but `Balance` and `balance` are the same variable.
- **Comments:** `/* like this */` anywhere, or `* like this;` as a whole statement.
- **Text in quotes** is case-sensitive: `'HOME'` is not equal to `'home'`.

### The Log: NOTE, WARNING, ERROR

| Message type | Colour in SAS PC | Meaning | What to do |
| --- | --- | --- | --- |
| `NOTE:` | Blue | Information: rows read, rows written, time taken | Read them. Some NOTEs signal real problems (see below). |
| `WARNING:` | Green | SAS continued, but something may be wrong | Always investigate |
| `ERROR:` | Red | SAS could not run the step (or part of it) | Fix before trusting any output |

⚠️ These NOTEs look harmless but usually mean a bug:

- `NOTE: Variable X is uninitialized.` (often a misspelt name)
- `NOTE: Character values have been converted to numeric values ...`
- `NOTE: Missing values were generated as a result of performing an operation on missing values.`
- `NOTE: Invalid data for ... in line ...`
- `NOTE: MERGE statement has more than one data set with repeats of BY values.`

Module 56 covers debugging in depth.

### SAS jargon (1.7)

| SAS word | Plain meaning | SQL Server | Pandas |
| --- | --- | --- | --- |
| Dataset (data set) | A table stored by SAS | Table | DataFrame |
| Observation | One row | Row | Row |
| Variable | One column | Column | Column |
| Library | A named place where datasets live | Database / schema | Folder |
| Libref | The short nickname of a library | Database name | Path variable |
| Member | Anything stored in a library (dataset, view, catalog) | Object | File |
| WORK library | Temporary library, emptied when SAS closes | `#temp` tables | Variables in memory |
| Raw data / external file | Data not yet in SAS format (TXT, CSV) | Flat file | CSV file |
| Fileref | Short nickname for an external file | — | File path variable |
| Step | A DATA step or a PROC step | A statement batch | A block of code |
| Procedure (PROC) | A ready-made tool | Built-in function / command | A library function |
| Informat | Instructions for **reading** a value | `CAST`/`CONVERT` on input | `pd.to_datetime(format=...)` |
| Format | Instructions for **displaying** a value | `FORMAT()` | `.dt.strftime()` |
| PDV | The one-row workspace the DATA step uses | — | — |
| Descriptor portion | The dataset's "header": names, types, lengths, row count | Table metadata | `df.info()` |
| Missing value | No value: `.` for numbers, blank for text | `NULL` | `NaN` / `None` |
| BY-group | Rows that share the same BY value | `PARTITION BY` group | `groupby` group |
| ODS | Output Delivery System: sends results to HTML, PDF, Excel | — | `to_html`, `to_excel` |
| Log | SAS's diary of what happened | Messages tab | Console output |

### 🧠 How SAS processes a program

SAS reads your program one statement at a time. When it reaches a step boundary (`RUN;`, `QUIT;`, or
the start of the next `DATA`/`PROC`), it runs that step. Each DATA step runs in two phases:

1. **Compilation:** SAS checks the syntax and builds a plan, including the PDV.
2. **Execution:** SAS runs the plan, usually once for every row.

Module 7 explains both phases in detail.

### SQL Server vs SAS: a different way of thinking

```sql
-- SQL Server: you say WHAT you want. The engine decides how.
SELECT loan_id, balance * 0.01 AS monthly_interest
FROM dbo.loans
WHERE product = 'HOME';
```

```sas
/* SAS DATA step: you describe what to do to EACH ROW, one at a time. */
data work.home_interest;
    set work.loans;
    where product = 'HOME';
    monthly_interest = balance * 0.01;
    keep loan_id monthly_interest;
run;
```

```sas
/* PROC SQL: SQL inside SAS. Close to what you already know. */
proc sql;
    create table work.home_interest as
    select loan_id, balance * 0.01 as monthly_interest
    from work.loans
    where product = 'HOME';
quit;
```

📌 SAS gives you both styles. The DATA step is best for row-by-row logic (running totals, comparing
with the previous row, reading raw files). PROC SQL is best for joins and summaries.

### Python / Pandas

```python
home_interest = (
    loans.loc[loans["product"] == "HOME", ["loan_id", "balance"]]
         .assign(monthly_interest=lambda d: d["balance"] * 0.01)
         .drop(columns="balance")
)
```

### ⚠️ Common mistakes

- **Missing semicolon.** `data work.a` followed by `set work.b;` makes SAS read `data work.a set
  work.b;`. You get confusing errors far from the real problem.
- **Unbalanced quotes.** A missing closing quote makes SAS treat the rest of your program as text.
  Nothing seems to run.
- **No `RUN;` at the end.** In SAS PC the last step may not run until you submit more code.
- **No `QUIT;` after PROC SQL.** The procedure stays open.

### Exercises

1. **Level 1:** Write a program with one DATA step and one PROC PRINT. Label each line with a comment.
2. **Level 2:** Remove one semicolon on purpose. Read the error and explain it.
3. **Level 3:** Write the same filter as a DATA step and as PROC SQL. Compare the Log of both.
4. **Level 4 — Interview:** Explain the difference between a DATA step and a PROC step.
5. **Level 5:** List five SAS jargon words and say them in SQL Server terms to a colleague.

### ⭐ Interview questions

**Q1. What are the two kinds of steps in SAS?**
- *What they are testing:* the basic model of SAS.
- *Strong answer:* "DATA steps create or change datasets, working row by row through the PDV. PROC
  steps run ready-made procedures on datasets, like SORT, MEANS, REPORT or SQL. Global statements such
  as LIBNAME, OPTIONS and TITLE sit outside steps."
- *Weak answer:* "DATA is for data and PROC is for procedures."
- *Follow-up:* "Which procedures end with QUIT instead of RUN, and why?"

**Q2. What do NOTE, WARNING and ERROR mean in the Log?**
- *Strong answer:* "NOTEs give information, but some NOTEs show bugs, like uninitialized variables or
  automatic type conversion. WARNINGs mean SAS carried on but something may be wrong. ERRORs mean SAS
  could not run the step. In production I treat all three seriously and scan logs automatically."

### Module wrap-up

- **I now know:** statements, DATA steps, PROC steps, global statements, RUN vs QUIT, and the main
  SAS jargon.
- **I can now:** write, run and read the Log of a small complete program.
- **Next:** Module 4 — libraries, datasets and variables.

---

## MODULE 4 — Libraries, Datasets and Variables: Names, Types and Values

**Syllabus items:** 1.13 SAS Library and Library naming criteria · 1.14 SAS Dataset and Variable naming
criteria · 1.15 SAS Variable types and values

**You will learn:** where SAS keeps data, how to name things, the only two data types in SAS, and how
missing values behave. **Why it matters:** naming errors and type errors are the most common beginner
problems, and missing values cause silent wrong answers. **Before you start:** Module 3.

### 🧠 Libraries

A **library** is a named place where SAS datasets are stored. Usually it is a folder on a disk, but it
can also be a database. You give the library a short nickname called a **libref** with the `LIBNAME`
statement.

```sas
libname bank "C:\sasdata\bank";        /* Windows path */
libname risk "/sasdata/risk/mart";     /* Linux/UNIX path on a server */
```

After this, `bank.customers` means the dataset file `customers` in the folder `C:\sasdata\bank`. On
disk it is stored as `customers.sas7bdat`.

| Library | Permanent? | What it holds |
| --- | --- | --- |
| **WORK** | No. Emptied when your SAS session ends. | Your temporary datasets |
| **SASHELP** | Yes, read-only | Sample datasets (`sashelp.class`, `sashelp.cars`) and system views |
| **SASUSER** | Yes | Your personal settings |
| **Your own librefs** (`bank`, `risk`) | Yes, as long as the folder exists | Your permanent datasets |

**One-level vs two-level names**

```sas
data loans;          /* one-level name  = WORK.LOANS (temporary) */
data bank.loans;     /* two-level name  = permanent, in the BANK library */
```

📌 A libref only lasts for your session. Next time you start SAS, run the `LIBNAME` statement again
(teams put them in a shared setup program called `autoexec.sas`).

```sas
libname bank list;    /* show where BANK points */
libname bank clear;   /* remove the libref (the files stay on disk) */
```

### Library naming rules (1.13)

| Rule | Detail |
| --- | --- |
| Length | 1 to **8** characters |
| First character | A letter or underscore |
| Other characters | Letters, digits and underscores only |
| Case | Not case-sensitive |
| Avoid | `WORK`, `SASHELP`, `SASUSER` and `LIBRARY` (SAS looks for formats in `LIBRARY` automatically) |

| Libref | Valid? | Why |
| --- | --- | --- |
| `bank` | ✓ | |
| `risk_26` | ✓ | |
| `_temp` | ✓ | Underscore start is allowed |
| `creditrisk` | ✗ | 10 characters, more than 8 |
| `2026data` | ✗ | Starts with a digit |
| `risk-mart` | ✗ | Hyphen not allowed |

### Dataset and variable naming rules (1.14)

These rules apply with the default setting `VALIDVARNAME=V7`.

| Rule | Detail |
| --- | --- |
| Length | 1 to **32** characters |
| First character | A letter or underscore |
| Other characters | Letters, digits and underscores only. No spaces or special characters. |
| Case | Not case-sensitive. Variables keep the case you first typed for display. |
| Avoid | Names SAS uses itself, such as `_N_`, `_ERROR_`, `_NULL_`, `_ALL_`, `_NUMERIC_`, `_CHARACTER_`, `_TEMPORARY_` |

| Name | Valid? | Why |
| --- | --- | --- |
| `txn_amount` | ✓ | |
| `Monthly_EMI_2026` | ✓ | |
| `_flag` | ✓ | |
| `1st_txn` | ✗ | Starts with a digit |
| `txn amount` | ✗ | Contains a space |
| `amount$` | ✗ | Contains `$` |
| `customer_lifetime_value_in_rupees_total` | ✗ | 39 characters, more than 32 |

**Names with spaces: VALIDVARNAME=ANY and name literals**

Excel files often have column headings with spaces, like `Total Sales`. With
`options validvarname=any;` SAS can keep such names. You then refer to them as **name literals**: the
name in quotes followed by `n`.

```sas
options validvarname=any;

data work.sales;
    set work.raw_excel;
    'Net Amount'n = 'Total Sales'n - 'Discount'n;
run;
```

⚠️ Enterprise Guide often uses `VALIDVARNAME=ANY` by default, while SAS for Windows uses `V7`. The
same import can give `Total_Sales` in one tool and `'Total Sales'n` in another. Check with
`proc options option=validvarname; run;`. Many teams set `options validvarname=v7;` at the top of
every program so names are always safe.

For **dataset** names with special characters, use `options validmemname=extend;` and name literals
such as `bank.'Loans 2026'n`. Most teams avoid this.

### Variable types and values (1.15)

SAS has only **two** data types.

| Type | Stores | Default length | Missing value | Notes |
| --- | --- | --- | --- | --- |
| **Numeric** | Numbers, dates, times, datetimes, flags | 8 bytes | `.` (a dot) | Stored as floating point. About 15–16 significant digits. |
| **Character** | Text | Set by first use (1 to 32,767 bytes) | A blank (`' '`) | Fixed length. Shorter values are padded with blanks. |

📌 There is **no separate date type**. A SAS date is a number: the count of days since 1 January 1960.
Module 23 covers this in depth.

📌 There is **no boolean type**. Use numeric 1 and 0. In SAS, any number that is not 0 and not missing
counts as "true".

⚠️ **Store long ID numbers as text.** A 16-digit card number is too long to store exactly as a
number. Keep card numbers, account numbers and anything with leading zeros (like `000123`) as
**character** variables.

### Missing values

| Type | How it looks | Sort position |
| --- | --- | --- |
| Numeric | `.` | **Lower than every number**, even negative numbers |
| Numeric special missing | `.A` to `.Z`, and `._` | Also low. Used to record *why* a value is missing. |
| Character | Blank | Before any other text |

⚠️ Because a missing number is smaller than every number, `if balance < 0` is **true** when `balance`
is missing. A missing balance would be flagged as "negative". Always write
`if not missing(balance) and balance < 0`.

| Situation | SAS | SQL Server | Pandas |
| --- | --- | --- | --- |
| Missing number | `.` | `NULL` | `NaN` |
| Missing text | `' '` (blank) | `NULL` (and `''` is different) | `None` / `NaN` |
| `missing < 0` | True | Unknown (row filtered out) | False |
| Sort order of missing | First | First in `ASC` (SQL Server puts NULL first) | Last by default |
| Blank text equals missing? | Yes | No (`''` is not `NULL`) | No |

### Descriptor portion and data portion

Every SAS dataset has two parts:

- **Descriptor portion:** the header. Dataset name, row count, creation date, and for each variable
  its name, type, length, format, informat and label.
- **Data portion:** the actual values.

`PROC CONTENTS` (Module 6) shows you the descriptor portion.

### 💼 Banking scenario: a library structure for a risk team

```text
/sasdata/
    raw/     libref RAW   - files landed from source systems, never changed
    stage/   libref STAGE - cleaned and validated data
    mart/    libref MART  - business-ready tables for reporting and models
    rpt/     libref RPT   - final report datasets
```

```sas
libname raw   "/sasdata/raw"   access=readonly;   /* protect source data from accidents */
libname stage "/sasdata/stage";
libname mart  "/sasdata/mart";
libname rpt   "/sasdata/rpt";
```

`ACCESS=READONLY` stops anyone from overwriting raw data by mistake. This is a common production
practice.

### ⚠️ Common mistakes

- A libref longer than 8 characters (`creditrisk`). SAS stops with an error saying the libref is
  longer than 8 characters, and the library is not assigned.
- Forgetting that WORK is temporary and losing a day's work when SAS closes.
- Storing card numbers as numbers and losing digits.
- Treating a missing number as zero or as negative by accident.

### Exercises

1. **Level 1:** Create librefs `raw` and `rpt` pointing to two folders. Check them with
   `libname _all_ list;`.
2. **Level 2:** Mark each as valid or invalid and explain: `txn2026`, `2026txn`, `txn-amt`, `_tmp`,
   `TxnAmt`.
3. **Level 3:** Show that a missing balance passes `if balance < 0` and fix the condition.
4. **Level 4 — Interview:** "What data types does SAS have, and how are dates stored?"
5. **Level 5:** Design a library layout for a fraud team and explain why raw data is read-only.

### ⭐ Interview questions

**Q1. How many data types does SAS have?**
- *Strong answer:* "Two: numeric and character. Dates, times and datetimes are numeric values with
  date formats. Numeric is 8 bytes by default; character length is fixed and set at compile time by
  the first time SAS sees the variable."
- *Common weak answer:* "Numeric, character and date."
- *Follow-up:* "How would you store a 16-digit card number, and why?"

**Q2. Where does a missing numeric value sort, and why does it matter?**
- *Strong answer:* "Missing sorts lower than any number, including negatives. So `amount < 100` is true
  for missing amounts. I add `not missing(amount)` to conditions like that."

**Q3. What is the difference between `WORK.LOANS` and `BANK.LOANS`?**
- *Strong answer:* "WORK is temporary and deleted at the end of the session. BANK is a permanent
  library pointing to a folder. A one-level name like `loans` means `WORK.LOANS`."

### Module wrap-up

- **I now know:** libraries and librefs, naming rules, the two data types, and missing values.
- **I can now:** set up libraries, name things safely, and avoid the missing-value trap.
- **Next:** Module 5 — creating datasets.

---

## MODULE 5 — Your First SAS Dataset, and the SET Statement

**Syllabus items:** 1.8 Creating the first SAS dataset · 1.21 Creating a new dataset from an existing
dataset · 2.1 SET statement

**You will learn:** how to type data straight into SAS, how to build one dataset from another, and
everything the SET statement can do. **Why it matters:** SET is the most-used statement in the DATA
step. **Before you start:** Module 4.

### Creating your first dataset (1.8)

You can type a small dataset directly into a program using `DATALINES` (the older keyword `CARDS`
does exactly the same).

This is the transaction dataset used in many examples in these notes:

```sas
data work.txn;
    length txn_id cust_id $4;
    input txn_id $ cust_id $ txn_date :date9. channel :$8. amount;
    format txn_date date9. amount comma12.;
    datalines;
T001 C101 02JAN2026 ATM 5000
T002 C102 02JAN2026 ONLINE 125000
T003 C101 05JAN2026 POS 2300
T004 C103 07JAN2026 ONLINE .
T005 C102 09JAN2026 ATM 20000
T006 C101 12JAN2026 ONLINE 78000
;
run;

proc print data=work.txn noobs;
run;
```

**Output**

| txn_id | cust_id | txn_date | channel | amount |
| --- | --- | --- | --- | --- |
| T001 | C101 | 02JAN2026 | ATM | 5,000 |
| T002 | C102 | 02JAN2026 | ONLINE | 125,000 |
| T003 | C101 | 05JAN2026 | POS | 2,300 |
| T004 | C103 | 07JAN2026 | ONLINE | . |
| T005 | C102 | 09JAN2026 | ATM | 20,000 |
| T006 | C101 | 12JAN2026 | ONLINE | 78,000 |

**Line by line**

| Code | What it does |
| --- | --- |
| `length txn_id cust_id $4;` | Both IDs are 4 characters. Giving every table the same length for `cust_id` matters later, when tables are joined (Module 33). |
| `input txn_id $ cust_id $` | Read two text values. Values are separated by spaces. |
| `txn_date :date9.` | Read a date written like `02JAN2026`. The colon means "read until the next space". |
| `channel :$8.` | Read text up to 8 characters long |
| `amount` | Read a number. A `.` in the data means missing. |
| `format txn_date date9. amount comma12.;` | Show the date as `02JAN2026` and the amount with commas |
| `datalines;` ... `;` | The data, ending with a lone semicolon |
| `proc print ... noobs;` | Print the dataset without the row-number column |

🧠 SAS stores `txn_date` as a number of days (`02JAN2026` is stored as `24108`). The `date9.` format
only changes how it is **shown**.

### The LENGTH trap: text cut to 8 characters

When you read text with simple list input and no length, SAS gives the variable a length of 8. Longer
values are cut off **without an error**.

```sas
/* WRONG: names longer than 8 characters are cut off */
data work.cust_bad;
    input cust_id $ name $ city $;
    datalines;
C101 Ashwathi Mumbai
C102 Bilal Navi_Mumbai
;
run;
/* name becomes 'Ashwathi' (fits), city becomes 'Navi_Mum' (cut!) */
```

```sas
/* RIGHT: set the lengths first */
data work.cust_ok;
    length cust_id $4 name $20 city $15;
    input cust_id $ name $ city $;
    datalines;
C101 Ashwathi Mumbai
C102 Bilal Navi_Mumbai
;
run;
```

📌 Put `LENGTH` **before** the first place the variable is used. SAS fixes each variable's type and
length the first time it sees the variable, during compilation (Module 7 explains why).

**Data with spaces inside values:** use a delimiter, such as a comma, with `DSD`.

```sas
data work.customers;
    infile datalines dlm=',' dsd;
    length cust_id $4 name $20 city $12 segment $1;
    input cust_id $ name $ city $ segment $ fico;
    datalines;
C101,Asha Rao,Mumbai,R,742
C102,Bilal Khan,Delhi,C,688
C103,Chetan Iyer,Pune,R,615
C104,Divya Menon,Chennai,S,
;
run;
```

`C104` has no FICO score after the last comma, so `fico` is missing. `DSD` treats two commas in a row
(or a comma at the end) as a missing value.

⚠️ If your data contains semicolons, use `DATALINES4;` and end the data with `;;;;`.

### Creating a new dataset from an existing one (1.21)

```sas
data work.big_txn;
    set work.txn;                     /* read every row of work.txn */
    where amount >= 50000;            /* keep only large transactions */
    gst = amount * 0.18;              /* add a new variable */
    format gst comma12.2;
run;
```

**Output**

| txn_id | cust_id | txn_date | channel | amount | gst |
| --- | --- | --- | --- | --- | --- |
| T002 | C102 | 02JAN2026 | ONLINE | 125,000 | 22,500.00 |
| T006 | C101 | 12JAN2026 | ONLINE | 78,000 | 14,040.00 |

**Why these rows:** T002 (125,000) and T006 (78,000) are at least 50,000. T004 is missing, and a
missing value is not `>= 50000`, so it is left out.

### The SET statement in depth (2.1)

`SET` reads observations from one or more SAS datasets into the DATA step, one observation per loop.

| Form | What it does | SQL Server | Pandas |
| --- | --- | --- | --- |
| `set a;` | Read every row of `a` | `SELECT * FROM a` | `df` |
| `set a b;` | Read all of `a`, then all of `b` (stacking) | `UNION ALL` | `pd.concat([a, b])` |
| `set a b; by date;` | Interleave: combine in `date` order (both must be sorted by `date`) | `UNION ALL ... ORDER BY date` | `pd.concat(...).sort_values("date")` |
| `set a(where=(...));` | Read only matching rows | `WHERE` | Boolean filter |
| `set a end=last;` | `last` becomes 1 on the final row | — | — |
| `set a nobs=n;` | `n` holds the number of rows (known before reading) | `COUNT(*)` | `len(df)` |
| `set a point=i;` | Read row number `i` directly (Module 20) | — | `df.iloc[i-1]` |

**Stacking two months of transactions**

```sas
data work.txn_jan;  set work.txn; where month(txn_date) = 1;  run;
data work.txn_feb;
    length txn_id cust_id $4;
    input txn_id $ cust_id $ txn_date :date9. channel :$8. amount;
    format txn_date date9. amount comma12.;
    datalines;
T101 C101 03FEB2026 ATM 4000
T102 C104 05FEB2026 POS 1500
;
run;

data work.txn_q1;
    set work.txn_jan work.txn_feb;      /* 6 rows + 2 rows = 8 rows */
run;
```

**Using END= to do something after the last row**

```sas
data _null_;                           /* _null_: run the step but create no dataset */
    set work.txn end=last;
    total + amount;                    /* running total (Module 34) */
    if last then put "Total amount: " total comma12.;
run;
```

**Log:**

```text
Total amount: 230,300
```

5,000 + 125,000 + 2,300 + 20,000 + 78,000 = 230,300. The missing amount is ignored by the sum
statement.

### 💼 Banking scenario

Every morning a bank lands three files: card, UPI and ATM transactions, all with the same columns. One
`SET` statement stacks them into a single daily dataset for the fraud rules:

```sas
data stage.txn_daily;
    set raw.card_txn raw.upi_txn raw.atm_txn indsname=source;
    length source_table $41;
    source_table = source;             /* which file each row came from */
run;
```

`INDSNAME=` stores the name of the dataset each row came from. This helps when a total does not
reconcile.

### 🚀 Best practices

- **Good:** set lengths before reading text. **Bad:** trusting the default length of 8.
- **Good:** write to a new dataset name while developing. **Bad:** `data work.txn; set work.txn;`,
  which replaces your input. A bug can lose data.
- **Good:** when stacking, check that the same variable has the same type and length in every
  dataset. A shorter length in the first dataset cuts off values from the later ones.

### ⚠️ Common mistakes

- Text cut to 8 characters (no error, only wrong data).
- `ERROR: Variable amount has been defined as both character and numeric.` when stacking datasets
  where `amount` is text in one and a number in the other.
- `WARNING: Multiple lengths were specified for the variable name by input data set(s). This can cause
  truncation of data.` Fix with a `LENGTH` statement before `SET`.
- Putting `DATALINES` anywhere but at the end of the DATA step.

### Exercises

1. **Level 1:** Create a dataset of 5 customers with id, name, city and balance using `DATALINES`.
2. **Level 2:** Create `work.online_txn` from `work.txn` with only ONLINE rows and a new variable
   `fee = amount * 0.01`.
3. **Level 3:** Stack two datasets where `name` has length 10 in the first and 25 in the second. Find
   the warning and fix it.
4. **Level 4 — Interview:** "What happens when you list two datasets in one SET statement?"
5. **Level 5:** Stack three channel files, record the source file, and print the row count per source.

### ⭐ Interview questions

**Q1. What does the SET statement do?**
- *Strong answer:* "SET reads observations from SAS datasets into the PDV, one per iteration of the
  DATA step. With several datasets it stacks them; with a BY statement it interleaves them in order.
  Options like WHERE=, END=, NOBS= and POINT= control what and how it reads."
- *Follow-up:* "What is the difference between `set a b;` and `merge a b;`?" (Stacking vs joining
  side by side — Module 33.)

**Q2. Why must LENGTH come before INPUT or SET?**
- *Strong answer:* "SAS fixes a variable's type and length at compile time, the first time it sees
  the variable. If INPUT or SET comes first, the length is already decided."

### Module wrap-up

- **I now know:** DATALINES, list input, the LENGTH trap, and the forms of SET.
- **I can now:** create datasets from typed data and from other datasets, and stack datasets.
- **Next:** Module 6 — describing and copying datasets.

---

## MODULE 6 — Describing and Copying Datasets

**Syllabus items:** 1.20 Describing a dataset and library · 1.22 Copying datasets from one library to
another

**You will learn:** how to see a dataset's structure, list a library, and copy or move datasets.
**Why it matters:** the first thing you do with unknown data is look at its structure. Copying
datasets between environments happens every week in real teams. **Before you start:** Modules 4–5.

### Describing a dataset: PROC CONTENTS

```sas
proc contents data=work.customers varnum;
run;
```

`VARNUM` lists variables in the order they are stored, instead of alphabetical order.

**Output (main parts)**

```text
Data Set Name   WORK.CUSTOMERS          Observations          4
Member Type     DATA                    Variables             5
Engine          V9                      Indexes               0
Created         05OCT2026 10:14:02

               Variables in Creation Order
 #    Variable    Type    Len
 1    cust_id     Char      4
 2    name        Char     20
 3    city        Char     12
 4    segment     Char      1
 5    fico        Num       8
```

This is the **descriptor portion** from Module 4.

### Describing a library

```sas
/* every dataset in the library, without the detail of each one */
proc contents data=bank._all_ nods;
run;

/* PROC DATASETS lists the members of a library */
proc datasets library=bank;
quit;
```

`_ALL_` means every member of the library. `NODS` means "no details", so you get just the list.

**Using dictionary tables** (more in Module 32):

```sas
proc sql;
    select memname, nobs, nvar, crdate
    from dictionary.tables
    where libname = 'BANK';        /* library names are stored in uppercase */
quit;
```

### Copying datasets between libraries (1.22)

**Option 1: PROC COPY** (best for straight copies)

```sas
libname dev  "/sasdata/dev/mart";
libname prod "/sasdata/prod/mart";

proc copy in=prod out=dev memtype=data;
    select loans customers;             /* only these two datasets */
run;
```

- Without `SELECT`, every dataset is copied.
- `EXCLUDE` copies everything except the listed datasets.
- `MOVE` (written `proc copy in=... out=... move;`) moves instead of copying, deleting the originals.

**Option 2: PROC DATASETS** (same idea, plus many management tools)

```sas
proc datasets library=prod nolist;
    copy out=dev;
    select loans;
quit;
```

**Option 3: a DATA step** (when you also want to change the data)

```sas
data dev.loans_2026;
    set prod.loans;
    where year(open_date) = 2026;
run;
```

| Method | Keeps indexes and constraints | Can change the data | Speed |
| --- | --- | --- | --- |
| `PROC COPY` | Yes | No | Fast (block copy) |
| `PROC DATASETS COPY` | Yes | No | Fast |
| DATA step with `SET` | No | Yes | Slower (rewrites every row) |

### PROC DATASETS: managing datasets without rewriting them (industry gap)

```sas
proc datasets library=work nolist;
    change txn_q1 = txn_quarter1;                  /* rename a dataset */
    modify customers;                              /* change attributes in place */
        rename fico = fico_score;
        label  fico_score = "Bureau FICO score";
        format fico_score 3.;
    delete txn_jan txn_feb;                        /* delete datasets */
quit;
```

`MODIFY` changes only the descriptor portion, so it is instant even on 100 million rows. A DATA step
would rewrite every row to do the same thing.

### SQL Server and Pandas equivalents

| Task | SAS | SQL Server | Pandas |
| --- | --- | --- | --- |
| Show structure | `PROC CONTENTS` | `sp_help 'dbo.loans'` or `INFORMATION_SCHEMA.COLUMNS` | `df.info()`, `df.dtypes` |
| List tables | `PROC DATASETS`, `dictionary.tables` | `INFORMATION_SCHEMA.TABLES` | `os.listdir()` |
| Copy table | `PROC COPY` | `SELECT * INTO dev.dbo.loans FROM prod.dbo.loans` | `df.to_parquet(...)` |
| Rename column | `PROC DATASETS MODIFY ... RENAME` | `sp_rename` | `df.rename(columns=...)` |

### 💼 Banking scenario

Before a release, a risk team copies last month's production loan mart into the test library, runs
the new code there, and compares results with production (PROC COMPARE, Module 39). PROC COPY moves
40 datasets in one step and keeps their indexes.

### ⚠️ Common mistakes

- Using a DATA step to copy and losing indexes without noticing.
- Running `PROC COPY` without `SELECT` and copying hundreds of datasets by accident.
- Using `MOVE` and deleting the source datasets.
- Forgetting `QUIT;` after `PROC DATASETS`.

### Exercises

1. **Level 1:** Run PROC CONTENTS on `sashelp.class` and list the variables and their types.
2. **Level 2:** List all datasets in `SASHELP` with their row counts using `dictionary.tables`.
3. **Level 3:** Copy two datasets from WORK to a new library, then rename one with PROC DATASETS.
4. **Level 4 — Interview:** "How would you copy 50 datasets from production to test and keep their
   indexes?"
5. **Level 5:** Write a program that lists every dataset in a library with fewer than 10 rows.

### ⭐ Interview questions

**Q1. How do you see the structure of a dataset?**
- *Strong answer:* "PROC CONTENTS shows the descriptor portion: row count, variable names, types,
  lengths, formats and labels. For a whole library I use `_ALL_ NODS` or query
  `dictionary.columns` in PROC SQL."

**Q2. PROC COPY or a DATA step to copy a dataset?**
- *Strong answer:* "PROC COPY for a straight copy: it is faster and keeps indexes and constraints. A
  DATA step only when I need to change the data on the way."

### Module wrap-up

- **I now know:** PROC CONTENTS, PROC DATASETS, PROC COPY, and dictionary tables.
- **I can now:** inspect unknown datasets and libraries, and copy, move, rename and delete datasets.
- **Next:** Module 7 — the PDV, the most important idea in SAS.

---

## MODULE 7 — How the DATA Step Works Inside: Compilation, Execution and the PDV

**Syllabus items:** 3.14 PDV and PDV by example

**You will learn:** exactly what SAS does when it runs a DATA step. **Why it matters:** 🔥 this is the
most important idea in SAS. It explains WHERE vs IF, RETAIN, FIRST./LAST., MERGE behaviour and the
LENGTH trap. Almost every SAS interview asks about it. **Before you start:** Modules 3–5.

### 🧠 What it is

The **Program Data Vector (PDV)** is a one-row workspace in memory. The DATA step builds each output
row in the PDV, one row at a time:

1. Clear the workspace (most variables become missing).
2. Read one row into the workspace.
3. Run your statements on that row.
4. Write the row from the workspace to the output dataset.
5. Go back to step 1 for the next row.

SQL and Pandas do not have a PDV. They work on whole tables or whole columns at once. The PDV is what
makes SAS a **row-by-row** language.

### The two phases of every DATA step

**Phase 1: Compilation (before any data is read)**

1. SAS checks the syntax of every statement.
2. If raw data is read with `INPUT`, SAS creates an **input buffer**: a memory area that holds one line
   of the raw file.
3. SAS creates the **PDV**, adding each variable in the order it first appears in the code. Each
   variable's type and length are fixed **now**.
4. SAS adds two **automatic variables** to the PDV:
   - `_N_` counts how many times the DATA step has started a new loop (iteration).
   - `_ERROR_` is 0, or 1 if an error happened in the current iteration (such as invalid data).
5. SAS creates the **descriptor portion** of the output dataset.

**Phase 2: Execution (once for each row)**

1. `_N_` goes up by 1. `_ERROR_` is reset to 0.
2. Variables from `INPUT` and from assignment statements are reset to missing. (Variables read with
   `SET`, `MERGE` or `UPDATE`, variables in a `RETAIN` statement, and sum-statement variables are
   **not** reset.)
3. SAS runs your statements from top to bottom.
4. At the bottom (`RUN;`) there is a hidden **OUTPUT**: the PDV is written as a new row.
5. Control returns to the top. When `INPUT` or `SET` finds no more data, the step ends.

```text
           COMPILATION                                EXECUTION (repeats per row)
   +---------------------------+          +-------------------------------------------+
   | check syntax              |          | _N_ + 1, _ERROR_ = 0                      |
   | build input buffer        |   --->   | reset non-retained variables to missing   |
   | build PDV (names, types,  |          | read a row (INPUT or SET)                 |
   |   lengths fixed here)     |          | run your statements                       |
   | add _N_ and _ERROR_       |          | implicit OUTPUT at RUN                    |
   | build descriptor portion  |          | back to the top; stop at end of data      |
   +---------------------------+          +-------------------------------------------+

   Raw file --> INFILE/INPUT --> Input buffer --> PDV --> Output SAS dataset --> PROCs
   SAS dataset ------------ SET -------------------^
```

### PDV by example (3.14)

Here is a small step with a hidden bug.

```sas
data work.txn_flag;
    input txn_id $ amount;
    if amount <= 50000 then risk = 'LOW';
    else risk = 'HIGH';
    datalines;
T001 5000
T002 125000
T003 abc
;
run;
```

**Output**

| txn_id | amount | risk |
| --- | --- | --- |
| T001 | 5000 | LOW |
| T002 | 125000 | **HIG** |
| T003 | . | LOW |

Two things went wrong, and the PDV explains both.

**Bug 1: `HIGH` became `HIG`.** During compilation SAS meets `risk = 'LOW'` first, so it gives `risk`
a length of **3**. Lengths are fixed at compilation, so `'HIGH'` cannot fit later.

**Bug 2: T003 is `LOW`.** `abc` is not a number, so `amount` becomes missing and `_ERROR_` becomes 1.
A missing value is smaller than any number, so `amount <= 50000` is **true**.

**The Log shows the invalid data**

```text
NOTE: Invalid data for amount in line 33 6-8.
RULE:      ----+----1----+----2----+----3----+----4----+----5----+----6
33         T003 abc
txn_id=T003 amount=. risk=LOW _ERROR_=1 _N_=3
NOTE: The data set WORK.TXN_FLAG has 3 observations and 3 variables.
```

(The line number `33` depends on where the code sits in your program.) The last line is the PDV dumped
to the Log: SAS does this automatically when `_ERROR_` is 1.

**The fixed program**

```sas
data work.txn_flag;
    input txn_id $ amount;
    length risk $7;                         /* fix bug 1: room for the longest value */
    if missing(amount) then risk = 'UNKNOWN'; /* fix bug 2: handle missing first */
    else if amount <= 50000 then risk = 'LOW';
    else risk = 'HIGH';
    datalines;
T001 5000
T002 125000
T003 abc
;
run;
```

`LENGTH` is placed after `INPUT` here, so the variable order stays `txn_id amount risk`. (Variables
are placed in the PDV in the order SAS first meets them. Putting `LENGTH` at the very top would make
`risk` the first column.)

**Watching the PDV, step by step**

| Moment | `_N_` | `_ERROR_` | `txn_id` | `amount` | `risk` | Written? |
| --- | --- | --- | --- | --- | --- | --- |
| Start of loop 1 | 1 | 0 | (blank) | . | (blank) | |
| After INPUT | 1 | 0 | T001 | 5000 | (blank) | |
| After IF/ELSE | 1 | 0 | T001 | 5000 | LOW | |
| At RUN (implicit OUTPUT) | 1 | 0 | T001 | 5000 | LOW | ✓ row 1 |
| Start of loop 2 | 2 | 0 | (blank) | . | (blank) | |
| After INPUT | 2 | 0 | T002 | 125000 | (blank) | |
| At RUN | 2 | 0 | T002 | 125000 | HIGH | ✓ row 2 |
| Start of loop 3 | 3 | 0 | (blank) | . | (blank) | |
| After INPUT (`abc` is invalid) | 3 | **1** | T003 | . | (blank) | |
| At RUN | 3 | 1 | T003 | . | UNKNOWN | ✓ row 3 |
| Start of loop 4: INPUT finds no data | 4 | 0 | | | | Step ends. Nothing written. |

**Final output**

| txn_id | amount | risk |
| --- | --- | --- |
| T001 | 5000 | LOW |
| T002 | 125000 | HIGH |
| T003 | . | UNKNOWN |

📌 `_N_` and `_ERROR_` are in the PDV but are **never** written to the output dataset.

### Seeing the PDV yourself: PUT _ALL_

```sas
data _null_;
    set work.txn(obs=2);
    put _all_;
run;
```

**Log**

```text
txn_id=T001 cust_id=C101 txn_date=02JAN2026 channel=ATM amount=5,000 _ERROR_=0 _N_=1
txn_id=T002 cust_id=C102 txn_date=02JAN2026 channel=ONLINE amount=125,000 _ERROR_=0 _N_=2
```

This is one of the best debugging tools in SAS. Add `put _all_;` anywhere in a DATA step to see the
workspace at that moment.

### Temporary vs permanent variables

| In the PDV and written to the output | In the PDV but **not** written to the output |
| --- | --- |
| Variables read from input | `_N_`, `_ERROR_` |
| Variables you create | Variables in a `DROP` statement or `DROP=` option |
| | `IN=` variables (Module 33), `FIRST.` and `LAST.` variables (Module 34) |
| | `END=`, `NOBS=` and `POINT=` variables |
| | Temporary array elements (Module 38) |

### What the PDV explains (preview of later modules)

| Behaviour | Explained by |
| --- | --- |
| `WHERE` cannot use variables you create in the step | WHERE filters **before** a row enters the PDV (Module 16) |
| `RETAIN` keeps values between rows | Retained variables are not reset at the top of the loop (Module 34) |
| Running totals with `total + amount;` | Sum-statement variables are retained automatically (Module 34) |
| `FIRST.` and `LAST.` | Temporary PDV variables set by the BY statement (Module 34) |
| MERGE repeats values in one-to-many joins | Variables read by MERGE are not reset within a BY group (Module 33) |
| `LENGTH` must come first | Types and lengths are fixed at compilation (this module) |

### SQL Server and Pandas comparison

| Question | SAS DATA step | SQL Server | Pandas |
| --- | --- | --- | --- |
| How is data processed? | One row at a time through the PDV | All rows as a set | Whole columns at once |
| "Previous row" logic | Natural (RETAIN, LAG) | Window functions (`LAG`, `SUM() OVER`) | `shift()`, `cumsum()` |
| Memory use | One row (plus buffers): works on huge files | Engine-managed | Whole table in memory |

### 💼 Banking scenario

A fraud rule needs "time since this card's previous transaction". In SQL Server you would write a
window function. In SAS, because the PDV processes rows in order, you sort by card and time, then
compare each row with the value kept from the previous row (Module 34). Knowing the PDV is what makes
this logic easy and fast, even on 100 million rows.

### ⚠️ Common mistakes and interview traps

- Thinking `_N_` is the row number of the **output**. It counts loop iterations. If you delete rows,
  `_N_` and the output row number differ (Module 20).
- Expecting a new variable to keep its value from the previous row. It is reset to missing unless you
  RETAIN it.
- Setting `LENGTH` after the first use of a variable. You get
  `WARNING: Length of character variable has already been set.`

### Exercises

1. **Level 1:** Add `put _all_;` to a DATA step and read the Log.
2. **Level 2:** Write the PDV table (like the one above) for a 3-row dataset of your own.
3. **Level 3:** Create a bug where a text value is truncated because of compile-time length, then fix
   it in two different ways.
4. **Level 4 — Interview:** "Explain the compilation and execution phases of a DATA step."
5. **Level 5:** A colleague's flag variable shows `CRITICA` instead of `CRITICAL`. Explain the cause
   using the PDV, and fix it.

### ⭐ Interview questions

**Q1. What is the PDV?**
- *What they are testing:* whether you understand how SAS really works.
- *Strong answer:* "The Program Data Vector is the memory area where the DATA step builds one
  observation at a time. It is created at compile time with every variable in order of first
  appearance, plus the automatic variables `_N_` and `_ERROR_`. During execution SAS resets
  non-retained variables to missing, reads a row, runs the statements and writes the PDV to the
  output dataset at the end of each iteration."
- *Example:* the `'HIG'` truncation above.
- *Weak answer:* "It is a temporary table."
- *Follow-up:* "Which variables are not reset to missing at the start of each iteration?"

**Q2. What happens during compilation?**
- *Strong answer:* "Syntax check, input buffer creation for raw data, PDV creation with types and
  lengths fixed, the automatic variables added, and the descriptor portion of the output dataset
  created. No data is read yet."

**Q3. Is `_N_` the observation number?**
- *Strong answer:* "It is the iteration count of the DATA step. It equals the row number only when
  every iteration writes exactly one row. With subsetting IF or DELETE, they differ."

### Module wrap-up

- **I now know:** compilation vs execution, the input buffer, the PDV, `_N_` and `_ERROR_`, and which
  variables are reset each loop.
- **I can now:** predict a DATA step's output and explain bugs like truncation and missing-value
  logic.
- **Next:** Part II — getting data in and out, starting with raw text files.

**Part I checklist:** ✓ 1.1 · ✓ 1.2 · ✓ 1.3 · ✓ 1.4 · ✓ 1.5 · ✓ 1.6 · ✓ 1.7 · ✓ 1.8 · ✓ 1.9 · ✓ 1.10 · ✓ 1.11 · ✓ 1.13 ·
✓ 1.14 · ✓ 1.15 · ✓ 1.16 · ✓ 1.20 · ✓ 1.21 · ✓ 1.22 · ✓ 2.1 · ✓ 2.2 · ✓ 3.14

---

# Part II — Getting Data In and Out (Modules 8–12)

## MODULE 8 — Reading Raw Text Files with INFILE and INPUT

**Syllabus items:** 1.12 Creating SAS dataset from fixed-format text file · 3.3 Reading and writing TXT
files · 3.11 Reading/writing TXT delimited files

**You will learn:** the three ways to read text files, how to handle delimiters, quotes, headers and
short lines, and how to write text files. **Why it matters:** banks still exchange huge fixed-width
and pipe-delimited files with card networks, bureaus and core banking systems. **Before you start:**
Modules 5 and 7.

### 🧠 What it is

Reading a text file takes two statements:

- **`INFILE`** says **where** the file is and how it is laid out (delimiter, header, short lines).
- **`INPUT`** says **how** to read each line into variables.

```text
accounts.txt --INFILE--> input buffer (one line) --INPUT--> PDV --> work.accounts
```

You can name a file directly in `INFILE`, or give it a short name (a **fileref**) with `FILENAME`:

```sas
filename acctin "C:\sasdata\raw\accounts.txt";
/* later: infile acctin; */
```

### The three input styles

| Style | Example | Use it when |
| --- | --- | --- |
| **List input** | `input cust_id $ amount;` | Values are separated by spaces or a delimiter |
| **Column input** | `input acct_id $ 1-6 balance 25-36;` | Each value is always in the same columns |
| **Formatted input** | `input @15 open_date ddmmyy10. @25 balance 12.;` | Fixed columns **and** values need special reading (dates, commas) |

You can mix styles in one `INPUT` statement.

### Reading a fixed-format file (1.12)

A core banking system sends `accounts.txt`. Every value is always in the same columns:

```text
----+----1----+----2----+----3----+--
A10001MUMBAI  15/03/2019   250000.50S
A10002DELHI   01/11/2021    18000.00C
A10003PUNE    22/07/2024        0.00S
```

| Field | Columns | Example |
| --- | --- | --- |
| Account ID | 1–6 | `A10001` |
| Branch | 7–14 | `MUMBAI` |
| Open date (dd/mm/yyyy) | 15–24 | `15/03/2019` |
| Balance | 25–36 | `250000.50` |
| Account type (S = savings, C = current) | 37 | `S` |

```sas
data work.accounts;
    infile "C:\sasdata\raw\accounts.txt" truncover;
    input @1  acct_id   $6.
          @7  branch    $8.
          @15 open_date ddmmyy10.
          @25 balance   12.
          @37 acct_type $1.;
    format open_date date9. balance comma14.2;
run;
```

**Line by line**

| Code | What it does |
| --- | --- |
| `infile "..." truncover;` | Read this file. If a line is shorter than expected, keep what is there (explained below). |
| `@1 acct_id $6.` | Go to column 1. Read 6 characters as text. |
| `@15 open_date ddmmyy10.` | Go to column 15. Read 10 characters as a day/month/year date. |
| `@25 balance 12.` | Go to column 25. Read 12 characters as a number. The decimal point in the data is kept. |
| `format ...` | Show the date as `15MAR2019` and the balance with commas |

**Output**

| acct_id | branch | open_date | balance | acct_type |
| --- | --- | --- | --- | --- |
| A10001 | MUMBAI | 15MAR2019 | 250,000.50 | S |
| A10002 | DELHI | 01NOV2021 | 18,000.00 | C |
| A10003 | PUNE | 22JUL2024 | 0.00 | S |

**The same file with column input** (simpler, but it cannot read dates):

```sas
data work.accounts_col;
    infile "C:\sasdata\raw\accounts.txt" truncover;
    input acct_id $ 1-6  branch $ 7-14  open_date_txt $ 15-24  balance 25-36  acct_type $ 37;
run;
```

Here the date stays as text. Formatted input is better when any field needs an informat.

**Testing without a file:** you can put the same lines after `datalines;` and use
`infile datalines truncover;`. The data lines must start in column 1, or the columns shift.

### Common informats

An **informat** tells SAS how to **read** a value.

| Informat | Reads | Example raw value | Stored value |
| --- | --- | --- | --- |
| `$w.` | Text, `w` characters, leading blanks removed | `MUMBAI  ` | `MUMBAI` |
| `$CHARw.` | Text, leading blanks kept | `  A12` | `  A12` |
| `w.d` | A plain number | `250000.50` | 250000.5 |
| `COMMAw.d` | A number with commas, currency signs or brackets | `1,25,000` | 125000 |
| `DATE9.` | `ddMONyyyy` | `02JAN2026` | 24108 |
| `DDMMYY10.` | `dd/mm/yyyy` | `15/03/2019` | 21623 |
| `YYMMDD10.` | `yyyy-mm-dd` | `2026-01-02` | 24108 |
| `ANYDTDTE10.` | Many date layouts (guesses) | `2026/01/02` | 24108 |

⚠️ `ANYDTDTE.` guesses. `03/04/2026` could be 3 April or 4 March. Use an exact informat when you
know the layout. The `DATESTYLE=` system option controls how ambiguous dates are guessed.

### Reading delimited files (3.11)

A card switch sends a pipe-delimited file with a header row. One merchant name contains a pipe
inside quotes, and one merchant is empty:

```text
txn_id|cust_id|txn_date|merchant|amount
T001|C101|2026-01-02|Amazon India|5000
T002|C102|2026-01-02|"Croma | Electronics"|125000
T003|C101|2026-01-05||2300
```

```sas
data work.txn_raw;
    infile "C:\sasdata\raw\transactions.txt" dlm='|' dsd firstobs=2 truncover;
    length txn_id $5 cust_id $5 merchant $40;
    input txn_id $ cust_id $ txn_date :yymmdd10. merchant $ amount;
    format txn_date date9.;
run;
```

**Output**

| txn_id | cust_id | txn_date | merchant | amount |
| --- | --- | --- | --- | --- |
| T001 | C101 | 02JAN2026 | Amazon India | 5000 |
| T002 | C102 | 02JAN2026 | Croma \| Electronics | 125000 |
| T003 | C101 | 05JAN2026 | (blank) | 2300 |

**The INFILE options that matter**

| Option | What it does |
| --- | --- |
| `DLM='\|'` | Values are separated by `\|`. Use `DLM=','` for commas and `DLM='09'x` for tabs. Once you set `DLM=`, spaces are no longer separators, so `Amazon India` stays in one piece. |
| `DSD` | Three things: two delimiters in a row mean a missing value; quotes around a value are removed; a delimiter **inside** quotes is treated as text |
| `FIRSTOBS=2` | Start reading at line 2 (skip the header) |
| `OBS=n` | Stop after line `n` (useful for testing) |
| `TRUNCOVER` | If a line ends early, keep what was read and set the rest to missing |
| `MISSOVER` | If a line ends early, set the rest to missing, **including a partly read value** |
| `LRECL=` | The longest line length to read. Raise it for very long lines (for example `lrecl=32767`). |

**List input modifiers**

| Modifier | Example | Meaning |
| --- | --- | --- |
| `:` (colon) | `txn_date :yymmdd10.` | Use this informat, but read only up to the next delimiter |
| `&` (ampersand) | `name & $30.` | The value may contain single spaces. Two spaces end it. |
| `~` (tilde) | `merchant ~ $40.` | With DSD: keep the quotes around the value |

### TRUNCOVER vs MISSOVER vs the default (FLOWOVER)

Suppose `remarks.txt` has lines of different lengths, and you read the remark from columns 8–37:

```text
A10001 KYC pending
A10002 Address updated
```

```sas
data work.remarks;
    infile "C:\sasdata\raw\remarks.txt" truncover;   /* try missover and no option too */
    input acct_id $ 1-6 remark $ 8-37;
run;
```

| INFILE option | What happens | Result |
| --- | --- | --- |
| None (FLOWOVER, the default) | SAS jumps to the **next line** to finish reading `remark`. The Log says `NOTE: SAS went to a new line when INPUT statement reached past the end of a line.` | ✗ Values come from the wrong lines and rows are lost |
| `MISSOVER` | `remark` needs columns 8–37 but the line stops earlier, so SAS sets `remark` to missing | ✗ Both remarks are blank |
| `TRUNCOVER` | SAS reads what is there | ✓ `KYC pending`, `Address updated` |

📌 Use `TRUNCOVER` by default for files with lines of different lengths.

⚠️ This problem **does not appear** when you test with `DATALINES`, because SAS pads data lines with
blanks to 80 characters. A program that works on DATALINES can still fail on the real file.

### Writing text files (3.3, 3.11)

Writing is the mirror of reading: `FILE` says where, and `PUT` says what to write.

**A fixed-width file**

```sas
data _null_;
    set work.accounts;
    file "C:\sasdata\out\accounts_fixed.txt";
    put @1  acct_id   $6.
        @7  branch    $8.
        @15 open_date ddmmyy10.
        @25 balance   12.2
        @37 acct_type $1.;
run;
```

**A delimited file with a header**

```sas
data _null_;
    set work.txn_raw;
    file "C:\sasdata\out\txn_export.csv" dlm=',' dsd;
    if _n_ = 1 then put "txn_id,cust_id,txn_date,merchant,amount";
    put txn_id cust_id txn_date :yymmdd10. merchant amount;
run;
```

With `DSD` on the `FILE` statement, SAS puts quotes around any value that contains the delimiter. A
merchant called `Shah, Sons & Co` would be written as `"Shah, Sons & Co"`, so the CSV columns stay
lined up.

`DATA _NULL_` runs the step without creating a dataset. It is the standard way to write files and
messages.

### SQL Server and Pandas

| Task | SAS | SQL Server | Pandas |
| --- | --- | --- | --- |
| Read CSV | `INFILE ... DLM=',' DSD FIRSTOBS=2` | `BULK INSERT ... WITH (FIELDTERMINATOR=',', FIRSTROW=2)` | `pd.read_csv(path)` |
| Read fixed width | Column or formatted input | `BULK INSERT` with a format file | `pd.read_fwf(path, colspecs=...)` |
| Write a file | `FILE` + `PUT` | `bcp` utility | `df.to_csv(path)` |

📌 The SAS approach gives you full control of every column's type, length and informat. `read_csv`
guesses types from the data; SAS lets you state them exactly, which is safer for production files.

### 💼 Banking scenario

A bank receives a 40 GB fixed-width card authorisation file every night. Pandas would need more memory
than the server has. A SAS DATA step reads it one line at a time with formatted input, so memory use
stays tiny. `LRECL=` is set to the record length, and `TRUNCOVER` protects against short trailer lines.

### ⚠️ Common mistakes

- Leaving out `DSD` on CSV files. Empty values shift all later columns left.
- Forgetting `FIRSTOBS=2`. The header becomes a data row, with invalid-data notes for every number.
- Using `MISSOVER` when the last field can be short. Real values become missing.
- Reading a date with `$10.`, so it stays text and cannot be used in date arithmetic.
- Text cut to 8 characters because there was no `LENGTH` statement.

### Exercises

1. **Level 1:** Read a 3-line CSV with a header into SAS using `INFILE` and `INPUT`.
2. **Level 2:** Read the fixed-width `accounts.txt` with column input, then with formatted input.
3. **Level 3:** Create a file with short lines and show the difference between FLOWOVER, MISSOVER and
   TRUNCOVER.
4. **Level 4 — Interview:** "What does the DSD option do?"
5. **Level 5:** Read a pipe file where merchant names contain pipes in quotes, then write it back out
   as a CSV with a header.

### ⭐ Interview questions

**Q1. What is the difference between MISSOVER and TRUNCOVER?**
- *What they are testing:* experience with real files.
- *Strong answer:* "Both stop SAS from jumping to the next line when a record is short. MISSOVER sets
  a value to missing if it is not complete. TRUNCOVER keeps the partial value. For variable-length
  records I use TRUNCOVER."
- *Common weak answer:* "They are the same."
- *Follow-up:* "Why might your test with DATALINES not show the problem?"

**Q2. List, column and formatted input: when do you use each?**
- *Strong answer:* "List input for delimited data, column input for fixed positions with simple
  values, and formatted input for fixed positions that need informats such as dates or numbers with
  commas."

**Q3. What does DSD do?**
- *Strong answer:* "It treats consecutive delimiters as missing values, removes quotes from values, and
  lets a quoted value contain the delimiter. It also makes comma the delimiter unless DLM= says
  otherwise."

### Module wrap-up

- **I now know:** INFILE, INPUT, the three input styles, informats, DLM, DSD, FIRSTOBS, TRUNCOVER,
  MISSOVER, FILE and PUT.
- **I can now:** read fixed-width and delimited files reliably and write files back out.
- **Next:** Module 9 — @, @@ and messy files.

---

## MODULE 9 — Holding the Line: @ and @@, and Reading Messy Files

**Syllabus items:** 3.12 @ vs @@ while reading data · 3.13 Reading unstructured data into structured
datasets

**You will learn:** how to read a line in several passes, how to read many records from one line, and
how to pull structure out of free text. **Why it matters:** real files are often not neat tables.
**Before you start:** Module 8.

### 🧠 Three different "@" symbols

| Symbol | Where | Meaning |
| --- | --- | --- |
| `@15` | Inside INPUT, before a variable | **Column pointer:** move to column 15 |
| `@'text'` | Inside INPUT | **Character pointer:** move to just after the next place `text` appears |
| `@` | At the **end** of INPUT | **Single trailing @:** keep this line for the **next INPUT in the same loop** |
| `@@` | At the **end** of INPUT | **Double trailing @:** keep this line **across loops** |

Normally every `INPUT` statement starts by moving to a new line. The trailing `@` and `@@` stop that.

### Single trailing @: decide how to read a line after peeking at it

A branch file has **header** lines (`H`) and **detail** lines (`D`):

```text
H BR001 05JAN2026
D T001 5000
D T002 125000
H BR002 05JAN2026
D T003 2300
```

```sas
data work.branch_txn;
    infile datalines;
    retain branch batch_date;                 /* keep header values for the detail lines */
    input rec_type $1. @;                     /* read 1 character, then HOLD the line */
    if rec_type = 'H' then
        input @3 branch $5. @9 batch_date date9.;
    else if rec_type = 'D' then do;
        input @3 txn_id $4. @8 amount;
        output;                               /* write only detail rows */
    end;
    format batch_date date9.;
    drop rec_type;
    datalines;
H BR001 05JAN2026
D T001 5000
D T002 125000
H BR002 05JAN2026
D T003 2300
;
run;
```

**Output**

| branch | batch_date | txn_id | amount |
| --- | --- | --- | --- |
| BR001 | 05JAN2026 | T001 | 5000 |
| BR001 | 05JAN2026 | T002 | 125000 |
| BR002 | 05JAN2026 | T003 | 2300 |

**Line by line**

| Code | What it does |
| --- | --- |
| `retain branch batch_date;` | Do not reset these at the top of each loop, so detail lines can use the last header's values (Module 34) |
| `input rec_type $1. @;` | Read the first character. The `@` keeps the same line for the next INPUT. |
| `if rec_type = 'H' then input ...;` | For a header, read the branch and date from the same line |
| `input @3 txn_id $4. @8 amount;` | For a detail, read the transaction from the same line |
| `output;` | Write a row. Because the step contains an OUTPUT statement, SAS writes rows **only** where OUTPUT runs, so header lines are not written. |

The line held by a single `@` is released at the end of the loop.

### Double trailing @@: many records on one line

```sas
data work.scores;
    input cust_id $ score @@;
    datalines;
C101 742 C102 688 C103 615
C104 790 C105 701
;
run;
```

**Output:** 5 rows.

| cust_id | score |
| --- | --- |
| C101 | 742 |
| C102 | 688 |
| C103 | 615 |
| C104 | 790 |
| C105 | 701 |

**Without `@@`** you get only 2 rows (`C101 742` and `C104 790`), because each loop's INPUT would jump
to a new line and ignore the rest of the current one.

| | Single trailing `@` | Double trailing `@@` |
| --- | --- | --- |
| Holds the line | Until the next INPUT **in the same loop** | **Across loops**, until the line is used up |
| Typical use | Read a record-type code, then decide how to read the rest | Several observations on one line |
| Released when | The loop ends | The line has no more data (or an INPUT without `@@` runs) |

⚠️ Do not combine `@@` with column input or with `MISSOVER`. `@@` is for list input across a line.

### Reading unstructured data into a structured dataset (3.13)

**1. Use text markers with the character pointer.** Call-centre notes look like this:

```text
Customer: C101 | Called on 03JAN2026 | Disputed amount: Rs 12,500 | Status: OPEN
Customer: C102 | Called on 04JAN2026 | Disputed amount: Rs 3,200 | Status: CLOSED
```

```sas
data work.disputes;
    infile datalines truncover;
    input @'Customer:'  cust_id      :$4.
          @'Called on'  call_date    :date9.
          @'Rs'         disputed_amt :comma10.
          @'Status:'    status       :$6.;
    format call_date date9. disputed_amt comma10.;
    datalines;
Customer: C101 | Called on 03JAN2026 | Disputed amount: Rs 12,500 | Status: OPEN
Customer: C102 | Called on 04JAN2026 | Disputed amount: Rs 3,200 | Status: CLOSED
;
run;
```

**Output**

| cust_id | call_date | disputed_amt | status |
| --- | --- | --- | --- |
| C101 | 03JAN2026 | 12,500 | OPEN |
| C102 | 04JAN2026 | 3,200 | CLOSED |

`@'Rs'` moves the pointer to just after the text `Rs`. The colon modifier then skips the space and
reads up to the next space. The search is case-sensitive.

**2. One record spread over several lines.** Use `#n` (go to line `n` of the record) or `/` (go to
the next line):

```sas
data work.cust_two_lines;
    input #1 cust_id $ name & $20.
          #2 city $ fico;
    datalines;
C101 Asha Rao
Mumbai 742
C102 Bilal Khan
Delhi 688
;
run;
```

Each observation uses two lines. `name & $20.` allows the single space in `Asha Rao`.

**3. Patterns with Perl regular expressions (industry gap).** When the text has no fixed markers,
search for a pattern. This finds Indian PAN numbers (5 letters, 4 digits, 1 letter) in free-text KYC
remarks:

```sas
data work.kyc_notes;
    infile datalines truncover;
    input remark $100.;
    datalines;
Customer submitted PAN ABCPK1234F with address proof
No document received
PAN on file: XYZAB9876Q verified by branch
;
run;

data work.pan_found;
    set work.kyc_notes;
    length pan $10;
    retain re;
    if _n_ = 1 then re = prxparse('/([A-Z]{5}[0-9]{4}[A-Z])/');
    if prxmatch(re, remark) then pan = prxposn(re, 1, remark);
    drop re;
run;
```

**Output**

| remark | pan |
| --- | --- |
| Customer submitted PAN ABCPK1234F with address proof | ABCPK1234F |
| No document received | (blank) |
| PAN on file: XYZAB9876Q verified by branch | XYZAB9876Q |

`PRXPARSE` compiles the pattern once (on the first row, then RETAIN keeps it). `PRXMATCH` returns the
position of the match (0 if none). The brackets in the pattern create capture group 1, and
`PRXPOSN(re, 1, remark)` returns the text that group matched.

### SQL Server and Pandas

| Task | SAS | SQL Server | Pandas |
| --- | --- | --- | --- |
| Header/detail records | Trailing `@` | Load to a staging table, then split with `CASE` / `WHERE` | `read_csv` then split by a type column |
| Many records per line | `@@` | `STRING_SPLIT` | `str.split().explode()` |
| Pattern extraction | `PRXMATCH`, `PRXPOSN` | `PATINDEX`, `LIKE` (no real regex) | `str.extract(r'...')` |

### 💼 Banking scenario

A legacy mainframe statement file mixes record types: `01` account header, `05` transaction, `99`
trailer with a control total. With a single trailing `@`, one DATA step reads the type code, sends each
record type to its own dataset, and compares the trailer's control total with the sum of the `05`
records. This is a standard **file reconciliation** pattern in banks.

### ⚠️ Common mistakes

- Forgetting the trailing `@`. The second INPUT reads the **next** line, so values come from the wrong
  record.
- Forgetting `@@` and losing most of the data without any error.
- Forgetting the colon modifier after a character pointer, so the leading space is read as part of the
  value.
- Writing a regular expression without RETAIN and recompiling it on every row (slow on big files).

### Exercises

1. **Level 1:** Read 6 customer/score pairs written on 2 lines using `@@`.
2. **Level 2:** Read a file with header and detail lines and attach the header date to every detail.
3. **Level 3:** Read a file where each customer uses 3 lines, using both `#n` and `/`.
4. **Level 4 — Interview:** "Explain @ vs @@ with an example."
5. **Level 5:** Extract every 10-digit mobile number from free-text complaint notes with PRX
   functions.

### ⭐ Interview questions

**Q. What is the difference between @ and @@?**
- *What they are testing:* the INPUT pointer and the DATA step loop.
- *Strong answer:* "Both hold the current input line so the next INPUT reads from it. A single `@`
  holds it only within the current iteration; it is released when the loop returns to the top. A
  double `@@` holds it across iterations, so you can read several observations from one line. I use
  `@` for record-type files and `@@` for many records per line."
- *Example:* the header/detail program above.
- *Weak answer:* "@ reads one value and @@ reads two."
- *Follow-up:* "What is the difference between `@15` and a trailing `@`?"

### Module wrap-up

- **I now know:** column pointer, character pointer, trailing @ and @@, line pointers, and PRX
  pattern matching.
- **I can now:** read mixed record-type files, many records per line, and semi-structured text.
- **Next:** Module 10 — PROC IMPORT and PROC EXPORT.

---

## MODULE 10 — PROC IMPORT and PROC EXPORT: TXT, CSV and Excel

**Syllabus items:** 1.17 Reading TXT file using PROC IMPORT · 1.18 Reading CSV file using PROC IMPORT ·
1.19 Reading Excel file using PROC IMPORT · 3.1 Reading and writing Excel files · 3.2 Reading and
writing Excel files with multiple sheets · 3.4 Reading and writing CSV files

**You will learn:** the quick way to load and save TXT, CSV and Excel files, and when the quick way is
not safe enough. **Why it matters:** business users send Excel files all the time. **Before you
start:** Module 8.

### 🧠 What it is

`PROC IMPORT` reads a file and **writes a DATA step for you**. It looks at the data to guess each
column's type and length. `PROC EXPORT` does the opposite.

| Approach | Good for | Risk |
| --- | --- | --- |
| `PROC IMPORT` | Quick loads, one-off analysis, files with clean headings | Guesses types and lengths. A guess can be wrong. |
| DATA step with `INFILE`/`INPUT` | Production jobs | More typing, but you control every column |

### Reading a CSV file (1.18, 3.4)

```sas
proc import datafile="C:\sasdata\raw\customers.csv"
            out=work.customers_imp
            dbms=csv
            replace;
    getnames=yes;          /* first row holds the column names */
    datarow=2;             /* data starts on row 2 */
    guessingrows=max;      /* look at every row before deciding types and lengths */
run;
```

| Statement | What it does |
| --- | --- |
| `datafile=` | The file to read |
| `out=` | The SAS dataset to create |
| `dbms=csv` | The file type |
| `replace` | Overwrite `out=` if it already exists |
| `getnames=yes` | Use the first row as variable names |
| `guessingrows=max` | Check all rows when guessing. The default is only the first 20 rows. |

⚠️ **Why GUESSINGROWS matters.** With the default of 20 rows, a city column whose first 20 values are
short (like `PUNE`) gets a short length, and `NAVI MUMBAI` on row 5,000 is cut off. A column of IDs
that looks numeric in the first 20 rows but has `A123` later is made numeric, and `A123` becomes
missing.

📌 **Useful trick:** for delimited files, PROC IMPORT writes the DATA step it generated into the Log.
Copy that code, fix the lengths and informats, and use it as your production program.

### Reading a TXT file (1.17)

```sas
/* tab-delimited text file */
proc import datafile="C:\sasdata\raw\branches.txt"
            out=work.branches dbms=tab replace;
    getnames=yes;
run;

/* pipe-delimited text file */
proc import datafile="C:\sasdata\raw\txn.txt"
            out=work.txn_pipe dbms=dlm replace;
    delimiter='|';
    getnames=yes;
    guessingrows=max;
run;
```

### Reading an Excel file (1.19, 3.1)

```sas
proc import datafile="C:\sasdata\raw\loan_book.xlsx"
            out=work.loan_book
            dbms=xlsx
            replace;
    sheet="Loans";             /* which sheet */
    getnames=yes;
run;

/* read only part of a sheet */
proc import datafile="C:\sasdata\raw\loan_book.xlsx"
            out=work.loan_top dbms=xlsx replace;
    range="Loans$A1:F500";
    getnames=yes;
run;
```

Reading Excel needs **SAS/ACCESS Interface to PC Files**. `DBMS=XLSX` does not need Microsoft Office
to be installed.

⚠️ Excel columns that mix numbers and text are usually read as **character**. Headings with spaces
become name literals if `VALIDVARNAME=ANY` (Module 4).

### Excel files with several sheets (3.2)

The cleanest way is the **XLSX library engine**: each sheet behaves like a dataset.

```sas
libname xl xlsx "C:\sasdata\raw\monthly_fraud.xlsx";

proc contents data=xl._all_ nods;      /* list the sheets */
run;

data work.fraud_q1;
    set xl.Jan xl.Feb xl.Mar;           /* stack three sheets */
run;

libname xl clear;                       /* release the file */
```

If a sheet name has a space, use a name literal: `xl.'Jan 2026'n` (with `options validmemname=extend;`).

**Writing several sheets into one workbook:**

```sas
libname out xlsx "C:\sasdata\out\branch_report.xlsx";

data out.Summary;  set work.branch_summary;  run;
data out.Detail;   set work.branch_detail;   run;

libname out clear;                      /* finish writing and release the file */
```

For formatted Excel reports (titles, colours, several tables on a sheet) use `ODS EXCEL` (Module 40).

### Writing CSV, TXT and Excel files with PROC EXPORT (3.1, 3.4)

```sas
/* CSV */
proc export data=work.big_txn
            outfile="C:\sasdata\out\big_txn.csv"
            dbms=csv replace;
    putnames=yes;
run;

/* pipe-delimited TXT */
proc export data=work.big_txn
            outfile="C:\sasdata\out\big_txn.txt"
            dbms=dlm replace;
    delimiter='|';
run;

/* Excel, one sheet */
proc export data=work.big_txn
            outfile="C:\sasdata\out\big_txn.xlsx"
            dbms=xlsx replace;
    sheet="Large Transactions";
run;
```

⚠️ PROC EXPORT writes the **formatted** values for CSV files. A date with `DATE9.` is written as
`02JAN2026`. Change the format first if the receiving system needs `2026-01-02`.

### SQL Server and Pandas

| Task | SAS | SQL Server | Pandas |
| --- | --- | --- | --- |
| Read CSV | `PROC IMPORT DBMS=CSV` | Import Flat File wizard, `BULK INSERT` | `pd.read_csv()` |
| Read Excel | `PROC IMPORT DBMS=XLSX` / `LIBNAME XLSX` | `OPENROWSET` with an ACE provider | `pd.read_excel(sheet_name=...)` |
| All sheets | `LIBNAME XLSX` | One import per sheet | `pd.read_excel(sheet_name=None)` |
| Write CSV | `PROC EXPORT DBMS=CSV` | `bcp` | `df.to_csv()` |
| Write many sheets | `LIBNAME XLSX` / `ODS EXCEL` | — | `pd.ExcelWriter` |

### 💼 Banking scenario

Every month, 30 branch managers send an Excel file of collection results. A program assigns
`LIBNAME XLSX` to each file, stacks the `Collections` sheet from all of them with one `SET` statement,
and records the source file name. A data-quality step then checks that every branch file arrived and
that every row has a valid account number before the numbers reach the collections dashboard.

### ⚠️ Common mistakes

- Trusting PROC IMPORT in production. A new file with a longer value or an odd row changes the
  guessed types, and the job breaks or quietly cuts values.
- Forgetting `REPLACE`. The import is skipped because the dataset exists, and you analyse old data.
- Leaving the Excel file open in Excel. SAS cannot read or write it.
- Not clearing an XLSX libref, so the file stays locked.

### Exercises

1. **Level 1:** Import a CSV with PROC IMPORT and check the variable lengths with PROC CONTENTS.
2. **Level 2:** Import the same CSV with `GUESSINGROWS=20` and `MAX`. Find a value that gets cut off.
3. **Level 3:** Read three sheets from one workbook with `LIBNAME XLSX` and stack them.
4. **Level 4 — Interview:** "When would you not use PROC IMPORT?"
5. **Level 5:** Export a summary and a detail table into two sheets of one workbook.

### ⭐ Interview questions

**Q. PROC IMPORT or a DATA step to read a CSV in production?**
- *Strong answer:* "A DATA step with INFILE and INPUT. PROC IMPORT guesses types and lengths from the
  data, so a new file can change the structure. In production I want fixed lengths, informats and
  validation. I often run PROC IMPORT once, copy the generated code from the Log, and harden it."
- *Follow-up:* "What does GUESSINGROWS do?"

### Module wrap-up

- **I now know:** PROC IMPORT and EXPORT for TXT, CSV and Excel, GUESSINGROWS, and the XLSX engine.
- **I can now:** load and save business files quickly and know when to use a DATA step instead.
- **Next:** Module 11 — Access, SQL Server and Oracle.

---

## MODULE 11 — Microsoft Access, SQL Server and Oracle

**Syllabus items:** 3.5 Reading and writing Access databases · 3.6 Reading from database servers such
as SQL Server · 3.7 Reading from Oracle database

**You will learn:** how SAS connects to databases, how to read and write tables, and how to make the
database do the heavy work. **Why it matters:** in a bank most data lives in SQL Server, Oracle or
Teradata. **Before you start:** Modules 4 and 10.

### 🧠 What it is

**SAS/ACCESS** products let SAS talk to databases. Once a database is connected through `LIBNAME`,
its tables look like SAS datasets. You can use them in DATA steps and procedures.

```text
Your SAS program ---> SAS/ACCESS engine ---> database driver ---> SQL Server / Oracle / Access
                       (translates SAS requests into the database's SQL where it can)
```

Two ways to send work to the database:

| Method | How | Who writes the SQL |
| --- | --- | --- |
| **Implicit pass-through** | Use a `LIBNAME` table in PROC SQL or a DATA step | SAS translates your code into database SQL **if it can** |
| **Explicit pass-through** | `CONNECT TO` ... `CONNECTION TO (...)` in PROC SQL | **You** write native database SQL. It runs exactly as written. |

🚀 The goal is always **pushdown**: let the database filter and summarise, and bring back only the
rows you need.

### Microsoft Access (3.5)

```sas
/* read an Access table */
proc import out=work.branch_master
            datatable="BranchMaster"
            dbms=access replace;
    database="C:\sasdata\raw\branches.accdb";
run;

/* write a SAS dataset into an Access database */
proc export data=work.branch_summary
            outtable="BranchSummary"
            dbms=access replace;
    database="C:\sasdata\out\reports.accdb";
run;

/* or connect the whole database as a library (Windows) */
libname acc access path="C:\sasdata\raw\branches.accdb";
proc print data=acc.BranchMaster(obs=5);
run;
libname acc clear;
```

⚠️ Access needs SAS/ACCESS to PC Files and Microsoft's Access driver. If SAS is 64-bit and Office is
32-bit, the direct connection fails; teams then use the **PC Files Server** (`DBMS=ACCESSCS`).

### SQL Server (3.6)

**Connect with a LIBNAME** (through ODBC, which most banks use):

```sas
libname dw odbc
    noprompt="Driver={ODBC Driver 17 for SQL Server};Server=sqlprod01;Database=BankDW;Trusted_Connection=yes;"
    schema=dbo;

/* tables now behave like SAS datasets */
proc contents data=dw.transactions;
run;
```

With the dedicated SQL Server engine the statement is similar:
`libname dw sqlsvr datasrc="BankDW" schema=dbo user=... password=...;`.

**Implicit pass-through:** write normal PROC SQL. SAS sends the filter and the grouping to SQL Server
when it can.

```sas
proc sql;
    create table work.jan_cust as
    select customer_id, count(*) as txn_count, sum(amount) as total_amount
    from dw.transactions
    where txn_date >= '01JAN2026'd and txn_date < '01FEB2026'd
    group by customer_id;
quit;
```

⚠️ This assumes `txn_date` is a SQL Server `DATE` column, which arrives in SAS as a SAS date. A
`DATETIME` column arrives as a SAS **datetime** (seconds, not days), so you would compare it with
`'01JAN2026:00:00:00'dt` instead. Check with `PROC CONTENTS` on the libref table first.

**See what SAS actually sent to the database:**

```sas
options sastrace=',,,d' sastraceloc=saslog nostsuffix;
```

The Log then shows the SQL that reached SQL Server. If the `WHERE` clause is missing from it, SAS
pulled every row and filtered locally, which is slow.

**Explicit pass-through:** write T-SQL yourself.

```sas
proc sql;
    connect to odbc as dwcon
        (noprompt="Driver={ODBC Driver 17 for SQL Server};Server=sqlprod01;Database=BankDW;Trusted_Connection=yes;");

    create table work.jan_cust as
    select * from connection to dwcon (
        SELECT customer_id,
               COUNT(*)    AS txn_count,
               SUM(amount) AS total_amount
        FROM dbo.transactions
        WHERE txn_date >= '2026-01-01' AND txn_date < '2026-02-01'
        GROUP BY customer_id
    );

    /* run a statement that returns no rows, such as a stored procedure */
    execute (EXEC dbo.usp_refresh_daily_scores @run_date = '2026-10-05') by dwcon;

    disconnect from dwcon;
quit;
```

| Part | Meaning |
| --- | --- |
| `connect to odbc as dwcon (...)` | Open a connection called `dwcon` |
| `select * from connection to dwcon ( ... )` | Everything inside the brackets is sent to SQL Server as written |
| `execute (...) by dwcon;` | Run a database statement that does not return rows (`EXEC`, `TRUNCATE`, `CREATE INDEX`) |
| `disconnect from dwcon;` | Close the connection |

📌 Inside `CONNECTION TO (...)` you write **SQL Server** syntax (`'2026-01-01'` dates, T-SQL
functions). Outside it you write **SAS** syntax (`'01JAN2026'd`).

**Writing results back to SQL Server:**

```sas
proc append base=dw.fraud_alerts data=work.alerts;
run;
```

For large loads, options such as `INSERTBUFF=` or `BULKLOAD=YES` on the libref or dataset make
inserts much faster.

### Oracle (3.7)

```sas
libname ora oracle user="&ora_user" password="&ora_pwd"
        path="RISKPRD" schema=CREDIT readbuff=5000;

proc sql;
    connect to oracle as oc (user="&ora_user" password="&ora_pwd" path="RISKPRD");
    create table work.dpd90 as
    select * from connection to oc (
        SELECT loan_id, customer_id, dpd, outstanding
        FROM credit.loan_daily
        WHERE as_of_date = DATE '2026-09-30'
          AND dpd > 90
    );
    disconnect from oc;
quit;
```

- `PATH=` is the Oracle connection name (TNS alias).
- `READBUFF=` fetches many rows per trip to the database, which speeds up large reads.
- Oracle stores unquoted names in uppercase, so `schema=CREDIT`.

### Keeping passwords out of programs

```sas
proc pwencode in='MyS3cretP@ss';
run;
```

The Log shows an encoded string such as `{SAS002}...`. Use that string as the password in your
code. This hides the password from casual reading. It is **not** strong encryption, so the better
production practice is an **authentication domain** set up by the SAS administrator
(`authdomain="OracleAuth"`), which keeps credentials out of code completely.

### SQL Server vs SAS vs Pandas

| Task | SAS | SQL Server | Pandas |
| --- | --- | --- | --- |
| Connect | `LIBNAME ... ODBC/ORACLE` | Connection in SSMS | `sqlalchemy.create_engine()` |
| Run native SQL | Explicit pass-through | Native | `pd.read_sql(sql, engine)` |
| Write a table | `PROC APPEND`, DATA step | `INSERT` | `df.to_sql()` |

### 💼 Banking scenario

The credit-risk team needs accounts more than 90 days past due from a 2-billion-row Oracle table. A
DATA step on the libref without a good WHERE clause would drag every row across the network. Explicit
pass-through sends one Oracle query, the database uses its partitions and indexes, and only about
80,000 rows come back to SAS.

### ⚠️ Common mistakes

- Using a SAS function that the database does not understand in a WHERE clause. SAS then cannot push
  the filter down and reads the whole table. Check with `SASTRACE`.
- Writing passwords in plain text in programs that are shared or saved in version control.
- Joining a SAS dataset to a huge database table in one query. SAS may pull the whole table to do the
  join. Upload the small table or use explicit pass-through.
- Forgetting that database names may be case-sensitive or uppercase (Oracle).

### Exercises

1. **Level 1:** Write a `LIBNAME` statement for a SQL Server database using a DSN.
2. **Level 2:** Write an explicit pass-through query that counts transactions per day in T-SQL.
3. **Level 3:** Turn on `SASTRACE`, run an implicit query, and check whether the WHERE clause was
   pushed down.
4. **Level 4 — Interview:** "What is the difference between implicit and explicit pass-through?"
5. **Level 5:** Design how you would pull 90+ DPD loans from Oracle every morning without moving the
   whole table.

### ⭐ Interview questions

**Q. Implicit vs explicit pass-through?**
- *What they are testing:* whether you can work efficiently with databases.
- *Strong answer:* "With implicit pass-through I query a LIBNAME table in PROC SQL and SAS tries to
  translate it into database SQL. With explicit pass-through I write native SQL inside CONNECTION TO,
  so it runs in the database exactly as written. For heavy filters, joins and aggregations on big
  tables I use explicit pass-through, or I check with SASTRACE that implicit pass-through really
  pushed the work down."
- *Weak answer:* "Explicit is when you connect."
- *Follow-up:* "How do you run a stored procedure in the database from SAS?" (`EXECUTE ... BY`.)

### Module wrap-up

- **I now know:** SAS/ACCESS, LIBNAME engines, implicit and explicit pass-through, SASTRACE and
  PWENCODE.
- **I can now:** read from and write to Access, SQL Server and Oracle efficiently and safely.
- **Next:** Module 12 — remote servers and Hadoop.

---

## MODULE 12 — Remote Servers and Hadoop: PROC DOWNLOAD, PROC UPLOAD and HDFS

**Syllabus items:** 3.8 PROC DOWNLOAD · 3.9 PROC UPLOAD · 3.10 HDFS connection

**You will learn:** how to run code on a remote SAS server, move data between your session and the
server, and connect to Hadoop. **Why it matters:** banks keep data on central servers and data lakes,
not on laptops. **Before you start:** Module 11.

### 🧠 SAS/CONNECT in plain words

**SAS/CONNECT** lets your SAS session (the **client**) send code to another SAS session (the
**server**) and move data between them.

```text
   YOUR SAS SESSION (client)                         SAS SERVER (remote)
   +-----------------------+   SIGNON / RSUBMIT     +-----------------------+
   | WORK library          |  ------------------->  | big risk datasets     |
   |                       |  <---- DOWNLOAD -----  |                       |
   |                       |  ----- UPLOAD ------>  |                       |
   +-----------------------+   SIGNOFF              +-----------------------+
```

| Statement | What it does |
| --- | --- |
| `SIGNON` | Connect to the remote SAS server |
| `RSUBMIT; ... ENDRSUBMIT;` | Run the code between them **on the server** |
| `PROC DOWNLOAD` | Copy data **from the server to your session** |
| `PROC UPLOAD` | Copy data **from your session to the server** |
| `SIGNOFF` | Disconnect |

📌 `PROC DOWNLOAD` and `PROC UPLOAD` are written **inside** an `RSUBMIT` block, because they run on the
server.

### PROC DOWNLOAD (3.8)

```sas
%let risksrv = riskserver.bank.local 7551;      /* server name and port */
signon risksrv username=_prompt_;               /* asks for your user ID and password */

rsubmit risksrv;
    libname riskmart "/sasdata/risk/mart";

    /* filter on the server first, so only the needed rows travel */
    data work.npa_2026;
        set riskmart.npa_accounts;
        where year(npa_date) = 2026;
    run;

    proc download data=work.npa_2026 out=work.npa_2026;
    run;
endrsubmit;

signoff risksrv;
```

- `data=` names the dataset **on the server** (in the server's WORK here).
- `out=` names the dataset **in your session**.
- To download several datasets: `proc download inlib=riskmart outlib=work; select a b; run;`.
- To download a file: `proc download infile='/sasdata/out/report.pdf' outfile='C:\reports\report.pdf'
  binary; run;`.

### PROC UPLOAD (3.9)

```sas
signon risksrv username=_prompt_;

rsubmit risksrv;
    libname riskmart "/sasdata/risk/mart";
    proc upload data=work.blocked_cards out=riskmart.blocked_cards;
    run;
endrsubmit;

signoff risksrv;
```

Here `data=` is the dataset **in your session** and `out=` is the dataset **on the server**.

🚀 **Process where the data lives.** Do not download 50 million rows to summarise them on your laptop.
Run the summary inside `RSUBMIT` and download only the result.

### HDFS and Hadoop connection (3.10)

**Hadoop** stores huge files across many machines. Its file system is **HDFS**. Tables on top of it
are usually read through **Hive**. SAS connects in three ways.

**1. Hive tables through SAS/ACCESS Interface to Hadoop**

```sas
libname hdp hadoop server="hive-prod.bank.local" port=10000 schema=fraud
        user="&hdp_user" password="&hdp_pwd";

proc sql;
    create table work.card_txn_day as
    select card_id, txn_ts, amount, merchant_id
    from hdp.card_txn
    where txn_dt = '2026-10-04';        /* filter pushed down to Hive where possible */
quit;
```

**2. HDFS commands with PROC HADOOP** (create folders, copy files in and out)

```sas
proc hadoop username="&hdp_user" password="&hdp_pwd" verbose;
    hdfs mkdir="/data/fraud/incoming";
    hdfs copyfromlocal="/sasdata/out/alerts.csv" out="/data/fraud/incoming/alerts.csv";
run;
```

**3. Reading an HDFS file directly with FILENAME HADOOP**

```sas
filename hdin hadoop "/data/fraud/incoming/alerts.csv" user="&hdp_user" pass="&hdp_pwd";

data work.alerts_back;
    infile hdin dlm=',' dsd firstobs=2 truncover;
    input card_id :$16. txn_ts :e8601dt19. amount;
    format txn_ts datetime20.;
run;
```

⚠️ These need your site's Hadoop setup: the SAS administrator sets the `SAS_HADOOP_JAR_PATH` and
`SAS_HADOOP_CONFIG_PATH` environment variables so SAS can find the Hadoop libraries and
configuration. If they are missing, the connection fails before any code runs.

**Today:** many banks are moving from Hadoop to cloud storage (Amazon S3, Azure Data Lake). SAS Viya
reads those through CAS libraries, and SAS 9.4 has procedures such as `PROC S3`. The idea is the same:
connect, push work to where the data is, and bring back only what you need.

### SQL Server and Pandas

| Task | SAS | SQL Server | Python |
| --- | --- | --- | --- |
| Run code on a server | `RSUBMIT` | Run the query on the server | Run the script on the server |
| Copy data down | `PROC DOWNLOAD` | Export / linked server | `pd.read_sql`, `scp` |
| Read Hive | `LIBNAME HADOOP` | PolyBase | `pyhive`, `pyspark` |

### 💼 Banking scenario

A fraud analyst works in Enterprise Guide on a laptop. The 6-month card history (900 million rows)
sits on the Hadoop cluster. The analyst sends one Hive query that summarises spend per card per day,
lands the 4-million-row result on the SAS server, and downloads only the 2,000 flagged cards for an
investigation report.

### ⚠️ Common mistakes

- Downloading huge datasets instead of summarising on the server first.
- Writing PROC DOWNLOAD outside `RSUBMIT`. It must run on the server.
- Mixing up `data=` and `out=` direction between DOWNLOAD and UPLOAD.
- Hard-coding passwords. Use prompts, encoded passwords or authentication domains.

### Exercises

1. **Level 1:** Explain what each of SIGNON, RSUBMIT, ENDRSUBMIT and SIGNOFF does.
2. **Level 2:** Write the code to download one dataset from a server's `riskmart` library.
3. **Level 3:** Change it so the summary runs on the server and only the summary is downloaded.
4. **Level 4 — Interview:** "How would you get data from Hadoop into SAS?"
5. **Level 5:** Upload a list of blocked cards to the server and use it there to filter a large
   table.

### ⭐ Interview questions

**Q. What is the difference between PROC DOWNLOAD and PROC UPLOAD?**
- *Strong answer:* "Both are SAS/CONNECT procedures that run inside RSUBMIT on the server. DOWNLOAD
  copies datasets or files from the server to my client session; UPLOAD copies from my session to the
  server. For performance I process on the server and move only results."

### Module wrap-up

- **I now know:** SAS/CONNECT, SIGNON, RSUBMIT, PROC DOWNLOAD and UPLOAD, and three ways to reach
  Hadoop.
- **I can now:** work with data on remote servers and data lakes without moving more than needed.
- **Next:** Part III — core DATA step processing.

**Part II checklist:** ✓ 1.12 · ✓ 1.17 · ✓ 1.18 · ✓ 1.19 · ✓ 3.1 · ✓ 3.2 · ✓ 3.3 · ✓ 3.4 · ✓ 3.5 · ✓ 3.6 · ✓ 3.7 ·
✓ 3.8 · ✓ 3.9 · ✓ 3.10 · ✓ 3.11 · ✓ 3.12 · ✓ 3.13

---

# Part III — Core DATA Step Processing (Modules 13–20)

Most examples in this Part use `work.txn` and `work.customers` from Module 5. Run that code first.

## MODULE 13 — Choosing Columns: KEEP, DROP and RENAME

**Syllabus items:** 2.3 KEEP as a statement and option · 2.4 DROP as a statement and option · 2.5
RENAME as a statement and option

**You will learn:** how to choose and rename columns, and the important difference between a
**statement** and a **dataset option**. **Why it matters:** reading only the columns you need is one
of the biggest speed-ups in SAS. The order in which these options run is a favourite interview
question. **Before you start:** Module 7.

### 🧠 Statement vs dataset option

| | Statement | Dataset option |
| --- | --- | --- |
| How it looks | `keep cust_id fico;` | `set work.customers(keep=cust_id fico);` |
| Where it goes | A separate statement inside the DATA step | In brackets right after a dataset name |
| What it affects | **Every output dataset** of the step | **Only the dataset it is attached to** |
| On an input dataset? | Not possible | Yes: controls what is **read into the PDV** |

```text
INPUT side                      PDV                         OUTPUT side
set ds(keep= drop= rename=)  -> variables available     ->  data out(keep= drop= rename=);
  controls what is READ          to your code               keep/drop/rename statements
                                                            control what is WRITTEN
```

### Example

```sas
data work.cust_slim (rename=(fico=fico_score));            /* output option */
    set work.customers (keep=cust_id name segment fico);    /* input option */
    if segment = 'R' then retail_flag = 1;
    else retail_flag = 0;
    drop segment;                                            /* statement: output only */
run;
```

**Output**

| cust_id | name | fico_score | retail_flag |
| --- | --- | --- | --- |
| C101 | Asha Rao | 742 | 1 |
| C102 | Bilal Khan | 688 | 0 |
| C103 | Chetan Iyer | 615 | 1 |
| C104 | Divya Menon | . | 0 |

**What happened**

| Step | Effect |
| --- | --- |
| `keep=` on the input | `city` was never read. The PDV holds `cust_id name segment fico`. |
| `if segment = 'R'` | Works, because `segment` **is** in the PDV. The DROP statement only affects output. |
| `drop segment;` | `segment` is not written to the output |
| `rename=` on the output | `fico` is written with the name `fico_score` |

### 🔥 The order SAS applies dataset options

On an input dataset, SAS applies **DROP= and KEEP= first, then RENAME=, then WHERE=**.

```sas
data work.good_scores;
    set work.customers (keep=cust_id fico             /* 1. use the OLD name here */
                        rename=(fico=score)           /* 2. rename */
                        where=(score > 650));         /* 3. use the NEW name here */
run;
```

**Output:** C101 (742) and C102 (688). C103 (615) fails the test. C104 is missing, and missing is not
greater than 650.

⚠️ Writing `keep=cust_id score` would fail with an error saying the variable `score` was never
referenced, because KEEP= runs before the rename, when `score` does not exist yet.

### The RENAME statement

With the `RENAME` statement, your code keeps using the **old** name. The new name only appears in the
output.

```sas
data work.cust_r;
    set work.customers;
    rename fico = fico_score;
    length score_band $4;
    if not missing(fico) and fico < 650 then score_band = 'LOW';     /* old name in code */
run;
```

### 🚀 Why this matters for speed

`set bank.transactions(keep=txn_id cust_id amount);` reads 3 columns instead of, say, 60. SAS moves
far less data from disk into the PDV. On a 100-million-row table this can cut run time a lot. A
`KEEP` **statement** would not help here, because it only acts on output; all 60 columns would still
be read.

### SQL Server, PROC SQL and Pandas

| Task | DATA step | PROC SQL / SQL Server | Pandas |
| --- | --- | --- | --- |
| Choose columns | `keep=` / `keep` | `SELECT cust_id, fico` | `df[["cust_id", "fico"]]` |
| Remove columns | `drop=` / `drop` | List only the others | `df.drop(columns=["city"])` |
| Rename | `rename=(fico=fico_score)` | `fico AS fico_score` | `df.rename(columns={"fico": "fico_score"})` |

### 💼 Banking scenario

A fraud scoring job needs 8 of the 140 columns in the card authorisation table. Adding
`keep=` to the `SET` statement cuts the nightly run from 50 minutes to 12, because SAS reads a fraction
of the data from disk.

### ⚠️ Common mistakes

- Using a KEEP **statement** and expecting it to speed up reading. Use the input dataset option.
- Using the new name in `KEEP=` on the same dataset as `RENAME=`.
- Dropping a variable on input with `drop=` and then using it in the code. It is uninitialized:
  `NOTE: Variable segment is uninitialized.`
- Expecting the RENAME statement to let you use the new name in your code.

### Exercises

1. **Level 1:** Create a dataset with only `txn_id` and `amount` from `work.txn`, two ways.
2. **Level 2:** Rename `amount` to `txn_amount` on output and filter `txn_amount > 10000` in the same
   step.
3. **Level 3:** Read only 3 columns from a dataset, create two outputs that keep different columns.
4. **Level 4 — Interview:** "In what order are KEEP=, RENAME= and WHERE= applied on an input dataset?"
5. **Level 5:** Measure the run time of a DATA step on a wide table with and without `keep=` on
   input (`options fullstimer;` shows detailed timings).

### ⭐ Interview questions

**Q1. What is the difference between the KEEP statement and the KEEP= option?**
- *Strong answer:* "The statement affects all output datasets. The option affects only the dataset it
  is attached to. On an input dataset, KEEP= also limits what is read into the PDV, which saves I/O.
  The statement cannot do that."
- *Follow-up:* "Can you use a dropped variable in your code?"

**Q2. In what order are dataset options processed?**
- *Strong answer:* "On input: DROP= and KEEP= first, then RENAME=, then WHERE=. So KEEP= uses old names
  and WHERE= uses new names."

### Module wrap-up

- **I now know:** KEEP, DROP and RENAME as statements and options, and their processing order.
- **I can now:** read only the columns I need and rename safely.
- **Next:** Module 14 — choosing rows with WHERE.

---

## MODULE 14 — Choosing Rows: WHERE and Its Operators

**Syllabus items:** 2.6 WHERE as a statement and option · 2.7 WHERE statement with operators and
operands

**You will learn:** every way to filter rows with WHERE and all its operators. **Why it matters:**
WHERE is the fastest way to filter in SAS, and it works in both DATA steps and procedures. **Before you
start:** Module 13.

### 🧠 What it is

`WHERE` keeps only the rows that meet a condition. It tests each row **before** the row enters the
PDV, so rows that fail are never read into the step.

| Form | Example | Applies to |
| --- | --- | --- |
| WHERE **statement** in a DATA step | `where amount > 10000;` | Every dataset in the SET/MERGE statement |
| WHERE= **dataset option** | `set work.txn(where=(amount > 10000));` | Only that dataset |
| WHERE statement in a **PROC** | `proc print data=work.txn; where channel = 'ATM'; run;` | The procedure's input |

⚠️ WHERE works only on data read from **SAS datasets or database tables**. It cannot be used with
`INPUT` (raw files), and it cannot see variables you create inside the step.

### Operators and operands (2.7)

An **operand** is a value or variable being tested (`amount`, `10000`, `'ATM'`). An **operator** is
what tests it (`>`, `IN`, `LIKE`).

| Operator | Meaning | Example |
| --- | --- | --- |
| `=` or `EQ` | equal | `where channel = 'ATM';` |
| `^=`, `~=` or `NE` | not equal | `where channel ne 'ATM';` |
| `>` `GT`, `<` `LT`, `>=` `GE`, `<=` `LE` | comparisons | `where amount >= 50000;` |
| `AND`, `OR`, `NOT` | combine conditions | `where channel = 'ONLINE' and amount > 50000;` |
| `IN` | in a list | `where channel in ('ATM', 'POS');` |
| `BETWEEN a AND b` | in a range, ends included | `where amount between 5000 and 80000;` |
| `CONTAINS` or `?` | contains this text | `where name contains 'Khan';` |
| `LIKE` | pattern: `%` any text, `_` one character | `where name like 'A%';` |
| `IS MISSING` / `IS NULL` | missing value | `where amount is missing;` |
| `=*` | sounds like (rough spelling match) | `where name =* 'Asha Rau';` |
| `SAME AND` / `WHERE ALSO` | add a condition to an existing WHERE | `where also amount > 0;` |

You can also use arithmetic and SAS functions: `where year(txn_date) = 2026 and amount * 1.18 > 10000;`

📌 `CONTAINS`, `LIKE`, `BETWEEN` and `IS MISSING` work only in WHERE. They are **not** allowed in an IF
statement.

### Examples on `work.txn`

| WHERE condition | Rows kept | Why |
| --- | --- | --- |
| `channel in ('ATM', 'POS')` | T001, T003, T005 | Only those channels |
| `amount between 5000 and 80000` | T001, T005, T006 | 5,000, 20,000 and 78,000 are in range (ends included). T004 is missing. |
| `amount is missing` | T004 | |
| `channel = 'ONLINE' and amount > 50000` | T002, T006 | Both conditions true |
| `txn_date between '01JAN2026'd and '05JAN2026'd` | T001, T002, T003 | Dates are numbers, so ranges work |
| `upcase(channel) = 'ONLINE'` | T002, T004, T006 | Safe if the data's case is mixed |

**A complete example**

```sas
data work.big_online;
    set work.txn;
    where channel = 'ONLINE' and amount > 50000;
run;

proc print data=work.txn noobs;          /* WHERE inside a procedure */
    where amount is missing;
run;
```

### Two WHERE statements: the second replaces the first

```sas
data work.test;
    set work.txn;
    where channel = 'ONLINE';
    where amount > 50000;          /* replaces the line above */
run;
```

The Log says `NOTE: WHERE clause has been replaced.` and the result has every row with amount over
50,000 from **any** channel. To add a condition instead, write `where also amount > 50000;` (or
combine them with `AND`).

### 🧠 Why WHERE is fast

1. Rows that fail never enter the PDV, so less work is done per row.
2. If the dataset has an **index** on the WHERE variable, SAS can jump straight to matching rows
   instead of reading everything (Module 32).
3. For database tables, SAS can send the WHERE to the database (Module 11).

### SQL Server, PROC SQL and Pandas

```sql
-- SQL Server
SELECT * FROM dbo.txn WHERE channel = 'ONLINE' AND amount > 50000;
```

```sas
/* PROC SQL: the same WHERE syntax as SQL */
proc sql;
    select * from work.txn where channel = 'ONLINE' and amount > 50000;
quit;
```

```python
# Pandas
txn[(txn["channel"] == "ONLINE") & (txn["amount"] > 50000)]
txn.query("channel == 'ONLINE' and amount > 50000")
```

⚠️ Difference: in SQL Server, `NULL > 50000` is unknown, so the row is dropped. In SAS, a missing
value is lower than any number, so `amount < 100` would **keep** missing amounts. In Pandas, `NaN <
100` is `False`. Always handle missing values explicitly.

### 💼 Banking scenario

An AML (anti-money laundering) team must review cash deposits between ₹9 lakh and ₹10 lakh, because
people sometimes split cash to stay below a ₹10 lakh reporting limit:

```sas
data work.possible_structuring;
    set bank.transactions (keep=txn_id cust_id txn_date txn_type channel amount);
    where txn_type = 'CASH DEPOSIT'
      and amount between 900000 and 999999
      and txn_date >= intnx('month', today(), -3, 'b');
run;
```

### ⚠️ Common mistakes

- Using WHERE on a variable you create in the same step:
  `ERROR: Variable gst is not on file WORK.TXN.`
- Using WHERE with raw data from INPUT: `ERROR: No input data sets available for WHERE statement.`
- Writing two WHERE statements and losing the first condition.
- Case problems: `'online'` does not equal `'ONLINE'`. Use `upcase()`.
- Forgetting that `BETWEEN` includes both ends.

### Exercises

1. **Level 1:** Keep transactions from the POS and ATM channels.
2. **Level 2:** Keep customers whose name starts with `B` or contains `Rao`.
3. **Level 3:** Use a WHERE= option on one dataset and a WHERE statement on another in two steps, and
   explain the difference.
4. **Level 4 — Interview:** "Name four operators that work in WHERE but not in IF."
5. **Level 5:** Write the AML structuring filter for the last 6 months and print the result with
   PROC PRINT using a WHERE statement inside the procedure.

### ⭐ Interview questions

**Q. Which WHERE operators can't you use in an IF statement?**
- *Strong answer:* "CONTAINS (or ?), LIKE, BETWEEN-AND, IS MISSING / IS NULL, sounds-like `=*`, and
  SAME AND. In IF, I use functions instead: `index()` or `find()` for contains, and `missing()`."
- *Follow-up:* "Why is WHERE usually faster than IF?"

### Module wrap-up

- **I now know:** WHERE statement vs option, every WHERE operator, and why WHERE is fast.
- **I can now:** filter any dataset precisely in DATA steps and procedures.
- **Next:** Module 15 — IF-THEN logic.

---

## MODULE 15 — Conditional Logic: IF-THEN, ELSE and DO Blocks

**Syllabus items:** 2.12 IF THEN statement · 2.13 IF THEN DO statement

**You will learn:** how to make decisions in the DATA step, run several statements per decision, and
write clean multi-way logic with SELECT. **Why it matters:** business rules (risk bands, fees,
flags) are all conditional logic. **Before you start:** Module 7.

### IF-THEN and ELSE (2.12)

```sas
data work.cust_risk;
    set work.customers;
    length risk_band $8;
    if missing(fico)     then risk_band = 'NO SCORE';
    else if fico >= 750  then risk_band = 'LOW';
    else if fico >= 650  then risk_band = 'MEDIUM';
    else                      risk_band = 'HIGH';
run;
```

**Output**

| cust_id | fico | risk_band |
| --- | --- | --- |
| C101 | 742 | MEDIUM |
| C102 | 688 | MEDIUM |
| C103 | 615 | HIGH |
| C104 | . | NO SCORE |

**Why missing is checked first:** a missing FICO is lower than every number. Without the first line,
C104 would fall to the last `else` and be labelled `HIGH`.

**Why `LENGTH` is there:** without it, the first value SAS sees (`'NO SCORE'`, 8 characters) would set
the length, which happens to be fine here. But if you later reorder the conditions so `'LOW'` comes
first, every longer value would be cut to 3 characters (Module 7).

### IF-THEN-DO (2.13)

Use `DO; ... END;` when one decision needs several statements.

```sas
data work.cust_actions;
    set work.cust_risk;
    length action $20;
    if risk_band = 'HIGH' then do;
        credit_limit = 25000;
        action = 'MANUAL REVIEW';
    end;
    else if risk_band = 'NO SCORE' then do;
        credit_limit = 0;
        action = 'GET BUREAU REPORT';
    end;
    else do;
        credit_limit = 100000;
        action = 'AUTO APPROVE';
    end;
run;
```

**Output**

| cust_id | risk_band | credit_limit | action |
| --- | --- | --- | --- |
| C101 | MEDIUM | 100000 | AUTO APPROVE |
| C102 | MEDIUM | 100000 | AUTO APPROVE |
| C103 | HIGH | 25000 | MANUAL REVIEW |
| C104 | NO SCORE | 0 | GET BUREAU REPORT |

### SELECT-WHEN: a cleaner way to write long chains (industry gap)

```sas
data work.cust_risk2;
    set work.customers;
    length risk_band $8;
    select;
        when (missing(fico)) risk_band = 'NO SCORE';
        when (fico >= 750)   risk_band = 'LOW';
        when (fico >= 650)   risk_band = 'MEDIUM';
        otherwise            risk_band = 'HIGH';
    end;
run;

/* SELECT on one variable's value */
data work.cust_seg;
    set work.customers;
    length segment_name $12;
    select (segment);
        when ('R')  segment_name = 'Retail';
        when ('C')  segment_name = 'Corporate';
        when ('S')  segment_name = 'SME';
        otherwise   segment_name = 'Unknown';
    end;
run;
```

⚠️ If no WHEN matches and there is no OTHERWISE, the step stops with
`ERROR: Unsatisfied WHEN clause and no OTHERWISE statement.` Always include OTHERWISE.

### Subsetting IF and DELETE

An `IF` with no `THEN` is a **subsetting IF**. It keeps the row only if the condition is true.

```sas
data work.online_only;
    set work.txn;
    if channel = 'ONLINE';          /* keep only ONLINE rows */
run;

data work.no_missing;
    set work.txn;
    if missing(amount) then delete; /* the same idea, written the other way round */
run;
```

When the condition is false, SAS stops processing that row and returns to the top of the loop. The
row is not written.

### Rules for conditions

- Text comparisons are **case-sensitive**: `'Atm'` is not `'ATM'`.
- Trailing blanks are ignored in comparisons: `'ATM'` equals `'ATM   '`.
- A number counts as **true** if it is not 0 and not missing. So `if review_flag then ...` works for a
  0/1 flag.
- `IN` works in IF too: `if channel in ('ATM', 'POS') then ...`.

### SQL Server, PROC SQL and Pandas

```sql
-- SQL Server / PROC SQL
CASE WHEN fico IS NULL THEN 'NO SCORE'
     WHEN fico >= 750  THEN 'LOW'
     WHEN fico >= 650  THEN 'MEDIUM'
     ELSE 'HIGH' END AS risk_band
```

```python
# Pandas
import numpy as np
conditions = [df["fico"].isna(), df["fico"] >= 750, df["fico"] >= 650]
df["risk_band"] = np.select(conditions, ["NO SCORE", "LOW", "MEDIUM"], default="HIGH")
```

### 💼 Banking scenario: tiered transaction fees

```sas
data work.txn_fees;
    set work.txn;
    length fee_rule $15;
    if missing(amount) then do;
        fee = .;  fee_rule = 'NO AMOUNT';
    end;
    else if channel = 'ATM' and amount > 10000 then do;
        fee = 20;  fee_rule = 'ATM HIGH VALUE';
    end;
    else if channel = 'ONLINE' then do;
        fee = round(amount * 0.001, 0.01);  fee_rule = 'ONLINE 0.1%';
    end;
    else do;
        fee = 0;  fee_rule = 'FREE';
    end;
run;
```

### ⚠️ Common mistakes

- Not handling missing values first.
- Truncated text because the first assignment was short.
- Forgetting `END;` after `DO;`. The Log reports `ERROR 117-185: There was 1 unclosed DO block.`
- Writing `else if` conditions in the wrong order, so a broad test catches everything before a
  narrower one is checked.

### Exercises

1. **Level 1:** Flag transactions over 50,000 as `LARGE` and others as `NORMAL`.
2. **Level 2:** Rewrite the risk-band logic with SELECT-WHEN.
3. **Level 3:** Create three variables in one IF-THEN-DO block based on the channel.
4. **Level 4 — Interview:** "What is a subsetting IF?"
5. **Level 5:** Build a fee engine with five rules, handle missing values, and prove each rule fires
   with a test dataset.

### ⭐ Interview questions

**Q. What happens in `if fico < 650 then band = 'HIGH';` when FICO is missing?**
- *What they are testing:* the missing-value trap.
- *Strong answer:* "The condition is true, because a missing number is lower than any value, so the
  customer is wrongly banded HIGH. I check `missing(fico)` first or add `not missing(fico)`."

### Module wrap-up

- **I now know:** IF-THEN, ELSE IF, IF-THEN-DO, SELECT-WHEN, subsetting IF and DELETE.
- **I can now:** write business rules safely, including missing values.
- **Next:** Module 16 — IF vs WHERE.

---

## MODULE 16 — IF vs WHERE

**Syllabus items:** 2.18 Difference between IF and WHERE

**You will learn:** exactly when IF and WHERE give different results, and which to use. **Why it
matters:** ⭐ this is one of the most asked SAS interview questions. **Before you start:** Modules 7,
14 and 15.

### 🧠 The key idea

```text
              WHERE checks here                         IF checks here
                    |                                         |
  dataset --> [ row passes? ] --> PDV --> your statements --> [ row passes? ] --> output
                    |                                         |
           failing rows never enter                  failing rows were read,
           the PDV (less work)                       then thrown away
```

### Comparison table

| | WHERE | Subsetting IF |
| --- | --- | --- |
| When it tests | **Before** the row enters the PDV | **After** the row is in the PDV |
| Can use variables created in the step | ✗ No | ✓ Yes |
| Can use `_N_`, `FIRST.`/`LAST.`, `IN=` | ✗ No | ✓ Yes |
| Works with raw data (INPUT) | ✗ No | ✓ Yes |
| Works inside procedures (PROC PRINT, MEANS) | ✓ Yes | ✗ No |
| Special operators (LIKE, CONTAINS, BETWEEN, IS MISSING) | ✓ Yes | ✗ No |
| Can use an index | ✓ Yes | ✗ No |
| Speed | Faster | Slower |
| With `OBS=` | `OBS=` counts rows **after** the WHERE | `OBS=` counts rows **before** the IF |
| With MERGE | Filters each input **before** the join | Filters the joined row **after** the join |

### Proof 1: new variables

```sas
data work.test;
    set work.txn;
    gst = amount * 0.18;
    where gst > 1000;       /* ERROR: Variable gst is not on file WORK.TXN. */
run;
```

```sas
data work.test;
    set work.txn;
    gst = amount * 0.18;
    if gst > 1000;          /* works */
run;
```

### Proof 2: the same filter, different answers with OBS=

```sas
data work.w;  set work.txn(obs=3);  where channel = 'ONLINE';  run;
data work.i;  set work.txn(obs=3);  if channel = 'ONLINE';     run;
```

| Program | Rows | Why |
| --- | --- | --- |
| WHERE | T002, T004, T006 (3 rows) | WHERE runs first, then `OBS=3` takes the first 3 **matching** rows |
| IF | T002 (1 row) | `OBS=3` reads T001, T002, T003 first; IF keeps only T002 from those |

### Proof 3: MERGE

With MERGE (Module 33), a WHERE filters each input dataset **before** the rows are matched. A
subsetting IF filters the **combined** row afterwards. If you filter accounts to "active" with WHERE=
on the accounts dataset, customers without an active account still appear (with blank account data).
If you filter with IF after the merge, those customers disappear. Choose based on the business
question.

### Which should you use?

- Use **WHERE** when the condition uses variables that already exist in the input. It is faster.
- Use **IF** when the condition uses a variable you create, `_N_`, `FIRST.`/`LAST.`, `IN=` flags, or
  raw data from INPUT.

### SQL and Pandas

- In SQL, `WHERE` filters rows before grouping, and `HAVING` filters after grouping. That is a
  different pair (Module 29), but the idea "filter early vs filter late" is similar.
- In Pandas there is only one kind of filter: a boolean mask on the DataFrame.

### ⭐ Interview questions

**Q. What is the difference between WHERE and IF?**
- *What they are testing:* PDV understanding, not memorised rules.
- *Strong answer:* "WHERE filters before the observation enters the PDV, so it is faster and can use
  indexes, but it can only see variables that already exist in the input datasets. The subsetting IF
  runs after the row is in the PDV, so it can use new variables, `_N_`, FIRST./LAST. and IN= flags,
  and it works with INPUT. WHERE also works in procedures and supports LIKE, CONTAINS, BETWEEN and IS
  MISSING."
- *Example:* the OBS= proof above.
- *Weak answer:* "WHERE is for datasets and IF is for conditions."
- *Follow-up:* "With MERGE, which one would you use to keep only matched rows, and why?" (IF with IN=
  flags — WHERE cannot see IN= variables.)

### Exercises

1. **Level 1:** Write one filter both ways and confirm the same result.
2. **Level 2:** Write a filter that **must** use IF and explain why.
3. **Level 3:** Show a case where WHERE and IF give different results with `OBS=`.
4. **Level 4 — Interview:** Explain IF vs WHERE using the PDV, in under one minute.
5. **Level 5:** On a large dataset, time WHERE vs IF for the same condition (`options fullstimer;`).

### Module wrap-up

- **I now know:** where WHERE and IF act in the DATA step, and when their results differ.
- **I can now:** choose the right filter and explain the choice in an interview.
- **Next:** Module 17 — creating several datasets in one step.

---

## MODULE 17 — Writing Several Datasets in One Step

**Syllabus items:** 2.14 Creating multiple datasets from an existing dataset

**You will learn:** how one DATA step can write many datasets with the OUTPUT statement. **Why it
matters:** you read the big input only once, which saves time. **Before you start:** Modules 7 and
15.

### 🧠 What it is

List several dataset names on the `DATA` statement. Then use `OUTPUT dataset-name;` to send each row
where it belongs.

📌 As soon as a DATA step contains **any** OUTPUT statement, the hidden OUTPUT at the end is switched
off. Rows are written only where you say.

### Example

```sas
data work.txn_high   (keep=txn_id cust_id amount)
     work.txn_normal
     work.txn_bad     (keep=txn_id cust_id);
    set work.txn;
    if missing(amount)       then output work.txn_bad;
    else if amount >= 50000  then output work.txn_high;
    else                          output work.txn_normal;
run;
```

**Log**

```text
NOTE: There were 6 observations read from the data set WORK.TXN.
NOTE: The data set WORK.TXN_HIGH has 2 observations and 3 variables.
NOTE: The data set WORK.TXN_NORMAL has 3 observations and 5 variables.
NOTE: The data set WORK.TXN_BAD has 1 observations and 2 variables.
```

| Dataset | Rows | Why |
| --- | --- | --- |
| `txn_high` | T002, T006 | Amount at least 50,000 |
| `txn_normal` | T001, T003, T005 | Amount below 50,000 |
| `txn_bad` | T004 | Amount missing |

📌 Each output dataset can have its own `KEEP=` or `DROP=` option.

### A row can go to more than one dataset

```sas
data work.all_online work.all_large;
    set work.txn;
    if channel = 'ONLINE' then output work.all_online;
    if amount >= 50000    then output work.all_large;    /* not ELSE: a row can go to both */
run;
```

T002 and T006 go to **both** datasets.

### ⚠️ Without OUTPUT statements, every row goes everywhere

```sas
data work.a work.b;
    set work.txn;
run;
/* both work.a and work.b get all 6 rows */
```

### SQL Server, PROC SQL and Pandas

```sql
-- SQL Server needs one query (and one scan of the table) per output
SELECT * INTO dbo.txn_high   FROM dbo.txn WHERE amount >= 50000;
SELECT * INTO dbo.txn_normal FROM dbo.txn WHERE amount < 50000;
```

```python
high = txn[txn["amount"] >= 50000]
normal = txn[txn["amount"] < 50000]
bad = txn[txn["amount"].isna()]
```

🚀 SAS writes all outputs in **one pass** over the input. With a 50 GB table, that is one read instead
of three.

### 💼 Banking scenario

A nightly data-quality step reads the day's transactions once and writes three datasets: `clean`
(passes all checks), `rejects` (missing account or negative amount) and `review` (passes checks but
over ₹10 lakh). Rejects go back to the source team; the review set goes to the AML queue.

### ⚠️ Common mistakes

- Expecting the hidden OUTPUT to still work after adding an OUTPUT statement.
- Using `else` where a row should be allowed into two outputs, or forgetting `else` where it should
  go to only one.
- Writing `output txn_high;` when the DATA statement says `work.txn_high` (both work, because WORK is
  the default library; be consistent).

### Exercises

1. **Level 1:** Split `work.txn` into one dataset per channel.
2. **Level 2:** Give each output dataset different KEEP= options.
3. **Level 3:** Write each row twice to the same dataset with a variable showing "copy 1" or "copy 2".
4. **Level 4 — Interview:** "What happens to implicit output when you use an OUTPUT statement?"
5. **Level 5:** Build the clean/rejects/review split with at least four validation rules.

### ⭐ Interview questions

**Q. How do you create several datasets from one in a single step?**
- *Strong answer:* "List them on the DATA statement and use `OUTPUT dataset;` in IF-THEN logic. Any
  OUTPUT statement turns off the implicit output, so rows go only where I send them. Each dataset can
  have its own KEEP= or DROP=. It reads the input once, which is efficient."

### Module wrap-up

- **I now know:** multiple datasets on the DATA statement, the OUTPUT statement, and implicit output.
- **I can now:** route rows into several datasets in one efficient pass.
- **Next:** Module 18 — sorting and duplicates.

---

## MODULE 18 — Sorting and Removing Duplicates

**Syllabus items:** 2.8 Sorting datasets · 2.9 Removing duplicates using PROC SORT

**You will learn:** PROC SORT, descending order, and every way PROC SORT can remove or separate
duplicates. **Why it matters:** BY-group processing, MERGE and FIRST./LAST. all need sorted data, and
duplicate handling is a daily data-quality task. **Before you start:** Module 5.

### Sorting (2.8)

```sas
proc sort data=work.txn out=work.txn_sorted;
    by cust_id descending txn_date;
run;
```

**Output**

| txn_id | cust_id | txn_date | channel | amount |
| --- | --- | --- | --- | --- |
| T006 | C101 | 12JAN2026 | ONLINE | 78,000 |
| T003 | C101 | 05JAN2026 | POS | 2,300 |
| T001 | C101 | 02JAN2026 | ATM | 5,000 |
| T005 | C102 | 09JAN2026 | ATM | 20,000 |
| T002 | C102 | 02JAN2026 | ONLINE | 125,000 |
| T004 | C103 | 07JAN2026 | ONLINE | . |

| Part | Meaning |
| --- | --- |
| `data=` | The dataset to sort |
| `out=` | Where to write the sorted copy. **Without `OUT=`, the original dataset is replaced.** |
| `by cust_id descending txn_date;` | Sort by customer (A to Z), then newest date first within each customer |

📌 `DESCENDING` goes **before** the variable it applies to, and it applies only to that one variable.

📌 Missing values sort **first** in ascending order (they are the lowest values).

**Case-insensitive sorting:** normally uppercase letters sort before lowercase. To sort names the way
a person reads them:

```sas
proc sort data=work.customers out=work.cust_by_name sortseq=linguistic(strength=primary);
    by name;
run;
```

### Removing duplicates (2.9)

| Option | What it removes | Typical use |
| --- | --- | --- |
| `NODUPKEY` | Every row after the first for each **BY value** | One row per customer |
| `NODUPRECS` (or `NODUP`) | A row that is **identical in every variable** to the row before it | Exact duplicate rows |
| `DUPOUT=` | Saves the removed rows in a dataset | Audit trail |
| `NOUNIQUEKEY` | Rows whose BY value appears **only once** | Find keys that repeat |
| `UNIQUEOUT=` | Saves the rows removed by NOUNIQUEKEY | |

**Keep the latest transaction per customer** (a classic interview task):

```sas
proc sort data=work.txn out=work.txn_sorted;
    by cust_id descending txn_date;
run;

proc sort data=work.txn_sorted out=work.latest_txn nodupkey dupout=work.older_txn;
    by cust_id;
run;
```

**Log:** `NOTE: 3 observations with duplicate key values were deleted.`

| `work.latest_txn` | `work.older_txn` |
| --- | --- |
| T006 (C101, 12JAN2026) | T003 (C101) |
| T005 (C102, 09JAN2026) | T001 (C101) |
| T004 (C103, 07JAN2026) | T002 (C102) |

**Why it works:** after the first sort, the newest transaction is the **first** row for each customer.
`NODUPKEY` keeps the first row of each BY group. PROC SORT keeps rows with equal keys in their original
order (the `EQUALS` option, on by default), so the result is predictable.

### ⚠️ The NODUPRECS trap

`NODUPRECS` only compares a row with the row **directly before it**. Duplicates that are not next to
each other after sorting are missed.

```sas
data work.dup_demo;
    input cust_id $ product $ balance;
    datalines;
C101 SAVINGS 5000
C101 LOAN 90000
C101 SAVINGS 5000
;
run;

proc sort data=work.dup_demo out=work.try1 noduprecs;
    by cust_id;          /* the two SAVINGS rows are not next to each other */
run;                     /* result: 3 rows - nothing removed! */

proc sort data=work.dup_demo out=work.try2 noduprecs;
    by _all_;            /* sort by every variable, so identical rows are adjacent */
run;                     /* result: 2 rows */
```

📌 To remove exact duplicates reliably, sort `BY _ALL_` with `NODUPRECS` (or use `NODUPKEY` with
`BY _ALL_`).

**Find customers who appear more than once:**

```sas
proc sort data=work.txn out=work.repeat_cust nouniquekey uniqueout=work.single_cust;
    by cust_id;
run;
/* repeat_cust: 5 rows for C101 and C102.  single_cust: 1 row for C103. */
```

### SQL Server, PROC SQL and Pandas

| Task | PROC SORT | SQL Server | Pandas |
| --- | --- | --- | --- |
| Sort | `by cust_id descending txn_date;` | `ORDER BY cust_id, txn_date DESC` | `sort_values(["cust_id", "txn_date"], ascending=[True, False])` |
| Latest per key | Sort, then `NODUPKEY` | `ROW_NUMBER() OVER (PARTITION BY cust_id ORDER BY txn_date DESC) = 1` | `sort_values(...).drop_duplicates("cust_id")` |
| Exact duplicates | `NODUPRECS` with `BY _ALL_` | `SELECT DISTINCT *` | `drop_duplicates()` |
| Keys that repeat | `NOUNIQUEKEY` | `GROUP BY cust_id HAVING COUNT(*) > 1` | `df[df.duplicated("cust_id", keep=False)]` |

```sql
-- SQL Server: latest transaction per customer
WITH ranked AS (
    SELECT *, ROW_NUMBER() OVER (PARTITION BY cust_id ORDER BY txn_date DESC) AS rn
    FROM dbo.txn
)
SELECT * FROM ranked WHERE rn = 1;
```

### 🚀 Sorting is expensive

Sorting a big dataset reads it, writes temporary files, and writes it again. Ways to avoid or reduce
sorts:

- Use `CLASS` instead of `BY` in PROC MEANS and PROC SUMMARY (no sort needed, Module 41).
- Sort once and keep the dataset sorted. SAS records the sort order (`Sorted by` in PROC CONTENTS)
  and skips a repeat sort with the same BY variables.
- Use `TAGSORT` for very wide datasets with short keys (sorts only the keys, uses less temporary
  space).
- Drop unneeded columns while sorting: `proc sort data=big(keep=...) out=...`.
- For lookups, use a hash object instead of sort + merge (Module 33).

### 💼 Banking scenario

A KYC refresh file contains several address updates for some customers on the same day. The
customer master must hold only the newest one. Sort by `customer_id` and `descending update_ts`, keep
the first row with `NODUPKEY`, and send the older rows to `DUPOUT=` for the audit log.

### ⚠️ Common mistakes

- Forgetting `OUT=` and overwriting the source dataset.
- Using `NODUPKEY` without sorting the right way first, so a random row (not the latest) is kept.
- Expecting `NODUPRECS` to remove all exact duplicates without sorting `BY _ALL_`.
- Sorting the same big dataset many times in one program.

### Exercises

1. **Level 1:** Sort `work.txn` by amount, largest first.
2. **Level 2:** Keep the **earliest** transaction per customer and save the others with `DUPOUT=`.
3. **Level 3:** Build a dataset with non-adjacent exact duplicates and remove them correctly.
4. **Level 4 — Interview:** "What is the difference between NODUPKEY and NODUPRECS?"
5. **Level 5:** For a customer master with repeated IDs, produce: the latest row per customer, the
   removed rows, and a list of IDs that appeared more than twice.

### ⭐ Interview questions

**Q1. NODUPKEY vs NODUPRECS?**
- *What they are testing:* a classic trap.
- *Strong answer:* "NODUPKEY removes rows with a duplicate BY value, keeping the first one in each BY
  group. NODUPRECS removes a row only if it is identical in all variables to the previous row in the
  sorted output, so non-adjacent duplicates can survive unless I sort BY _ALL_."
- *Weak answer:* "NODUPKEY is for keys and NODUPRECS is for records."
- *Follow-up:* "How do you make sure NODUPKEY keeps the latest record?"

**Q2. What happens if you omit OUT= in PROC SORT?**
- *Strong answer:* "The input dataset is replaced by the sorted version. That is fine on purpose, but
  dangerous with NODUPKEY because removed rows are lost permanently."

### Module wrap-up

- **I now know:** PROC SORT, DESCENDING, NODUPKEY, NODUPRECS, DUPOUT, NOUNIQUEKEY, and sort costs.
- **I can now:** sort data and remove or isolate duplicates correctly.
- **Next:** Module 19 — formats.

---

## MODULE 19 — Formats, Informats and User-Defined Formats

**Syllabus items:** 2.15 SAS FORMAT · 2.16 Creating user-defined SAS formats · 2.17 Storing and using
SAS formats in a permanent library

**You will learn:** how formats change the way values look, how to build your own, how to use them for
grouping and lookups, and how to store them permanently. **Why it matters:** formats are one of the
most powerful SAS features and have no exact equivalent in SQL or Pandas. **Before you start:**
Modules 4 and 8.

### 🧠 What it is

- A **format** changes how a value is **shown**. The stored value does not change.
- An **informat** tells SAS how to **read** a value from text (Module 8).

```text
stored value 24108  --DATE9. format-->  shown as 02JAN2026
stored value 125000 --COMMA12. format--> shown as 125,000
```

### Common built-in formats (2.15)

| Format | Value | Shown as |
| --- | --- | --- |
| `COMMA12.` | 1250000 | `1,250,000` |
| `COMMA12.2` | 1250000.5 | `1,250,000.50` |
| `DOLLAR12.2` | 1250 | `$1,250.00` |
| `PERCENT8.1` | 0.125 | `12.5%` |
| `Z6.` | 123 | `000123` (leading zeros) |
| `8.2` | 3.14159 | `3.14` |
| `DATE9.` | 24108 | `02JAN2026` |
| `DDMMYY10.` | 24108 | `02/01/2026` |
| `YYMMDD10.` | 24108 | `2026-01-02` |
| `MONYY7.` | 24108 | `JAN2026` |
| `DATETIME20.` | a datetime | `02JAN2026:10:30:00` |
| `$UPCASE10.` | `mumbai` | `MUMBAI` |
| `BEST12.` | any number | SAS picks the best layout |

**Where you attach a format matters:**

```sas
data work.txn2;
    set work.txn;
    format amount comma12.2;      /* stored with the dataset: used everywhere later */
run;

proc print data=work.txn;
    format amount dollar12.2;     /* only for this PROC PRINT */
run;
```

**PUT and INPUT functions** convert between types using formats and informats:

```sas
data _null_;
    amount_text = put(125000, comma12.);           /* number -> text: '     125,000' */
    date_value  = input('02/01/2026', ddmmyy10.);  /* text -> number: 24108 */
    put amount_text= date_value= date_value= date9.;
run;
```

### User-defined formats with PROC FORMAT (2.16)

```sas
proc format;
    value ficoband
        low  -< 650 = 'High risk'
        650  -< 750 = 'Medium risk'
        750 - high  = 'Low risk'
        .           = 'No score';
    value $segment
        'R'   = 'Retail'
        'C'   = 'Corporate'
        'S'   = 'SME'
        other = 'Unknown';
run;

proc print data=work.customers noobs;
    var cust_id fico segment;
    format fico ficoband. segment $segment.;
run;
```

**Output**

| cust_id | fico | segment |
| --- | --- | --- |
| C101 | Medium risk | Retail |
| C102 | Medium risk | Corporate |
| C103 | High risk | Retail |
| C104 | No score | SME |

**Range rules**

| Range | Means |
| --- | --- |
| `650 -< 750` | 650 up to, but **not including**, 750 |
| `650 <- 750` | above 650, up to and including 750 |
| `low - 650` | everything up to 650 |
| `750 - high` | 750 and above |
| `other` | anything not listed |
| `.` | missing |

⚠️ For **numeric** formats, `LOW` does **not** include missing values. That is why `.` has its own
line. (For character formats, `LOW` does include blank values.)

⚠️ Format names cannot end in a number (`band2` is not allowed), because SAS would confuse the number
with a width. Character format names start with `$`.

### Formats for grouping (very powerful)

Procedures group by **formatted** values. A format can turn 700 different FICO scores into 4 groups
without creating a new variable:

```sas
proc freq data=work.customers;
    tables fico / missing;
    format fico ficoband.;
run;
```

**Output (main columns)**

| fico | Frequency | Percent |
| --- | --- | --- |
| No score | 1 | 25.00 |
| High risk | 1 | 25.00 |
| Medium risk | 2 | 50.00 |

The rows appear in the order of the underlying values (missing first, then 615, then 688 and 742).
`MISSING` makes PROC FREQ count missing values as a group.

### Formats as lookup tables

```sas
data work.cust_named;
    set work.customers;
    length segment_name $12;
    segment_name = put(segment, $segment.);    /* a lookup, no join needed */
run;
```

**Building a format from a dataset (CNTLIN)**, for example 2,000 branch codes:

```sas
data work.branch_master;
    length branch_code $5 branch_name $20;
    input branch_code $ branch_name $;
    datalines;
BR001 Mumbai-Fort
BR002 Delhi-CP
BR003 Pune-Camp
;
run;

data work.branch_fmt;
    set work.branch_master (rename=(branch_code=start branch_name=label));
    retain fmtname 'branch' type 'C';     /* TYPE='C' makes it a character format: $BRANCH. */
run;

proc format cntlin=work.branch_fmt;
run;

data _null_;
    name = put('BR002', $branch.);
    put name=;                              /* name=Delhi-CP */
run;
```

🚀 Format lookups are fast and need no sorting. Many banks use them instead of joins for small
reference tables.

### Storing formats permanently (2.17)

By default, PROC FORMAT stores formats in `WORK.FORMATS`, which disappears when SAS closes. To keep
them, store them in a permanent library:

```sas
libname fmtlib "C:\sasdata\formats";

proc format library=fmtlib;       /* stored in the catalog FMTLIB.FORMATS */
    value ficoband
        low  -< 650 = 'High risk'
        650  -< 750 = 'Medium risk'
        750 - high  = 'Low risk'
        .           = 'No score';
run;
```

**Using them in any later program:**

```sas
libname fmtlib "C:\sasdata\formats";
options fmtsearch=(fmtlib work library);   /* where SAS looks for formats, in order */

proc freq data=bank.customers;
    tables fico;
    format fico ficoband.;
run;
```

📌 `FMTSEARCH=` tells SAS where to look. SAS always checks `WORK` and `LIBRARY` first unless you
list them yourself; a libref named `LIBRARY` is searched automatically.

**See what a format contains:**

```sas
proc format library=fmtlib fmtlib;
    select ficoband;
run;
```

⚠️ If a dataset has a permanent format attached but SAS cannot find the format, you get
`ERROR: The format FICOBAND was not found or could not be loaded.` Fix `FMTSEARCH=`, or run
`options nofmterr;` to let SAS continue using default formats.

### SQL Server and Pandas

| Task | SAS | SQL Server | Pandas |
| --- | --- | --- | --- |
| Display a number with commas | `format amount comma12.;` | `FORMAT(amount, 'N0')` | `df["amount"].map("{:,.0f}".format)` |
| Code to label | `put(segment, $segment.)` | Join a lookup table / `CASE` | `df["segment"].map({"R": "Retail"})` |
| Group by bands | `format fico ficoband.` in the PROC | `CASE` in `GROUP BY` | `pd.cut(df["fico"], bins=...)` |

📌 The big difference: in SQL and Pandas you create a new column to change appearance or grouping. In
SAS the format is attached to the variable, so the same stored value can be shown or grouped many
ways without new columns.

### 💼 Banking scenario

A bank keeps a permanent format library maintained by the data team: `$branch.` (branch names),
`$product.` (product names), `dpdbucket.` (0, 1–30, 31–60, 61–90, 90+ days past due) and `ficoband.`.
Every report uses the same definitions, so every team's "61–90 DPD" means exactly the same thing.

### ⚠️ Common mistakes

- Thinking a format changes the stored value. `fico` is still 742, not `'Medium risk'`.
- Overlapping ranges in PROC FORMAT (`ERROR: These two ranges overlap`).
- Forgetting missing values in numeric formats.
- Forgetting `FMTSEARCH=` in a new session, so every report fails.

### Exercises

1. **Level 1:** Show `txn_date` three ways: `DATE9.`, `DDMMYY10.` and `MONYY7.`.
2. **Level 2:** Create a format `amtband` for amounts: under 10,000; 10,000 to under 1 lakh; 1 lakh
   and above; missing.
3. **Level 3:** Use that format in PROC FREQ to count transactions per band.
4. **Level 4 — Interview:** "What is the difference between a format and an informat?"
5. **Level 5:** Build a branch-name format from a dataset with CNTLIN, store it permanently, and use it
   in a new session.

### ⭐ Interview questions

**Q1. What is the difference between FORMAT and INFORMAT?**
- *Strong answer:* "An informat reads raw text into a SAS value, for example `ddmmyy10.` turns
  `02/01/2026` into the date value 24108. A format controls how a stored value is displayed, for
  example `date9.` shows 24108 as `02JAN2026`. The stored value never changes."

**Q2. How do you use the same user-defined formats across many programs?**
- *Strong answer:* "Store them in a permanent catalog with `PROC FORMAT LIBRARY=fmtlib`, then set
  `options fmtsearch=(fmtlib work library);` in the autoexec so every session finds them."

**Q3. How can formats replace a join?**
- *Strong answer:* "Turn the lookup table into a format with CNTLIN, then use `PUT(code, $fmt.)`. No
  sorting or merging is needed, which is fast for small to medium lookup tables."

### Module wrap-up

- **I now know:** built-in formats, PUT and INPUT functions, PROC FORMAT value ranges, CNTLIN, and
  permanent format catalogs.
- **I can now:** label, band and look up values with formats, and share them across programs.
- **Next:** Module 20 — selecting observations.

---

## MODULE 20 — Picking Observations: Samples, Ranges, Every Other Row and Row Numbers

**Syllabus items:** 3.15 Selecting random observations · 3.16 Reading data from one dataset to another
while selecting observations · 5.10 Creating row numbers · 5.11 Selecting random observations (same as
3.15) · 5.12 Selecting every alternate observation

**You will learn:** how to take random samples, read a range of rows, pick every n-th row, and number
rows correctly. **Why it matters:** sampling is used for audits, model building and testing on big
data. **Before you start:** Modules 7 and 15.

### Selecting a range of observations (3.16)

```sas
data work.rows_2_to_4;
    set work.txn (firstobs=2 obs=4);
run;
```

**Result:** T002, T003, T004 — **3 rows**, not 4.

⚠️ `OBS=` is the number of the **last** row to read, not how many rows to read. `firstobs=2 obs=4`
means rows 2 to 4.

**Read one specific row directly with POINT=:**

```sas
data work.fifth_row;
    pick = 5;
    set work.txn point=pick;
    output;
    stop;          /* REQUIRED with POINT=, or the step never ends */
run;
```

With `POINT=`, SAS jumps straight to that row instead of reading from the top. It never reaches an
end-of-file, so you must stop the step yourself with `STOP;`.

### Selecting every alternate observation (5.12)

```sas
/* Method 1: MOD on _N_ (keeps rows 2, 4, 6, ...) */
data work.even_rows;
    set work.txn;
    if mod(_n_, 2) = 0;
run;

/* Method 2: POINT= (reads only the rows needed - faster on big data) */
data work.even_rows2;
    do i = 2 to n by 2;
        set work.txn point=i nobs=n;
        output;
    end;
    stop;
run;
```

**Result of both:** T002, T004, T006.

`MOD(_N_, 2)` is the remainder after dividing the row count by 2. For every 10th row use
`mod(_n_, 10) = 0`, or `do i = 10 to n by 10;`.

### Selecting random observations (3.15, 5.11)

**Method 1: PROC SURVEYSELECT** (the standard tool; part of SAS/STAT)

```sas
/* exactly 1,000 rows at random */
proc surveyselect data=bank.transactions out=work.txn_sample
                  method=srs sampsize=1000 seed=2026;
run;

/* 10% at random */
proc surveyselect data=bank.transactions out=work.txn_10pct
                  method=srs samprate=0.10 seed=2026;
run;

/* 200 rows from EACH channel (stratified sample) */
proc sort data=bank.transactions out=work.txn_by_channel;
    by channel;
run;

proc surveyselect data=work.txn_by_channel out=work.txn_strat
                  method=srs sampsize=200 seed=2026 selectall;
    strata channel;
run;
```

- `METHOD=SRS` means simple random sampling: every row has the same chance.
- `SEED=` makes the sample repeatable. The same seed gives the same sample next time.
- `STRATA` samples within each group. The data must be sorted by the STRATA variable.
- `SELECTALL` takes the whole group if it has fewer rows than requested (otherwise SAS stops with an
  error).

**Method 2: DATA step with RAND** (about 10%, no SAS/STAT needed)

```sas
data work.sample_about_10pct;
    if _n_ = 1 then call streaminit(2026);   /* set the seed once */
    set bank.transactions;
    if rand('uniform') <= 0.10;
run;
```

`RAND('UNIFORM')` gives a random number between 0 and 1. Each row is kept with a 10% chance, so the
sample size is **about** 10%, not exactly.

**Method 3: DATA step, exactly n rows** (selection sampling)

```sas
data work.sample_exact_500;
    if _n_ = 1 then call streaminit(2026);
    retain k 500;                                  /* rows still to pick */
    set bank.transactions nobs=n;
    if rand('uniform') < k / (n - _n_ + 1) then do;
        output;
        k = k - 1;
    end;
    if k = 0 then stop;
    drop k;
run;
```

Each row is picked with probability "rows still needed ÷ rows still left". This always picks exactly
500 rows, each with an equal chance, in one pass.

**Method 4: PROC SQL**

```sas
proc sql outobs=100;
    create table work.sql_sample as
    select * from bank.transactions
    order by ranuni(2026);
quit;
```

This shuffles the whole table, so it is slow on big data. `OUTOBS=` keeps the first 100 rows and the
Log shows a warning that the statement stopped early, which is expected.

📌 Use `RAND` with `CALL STREAMINIT`. The older `RANUNI` function still works but uses an older,
weaker random-number method.

### Creating row numbers (5.10)

```sas
/* all rows: _N_ is fine */
data work.numbered;
    set work.txn;
    row_num = _n_;
run;
```

⚠️ But `_N_` counts **loops**, not output rows. With a subsetting IF they differ:

```sas
data work.online_numbered;
    set work.txn;
    if channel = 'ONLINE';
    iter = _n_;          /* loop number */
    row_num + 1;         /* sum statement: counts only rows that got this far */
run;
```

**Output**

| txn_id | channel | iter | row_num |
| --- | --- | --- | --- |
| T002 | ONLINE | 2 | 1 |
| T004 | ONLINE | 4 | 2 |
| T006 | ONLINE | 6 | 3 |

📌 `row_num + 1;` is a **sum statement**: `row_num` starts at 0, is retained between rows, and goes up
by 1 each time the statement runs (Module 34).

**Row number within each group** (preview of Module 34):

```sas
proc sort data=work.txn out=work.txn_s;
    by cust_id txn_date;
run;

data work.txn_seq;
    set work.txn_s;
    by cust_id;
    if first.cust_id then seq = 0;
    seq + 1;
run;
```

C101 gets 1, 2, 3; C102 gets 1, 2; C103 gets 1.

### SQL Server, PROC SQL and Pandas

| Task | SAS | SQL Server | Pandas |
| --- | --- | --- | --- |
| Rows 2 to 4 | `set ds(firstobs=2 obs=4);` | `ORDER BY ... OFFSET 1 ROWS FETCH NEXT 3 ROWS ONLY` | `df.iloc[1:4]` |
| Every 2nd row | `if mod(_n_, 2) = 0;` | `WHERE rn % 2 = 0` with `ROW_NUMBER()` | `df.iloc[1::2]` |
| Random n | `PROC SURVEYSELECT sampsize=` | `SELECT TOP 1000 * ... ORDER BY NEWID()` | `df.sample(n=1000, random_state=2026)` |
| Random % | `samprate=0.10` | `TABLESAMPLE (10 PERCENT)` | `df.sample(frac=0.10)` |
| Row number | `_n_` / `row_num + 1;` | `ROW_NUMBER() OVER (ORDER BY ...)` | `range(1, len(df) + 1)` |
| Number within group | `FIRST.` + sum statement | `ROW_NUMBER() OVER (PARTITION BY ...)` | `groupby().cumcount() + 1` |

### 💼 Banking scenario

Internal audit asks for a random, repeatable sample of 50 loan files from each branch to check
documents. PROC SURVEYSELECT with `STRATA branch`, `SAMPSIZE=50`, `SELECTALL` and a recorded `SEED=`
gives a sample the auditors can reproduce exactly, which they require.

### ⚠️ Common mistakes

- Reading `OBS=` as a count.
- Forgetting `STOP;` with `POINT=`. The step runs forever.
- Using `_N_` as a row number after filtering with IF.
- Not setting a seed, so the sample changes each run and cannot be checked.
- Calling `CALL STREAMINIT` after `RAND` has already been used. It has no effect then.

### Exercises

1. **Level 1:** Read rows 3 to 5 of `work.txn`.
2. **Level 2:** Keep every 3rd row two ways (MOD and POINT=).
3. **Level 3:** Take a repeatable 5% sample with RAND and count the rows you got. Run it twice.
4. **Level 4 — Interview:** "Why can _N_ differ from the row number in the output?"
5. **Level 5:** Draw a stratified audit sample of 20 accounts per branch and prove it is repeatable.

### ⭐ Interview questions

**Q1. How do you select a random sample in SAS?**
- *Strong answer:* "PROC SURVEYSELECT with METHOD=SRS and SAMPSIZE= or SAMPRATE=, with a SEED so it is
  repeatable, and STRATA for stratified samples. Without SAS/STAT I use the DATA step with
  `RAND('UNIFORM')` after `CALL STREAMINIT`, or the selection-sampling method for an exact count."

**Q2. What does `set ds(firstobs=5 obs=10);` read?**
- *Strong answer:* "Rows 5 through 10, which is 6 rows. OBS= is the last row number, not a count."

### Module wrap-up

- **I now know:** FIRSTOBS/OBS, POINT=, MOD(_N_), SURVEYSELECT, RAND, exact sampling, and correct row
  numbering.
- **I can now:** sample, slice and number observations for audits, testing and modelling.
- **Next:** Mini Project 1, then Part IV — functions.

---

## Mini Project 1 — Customer and Transaction Data Intake

**Uses:** Parts I–III. **Domain:** retail banking.

**Business requirement:** every morning the bank receives `customers.csv` and a pipe-delimited
`transactions.txt`. Build the SAS intake step that loads, checks and cleans them before any report
runs.

**Source files (create them yourself with at least 30 customers and 300 transactions):**

| File | Columns |
| --- | --- |
| `customers.csv` (header row) | customer_id, name, city, segment, open_date (dd/mm/yyyy), fico |
| `transactions.txt` (pipe, header row) | txn_id, customer_id, txn_date (yyyy-mm-dd), channel, merchant, amount |

Put some problems in the data on purpose: duplicate transaction IDs, a few missing amounts, negative
amounts, unknown channels, merchant names containing the delimiter in quotes, and names longer than 8
characters.

**Tasks**

1. Assign libraries `raw` (read-only), `stage` and `rpt` (Module 4).
2. Read both files with DATA steps (not PROC IMPORT), with explicit `LENGTH`, informats and formats
   (Modules 5 and 8).
3. Check structure with PROC CONTENTS (Module 6).
4. Split transactions into `stage.txn_clean`, `stage.txn_reject` (missing or negative amount, unknown
   channel) and `stage.txn_review` (amount over ₹10 lakh) in **one** DATA step (Modules 15 and 17).
5. Remove duplicate transaction IDs, keeping the latest load, and save the removed rows (Module 18).
6. Create formats for segment names and amount bands and store them permanently (Module 19).
7. Take a repeatable 10% sample of clean transactions for a manual spot check (Module 20).
8. Print row counts for every dataset and confirm: clean + reject + review + duplicates = rows read.

**What it proves:** you can build a reliable data-intake step, which is the first thing every SAS job
in a bank does.

**Part III checklist:** ✓ 2.3 · ✓ 2.4 · ✓ 2.5 · ✓ 2.6 · ✓ 2.7 · ✓ 2.8 · ✓ 2.9 · ✓ 2.12 · ✓ 2.13 · ✓ 2.14 · ✓ 2.15 · ✓ 2.16 ·
✓ 2.17 · ✓ 2.18 · ✓ 3.15 · ✓ 3.16 · ✓ 5.10 · ✓ 5.11 · ✓ 5.12

---

# Part IV — SAS Functions (Modules 21–24)

A **function** takes one or more values and returns one value. In SAS you can use functions in DATA
steps, in WHERE clauses, in PROC SQL and (through `%SYSFUNC`) in macro code. Part X has a complete
reference table of every function in these modules with its SQL Server and Pandas equivalent.

## MODULE 21 — Character Functions

**Syllabus items:** 4.1 Character functions · 6.1 Character functions (same topic)

**You will learn:** the functions for measuring, cutting, searching, cleaning, joining and converting
text. **Why it matters:** bank data is full of messy names, phone numbers, addresses and codes.
**Before you start:** Modules 4 and 19.

### Measuring text: LENGTH, LENGTHN, LENGTHC

| Function | Returns | `'Mumbai   '` | `'   '` (all blank) |
| --- | --- | --- | --- |
| `LENGTH(s)` | Length without trailing blanks | 6 | **1** |
| `LENGTHN(s)` | Same, but 0 for a blank value | 6 | **0** |
| `LENGTHC(s)` | Length **including** trailing blanks (the stored length) | 9 | 3 |

📌 Use `LENGTHN` when you need to test for "empty". `LENGTH` returns 1 for a blank value, which
surprises people.

### Cutting text: SUBSTR and SCAN

```sas
data _null_;
    acct = 'ACC1234567';
    a = substr(acct, 4, 4);                 /* '1234'  : from position 4, 4 characters */
    b = substr(acct, 4);                    /* '1234567': from position 4 to the end */
    full_name = 'Asha Rao Kulkarni';
    c = scan(full_name, 2);                 /* 'Rao'      : 2nd word */
    d = scan(full_name, -1);                /* 'Kulkarni' : last word */
    e = scan('C101|Mumbai|R', 2, '|');      /* 'Mumbai'   : 2nd field, '|' as the only delimiter */
    put a= b= c= d= e=;
run;
```

**Masking with SUBSTR on the left side** (replaces characters in place):

```sas
data _null_;
    card = '4111111111111111';
    substr(card, 1, 12) = 'XXXXXXXXXXXX';
    put card=;                              /* card=XXXXXXXXXXXX1111 */
run;
```

⚠️ **SCAN's default delimiters** include blank and `! $ % & ( ) * + , - . / ; < ^ |`. So
`scan('ravi.k@bank.com', 1)` returns `ravi`, not the whole user name, because `.` is a delimiter.
Always give the delimiter yourself: `scan(email, 2, '@')` returns `bank.com`.

### Counting and searching: COUNT, COUNTW, COUNTC, INDEX, FIND

```sas
data _null_;
    a = count('ATM-ATM-POS', 'ATM');            /* 2  : times 'ATM' appears */
    b = countw('Asha Rao Kulkarni');            /* 3  : number of words */
    c = countc('9820-123-456', '-');            /* 2  : number of '-' characters */
    d = index('NEFT/IMPS/UPI', 'UPI');          /* 11 : position of 'UPI', 0 if absent */
    e = index('upi payment', 'UPI');            /* 0  : INDEX is case-sensitive */
    f = find('upi payment', 'UPI', 'i');        /* 1  : 'i' = ignore case */
    put a= b= c= d= e= f=;
run;
```

`FIND(string, text, modifiers, start)` is the more flexible version of `INDEX`: `'i'` ignores case,
`'t'` trims trailing blanks, and `start` says where to begin searching.

### Changing case: UPCASE, LOWCASE, PROPCASE

| Call | Result |
| --- | --- |
| `upcase('mumbai')` | `MUMBAI` |
| `lowcase('ATM')` | `atm` |
| `propcase('ASHA RAO')` | `Asha Rao` |
| `propcase("o'brien")` | `O'brien` (the apostrophe is not a word break by default) |

📌 Compare text in one case: `if upcase(channel) = 'ONLINE'`.

### Cleaning text: COMPRESS, COMPBL, STRIP, TRIM, LEFT

| Call | Result | What it did |
| --- | --- | --- |
| `compress('98201 23456')` | `9820123456` | Removed blanks (the default) |
| `compress('+91-98201-23456', '+-')` | `919820123456` | Removed `+` and `-` |
| `compress('Ph: +91 98201 23456', , 'kd')` | `919820123456` | `k` = **keep**, `d` = digits: keep only digits |
| `compbl('Asha    Rao')` | `Asha Rao` | Squashed repeated blanks into one |
| `strip('  C101  ')` | `C101` | Removed leading **and** trailing blanks |
| `trim('C101   ')` | `C101` | Removed trailing blanks only |
| `left('   C101')` | `C101   ` | Moved leading blanks to the end |

🧠 SAS character variables have a fixed length, so trailing blanks come back when you store a value.
`TRIM` and `STRIP` matter most **inside** concatenation and comparisons, not when assigning.

### Joining text: CAT, CATS, CATT, CATX and ||

Suppose `first` is `'Asha'` and `last` is `'Rao'`, both stored in variables of length 10 (so each has
trailing blanks), and `middle` is blank.

| Call | Result | Rule |
| --- | --- | --- |
| `first \|\| last` | `Asha      Rao` | Joins exactly, blanks and all |
| `cat(first, last)` | `Asha      Rao` | Same as `\|\|` |
| `cats(first, last)` | `AshaRao` | **S**trips leading and trailing blanks from each value |
| `catt(first, last)` | `AshaRao` | **T**rims trailing blanks only |
| `catx(' ', first, middle, last)` | `Asha Rao` | Strips, puts the separator between values, and **skips blank values** |
| `catx('-', 'BR001', '', '2026')` | `BR001-2026` | The empty value is skipped, so no `--` |

📌 `CATX` is ideal for addresses and keys: no double separators when a part is missing.

⚠️ If the result variable has no LENGTH, CAT-family functions give it a length of **200**. Set the
length yourself.

### Replacing text: TRANWRD and TRANSLATE

```sas
data _null_;
    a = tranwrd('ROAD NO 5 ROAD', 'ROAD', 'RD');   /* 'RD NO 5 RD' : every occurrence */
    b = translate('98-201/234', '  ', '-/');       /* '98 201 234' : each - and / becomes a blank */
    put a= b=;
run;
```

| | `TRANWRD(source, target, replacement)` | `TRANSLATE(source, to, from)` |
| --- | --- | --- |
| Replaces | Whole words or substrings | Single characters, one for one |
| Argument order | **target, then replacement** | ⚠️ **to, then from** (the opposite way round) |

### Converting between text and numbers: INPUT and PUT

| Call | Result | Direction |
| --- | --- | --- |
| `input('1,25,000', comma10.)` | 125000 | Text → number |
| `input('02/01/2026', ddmmyy10.)` | 24108 (a date) | Text → date |
| `put(24108, yymmdd10.)` | `2026-01-02` | Number → text |
| `put(42, z6.)` | `000042` | Number → text with leading zeros |

⚠️ Let SAS convert types automatically (for example `amount_num = amount_text * 1;`) and the Log
shows `NOTE: Character values have been converted to numeric values at the places given by:
(Line):(Column).` It works, but it hides intent and can produce wrong results. Use `INPUT` and `PUT`
on purpose. Many teams treat that NOTE as an error.

### Validation helpers

| Function | Returns | Example use |
| --- | --- | --- |
| `NOTDIGIT(s)` | Position of the first non-digit (0 if all digits) | `if notdigit(strip(mobile)) = 0` → digits only |
| `ANYDIGIT(s)` | Position of the first digit (0 if none) | Find names that contain numbers |
| `ANYALPHA(s)` | Position of the first letter | Check account numbers have no letters |
| `REVERSE(s)` | Text backwards | Some check-digit routines |
| `REPEAT(s, n)` | `s` repeated **n + 1** times | ⚠️ `repeat('X', 3)` is `XXXX` |

### A complete cleaning example

```sas
data work.messy;
    infile datalines dlm=',' dsd;
    length cust_id $5 raw_name $30 raw_phone $20 raw_email $40;
    input cust_id $ raw_name $ raw_phone $ raw_email $;
    datalines;
C101,  asha   RAO ,+91-98201-23456,Asha.Rao@Bank.COM
C102,BILAL khan,98765 43210,bilal.khan@bank.com
C103,chetan  iyer,(022) 2345 6789,
;
run;

data work.clean_cust;
    set work.messy;
    length name $30 digits $20 phone $10 email $40 email_domain $30;
    name   = propcase(compbl(strip(raw_name)));
    digits = compress(raw_phone, , 'kd');                       /* keep digits only */
    if length(digits) >= 10 then phone = substr(digits, length(digits) - 9);   /* last 10 */
    valid_mobile = (length(phone) = 10 and substr(phone, 1, 1) in ('6', '7', '8', '9'));
    email = lowcase(strip(raw_email));
    if email ne '' then email_domain = scan(email, 2, '@');
    drop raw_: digits;                                          /* raw_: = every name starting raw_ */
run;
```

**Output**

| cust_id | name | phone | email | email_domain | valid_mobile |
| --- | --- | --- | --- | --- | --- |
| C101 | Asha Rao | 9820123456 | asha.rao@bank.com | bank.com | 1 |
| C102 | Bilal Khan | 9876543210 | bilal.khan@bank.com | bank.com | 1 |
| C103 | Chetan Iyer | 2223456789 | (blank) | (blank) | 0 |

**Why C103 is not a valid mobile:** its digits are `02223456789` (a landline with an area code). The
last 10 digits start with `2`, and Indian mobile numbers start with 6, 7, 8 or 9.

### SQL Server and Pandas (main ones)

| SAS | SQL Server | Pandas |
| --- | --- | --- |
| `substr(s, 4, 4)` | `SUBSTRING(s, 4, 4)` | `s.str[3:7]` |
| `scan(s, 2, '@')` | `PARSENAME` / `STRING_SPLIT` | `s.str.split('@').str[1]` |
| `index(s, 'UPI')` | `CHARINDEX('UPI', s)` | `s.str.find('UPI') + 1` |
| `upcase(s)` | `UPPER(s)` | `s.str.upper()` |
| `strip(s)` | `TRIM(s)` (SQL Server 2017+) | `s.str.strip()` |
| `catx('-', a, b)` | `CONCAT_WS('-', a, b)` | `a + '-' + b` |
| `tranwrd(s, 'a', 'b')` | `REPLACE(s, 'a', 'b')` | `s.str.replace('a', 'b')` |
| `compress(s, , 'kd')` | Nested `REPLACE` or `TRANSLATE` | `s.str.replace(r'\D', '', regex=True)` |

### ⚠️ Common mistakes

- Forgetting SCAN's default delimiters.
- Swapping TRANSLATE's `to` and `from`.
- Using `LENGTH` to test for blank values.
- Leaving result lengths at 200 (wasted space) or too short (cut-off values).
- Relying on automatic character-to-number conversion.

### Exercises

1. **Level 1:** Extract the first name and last name from `'Asha Rao Kulkarni'`.
2. **Level 2:** Mask all but the last 4 digits of a 16-digit card number two ways (SUBSTR on the left
   side, and CATS with REPEAT).
3. **Level 3:** Clean a phone column that has `+91`, spaces, dashes and brackets into 10 digits, and
   flag invalid numbers.
4. **Level 4 — Interview:** "What is the difference between CATS, CATT and CATX?"
5. **Level 5:** Standardise a messy address column (case, spaces, `ROAD` → `RD`, `NAGAR` spelling
   variants) and build a matching key to find duplicate customers.

### ⭐ Interview questions

**Q1. TRIM vs STRIP vs COMPRESS?**
- *Strong answer:* "TRIM removes trailing blanks. STRIP removes leading and trailing blanks. COMPRESS
  removes characters anywhere in the string: blanks by default, or the characters I list, and with
  modifiers like `'kd'` it can keep only digits."

**Q2. Why might `scan(email, 1)` return the wrong value?**
- *Strong answer:* "SCAN's default delimiters include the period, so `ravi.k@bank.com` splits at the
  dot. I always pass the delimiter explicitly."

### Module wrap-up

- **I now know:** the main character functions, their traps, and their SQL and Pandas equivalents.
- **I can now:** clean names, phones, emails and codes reliably.
- **Next:** Module 22 — numeric functions.

---

## MODULE 22 — Numeric Functions, and SUM vs Addition

**Syllabus items:** 4.2 Numeric functions · 6.2 Numeric functions (same topic) · 5.4 Difference between
SUM and addition

**You will learn:** the numeric functions you will use daily, how missing values behave in each, and
the LAG trap. **Why it matters:** "SUM vs +" and "LAG in an IF" are classic interview questions, and
they cause real reporting errors. **Before you start:** Module 4.

### 🔥 SUM vs addition (5.4)

| Expression | `a = 100, b = .` | Rule |
| --- | --- | --- |
| `a + b` | `.` (missing) | Any missing value makes the result missing |
| `sum(a, b)` | 100 | Missing values are ignored |
| `sum(., .)` | `.` | All missing gives missing |
| `sum(0, a, b)` | 100, and 0 if all are missing | The `0` makes the result never missing |
| `total + amount;` (sum **statement**) | Adds, ignores missing, keeps the total between rows | Module 34 |

```sas
data work.monthly;
    input cust_id $ jan feb mar;
    plus_total = jan + feb + mar;
    sum_total  = sum(jan, feb, mar);
    list_total = sum(of jan--mar);      /* every variable from jan to mar in PDV order */
    datalines;
C101 1000 2000 3000
C102 1000 . 3000
;
run;
```

**Output**

| cust_id | jan | feb | mar | plus_total | sum_total | list_total |
| --- | --- | --- | --- | --- | --- | --- |
| C101 | 1000 | 2000 | 3000 | 6000 | 6000 | 6000 |
| C102 | 1000 | . | 3000 | **.** | 4000 | 4000 |

The Log also shows `NOTE: Missing values were generated as a result of performing an operation on
missing values.`

⚠️ **The OF trap:** `sum(m1-m12)` means "m1 **minus** m12". To add a range of variables, write
`sum(of m1-m12)`. The same applies to `mean(of ...)`, `max(of ...)` and others.

| Variable list | Means |
| --- | --- |
| `of m1-m12` | `m1`, `m2`, ..., `m12` (numbered names) |
| `of jan--dec` | Every variable from `jan` to `dec` in the dataset's column order |
| `of amt_:` | Every variable whose name starts with `amt_` |
| `of _numeric_` | Every numeric variable |

**Which one is right?** It depends on the business meaning. If a missing month means "no data yet",
`a + b` (giving missing) may be the honest answer. If missing means "zero spend", use `SUM`.

### Statistics across columns: SUM, MEAN, MIN, MAX, N, NMISS

| Call | Result |
| --- | --- |
| `mean(10, ., 20)` | 15 (missing ignored) |
| `min(5, ., 3)` | 3 |
| `max(., .)` | `.` |
| `n(10, ., 20)` | 2 (count of non-missing values) |
| `nmiss(10, ., 20)` | 1 (count of missing values) |

📌 These work **across columns in one row**. To summarise **down rows** (all customers), use PROC MEANS
or PROC SQL.

### Rounding: ROUND, CEIL, FLOOR, INT

| Call | Result |
| --- | --- |
| `round(1234.5678, 0.01)` | 1234.57 |
| `round(1234.5678, 100)` | 1200 |
| `round(2.5)` | 3 |
| `round(-2.5)` | -3 (halves go away from zero) |
| `ceil(4.1)` | 5 |
| `floor(4.9)` | 4 |
| `int(-3.7)` | -3 (cuts off the decimals) |
| `floor(-3.7)` | -4 (goes down) |

⚠️ Python's built-in `round(2.5)` gives **2** (it rounds halves to the nearest even number). SAS gives 3.
SQL Server's `ROUND(2.5, 0)` gives 3. This difference can make reconciliation totals disagree by a
few paise.

### Other numeric functions: ABS, MOD

| Call | Result | Use |
| --- | --- | --- |
| `abs(-500)` | 500 | Size of a reversal, ignoring sign |
| `mod(17, 5)` | 2 | Remainder. Every n-th row: `mod(_n_, 10) = 0` |
| `mod(-17, 5)` | -2 | The result takes the sign of the first value |

### LAG and DIF: values from earlier rows

`LAG(x)` returns the value of `x` from the previous time **the LAG function ran**. `DIF(x)` is
`x - LAG(x)`.

🧠 Each LAG call keeps its own little queue. It returns what is in the queue and stores the current
value. That works like "previous row" **only if LAG runs on every row**.

```sas
proc sort data=work.txn out=work.txn_s;
    by cust_id txn_date;
run;

data work.lag_demo;
    set work.txn_s;
    prev_amt_good = lag(amount);                       /* runs on every row */
    if channel = 'ONLINE' then prev_amt_bad = lag(amount);   /* runs only on ONLINE rows */
run;
```

**Output**

| txn_id | cust_id | channel | amount | prev_amt_good | prev_amt_bad |
| --- | --- | --- | --- | --- | --- |
| T001 | C101 | ATM | 5000 | . | . |
| T003 | C101 | POS | 2300 | 5000 | . |
| T006 | C101 | ONLINE | 78000 | 2300 | . |
| T002 | C102 | ONLINE | 125000 | 78000 | 78000 |
| T005 | C102 | ATM | 20000 | 125000 | . |
| T004 | C103 | ONLINE | . | 20000 | **125000** |

**Two lessons:**

1. **Conditional LAG is wrong.** T004's previous row is T005 (20,000), but `prev_amt_bad` is 125,000:
   the value from the last time LAG *ran*, on T002.
2. **LAG crosses groups.** T002 is C102's first transaction, but `prev_amt_good` shows C101's 78,000.
   Reset it at the start of each customer (Module 34):

```sas
data work.lag_fixed;
    set work.txn_s;
    by cust_id;
    prev_amt = lag(amount);                 /* always run LAG */
    if first.cust_id then prev_amt = .;     /* then blank it for a new customer */
    amt_change = amount - prev_amt;
run;
```

### Random numbers: RAND and RANUNI

```sas
data work.random_demo;
    call streaminit(2026);                  /* seed: makes results repeatable */
    do i = 1 to 3;
        u    = rand('uniform');             /* between 0 and 1 */
        z    = rand('normal', 0, 1);        /* normal distribution */
        dice = rand('integer', 1, 6);       /* whole number 1-6 (SAS 9.4M5 and later) */
        output;
    end;
run;
```

`RANUNI(seed)` is the older function. It still works but uses a weaker random-number method. Use
`RAND` for new work.

### SQL Server and Pandas

| SAS | SQL Server | Pandas |
| --- | --- | --- |
| `sum(a, b)` (row-wise, ignores missing) | `ISNULL(a,0) + ISNULL(b,0)` | `df[["a","b"]].sum(axis=1)` |
| `a + b` | `a + b` (NULL if any NULL) | `df["a"] + df["b"]` (NaN if any NaN) |
| `round(x, 0.01)` | `ROUND(x, 2)` | `df["x"].round(2)` (halves to even) |
| `lag(x)` | `LAG(x) OVER (ORDER BY ...)` | `df["x"].shift(1)` |
| `dif(x)` | `x - LAG(x) OVER (...)` | `df["x"].diff()` |
| `mod(a, b)` | `a % b` | `df["a"] % df["b"]` (sign follows the divisor) |

⚠️ Pandas' `%` gives `-17 % 5 = 3`, while SAS `mod(-17, 5)` gives -2 and SQL Server gives -2.

### 💼 Banking scenario

A monthly statement totals 12 months of fees. One customer had no account in March, so `fee_mar` is
missing. `fee_jan + ... + fee_dec` would make their **annual total missing**, and they would vanish
from the fee report. `sum(of fee_jan--fee_dec)` gives the correct total of the months that exist.

### ⚠️ Common mistakes

- Using `+` when missing values are possible, or `SUM` when a missing value should make the total
  unknown.
- Writing `sum(m1-m12)` without `OF`.
- Calling LAG inside an IF statement.
- Forgetting to reset LAG values at the start of each BY group.

### Exercises

1. **Level 1:** Compute quarterly totals for three months where some months are missing, using `+`
   and `SUM`. Compare.
2. **Level 2:** Round amounts to the nearest rupee, nearest 100 and nearest 0.05.
3. **Level 3:** Use LAG to compute the change in balance from the previous month per account,
   resetting at each new account.
4. **Level 4 — Interview:** "What is the difference between SUM() and the + operator?"
5. **Level 5:** Find accounts whose balance dropped by more than 50% from one month to the next.

### ⭐ Interview questions

**Q1. What is the difference between the SUM function and the + operator?**
- *Strong answer:* "With +, any missing operand makes the result missing, and SAS writes a NOTE. SUM
  ignores missing values and returns missing only if all are missing; `sum(0, ...)` returns 0 instead.
  The sum statement `total + x;` also ignores missing values and retains the total across rows."
- *Follow-up:* "What does `sum(x1-x5)` return?" ("x1 minus x5. You need OF.")

**Q2. Why can LAG give the wrong previous value?**
- *Strong answer:* "LAG keeps a queue that is updated only when the LAG function executes. Inside an IF
  it skips rows, so it returns the value from the last time it ran, not the previous observation. I
  always call LAG unconditionally and then use the result conditionally, and I reset it with
  FIRST.var."

### Module wrap-up

- **I now know:** SUM vs +, variable lists with OF, row-wise statistics, rounding rules, MOD, LAG,
  DIF and RAND.
- **I can now:** do numeric work safely with missing values and previous-row logic.
- **Next:** Module 23 — dates and times.

---

## MODULE 23 — Dates, Times and Datetimes

**Syllabus items:** 4.3 Datetime functions · 6.3 Datetime functions (same topic)

**You will learn:** how SAS stores dates, times and datetimes, how to read and display them, and the
functions for date arithmetic. **Why it matters:** 🔥 almost every banking metric depends on dates:
days past due, months on book, account age, statement cycles. **Before you start:** Modules 4, 8 and
19.

### 🧠 The SAS date and time model

| Type | Stored as | Zero point | Example value | Shown with |
| --- | --- | --- | --- | --- |
| **Date** | Number of **days** | 1 January 1960 = 0 | `02JAN2026` = 24108 | `DATE9.`, `DDMMYY10.` |
| **Datetime** | Number of **seconds** | 1 January 1960 00:00:00 = 0 | `02JAN2026:10:30:00` = 2082969000 | `DATETIME20.` |
| **Time** | Number of **seconds** since midnight | 00:00:00 = 0 | `10:30:00` = 37800 | `TIME8.` |

- Dates before 1960 are negative: `31DEC1959` = -1.
- They are ordinary numbers, so you can subtract them, compare them and sort them.
- The **format** decides how they look; the stored number never changes.

⚠️ Never mix them up. A date (days) compared with a datetime (seconds) gives nonsense with no error.

**Date, datetime and time constants** (written in your code):

```sas
d  = '02JAN2026'd;               /* date */
dt = '02JAN2026:10:30:00'dt;     /* datetime */
t  = '10:30't;                   /* time */
```

### Informat vs format for dates

| | Informat (reading) | Format (showing) |
| --- | --- | --- |
| `2026-01-02` | `YYMMDD10.` | `YYMMDD10.` |
| `02/01/2026` | `DDMMYY10.` | `DDMMYY10.` |
| `02JAN2026` | `DATE9.` | `DATE9.` |
| `2026-01-02T10:30:00` | `E8601DT19.` | `E8601DT19.` |
| `02JAN2026:10:30:00` | `DATETIME20.` | `DATETIME20.` |

### Getting today and building dates

| Function | Returns | Example |
| --- | --- | --- |
| `TODAY()` or `DATE()` | Today's date | `asof = today();` |
| `DATETIME()` | The current date and time | `run_ts = datetime();` |
| `TIME()` | The current time | |
| `MDY(m, d, y)` | A date from month, day, year | `mdy(9, 30, 2026)` = 24379 (`30SEP2026`) |
| `DHMS(date, h, m, s)` | A datetime from a date and a time | `dhms('02JAN2026'd, 10, 30, 0)` = `02JAN2026:10:30:00` |
| `HMS(h, m, s)` | A time | `hms(10, 30, 0)` = 37800 |

⚠️ **There is no `YMD()` function in SAS**, even though it appears in many cheat sheets. To build a
date from year, month and day use `mdy(month, day, year)`. To read text like `2026-09-30` use
`input('2026-09-30', yymmdd10.)`.

### Taking dates apart

For `d = '30SEP2026'd`:

| Function | Result |
| --- | --- |
| `year(d)` | 2026 |
| `month(d)` | 9 |
| `day(d)` | 30 |
| `qtr(d)` | 3 |
| `weekday('02JAN2026'd)` | 6 (1 = Sunday, so 6 = Friday) |

For `dt = '02JAN2026:10:30:00'dt`:

| Function | Result |
| --- | --- |
| `datepart(dt)` | 24108 (`02JAN2026`) |
| `timepart(dt)` | 37800 (`10:30:00`) |
| `hour(dt)` | 10 |

### 🔥 Date arithmetic: INTCK and INTNX

**Plain subtraction** gives days:

```sas
days_past_due = '30SEP2026'd - due_date;
next_review   = '30SEP2026'd + 90;
```

**INTCK** counts how many interval **boundaries** are crossed between two dates.

| Call | Result | Why |
| --- | --- | --- |
| `intck('month', '01JAN2026'd, '31JAN2026'd)` | 0 | No month boundary crossed |
| `intck('month', '31JAN2026'd, '01FEB2026'd)` | **1** | 1 day apart, but a month boundary is crossed |
| `intck('month', '31JAN2026'd, '01FEB2026'd', 'c')` | 0 | `'c'` = continuous: counts complete months |
| `intck('year', '15MAR2019'd, '30SEP2026'd)` | 7 | Boundaries 2020 to 2026 |
| `intck('year', '14FEB1990'd, '30SEP2026'd, 'c')` | 36 | Age in complete years |

📌 The default is the **discrete** method (count boundaries). Use `'c'` for "complete periods", such as
age or tenure. `yrdif(dob, asof, 'AGE')` also gives an exact age.

**INTNX** moves a date forward or back by a number of intervals, and can line it up to the start,
middle or end of the interval.

| Call | Result | Alignment |
| --- | --- | --- |
| `intnx('month', '15JAN2026'd, 1)` | `01FEB2026` | `'b'` beginning (the default) |
| `intnx('month', '15JAN2026'd, 1, 'e')` | `28FEB2026` | end of the month |
| `intnx('month', '15JAN2026'd, 0, 'e')` | `31JAN2026` | end of **this** month |
| `intnx('month', '31JAN2026'd, 1, 's')` | `28FEB2026` | same day (moved back to the month end when needed) |
| `intnx('year', '15MAR2026'd, 0, 'b')` | `01JAN2026` | start of this year |
| `intnx('day', '30SEP2026'd, 30)` | `30OCT2026` | 30 days later |

### A complete example

```sas
data work.loan_dates;
    input loan_id $ disb_date :date9. due_date :date9. paid_flag;
    asof = '30SEP2026'd;
    months_on_book = intck('month', disb_date, asof);
    if paid_flag = 0 then dpd = max(0, asof - due_date);
    else dpd = 0;
    next_emi   = intnx('month', due_date, 1, 's');
    month_end  = intnx('month', asof, 0, 'e');
    format disb_date due_date asof next_emi month_end date9.;
    datalines;
L001 15MAR2024 05SEP2026 0
L002 01JUL2026 05SEP2026 1
L003 10JAN2025 05JUL2026 0
;
run;
```

**Output**

| loan_id | disb_date | due_date | months_on_book | dpd | next_emi | month_end |
| --- | --- | --- | --- | --- | --- | --- |
| L001 | 15MAR2024 | 05SEP2026 | 30 | 25 | 05OCT2026 | 30SEP2026 |
| L002 | 01JUL2026 | 05SEP2026 | 2 | 0 | 05OCT2026 | 30SEP2026 |
| L003 | 10JAN2025 | 05JUL2026 | 20 | 87 | 05AUG2026 | 30SEP2026 |

(`paid_flag` and `asof` are also in the dataset; they are left out of this table to save space.)

**Check the numbers:** L001 crossed 30 month boundaries from March 2024 to September 2026. Its unpaid
EMI was due on 5 September, so it is 25 days past due on 30 September. L003's due date was 5 July:
26 days left in July, 31 in August and 30 in September make 87 days.

### Converting from Excel and other systems

Excel stores dates as days since 30 December 1899. SAS day 0 (1 January 1960) is Excel day 21916. So:

```sas
sas_date = excel_serial - 21916;     /* Excel 46024 becomes 02JAN2026 */
```

### SQL Server and Python comparison

| Task | SAS | SQL Server | Python / Pandas |
| --- | --- | --- | --- |
| Today | `today()` | `CAST(GETDATE() AS DATE)` | `date.today()` |
| Build a date | `mdy(9, 30, 2026)` | `DATEFROMPARTS(2026, 9, 30)` | `date(2026, 9, 30)` |
| Days between | `d2 - d1` | `DATEDIFF(day, d1, d2)` | `(d2 - d1).days` |
| Month boundaries crossed | `intck('month', d1, d2)` | `DATEDIFF(month, d1, d2)` (same boundary logic) | `(d2.year - d1.year) * 12 + d2.month - d1.month` |
| Add a month | `intnx('month', d, 1, 's')` | `DATEADD(month, 1, d)` | `d + relativedelta(months=1)` |
| Month end | `intnx('month', d, 0, 'e')` | `EOMONTH(d)` | `d + pd.offsets.MonthEnd(0)` |
| Date part of a datetime | `datepart(dt)` | `CAST(dt AS DATE)` | `ts.normalize()` / `ts.date()` |
| Stored as | Days since 1960 | Internal date type | Nanoseconds since 1970 (Pandas) |

### 💼 Banking scenario: DPD buckets

Regulators and collections teams group loans by **days past due**: current, 1–30, 31–60, 61–90 and 90+
(often treated as non-performing). With `dpd = asof - oldest_unpaid_due_date` and a PROC FORMAT with
those ranges (Module 19), one PROC FREQ produces the bucket report for the whole portfolio.

### ⚠️ Common mistakes

- Reading dates as text and comparing them alphabetically (`'02/01/2026' > '15/12/2025'` is false).
- Comparing a datetime with a date constant: `where txn_dt >= '01JAN2026'd` keeps almost everything,
  because a datetime in seconds is far larger than a date in days. Use `'01JAN2026:00:00:00'dt` or
  `datepart(txn_dt)`.
- Using INTCK's default when you need complete months or years.
- Using `TODAY()` in a report that must be reproducible. Pass the as-of date as a parameter instead
  (Module 48).
- Using a `YMD()` function that does not exist.

### Exercises

1. **Level 1:** Show today's date in three formats.
2. **Level 2:** Compute each customer's age in complete years at 30 September 2026.
3. **Level 3:** For each loan, find the first and last day of the month of its next EMI.
4. **Level 4 — Interview:** "Explain INTCK vs INTNX with an example."
5. **Level 5:** From a datetime transaction table, flag transactions between midnight and 5 a.m.
   and count them by weekday.

### ⭐ Interview questions

**Q1. How does SAS store dates?**
- *What they are testing:* the core model.
- *Strong answer:* "As numbers: a date is days since 1 January 1960, a datetime is seconds since
  midnight on 1 January 1960, and a time is seconds since midnight. Formats like DATE9. only change the
  display, so date arithmetic is just arithmetic."
- *Follow-up:* "How do you get the date from a datetime?" (`DATEPART`.)

**Q2. What does `intck('month', '31JAN2026'd, '01FEB2026'd)` return?**
- *Strong answer:* "1. INTCK counts interval boundaries crossed, not elapsed time. With the `'c'`
  method it returns 0."

**Q3. How do you get the last day of the current month?**
- *Strong answer:* "`intnx('month', today(), 0, 'e')`."

### Module wrap-up

- **I now know:** the SAS date, time and datetime model, date informats and formats, and the main date
  functions including INTCK and INTNX.
- **I can now:** calculate ages, tenures, DPD, due dates and month ends correctly.
- **Next:** Module 24 — functions by example.

---

## MODULE 24 — Functions by Example: A Banking Clean-Up

**Syllabus items:** 4.4 SAS functions with examples

**You will learn:** how character, numeric and date functions work together in one realistic program.
**Why it matters:** real work combines many functions in one step. **Before you start:** Modules
21–23.

### The task

A credit-card team needs a feature table for each card holder as of 30 September 2026: a clean name,
a masked card number, card type, age, months on book, days since the last transaction, credit
utilisation and two flags.

```sas
data work.cards;
    infile datalines dlm=',' dsd;
    length card_no $16 cust_name $25;
    input card_no $ cust_name $ dob :date9. open_date :date9. last_txn :date9.
          credit_limit balance;
    format dob open_date last_txn date9. credit_limit balance comma12.;
    datalines;
4111111111111111,  meera NAIR,14FEB1990,10JUN2018,28SEP2026,200000,186000
5500005555555559,RAHUL sharma,03NOV1985,01APR2022,02JUL2026,150000,12000
4012888888881881,zoya  khan ,25DEC2001,15JAN2026,,50000,
;
run;

data work.card_features;
    set work.cards;
    length name $25 masked_card $16 card_type $10 util_band $8;
    asof = '30SEP2026'd;

    /* character functions */
    name        = propcase(compbl(strip(cust_name)));
    masked_card = cats(repeat('X', 11), substr(card_no, 13));    /* REPEAT gives n+1 copies: 12 X's */
    card_type   = ifc(substr(card_no, 1, 1) = '4', 'VISA',
                  ifc(substr(card_no, 1, 1) = '5', 'MASTERCARD', 'OTHER'));

    /* date functions */
    age            = intck('year', dob, asof, 'c');
    months_on_book = intck('month', open_date, asof);
    days_since_txn = asof - last_txn;

    /* numeric functions */
    utilisation = round(sum(balance, 0) / credit_limit * 100, 0.1);   /* missing balance counts as 0 */

    if utilisation >= 90      then util_band = 'CRITICAL';
    else if utilisation >= 50 then util_band = 'HIGH';
    else                           util_band = 'NORMAL';

    dormant_flag = (missing(last_txn) or days_since_txn > 60);

    keep name masked_card card_type age months_on_book days_since_txn
         utilisation util_band dormant_flag;
run;
```

**Output**

| name | masked_card | card_type | age | months_on_book | days_since_txn | utilisation | util_band | dormant_flag |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Meera Nair | XXXXXXXXXXXX1111 | VISA | 36 | 99 | 2 | 93 | CRITICAL | 0 |
| Rahul Sharma | XXXXXXXXXXXX5559 | MASTERCARD | 40 | 53 | 90 | 8 | NORMAL | 1 |
| Zoya Khan | XXXXXXXXXXXX1881 | VISA | 24 | 8 | . | 0 | NORMAL | 1 |

### Line by line (the important lines)

| Code | What it does and why |
| --- | --- |
| `propcase(compbl(strip(cust_name)))` | Remove outer spaces, squash inner spaces, then capitalise each word. Functions run inside-out. |
| `cats(repeat('X', 11), substr(card_no, 13))` | 12 X's plus the last 4 digits. ⚠️ `REPEAT(s, n)` returns n + 1 copies. |
| `ifc(cond, 'VISA', ...)` | `IFC` returns one of two text values. It is a compact IF. Its result length defaults to 200, so `card_type` is given a LENGTH. |
| `intck('year', dob, asof, 'c')` | Age in **complete** years. Rahul turns 41 in November, so he is 40. |
| `intck('month', open_date, asof)` | Month boundaries from June 2018 to September 2026: 8 × 12 + 3 = 99 |
| `asof - last_txn` | Days since last use. July 2 to September 30 is 29 + 31 + 30 = 90 days. Zoya has no transaction, so it is missing (with a NOTE in the Log). |
| `sum(balance, 0) / credit_limit` | Treats a missing balance as zero so Zoya gets 0% instead of missing |
| `round(..., 0.1)` | 186,000 ÷ 200,000 = 93.0% |
| `(missing(last_txn) or days_since_txn > 60)` | A comparison returns 1 or 0, so this creates a 0/1 flag. The `missing()` check is needed: `. > 60` is false. |

### The same logic in PROC SQL

```sas
proc sql;
    create table work.card_features_sql as
    select propcase(compbl(strip(cust_name)))            as name length=25,
           cats(repeat('X', 11), substr(card_no, 13))    as masked_card length=16,
           intck('year', dob, '30SEP2026'd, 'c')         as age,
           '30SEP2026'd - last_txn                       as days_since_txn,
           round(sum(balance, 0) / credit_limit * 100, 0.1) as utilisation
    from work.cards;
quit;
```

📌 Most SAS functions work in PROC SQL too. One difference: in PROC SQL, `SUM(balance, 0)` with
**two or more arguments** is the row-wise SAS function; `SUM(balance)` with **one** argument is the
SQL aggregate that adds down rows.

### The same logic in Pandas

```python
import numpy as np
import pandas as pd

asof = pd.Timestamp("2026-09-30")
f = pd.DataFrame()
f["name"] = cards["cust_name"].str.strip().str.split().str.join(" ").str.title()
f["masked_card"] = "X" * 12 + cards["card_no"].str[-4:]
f["months_on_book"] = (asof.year - cards["open_date"].dt.year) * 12 + (asof.month - cards["open_date"].dt.month)
f["days_since_txn"] = (asof - cards["last_txn"]).dt.days
f["utilisation"] = (cards["balance"].fillna(0) / cards["credit_limit"] * 100).round(1)
```

### ⚠️ Common mistakes shown by this example

- `REPEAT` gives one more copy than you expect.
- `IFC`, `CATS`, `SCAN` and `TRANWRD` results default to length 200 without a LENGTH statement.
- A comparison involving a missing value (`. > 60`) is simply false. Decide what missing should mean.
- Nested functions run inside-out. Read them from the inside.

### Exercises

1. **Level 1:** Add the card holder's birth month name (`put(dob, monname.)`).
2. **Level 2:** Add `months_to_birthday` using INTNX and INTCK.
3. **Level 3:** Add a flag for cards whose holder is under 21 or over 70 years old.
4. **Level 4 — Interview:** "Why does REPEAT('X', 3) return four X's?"
5. **Level 5:** Extend the feature table with: average spend in the last 30 days (needs a transaction
   table and PROC SQL), and a "sudden jump" flag when this month's spend is more than three times the
   6-month average.

### Module wrap-up

- **I now know:** how to combine character, numeric and date functions in one clean program.
- **I can now:** build a feature table of the kind used in risk and marketing models.
- **Next:** Part V — PROC SQL.

**Part IV checklist:** ✓ 4.1 · ✓ 4.2 · ✓ 4.3 · ✓ 4.4 · ✓ 5.4 · ✓ 6.1 · ✓ 6.2 · ✓ 6.3

---

# Part V — PROC SQL (Modules 25–32)

You already know SQL from SQL Server. This Part focuses on **what is the same, what is different, and
what is missing** in SAS's version of SQL (PROC SQL in SAS 9.4).

## MODULE 25 — PROC SQL Basics: Creating Tables and Inserting Rows

**Syllabus items:** 4.5 SAS SQL Programming · 4.6 Creating a table using PROC SQL · 4.7 Inserting
values using PROC SQL · 4.14 Creating a new table from an existing table · 4.15 Creating a new table
by limiting records · 7.1, 7.2, 7.3 (same topics in Session 7)

**You will learn:** how PROC SQL works, how it differs from T-SQL, and how to create and fill tables.
**Why it matters:** many SAS jobs mix DATA steps and PROC SQL, and interviewers test the differences.
**Before you start:** Modules 3 and 4.

### 🧠 How PROC SQL works (4.5)

```sas
proc sql;
    select * from work.txn;                 /* a query: prints a report */
    create table work.big as                /* another statement: creates a table */
        select * from work.txn where amount > 50000;
quit;                                       /* ends PROC SQL */
```

- Each SQL statement ends with `;` and runs straight away. No `RUN;` is needed.
- `QUIT;` ends the procedure.
- A plain `SELECT` **prints** the result. `CREATE TABLE ... AS SELECT` **stores** it.
- In PROC SQL a **table** is a SAS dataset, a **row** is an observation and a **column** is a variable.
- You can use almost any SAS function, format or informat inside PROC SQL.

**Useful PROC SQL options**

| Option | Effect |
| --- | --- |
| `NUMBER` | Adds a row-number column to printed output |
| `NOPRINT` | Runs queries without printing (useful with `INTO`, Module 50) |
| `FEEDBACK` | Writes the expanded query (with `*` replaced by column names) to the Log |
| `OUTOBS=n` | Stops after `n` output rows |
| `INOBS=n` | Reads only `n` rows from each table (handy for testing) |

### 🔥 PROC SQL vs SQL Server (T-SQL)

| Feature | SQL Server | PROC SQL (SAS 9.4) |
| --- | --- | --- |
| Statement end | `;` optional, `GO` batches | `;` required; `QUIT;` ends the procedure |
| First n rows | `SELECT TOP 10` | `PROC SQL OUTOBS=10;` |
| Window functions (`ROW_NUMBER() OVER`) | Yes | **No.** Use the DATA step or PROC RANK. |
| Common table expressions (`WITH`) | Yes | **No.** Use subqueries, views or temporary tables. |
| Data types | Many (INT, DECIMAL, VARCHAR, DATE...) | Only numeric and character. Others are mapped to these. |
| Column alias in WHERE | Not allowed | Allowed with the `CALCULATED` keyword |
| Mix detail columns with aggregates | Error unless in GROUP BY | Allowed: SAS "remerges" and writes a NOTE |
| String concatenation | `+` or `CONCAT` | `\|\|` or `CATX` |
| `ISNULL(a, b)` | Yes | Use `COALESCE(a, b)` |
| Text comparison | Usually case-insensitive (depends on collation) | **Case-sensitive** |
| Empty string vs NULL | Different | A blank character value **is** missing |
| `7 / 2` | `3` (integer division) | `3.5` |
| Date literal | `'2026-01-02'` | `'02JAN2026'd` |
| Identity column | `IDENTITY(1,1)` | None. Number rows in a DATA step. |
| Stored procedures | `CREATE PROCEDURE` | **None.** See Module 32. |
| `TRUNCATE TABLE` | Yes | **No.** See Module 26. |
| `UPDATE ... FROM ... JOIN` | Yes | No. Use a correlated subquery (Module 26). |

### Creating a table and inserting values (4.6, 4.7)

```sas
proc sql;
    create table work.accounts
        (acct_id    char(8)   label='Account ID',
         cust_id    char(5),
         product    char(12),
         open_date  num       format=date9.,
         balance    num       format=comma14.2,
         status     char(1));

    insert into work.accounts
        values ('A0000001', 'C101', 'SAVINGS',     '15MAR2019'd,  250000.50, 'A')
        values ('A0000002', 'C102', 'CURRENT',     '01NOV2021'd,   18000.00, 'A')
        values ('A0000003', 'C101', 'CREDIT CARD', '20JAN2024'd,  -45000.00, 'A')
        values ('A0000004', 'C103', 'SAVINGS',     '22JUL2024'd,       0.00, 'D');

    insert into work.accounts
        set acct_id = 'A0000005', cust_id = 'C104', product = 'LOAN',
            open_date = '05MAY2025'd, balance = 900000, status = 'A';
quit;
```

**Log**

```text
NOTE: Table WORK.ACCOUNTS created, with 0 rows and 6 columns.
NOTE: 4 rows were inserted into WORK.ACCOUNTS.
NOTE: 1 row was inserted into WORK.ACCOUNTS.
```

| Part | Meaning |
| --- | --- |
| `char(8)` | Character column of length 8. `varchar(8)` is accepted but stored as fixed `char`. |
| `num` | Numeric column (8 bytes). `int`, `decimal`, `float` are also accepted and stored as numeric. |
| `format=`, `label=` | SAS attributes attached to the column |
| Several `values (...)` clauses | PROC SQL lets you list many rows in one INSERT, with **no commas** between them |
| `insert ... set col = value, ...` | Another way to insert one row, naming each column |

**See a table's structure as SQL:**

```sas
proc sql;
    describe table work.accounts;     /* writes the CREATE TABLE statement to the Log */
quit;
```

### Creating a new table from an existing one (4.14)

```sas
proc sql;
    /* copy some rows and columns */
    create table work.active_accounts as
    select acct_id, cust_id, product, balance
    from work.accounts
    where status = 'A';

    /* copy only the structure (no rows), then fill it */
    create table work.savings like work.accounts;
    insert into work.savings
        select * from work.accounts where product = 'SAVINGS';
quit;
```

`work.active_accounts` has 4 rows (A0000004 is dormant). `work.savings` has 2 rows.

### Creating a new table by limiting records (4.15)

There is no `TOP` in PROC SQL. Use `OUTOBS=`:

```sas
proc sql outobs=3;
    create table work.top3_balance as
    select acct_id, balance
    from work.accounts
    order by balance desc;
quit;
```

**Output:** A0000005 (900,000.00), A0000001 (250,000.50), A0000002 (18,000.00).

The Log shows `WARNING: Statement terminated early due to OUTOBS=3 option.` This is expected.

| Option | Limits | Typical use |
| --- | --- | --- |
| `OUTOBS=n` | Rows **written** by each statement | Top-n reports |
| `INOBS=n` | Rows **read** from each table | Testing a heavy join on a small slice |
| `FROM tbl(obs=n)` | Rows read from one table (dataset option) | Same, for one table only |

⚠️ `OUTOBS=` stays in force for every statement until the next `PROC SQL` or a `RESET` statement.

### ⚠️ Common mistakes

- Expecting `SELECT TOP 10` to work.
- Expecting `7/2` to be 3.
- Forgetting that text comparisons are case-sensitive in SAS.
- Writing commas between `VALUES` clauses in a multi-row INSERT (that is the SQL Server style).
- Forgetting `QUIT;`.

### Exercises

1. **Level 1:** Create a `branches` table with 4 columns and insert 5 rows.
2. **Level 2:** Create a table with the same structure as `work.accounts` and insert only CURRENT
   accounts.
3. **Level 3:** Use `INOBS=` to test a query on 100 rows of a big table, then remove it.
4. **Level 4 — Interview:** "Name five differences between PROC SQL and SQL Server."
5. **Level 5:** Rewrite a SQL Server script that uses `TOP`, `ISNULL`, integer division and a CTE as
   working PROC SQL.

### ⭐ Interview questions

**Q. How is PROC SQL different from ANSI or SQL Server SQL?**
- *What they are testing:* whether you can move SQL skills into SAS safely.
- *Strong answer:* "PROC SQL works on SAS datasets and supports SAS functions, formats and the
  CALCULATED keyword. It has no TOP (I use OUTOBS), no window functions or CTEs in SAS 9.4, no stored
  procedures and no TRUNCATE. It remerges aggregates with detail rows instead of failing, division is
  not integer division, comparisons are case-sensitive, and there are only two data types."
- *Follow-up:* "How would you number rows within a group, then?" (DATA step with FIRST., Module 34.)

### Module wrap-up

- **I now know:** PROC SQL structure and options, the main differences from SQL Server, CREATE TABLE,
  INSERT, CREATE TABLE AS / LIKE, OUTOBS and INOBS.
- **I can now:** create and fill tables with PROC SQL and avoid T-SQL habits that fail in SAS.
- **Next:** Module 26 — changing tables.

---

## MODULE 26 — Changing Tables: Columns, UPDATE, DELETE, DROP and Truncate

**Syllabus items:** 4.8 Adding columns · 4.9 Dropping columns · 4.10 Renaming columns · 4.11 Dropping
tables · 4.12 Deleting tables · 4.13 Truncating tables · 7.15 UPDATE statement · 7.16 DELETE statement

**You will learn:** how to change a table's columns and rows in PROC SQL, and what to do when PROC SQL
has no direct command. **Why it matters:** maintaining reference tables and status flags is routine
work. **Before you start:** Module 25.

### Adding, changing and dropping columns (4.8, 4.9)

```sas
proc sql;
    alter table work.accounts
        add risk_grade char(2) label='Risk grade',
            last_review num format=date9.;

    alter table work.accounts
        modify product char(20) format=$20.;    /* change length, format or label */

    alter table work.accounts
        drop last_review;
quit;
```

New columns start as missing for every existing row.

### Renaming columns (4.10)

⚠️ PROC SQL has **no** `ALTER TABLE ... RENAME COLUMN`. Use one of these:

```sas
/* 1. Best: rename in place. Only the header changes, so it is instant on any size. */
proc datasets library=work nolist;
    modify accounts;
    rename balance = ledger_balance;
quit;

/* 2. Rename while creating a new table */
proc sql;
    create table work.accounts2 as
    select acct_id, cust_id, ledger_balance as balance
    from work.accounts;
quit;

/* 3. A RENAME= dataset option inside PROC SQL */
proc sql;
    create table work.accounts3 as
    select * from work.accounts(rename=(ledger_balance=bal));
quit;
```

### UPDATE: changing values (7.15)

```sas
proc sql;
    /* 1. a simple update */
    update work.accounts
        set status = 'D'
        where product = 'SAVINGS' and ledger_balance = 0;

    /* 2. an update with CASE (charge 1% on negative credit-card balances) */
    update work.accounts
        set ledger_balance = case
                                when product = 'CREDIT CARD' and ledger_balance < 0
                                then round(ledger_balance * 1.01, 0.01)
                                else ledger_balance
                             end;
quit;
```

**Log**

```text
NOTE: 1 row was updated in WORK.ACCOUNTS.
NOTE: 5 rows were updated in WORK.ACCOUNTS.
```

The second UPDATE has no WHERE, so it touches all 5 rows, but only A0000003 actually changes:
-45,000 becomes -45,450.

**Updating from another table:** PROC SQL has no `UPDATE ... FROM ... JOIN`. Use a correlated
subquery:

```sas
data work.status_changes;
    input acct_id $ new_status $;
    datalines;
A0000002 F
A0000005 C
;
run;

proc sql;
    update work.accounts as a
        set status = (select s.new_status
                      from work.status_changes as s
                      where s.acct_id = a.acct_id)
        where a.acct_id in (select acct_id from work.status_changes);
quit;
```

⚠️ Without the outer `WHERE`, every account **not** in `status_changes` would get a missing status,
because the subquery returns nothing for them.

### DELETE: removing rows (7.16) and "deleting tables" (4.12)

```sas
proc sql;
    delete from work.accounts
        where status = 'C';                  /* remove closed accounts */

    delete from work.savings;                /* no WHERE: remove ALL rows, keep the table */
quit;
```

🧠 In a SAS dataset, `DELETE` marks rows as deleted. The file does not shrink until the dataset is
rewritten. PROC CONTENTS shows a "Deleted Observations" count.

### DROP TABLE: removing a table (4.11)

```sas
proc sql;
    drop table work.savings, work.top3_balance;     /* several at once */
quit;
```

The same thing with PROC DATASETS: `proc datasets library=work nolist; delete savings top3_balance;
quit;`

### Truncating tables (4.13)

⚠️ PROC SQL has **no** `TRUNCATE TABLE` for SAS datasets. The options:

| Goal | SAS way | Notes |
| --- | --- | --- |
| Remove all rows, keep the table | `delete from work.t;` | Rows marked deleted; file keeps its size |
| Remove all rows **and** reclaim space | `data work.t; set work.t(obs=0); run;` | Rewrites as an empty table with the same columns |
| Empty copy under a new name | `create table work.t_empty like work.t;` | Structure only |
| Truncate a **database** table | `execute (truncate table stg.daily_load) by dwcon;` | Explicit pass-through (Module 11) |

### SQL Server comparison

| Task | SQL Server | SAS |
| --- | --- | --- |
| Add column | `ALTER TABLE t ADD c INT` | `alter table t add c num;` |
| Rename column | `EXEC sp_rename 't.old', 'new', 'COLUMN'` | `PROC DATASETS MODIFY ... RENAME` |
| Update from join | `UPDATE a SET ... FROM a JOIN b ON ...` | Correlated subquery, or a DATA step MERGE / UPDATE (Module 39) |
| Remove all rows | `TRUNCATE TABLE t` | `delete from t;` or a DATA step with `obs=0` |

**Pandas:** `df["c"] = None`, `df.drop(columns=...)`, `df.rename(columns=...)`, `df.loc[mask, "c"] =
v`, `df = df[~mask]`, `df.iloc[0:0]`.

### 💼 Banking scenario

Each night, a dormancy job sets `status = 'D'` for savings accounts with no customer-initiated
transaction for 24 months. The UPDATE uses a WHERE with `last_cust_txn_date <
intnx('month', &asof, -24, 's')`, and a control step counts rows before and after so the operations
team can sign off the change.

### ⚠️ Common mistakes

- Looking for `RENAME COLUMN` or `TRUNCATE` in PROC SQL.
- A correlated UPDATE without an outer WHERE, which wipes values for non-matching rows.
- Running `DELETE` without `WHERE` by accident. There is no undo. Test with `SELECT COUNT(*)` and the
  same WHERE first.

### Exercises

1. **Level 1:** Add a column `branch char(5)` and fill it with UPDATE.
2. **Level 2:** Rename a column with PROC DATASETS and check with PROC CONTENTS.
3. **Level 3:** Update balances from a `daily_postings` table using a correlated subquery.
4. **Level 4 — Interview:** "How do you truncate a SAS table?"
5. **Level 5:** Write a safe "close accounts" job that counts, updates, re-counts and logs the change.

### ⭐ Interview questions

**Q. How do you rename a column with PROC SQL?**
- *Strong answer:* "PROC SQL has no RENAME COLUMN. I either alias it in a CREATE TABLE AS SELECT, use
  the RENAME= dataset option, or, best for big tables, PROC DATASETS MODIFY with RENAME, which only
  changes the header and does not rewrite the data."

### Module wrap-up

- **I now know:** ALTER TABLE ADD/MODIFY/DROP, renaming, UPDATE, correlated updates, DELETE, DROP
  TABLE, and the truncate options.
- **I can now:** maintain tables safely in PROC SQL.
- **Next:** Module 27 — querying.

---

## MODULE 27 — Querying: Selecting, Aliases, Expressions, WHERE and Calculated Columns

**Syllabus items:** 7.4 Selecting observations · 7.7 Table aliases and column aliases · 7.8
Expressions · 7.9 WHERE clause with operators and operands · 4.21 Creating calculated columns · 7.19
Calculated fields (same topic)

**You will learn:** the SELECT statement the SAS way, including the very useful `CALCULATED` keyword.
**Why it matters:** this is everyday querying. **Before you start:** Modules 14 and 25.

### Selecting observations (7.4)

```sas
proc sql;
    select txn_id, cust_id, amount
    from work.txn
    where channel = 'ONLINE'
    order by amount desc;
quit;
```

**Output**

| txn_id | cust_id | amount |
| --- | --- | --- |
| T002 | C102 | 125,000 |
| T006 | C101 | 78,000 |
| T004 | C103 | . |

Missing values sort lowest, so T004 is last in descending order.

`select distinct channel from work.txn;` returns one row per channel. Add `ORDER BY` if the order
matters.

### Table and column aliases (7.7)

```sas
proc sql;
    select t.txn_id,
           c.name               as customer_name   label='Customer',
           t.amount             as txn_amount      format=comma12.2
    from work.txn       as t
         inner join
         work.customers as c
         on t.cust_id = c.cust_id;
quit;
```

- **Table alias:** `work.txn as t` (the word `AS` is optional). Needed when two tables share column
  names.
- **Column alias:** `c.name as customer_name`. Becomes the column name in the result.
- **Column modifiers:** `label=`, `format=` and `length=` set SAS attributes in the result.

### Expressions (7.8)

You can calculate anything in the SELECT list.

```sas
proc sql;
    select txn_id,
           amount * 0.18                       as gst,
           upcase(channel)                     as channel_uc,
           catx('-', cust_id, txn_id)          as txn_key length=12,
           year(txn_date)                      as txn_year,
           case when amount >= 50000 then 'LARGE' else 'NORMAL' end as size_band
    from work.txn;
quit;
```

### WHERE operators and operands (7.9)

PROC SQL supports everything from DATA step WHERE (Module 14) plus SQL features:

| Operator | Example |
| --- | --- |
| `=`, `<>`, `ne`, `>`, `<`, `>=`, `<=` | `where amount >= 50000` |
| `AND`, `OR`, `NOT` | `where channel = 'ONLINE' and amount > 0` |
| `IN (list)` / `IN (subquery)` | `where cust_id in (select cust_id from work.blacklist)` |
| `BETWEEN a AND b` | `where txn_date between '01JAN2026'd and '31JAN2026'd` |
| `LIKE` with `%` and `_` | `where name like 'A%'` |
| `IS NULL` / `IS MISSING` | `where amount is missing` |
| `CONTAINS` | `where name contains 'Khan'` |
| `EXISTS (subquery)` | `where exists (select 1 from work.acct a where a.cust_id = c.cust_id)` |
| `ANY` / `ALL` with a subquery | `where amount > all (select amount from work.txn where channel = 'ATM')` |
| `=*` (sounds like) | `where name =* 'Bilal Kan'` |

### 🔥 Calculated columns and the CALCULATED keyword (4.21, 7.19)

In SQL Server you cannot use a column alias in the WHERE clause or reuse it in the same SELECT. In
PROC SQL you can, with `CALCULATED`:

```sas
proc sql;
    create table work.txn_tax as
    select txn_id,
           amount,
           amount * 0.18             as gst       format=comma12.2,
           calculated gst + amount   as total_due format=comma12.2
    from work.txn
    where calculated gst > 1000;
quit;
```

**Output**

| txn_id | amount | gst | total_due |
| --- | --- | --- | --- |
| T002 | 125,000 | 22,500.00 | 147,500.00 |
| T005 | 20,000 | 3,600.00 | 23,600.00 |
| T006 | 78,000 | 14,040.00 | 92,040.00 |

**Why these rows:** GST over 1,000 means an amount over about 5,556. T001 (5,000) gives 900, T003
gives 414, and T004 is missing.

Without `CALCULATED` you get `ERROR: The following columns were not found in the contributing tables:
gst.`

**The SQL Server way** (for comparison): repeat the expression, or use `CROSS APPLY` or a CTE.

```sql
SELECT txn_id, amount, amount * 0.18 AS gst, amount * 1.18 AS total_due
FROM dbo.txn
WHERE amount * 0.18 > 1000;
```

**Pandas:**

```python
out = txn.assign(gst=txn["amount"] * 0.18)
out = out.assign(total_due=out["gst"] + out["amount"])
out = out[out["gst"] > 1000]
```

### 💼 Banking scenario

A merchant-risk query computes `refund_rate = refund_count / sale_count` and must keep only merchants
with `refund_rate > 0.10` **and** at least 200 sales. With `CALCULATED refund_rate` in HAVING, the
rate is written once, so the formula cannot drift between the SELECT and the filter.

### ⚠️ Common mistakes

- Using an alias in WHERE without `CALCULATED`.
- Forgetting table aliases when column names repeat: `ERROR: Ambiguous reference, column cust_id is in
  more than one table.`
- Forgetting that text comparisons are case-sensitive.

### Exercises

1. **Level 1:** Select ATM and POS transactions over 1,000, newest first.
2. **Level 2:** Add a `net_amount` column (amount minus a 1% fee) and filter on it with CALCULATED.
3. **Level 3:** Find customers with no transactions using `NOT EXISTS`.
4. **Level 4 — Interview:** "What does the CALCULATED keyword do?"
5. **Level 5:** Find transactions larger than every ATM transaction using `ALL`.

### ⭐ Interview questions

**Q. What does CALCULATED do in PROC SQL?**
- *Strong answer:* "It lets me reference a column alias created in the same SELECT, in another SELECT
  expression, in WHERE or in HAVING. SQL Server cannot do that; you have to repeat the expression or
  use a subquery or CTE."

### Module wrap-up

- **I now know:** SELECT, DISTINCT, aliases, column modifiers, expressions, WHERE operators,
  subqueries in WHERE, and CALCULATED.
- **I can now:** write any filtering query a SQL Server analyst would, in PROC SQL.
- **Next:** Module 28 — CASE WHEN.

---

## MODULE 28 — CASE WHEN and Nested CASE

**Syllabus items:** 4.18 CASE WHEN · 7.10 CASE WHEN (same topic) · 7.11 Nested CASE WHEN

**You will learn:** both forms of CASE, nesting, and conditional aggregation. **Why it matters:**
CASE is how business rules are written in SQL. **Before you start:** Modules 15 and 27.

### Two forms of CASE

```sas
/* searched CASE: any conditions */
case
    when fico is missing then 'NO SCORE'
    when fico >= 750     then 'LOW'
    when fico >= 650     then 'MEDIUM'
    else 'HIGH'
end

/* simple CASE: compare one value */
case segment
    when 'R' then 'Retail'
    when 'C' then 'Corporate'
    else 'Other'
end
```

- Conditions are checked from top to bottom. The first true one wins.
- Without `ELSE`, unmatched rows get a missing value.
- PROC SQL sets the result's length from the **longest** value, so the DATA step truncation trap from
  Module 7 does not happen here.

### Nested CASE (7.11)

```sas
proc sql;
    create table work.cust_offer as
    select c.cust_id,
           c.segment,
           c.fico,
           case
               when c.fico is missing then 'NO SCORE'
               when c.fico >= 750     then 'LOW'
               when c.fico >= 650     then 'MEDIUM'
               else 'HIGH'
           end as risk_band,
           case c.segment
               when 'R' then case when c.fico >= 700 then 'PREMIUM CARD'
                                  else 'CLASSIC CARD' end
               when 'C' then 'CORPORATE LOAN'
               else 'REVIEW'
           end as offer length=15
    from work.customers as c;
quit;
```

**Output**

| cust_id | segment | fico | risk_band | offer |
| --- | --- | --- | --- | --- |
| C101 | R | 742 | MEDIUM | PREMIUM CARD |
| C102 | C | 688 | MEDIUM | CORPORATE LOAN |
| C103 | R | 615 | HIGH | CLASSIC CARD |
| C104 | S | . | NO SCORE | REVIEW |

📌 Keep nesting shallow. Two levels are readable. Deeper logic is clearer as a format (Module 19) or a
lookup table.

### Conditional aggregation (CASE inside SUM)

```sas
proc sql;
    select cust_id,
           sum(case when channel = 'ONLINE' then amount else 0 end)  as online_amt  format=comma12.,
           sum(case when channel ne 'ONLINE' then amount else 0 end) as offline_amt format=comma12.
    from work.txn
    group by cust_id;
quit;
```

**Output**

| cust_id | online_amt | offline_amt |
| --- | --- | --- |
| C101 | 78,000 | 7,300 |
| C102 | 125,000 | 20,000 |
| C103 | . | 0 |

**Why C103's online amount is missing:** its only ONLINE row (T004) has a missing amount, so the CASE
returns missing. SUM ignores missing values, but if **every** value in the group is missing the result
is missing. Use `coalesce(amount, 0)` inside the CASE if you want 0.

This pattern is also how you **pivot** in SQL (Module 36).

### SQL Server and Pandas

CASE syntax is the same in SQL Server. In Pandas use `np.select` (Module 15) for searched CASE,
`.map()` for simple CASE, and `pivot_table` or `groupby` with masks for conditional sums.

### ⚠️ Common mistakes

- Putting a broad condition before a narrow one.
- Forgetting missing values: `fico < 650` is true for missing in SAS.
- Forgetting `END`.
- Expecting a group of only-missing values to SUM to 0.

### Exercises

1. **Level 1:** Band transactions into SMALL (<10,000), MEDIUM (<1,00,000) and LARGE.
2. **Level 2:** Use simple CASE to turn channel codes into descriptions.
3. **Level 3:** Write a nested CASE for loan pricing by segment and FICO band.
4. **Level 4 — Interview:** "What happens when no WHEN matches and there is no ELSE?"
5. **Level 5:** Produce one row per customer with transaction counts per channel using conditional
   aggregation.

### ⭐ Interview questions

**Q. How do you pivot data in PROC SQL?**
- *Strong answer:* "PROC SQL has no PIVOT operator. I use conditional aggregation:
  `SUM(CASE WHEN month = 'JAN' THEN amount ELSE 0 END) AS jan` for each column, grouped by the row key.
  For many or unknown columns I use PROC TRANSPOSE instead."

### Module wrap-up

- **I now know:** searched and simple CASE, nesting, missing-value handling, and conditional sums.
- **I can now:** express business rules and simple pivots in PROC SQL.
- **Next:** Module 29 — summarising data.

---

## MODULE 29 — Summarising Data, WHERE vs HAVING, and the Order of Clauses

**Syllabus items:** 4.16 Sorting and summarizing a table · 4.17 WHERE vs HAVING · 7.12 Summarizing
data · 7.13 WHERE vs HAVING · 7.14 Sequence of SQL clauses

**You will learn:** GROUP BY with summary functions, the SAS "remerge" feature, WHERE vs HAVING, and
the order SQL clauses are written and run. **Why it matters:** summaries are the core of reporting,
and WHERE vs HAVING is a standard interview question. **Before you start:** Module 27.

### Sorting and summarising (4.16, 7.12)

```sas
proc sql;
    create table work.cust_summary as
    select cust_id,
           count(*)       as txn_count,
           count(amount)  as amount_count,
           sum(amount)    as total_amt  format=comma12.,
           avg(amount)    as avg_amt    format=comma12.2,
           max(txn_date)  as last_txn   format=date9.
    from work.txn
    group by cust_id
    order by total_amt desc;
quit;
```

**Output**

| cust_id | txn_count | amount_count | total_amt | avg_amt | last_txn |
| --- | --- | --- | --- | --- | --- |
| C102 | 2 | 2 | 145,000 | 72,500.00 | 09JAN2026 |
| C101 | 3 | 3 | 85,300 | 28,433.33 | 12JAN2026 |
| C103 | 1 | 0 | . | . | 07JAN2026 |

**Why:** `COUNT(*)` counts rows. `COUNT(amount)` counts non-missing values, so C103 has 1 row but 0
amounts. SUM and AVG ignore missing values; a group with no values gives missing. Missing sorts lowest,
so C103 is last in descending order.

**Summary functions in PROC SQL**

| Function | Meaning |
| --- | --- |
| `COUNT(*)` | Number of rows |
| `COUNT(col)`, `N(col)` | Number of non-missing values |
| `COUNT(DISTINCT col)` | Number of different non-missing values |
| `NMISS(col)` | Number of missing values |
| `SUM`, `AVG` (or `MEAN`), `MIN`, `MAX` | The usual |
| `STD`, `VAR`, `RANGE` | Spread |

📌 For medians and percentiles, use PROC MEANS or PROC UNIVARIATE (Modules 41–42).

📌 PROC SQL allows `ORDER BY` with column positions: `order by 4 desc` sorts by the fourth column.

### 🔥 Remerging: a SAS-only feature

In SQL Server, every SELECT column must be in GROUP BY or inside an aggregate. PROC SQL relaxes this.
It calculates the aggregate per group and **joins it back** to every detail row:

```sas
proc sql;
    select txn_id, cust_id, amount,
           sum(amount)                    as cust_total format=comma12.,
           amount / calculated cust_total as share      format=percent8.1
    from work.txn
    group by cust_id
    order by cust_id, txn_id;
quit;
```

**Log:** `NOTE: The query requires remerging summary statistics back with the original data.`

**Output**

| txn_id | cust_id | amount | cust_total | share |
| --- | --- | --- | --- | --- |
| T001 | C101 | 5,000 | 85,300 | 5.9% |
| T003 | C101 | 2,300 | 85,300 | 2.7% |
| T006 | C101 | 78,000 | 85,300 | 91.4% |
| T002 | C102 | 125,000 | 145,000 | 86.2% |
| T005 | C102 | 20,000 | 145,000 | 13.8% |
| T004 | C103 | . | . | . |

**SQL Server equivalent** (a window function):

```sql
SELECT txn_id, cust_id, amount,
       SUM(amount) OVER (PARTITION BY cust_id) AS cust_total,
       amount * 1.0 / SUM(amount) OVER (PARTITION BY cust_id) AS share
FROM dbo.txn;
```

**Pandas:** `txn["cust_total"] = txn.groupby("cust_id")["amount"].transform("sum")`

⚠️ Remerging is useful, but when it happens **by accident** (you forgot a column in GROUP BY) it
silently returns detail rows instead of one row per group. Always read the Log for that NOTE.

### 🔥 WHERE vs HAVING (4.17, 7.13)

| | WHERE | HAVING |
| --- | --- | --- |
| Filters | **Rows**, before grouping | **Groups**, after grouping |
| Can use aggregates (SUM, COUNT) | ✗ No | ✓ Yes |
| Can use `CALCULATED` aggregates | ✗ | ✓ |
| Runs | Early (less data to group) | Late |

```sas
proc sql;
    select cust_id, sum(amount) as total_amt format=comma12.
    from work.txn
    where channel ne 'ATM'                    /* rows: drop ATM before grouping */
    group by cust_id
    having calculated total_amt > 50000       /* groups: keep big customers */
    order by cust_id;
quit;
```

**Output**

| cust_id | total_amt |
| --- | --- |
| C101 | 80,300 |
| C102 | 125,000 |

**Step by step:** WHERE removes T001 and T005 (ATM). The remaining rows group into C101 (2,300 +
78,000 = 80,300), C102 (125,000) and C103 (missing). HAVING keeps groups over 50,000.

🚀 Put row filters in WHERE, not HAVING. Filtering early means less data to group.

⚠️ `HAVING` without `GROUP BY` treats the whole table as one group.

### Order of clauses (7.14)

**The order you write them:**

```text
SELECT  ->  FROM  ->  WHERE  ->  GROUP BY  ->  HAVING  ->  ORDER BY
```

Memory trick: **S**o **F**ew **W**orkers **G**o **H**ome **O**n time.

**The order SQL runs them (logical order):**

```text
1. FROM      which tables, joined how
2. WHERE     which rows
3. GROUP BY  which groups
4. HAVING    which groups to keep
5. SELECT    which columns and calculations
6. ORDER BY  the final sort
```

📌 This explains the rules: WHERE cannot use aggregates (groups do not exist yet), and in SQL Server a
SELECT alias cannot be used in WHERE (SELECT runs later). PROC SQL's `CALCULATED` keyword is SAS's way
around the second rule.

### PROC SQL vs PROC SUMMARY vs Pandas

| Task | PROC SQL | PROC SUMMARY / MEANS | Pandas |
| --- | --- | --- | --- |
| Totals per group | `GROUP BY` | `CLASS` + `OUTPUT` (Module 41) | `groupby().agg()` |
| Median, percentiles | Not built in | `MEDIAN`, `P90` | `.median()`, `.quantile()` |
| Many statistics on many columns | Long SELECT | Short | `.agg(["sum", "mean"])` |
| Group-level filter | `HAVING` | Filter the output dataset | Filter after `agg` |

### 💼 Banking scenario

A branch manager wants branches where **average** online transaction value in September is above
₹25,000, counting only successful transactions:

```sas
proc sql;
    create table work.branch_online as
    select branch,
           count(*)    as txns,
           avg(amount) as avg_amt format=comma12.2
    from bank.transactions
    where channel = 'ONLINE'
      and status = 'SUCCESS'
      and txn_date between '01SEP2026'd and '30SEP2026'd
    group by branch
    having calculated avg_amt > 25000
    order by avg_amt desc;
quit;
```

### ⚠️ Common mistakes

- Putting a row condition in HAVING (slow) or an aggregate in WHERE (error).
- Forgetting a column in GROUP BY and getting an accidental remerge.
- Using `COUNT(*)` when you mean `COUNT(DISTINCT cust_id)`.

### Exercises

1. **Level 1:** Count transactions and total amount per channel.
2. **Level 2:** Find channels with more than 2 transactions using HAVING.
3. **Level 3:** Show each transaction's share of its channel's total using remerging.
4. **Level 4 — Interview:** "What is the difference between WHERE and HAVING?" and "In what order are
   SQL clauses processed?"
5. **Level 5:** For each customer, show total spend, the number of distinct channels used, and the
   share of spend that was online, keeping customers with at least 2 channels.

### ⭐ Interview questions

**Q1. What is remerging in PROC SQL?**
- *Strong answer:* "When a SELECT mixes detail columns with aggregates, PROC SQL computes the aggregate
  per group and merges it back onto each detail row, with a NOTE in the Log. It replaces what SQL
  Server does with `SUM() OVER (PARTITION BY ...)`. If it happens by mistake it hides a missing GROUP BY
  column, so I check the Log."

**Q2. WHERE vs HAVING?**
- *Strong answer:* "WHERE filters rows before grouping and cannot use aggregates. HAVING filters
  groups after aggregation. For performance I put every row-level condition in WHERE."

### Module wrap-up

- **I now know:** summary functions, GROUP BY, ORDER BY, remerging, WHERE vs HAVING, and the order of
  clauses.
- **I can now:** write correct and efficient summary queries.
- **Next:** Module 30 — COALESCE, row numbers and SQL functions.

---

## MODULE 30 — COALESCE, Row Numbers and SQL Functions

**Syllabus items:** 4.22 COALESCE · 4.23 SAS SQL functions · 7.5 Adding row numbers · 7.6 Creating row
numbers · 7.20 COALESCE · 7.21 Character, numeric and datetime functions · 7.22 SAS SQL functions with
examples

**You will learn:** COALESCE, reliable ways to number rows, and using SAS functions inside PROC SQL.
**Why it matters:** missing-value handling and row numbering come up in almost every query. **Before
you start:** Modules 21–23 and 29.

### COALESCE (4.22, 7.20)

`COALESCE(a, b, c)` returns the first value that is not missing.

```sas
proc sql;
    select cust_id,
           fico,
           coalesce(fico, 0)             as fico_or_zero,
           coalesce(city, 'UNKNOWN')     as city_clean
    from work.customers;
quit;
```

| cust_id | fico | fico_or_zero | city_clean |
| --- | --- | --- | --- |
| C101 | 742 | 742 | Mumbai |
| C102 | 688 | 688 | Delhi |
| C103 | 615 | 615 | Pune |
| C104 | . | 0 | Chennai |

- In PROC SQL, `COALESCE` works for numbers **and** text.
- In the DATA step, use `COALESCE` for numbers and `COALESCEC` for text.
- Its most important use is combining keys in a **full join** (Module 31).

| SAS | SQL Server | Pandas |
| --- | --- | --- |
| `coalesce(a, b)` | `COALESCE(a, b)` or `ISNULL(a, b)` | `df["a"].fillna(df["b"])` / `combine_first` |

### Row numbers (7.5, 7.6)

⚠️ PROC SQL in SAS 9.4 has **no** `ROW_NUMBER()`. There are three approaches.

**1. The NUMBER option** (for printed reports only):

```sas
proc sql number;
    select txn_id, amount from work.txn order by amount desc;
quit;
```

The output gets a `Row` column: 1, 2, 3, and so on. Nothing is stored.

**2. The MONOTONIC() function** (stored, but use with care):

```sas
proc sql;
    create table work.txn_numbered as
    select monotonic() as row_num, *
    from work.txn
    where channel = 'ONLINE';
quit;
```

This gives 1, 2, 3 for T002, T004 and T006. ⚠️ `MONOTONIC()` is **not officially documented or
supported** by SAS. It numbers rows as they are read, so with `ORDER BY`, `GROUP BY` or joins the
numbers can be wrong. Do not use it in production.

**3. The reliable way:** create the table in PROC SQL, then number it in a DATA step.

```sas
proc sql;
    create table work.online_sorted as
    select * from work.txn
    where channel = 'ONLINE'
    order by amount desc;
quit;

data work.online_sorted;
    set work.online_sorted;
    row_num = _n_;
run;
```

For row numbers **within groups** (like `ROW_NUMBER() OVER (PARTITION BY ...)`), use FIRST. in a DATA
step (Module 34) or PROC RANK (Module 35).

### SAS functions inside PROC SQL (4.23, 7.21, 7.22)

Almost every DATA step function works in PROC SQL.

```sas
proc sql;
    select txn_id,
           upcase(channel)                          as channel_uc,       /* character */
           substr(txn_id, 2)                        as txn_num,
           catx('|', cust_id, channel)              as cust_channel length=15,
           round(amount * 1.18, 1)                  as amt_with_gst,     /* numeric */
           ceil(amount / 1000)                      as thousands,
           year(txn_date)                           as yr,               /* date */
           intnx('month', txn_date, 0, 'e')         as month_end format=date9.,
           '30SEP2026'd - txn_date                  as days_old,
           put(txn_date, yymmdd10.)                 as txn_date_iso      /* conversion */
    from work.txn
    where txn_id = 'T002';
quit;
```

**Output**

| txn_id | channel_uc | txn_num | cust_channel | amt_with_gst | thousands | yr | month_end | days_old | txn_date_iso |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| T002 | ONLINE | 002 | C102\|ONLINE | 147500 | 125 | 2026 | 31JAN2026 | 271 | 2026-01-02 |

**Check:** 30 September 2026 is day 24379 and 2 January 2026 is day 24108, so `days_old` is 271.

**Summary functions vs row functions**

| Call | In PROC SQL it is |
| --- | --- |
| `sum(amount)` (one argument) | An **aggregate**: adds down the rows of the group |
| `sum(a, b)` (two or more arguments) | A **row function**: adds across columns in one row |
| `max(txn_date)` | Aggregate |
| `max(a, b, c)` | Row function |

### SQL Server function map

| Purpose | SAS (PROC SQL) | SQL Server |
| --- | --- | --- |
| Upper case | `upcase(x)` | `UPPER(x)` |
| Substring | `substr(x, 2, 3)` | `SUBSTRING(x, 2, 3)` |
| Find text | `index(x, 'a')` / `find(x, 'a', 'i')` | `CHARINDEX('a', x)` |
| Join with separator | `catx('-', a, b)` | `CONCAT_WS('-', a, b)` |
| Text to number | `input(x, 8.)` | `CAST(x AS INT)` / `TRY_CAST` |
| Number to text | `put(x, 8.)` | `CAST(x AS VARCHAR)` |
| Round | `round(x, 0.01)` | `ROUND(x, 2)` |
| Year | `year(d)` | `YEAR(d)` |
| Add months | `intnx('month', d, 1, 's')` | `DATEADD(month, 1, d)` |
| Month end | `intnx('month', d, 0, 'e')` | `EOMONTH(d)` |
| Date difference in days | `d2 - d1` | `DATEDIFF(day, d1, d2)` |
| Current date | `today()` | `CAST(GETDATE() AS DATE)` |

### ⚠️ Common mistakes

- Using `MONOTONIC()` with ORDER BY and trusting the numbers.
- Forgetting that `sum(a, b)` in PROC SQL is a row function, not an aggregate.
- Using SQL Server function names (`ISNULL`, `GETDATE`, `LEN`) in PROC SQL.

### Exercises

1. **Level 1:** Replace missing amounts with 0 using COALESCE.
2. **Level 2:** Number transactions by amount (largest first) the reliable way.
3. **Level 3:** Using SAS functions in PROC SQL, show each transaction's weekday name and its days
   since month start.
4. **Level 4 — Interview:** "How do you create a row number in PROC SQL?"
5. **Level 5:** Translate 10 SQL Server functions you use often into their SAS equivalents and test
   each in PROC SQL.

### ⭐ Interview questions

**Q. How do you create row numbers in PROC SQL?**
- *Strong answer:* "PROC SQL in SAS 9.4 has no ROW_NUMBER. For printed output I use the NUMBER option.
  MONOTONIC() exists but is undocumented and unreliable with ORDER BY, GROUP BY or joins. In production
  I build the table in PROC SQL and number it in a DATA step with `_N_`, or with FIRST. for row numbers
  within groups."

### Module wrap-up

- **I now know:** COALESCE, the three row-number approaches, and SAS functions in PROC SQL.
- **I can now:** handle missing values, number rows reliably and translate SQL Server functions.
- **Next:** Module 31 — joining and appending tables.

---

## MODULE 31 — Joining and Appending Tables

**Syllabus items:** 4.20 Joining tables vertically and horizontally · 7.17 Appending tables · 7.18
Merging tables

**You will learn:** horizontal joins (side by side), vertical joins (stacking), set operators, and
PROC APPEND. **Why it matters:** combining tables is the heart of analytics work. **Before you
start:** Modules 27 and 29.

### Sample tables

```sas
data work.acct;
    length acct_id $3 cust_id $4;
    input acct_id $ cust_id $ product :$12. balance;
    datalines;
A01 C101 SAVINGS 250000
A02 C101 CREDITCARD -45000
A03 C102 CURRENT 18000
A04 C105 LOAN 900000
;
run;
/* work.customers has C101, C102, C103, C104 (Module 5) */
```

C103 and C104 have no account. C105 has an account but no customer record (an orphan).

### Horizontal joins (4.20, 7.18)

```text
INNER JOIN : rows with a match on both sides
LEFT JOIN  : every row from the left table, plus matches from the right
RIGHT JOIN : every row from the right table, plus matches from the left
FULL JOIN  : every row from both tables
```

**Inner join**

```sas
proc sql;
    create table work.cust_acct as
    select c.cust_id, c.name, a.acct_id, a.product, a.balance
    from work.customers as c
         inner join work.acct as a
         on c.cust_id = a.cust_id
    order by c.cust_id, a.acct_id;
quit;
```

📌 Without `ORDER BY`, SQL does not promise any row order, in SAS or SQL Server.

| cust_id | name | acct_id | product | balance |
| --- | --- | --- | --- | --- |
| C101 | Asha Rao | A01 | SAVINGS | 250000 |
| C101 | Asha Rao | A02 | CREDITCARD | -45000 |
| C102 | Bilal Khan | A03 | CURRENT | 18000 |

**Full join with COALESCE for the key**

```sas
proc sql;
    create table work.cust_acct_full as
    select coalesce(c.cust_id, a.cust_id) as cust_id,
           c.name, a.acct_id, a.product
    from work.customers as c
         full join work.acct as a
         on c.cust_id = a.cust_id
    order by cust_id;
quit;
```

| cust_id | name | acct_id | product |
| --- | --- | --- | --- |
| C101 | Asha Rao | A01 | SAVINGS |
| C101 | Asha Rao | A02 | CREDITCARD |
| C102 | Bilal Khan | A03 | CURRENT |
| C103 | Chetan Iyer | | |
| C104 | Divya Menon | | |
| C105 | | A04 | LOAN |

Without `COALESCE`, `c.cust_id` would be blank for C105, because that row has no customer.

| Join | Rows here | Why |
| --- | --- | --- |
| INNER | 3 | Only C101 (2 accounts) and C102 match |
| LEFT (customers on the left) | 5 | C101 twice, C102, C103, C104 |
| RIGHT | 4 | A01, A02, A03, A04 |
| FULL | 6 | Everything |

**Anti-join: customers with no account**

```sas
proc sql;
    select c.cust_id, c.name
    from work.customers as c
         left join work.acct as a
         on c.cust_id = a.cust_id
    where a.cust_id is missing;      /* C103 and C104 */
quit;
```

The same result with `where c.cust_id not in (select cust_id from work.acct)` or with `NOT EXISTS`.

⚠️ **Many-to-many joins** produce every combination of matching rows (a Cartesian product within each
key), just like SQL Server. This is a key difference from the DATA step MERGE (Module 33).

⚠️ A join with no ON condition joins every row to every row. The Log says `NOTE: The execution of this
query involves performing one or more Cartesian product joins that can not be optimized.`

### Vertical joins: set operators (4.20)

```sas
data work.q1; input cust_id $; datalines;
C101
C102
C103
;
run;
data work.q2; input cust_id $; datalines;
C102
C103
C104
;
run;
```

| Operator | Result | Meaning |
| --- | --- | --- |
| `select * from q1 union select * from q2` | C101, C102, C103, C104 | Stack and remove duplicates |
| `union all` | 6 rows | Stack, keep duplicates |
| `intersect` | C102, C103 | In both |
| `except` (q1 except q2) | C101 | In the first but not the second |
| `outer union corr` | All rows, columns matched by **name** | Stack tables with different columns |

⚠️ `UNION`, `INTERSECT` and `EXCEPT` match columns by **position**, not by name. If the column order
differs between the tables, values land in the wrong columns. Add `CORR` (`union corr`) to match by
name and keep only the shared columns.

### Appending tables (7.17)

| Method | Code | Notes |
| --- | --- | --- |
| **PROC APPEND** | `proc append base=bank.txn_history data=work.txn_today; run;` | 🚀 Fastest. Adds rows to the end without rewriting the base table. |
| PROC SQL INSERT | `insert into bank.txn_history select * from work.txn_today;` | Column order must match |
| PROC SQL UNION ALL | `create table x as select * from a union all select * from b;` | Writes a new table |
| DATA step SET | `data x; set a b; run;` | Rewrites everything (slow for a big base) |

```sas
proc append base=bank.txn_history data=work.txn_today force;
run;
```

`FORCE` lets the append run even when the two tables differ slightly (for example an extra column in
the new data). Read the warnings: extra columns are dropped and longer text is cut to the base length.

🚀 Appending 1 million new rows to a 500-million-row history table with PROC APPEND reads only the 1
million new rows. A DATA step `SET history new;` would read and rewrite all 501 million.

### SQL joins vs DATA step MERGE (preview of Module 33)

| | PROC SQL join | DATA step MERGE |
| --- | --- | --- |
| Needs sorted data | No | Yes (BY variables) |
| Many-to-many | Cartesian product per key (like SQL Server) | Matches row by row (usually wrong) |
| Join on different column names | Easy (`on a.x = b.y`) | Rename first |
| Non-equal joins (`between`, `<`) | Yes | No |
| Tell which side a row came from | Check for missing keys | `IN=` flags |

### Pandas equivalents

| SAS | Pandas |
| --- | --- |
| Inner / left / right / full join | `pd.merge(c, a, on="cust_id", how="inner" / "left" / "right" / "outer")` |
| Anti-join | `merge(..., how="left", indicator=True)` then keep `"left_only"` |
| UNION ALL | `pd.concat([q1, q2])` |
| UNION | `pd.concat([q1, q2]).drop_duplicates()` |
| INTERSECT | `q1.merge(q2)` |
| EXCEPT | `q1[~q1["cust_id"].isin(q2["cust_id"])]` |

### 💼 Banking scenario

Reconciliation between the core banking system and the card system: a **full join** on account
number, with COALESCE on the key, shows accounts that exist in only one system. Rows where both sides
exist but balances differ go to a mismatch report. This is a daily control in most banks.

### ⚠️ Common mistakes

- Using UNION when you need UNION ALL (losing genuine duplicate transactions).
- Stacking tables whose columns are in a different order without `CORR`.
- Forgetting COALESCE on the key in a full join.
- Appending with a DATA step and rewriting a huge history table every day.

### Exercises

1. **Level 1:** Inner join customers and accounts.
2. **Level 2:** List customers with no account, three ways (LEFT JOIN, NOT IN, NOT EXISTS).
3. **Level 3:** Full join two systems' account lists and flag "only in A", "only in B", "both".
4. **Level 4 — Interview:** "What is the difference between UNION and UNION ALL, and how does SAS
   match columns?"
5. **Level 5:** Append today's transactions to a history table with PROC APPEND, and add a control
   check that the row count increased by exactly the number of new rows.

### ⭐ Interview questions

**Q1. How do PROC SQL set operators match columns?**
- *Strong answer:* "By position by default. If the tables have the same columns in a different order,
  values go into the wrong columns. The CORR keyword matches by name and keeps only common columns.
  OUTER UNION CORR keeps all columns from both."

**Q2. Fastest way to add rows to a large table?**
- *Strong answer:* "PROC APPEND. It only reads the new data and writes it to the end of the base
  table, instead of rewriting the whole table like a DATA step SET."

### Module wrap-up

- **I now know:** inner, left, right, full and anti-joins, set operators, CORR, and PROC APPEND.
- **I can now:** combine tables side by side and stack them efficiently.
- **Next:** Module 32 — views, stored procedures, indexes and dictionary tables.

---

## MODULE 32 — Views, "Stored Procedures", Indexes and Dictionary Tables

**Syllabus items:** 4.24 SAS SQL Views · 4.25 SAS SQL Stored Procedures · 7.23 SAS SQL Views (same) ·
7.24 SAS SQL Stored Procedures (same)

**You will learn:** SQL views, what SAS offers instead of stored procedures, indexes, and dictionary
tables. **Why it matters:** these are the tools for reusable, fast, self-documenting SAS work.
**Before you start:** Modules 25–31.

### SQL views (4.24, 7.23)

A **view** is a saved query. It holds no data. Each time you use it, the query runs and returns the
current data.

```sas
proc sql;
    create view work.v_high_value as
    select t.txn_id, t.cust_id, c.name, t.amount
    from work.txn as t
         inner join work.customers as c
         on t.cust_id = c.cust_id
    where t.amount >= 50000;
quit;

proc print data=work.v_high_value noobs;     /* the query runs now */
run;
```

**Output:** T002 (Bilal Khan, 125,000) and T006 (Asha Rao, 78,000).

| | Table | View |
| --- | --- | --- |
| Stores data | Yes | No, only the query |
| Data is current | As of when it was created | Always current |
| Disk space | Uses space | Almost none |
| Speed when used | Fast (already computed) | Runs the query every time |

**A permanent view that knows its own libraries** (so it works in any session):

```sas
proc sql;
    create view mart.v_npa as
    select loan_id, cust_id, outstanding
    from risk.loans
    where dpd > 90
    using libname risk "/sasdata/risk/loans";
quit;
```

`DESCRIBE VIEW mart.v_npa;` writes the view's query to the Log.

DATA step views also exist: `data work.v_clean / view=work.v_clean; set ...; run;`.

### "Stored procedures" (4.25, 7.24)

⚠️ PROC SQL has **no** `CREATE PROCEDURE`. SAS meets the same needs (saved, reusable, parameterised
logic) in other ways:

| Need | SAS way |
| --- | --- |
| Reusable SQL with parameters | A **macro** containing PROC SQL (most common, Part VIII) |
| Saved query that always returns current data | A **view** |
| Saved program run by other programs | A `.sas` file brought in with `%INCLUDE` (Module 54) |
| Program run on the server from EG, a web page or Excel | A **SAS Stored Process** (set up by administrators) |
| Your own reusable function | **PROC FCMP** |
| Run a real database stored procedure | Explicit pass-through: `execute (exec dbo.usp_name) by con;` |

**A macro acting as a parameterised stored procedure**

```sas
%macro top_customers(month_start=, n=10);
    proc sql outobs=&n;
        create table work.top_customers as
        select cust_id, sum(amount) as total_amt format=comma14.
        from bank.transactions
        where txn_date between "&month_start"d
                           and intnx('month', "&month_start"d, 0, 'e')
        group by cust_id
        order by total_amt desc;
    quit;
%mend top_customers;

%top_customers(month_start=01SEP2026, n=20)
```

`"&month_start"d` becomes `"01SEP2026"d`. Double quotes are needed so the macro variable resolves
(Module 48).

### Indexes

An **index** lets SAS find matching rows without reading the whole table, like the index at the back of
a book.

```sas
proc sql;
    create index cust_id on bank.transactions(cust_id);                 /* simple: name = column */
    create index cust_date on bank.transactions(cust_id, txn_date);     /* composite: any name */
    create unique index txn_id on bank.transactions(txn_id);            /* also blocks duplicates */
quit;

options msglevel=i;      /* the Log then says when an index is used */
```

When an index is used, the Log says something like `INFO: Index cust_id selected for WHERE clause
optimization.`

| Index helps | Index does not help |
| --- | --- |
| WHERE that selects a small part of a big table (roughly under 15–20% of rows) | Reading most of the table |
| Joins and lookups on the indexed column | Small tables |
| BY processing without re-sorting | Columns with very few different values (like Y/N flags) |

⚠️ Indexes cost disk space and slow down inserts and updates. A DATA step that rewrites a table loses
its indexes; PROC APPEND and PROC SQL INSERT keep them.

### Dictionary tables

Dictionary tables describe everything in your SAS session: libraries, tables, columns, macro
variables, formats and options.

```sas
proc sql;
    /* every table in BANK that has a column called CUST_ID */
    select libname, memname
    from dictionary.columns
    where libname = 'BANK' and upcase(name) = 'CUST_ID';

    /* size of every table in BANK */
    select memname, nobs format=comma12., nvar, filesize format=sizekmg.
    from dictionary.tables
    where libname = 'BANK' and memtype = 'DATA';
quit;
```

| Dictionary table | Holds | SASHELP view (usable outside PROC SQL) |
| --- | --- | --- |
| `dictionary.tables` | Tables and views | `sashelp.vtable` |
| `dictionary.columns` | Columns | `sashelp.vcolumn` |
| `dictionary.libnames` | Libraries | `sashelp.vlibnam` |
| `dictionary.macros` | Macro variables | `sashelp.vmacro` |
| `dictionary.indexes` | Indexes | `sashelp.vindex` |

📌 Library and table names are stored in **uppercase** in dictionary tables.

**SQL Server equivalent:** `INFORMATION_SCHEMA.TABLES`, `INFORMATION_SCHEMA.COLUMNS`, `sys.indexes`.

### 💼 Banking scenario

A risk team publishes `mart.v_npa` (a view) so every analyst gets current non-performing loans without
copying data. A nightly job uses `dictionary.tables` to check every mart table was refreshed today and
has a non-zero row count, and emails the team if not.

### ⚠️ Common mistakes

- Using a view inside a heavy loop, so the same expensive query runs many times. Create a table once
  instead.
- A permanent view without `USING LIBNAME`, which fails in sessions where the libref is not assigned.
- Indexing everything. Index columns that are used for selective lookups.
- Searching dictionary tables with lowercase library names.

### Exercises

1. **Level 1:** Create a view of ONLINE transactions and print it.
2. **Level 2:** Write a macro that returns the top `n` customers for a given channel.
3. **Level 3:** Create an index on `cust_id`, turn on `MSGLEVEL=I`, and confirm in the Log that a WHERE
   query uses it.
4. **Level 4 — Interview:** "Does PROC SQL support stored procedures?"
5. **Level 5:** Use dictionary tables to list every column in a library whose name contains `DATE`,
   with its format, to check that date columns are formatted consistently.

### ⭐ Interview questions

**Q1. Does PROC SQL have stored procedures?**
- *What they are testing:* honest, precise knowledge.
- *Strong answer:* "No, PROC SQL has no CREATE PROCEDURE. For reusable parameterised SQL I wrap PROC
  SQL in a macro. For saved queries I use views. Server-side programs can be SAS Stored Processes. And
  I can call a database's own stored procedure with explicit pass-through EXECUTE."
- *Weak answer:* "Yes, with CREATE PROCEDURE."

**Q2. View or table?**
- *Strong answer:* "A view when data must be current and the query is light or used rarely. A table
  when the result is reused many times or the query is expensive."

### Module wrap-up

- **I now know:** SQL and DATA step views, SAS alternatives to stored procedures, indexes, and
  dictionary tables.
- **I can now:** build reusable, current, fast and self-checking SAS SQL solutions.
- **Next:** Mini Project 2, then Part VI — advanced DATA step.

---

## Mini Project 2 — Branch Performance Analysis with PROC SQL

**Uses:** Part V (and the cleaned data from Mini Project 1). **Domain:** retail banking.

**Business requirement:** the regional head wants a monthly branch performance pack.

**Data:** `stage.txn_clean`, `stage.customers`, and a new `branches` table (branch code, name, region,
manager) that you create with `CREATE TABLE` and `INSERT`.

**Stakeholder questions (answer each with PROC SQL)**

1. Total transaction value and count per branch for September 2026.
2. Average transaction value per branch, keeping branches above the regional average (remerging or a
   subquery).
3. Each branch's share of its region's total (remerging).
4. Number of distinct active customers per branch, and customers with no September transaction
   (anti-join).
5. Channel mix per branch as columns (conditional aggregation).
6. Branches whose September total fell by more than 20% compared with August.
7. The top 5 customers per region (PROC SQL to summarise, then a DATA step or PROC RANK to rank).
8. A permanent view that always shows the current month's branch totals.

**Deliverables:** one program with clear comments, a `rpt.branch_pack` table, and a short note on any
data-quality issue you found (orphan accounts, missing branches).

**Part V checklist:** ✓ 4.5 · ✓ 4.6 · ✓ 4.7 · ✓ 4.8 · ✓ 4.9 · ✓ 4.10 · ✓ 4.11 · ✓ 4.12 · ✓ 4.13 · ✓ 4.14 · ✓ 4.15 · ✓ 4.16 ·
✓ 4.17 · ✓ 4.18 · ✓ 4.20 · ✓ 4.21 · ✓ 4.22 · ✓ 4.23 · ✓ 4.24 · ✓ 4.25 · ✓ 7.1–7.24 (all)

---

# Part VI — Advanced DATA Step (Modules 33–39)

## MODULE 33 — MERGE: Joining in the DATA Step

**Syllabus items:** this module is the DATA step side of 7.18 (Merging tables) and concept-map row 8
(JOIN ↔ MERGE).

**You will learn:** how MERGE combines datasets side by side, why it needs sorted data, how IN= flags
give you every join type, and the many-to-many trap. **Why it matters:** ⭐ "MERGE vs JOIN" is one of
the most common SAS interview questions. **Before you start:** Modules 7, 18 and 31.

### 🧠 What it is

`MERGE` reads one row from each dataset that has the current BY value and combines them into a single
row in the PDV.

```sas
proc sort data=work.customers out=work.cust_s;  by cust_id;  run;
proc sort data=work.acct      out=work.acct_s;  by cust_id;  run;

data work.cust_acct_m;
    merge work.cust_s (in=in_c)
          work.acct_s (in=in_a);
    by cust_id;
    in_cust = in_c;            /* copy the flags so you can see them */
    in_acct = in_a;
run;
```

**Output**

| cust_id | name | city | segment | fico | acct_id | product | balance | in_cust | in_acct |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| C101 | Asha Rao | Mumbai | R | 742 | A01 | SAVINGS | 250000 | 1 | 1 |
| C101 | Asha Rao | Mumbai | R | 742 | A02 | CREDITCARD | -45000 | 1 | 1 |
| C102 | Bilal Khan | Delhi | C | 688 | A03 | CURRENT | 18000 | 1 | 1 |
| C103 | Chetan Iyer | Pune | R | 615 | | | . | 1 | 0 |
| C104 | Divya Menon | Chennai | S | . | | | . | 1 | 0 |
| C105 | | | | . | A04 | LOAN | 900000 | 0 | 1 |

With no subsetting IF, MERGE behaves like a **full join**.

### IN= flags give you every join type

`IN=` creates a temporary 0/1 variable that is 1 when the current BY group has a row from that
dataset. It is not written to the output (that is why the example copied it into `in_cust`).

| Join type | Add this line | Rows from the example |
| --- | --- | --- |
| Inner | `if in_c and in_a;` | C101 (×2), C102 |
| Left (all customers) | `if in_c;` | C101 (×2), C102, C103, C104 |
| Right (all accounts) | `if in_a;` | C101 (×2), C102, C105 |
| Full | (nothing) | All 6 |
| Customers without accounts | `if in_c and not in_a;` | C103, C104 |
| Orphan accounts | `if in_a and not in_c;` | C105 |

**Sending each case to its own dataset in one pass:**

```sas
data work.matched work.no_account work.orphan_account;
    merge work.cust_s (in=in_c) work.acct_s (in=in_a);
    by cust_id;
    if in_c and in_a then output work.matched;
    else if in_c     then output work.no_account;
    else                  output work.orphan_account;
run;
```

### 🧠 Why MERGE needs sorted data

MERGE walks down all the datasets **at the same time**, like zipping two sorted lists together. It
only looks at the current BY value in each dataset. If the data is not sorted, it cannot know whether a
matching row is still coming, so it stops:

```text
ERROR: BY variables are not properly sorted on data set WORK.ACCT.
```

The data must be sorted (or indexed) by the BY variables. This is why SQL joins, which can sort or hash
internally, are often simpler.

### 🧠 One-to-one, one-to-many and many-to-many

**One-to-many works like a join.** For C101 there is one customer row and two account rows. MERGE keeps
the customer values in the PDV while it reads the second account row. Variables read by MERGE are not
reset to missing within a BY group (Module 7), so `name` and `city` repeat.

**Many-to-many does NOT work like SQL.**

```sas
data work.a;  input id $ a_val $;  datalines;
X a1
X a2
;
run;
data work.b;  input id $ b_val $;  datalines;
X b1
X b2
X b3
;
run;

data work.mm;
    merge work.a work.b;
    by id;
run;
```

| id | a_val | b_val |
| --- | --- | --- |
| X | a1 | b1 |
| X | a2 | b2 |
| X | a2 | b3 |

**3 rows**, not the 6 a SQL join would give. MERGE matches row 1 with row 1, row 2 with row 2, and then
repeats the last `a` value for the extra `b` row. The Log warns: `NOTE: MERGE statement has more than
one data set with repeats of BY values.` Treat that NOTE as a bug. For many-to-many, use PROC SQL.

**One-to-one MERGE without BY** matches purely by position (row 1 with row 1). It is almost never what
you want with real data.

### ⚠️ The overwrite trap

If both datasets have a non-BY variable with the **same name**, the value from the dataset listed
**later** overwrites the earlier one (when both have a row in that BY group).

```sas
/* both have a variable called STATUS */
data work.combined;
    merge work.customers_status work.accounts_status;   /* accounts' status wins */
    by cust_id;
run;
```

Fix it by renaming: `merge work.customers_status(rename=(status=cust_status))
work.accounts_status(rename=(status=acct_status));`.

### Hash objects: lookups without sorting (industry gap)

When you only need to look up values from a small table, a **hash object** loads that table into
memory and finds matches instantly. No sorting is needed.

```sas
data work.txn_with_name;
    if _n_ = 1 then do;
        if 0 then set work.customers(keep=cust_id name);      /* define name's type and length */
        declare hash cust(dataset: 'work.customers(keep=cust_id name)');
        cust.defineKey('cust_id');
        cust.defineData('name');
        cust.defineDone();
    end;
    set work.txn;
    if cust.find() ne 0 then name = 'NOT FOUND';              /* find() returns 0 when found */
run;
```

| Line | What it does |
| --- | --- |
| `if 0 then set ...;` | Never runs, but at compile time adds `name` to the PDV with the right type and length |
| `declare hash cust(dataset: ...)` | Loads the customer table into memory once |
| `defineKey` / `defineData` | The lookup key and the value to return |
| `cust.find()` | Looks up the current `cust_id`. Returns 0 if found and fills `name`. |

🚀 Fraud teams use hash objects to check every transaction against blocked-card or watch lists with
millions of rows, without sorting the transactions.

### MERGE vs SQL JOIN

| | DATA step MERGE | PROC SQL JOIN |
| --- | --- | --- |
| Sorting | Required | Not required |
| Many-to-many | Matches row by row (wrong for most uses) | Cartesian product per key |
| Different key names | Rename first | `on a.x = b.y` |
| Range or non-equal conditions | No | Yes |
| Several outputs in one pass | Yes (`OUTPUT`) | No (one table per statement) |
| Know where a row came from | `IN=` flags | Check missing keys |
| Can add row-by-row logic (RETAIN, FIRST.) | Yes, in the same step | No |
| Same-named columns | Later dataset overwrites | Must choose with aliases |
| Speed on big sorted data | Very fast | Fast; SAS chooses a method |

**SQL Server and Pandas equivalents:** MERGE with IN= maps to `JOIN` types in SQL and
`pd.merge(..., how=..., indicator=True)` in Pandas.

### 💼 Banking scenario

A daily job matches the card authorisation file with the card master. Both are already sorted by
card number from previous steps. One MERGE writes three datasets in one pass: matched transactions
(for scoring), authorisations with no card master record (a data-quality alert), and cards with no
activity today (for dormancy tracking). Doing the same in SQL would take three queries.

### ⚠️ Common mistakes

- Forgetting to sort: `ERROR: BY variables are not properly sorted`.
- Ignoring the "repeats of BY values" NOTE.
- Same-named non-BY variables overwriting each other.
- Forgetting the BY statement (merges by position).
- BY variables with different lengths in the two datasets (`WARNING: Multiple lengths were specified
  for the BY variable ...`), which can cause mismatches. Make the lengths equal first.

### Exercises

1. **Level 1:** Merge customers and accounts and keep only matches.
2. **Level 2:** Produce matched, customer-only and account-only datasets in one step.
3. **Level 3:** Build a many-to-many example, merge it, read the NOTE, and redo it with PROC SQL.
4. **Level 4 — Interview:** "What is the difference between MERGE and a SQL join?"
5. **Level 5:** Look up a 1-million-row blocked-card list for 50 million transactions with a hash
   object, and compare the run time with sort + MERGE.

### ⭐ Interview questions

**Q1. MERGE vs PROC SQL join?**
- *What they are testing:* PDV knowledge and practical judgement.
- *Strong answer:* "MERGE needs data sorted by the BY variables, uses IN= flags for join types, can
  write several outputs and add row-by-row logic in one pass. For many-to-many it matches row by row
  instead of producing a Cartesian product, so I use PROC SQL there. PROC SQL needs no sorting and
  supports different key names and range joins. For lookups against a small table I use a hash
  object."
- *Example:* the a1/a2 × b1/b2/b3 table.
- *Weak answer:* "They are the same."
- *Follow-up:* "What happens to same-named variables in a MERGE?"

**Q2. How do you do a left join with MERGE?**
- *Strong answer:* "`merge a(in=ina) b(in=inb); by key; if ina;`."

### Module wrap-up

- **I now know:** MERGE, BY, IN=, all join types, one-to-many vs many-to-many, the overwrite trap, and
  hash lookups.
- **I can now:** join in the DATA step correctly and choose between MERGE, SQL and hash.
- **Next:** Module 34 — RETAIN, FIRST. and LAST.

---

## MODULE 34 — RETAIN, the Sum Statement, FIRST. and LAST.

**Syllabus items:** 5.3 RETAIN statement · 5.7 FIRST. and LAST.

**You will learn:** how to carry values from one row to the next, and how to detect the first and last
row of each group. **Why it matters:** 🔥 running totals, previous values, group totals and "latest
record" logic are everyday SAS work, and interviewers always test them. **Before you start:** Modules
7, 18 and 22.

### 🧠 RETAIN in plain words

Normally, at the top of each DATA step loop, variables you calculate are reset to missing (Module 7).
**RETAIN tells SAS not to reset them**, so a value carries over to the next row.

```sas
retain running_total 0;    /* start at 0 and keep the value between rows */
```

**The sum statement** is a short-cut that retains automatically:

```sas
running_total + amount;    /* same as: retain running_total 0; running_total = sum(running_total, amount); */
```

| | `retain x 0; x = x + amount;` | `x + amount;` (sum statement) |
| --- | --- | --- |
| Starts at | 0 (the RETAIN value) | 0 |
| Kept between rows | Yes | Yes |
| If `amount` is missing | **x becomes missing** and stays missing | Missing is ignored |

### Running total (whole dataset)

```sas
data work.running;
    set work.txn;
    running_total + amount;
run;
```

| txn_id | amount | running_total |
| --- | --- | --- |
| T001 | 5,000 | 5000 |
| T002 | 125,000 | 130000 |
| T003 | 2,300 | 132300 |
| T004 | . | 132300 |
| T005 | 20,000 | 152300 |
| T006 | 78,000 | 230300 |

### 🔥 FIRST. and LAST.

When you use a `BY` statement in a DATA step, SAS creates two temporary variables for each BY
variable:

- `FIRST.var` = 1 on the **first** row of each group, otherwise 0.
- `LAST.var` = 1 on the **last** row of each group, otherwise 0.

The data must be sorted by the BY variables.

```sas
proc sort data=work.txn out=work.txn_s;
    by cust_id txn_date;
run;

data work.flags;
    set work.txn_s;
    by cust_id;
    first_flag = first.cust_id;      /* copy them so you can see them */
    last_flag  = last.cust_id;
run;
```

| txn_id | cust_id | txn_date | first_flag | last_flag |
| --- | --- | --- | --- | --- |
| T001 | C101 | 02JAN2026 | 1 | 0 |
| T003 | C101 | 05JAN2026 | 0 | 0 |
| T006 | C101 | 12JAN2026 | 0 | 1 |
| T002 | C102 | 02JAN2026 | 1 | 0 |
| T005 | C102 | 09JAN2026 | 0 | 1 |
| T004 | C103 | 07JAN2026 | 1 | 1 |

A group with one row has both flags equal to 1.

### The seven classic patterns

**1. Running total per customer**

```sas
data work.cust_running;
    set work.txn_s;
    by cust_id;
    if first.cust_id then cust_running = 0;   /* reset at each new customer */
    cust_running + amount;
run;
```

C101: 5,000 → 7,300 → 85,300. C102: 125,000 → 145,000. C103: 0 (its only amount is missing).

**2. Group total, one row per customer**

```sas
data work.cust_total;
    set work.txn_s;
    by cust_id;
    if first.cust_id then do;
        total_amt = 0;
        txn_count = 0;
    end;
    total_amt + amount;
    txn_count + 1;
    if last.cust_id then output;              /* write only the final row of each group */
    keep cust_id total_amt txn_count;
run;
```

| cust_id | total_amt | txn_count |
| --- | --- | --- |
| C101 | 85300 | 3 |
| C102 | 145000 | 2 |
| C103 | 0 | 1 |

**3. First transaction per customer:** `if first.cust_id;`

**4. Last (latest) transaction per customer:** `if last.cust_id;` (data sorted by date within
customer).

**5. Previous value within the group**

```sas
data work.prev_value;
    set work.txn_s;
    by cust_id;
    retain prev_date;
    if first.cust_id then prev_date = .;
    days_since_prev = txn_date - prev_date;
    output;
    prev_date = txn_date;            /* remember this row's date for the next row */
    format prev_date date9.;
run;
```

C101: T001 (no previous), T003 (3 days after T001), T006 (7 days after T003).

📌 The order matters: calculate with the **old** value first, `OUTPUT`, then save the current value.

**6. Count of rows per group and position in the group**

```sas
data work.positions;
    set work.txn_s;
    by cust_id;
    if first.cust_id then seq = 0;
    seq + 1;                          /* 1, 2, 3 within each customer: like ROW_NUMBER() */
run;
```

**7. Carry a value forward (fill missing values down)**

```sas
data work.filled;
    set work.daily_rates;             /* date, rate (some days missing) */
    retain last_rate;
    if not missing(rate) then last_rate = rate;
    else rate = last_rate;
run;
```

### Two BY variables

With `by branch cust_id;`, `FIRST.cust_id` is also 1 whenever **branch** changes, even if the same
customer ID appears in the next branch. A change in an outer BY variable starts a new inner group.

### SQL Server and Pandas

| SAS | SQL Server | Pandas |
| --- | --- | --- |
| Running total per group | `SUM(amount) OVER (PARTITION BY cust_id ORDER BY txn_date)` | `df.groupby("cust_id")["amount"].cumsum()` |
| Group total, one row | `GROUP BY` | `groupby().agg()` |
| `if first.cust_id;` | `ROW_NUMBER() OVER (...) = 1` | `groupby().head(1)` |
| `if last.cust_id;` | `ROW_NUMBER() OVER (... DESC) = 1` | `groupby().tail(1)` |
| Previous value | `LAG(txn_date) OVER (PARTITION BY cust_id ORDER BY txn_date)` | `groupby()["txn_date"].shift()` |
| Position in group | `ROW_NUMBER() OVER (PARTITION BY ...)` | `groupby().cumcount() + 1` |
| Fill down | `LAST_VALUE(... IGNORE NULLS)` (SQL Server 2022+) | `ffill()` |

📌 SQL Server needs a different window function for each pattern. In SAS one DATA step with BY can do
several of them at once, in a single pass, on data far larger than memory.

### 💼 Banking scenario: rapid repeat transactions

Fraud teams flag cards with 3 or more transactions within 10 minutes. Sort by card and datetime; use
RETAIN to keep the times of the previous two transactions within each card (reset at `first.card_no`);
flag a transaction when the earliest of the three is less than 600 seconds before it. One pass over
millions of transactions.

### ⚠️ Common mistakes

- Forgetting to reset at `FIRST.`, so totals run across customers.
- Using `x = x + amount;` with RETAIN, so one missing amount makes every later total missing.
- Using FIRST./LAST. without sorting (`ERROR: BY variables are not properly sorted`).
- Saving the "previous value" before using it, so you compare a row with itself.
- Forgetting that FIRST./LAST. are not written to the output.

### Exercises

1. **Level 1:** Keep the first transaction of each customer.
2. **Level 2:** One row per customer with total, count, first date and last date.
3. **Level 3:** Days since the previous transaction, reset for each customer.
4. **Level 4 — Interview:** "What is the difference between RETAIN and the sum statement?"
5. **Level 5:** Flag customers whose spend increased three months in a row.

### ⭐ Interview questions

**Q1. What does RETAIN do?**
- *Strong answer:* "It stops a variable being reset to missing at the start of each DATA step
  iteration, so its value carries to the next observation. It can also set an initial value. The sum
  statement `var + expr;` retains automatically, starts at 0 and ignores missing values."
- *Follow-up:* "Which variables are retained automatically?" (Variables read with SET, MERGE, UPDATE;
  sum-statement variables; automatic variables.)

**Q2. What are FIRST. and LAST.?**
- *Strong answer:* "Temporary flags created by a BY statement, equal to 1 on the first or last
  observation of each BY group. The data must be sorted. I use them for group totals, first/last
  records and resetting running values. They are not written to the output."

**Q3. How do you get the latest record per customer?**
- *Strong answer:* "Sort by customer and date, then `if last.cust_id;`, or sort descending by date and
  use PROC SORT NODUPKEY."

### Module wrap-up

- **I now know:** RETAIN, the sum statement, FIRST./LAST., and the seven classic BY-group patterns.
- **I can now:** do running totals, group totals, previous-value logic and fill-down in one pass.
- **Next:** Module 35 — PROC RANK.

---

## MODULE 35 — PROC RANK, and FIRST./LAST. vs PROC RANK

**Syllabus items:** 5.8 PROC RANK · 5.9 FIRST./LAST. vs PROC RANK

**You will learn:** ranking values with ties, ranking within groups, splitting data into deciles, and
when to use FIRST./LAST. instead. **Why it matters:** ranking customers, merchants and branches is a
standard analytics task. **Before you start:** Module 34.

### PROC RANK (5.8)

```sas
data work.cust_spend;
    input cust_id $ branch $ spend;
    datalines;
C101 MUM 85300
C102 MUM 145000
C103 MUM 85300
C104 DEL 52000
C105 DEL 98000
;
run;

proc rank data=work.cust_spend out=work.ranked descending ties=dense;
    var spend;
    ranks spend_rank;
run;
```

**Output**

| cust_id | branch | spend | spend_rank |
| --- | --- | --- | --- |
| C101 | MUM | 85300 | 3 |
| C102 | MUM | 145000 | 1 |
| C103 | MUM | 85300 | 3 |
| C104 | DEL | 52000 | 4 |
| C105 | DEL | 98000 | 2 |

| Part | Meaning |
| --- | --- |
| `descending` | Largest value gets rank 1 |
| `var spend;` | The variable to rank |
| `ranks spend_rank;` | The name of the new rank variable (without it, `spend` is **replaced** by its rank) |
| `ties=` | How to rank equal values |

**How ties are ranked** (for the values 145000, 98000, 85300, 85300, 52000):

| `TIES=` | Ranks given | SQL Server equivalent |
| --- | --- | --- |
| `MEAN` (default) | 1, 2, 3.5, 3.5, 5 | — |
| `LOW` | 1, 2, 3, 3, 5 | `RANK()` |
| `HIGH` | 1, 2, 4, 4, 5 | — |
| `DENSE` | 1, 2, 3, 3, 4 | `DENSE_RANK()` |

**Ranking within groups:** sort first, then use BY.

```sas
proc sort data=work.cust_spend;
    by branch;
run;

proc rank data=work.cust_spend out=work.ranked_branch descending ties=low;
    by branch;
    var spend;
    ranks branch_rank;
run;
```

DEL: C105 = 1, C104 = 2. MUM: C102 = 1, C101 = 2, C103 = 2.

**Deciles and quartiles with GROUPS=**

```sas
proc rank data=bank.customers out=work.deciles groups=10;
    var total_spend;
    ranks spend_decile;          /* 0 = lowest 10%, 9 = highest 10% */
run;
```

`GROUPS=n` splits the data into `n` roughly equal groups numbered 0 to n − 1. Add 1 if you want 1
to 10. This is how risk teams build score deciles and marketing teams build value tiers.

### FIRST./LAST. vs PROC RANK (5.9)

| Need | Best tool | Why |
| --- | --- | --- |
| Rank with proper tie handling | PROC RANK | `TIES=` options |
| Deciles, quartiles | PROC RANK `GROUPS=` | Built in |
| Unique row number within a group (`ROW_NUMBER`) | Sort + FIRST. with a counter | PROC RANK gives ties the same rank |
| Break ties with a second variable | Sort by both variables + FIRST. counter | PROC RANK ranks one variable at a time |
| Keep only the top row per group | Sort + `if first.group;` | No ranking needed |
| Top n per group | Sort + counter + `if seq <= n;` | One pass |

**Top 2 customers per branch, ties broken by customer ID:**

```sas
proc sort data=work.cust_spend out=work.cs;
    by branch descending spend cust_id;
run;

data work.top2;
    set work.cs;
    by branch;
    if first.branch then seq = 0;
    seq + 1;
    if seq <= 2;
run;
```

DEL: C105, C104. MUM: C102, C101 (C101 wins the tie with C103 because its ID sorts first).

### SQL Server and Pandas

| SAS | SQL Server | Pandas |
| --- | --- | --- |
| `ties=low` | `RANK() OVER (ORDER BY spend DESC)` | `rank(method="min", ascending=False)` |
| `ties=dense` | `DENSE_RANK()` | `rank(method="dense")` |
| `ties=mean` | — | `rank(method="average")` (the default) |
| `groups=10` | `NTILE(10)` | `pd.qcut(x, 10, labels=False)` |
| Sort + FIRST. counter | `ROW_NUMBER()` | `groupby().cumcount() + 1` |

⚠️ `NTILE(10)` and `GROUPS=10` can put **tied** values in different groups differently: PROC RANK keeps
equal values in the same group, while `NTILE` fills groups by row count.

### 💼 Banking scenario

A collections team ranks overdue accounts within each region by outstanding amount and assigns the top
50 per region to senior agents. Sort by region and descending outstanding, then a FIRST. counter with
`if seq <= 50` gives exactly 50 per region, with ties broken by account age.

### ⚠️ Common mistakes

- Forgetting `RANKS`, so the original values are overwritten by ranks.
- Forgetting `DESCENDING` when "rank 1" should be the largest.
- Using BY in PROC RANK without sorting first.
- Using PROC RANK when you need unique numbers (ties share a rank).

### Exercises

1. **Level 1:** Rank customers by spend, highest first, with dense ranks.
2. **Level 2:** Rank within each branch.
3. **Level 3:** Split customers into spend quartiles and count customers per quartile.
4. **Level 4 — Interview:** "How is PROC RANK different from FIRST./LAST.?"
5. **Level 5:** Top 3 merchants by fraud loss per merchant category, ties broken by transaction count.

### ⭐ Interview questions

**Q. PROC RANK vs FIRST./LAST.?**
- *Strong answer:* "PROC RANK computes ranks of a variable with tie rules (RANK, DENSE_RANK-style or
  mean) and can create deciles with GROUPS=. FIRST./LAST. with a counter gives unique row numbers within
  BY groups and lets me break ties with more sort variables, like ROW_NUMBER. For top-n per group I
  usually sort and use a counter."

### Module wrap-up

- **I now know:** PROC RANK with TIES=, BY and GROUPS=, and when FIRST./LAST. is the better tool.
- **I can now:** rank, bucket and pick top-n per group correctly.
- **Next:** Module 36 — transposing.

---

## MODULE 36 — Transposing Data

**Syllabus items:** 4.19 Transposing a table · 5.1 Transposing datasets from rows to columns and columns
to rows · 5.2 Transpose examples and challenges

**You will learn:** PROC TRANSPOSE in both directions with BY, ID, VAR, PREFIX and COPY, plus the DATA
step and SQL alternatives. **Why it matters:** reports want wide data (one column per month); analysis
wants long data (one row per month). **Before you start:** Modules 18, 28 and 34.

### 🧠 Long vs wide

```text
LONG (one row per customer per month)        WIDE (one row per customer)
cust_id  month  spend                        cust_id  spend_JAN  spend_FEB  spend_MAR
C101     JAN    5000                         C101     5000       7000       .
C101     FEB    7000          <----->        C102     2000       .          4000
C102     JAN    2000
C102     MAR    4000
```

### Rows to columns (long → wide)

```sas
data work.monthly_spend;
    input cust_id $ month $ spend;
    datalines;
C101 JAN 5000
C101 FEB 7000
C102 JAN 2000
C102 MAR 4000
;
run;

proc transpose data=work.monthly_spend
               out=work.spend_wide (drop=_name_)
               prefix=spend_;
    by cust_id;            /* one output row per customer (data must be sorted by cust_id) */
    id month;              /* values of MONTH become column names */
    var spend;             /* values to spread across the columns */
run;
```

**Output**

| cust_id | spend_JAN | spend_FEB | spend_MAR |
| --- | --- | --- | --- |
| C101 | 5000 | 7000 | . |
| C102 | 2000 | . | 4000 |

| Statement / option | Meaning |
| --- | --- |
| `BY` | Keeps these variables as row keys. One output row per BY group per VAR variable. |
| `ID` | Its values become the new column names |
| `VAR` | The variables whose values are moved |
| `PREFIX=` | Text added in front of each new column name |
| `_NAME_` | A column PROC TRANSPOSE adds, holding the name of the transposed variable. Usually dropped. |
| `NAME=` | Gives `_NAME_` a better name |

📌 Columns are created in the order the ID values are **first seen**, not alphabetically. Here JAN,
FEB, then MAR.

### Columns to rows (wide → long)

```sas
proc transpose data=work.spend_wide
               out=work.spend_long (rename=(col1=spend _name_=month));
    by cust_id;
    var spend_:;          /* every variable starting with spend_ */
run;
```

**Output**

| cust_id | month | spend |
| --- | --- | --- |
| C101 | spend_JAN | 5000 |
| C101 | spend_FEB | 7000 |
| C101 | spend_MAR | . |
| C102 | spend_JAN | 2000 |
| C102 | spend_FEB | . |
| C102 | spend_MAR | 4000 |

To clean up: `month = scan(month, 2, '_');` gives `JAN`, `FEB`, `MAR`. To drop the empty months:
`where spend is not missing` in a later step.

### COPY

`COPY var;` carries a variable across without transposing it. Because the output usually has a
different number of rows than the input, it is safest for variables that have one value per BY group.
In most cases, adding the variable to `BY` is clearer.

### Transpose challenges (5.2)

**Challenge 1: duplicate ID values.** If C101 has two JAN rows, PROC TRANSPOSE stops:

```text
ERROR: The ID value "JAN" occurs twice in the same BY group.
```

Fix: summarise first (PROC SUMMARY or SQL GROUP BY), or add `LET` to keep the last value (only if
that is truly correct).

**Challenge 2: several value variables at once.** With `var spend txn_count;` you get one output row
per variable per customer (with `_NAME_` telling them apart). To get `spend_JAN` and `count_JAN` side
by side, transpose twice and merge, or use the DATA step method below.

**Challenge 3: unknown months.** If new months appear every month, PROC TRANSPOSE adapts
automatically. The SQL CASE method needs code changes. This is a big advantage of PROC TRANSPOSE.

### The DATA step way (full control)

```sas
proc sort data=work.monthly_spend out=work.ms;
    by cust_id;
run;

data work.spend_wide2;
    set work.ms;
    by cust_id;
    array m{3} spend_jan spend_feb spend_mar;
    retain spend_jan spend_feb spend_mar;
    if first.cust_id then call missing(of m{*});
    select (month);
        when ('JAN') m{1} = spend;
        when ('FEB') m{2} = spend;
        when ('MAR') m{3} = spend;
        otherwise;
    end;
    if last.cust_id then output;
    keep cust_id spend_jan spend_feb spend_mar;
run;
```

This uses RETAIN, FIRST./LAST. and an array (Module 38). It is longer but works in one pass and gives
complete control.

### The SQL way (4.19)

```sas
proc sql;
    create table work.spend_wide_sql as
    select cust_id,
           sum(case when month = 'JAN' then spend end) as spend_jan,
           sum(case when month = 'FEB' then spend end) as spend_feb,
           sum(case when month = 'MAR' then spend end) as spend_mar
    from work.monthly_spend
    group by cust_id;
quit;
```

Leaving out `ELSE` makes non-matching rows missing, so a customer with no FEB row gets a missing
`spend_feb` (matching PROC TRANSPOSE). Use `ELSE 0` if you want zeros.

### Comparison

| | PROC TRANSPOSE | SQL CASE pivot | DATA step array | SQL Server | Pandas |
| --- | --- | --- | --- | --- | --- |
| Long → wide | ✓ | ✓ | ✓ | `PIVOT` | `pivot()` / `pivot_table()` |
| Wide → long | ✓ | `UNION ALL` | ✓ (loop + OUTPUT) | `UNPIVOT` | `melt()` |
| New values handled automatically | ✓ | ✗ | ✗ | ✗ (dynamic SQL) | ✓ |
| Duplicates | Error (or `LET`) | Summed | Your choice | Aggregated | `pivot` errors, `pivot_table` aggregates |

### 💼 Banking scenario

A credit-risk model needs each customer's balance for the last 12 months as 12 columns
(`bal_m1`–`bal_m12`). The source has one row per account per month. PROC SUMMARY first totals per
customer per month (to remove duplicate months), then PROC TRANSPOSE with `PREFIX=bal_m` builds the
wide table.

### ⚠️ Common mistakes

- Forgetting to sort by the BY variables.
- Duplicate ID values in a BY group.
- Not dropping or renaming `_NAME_` and `COL1`.
- ID values that are not valid variable names (spaces, leading digits). PROC TRANSPOSE changes them;
  use `PREFIX=` to keep names valid and readable.

### Exercises

1. **Level 1:** Transpose monthly spend from long to wide.
2. **Level 2:** Transpose it back to long and clean the month names.
3. **Level 3:** Create a duplicate month, read the error, and fix it with PROC SUMMARY first.
4. **Level 4 — Interview:** "What do BY, ID and VAR do in PROC TRANSPOSE?"
5. **Level 5:** Build a 12-month balance matrix per customer for a risk model, with months as
   `bal_m1`–`bal_m12` where m1 is the latest month.

### ⭐ Interview questions

**Q. Explain PROC TRANSPOSE's BY, ID and VAR.**
- *Strong answer:* "BY defines the row key; one output row per BY group (per VAR variable). ID's values
  become column names. VAR lists the variables whose values are moved. `PREFIX=` names the columns, and
  `_NAME_` holds the source variable's name. Data must be sorted by the BY variables and ID values must
  be unique within each group."
- *Follow-up:* "How would you do the same in SQL?" (Conditional aggregation.)

### Module wrap-up

- **I now know:** long vs wide, PROC TRANSPOSE in both directions, BY/ID/VAR/PREFIX/COPY/LET, and the
  DATA step and SQL alternatives.
- **I can now:** reshape data for reports and models, and handle the common transpose errors.
- **Next:** Module 37 — loops.

---

## MODULE 37 — Loops

**Syllabus items:** 5.13 SAS loops · 5.14 Loop examples

**You will learn:** the iterative DO loop, DO WHILE, DO UNTIL, LEAVE and CONTINUE, and how to create
many rows from one with OUTPUT inside a loop. **Why it matters:** loan schedules, projections and
calendars all need loops. **Before you start:** Modules 7 and 15.

### 🧠 Two kinds of looping in SAS

1. The **DATA step loop** is automatic: the step runs once per input row (Module 7).
2. A **DO loop** repeats statements **within one row** of that automatic loop.

### The forms of DO

| Form | Example | Runs |
| --- | --- | --- |
| Iterative | `do i = 1 to 12;` | 12 times |
| With a step | `do i = 0 to 100 by 25;` | 0, 25, 50, 75, 100 |
| Counting down | `do i = 10 to 1 by -1;` | 10 down to 1 |
| A list of values | `do channel = 'ATM', 'POS', 'ONLINE';` | Once per value |
| DO WHILE | `do while (balance > 0);` | While true. Checked at the **top**, so it may run 0 times. |
| DO UNTIL | `do until (amount >= 200000);` | Until true. Checked at the **bottom**, so it runs at least once. |
| Combined | `do i = 1 to 360 while (balance > 0);` | Up to 360 times, stopping early when false |

`LEAVE;` jumps out of the loop. `CONTINUE;` skips to the next round of the loop.

### Example 1: a loan EMI schedule (OUTPUT inside a loop)

A ₹5,00,000 loan at 12% a year, repaid over 12 months.

```sas
data work.emi_schedule;
    format month 3. emi interest principal_paid balance comma12.2;   /* sets the column order */
    principal   = 500000;
    annual_rate = 12;
    months      = 12;
    r   = annual_rate / 12 / 100;                                    /* 1% per month */
    emi = round(principal * r * (1 + r)**months / ((1 + r)**months - 1), 0.01);
    balance = principal;
    do month = 1 to months;
        interest       = round(balance * r, 0.01);
        principal_paid = round(emi - interest, 0.01);
        balance        = round(balance - principal_paid, 0.01);
        output;                                                      /* one row per month */
    end;
    keep month emi interest principal_paid balance;
run;
```

**Output (first 3 of 12 rows)**

| month | emi | interest | principal_paid | balance |
| --- | --- | --- | --- | --- |
| 1 | 44,424.39 | 5,000.00 | 39,424.39 | 460,575.61 |
| 2 | 44,424.39 | 4,605.76 | 39,818.63 | 420,756.98 |
| 3 | 44,424.39 | 4,207.57 | 40,216.82 | 380,540.16 |

**How it works:** there is no input dataset, so the DATA step runs once. Inside that one run, the DO
loop runs 12 times and `OUTPUT` writes a row each time. The `FORMAT` statement comes first so the
columns appear in this order (SAS orders variables by where it first meets them, Module 7). Because
each step is rounded to paise, the last month's balance can end a few paise away from zero; real loan
systems adjust the final EMI.

### Example 2: DO UNTIL — years to double an investment at 7%

```sas
data _null_;
    amount = 100000;
    year = 0;
    do until (amount >= 200000);
        year + 1;
        amount = amount * 1.07;
    end;
    put year= amount= comma12.2;
run;
```

**Log:** `year=11 amount=210,485.20`

### Example 3: a calendar of month ends

```sas
data work.month_ends;
    do i = 0 to 11;
        month_end = intnx('month', '01JAN2026'd, i, 'e');
        output;
    end;
    format month_end date9.;
    drop i;
run;
```

12 rows: `31JAN2026`, `28FEB2026`, ..., `31DEC2026`.

### Example 4: DO WHILE vs DO UNTIL

```sas
data _null_;
    x = 5;
    count_while = 0;
    do while (x < 0);  count_while + 1;  end;   /* condition false at the start: runs 0 times */
    count_until = 0;
    do until (x > 0);  count_until + 1;  end;   /* checked at the end: runs once */
    put count_while= count_until=;               /* count_while=0 count_until=1 */
run;
```

### Example 5: LEAVE — stop at the first overdue month

```sas
data work.first_overdue;
    set work.repayments;                 /* acct_id, paid1-paid12 (1 = paid, 0 = missed) */
    array paid{12} paid1-paid12;
    first_missed = .;
    do m = 1 to 12;
        if paid{m} = 0 then do;
            first_missed = m;
            leave;                       /* no need to check later months */
        end;
    end;
    drop m;
run;
```

### ⚠️ Loop traps

- **The index ends one past the end.** After `do i = 1 to 3; end;`, `i` is **4**.
- **A list loop takes its length from the first value.** `do channel = 'ATM', 'ONLINE';` makes
  `channel` 3 characters long, so `'ONLINE'` becomes `'ONL'`. Put `length channel $6;` first.
- **Infinite loops.** A DO WHILE whose condition never becomes false never ends. Add a safety limit:
  `do i = 1 to 1000 while (...)`.
- **Forgetting OUTPUT** inside a loop that should create many rows: you get only the last value.

### SQL Server and Pandas

- SQL Server has `WHILE` loops and recursive CTEs, but set-based SQL avoids loops where possible. A
  number table or `GENERATE_SERIES` (SQL Server 2022) often replaces a loop.
- Pandas usually avoids loops with vectorised column operations. An EMI schedule can be built with
  `numpy` and `cumprod`, but a plain `for` loop is often clearer for amortisation.

### 💼 Banking scenario

Risk teams project each loan's outstanding balance for the next 36 months for IFRS 9 expected-loss
calculations. A DO loop with OUTPUT creates 36 future rows per loan from one input row, applying the
interest and repayment rules month by month.

### Exercises

1. **Level 1:** Print the numbers 1 to 10 to the Log with a DO loop and PUT.
2. **Level 2:** Build the EMI schedule for a 24-month loan at 10.5% and check the final balance.
3. **Level 3:** Use DO UNTIL to find how many months a ₹10,000 monthly SIP at 1% per month needs to
   reach ₹5,00,000.
4. **Level 4 — Interview:** "What is the difference between DO WHILE and DO UNTIL?"
5. **Level 5:** For each loan, create one row per remaining month with the projected balance, stopping
   when the balance reaches zero.

### ⭐ Interview questions

**Q1. DO WHILE vs DO UNTIL?**
- *Strong answer:* "DO WHILE tests the condition at the top, so the loop may not run at all. DO UNTIL
  tests at the bottom, so it always runs at least once."

**Q2. What is the value of `i` after `do i = 1 to 10; end;`?**
- *Strong answer:* "11. The loop increments `i` and then finds it is past the end."

### Module wrap-up

- **I now know:** iterative, list, WHILE and UNTIL loops, LEAVE, CONTINUE and the loop traps.
- **I can now:** generate schedules and projections, and stop loops safely.
- **Next:** Module 38 — arrays.

---

## MODULE 38 — Arrays

**Syllabus items:** 5.15 SAS arrays · 5.16 Array examples

**You will learn:** how arrays let one piece of code work on many variables. **Why it matters:** wide
data (12 months, 24 balances, 50 flags) is common in banking, and arrays turn hundreds of lines into
five. **Before you start:** Module 37.

### 🧠 What an array is

An **array** is a temporary short name for a group of variables, so you can work on them in a loop.

```sas
array bal{6} bal1-bal6;      /* bal{1} means bal1, bal{2} means bal2, ... */
```

- It exists only while the DATA step runs. It is **not** stored in the dataset.
- All variables in one array must be the same type.
- `DIM(bal)` returns the number of elements (6).
- `{*}` lets SAS count the elements: `array bal{*} bal1-bal6;`.

| Declaration | Meaning |
| --- | --- |
| `array bal{6} bal1-bal6;` | Six existing (or new) numeric variables |
| `array flag{6};` | Creates `flag1`–`flag6` |
| `array nm{*} $ name city segment;` | A **character** array (note the `$`) |
| `array nm{3} $20 a b c;` | Character array, length 20 for new variables |
| `array num{*} _numeric_;` | Every numeric variable defined so far |
| `array limit{6} _temporary_ (6000 6000 6000 6000 8000 8000);` | Values only; **no** variables are created or output |

### Example 1: replace missing values and flag negatives across six months

```sas
data work.monthly_bal;
    input acct_id $ bal1-bal6;
    datalines;
A01 5000 . 7000 -200 8000 9000
A02 . . 1500 1600 . 1800
;
run;

data work.bal_clean;
    set work.monthly_bal;
    array bal{6} bal1-bal6;
    array neg_flag{6};                     /* creates neg_flag1-neg_flag6 */
    missing_months = 0;
    do i = 1 to dim(bal);
        if missing(bal{i}) then do;
            missing_months + 1;
            bal{i} = 0;
        end;
        neg_flag{i} = (bal{i} < 0);
    end;
    drop i;
run;
```

**Output**

| acct_id | bal1 | bal2 | bal3 | bal4 | bal5 | bal6 | neg_flag1–6 | missing_months |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| A01 | 5000 | 0 | 7000 | -200 | 8000 | 9000 | 0 0 0 1 0 0 | 1 |
| A02 | 0 | 0 | 1500 | 1600 | 0 | 1800 | 0 0 0 0 0 0 | 3 |

### Example 2: compare each month with its own limit (temporary array)

```sas
data work.limit_check;
    set work.monthly_bal;
    array bal{6} bal1-bal6;
    array limit{6} _temporary_ (6000 6000 6000 6000 8000 8000);
    over_limit_months = 0;
    do i = 1 to 6;
        if bal{i} > limit{i} then over_limit_months + 1;
    end;
    drop i;
run;
```

A01 is over its limit in month 3 (7,000 > 6,000) and month 6 (9,000 > 8,000), so 2. A02 is never over,
so 0. The limits are not written to the output because the array is temporary.

### Example 3: clean many text columns at once

```sas
data work.cust_std;
    set work.customers;
    array txt{*} $ name city segment;
    do i = 1 to dim(txt);
        txt{i} = upcase(strip(txt{i}));
    end;
    drop i;
run;
```

### Example 4: wide to long with an array

```sas
data work.bal_long;
    set work.monthly_bal;
    array bal{6} bal1-bal6;
    do month = 1 to 6;
        balance = bal{month};
        output;
    end;
    keep acct_id month balance;
run;
```

2 accounts × 6 months = 12 rows.

### ⚠️ Common mistakes

- `ERROR: Array subscript out of range` when the loop goes past `DIM`. Always loop `to dim(arr)`.
- Mixing numeric and character variables in one array.
- Forgetting `$` for character arrays.
- Thinking a `_TEMPORARY_` array is saved in the dataset.
- `array x{*} _numeric_;` placed before the variables exist: it only includes numeric variables
  defined **so far** in the step.

### SQL Server and Pandas

- SQL Server has no arrays. Working on 12 columns means writing 12 expressions (or unpivoting).
- Pandas works on many columns at once without arrays: `df[cols] = df[cols].fillna(0)`,
  `(df[cols] < 0).astype(int)`, `df.melt(...)` for wide to long.

### 💼 Banking scenario

A behavioural scorecard uses 24 monthly features per account (balance, utilisation, days past due).
With three arrays and one loop, a SAS step caps outliers, fills missing months, and counts "months
with DPD over 30" for all 72 columns in under 20 lines.

### Exercises

1. **Level 1:** Replace missing values with 0 in `bal1`–`bal6`.
2. **Level 2:** Create `growth2`–`growth6`, each month's change from the previous month.
3. **Level 3:** Count how many months each account had a balance over its own limit.
4. **Level 4 — Interview:** "What is a _TEMPORARY_ array and when would you use it?"
5. **Level 5:** For 12 monthly DPD columns, find the worst DPD, the month it happened, and the number of
   months with DPD over 30.

### ⭐ Interview questions

**Q. What is an array in SAS?**
- *Strong answer:* "A temporary group name for variables of the same type within a DATA step, so I can
  process them in a DO loop with `arr{i}`. It is not stored in the dataset. `_TEMPORARY_` arrays hold
  constants, like limits or lookup values, without creating variables."

### Module wrap-up

- **I now know:** array declarations, DIM, `{*}`, character and temporary arrays, and array + loop
  patterns.
- **I can now:** process dozens of similar columns with a few lines of code.
- **Next:** Module 39 — PROC COMPARE and UPDATE.

---

## MODULE 39 — PROC COMPARE and the UPDATE Statement

**Syllabus items:** 5.5 SAS COMPARE procedure · 5.6 SAS UPDATE statement

**You will learn:** how to compare two datasets value by value, and how to apply changes to a master
dataset. **Why it matters:** comparing outputs is how changes are tested before production, and
master-file updates are standard maintenance jobs. **Before you start:** Modules 18 and 33.

### PROC COMPARE (5.5)

```sas
data work.prod_bal;
    input acct_id $ balance status $;
    datalines;
A01 5000 A
A02 1800 A
A03 900 D
;
run;

data work.dev_bal;
    input acct_id $ balance status $;
    datalines;
A01 5000 A
A02 1850 A
A04 100 A
;
run;

proc compare base=work.prod_bal compare=work.dev_bal
             out=work.diffs outnoequal outbase outcomp outdif
             method=absolute criterion=0.01;
    id acct_id;
run;
```

**Report (simplified main parts)**

```text
Observation Summary
  Number of Observations in Common: 2.
  Number of Observations in WORK.PROD_BAL but not in WORK.DEV_BAL: 1.
  Number of Observations in WORK.DEV_BAL but not in WORK.PROD_BAL: 1.
  Number of Observations with Some Compared Variables Unequal: 1.

Value Comparison Results for Variables
           ||       Base    Compare
  acct_id  ||    balance    balance      Diff.     % Diff
  ________ ||  _________  _________  _________  _________
  A02      ||  1800.0000  1850.0000    50.0000     2.7778
```

| Option | Meaning |
| --- | --- |
| `base=` / `compare=` | The trusted dataset and the one being checked |
| `id acct_id;` | Match rows by this key (both datasets sorted by it). Without ID, rows are matched by position. |
| `out=` with `outnoequal outbase outcomp outdif` | Save rows that differ, with the base value, the compare value and the difference |
| `method=absolute criterion=0.01` | Treat numbers within 0.01 of each other as equal (ignore tiny rounding differences) |
| `listall` | List every row and variable found in only one dataset |
| `var` / `with` | Compare only some variables, or variables with different names |

📌 After PROC COMPARE, the automatic macro variable `&SYSINFO` is **0** if the datasets match. Any
other value is a sum of codes describing the differences (for example, 4096 means at least one value
differs). Automated jobs use it to pass or fail a test.

### The UPDATE statement (5.6)

UPDATE applies changes from a **transaction** dataset to a **master** dataset, matched by a BY
variable.

```sas
data work.cust_master;
    length cust_id $4 city $10 phone $10;
    input cust_id $ city $ phone $ fico;
    datalines;
C101 Mumbai 9820123456 742
C102 Delhi 9876543210 688
C103 Pune 9822000000 615
;
run;

data work.cust_updates;
    length cust_id $4 city $10 phone $10;
    input cust_id $ city $ phone $ fico;
    datalines;
C101 Thane . 760
C103 . 9811111111 .
C104 Chennai 9000000001 701
;
run;

data work.cust_master_new;
    update work.cust_master work.cust_updates;
    by cust_id;
run;
```

**Output**

| cust_id | city | phone | fico |
| --- | --- | --- | --- |
| C101 | **Thane** | 9820123456 | **760** |
| C102 | Delhi | 9876543210 | 688 |
| C103 | Pune | **9811111111** | 615 |
| C104 | Chennai | 9000000001 | 701 |

**Why:** C101's city and FICO changed, but its phone stayed, because a **missing value in the
transaction does not overwrite** the master. C103 changed only its phone. C102 had no change. C104 is
new, so it was **added**.

**UPDATE rules**

| Rule | Detail |
| --- | --- |
| Sorted | Both datasets sorted by the BY variables |
| Master keys | Must be unique in the master |
| Transaction keys | Can repeat; the changes are applied in order |
| Missing values | Do not overwrite (set `UPDATEMODE=NOMISSINGCHECK` to allow it, or use the special missing value `._` in the transaction to force a blank) |
| New keys | Added as new rows |

### UPDATE vs MERGE vs MODIFY

| | UPDATE | MERGE | MODIFY |
| --- | --- | --- | --- |
| Missing values in the second dataset | Ignored | **Overwrite** | Your code decides |
| Repeated keys in the first dataset | Not allowed | Allowed | Allowed |
| Output | A new dataset | A new dataset | Changes the dataset **in place** (no rewrite) |

📌 Interview trap: **SQL Server's `MERGE` statement is an "upsert", which is what SAS calls UPDATE.**
SAS's `MERGE` is a join. Same word, different meaning.

### SQL Server and Pandas

| Task | SAS | SQL Server | Pandas |
| --- | --- | --- | --- |
| Compare two tables | `PROC COMPARE` | `EXCEPT` both ways | `df1.compare(df2)` (same shape) or `merge(indicator=True)` |
| Upsert with non-missing values | `UPDATE` | `MERGE ... WHEN MATCHED THEN UPDATE ... WHEN NOT MATCHED THEN INSERT` | `master.update(changes)` plus `concat` for new rows |

### 💼 Banking scenario

Before a new interest-calculation program goes live, the team runs old and new code on the same
month's data. PROC COMPARE with `ID account_id` and `method=absolute criterion=0.005` must report zero
differences (`&SYSINFO = 0`) on 4 million accounts. The comparison report is attached to the change
request as UAT evidence.

### ⚠️ Common mistakes

- Comparing without `ID`, so one extra row shifts every later row and everything looks different.
- Forgetting tolerance for floating-point sums, and chasing differences in the 12th decimal place.
- Using MERGE for master updates and wiping good values with missing ones.
- Duplicate keys in the UPDATE master (`WARNING: The MASTER data set contains more than one
  observation for a BY group.`).

### Exercises

1. **Level 1:** Compare two copies of a dataset where one value differs.
2. **Level 2:** Save only the differing rows with `OUT=` and `OUTNOEQUAL`.
3. **Level 3:** Apply a day's customer changes to a master with UPDATE, including new customers.
4. **Level 4 — Interview:** "How is UPDATE different from MERGE?"
5. **Level 5:** Build an automated regression test: run PROC COMPARE, check `&SYSINFO`, and write PASS
   or FAIL to a log dataset.

### ⭐ Interview questions

**Q1. UPDATE vs MERGE?**
- *Strong answer:* "UPDATE applies transactions to a master with unique keys: missing values in the
  transaction do not overwrite, and new keys are added. MERGE joins datasets, and a missing value in a
  later dataset does overwrite. Also, SQL Server's MERGE corresponds to SAS UPDATE, not SAS MERGE."

**Q2. How do you check that a code change did not alter results?**
- *Strong answer:* "Run old and new code on the same input and use PROC COMPARE with an ID statement
  and a small tolerance. `&SYSINFO` equal to 0 means identical, and I keep the report as test
  evidence."

### Module wrap-up

- **I now know:** PROC COMPARE with ID, OUT options, tolerance and SYSINFO; the UPDATE statement and
  its rules; UPDATE vs MERGE vs MODIFY.
- **I can now:** test changes with evidence and maintain master datasets safely.
- **Next:** Mini Project 3, then Part VII — reporting.

---

## Mini Project 3 — Bank Transaction Fraud Analysis

**Uses:** Parts I–VI. **Domain:** fraud analytics.

**Business requirement:** the fraud team wants a daily process that finds suspicious card and UPI
transactions and summarises risk by customer and merchant.

**Source:** CSV, TXT and a SQL database table (simulate the database with a SAS dataset if you have no
database).

**Process**

```text
Raw data -> SAS ingestion -> Data validation -> Cleaning -> Transformation
         -> Deduplication -> Aggregation -> Fraud rules -> Reporting
```

**Requirements**

- 10 million+ transactions (generate them with a DATA step loop and RAND; Modules 20, 37)
- Columns: customer ID, transaction ID, merchant, transaction amount, transaction date and time,
  location (city), transaction type (POS, ONLINE, ATM, UPI) and fraud flag

**Tasks**

1. **Import data** with DATA steps, explicit lengths and informats (Module 8).
2. **Clean data:** standardise merchant names and cities, fix case and spaces (Module 21).
3. **Validate data:** missing IDs, negative or zero amounts, future dates, unknown types; send failures
   to a reject dataset (Modules 17 and 58).
4. **Remove duplicates** on transaction ID, keeping the latest load (Module 18).
5. **Create derived variables:** hour of day, weekday, night flag (00:00–05:00), amount band, days since
   the customer's previous transaction (Modules 23 and 34).
6. **Identify suspicious transactions** with rules such as:
   - 3 or more transactions on the same card within 10 minutes (RETAIN, FIRST., Module 34)
   - an amount over 5 times the customer's 90-day average (PROC SQL remerging or MERGE, Modules 29 and 33)
   - transactions in two different cities within one hour
   - night-time high-value online transactions
   - customer on a watch list (hash lookup, Module 33)
7. **Aggregate by customer:** count, total, suspicious count and share (PROC SQL or PROC SUMMARY).
8. **Aggregate by merchant:** volume, fraud rate and average amount.
9. **Rank merchants** by fraud rate within merchant category (PROC RANK, Module 35).
10. **Generate summary reports** (Part VII: PROC REPORT and ODS EXCEL).
11. **Export** the final suspicious-transaction dataset to CSV for the case management system (Module
    10).
12. **Create a reusable macro** that runs the whole process for any date (Part VIII).
13. **Generate an automated report** that emails or saves the daily summary (Module 55).

**What it proves:** you can apply BY-group logic, joins, ranking and rules to a realistic fraud
problem at scale. Mention the run time you achieved and the optimisations you used.

**Part VI checklist:** ✓ 4.19 · ✓ 5.1 · ✓ 5.2 · ✓ 5.3 · ✓ 5.5 · ✓ 5.6 · ✓ 5.7 · ✓ 5.8 · ✓ 5.9 · ✓ 5.13 · ✓ 5.14 · ✓ 5.15 ·
✓ 5.16 · ✓ 7.18 (with Module 31)

---

# Part VII — Reporting, Summary Statistics and Charts (Modules 40–46)

All examples use `work.txn` from Module 5. The amounts are 5,000, 125,000, 2,300, missing, 20,000 and
78,000.

## MODULE 40 — List Reports (PROC PRINT) and ODS

**Syllabus items:** 2.10 List Report · 2.11 ODS

**You will learn:** how to produce clean detail listings, and how the Output Delivery System sends any
procedure's output to HTML, PDF, Excel or a dataset. **Why it matters:** every report you build ends
up in a file someone opens. **Before you start:** Module 18.

### List reports with PROC PRINT (2.10)

A **list report** shows the detail rows of a dataset, one line per observation.

```sas
proc sort data=work.txn out=work.txn_by_cust;
    by cust_id txn_date;
run;

title "Transactions by Customer";
footnote "Source: core banking extract";

proc print data=work.txn_by_cust label n;
    by cust_id;
    id txn_id;
    var txn_date channel amount;
    sum amount;
    label txn_id   = 'Txn ID'
          txn_date = 'Date'
          amount   = 'Amount (Rs)';
    format amount comma12.;
run;

title;  footnote;     /* clear them so later output is not affected */
```

**Output (one BY group shown)**

```text
                        Transactions by Customer

-------------------------------- cust_id=C101 ---------------------------------
   Txn ID    Date         channel     Amount (Rs)
   T001      02JAN2026    ATM               5,000
   T003      05JAN2026    POS               2,300
   T006      12JAN2026    ONLINE           78,000
   -------                            -----------
   cust_id                                 85,300
                              N = 3
```

| Statement / option | Purpose |
| --- | --- |
| `noobs` | Hide the `Obs` row-number column (not needed here because `ID` replaces it) |
| `label` | Show variable labels instead of names as column headings |
| `n` | Print the number of rows at the end of each BY group |
| `by` | One section per BY group (data must be sorted) |
| `id` | Use this column instead of `Obs` to identify rows |
| `var` | Which columns to show, and in what order |
| `sum` | Totals for these columns (per BY group and overall) |
| `where` | Filter rows for this report only |
| `(obs=20)` after the dataset name | Print only the first 20 rows (for quick checks) |

### ODS: the Output Delivery System (2.11)

🧠 Every procedure produces **output objects** (tables and graphs). ODS decides where they go and how
they look.

```text
PROC MEANS / FREQ / REPORT ...  --->  output objects  --->  ODS  --->  HTML  (Results Viewer)
                                                                  --->  PDF   (ODS PDF)
                                                                  --->  Excel (ODS EXCEL)
                                                                  --->  RTF / Word (ODS RTF)
                                                                  --->  text  (ODS LISTING)
                                                                  --->  SAS dataset (ODS OUTPUT)
```

**Excel workbook with several sheets**

```sas
ods excel file="C:\sasdata\out\branch_pack.xlsx"
          options(sheet_name="Summary" embedded_titles="yes");

title "Customer Summary";
proc print data=work.cust_summary noobs;
run;

ods excel options(sheet_name="Detail");
title "All Transactions";
proc print data=work.txn noobs;
run;

ods excel close;
title;
```

**PDF report**

```sas
ods pdf file="C:\sasdata\out\cust_report.pdf" style=journal;
title "Customer Summary";
proc print data=work.cust_summary noobs;
run;
ods pdf close;
title;
```

📌 Always **close** a destination (`ods pdf close;`). The file is not complete until you do.

**ODS OUTPUT: turn any printed table into a dataset**

```sas
ods trace on;                         /* writes each output object's name to the Log */
proc means data=work.txn n sum mean;
    var amount;
run;
ods trace off;
```

The Log shows `Output Added: Name: Summary ...`. Now capture it:

```sas
ods output Summary=work.means_out;    /* the table named Summary goes to a dataset */
proc means data=work.txn n sum mean;
    var amount;
run;
```

**Choosing which tables appear**

```sas
ods select Moments Quantiles;         /* only these two tables from the next procedure */
proc univariate data=work.txn;
    var amount;
run;
```

### SQL Server and Pandas

| Task | SAS | SQL Server | Pandas |
| --- | --- | --- | --- |
| Detail listing | PROC PRINT | `SELECT` in SSMS / SSRS report | `df.head()`, `display(df)` |
| Excel output | `ODS EXCEL` | SSRS / SSIS export | `df.to_excel()` with `ExcelWriter` |
| PDF output | `ODS PDF` | SSRS | `matplotlib` / `reportlab` |
| Printed table to data | `ODS OUTPUT` | `INSERT INTO ... EXEC` | The DataFrame is already data |

### 💼 Banking scenario

A monthly regulatory pack has 12 tables. One program wraps all the procedures between
`ods pdf file=...;` and `ods pdf close;`, adding a title page and page numbers. The same program with
`ods excel` produces the editable version for the finance team.

### ⚠️ Common mistakes

- Forgetting to close an ODS destination: the file is empty or corrupt.
- Titles from one report appearing on the next. Clear them with `title;`.
- PROC PRINT on millions of rows. Use `(obs=)` or a summary.

### Exercises

1. **Level 1:** Print `work.txn` with labels and no Obs column.
2. **Level 2:** Print by customer with totals per customer.
3. **Level 3:** Send two reports to two sheets of one Excel file.
4. **Level 4 — Interview:** "What is ODS and how do you save a procedure's table as a dataset?"
5. **Level 5:** Build a PDF with a title, a summary table, a detail table and a chart.

### ⭐ Interview questions

**Q. What is ODS?**
- *Strong answer:* "The Output Delivery System. Procedures create output objects, and ODS sends them to
  destinations such as HTML, PDF, RTF, Excel or a SAS dataset, using styles for appearance. I use ODS
  TRACE to find object names, ODS OUTPUT to capture tables as data, and ODS SELECT to choose which
  tables print."

### Module wrap-up

- **I now know:** PROC PRINT options, ODS destinations, ODS EXCEL, ODS PDF, ODS TRACE, OUTPUT and
  SELECT.
- **I can now:** produce listings and send any output to the format the business needs.
- **Next:** Module 41 — summary statistics.

---

## MODULE 41 — Summary Reports: PROC MEANS and PROC SUMMARY

**Syllabus items:** 6.4 Summary reports · 6.5 PROC MEANS · 6.6 PROC SUMMARY

**You will learn:** how to summarise numeric data by groups, print it or save it as a dataset, and
the difference between MEANS and SUMMARY. **Why it matters:** summaries are the most common report.
**Before you start:** Module 29.

### Summary reports (6.4)

A **summary report** shows totals, counts or averages per group instead of every detail row. In SAS
you can build one with PROC SQL (Module 29), PROC MEANS or SUMMARY (this module), PROC REPORT
(Module 44) or PROC TABULATE (Module 45).

### PROC MEANS (6.5)

```sas
proc means data=work.txn n nmiss sum mean min max maxdec=0;
    class channel;
    var amount;
run;
```

**Output**

| channel | N Obs | N | N Miss | Sum | Mean | Minimum | Maximum |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ATM | 2 | 2 | 0 | 25000 | 12500 | 5000 | 20000 |
| ONLINE | 3 | 2 | 1 | 203000 | 101500 | 78000 | 125000 |
| POS | 1 | 1 | 0 | 2300 | 2300 | 2300 | 2300 |

`N Obs` counts rows; `N` counts non-missing values. ONLINE has 3 rows but only 2 amounts.

**Without any statistic keywords**, PROC MEANS shows N, Mean, Std Dev, Minimum and Maximum.

**Useful statistic keywords:** `N NMISS SUM MEAN MEDIAN MIN MAX STD VAR RANGE CV P1 P5 Q1 Q3 P95 P99
QRANGE`.

### Saving the results: OUTPUT OUT=

```sas
proc means data=work.txn noprint;
    class channel;
    var amount;
    output out=work.chan_stats sum=total_amt mean=avg_amt n=txn_n;
run;
```

**Output dataset**

| channel | _TYPE_ | _FREQ_ | total_amt | avg_amt | txn_n |
| --- | --- | --- | --- | --- | --- |
| (blank) | 0 | 6 | 230300 | 46060 | 5 |
| ATM | 1 | 2 | 25000 | 12500 | 2 |
| ONLINE | 1 | 3 | 203000 | 101500 | 2 |
| POS | 1 | 1 | 2300 | 2300 | 1 |

- `_TYPE_ = 0` is the **overall** row (all channels). `_TYPE_ = 1` rows are per channel.
- `_FREQ_` is the number of rows in each group.
- Add `NWAY` to the PROC statement to keep only the most detailed level (here, only the channel rows).
- With several CLASS variables, `_TYPE_` numbers every combination of subtotals, like SQL Server's
  `GROUP BY ROLLUP` or `CUBE`.
- With several VAR variables, use `autoname` to name the outputs automatically (`amount_Sum`,
  `amount_Mean`, ...).

### CLASS vs BY

| | CLASS | BY |
| --- | --- | --- |
| Needs sorted data | No | Yes |
| Memory | Keeps all groups in memory | One group at a time |
| Subtotal levels (`_TYPE_`) | Yes | No |
| Best for | Most cases | Huge data with very many groups, already sorted |

⚠️ By default, rows with a **missing CLASS value** are left out. Add the `MISSING` option to keep them
as their own group.

### PROC SUMMARY (6.6)

PROC SUMMARY uses the same engine as PROC MEANS. The differences:

| | PROC MEANS | PROC SUMMARY |
| --- | --- | --- |
| Prints results by default | Yes | No (add `PRINT` to print) |
| No VAR statement | Analyses every numeric variable | Gives only counts (`_FREQ_`) |
| Typical use | Quick look at statistics | Building summary datasets in programs |

```sas
proc summary data=work.txn nway;
    class cust_id;
    var amount;
    output out=work.cust_stats (drop=_type_ _freq_)
           n=txn_count sum=total_amt mean=avg_amt max=max_amt;
run;
```

### SQL Server and Pandas

| Task | SAS | SQL Server | Pandas |
| --- | --- | --- | --- |
| Stats per group | `PROC MEANS ... CLASS` | `GROUP BY` | `groupby().agg()` |
| Overall + per group | `_TYPE_` levels | `GROUP BY ROLLUP(channel)` | `groupby` plus a total row |
| Median | `MEDIAN` keyword | `PERCENTILE_CONT(0.5) WITHIN GROUP` | `.median()` |
| Describe everything | `PROC MEANS` with no VAR | — | `df.describe()` |

### 💼 Banking scenario

A daily summary of card spend by merchant category and city uses `PROC SUMMARY` with two CLASS
variables. The output's `_TYPE_` gives four levels in one pass: overall, by category, by city, and by
category × city. That feeds four dashboard tiles without four separate queries.

### ⚠️ Common mistakes

- Confusing `N Obs` with `N`.
- Forgetting `NWAY` and getting overall rows mixed with group rows.
- Losing missing CLASS values without noticing (use `MISSING`).
- Using BY without sorting.

### Exercises

1. **Level 1:** Total and average amount per channel.
2. **Level 2:** Save per-customer statistics to a dataset with PROC SUMMARY.
3. **Level 3:** Use two CLASS variables and explain each `_TYPE_` value.
4. **Level 4 — Interview:** "What is the difference between PROC MEANS and PROC SUMMARY?"
5. **Level 5:** Produce median, 95th and 99th percentile spend per customer segment.

### ⭐ Interview questions

**Q1. PROC MEANS vs PROC SUMMARY?**
- *Strong answer:* "Same engine. MEANS prints by default and analyses all numeric variables if there is
  no VAR statement. SUMMARY does not print unless asked and, with no VAR, gives only counts. I use
  SUMMARY with OUTPUT OUT= to build summary datasets."

**Q2. What are `_TYPE_` and `_FREQ_`?**
- *Strong answer:* "`_FREQ_` is the number of rows in each group. `_TYPE_` identifies which combination
  of CLASS variables the row summarises: 0 is the overall total. NWAY keeps only the most detailed
  level."

### Module wrap-up

- **I now know:** PROC MEANS and SUMMARY, statistic keywords, CLASS vs BY, OUTPUT OUT=, `_TYPE_`,
  `_FREQ_` and NWAY.
- **I can now:** produce summary reports and summary datasets at any level of detail.
- **Next:** Module 42 — PROC UNIVARIATE.

---

## MODULE 42 — PROC UNIVARIATE

**Syllabus items:** 6.7 PROC UNIVARIATE

**You will learn:** how to study the full distribution of a variable: averages, spread, percentiles,
extreme values and normality. **Why it matters:** outlier detection and percentile limits are central
to fraud and risk work. **Before you start:** Module 41.

### Example

```sas
proc univariate data=work.txn nextrobs=3;
    var amount;
    id txn_id;
run;
```

**Main parts of the output (simplified)**

```text
Moments
  N                     5      Sum Weights           5
  Mean              46060      Sum Observations  230300
  Std Deviation  53692.81

Basic Statistical Measures
  Mean     46060.00      Std Deviation   53692.81
  Median   20000.00      Range          122700.00

Quantiles (Definition 5)
  100% Max   125000
  75% Q3      78000
  50% Median  20000
  25% Q1       5000
  0% Min       2300

Extreme Observations
  ------Lowest------      ------Highest-----
   Value   txn_id          Value   txn_id
    2300   T003            20000   T005
    5000   T001            78000   T006
   20000   T005           125000   T002

Missing Values
  Missing Value   Count   Percent of All Obs
  .                   1                16.67
```

**How to read it:** the mean (46,060) is much larger than the median (20,000), so a few large values
pull the average up. That is normal for transaction amounts, and it is why fraud teams use percentiles
rather than averages to set limits.

| Statement / option | Purpose |
| --- | --- |
| `var` | Variables to analyse |
| `id` | Show this column next to the extreme values, so you can find them |
| `nextrobs=n` | How many extreme values to list (default 5) |
| `normal` | Add tests of whether the data is normally distributed |
| `histogram amount;` | Draw a histogram (with ODS Graphics) |
| `class` / `by` | Separate analysis per group |
| `output out= pctlpts= pctlpre=` | Save chosen percentiles to a dataset |

### Saving percentiles for outlier rules

```sas
proc univariate data=bank.transactions noprint;
    var amount;
    output out=work.amt_pctl pctlpts=95 99 99.9 pctlpre=amt_p;
run;
/* creates amt_p95, amt_p99 and amt_p99_9 (the dot becomes an underscore) */
```

A typical next step: flag transactions above the 99.9th percentile for review, or **cap** values at the
99th percentile before building a model.

### SQL Server and Pandas

| Task | SAS | SQL Server | Pandas |
| --- | --- | --- | --- |
| Percentiles | `PROC UNIVARIATE`, `PROC MEANS P99` | `PERCENTILE_CONT(0.99) WITHIN GROUP (ORDER BY amount) OVER ()` | `df["amount"].quantile(0.99)` |
| Full distribution | `PROC UNIVARIATE` | Several queries | `df["amount"].describe()` |
| Extreme values | Extreme Observations table | `TOP n ... ORDER BY` | `nlargest()`, `nsmallest()` |
| Normality test | `NORMAL` option | — | `scipy.stats.shapiro` |

### 💼 Banking scenario

The fraud team sets "unusual amount" thresholds per merchant category at the 99.5th percentile of the
last 90 days. PROC UNIVARIATE with `CLASS merchant_category` and `OUTPUT PCTLPTS=99.5` creates the
threshold table every week, and the scoring job joins to it.

### ⚠️ Common mistakes

- Using the mean to describe skewed amounts.
- Printing full output for hundreds of groups. Use `NOPRINT` and `OUTPUT`, or `ODS SELECT`.
- Forgetting that `pctlpre=` names change `99.9` into `99_9`.

### Exercises

1. **Level 1:** Run PROC UNIVARIATE on transaction amount and find the median.
2. **Level 2:** List the 10 largest transactions with their IDs.
3. **Level 3:** Save the 95th and 99th percentiles per channel to a dataset.
4. **Level 4 — Interview:** "How would you find outliers in SAS?"
5. **Level 5:** Cap amounts at each channel's 99th percentile and compare the mean before and after.

### ⭐ Interview questions

**Q. How do you detect outliers in SAS?**
- *Strong answer:* "PROC UNIVARIATE shows extreme observations with an ID, quantiles and a histogram.
  For rules, I save percentiles with OUTPUT PCTLPTS=, then flag or cap values above, say, the 99th
  percentile. I can also use the interquartile range: below Q1 − 1.5 × IQR or above Q3 + 1.5 × IQR."

### Module wrap-up

- **I now know:** PROC UNIVARIATE's moments, quantiles, extremes, missing values, histograms and
  OUTPUT.
- **I can now:** analyse distributions and set percentile-based thresholds.
- **Next:** Module 43 — PROC FREQ.

---

## MODULE 43 — PROC FREQ

**Syllabus items:** 6.8 PROC FREQ

**You will learn:** one-way and two-way frequency tables, the options that control them, and using
PROC FREQ for data checks. **Why it matters:** counting categories is the first step in profiling any
dataset. **Before you start:** Module 19.

### One-way tables

```sas
proc freq data=work.txn order=freq;
    tables channel / nocum;
run;
```

**Output**

| channel | Frequency | Percent |
| --- | --- | --- |
| ONLINE | 3 | 50.00 |
| ATM | 2 | 33.33 |
| POS | 1 | 16.67 |

`ORDER=FREQ` puts the most common value first. `NOCUM` hides the cumulative columns.

### Two-way tables (crosstabs)

```sas
proc freq data=work.txn;
    tables cust_id * channel / norow nocol nopercent;
run;
```

**Output (counts only)**

| cust_id | ATM | ONLINE | POS | Total |
| --- | --- | --- | --- | --- |
| C101 | 1 | 1 | 1 | 3 |
| C102 | 1 | 1 | 0 | 2 |
| C103 | 0 | 1 | 0 | 1 |
| Total | 2 | 3 | 1 | 6 |

### Important options

| Option | Effect |
| --- | --- |
| `MISSING` | Count missing values as a category (by default they are left out of percentages) |
| `NOCUM`, `NOPERCENT`, `NOROW`, `NOCOL` | Hide those columns or cell percentages |
| `LIST` | Show a two-way table as a list (one line per combination) |
| `OUT=` | Save the counts to a dataset |
| `ORDER=FREQ` | Most frequent first |
| `NLEVELS` (on the PROC statement) | Number of different values per variable |
| `CHISQ` | Chi-square test of association |
| `WEIGHT var;` | Count using a weight (for example amount-weighted shares) |
| `FORMAT` | Group values with a format (Module 19) |

### PROC FREQ for data checks

```sas
/* how many different values does each column have? */
proc freq data=work.txn nlevels;
    tables cust_id channel / noprint;
run;
/* NLEVELS table: cust_id 3 levels, channel 3 levels */

/* which customers appear more than once? */
proc freq data=work.txn noprint;
    tables cust_id / out=work.cust_counts (where=(count > 1));
run;
/* work.cust_counts: C101 (COUNT=3), C102 (COUNT=2) */
```

The `OUT=` dataset has the value, `COUNT` and `PERCENT`. Filtering `count > 1` is a quick **duplicate
key check** — for a transaction ID column, any row in the output is a problem.

### SQL Server and Pandas

| Task | SAS | SQL Server | Pandas |
| --- | --- | --- | --- |
| Counts | `TABLES x` | `GROUP BY x` with `COUNT(*)` | `value_counts()` |
| Percent | Automatic | `COUNT(*) * 100.0 / SUM(COUNT(*)) OVER ()` | `value_counts(normalize=True)` |
| Crosstab | `TABLES x * y` | `PIVOT` | `pd.crosstab(x, y)` |
| Distinct count | `NLEVELS` | `COUNT(DISTINCT x)` | `nunique()` |
| Test of association | `CHISQ` | — | `scipy.stats.chi2_contingency` |

### 💼 Banking scenario

Before a fraud model is built, analysts run PROC FREQ on every categorical field: `channel`,
`merchant_category`, `country`, `fraud_flag`. They check for unexpected codes, missing values and how
rare fraud is (often well under 1% of transactions). `TABLES channel * fraud_flag / CHISQ` shows which
channels have a higher fraud rate.

### ⚠️ Common mistakes

- Forgetting `MISSING`, so percentages hide missing values.
- Running two-way tables on high-cardinality columns (thousands of rows of output).
- Reading row percent as column percent.

### Exercises

1. **Level 1:** Frequency of transactions per channel, most common first.
2. **Level 2:** Crosstab of customer by channel with counts only.
3. **Level 3:** Find duplicate transaction IDs with `OUT=`.
4. **Level 4 — Interview:** "How do you check a dataset for duplicate keys quickly?"
5. **Level 5:** Fraud rate per channel and per merchant category, with a chi-square test.

### ⭐ Interview questions

**Q. How do you count distinct values of every column quickly?**
- *Strong answer:* "PROC FREQ with the NLEVELS option and `TABLES _ALL_ / NOPRINT;` gives the number of
  levels for every variable without printing huge tables."

### Module wrap-up

- **I now know:** one-way and two-way tables, the main options, NLEVELS, OUT= and CHISQ.
- **I can now:** profile categorical data and run quick data-quality checks.
- **Next:** Module 44 — PROC REPORT.

---

## MODULE 44 — PROC REPORT

**Syllabus items:** 6.9 PROC REPORT

**You will learn:** how to build business-ready tables with groups, totals, computed columns and
columns spread across. **Why it matters:** PROC REPORT is the standard tool for formatted management
reports in SAS. **Before you start:** Modules 40 and 41.

### 🧠 How PROC REPORT thinks

- `COLUMN` lists the columns in order.
- `DEFINE` says how each column is used:

| Usage | Meaning |
| --- | --- |
| `DISPLAY` | Show each row's value (detail report) |
| `ORDER` | Show and sort by this value; repeated values shown once |
| `GROUP` | Collapse rows into one line per value (like GROUP BY) |
| `ACROSS` | Spread the values into columns (like a pivot) |
| `ANALYSIS` | A number to summarise (`SUM`, `MEAN`, ...) |
| `COMPUTED` | A new column calculated in a `COMPUTE` block |

- `BREAK` adds subtotals after groups; `RBREAK` adds a grand total.

### A grouped report with a computed column

```sas
data work.txn_r;
    set work.txn;
    txn_count = 1;             /* one per row, so its SUM is the row count */
run;

title "Transactions by Channel";
proc report data=work.txn_r nowd;
    column channel txn_count amount avg_amt;
    define channel   / group 'Channel';
    define txn_count / analysis sum 'Transactions';
    define amount    / analysis sum format=comma12. 'Total Amount';
    define avg_amt   / computed format=comma12.2 'Average per Transaction';
    compute avg_amt;
        avg_amt = amount.sum / txn_count.sum;
    endcomp;
    rbreak after / summarize style=[font_weight=bold];
run;
title;
```

**Output**

| Channel | Transactions | Total Amount | Average per Transaction |
| --- | --- | --- | --- |
| ATM | 2 | 25,000 | 12,500.00 |
| ONLINE | 3 | 203,000 | 67,666.67 |
| POS | 1 | 2,300 | 2,300.00 |
| **(total)** | **6** | **230,300** | **38,383.33** |

📌 **Look at ONLINE.** PROC MEANS gave a mean of 101,500 (it ignores the missing amount, dividing by
2). This report divides by 3 transactions. Neither is wrong; they answer different questions. Always
decide what the denominator should be.

| Code | Meaning |
| --- | --- |
| `nowd` | No interactive window (only matters in SAS for Windows; harmless elsewhere) |
| `amount.sum` | Inside a COMPUTE block, an analysis variable is referred to as `variable.statistic` |
| `compute avg_amt; ... endcomp;` | Calculates the computed column for every row, including the total row |
| `rbreak after / summarize` | Adds a grand-total row at the end |

### ACROSS: spreading values into columns

```sas
proc report data=work.txn_r nowd;
    column cust_id channel,amount amount=total;
    define cust_id / group 'Customer';
    define channel / across 'Channel';
    define amount  / analysis sum format=comma12. ' ';
    define total   / analysis sum format=comma12. 'Total';
    rbreak after / summarize;
run;
```

**Output**

| Customer | ATM | ONLINE | POS | Total |
| --- | --- | --- | --- | --- |
| C101 | 5,000 | 78,000 | 2,300 | 85,300 |
| C102 | 20,000 | 125,000 | . | 145,000 |
| C103 | . | . | . | . |
| (total) | 25,000 | 203,000 | 2,300 | 230,300 |

`channel,amount` (with a comma) means "amount under each channel". `amount=total` creates a second
copy of `amount` called `total`, used for the row total. C103's only transaction has a missing amount,
so its cells are missing.

### Subtotals with BREAK

With two GROUP columns (for example `branch` and `channel`), `break after branch / summarize;` adds a
subtotal line after each branch, and `rbreak after / summarize;` adds the grand total.

### Highlighting with style

```sas
compute amount;
    if amount.sum > 100000 then
        call define(_col_, 'style', 'style=[background=lightyellow]');
endcomp;
```

### SQL Server and Pandas

| Task | PROC REPORT | SQL Server | Pandas |
| --- | --- | --- | --- |
| Grouped report | `GROUP` + `ANALYSIS` | `GROUP BY` | `groupby().agg()` |
| Spread across | `ACROSS` | `PIVOT` | `pivot_table()` |
| Grand total | `RBREAK` | `ROLLUP` | `.loc["Total"] = df.sum()` |
| Formatting | `FORMAT=`, `STYLE=` | SSRS | `df.style` |

### 💼 Banking scenario

A monthly collections report shows, per region and DPD bucket (ACROSS), the number of accounts and
outstanding amount, with region subtotals, a grand total, and cells over a threshold highlighted. It
is sent to the regional heads as a PDF through ODS every month.

### ⚠️ Common mistakes

- Referring to an analysis variable by its plain name in a COMPUTE block (use `amount.sum`).
- Computing a column that depends on a column listed **after** it in `COLUMN` (PROC REPORT works left
  to right).
- Forgetting the comma in `channel,amount` for ACROSS.

### Exercises

1. **Level 1:** A report of total amount per channel with a grand total.
2. **Level 2:** Add a computed "share of total" column.
3. **Level 3:** A customer × channel report using ACROSS with row totals.
4. **Level 4 — Interview:** "What is the difference between GROUP and ORDER in PROC REPORT?"
5. **Level 5:** A two-level report (branch, channel) with subtotals, a grand total and highlighting of
   branches whose average amount is above the overall average.

### ⭐ Interview questions

**Q. GROUP vs ORDER vs DISPLAY in PROC REPORT?**
- *Strong answer:* "DISPLAY shows every row's value. ORDER sorts by the variable and shows each value
  once, but still lists all rows. GROUP collapses rows into one line per value and summarises the
  analysis variables, like GROUP BY."

### Module wrap-up

- **I now know:** COLUMN, DEFINE usages, COMPUTE blocks, BREAK, RBREAK, ACROSS and CALL DEFINE.
- **I can now:** build formatted management reports with totals and calculations.
- **Next:** Module 45 — PROC TABULATE.

---

## MODULE 45 — PROC TABULATE

**Syllabus items:** 6.10 PROC TABULATE

**You will learn:** how to build multi-dimensional summary tables (rows × columns × pages) with totals.
**Why it matters:** TABULATE produces publication-style tables in very little code. **Before you
start:** Module 41.

### 🧠 The TABLE statement

```text
TABLE  page-dimension ,  row-dimension ,  column-dimension ;
                     ^ commas separate the dimensions

   *      crosses (nests) items:            channel * amount
   space  places items side by side:        channel all
   ALL    adds a total
   ='x'   sets a label
   f=     sets a format
```

### Example

```sas
proc tabulate data=work.txn format=comma12.;
    class cust_id channel;
    var amount;
    table cust_id all='All customers',
          (channel all='All channels') * amount=' ' * sum=' ';
run;
```

**Output**

| | ATM | ONLINE | POS | All channels |
| --- | --- | --- | --- | --- |
| C101 | 5,000 | 78,000 | 2,300 | 85,300 |
| C102 | 20,000 | 125,000 | . | 145,000 |
| C103 | . | . | . | . |
| **All customers** | **25,000** | **203,000** | **2,300** | **230,300** |

- `class` lists the grouping variables; `var` lists the analysis variables.
- `amount=' '` and `sum=' '` remove those headings so the table is cleaner.
- Empty cells show `.` (change it with `misstext='0'` in the TABLE statement's options).

**Several statistics at once**

```sas
proc tabulate data=work.txn;
    class channel;
    var amount;
    table channel all='Total',
          amount * (n='Count' sum='Total'*f=comma12. mean='Average'*f=comma12.2);
run;
```

### PROC TABULATE vs PROC REPORT vs PROC MEANS

| | TABULATE | REPORT | MEANS / SUMMARY |
| --- | --- | --- | --- |
| Strength | Multi-dimensional tables with totals in a few lines | Row-by-row control, computed columns, styling | Statistics and output datasets |
| Computed columns | Limited | Full (COMPUTE blocks) | No |
| Detail rows | No | Yes | No |
| Output dataset | `OUT=` | `OUT=` | `OUTPUT OUT=` |

### SQL Server and Pandas

PROC TABULATE is closest to a pivot table: SQL Server `PIVOT` with `ROLLUP`, or Pandas
`pd.pivot_table(df, index="cust_id", columns="channel", values="amount", aggfunc="sum",
margins=True)`.

### 💼 Banking scenario

A board pack needs a table of loan counts and balances by product (rows) and risk grade (columns),
with totals both ways and a separate page per region. One TABULATE statement with a page dimension
produces it.

### ⚠️ Common mistakes

- Mixing up commas (dimensions) and asterisks (crossing).
- Putting a VAR variable in the CLASS statement, or the other way round.
- Rows silently dropped because a CLASS variable is missing (add the `MISSING` option).

### Exercises

1. **Level 1:** Sum of amount by channel with a total row.
2. **Level 2:** Customer rows by channel columns with totals both ways.
3. **Level 3:** Add a page dimension for branch.
4. **Level 4 — Interview:** "When would you choose TABULATE over REPORT?"
5. **Level 5:** Loan counts and outstanding by product × DPD bucket (using a format), with totals and
   percentages of the column total (`colpctsum`).

### ⭐ Interview questions

**Q. Explain the TABLE statement's syntax.**
- *Strong answer:* "Commas separate page, row and column dimensions; an asterisk crosses items; a space
  concatenates them; ALL adds totals; `='label'` and `f=` set labels and formats."

### Module wrap-up

- **I now know:** CLASS, VAR, TABLE with dimensions, crossing, ALL, labels and formats.
- **I can now:** build multi-dimensional summary tables quickly.
- **Next:** Module 46 — charts.

---

## MODULE 46 — SAS Charts

**Syllabus items:** 6.11 SAS Charts

**You will learn:** the main chart types with PROC SGPLOT and PROC SGPANEL, and how to save charts.
**Why it matters:** a chart often explains a trend faster than a table. **Before you start:** Modules
40 and 41.

### 🧠 Which tool

- **ODS Graphics procedures** (`SGPLOT`, `SGPANEL`, `SGSCATTER`) are part of Base SAS and are the
  modern choice.
- **SAS/GRAPH procedures** (`GCHART`, `GPLOT`) are older and need a separate licence. You will still
  see them in old programs.

### The main chart types

```sas
/* 1. Bar chart: total amount by channel */
proc sgplot data=work.txn;
    vbar channel / response=amount stat=sum datalabel;
    yaxis label='Total amount (Rs)';
    title 'Transaction Value by Channel';
run;

/* 2. Line chart: a monthly trend */
proc sgplot data=work.monthly_fraud;           /* month, fraud_rate */
    series x=month y=fraud_rate / markers;
    yaxis label='Fraud rate (%)';
    title 'Monthly Fraud Rate';
run;

/* 3. Histogram with a smooth curve: the shape of amounts */
proc sgplot data=bank.transactions;
    histogram amount;
    density amount;
run;

/* 4. Box plot: amounts by channel, showing outliers */
proc sgplot data=bank.transactions;
    vbox amount / category=channel;
run;

/* 5. Scatter plot: credit limit vs balance */
proc sgplot data=bank.cards;
    scatter x=credit_limit y=balance;
run;

/* 6. One small chart per region */
proc sgpanel data=work.branch_month;
    panelby region;
    vbar month / response=fraud_cases;
run;
title;
```

| Statement | Chart |
| --- | --- |
| `VBAR` / `HBAR` | Vertical / horizontal bars |
| `SERIES` / `VLINE` | Line over x values / over categories |
| `HISTOGRAM` + `DENSITY` | Distribution |
| `VBOX` / `HBOX` | Box plot (median, quartiles, outliers) |
| `SCATTER` | Two numeric variables |
| `REG` | Scatter with a fitted line |

### Saving charts as image files

```sas
ods listing gpath="C:\sasdata\out\charts";
ods graphics on / imagename="fraud_trend" imagefmt=png width=8in height=4in;

proc sgplot data=work.monthly_fraud;
    series x=month y=fraud_rate / markers;
run;

ods graphics off;
```

Charts also go into ODS PDF, RTF, HTML and EXCEL output automatically when those destinations are
open.

### SQL Server and Pandas

| SAS | SQL Server | Python |
| --- | --- | --- |
| `PROC SGPLOT` | SSRS charts, Power BI | `matplotlib`, `seaborn`, `df.plot()` |
| `PROC SGPANEL` | Small multiples in Power BI | `seaborn.FacetGrid` |

📌 In many banks SAS prepares the data and Power BI or SAS Visual Analytics draws interactive charts.
SGPLOT is used for static charts inside PDF and email reports.

### 💼 Banking scenario

The fraud MI pack includes a 13-month line chart of fraud loss rate per channel, a box plot of
transaction amounts per merchant category, and a panel of bar charts per region. All three are built
with SGPLOT and SGPANEL inside one ODS PDF block.

### ⚠️ Common mistakes

- Charting unsorted dates as text (months in alphabetical order). Use real SAS dates with a format.
- Forgetting `ods graphics on` in older setups, so no graph is produced.
- Charting millions of points in a scatter plot. Sample first (Module 20).

### Exercises

1. **Level 1:** Bar chart of transaction count per channel.
2. **Level 2:** Monthly line chart of total spend.
3. **Level 3:** Box plot of amounts per channel, then explain the outliers.
4. **Level 4 — Interview:** "Which procedure do you use for charts in SAS?"
5. **Level 5:** A PDF with a title page, one summary table and three charts.

### ⭐ Interview questions

**Q. SGPLOT vs GPLOT?**
- *Strong answer:* "SGPLOT is an ODS Graphics procedure in Base SAS: modern, simpler syntax, works with
  all ODS destinations. GPLOT and GCHART are older SAS/GRAPH procedures that need a separate licence. I
  use SGPLOT and SGPANEL for new work."

### Module wrap-up

- **I now know:** SGPLOT chart types, SGPANEL, and saving charts with ODS GRAPHICS.
- **I can now:** add clear charts to SAS reports.
- **Next:** Part VIII — macros and automation.

---

## Reporting Procedures Compared

| Procedure | Purpose | Prints by default | Saves a dataset | Best for |
| --- | --- | --- | --- | --- |
| PROC PRINT | List detail rows | Yes | No | Checks, listings |
| PROC REPORT | Custom formatted reports | Yes | `OUT=` | Management reports with computed columns |
| PROC MEANS | Descriptive statistics | Yes | `OUTPUT OUT=` | Quick statistics |
| PROC SUMMARY | Same as MEANS, quiet | No | `OUTPUT OUT=` | Summary datasets in programs |
| PROC UNIVARIATE | Full distribution | Yes | `OUTPUT OUT=` | Outliers, percentiles, normality |
| PROC FREQ | Counts and crosstabs | Yes | `OUT=` | Categorical analysis, data checks |
| PROC TABULATE | Multi-dimensional tables | Yes | `OUT=` | Pivot-style tables with totals |
| PROC SGPLOT / SGPANEL | Charts | Yes | No | Visuals in PDF, HTML and email reports |

**Part VII checklist:** ✓ 2.10 · ✓ 2.11 · ✓ 6.4 · ✓ 6.5 · ✓ 6.6 · ✓ 6.7 · ✓ 6.8 · ✓ 6.9 · ✓ 6.10 · ✓ 6.11

---

# Part VIII — Macros and Automation (Modules 47–55)

The order of this Part follows the macro learning path in your prompt: macro processing → macro
variables → %LET → parameters (positional, keyword) → %GLOBAL / %LOCAL → PROC SQL INTO → CALL SYMPUT →
macro functions → %IF/%THEN → %DO loops → reusable and stored macros → %INCLUDE → debugging →
automation → scheduling → industry use cases.

## MODULE 47 — Automation, and How a Macro Program Starts and Ends

**Syllabus items:** 8.1 SAS automation program with an example · 8.2 How a SAS macro program starts and
ends

**You will learn:** what the macro language is, how SAS processes it, and how a hard-coded program
becomes a reusable macro. **Why it matters:** 🔥 macros are how SAS work is automated in every bank.
**Before you start:** Parts I–VII.

### 🧠 What the macro language is

The **macro language** writes SAS code for you. It works on **text**. Before SAS compiles a DATA step
or PROC step, the macro processor replaces macro references with text, and then the normal SAS code
runs.

- A **macro variable** holds a piece of text: `%let month = SEP2026;` then `&month` is replaced by
  `SEP2026`.
- A **macro** is a named block of code that can take parameters: `%macro report(month=); ... %mend;`
  and you run it with `%report(month=SEP2026)`.

### 🧠 How SAS processes macro code

```text
Your program
    |
    v
WORD SCANNER  breaks the code into tokens (words, numbers, symbols)
    |
    |  sees % or & followed by a name?
    |------------- yes -------------> MACRO PROCESSOR
    |                                   - looks up macro variables in symbol tables
    |                                   - runs macro statements (%IF, %DO, %LET)
    |                                   - sends the resulting TEXT back to be scanned again
    |<---------------------------------+
    v
COMPILER  compiles the DATA or PROC step that has been built
    |
    v
EXECUTION  the step runs (DATA step loop, procedure)
```

📌 **The key fact:** macro code is fully resolved **before** the DATA step runs. The macro processor
never sees your data values; it only produces text. This explains many classic macro problems (Module
50).

### An automation program by example (8.1)

**Before: a hard-coded monthly report** (someone edits the dates every month)

```sas
proc sql;
    create table work.sep_summary as
    select channel, count(*) as txns, sum(amount) as total_amt
    from bank.transactions
    where txn_date between '01SEP2026'd and '30SEP2026'd
    group by channel;
quit;

proc print data=work.sep_summary noobs;
    title "Channel Summary - SEP2026";
run;
```

**After: a macro that works for any month**

```sas
%macro channel_summary(month_start=);
    %local month_end label;
    %let month_end = %sysfunc(intnx(month, "&month_start"d, 0, e), date9.);
    %let label     = %sysfunc(inputn(&month_start, date9.), monyy7.);

    proc sql;
        create table work.summary_&label as
        select channel, count(*) as txns, sum(amount) as total_amt format=comma14.
        from bank.transactions
        where txn_date between "&month_start"d and "&month_end"d
        group by channel;
    quit;

    proc print data=work.summary_&label noobs;
        title "Channel Summary - &label";
    run;
    title;
%mend channel_summary;

%channel_summary(month_start=01SEP2026)
%channel_summary(month_start=01OCT2026)
```

For `01SEP2026`, the macro sets `month_end` to `30SEP2026` and `label` to `SEP2026`, so it creates
`work.summary_SEP2026`. No code changes are needed for October.

### How a macro program starts and ends (8.2)

```sas
%macro macro_name(parameters);     /* starts the definition */
    ... any SAS code and macro statements ...
%mend macro_name;                  /* ends the definition (repeating the name is optional but good practice) */

%macro_name(values)                /* runs (calls) the macro */
```

| Moment | What happens |
| --- | --- |
| SAS reads `%macro ... %mend` | The macro is **compiled** and stored (by default in the catalog `WORK.SASMACR`). Nothing runs yet. |
| You call `%macro_name(...)` | The macro **executes**: parameters are set, macro logic runs, and the generated SAS code is sent to the compiler |
| End of the SAS session | `WORK.SASMACR` is deleted, so session macros must be defined again (or stored, Module 54) |

📌 A macro call does not need a semicolon after it. A semicolon there is usually harmless, but inside
some statements it can end the statement early, so get used to leaving it out.

### ⚠️ Common mistakes

- Using single quotes around a macro reference: `'&month'` stays as the literal text `&month`. Use
  double quotes: `"&month"`.
- Forgetting that the macro produces text: `%let total = 10 + 5;` stores the text `10 + 5`, not 15.
- Defining the macro after calling it.

### Exercises

1. **Level 1:** Turn a PROC PRINT with a hard-coded title into a macro with a `title=` parameter.
2. **Level 2:** Write a macro that summarises any dataset by any class variable.
3. **Level 3:** Write the channel summary macro and run it for three months.
4. **Level 4 — Interview:** "When does macro code run compared with DATA step code?"
5. **Level 5:** Identify the hard-coded values in an old report program of yours and design its macro
   parameters.

### ⭐ Interview questions

**Q. How does the macro processor work?**
- *What they are testing:* understanding, not syntax.
- *Strong answer:* "The word scanner tokenises the program. When it finds a `%` or `&` trigger, the
  macro processor resolves macro variables and runs macro statements, producing text that goes back
  into the input stack. Only then is the DATA or PROC step compiled and executed. So macro code runs
  before any data is processed and cannot see data values directly."

### Module wrap-up

- **I now know:** what macros are, how macro processing works, and how a macro starts, ends and runs.
- **I can now:** turn a hard-coded program into a parameterised macro.
- **Next:** Module 48 — macro variables.

---

## MODULE 48 — Macro Variables: %LET, Practical Uses, Global, Local, and Seeing Them All

**Syllabus items:** 8.3 Defining SAS macro variables · 8.4 Macro variables and practical uses · 8.5
%LET and practical uses · 8.7 %GLOBAL macro variables · 8.8 %LOCAL macro variables · 8.15 Viewing all
defined macro variables

**You will learn:** how to create, use, scope and inspect macro variables. **Why it matters:** macro
variables remove hard-coded values from programs. **Before you start:** Module 47.

### Defining macro variables with %LET (8.3, 8.5)

```sas
%let asof      = 30SEP2026;
%let threshold = 50000;
%let region    = WEST;
%let lib       = bank;
%let out_path  = /sas/out/fraud;
```

- The value is **text**. No quotes are needed; if you type quotes, they become part of the value.
- Leading and trailing blanks are removed.
- The value ends at the semicolon.
- Names follow normal SAS naming rules (up to 32 characters).

### Using them: & references

```sas
data work.big_txn;
    set &lib..transactions;                          /* two dots: see below */
    where amount > &threshold and txn_date <= "&asof"d;
run;

title "Large transactions up to &asof (threshold &threshold)";
```

📌 **The dot ends a macro reference.** `&lib..transactions` becomes `bank.transactions`: the first dot
ends `&lib`, the second is the normal dot between library and dataset. `&region._2026` becomes
`WEST_2026`; without the dot SAS would look for a macro variable called `region_2026`.

📌 **Quotes:** macro references resolve inside **double** quotes, not inside single quotes.

| Code | Becomes |
| --- | --- |
| `"&asof"d` | `"30SEP2026"d` (a date constant) |
| `'&asof'd` | `'&asof'd` (not resolved, an error) |
| `title "Region &region";` | `title "Region WEST";` |

### Practical uses (8.4)

| Use | Example |
| --- | --- |
| Run dates | `%let asof = 30SEP2026;` used in every WHERE and title |
| Paths | `%let in_path = /sas/raw/2026;` then `infile "&in_path/txn.txt";` |
| Thresholds and business rules | `%let ctr_limit = 1000000;` |
| Library switching (dev/test/prod) | `%let env = prod;` then `libname mart "/sas/&env/mart";` |
| Lists | `%let channels = ATM POS ONLINE;` used in loops (Module 50) |
| Counts and results from data | Created with INTO or CALL SYMPUTX (Module 50) |

### Automatic macro variables

SAS creates these for you:

| Variable | Holds |
| --- | --- |
| `&SYSDATE9` | The date the **SAS session started** (for example `05OCT2026`) |
| `&SYSDAY` | The weekday the session started |
| `&SYSTIME` | The time the session started |
| `&SYSUSERID` | Your user ID |
| `&SYSLAST` | The last dataset created |
| `&SYSERR` | Return code of the last step (0 = OK) |
| `&SYSCC` | Overall condition code of the session or job |
| `&SYSINFO` | Extra return information (for example from PROC COMPARE) |
| `&SYSPARM` | Text passed with the `-sysparm` option when SAS starts (Module 55) |
| `&SQLOBS` | Rows processed by the last PROC SQL statement |
| `&SYSVER` | The SAS version |

⚠️ `&SYSDATE9` is the date the session **started**, not today. A session left open overnight gives
yesterday's date. For today's date use `%sysfunc(today(), date9.)`.

### 🔥 Global and local macro variables (8.7, 8.8)

Macro variables live in **symbol tables**.

```text
GLOBAL symbol table   (exists for the whole session)
   asof=30SEP2026  region=WEST  ...
        ^
        |  looked up if not found locally
LOCAL symbol table of %channel_summary   (exists only while that macro runs)
   month_start=01SEP2026  month_end=30SEP2026  label=SEP2026
```

| Created | Goes into |
| --- | --- |
| `%let` in open code (outside any macro) | Global table |
| Macro parameters | The macro's local table |
| `%let` inside a macro | The nearest table that already has that name; if none has it, the macro's **local** table |
| `%global x;` | Global table, even inside a macro |
| `%local x;` | The current macro's local table, even if a global `x` exists |

```sas
%let region = WEST;                 /* global */

%macro show;
    %local region;                  /* a separate local variable */
    %let region = EAST;
    %put Inside:  &=region;
%mend show;

%show
%put Outside: &=region;
```

**Log**

```text
Inside:  REGION=EAST
Outside: REGION=WEST
```

**Without `%LOCAL`, a macro can change your global value by accident:**

```sas
%macro change;
    %let region = NORTH;            /* REGION already exists globally, so the global value changes */
%mend change;

%change
%put &=region;                      /* REGION=NORTH */
```

📌 **Best practice:** declare every variable a macro uses internally with `%LOCAL`. Use `%GLOBAL` only
for values that must survive after the macro ends (for example a status flag read by a later step).

### Viewing macro variables (8.15)

```sas
%put &=asof;            /* ASOF=30SEP2026 */
%put _user_;            /* every macro variable you created (global and local) */
%put _global_;          /* global ones only */
%put _local_;           /* local ones (inside a macro) */
%put _automatic_;       /* SAS's automatic ones */
%put _all_;             /* everything */

proc sql;               /* as a table */
    select scope, name, value
    from dictionary.macros
    where scope = 'GLOBAL';
quit;
```

`SASHELP.VMACRO` is the same information as a view you can use in a DATA step.

**Removing a macro variable:** `%symdel region;`

### SQL Server and Python

| SAS | SQL Server | Python |
| --- | --- | --- |
| `%let x = 10;` | `DECLARE @x INT = 10;` | `x = 10` |
| `&x` in code | `@x` in a query | `f"... {x} ..."` in a string |
| Global/local scope | Batch / procedure scope | Module / function scope |
| Text substitution before running | Dynamic SQL with `sp_executesql` | f-strings building SQL |

⚠️ A T-SQL variable holds a typed **value**. A SAS macro variable holds **text** that is pasted into
the code before it runs. That is why `"&asof"d` is needed to turn the text into a date constant.

### 💼 Banking scenario

At the top of every production program, one block sets the environment:

```sas
%let env      = prod;
%let asof     = 30SEP2026;
%let raw_path = /sas/&env/raw;
%let rpt_path = /sas/&env/reports;
libname raw "&raw_path" access=readonly;
libname rpt "&rpt_path";
```

Moving from test to production means changing one word, `env`, and nothing else.

### ⚠️ Common mistakes

- Single quotes around a reference.
- Missing the extra dot: `&lib.transactions` becomes `banktransactions`.
- `WARNING: Apparent symbolic reference X not resolved.` because of a typo or a variable that only
  existed inside a macro (local scope).
- Relying on `&SYSDATE9` for today's date.
- Macros overwriting global variables because `%LOCAL` was not used.

### Exercises

1. **Level 1:** Create macro variables for an as-of date and a threshold and use them in a WHERE.
2. **Level 2:** Build a dataset name from two macro variables (`&region._&year`).
3. **Level 3:** Show a macro changing a global variable by accident, then fix it with `%LOCAL`.
4. **Level 4 — Interview:** "What is the difference between %GLOBAL and %LOCAL?"
5. **Level 5:** Write an environment block that switches between dev, test and prod libraries using
   one macro variable.

### ⭐ Interview questions

**Q1. Global vs local macro variables?**
- *Strong answer:* "Global variables live in the global symbol table for the whole session; `%let` in
  open code creates them. Local variables live in a macro's local table and disappear when it ends;
  parameters are local. A `%let` inside a macro updates the nearest existing variable with that name,
  so I always declare internal variables with %LOCAL to avoid overwriting globals."

**Q2. Why does `'&x'` not resolve?**
- *Strong answer:* "The macro processor does not look inside single quotes. Use double quotes."

### Module wrap-up

- **I now know:** %LET, references, the dot rule, quoting, automatic variables, global and local symbol
  tables, and how to list macro variables.
- **I can now:** remove hard-coded values from programs and control macro variable scope.
- **Next:** Module 49 — macro parameters.

---

## MODULE 49 — Macro Parameters: Positional and Keyword

**Syllabus items:** 8.6 Positional and keyword parameters

**You will learn:** the two kinds of parameters, default values, and how to validate inputs. **Why it
matters:** good parameters make a macro safe and reusable. **Before you start:** Module 48.

### Positional parameters

Values are matched by **position**, so the order matters.

```sas
%macro print_top(ds, n);
    proc print data=&ds(obs=&n) noobs;
    run;
%mend print_top;

%print_top(work.txn, 3)
```

### Keyword parameters

Values are matched by **name**, so the order does not matter, and each can have a **default**.

```sas
%macro print_top(ds=work.txn, n=5, title=Top rows);
    title "&title";
    proc print data=&ds(obs=&n) noobs;
    run;
    title;
%mend print_top;

%print_top()                             /* all defaults: work.txn, 5 rows */
%print_top(n=3)                          /* only change n */
%print_top(title=Customers, ds=work.customers)
```

### Mixing both

Positional parameters must come **first**.

```sas
%macro summarise(ds, classvar, stat=sum, out=work.summary);
    proc means data=&ds noprint nway;
        class &classvar;
        var amount;
        output out=&out(drop=_type_ _freq_) &stat=;
    run;
%mend summarise;

%summarise(work.txn, channel)
%summarise(work.txn, cust_id, stat=mean, out=work.cust_mean)
```

`&stat=` with nothing after the `=` keeps the variable's own name (`amount`) in the output.

| | Positional | Keyword |
| --- | --- | --- |
| Matched by | Order | Name |
| Defaults | No | Yes |
| Easy to read in a call | Less (what is `3`?) | More (`n=3`) |
| Best for | One or two obvious inputs | Everything else, especially optional settings |

📌 Parameters are **local** macro variables of the macro.

### Validating parameters

```sas
%macro load_day(run_date=, lib=stage);
    %if %length(&run_date) = 0 %then %do;
        %put ERROR: run_date is required, for example run_date=30SEP2026.;
        %return;
    %end;
    %if not %sysfunc(exist(&lib..txn_daily)) %then %do;
        %put ERROR: &lib..txn_daily does not exist.;
        %return;
    %end;
    %put NOTE: Loading &run_date into &lib..;
    /* ... the real work ... */
%mend load_day;
```

`%RETURN` leaves the macro early. A message that begins with `ERROR:` or `WARNING:` is coloured in the
Log like a real SAS message, which makes it easy to spot.

### Commas and special characters in values

A comma in a value would be read as the start of the next parameter. Hide it with `%STR`:

```sas
%macro filter_print(where=);
    proc print data=work.txn noobs;
        where &where;
    run;
%mend filter_print;

%filter_print(where=%str(channel in ('ATM', 'POS')))
```

(Module 52 covers quoting in depth.)

### Python comparison

```python
def print_top(ds="txn", n=5, title="Top rows"):     # keyword arguments with defaults
    ...
print_top(n=3)
```

SAS keyword parameters behave like Python keyword arguments with defaults.

### ⚠️ Common mistakes

- Positional parameters in the wrong order.
- Positional parameters listed after keyword ones in the definition (`ERROR`).
- Unquoted commas in a parameter value: `ERROR: More positional parameters found than defined.`
- No validation, so a blank parameter produces confusing errors deep inside the macro.

### Exercises

1. **Level 1:** Write a macro with keyword parameters `ds=` and `n=` that prints the first rows.
2. **Level 2:** Add a `where=` parameter and call it with a condition containing a comma.
3. **Level 3:** Validate that a required parameter is given and that the dataset exists.
4. **Level 4 — Interview:** "Positional vs keyword parameters?"
5. **Level 5:** Design the parameters for a "monthly portfolio report" macro used by 10 teams, with
   sensible defaults.

### ⭐ Interview questions

**Q. Positional vs keyword parameters?**
- *Strong answer:* "Positional values are matched by order and have no defaults; keyword values are
  matched by name, can have defaults and can be given in any order. Positional ones must come first
  when mixing. I prefer keyword parameters for readability and safe defaults."

### Module wrap-up

- **I now know:** positional and keyword parameters, defaults, mixing them, validation with %RETURN,
  and quoting commas.
- **I can now:** design safe, readable macro interfaces.
- **Next:** Module 50 — macro variables from data.

---

## MODULE 50 — Macro Variables from Data: PROC SQL INTO, CALL SYMPUT and %DO Loops

**Syllabus items:** 8.9 PROC SQL INTO clause for creating macro variables · 8.10 %DO loop for creating
macro variables · 8.11 CALL SYMPUT

**You will learn:** how to move values **from data into macro variables**, and how to loop over them.
**Why it matters:** this is how programs adapt to the data: one report per branch, a total in a title,
a list of new products. **Before you start:** Modules 29 and 48.

### PROC SQL INTO (8.9)

```sas
proc sql noprint;
    select count(*)                into :n_txn       trimmed from work.txn;
    select sum(amount) format=comma14. into :total_amt trimmed from work.txn;
    select distinct channel        into :channels    separated by ' ' from work.txn;
    select distinct quote(trim(channel)) into :channel_list separated by ', ' from work.txn;
quit;

%put &=n_txn &=total_amt;
%put &=channels;
%put &=channel_list;
```

**Log**

```text
N_TXN=6 TOTAL_AMT=230,300
CHANNELS=ATM ONLINE POS
CHANNEL_LIST="ATM", "ONLINE", "POS"
```

| Form | Creates |
| --- | --- |
| `into :x` | One macro variable from the first row |
| `into :x trimmed` | Same, without leading or trailing blanks |
| `into :x separated by ' '` | One macro variable holding **all** rows, joined |
| `into :ch1-:ch3` | `ch1`, `ch2`, `ch3` from rows 1 to 3 |
| `into :ch1-` | As many as there are rows (`ch1`, `ch2`, ...) |

After the query, `&SQLOBS` holds the number of rows.

`&channel_list` is ready to use in a WHERE: `where channel in (&channel_list)`.

### CALL SYMPUT and CALL SYMPUTX (8.11)

These create macro variables from **inside a DATA step**.

```sas
data _null_;
    set work.cust_summary end=last;          /* C102, C101, C103 (Module 29) */
    call symputx(cats('cust', _n_), cust_id);
    if last then call symputx('n_cust', _n_);
run;

%put &=n_cust &=cust1 &=cust2 &=cust3;      /* N_CUST=3 CUST1=C102 CUST2=C101 CUST3=C103 */
```

| | `CALL SYMPUT` | `CALL SYMPUTX` |
| --- | --- | --- |
| Removes leading and trailing blanks | No | Yes |
| Numbers | Converts with a NOTE in the Log, may add blanks | Converts cleanly |
| Choose global or local | No | Yes: third argument `'G'` or `'L'` |
| Use today | Rarely | ✓ Preferred |

### 🔥 The timing trap (a top interview question)

```sas
data _null_;
    call symputx('flag', 'YES');
    x = "&flag";                 /* resolved at COMPILE time - before CALL SYMPUTX has run */
run;
/* WARNING: Apparent symbolic reference FLAG not resolved. */

%put &=flag;                     /* FLAG=YES : available after the step has finished */
```

**Why:** `&flag` is replaced with text while the step is being **compiled**. CALL SYMPUTX only runs
during **execution**, which comes later. A macro variable created by CALL SYMPUT(X) can be used with
`&` only in a **later** step.

**If you need the value in the same step**, read it at execution time with `SYMGET`:

```sas
data _null_;
    call symputx('flag', 'YES');
    x = symget('flag');          /* x = 'YES' */
    put x=;
run;
```

### INTO vs CALL SYMPUTX

| | PROC SQL INTO | CALL SYMPUTX |
| --- | --- | --- |
| Best for | Counts, totals, lists of distinct values | Values that need DATA step logic (RETAIN, FIRST., conditions) |
| Many values in one variable | `SEPARATED BY` | Build the text yourself |
| One variable per row | `:v1-` | `cats('v', _n_)` |
| Scope control | Created in the current scope | `'G'` / `'L'` argument |

### %DO loops with macro variables (8.10)

**Loop over values read from the data**, creating one dataset per channel:

```sas
%macro split_by_channel;
    %local i n;
    proc sql noprint;
        select distinct channel into :ch1- from work.txn;
    quit;
    %let n = &sqlobs;

    %do i = 1 %to &n;
        data work.txn_&&ch&i;
            set work.txn;
            where channel = "&&ch&i";
        run;
    %end;
%mend split_by_channel;

%split_by_channel
```

This creates `work.txn_ATM`, `work.txn_ONLINE` and `work.txn_POS`.

🧠 **How `&&ch&i` resolves** (when `i` is 2):

```text
pass 1:  &&  ->  &        ch  stays      &i  ->  2        result:  &ch2
pass 2:  &ch2  ->  ONLINE
```

**Create macro variables in a %DO loop:**

```sas
%macro make_months(start=01JAN2026, n=3);
    %local i;
    %do i = 1 %to &n;
        %global m&i;
        %let m&i = %sysfunc(intnx(month, "&start"d, %eval(&i - 1), b), monyy7.);
    %end;
%mend make_months;

%make_months()
%put &=m1 &=m2 &=m3;          /* M1=JAN2026 M2=FEB2026 M3=MAR2026 */
```

**Loop over a list stored in one variable** with `%SCAN`:

```sas
%macro loop_list(list=ATM POS ONLINE);
    %local i item;
    %do i = 1 %to %sysfunc(countw(&list));
        %let item = %scan(&list, &i);
        %put Processing channel &item;
    %end;
%mend loop_list;
```

### SQL Server and Python

| SAS | SQL Server | Python |
| --- | --- | --- |
| `select count(*) into :n` | `SELECT @n = COUNT(*) FROM ...` | `n = len(df)` |
| `separated by ', '` | `STRING_AGG(channel, ', ')` | `", ".join(df["channel"].unique())` |
| `%do i = 1 %to &n` with `&&ch&i` | Cursor or `WHILE` loop with dynamic SQL | `for ch in channels:` |

### 💼 Banking scenario

At month end, a program reads the list of active branches from the branch master into `:br1-`, then
loops to produce one PDF report per branch. When a new branch opens, it appears in the master and gets
its report automatically. No code change is needed.

### ⚠️ Common mistakes

- Using a CALL SYMPUT variable with `&` in the same step.
- Forgetting `TRIMMED` and getting leading blanks (for example in a file name).
- Using `&ch&i` instead of `&&ch&i`.
- Reading `&SQLOBS` after another SQL statement has run (it then refers to that statement).

### Exercises

1. **Level 1:** Put the number of customers into a macro variable and print it in a title.
2. **Level 2:** Put the list of distinct channels into one macro variable, quoted and comma-separated,
   and use it in a WHERE ... IN.
3. **Level 3:** Create one dataset per customer with a %DO loop.
4. **Level 4 — Interview:** "Why can't I use a macro variable created by CALL SYMPUT in the same DATA
   step?"
5. **Level 5:** For each region in a table, create a summary and an Excel sheet, all in one macro.

### ⭐ Interview questions

**Q1. CALL SYMPUT timing?**
- *What they are testing:* the compile-vs-execute difference.
- *Strong answer:* "`&var` references are resolved by the macro processor when the step is compiled.
  CALL SYMPUT runs during execution, so the variable does not exist yet at compile time. It is
  available from the next step onwards. Within the same step I would use SYMGET."
- *Weak answer:* "You need a RUN statement."
- *Follow-up:* "What is the difference between SYMPUT and SYMPUTX?"

**Q2. How do you create a macro variable list from a table?**
- *Strong answer:* "PROC SQL `SELECT DISTINCT col INTO :list SEPARATED BY ' '` for one variable, or
  `INTO :v1-` for one per row with `&SQLOBS` as the count, then a %DO loop with `&&v&i`."

### Module wrap-up

- **I now know:** INTO (single, list, numbered), TRIMMED, SQLOBS, CALL SYMPUT and SYMPUTX, SYMGET, the
  timing rule, `&&` indirect references and %DO loops.
- **I can now:** build data-driven programs that adapt to new values automatically.
- **Next:** Module 51 — conditional macros.

---

## MODULE 51 — Conditional Macros: %IF %THEN

**Syllabus items:** 8.16 Conditional macro execution using %IF %THEN

**You will learn:** how to make a macro generate different code depending on conditions. **Why it
matters:** production jobs must skip, branch and stop safely. **Before you start:** Modules 48–50.

### 🔥 %IF vs IF

| | `%IF` (macro) | `IF` (DATA step) |
| --- | --- | --- |
| Runs | **Before** the step, while code is being generated | **During** the step, for each row |
| Decides | **Which code** is created | **What happens** to each row |
| Can see data values | No (only macro variables) | Yes |
| Where | Inside a macro (or in open code in SAS 9.4M5+, with %DO blocks) | Inside a DATA step |

### Syntax

```sas
%if condition %then %do;
    ... code or macro statements ...
%end;
%else %do;
    ... other code ...
%end;
```

### Example: skip when there is no data, branch at month end

```sas
%macro daily_job(asof=);
    %local n_rows asof_num month_end;

    proc sql noprint;
        select count(*) into :n_rows trimmed
        from bank.transactions
        where txn_date = "&asof"d;
    quit;

    %if &n_rows = 0 %then %do;
        %put WARNING: No transactions for &asof.. Job skipped.;
        %return;
    %end;

    %let asof_num  = %sysfunc(inputn(&asof, date9.));
    %let month_end = %sysfunc(intnx(month, &asof_num, 0, e));

    %if &asof_num = &month_end %then %do;
        %put NOTE: &asof is a month end - running the monthly pack too.;
        /* monthly code here */
    %end;
    %else %do;
        %put NOTE: &asof is not a month end - daily summary only.;
    %end;

    /* daily code here */
%mend daily_job;

%daily_job(asof=30SEP2026)
```

**Why the date is converted first:** in `%IF`, `"30SEP2026"d` is only **text**; the macro processor does
not understand SAS date constants. `%sysfunc(inputn(&asof, date9.))` turns it into the number 24379, and
`%sysfunc(intnx(...))` returns a number too, so the comparison is between two numbers.

### How %IF compares values

`%IF` conditions are evaluated with `%EVAL`:

- If both sides are **whole numbers**, they are compared as numbers: `%if 10 > 9` is true.
- Otherwise they are compared as **text**, and text comparison is case-sensitive.
- ⚠️ **Decimals are compared as text**: `%if 10.5 > 9.2` compares `"10.5"` with `"9.2"`; `1` comes
  before `9`, so it is **false**. Use `%sysevalf`: `%if %sysevalf(10.5 > 9.2) %then ...`.

### Stopping a job on errors

```sas
%macro check_step(step=);
    %if &syserr > 4 %then %do;
        %put ERROR: Step &step failed (SYSERR=&syserr). Stopping the job.;
        %abort cancel;
    %end;
%mend check_step;

data stage.txn_clean;
    set raw.txn_daily;
run;
%check_step(step=load txn_daily)
```

`&SYSERR` is the return code of the last step: 0 means success, 4 means warnings, larger values mean
errors.

### ⚠️ Common mistakes

- Using `%IF` to test a data value (it cannot see data; use DATA step IF, or first move the value into a
  macro variable with INTO).
- Comparing decimals or dates as text.
- Comparing text in the wrong case (`%if &env = PROD` vs `prod`): use `%upcase(&env) = PROD`.
- Forgetting `%END`.

### Exercises

1. **Level 1:** A macro that prints a dataset only if it has rows.
2. **Level 2:** A macro that runs a different PROC depending on a `type=` parameter.
3. **Level 3:** Branch on whether a date is a quarter end.
4. **Level 4 — Interview:** "What is the difference between %IF and IF?"
5. **Level 5:** A job that stops with a clear message if any input file is missing or empty, and
   otherwise runs all steps, checking `&SYSERR` after each.

### ⭐ Interview questions

**Q. %IF vs IF?**
- *Strong answer:* "%IF is a macro statement: it runs while code is being generated and decides which
  SAS code is created; it only sees macro variables. IF runs during DATA step execution and decides
  what happens to each observation. %IF compares integers numerically but decimals as text, so I use
  %SYSEVALF for decimals."

### Module wrap-up

- **I now know:** %IF/%THEN/%ELSE with %DO blocks, how %IF compares values, %RETURN, %ABORT and
  &SYSERR checks.
- **I can now:** write macros that branch, skip and stop safely.
- **Next:** Module 52 — macro functions and quoting.

---

## MODULE 52 — Macro Functions and Quoting

**Syllabus items:** 8.18 SAS macro functions

**You will learn:** the macro functions for text, arithmetic and calling DATA step functions, and how
macro quoting protects special characters. **Why it matters:** quoting problems are the hardest macro
bugs, and interviewers know it. **Before you start:** Modules 48–51.

### Text functions

```sas
%let name = asha rao;
%put %upcase(&name);              /* ASHA RAO */
%put %substr(&name, 1, 4);        /* asha */
%put %scan(&name, 2);             /* rao */
%put %length(&name);              /* 8 */
%put %index(&name, rao);          /* 6 */
```

Also useful (these are **autocall macros** supplied with SAS, so they work like functions):
`%lowcase`, `%trim`, `%left`, `%cmpres` (squash repeated blanks).

### Arithmetic: %EVAL and %SYSEVALF

```sas
%put %eval(10 + 5);               /* 15 */
%put %eval(10 / 3);               /* 3  - whole numbers only, the decimals are dropped */
%put %sysevalf(10 / 3);           /* 3.33333333333333 */
%put %sysevalf(10.5 > 9.2);       /* 1 (true) */
%put %eval(1.5 + 1);              /* ERROR: a character operand was found ... */
```

📌 `%let total = 10 + 5;` stores the **text** `10 + 5`. You need `%eval(&total)` to get 15.

### %SYSFUNC: any DATA step function in macro code

```sas
%put %sysfunc(today(), date9.);                                    /* today, for example 05OCT2026 */
%put %sysfunc(intnx(month, %sysfunc(today()), -1, e), date9.);     /* last month's end: 30SEP2026 */
%put %sysfunc(exist(work.txn));                                    /* 1 if the dataset exists */
%put %sysfunc(fileexist(/sas/raw/txn_daily.txt));                  /* 1 if the file exists */
%put %sysfunc(countw(ATM POS ONLINE));                             /* 3 */
```

📌 Inside `%SYSFUNC`, text arguments are written **without** quotes (`month`, not `'month'`).

**Count the rows of a dataset without reading it:**

```sas
%let dsid = %sysfunc(open(work.txn));
%let nobs = %sysfunc(attrn(&dsid, nlobs));
%let rc   = %sysfunc(close(&dsid));
%put &=nobs;                                  /* NOBS=6 */
```

### 🔥 Macro quoting

Some characters have special meaning in macro code: `;` (ends a statement), `,` (separates
parameters), `&` and `%` (macro triggers), quotes and brackets. **Quoting** functions tell the macro
processor to treat them as plain text.

| Function | Hides | When it acts | Typical use |
| --- | --- | --- | --- |
| `%STR(...)` | `; , + - * / < > = ( )` and blanks, but **not** `&` and `%` | When the code is compiled | Semicolons or commas you type yourself |
| `%NRSTR(...)` | Everything `%STR` hides, **plus** `&` and `%` | When the code is compiled | Text containing `&` or `%` that must not resolve |
| `%BQUOTE(...)` | Special characters, including unmatched quotes | After resolution, while the macro runs | Values that come from data |
| `%SUPERQ(name)` | Everything; the value is **never** resolved | While the macro runs | The safest way to use a value from data |
| `%UNQUOTE(...)` | Removes quoting | | When the quoted text must be used as code again |

```sas
/* %STR: a semicolon inside a value */
%let code = %str(proc print data=work.txn; run;);

/* %STR: commas inside a parameter value */
%filter_print(where=%str(channel in ('ATM', 'POS')))

/* %NRSTR: stop &T being treated as a macro variable */
%let company = %nrstr(AT&T);
%put &company;                                /* AT&T, with no warning */

/* %SUPERQ: a value from data with an apostrophe and an ampersand */
data _null_;
    call symputx('cust_name', "O'Brien & Sons");
run;
%put %superq(cust_name);                      /* O'Brien & Sons - no quote or & problems */
```

⚠️ Without `%SUPERQ`, `%put &cust_name;` would see an **unmatched single quote** and could make the rest
of the program behave as if it were inside quotes. This is one of the most confusing macro bugs.

**Q-functions** (`%QSCAN`, `%QSUBSTR`, `%QSYSFUNC`, `%QUPCASE`) work like their normal versions but
return quoted results, so special characters in the result stay safe.

### SQL Server and Python

| SAS | SQL Server | Python |
| --- | --- | --- |
| `%upcase`, `%substr`, `%scan` | `UPPER`, `SUBSTRING` in dynamic SQL | `str.upper()`, slicing, `split()` |
| `%eval`, `%sysevalf` | Arithmetic on variables | Arithmetic |
| `%sysfunc(today())` | `GETDATE()` | `date.today()` |
| Macro quoting | Escaping quotes in dynamic SQL (`''`), `QUOTENAME()` | Escaping in strings, parameterised queries |

### ⚠️ Common mistakes

- Expecting `%eval` to handle decimals.
- Quotes inside `%SYSFUNC` arguments.
- Using `&value` directly when it may contain quotes, `&` or `%`. Use `%SUPERQ`.
- Using `%STR` when the value contains `&` that must not resolve (use `%NRSTR`).

### Exercises

1. **Level 1:** Get the first word of a macro variable and upper-case it.
2. **Level 2:** Calculate last month's start and end dates with `%SYSFUNC` and `INTNX`.
3. **Level 3:** Count the rows of a dataset with OPEN, ATTRN and CLOSE and skip a step if it is 0.
4. **Level 4 — Interview:** "What is the difference between %STR and %NRSTR? When do you use
   %SUPERQ?"
5. **Level 5:** Write a macro that safely prints customer names taken from data, including names with
   apostrophes and ampersands.

### ⭐ Interview questions

**Q. Explain macro quoting.**
- *Strong answer:* "Quoting stops the macro processor treating special characters as syntax.
  %STR and %NRSTR quote text I type, at compile time; %NRSTR also hides & and %. %BQUOTE and %SUPERQ
  quote values at execution time, for data that may contain unmatched quotes; %SUPERQ is the safest
  because it never resolves the value. %UNQUOTE removes quoting."

### Module wrap-up

- **I now know:** macro text functions, %EVAL, %SYSEVALF, %SYSFUNC, and the quoting functions.
- **I can now:** do calculations in macro code and handle special characters safely.
- **Next:** Module 53 — debugging macros.

---

## MODULE 53 — Debugging Macros

**Syllabus items:** 8.12 SAS macro debugging options

**You will learn:** the options that show what a macro is doing and the usual macro error messages.
**Why it matters:** macro problems are invisible unless you know how to look. **Before you start:**
Modules 47–52.

### The debugging options

```sas
options mprint mlogic symbolgen;
%top_customers(month_start=01SEP2026, n=20)          /* the macro from Module 32 */
options nomprint nomlogic nosymbolgen;
```

| Option | Shows in the Log | Use it to |
| --- | --- | --- |
| `MPRINT` | The SAS code the macro generated | See exactly what ran |
| `MLOGIC` | Macro execution: start and end, parameter values, %IF results, %DO loop steps | Follow the logic |
| `SYMBOLGEN` | Each macro variable reference and what it resolved to | Find wrong values |
| `MPRINTNEST` / `MLOGICNEST` | The same for macros called inside macros | Nested macros |
| `MFILE` | Writes the generated code to a file | Run or review the generated code alone |

**What the Log looks like (shortened)**

```text
MLOGIC(TOP_CUSTOMERS):  Beginning execution.
MLOGIC(TOP_CUSTOMERS):  Parameter MONTH_START has value 01SEP2026
MLOGIC(TOP_CUSTOMERS):  Parameter N has value 20
SYMBOLGEN:  Macro variable N resolves to 20
MPRINT(TOP_CUSTOMERS):   proc sql outobs=20;
SYMBOLGEN:  Macro variable MONTH_START resolves to 01SEP2026
MPRINT(TOP_CUSTOMERS):   create table work.top_customers as select cust_id, sum(amount) as
total_amt format=comma14. from bank.transactions where txn_date between "01SEP2026"d and
intnx('month', "01SEP2026"d, 0, 'e') group by cust_id order by total_amt desc;
MPRINT(TOP_CUSTOMERS):   quit;
MLOGIC(TOP_CUSTOMERS):  Ending execution.
```

**Save the generated code to a file**

```sas
filename mprint "C:\sasdata\debug\generated_code.sas";    /* the fileref must be called MPRINT */
options mprint mfile;
%top_customers(month_start=01SEP2026, n=20)
options nomfile;
```

**Your own messages**

```sas
%put NOTE: Starting load for &asof (environment: &env).;
%put &=n_rows;
%put _local_;          /* inside a macro: every local variable and its value */
```

### Common macro messages and fixes

| Log message | Usual cause | Fix |
| --- | --- | --- |
| `WARNING: Apparent symbolic reference X not resolved.` | Typo; variable not created yet; created locally inside another macro; inside single quotes | Check spelling, scope (%GLOBAL), timing (CALL SYMPUT), quotes |
| `WARNING: Apparent invocation of macro X not resolved.` | Macro not defined in this session, or not found in the autocall library | Run the definition, check SASAUTOS (Module 54) |
| `ERROR: More positional parameters found than defined.` | A comma inside a value | Quote it with `%STR` |
| `ERROR: A character operand was found in the %EVAL function or %IF condition where a numeric operand is required.` | Decimals or text in `%EVAL` / `%IF` | Use `%SYSEVALF`, or compare as text deliberately |
| `ERROR: There were n unclosed %DO statements.` | Missing `%END` | Add the `%END` |
| Nothing runs and later code is ignored | Unmatched quote or bracket in macro code | Look for an odd number of quotes; use `%SUPERQ` for data values |

### A debugging routine

1. Turn on `MPRINT` and read the **generated code**. Most bugs are visible there.
2. If the code is wrong, turn on `SYMBOLGEN` to see which variable has the wrong value.
3. If the wrong branch ran, turn on `MLOGIC` to see how each `%IF` was evaluated.
4. Copy the generated code (or use `MFILE`), run it outside the macro, and fix it there first.
5. Turn the options **off** in production. They make logs very large.

### ⚠️ Common mistakes

- Debugging the macro source instead of the generated code.
- Leaving `SYMBOLGEN` and `MLOGIC` on in production (huge logs, sometimes showing passwords).
- A stale macro definition: you edited the code but did not re-run the `%MACRO ... %MEND` block.

### Exercises

1. **Level 1:** Run a macro with `MPRINT` and copy its generated code.
2. **Level 2:** Create a "symbolic reference not resolved" warning on purpose and fix it.
3. **Level 3:** Use `MLOGIC` to explain why a `%IF` took the wrong branch.
4. **Level 4 — Interview:** "How do you debug a macro?"
5. **Level 5:** Write the generated code of a nested macro to a file with `MFILE` and run it on its
   own.

### ⭐ Interview questions

**Q. How do you debug a macro?**
- *Strong answer:* "MPRINT to see the generated SAS code, SYMBOLGEN to see how each macro variable
  resolved, MLOGIC to follow %IF and %DO decisions, and MFILE to save the generated code and run it
  separately. I add %PUT messages with &= for key values, and I turn the options off in production."

### Module wrap-up

- **I now know:** MPRINT, MLOGIC, SYMBOLGEN, MFILE, %PUT techniques and the common macro errors.
- **I can now:** find and fix macro bugs quickly.
- **Next:** Module 54 — storing and reusing macros.

---

## MODULE 54 — Storing Macros and %INCLUDE

**Syllabus items:** 8.13 Storing SAS macros in a permanent library · 8.14 %INCLUDE

**You will learn:** three ways to keep macros for reuse, and how %INCLUDE brings code from files into
a program. **Why it matters:** teams share macros so everyone uses the same tested logic. **Before you
start:** Module 47.

### Where macros live by default

When you run a `%MACRO ... %MEND` block, SAS compiles the macro into the catalog `WORK.SASMACR`. It is
deleted when the session ends.

### Three ways to keep macros (8.13)

**1. An autocall library** (the most common in teams)

Save each macro in its **own file**, named after the macro, in a shared folder:

```text
/sas/macros/
    top_customers.sas     <- contains %macro top_customers(...); ... %mend;
    check_step.sas
    daily_job.sas
```

Then, in every program (usually in `autoexec.sas`):

```sas
options mautosource sasautos=('/sas/macros' sasautos);
```

The first time you call `%top_customers(...)`, SAS finds `top_customers.sas`, compiles it and runs it.
On Linux the file name should be **lower case**. Keeping `sasautos` in the list keeps SAS's own
autocall macros (`%lowcase`, `%trim`, ...) available.

**2. Stored compiled macros**

```sas
libname mlib "/sas/compiled_macros";
options mstored sasmstore=mlib;

%macro top_customers(month_start=, n=10) / store source des='Top customers for a month';
    /* ... */
%mend top_customers;
```

The compiled macro is saved in `MLIB.SASMACR`. Later sessions only need the `LIBNAME` and the
`OPTIONS` line. `SOURCE` also stores the code, which you can get back with
`%copy top_customers / source library=mlib;`.

**3. %INCLUDE a file of macro definitions**

```sas
%include "/sas/macros/all_macros.sas";
```

The definitions are compiled again every time the file is included.

| | Autocall | Stored compiled | %INCLUDE |
| --- | --- | --- | --- |
| Storage | `.sas` source files | Compiled catalog | `.sas` source file(s) |
| Compiled | On first call in a session | Once, when stored | Every time included |
| Easy to read and version-control | ✓ | ✗ (compiled) | ✓ |
| Typical use | Shared team macro library | Protecting code, very large libraries | Small projects, setup code |

### %INCLUDE (8.14)

`%INCLUDE` reads a file of SAS code and runs it as if it were typed into your program.

```sas
%include "/sas/config/setup.sas";                     /* librefs, options, formats */
%include "/sas/jobs/01_load.sas" "/sas/jobs/02_clean.sas" / source2;

filename jobs "/sas/jobs";
%include jobs(03_report);                             /* member 03_report.sas in that folder */
```

`/SOURCE2` shows the included lines in the Log, which helps debugging.

**Typical uses**

- A shared **setup** file with LIBNAME statements, `OPTIONS` and `FMTSEARCH`.
- A **driver** program that runs a pipeline of step files in order.
- Bringing in macro definitions.

### 💼 Banking scenario

The risk team's Git repository holds `/macros` (one file per macro) and `/config/setup.sas`. Every job
starts with `%include "/sas/config/setup.sas";`, which assigns libraries for the current environment
and sets `sasautos` to the team's macro folder. A fix to a shared macro reaches every job on its next
run, after review and testing.

### ⚠️ Common mistakes

- Autocall file name not matching the macro name (or wrong case on Linux), so SAS cannot find it:
  `WARNING: Apparent invocation of macro X not resolved.`
- Replacing `sasautos` instead of adding to it, so SAS's own autocall macros disappear.
- Changing an autocall file during a session and seeing no change (the macro was already compiled).
  Re-run the definition or start a new session.
- Stored compiled macros without `SOURCE`: the source code is lost.

### Exercises

1. **Level 1:** `%INCLUDE` a setup file that assigns two librefs.
2. **Level 2:** Put a macro in its own file in a folder and call it through an autocall library.
3. **Level 3:** Store a compiled macro with `SOURCE` and retrieve the code with `%COPY`.
4. **Level 4 — Interview:** "How do you share macros across a team?"
5. **Level 5:** Design a folder layout and setup file for a team macro library under version control.

### ⭐ Interview questions

**Q. How do you make macros available in every program?**
- *Strong answer:* "An autocall library: one file per macro named after it, with `OPTIONS MAUTOSOURCE
  SASAUTOS=('path' sasautos)` in the autoexec. Alternatives are stored compiled macros with MSTORED and
  SASMSTORE, or %INCLUDE of a definitions file. Autocall is easiest to maintain under version control."

### Module wrap-up

- **I now know:** WORK.SASMACR, autocall libraries, stored compiled macros, and %INCLUDE.
- **I can now:** build and use a shared team macro library.
- **Next:** Module 55 — scheduling and industry examples.

---

## MODULE 55 — Scheduling and Industry Examples

**Syllabus items:** 8.17 SAS macro scheduling · 8.19 SAS macro industry examples

**You will learn:** how SAS jobs run unattended, how they receive parameters and report failure, and
complete industry-style macros. **Why it matters:** in production, nobody presses F3. **Before you
start:** Modules 47–54.

### 🧠 How scheduling really works (8.17)

SAS does not schedule itself. A **scheduler** starts SAS in **batch mode** at a set time, SAS runs the
program from top to bottom, writes a log, and returns an **exit code**.

```text
Scheduler (cron / Windows Task Scheduler / Control-M / LSF)
    |  06:30 every weekday
    v
sas -sysin daily_fraud.sas -log daily_fraud_30SEP2026.log -sysparm 30SEP2026
    |
    v
SAS runs the program  ->  writes the log  ->  exits with a code: 0 OK, 1 warnings, 2 errors
    |
    v
Scheduler reads the exit code  ->  success: run the next job;  failure: alert the support team
```

**Running SAS in batch on Windows**

```text
"C:\Program Files\SASHome\SASFoundation\9.4\sas.exe" -sysin "D:\jobs\daily_fraud.sas"
    -log "D:\logs\daily_fraud.log" -print "D:\out\daily_fraud.lst" -nosplash -sysparm "30SEP2026"
```

(Written on one line in practice.) Save it in a `.bat` file and point Windows Task Scheduler at it.

**Running SAS in batch on Linux** (a shell script called by cron)

```bash
#!/bin/bash
# run_daily_fraud.sh - started by cron at 06:30 on weekdays
RUNDATE=$(date -d "yesterday" +%d%b%Y)
/sas/SASHome/SASFoundation/9.4/sas -sysin /sas/jobs/daily_fraud.sas \
    -log "/sas/logs/daily_fraud_${RUNDATE}.log" -sysparm "${RUNDATE}"
exit $?
```

```text
# crontab entry: minute hour day month weekday command
30 6 * * 1-5 /sas/jobs/run_daily_fraud.sh
```

**Reading the parameter inside the program**

```sas
%macro set_run_date;
    %global run_date;
    %if %length(&sysparm) > 0 %then %let run_date = &sysparm;
    %else %let run_date = %sysfunc(intnx(day, %sysfunc(today()), -1), date9.);   /* default: yesterday */
%mend set_run_date;
%set_run_date
```

**Other schedulers you will meet**

| Tool | Where |
| --- | --- |
| Windows Task Scheduler | Single Windows servers or PCs |
| cron | Linux and UNIX servers |
| SAS Management Console Schedule Manager (with LSF or the operating system scheduler) | SAS 9.4 platform installations |
| Control-M, Autosys, Tivoli | Enterprise schedulers in large banks, managing dependencies between many jobs |
| Enterprise Guide "Schedule project" | Personal or small-team automation (uses Windows Task Scheduler) |
| SAS Viya Jobs and Flows | SAS Viya |

### Error handling and logging for unattended jobs

```sas
options errorabend;                 /* stop the whole job at the first error (batch) */

%macro check_step(step=);
    %if &syserr > 4 %then %do;
        %put ERROR: Step &step failed (SYSERR=&syserr).;
        %abort cancel;
    %end;
%mend check_step;

proc printto log="/sas/logs/daily_fraud_&run_date..log" new;   /* a dated log per run */
run;
/* ... job steps, each followed by %check_step(...) ... */
proc printto;                                                  /* back to the normal log */
run;
```

| Tool | Purpose |
| --- | --- |
| `&SYSERR` | Return code of the last step |
| `&SYSCC` | Highest condition code of the job so far (0 OK, 4 warnings, larger = errors) |
| `%ABORT CANCEL` | Stop the program |
| `OPTIONS ERRORABEND` | Stop the job at the first error (batch) |
| `PROC PRINTTO LOG=` | Send the log to a dated file |

### Industry examples (8.19)

**Example 1: one PDF report per branch**

```sas
%macro branch_reports(month=);
    %local i n_br;
    proc sql noprint;
        select distinct branch into :br1-
        from rpt.branch_monthly
        where month = "&month";
    quit;
    %let n_br = &sqlobs;

    %do i = 1 %to &n_br;
        ods pdf file="/sas/out/branch_&&br&i.._&month..pdf";
        title "Branch &&br&i - &month";
        proc report data=rpt.branch_monthly(where=(branch = "&&br&i" and month = "&month")) nowd;
            column product accounts outstanding;
            define product     / group;
            define accounts    / analysis sum;
            define outstanding / analysis sum format=comma16.;
            rbreak after / summarize;
        run;
        ods pdf close;
    %end;
    title;
%mend branch_reports;

%branch_reports(month=2026-09)
```

**How the file name resolves** (for `i = 1`, `br1 = BR001`): `branch_&&br&i.._&month..pdf` → first
pass gives `branch_&br1._2026-09.pdf` → second pass gives `branch_BR001_2026-09.pdf`. Each `&` reference
consumes one dot, which is why there are two dots in a row.

**Example 2: a reusable data-quality check**

```sas
%macro dq_check(ds=, key=, required=);
    %local n_rows n_dup_keys i var n_missing;
    proc sql noprint;
        select count(*) into :n_rows trimmed from &ds;
        select count(*) into :n_dup_keys trimmed
        from (select &key from &ds group by &key having count(*) > 1);
    quit;
    %put NOTE: &ds rows=&n_rows duplicate keys=&n_dup_keys;

    %do i = 1 %to %sysfunc(countw(&required));
        %let var = %scan(&required, &i);
        proc sql noprint;
            select nmiss(&var) into :n_missing trimmed from &ds;
        quit;
        %if &n_missing > 0 %then %put WARNING: &ds has &n_missing missing values in &var..;
    %end;
%mend dq_check;

%dq_check(ds=work.txn, key=txn_id, required=cust_id amount txn_date)
```

On `work.txn` this writes `rows=6 duplicate keys=0` and a warning that `amount` has 1 missing value.

**Example 3: emailing the result** (your SAS administrator must set up the email server options)

```sas
filename alert email
    to=("fraud.team@yourbank.example")
    subject="Daily fraud summary &run_date"
    attach=("/sas/out/fraud_summary_&run_date..xlsx");

data _null_;
    file alert;
    put "The daily fraud summary for &run_date is attached.";
    put "Suspicious transactions: &n_suspicious";
run;
```

### 🧠 The automation lifecycle (from your prompt, section 36)

A real workflow: the **daily card-fraud report**.

```text
Manual process         an analyst edits dates in 6 programs and runs them each morning
      |
Parameterised code     dates and paths moved into %LET variables at the top
      |
Macro                  the steps wrapped in %daily_fraud(run_date=)
      |
Reusable macro         saved in the team autocall library, used for reruns and backfills
      |
Macro variables        run date from &SYSPARM; counts from INTO; branch lists from data
      |
Conditional execution  no data -> warn and stop; month end -> add the monthly pack
      |
Scheduled execution    cron or Control-M runs it at 06:30 on weekdays
      |
Logging                one dated log per run; logs scanned for ERROR and WARNING
      |
Error handling         &SYSERR and &SYSCC checks; %ABORT; non-zero exit code to the scheduler
      |
Production automation  email on success or failure; reruns by date; audit trail of every run
```

### ⚠️ Common mistakes

- Relying on `TODAY()` in a scheduled job, so a rerun for last Tuesday uses today's date. Pass the run
  date as a parameter.
- No error checks, so a failed load is followed by a "successful" report built on yesterday's data.
- One log file overwritten every day, with no history.
- Hard-coded paths and passwords in scheduled code.

### Exercises

1. **Level 1:** Run a program in batch mode from the command line and find its log.
2. **Level 2:** Pass a date with `-sysparm` and use it in a WHERE.
3. **Level 3:** Add `%check_step` after each step of a three-step job and force a failure to test it.
4. **Level 4 — Interview:** "How do you schedule a SAS program?"
5. **Level 5:** Automate Mini Project 3 end to end: parameter, macro, checks, dated log and a summary
   email.

### ⭐ Interview questions

**Q. How do you schedule a SAS job?**
- *Strong answer:* "SAS runs in batch with `-sysin`, and a scheduler such as cron, Windows Task
  Scheduler, Control-M or the SAS Management Console Schedule Manager starts it. I pass the run date
  with `-sysparm` and read `&SYSPARM`, write a dated log with PROC PRINTTO, check `&SYSERR` and
  `&SYSCC` after key steps, and make the job end with a non-zero exit code on failure so the scheduler
  can alert support and hold dependent jobs."

### Module wrap-up

- **I now know:** batch mode, schedulers, `-sysparm`, exit codes, error handling, dated logs, and
  industry macro patterns.
- **I can now:** turn a manual report into a scheduled, monitored production job.
- **Next:** Mini Project 4, then Part IX — production skills.

---

## Mini Project 4 — Automated Monthly Risk Report

**Uses:** Parts I–VIII. **Domain:** credit risk.

**Business requirement:** at every month end, risk management wants a portfolio report without anyone
running code by hand.

**Report content**

- Loans by product and DPD bucket (current, 1–30, 31–60, 61–90, 90+), counts and outstanding amounts
- Movement between DPD buckets compared with last month (a roll-rate table)
- Top 20 exposures per region
- A 13-month trend chart of the 90+ DPD rate

**Tasks**

1. Write the report for one hard-coded month first.
2. Turn it into `%risk_report(asof=)` with keyword parameters and validation (Modules 47–49).
3. Read the list of regions from data with `INTO :reg1-` and produce one PDF per region (Module 50).
4. Skip with a warning if the month's data is missing; add the trend chart only at quarter end (Module
   51).
5. Store the macro in an autocall library and call it from a driver program with `%INCLUDE` of a setup
   file (Module 54).
6. Run it in batch with `-sysparm`, a dated log, `&SYSERR` checks and an email on completion (Module
   55).
7. Debug it with `MPRINT` and keep a copy of the generated code with `MFILE` (Module 53).

**What it proves:** you can deliver a complete, automated, production-style SAS report.

**Part VIII checklist:** ✓ 8.1 · ✓ 8.2 · ✓ 8.3 · ✓ 8.4 · ✓ 8.5 · ✓ 8.6 · ✓ 8.7 · ✓ 8.8 · ✓ 8.9 · ✓ 8.10 · ✓ 8.11 · ✓ 8.12 ·
✓ 8.13 · ✓ 8.14 · ✓ 8.15 · ✓ 8.16 · ✓ 8.17 · ✓ 8.18 · ✓ 8.19

---

# Part IX — Production Skills (Modules 56–59)

These modules cover sections 10, 11, 25 and 26 of your prompt: debugging, performance, data quality
and production SAS. They are not separate items in the syllabus, but every SAS job needs them.

## MODULE 56 — Debugging SAS Programs Through the Log

**You will learn:** how to read the Log, and how to fix the most common problems step by step. **Why
it matters:** a program that "runs" can still be wrong; the Log is where SAS tells you. **Before you
start:** Parts I–VIII.

### How to read a Log

1. **Start at the top.** The first ERROR is usually the real cause; later errors are often side
   effects.
2. **Read every NOTE**, not only ERRORs. Several NOTEs mean real bugs (listed below).
3. **Check the row counts** in the NOTEs ("has 5,000 observations"): do they match what you expect?
4. **Look at the line number** in the message and the code just before it (a missing semicolon often
   causes an error on the next line).

### Problem → Log message → Root cause → Debugging → Fix

**1. Variable not found**

```sas
proc print data=work.txn;
    var amout;
run;
```

- **Log:** `ERROR: Variable AMOUT not found.`
- **Cause:** a typo, or the variable was dropped earlier.
- **Debugging:** run `PROC CONTENTS` on the dataset and compare names.
- **Fix:** `var amount;`

**2. Uninitialized variable**

```sas
data work.x;
    set work.txn;
    total = amout * 2;
run;
```

- **Log:** `NOTE: Variable amout is uninitialized.` and `NOTE: Missing values were generated as a
  result of performing an operation on missing values.`
- **Cause:** a misspelt name creates a new, empty variable. The step does not fail; every `total` is
  missing.
- **Fix:** correct the name. Many teams treat "uninitialized" as an error.

**3. Character converted to numeric**

```sas
data work.x;
    set work.txn;
    txn_num = substr(txn_id, 2) + 0;
run;
```

- **Log:** `NOTE: Character values have been converted to numeric values at the places given by:
  (Line):(Column).`
- **Cause:** text used in arithmetic.
- **Fix:** convert on purpose: `txn_num = input(substr(txn_id, 2), 3.);`

**4. Numeric converted to character**

```sas
data work.x;
    set work.txn;
    key = cust_id || amount;
run;
```

- **Log:** `NOTE: Numeric values have been converted to character values at the places given by:
  (Line):(Column).`
- **Cause:** a number used in text concatenation. SAS converts it with the `BEST12.` format, which adds
  leading blanks: `C101        5000`.
- **Fix:** `key = catx('_', cust_id, put(amount, 12.));` gives `C101_5000`.

**5. Invalid data**

```sas
data work.x;
    amount_txt = 'abc';
    amount = input(amount_txt, 8.);
run;
```

- **Log:** `NOTE: Invalid argument to function INPUT at line ... column ...`, followed by the PDV dump
  with `_ERROR_=1`.
- **Cause:** text that is not a valid number.
- **Fix:** if bad values are expected, use the `??` modifier to suppress the message and still get a
  missing value, then count them: `amount = input(amount_txt, ?? 8.); if missing(amount) then
  bad_amount + 1;`

**6. Division by zero**

```sas
utilisation = balance / credit_limit;
```

- **Log:** `NOTE: Division by zero detected at line ... column ...` and a PDV dump.
- **Fix:** `if credit_limit > 0 then utilisation = balance / credit_limit;`

**7. BY variables not sorted**

- **Log:** `ERROR: BY variables are not properly sorted on data set WORK.ACCT.`
- **Cause:** MERGE, SET with BY, or FIRST./LAST. on unsorted data.
- **Fix:** PROC SORT by the same variables first (or sort descending to match a `DESCENDING` in BY).

**8. Duplicate BY values in MERGE**

- **Log:** `NOTE: MERGE statement has more than one data set with repeats of BY values.`
- **Cause:** a many-to-many merge (Module 33). The result is almost certainly wrong.
- **Debugging:** count keys in each input with PROC FREQ `OUT=` where `count > 1`.
- **Fix:** remove the duplicates, or use PROC SQL if a many-to-many join is intended.

**9. Different lengths**

- **Log:** `WARNING: Multiple lengths were specified for the variable name by input data set(s). This
  can cause truncation of data.`
- **Fix:** a `LENGTH` statement before SET or MERGE with the longest length needed.

**10. SQL errors**

| Log | Cause | Fix |
| --- | --- | --- |
| `ERROR: Ambiguous reference, column cust_id is in more than one table.` | Same column in two joined tables | Use table aliases: `c.cust_id` |
| `ERROR: The following columns were not found in the contributing tables: gst.` | Alias used without CALCULATED | `calculated gst` |
| `NOTE: The query requires remerging summary statistics back with the original data.` | A column missing from GROUP BY (or remerging on purpose) | Add it to GROUP BY if it was a mistake |
| `NOTE: The execution of this query involves performing one or more Cartesian product joins that can not be optimized.` | Missing or wrong join condition | Add the ON condition |

**11. Macro problems** (details in Module 53)

| Log | Usual cause |
| --- | --- |
| `WARNING: Apparent symbolic reference X not resolved.` | Typo, scope, timing (CALL SYMPUT), single quotes |
| `WARNING: Apparent invocation of macro X not resolved.` | Macro not defined or not in the autocall path |
| `ERROR: More positional parameters found than defined.` | Unquoted comma in a value |
| Odd behaviour after a value with an apostrophe | Unmatched quote from data: use `%SUPERQ` |

**12. Dataset locked**

- **Log:** `ERROR: A lock is not available for BANK.TXN.DATA.`
- **Cause:** someone (or you, in another window or the dataset viewer) has the dataset open, or another
  job is writing it.
- **Fix:** close the viewer or wait for the other job. `options filelockwait=60;` makes SAS wait up to
  60 seconds for the lock before failing. In production, schedule jobs so they do not write the same
  dataset at the same time.

**13. Missing semicolon**

```sas
data work.x
    set work.txn;
run;
```

- **Log:** errors that mention `work.x set work.txn` or a syntax error near the next statement.
- **Cause:** without the semicolon, SAS reads `data work.x set work.txn;` as one statement and thinks
  you want to create datasets called `x`, `set` and `txn`.
- **Fix:** add the semicolon. Always check the line **before** the reported error.

**14. Unbalanced quotes**

- **Symptom:** in an interactive session, nothing seems to run and the Log shows no new messages.
- **Cause:** a missing closing quote makes SAS treat the rest of the program as text.
- **Fix:** submit this "magic string" to close everything, then fix the code:

```sas
;*';*";*/;quit;run;
```

### A log-scanning macro for production

```sas
%macro scan_log(log=);
    %local n_issues;
    data work.log_issues;
        infile "&log" truncover;
        input line $char256.;
        line_no = _n_;
        if index(line, 'ERROR') = 1 or index(line, 'WARNING') = 1
           or find(line, 'uninitialized', 'i')
           or find(line, 'converted to', 'i')
           or find(line, 'repeats of BY values', 'i')
           or find(line, 'Invalid data', 'i')
           or find(line, 'Missing values were generated', 'i');
    run;

    proc sql noprint;
        select count(*) into :n_issues trimmed from work.log_issues;
    quit;

    %if &n_issues > 0 %then %put WARNING: &n_issues issue line(s) found in &log..;
    %else %put NOTE: &log is clean.;
%mend scan_log;

%scan_log(log=/sas/logs/daily_fraud_30SEP2026.log)
```

### Exercises

1. **Level 1:** Create an uninitialized-variable NOTE on purpose and fix it.
2. **Level 2:** Create both type-conversion NOTEs and rewrite the code with INPUT and PUT.
3. **Level 3:** Run a many-to-many MERGE, read the NOTE, and prove the result is wrong.
4. **Level 4 — Interview:** "Which NOTEs in the log do you treat as errors?"
5. **Level 5:** Run `%scan_log` on the logs of your mini projects and fix everything it finds.

### ⭐ Interview questions

**Q. Which NOTE messages worry you?**
- *Strong answer:* "Uninitialized variables, automatic character/numeric conversion, invalid data,
  missing values generated, division by zero, MERGE with repeats of BY values, and unexpected
  remerging. They don't stop the step, but they usually mean wrong results, so our log scan treats them
  like errors."

### Module wrap-up

- **I now know:** how to read the Log and fix the 14 most common problems.
- **I can now:** debug my own and other people's programs systematically, and scan logs automatically.
- **Next:** Module 57 — performance.

---

## MODULE 57 — Performance Optimization

**You will learn:** where SAS spends time, how to measure it, and the techniques that make programs
fast on 10 or 100 million rows. **Why it matters:** in banks, nightly jobs must finish before the
morning. **Before you start:** Parts III, V and VI.

### 🧠 Where the time goes

Most SAS jobs spend most of their time on **I/O**: reading and writing data on disk (or across a
network from a database). CPU work is usually smaller. So the biggest gains come from **moving less
data**: fewer rows, fewer columns, fewer passes, fewer copies.

### Measure first

```sas
options fullstimer;
```

The Log then shows, for every step:

```text
NOTE: DATA statement used (Total process time):
      real time           12.31 seconds
      user cpu time        2.10 seconds
      system cpu time      1.05 seconds
      memory              1024.00k
```

📌 If **real time** is much larger than **CPU time**, the step is waiting for I/O (disk or network).
Reduce data movement. If CPU time is high, look at the calculations, sorting or joins.

### The techniques: bad vs good, and why

| # | Bad approach | Good approach | Why it is faster |
| --- | --- | --- | --- |
| 1 | `set big;` then `keep a b c;` | `set big(keep=a b c);` | Only 3 columns are read from disk into the PDV |
| 2 | `set big; if region = 'WEST';` | `set big; where region = 'WEST';` | Failing rows never enter the PDV; an index can be used |
| 3 | Filtering after a join | Filtering each table before (or in) the join | Fewer rows to match |
| 4 | Sorting a big table before every report | Sort once; use `CLASS` instead of `BY`; let SQL choose | Sorting reads and writes the whole table |
| 5 | Sort + MERGE to look up a small table | Hash object or format lookup | No sorting of the big table |
| 6 | Five steps each reading the same big table | One DATA step with several OUTPUT datasets | One pass instead of five |
| 7 | Intermediate datasets for every step | Views, or combining steps | Less writing and re-reading |
| 8 | `data hist; set hist new; run;` | `proc append base=hist data=new; run;` | Only the new rows are written |
| 9 | Pulling a whole database table into SAS | Filter and aggregate in the database (pass-through) | Only the result crosses the network |
| 10 | Character lengths of 200 everywhere | Lengths that fit the data | Smaller rows, less I/O |
| 11 | No index on a column used for selective lookups | An index on it | Direct access to the few matching rows |
| 12 | Wide text-heavy data stored as is | `options compress=yes;` (or `compress=binary` for numeric-heavy data) | Smaller files; less I/O for some CPU |
| 13 | A macro loop that reads the full table once per branch | One step with `BY branch`, or one pass with OUTPUT per branch | One pass instead of hundreds |

### PROC SQL: seeing the join method

```sas
proc sql _method;
    create table work.j as
    select t.*, c.name
    from work.txn as t inner join work.customers as c
         on t.cust_id = c.cust_id;
quit;
```

The Log lists codes such as `sqxjhsh` (hash join), `sqxjm` (sort-merge join) or `sqxjndx` (index
join). A hash join is usually fastest when one table is small enough for memory.

### Database pushdown checklist

- Use `options sastrace=',,,d' sastraceloc=saslog nostsuffix;` to see the SQL SAS sends (Module 11).
- Avoid SAS-only functions in WHERE clauses on database tables; they stop the filter being pushed down.
- Use explicit pass-through for heavy joins and aggregations.
- Tune `READBUFF=` (rows fetched per trip) for reads and `INSERTBUFF=` or `BULKLOAD=` for writes.
- Do not join a big database table to a SAS dataset in one query; upload the small table or filter
  first.

### 💭 "What would happen with 100 million rows?"

| Program | With 10 thousand rows | With 100 million rows |
| --- | --- | --- |
| `if` instead of `where` | No difference you would notice | Every row read into the PDV; minutes lost |
| No `keep=` on a 150-column table | Instant | Gigabytes of extra I/O |
| Sorting twice | Instant | Two full read-write passes plus temporary disk space; may run out of space |
| Many-to-many SQL join by mistake | A few extra rows | Billions of rows; the job fails or fills the disk |
| PROC PRINT of the result | Fine | Useless, and a huge output file |
| Pandas in memory | Fine | Probably runs out of memory; SAS reads row by row |

### 💼 Banking scenario

A nightly card-fraud job took 3 hours 40 minutes. Changes: `keep=` on the 180-column authorisation
table (−60%), WHERE instead of IF for the date filter, a hash lookup for the watch list instead of
sort + MERGE, one DATA step writing three outputs instead of three steps, and PROC APPEND for the history
table. New run time: 38 minutes. (Describe changes like these, with your own measured numbers, in
interviews.)

### Exercises

1. **Level 1:** Turn on `FULLSTIMER` and record real and CPU time for a step.
2. **Level 2:** Compare `keep=` on input vs a KEEP statement on a wide table.
3. **Level 3:** Replace a sort + MERGE lookup with a hash object and compare times.
4. **Level 4 — Interview:** "How would you speed up a slow SAS job?"
5. **Level 5:** Take your Mini Project 3 program, measure every step, and halve its total run time.

### ⭐ Interview questions

**Q. How do you optimise a slow SAS program?**
- *Strong answer:* "First I measure with FULLSTIMER to find the slow steps and whether they are I/O or
  CPU bound. Then I reduce data movement: KEEP= and WHERE on input, filtering early, pushing work to the
  database, avoiding unneeded sorts (CLASS instead of BY, sort once), hash lookups instead of sort and
  merge, one pass with multiple outputs, PROC APPEND for appends, indexes for selective lookups, and
  right-sized lengths or compression. I re-measure after each change."

### Module wrap-up

- **I now know:** where time goes, FULLSTIMER, the main techniques and their reasons, join methods and
  database pushdown.
- **I can now:** make SAS programs fast on very large data and explain why.
- **Next:** Module 58 — data quality and validation.

---

## MODULE 58 — Data Quality and Validation

**You will learn:** the standard checks every bank runs on data, and how to build them into SAS jobs.
**Why it matters:** a fast report on bad data is worse than no report. Regulators expect documented
controls. **Before you start:** Parts III–VI.

### The checks

| Check | Question it answers | SAS tools | Banking example |
| --- | --- | --- | --- |
| **Null check** | Are required fields filled? | `NMISS` in PROC MEANS / SQL, `PROC FREQ ... MISSING` | Transactions without an account number |
| **Duplicate records** | Are whole rows repeated? | `PROC SORT NODUPRECS` with `BY _ALL_` | A file loaded twice |
| **Duplicate key check** | Is the key unique? | `PROC SORT NODUPKEY DUPOUT=`, SQL `GROUP BY ... HAVING COUNT(*) > 1` | Two rows with the same transaction ID |
| **Invalid values** | Are codes from the allowed list? | `NOT IN (...)`, formats with `OTHER` | Channel code `XX` |
| **Range check** | Are numbers within sensible limits? | `WHERE` / `IF` | FICO outside 300–900; negative loan amounts |
| **Pattern check** | Does text have the right shape? | `PRXMATCH`, `NOTDIGIT` | PAN, IFSC code, 10-digit mobile |
| **Outliers** | Are values extreme? | PROC UNIVARIATE percentiles | A ₹50 crore retail transaction |
| **Data type issues** | Did numbers arrive as text? | PROC CONTENTS, conversion NOTEs | Amount read as character |
| **Date issues** | Are dates valid and logical? | `missing()` after INPUT, comparisons | Transaction before account opening; future dates |
| **Referential integrity** | Does every child have a parent? | MERGE with `IN=`, SQL anti-join | Transactions for accounts not in the master |
| **Record counts** | Did every row arrive? | `&SQLOBS`, `NOBS=`, PROC SQL `COUNT(*)` | Source file says 1,204,553 rows; SAS loaded 1,204,551 |
| **Control totals** | Do the totals match? | SUM in SQL vs trailer record | Total amount in the trailer vs loaded total |
| **Reconciliation** | Do two systems agree? | Full join, PROC COMPARE | Core banking balance vs general ledger |
| **Source-to-target** | Did the ETL change anything it should not? | PROC COMPARE, counts and sums per key | Staging vs mart |
| **Before/after** | Did a code change alter results? | PROC COMPARE on old vs new output | UAT evidence |

### A complete check program on `work.txn`

```sas
proc sql;
    create table work.dq_results as
    select 'Missing amount' as check_name length=40,
           sum(case when missing(amount) then 1 else 0 end) as failed_rows
    from work.txn
    union all
    select 'Negative or zero amount',
           sum(case when amount <= 0 and not missing(amount) then 1 else 0 end)
    from work.txn
    union all
    select 'Unknown channel',
           sum(case when channel not in ('ATM', 'POS', 'ONLINE', 'UPI', 'BRANCH') then 1 else 0 end)
    from work.txn
    union all
    select 'Future transaction date',
           sum(case when txn_date > '30SEP2026'd then 1 else 0 end)
    from work.txn
    union all
    select 'Duplicate txn_id', count(*)
    from (select txn_id from work.txn group by txn_id having count(*) > 1)
    union all
    select 'Orphan customer (not in customer master)', count(*)
    from work.txn
    where cust_id not in (select cust_id from work.customers);
quit;

data work.dq_results;
    set work.dq_results;
    length status $4;
    status = ifc(failed_rows = 0, 'PASS', 'FAIL');
run;
```

**Output**

| check_name | failed_rows | status |
| --- | --- | --- |
| Missing amount | 1 | FAIL |
| Negative or zero amount | 0 | PASS |
| Unknown channel | 0 | PASS |
| Future transaction date | 0 | PASS |
| Duplicate txn_id | 0 | PASS |
| Orphan customer (not in customer master) | 0 | PASS |

**Why:** T004 has no amount. All channels are allowed codes, all dates are in January 2026, every
transaction ID is unique, and C101, C102 and C103 all exist in the customer master.

### Control totals: comparing with the source

```sas
%macro control_totals(src_rows=, src_amt=, target=);
    %local tgt_rows tgt_amt diff;
    proc sql noprint;
        select count(*), sum(amount) format=20.2
        into :tgt_rows trimmed, :tgt_amt trimmed
        from &target;
    quit;

    %let diff = %sysevalf(&tgt_amt - &src_amt);     /* %SYSFUNC cannot do arithmetic itself */

    %if &tgt_rows ne &src_rows %then
        %put ERROR: Row count mismatch: source=&src_rows target=&tgt_rows;
    %else %if %sysevalf(%sysfunc(abs(&diff)) > 0.01) %then
        %put ERROR: Amount mismatch: source=&src_amt target=&tgt_amt;
    %else
        %put NOTE: Control totals agree (&tgt_rows rows, &tgt_amt).;
%mend control_totals;

/* the source values usually come from the file's trailer record */
%control_totals(src_rows=6, src_amt=230300.00, target=work.txn)
```

**Log:** `NOTE: Control totals agree (6 rows, 230300.00).`

### Production practice

- Run checks **automatically** in every job, after loading and before reporting.
- Store results in a **DQ results table** with the run date, so trends are visible.
- Decide in advance which checks **stop** the job (for example a control-total mismatch) and which only
  **warn** (for example a few invalid codes).
- Send rejected rows to a **reject dataset** with a reason code, never just delete them.

### Python and SQL comparison

- SQL Server: the same checks as queries; often scheduled in SSIS or stored procedures.
- Python: libraries such as `great_expectations` or `pandera`, or plain Pandas checks
  (`df["amount"].isna().sum()`, `df.duplicated("txn_id").sum()`).

### Exercises

1. **Level 1:** Count missing values in every numeric column of a dataset with one PROC MEANS.
2. **Level 2:** Find duplicate transaction IDs and save them with `DUPOUT=`.
3. **Level 3:** Find transactions whose customer is not in the customer master, two ways.
4. **Level 4 — Interview:** "What data-quality checks would you run on a daily transaction feed?"
5. **Level 5:** Build a reusable DQ macro that writes one result row per check to a permanent DQ table
   with the run date, and stops the job when a critical check fails.

### ⭐ Interview questions

**Q. How do you validate a data load?**
- *Strong answer:* "Record counts and control totals against the source, null checks on key fields,
  duplicate-key checks, valid-value and range checks, date logic, referential integrity against
  masters, and reconciliation to downstream systems. Results go to a DQ table; critical failures stop
  the job and alert support, and rejected rows are kept with reason codes."

### Module wrap-up

- **I now know:** the standard data-quality checks, control totals, reconciliation and how to automate
  them.
- **I can now:** build validated, auditable data loads.
- **Next:** Module 59 — SAS in production.

---

## MODULE 59 — SAS in Production

**You will learn:** how SAS work is organised, tested, deployed, run and monitored in a real
organisation. **Why it matters:** interviewers for SAS developer roles ask "how does code get to
production?" **Before you start:** Modules 55–58.

### The environments

```text
DEVELOPMENT  ->  TEST / SIT  ->  UAT  ->  PRODUCTION
  write code      testers check   business users     scheduled jobs run
  unit tests      integration     sign off results   on real data; only
                                                     support staff change it
```

| Stage | Who | What happens |
| --- | --- | --- |
| **Development** | Developers | Write and unit-test code on sample or masked data |
| **Testing (SIT)** | Test team | Run the full process; check it works with other systems |
| **UAT** | Business users | Compare outputs with expectations (often with PROC COMPARE evidence) and sign off |
| **Production** | Operations / production support | Scheduled runs on real data; changes only through approved releases |

📌 **Segregation of duties:** developers normally cannot change production code or data directly.
Changes go through version control, review and a release process.

### What a production setup looks like

| Area | Typical practice |
| --- | --- |
| **Batch processing** | Jobs run unattended in batch mode, usually overnight |
| **Scheduling and dependencies** | An enterprise scheduler runs jobs in order; job B starts only when job A succeeds (or when a trigger file appears) |
| **Libraries** | Separate RAW, STAGE, MART and REPORT libraries per environment; RAW is read-only |
| **Shared environments** | Central SAS servers; access controlled by groups and metadata |
| **Database connections** | Defined once (authentication domains), not with passwords in code |
| **ETL** | DATA steps and PROC SQL in programs, or SAS Data Integration Studio jobs |
| **Reporting** | ODS PDF/Excel outputs, SAS Visual Analytics, or data marts feeding Power BI |
| **Logging** | One dated log per run; logs scanned automatically for ERROR, WARNING and bad NOTEs |
| **Error handling** | Return-code checks, `%ABORT`, non-zero exit codes, alerts |
| **Monitoring** | A job-status table with start time, end time, row counts and status per run |
| **Reusable macros** | A reviewed autocall library shared by all jobs |
| **Parameterisation** | Run date via `-sysparm`; settings in a config file or table, not in code |
| **Deployment** | Code in Git; promoted between environments by release scripts or SAS packages |

### A production program template

```sas
/*****************************************************************************
 Program    : daily_fraud.sas
 Purpose    : Apply fraud rules to yesterday's card transactions
 Inputs     : RAW.CARD_TXN_DAILY, MART.CARD_MASTER, MART.WATCHLIST
 Outputs    : RPT.FRAUD_ALERTS_DAILY, fraud_summary_<date>.xlsx
 Schedule   : 06:30 on weekdays (scheduler job FRD_DAILY_01)
 Parameters : -sysparm <run date as DDMONYYYY>; default = yesterday
 Change log : 05OCT2026  v1.0  first version
*****************************************************************************/

%include "/sas/config/setup.sas";      /* environment, librefs, options, sasautos */
%set_run_date                          /* autocall macro: &run_date from &sysparm or yesterday */

%job_status(step=START)                /* writes a row to the job-status table */

data stage.card_txn_&run_date;         /* 1. load */
    set raw.card_txn_daily(keep=txn_id card_no txn_ts amount merchant_id city channel);
    where datepart(txn_ts) = "&run_date"d;
run;
%check_step(step=load)

%dq_check(ds=stage.card_txn_&run_date, key=txn_id, required=card_no amount)   /* 2. validate */

/* 3. rules, 4. summary, 5. outputs ... each followed by %check_step(...) */

%job_status(step=END)
%scan_log(log=/sas/logs/daily_fraud_&run_date..log)
```

(`%set_run_date`, `%check_step`, `%dq_check` and `%scan_log` are the macros from Modules 55, 56 and 58;
`%job_status` is a small macro your team would write to record start and end times.)

### A day in production

```text
05:30  Source systems drop files; a trigger file arrives
05:35  Scheduler starts the load job (waits for the trigger)
05:50  Data-quality job: counts, control totals, key checks -> DQ table
06:00  If DQ passed: transformation and fraud-rule jobs run; if not: alert, dependent jobs held
06:30  Reporting jobs: ODS Excel/PDF reports, mart refresh for dashboards
06:45  Log scan; job-status table updated; success email to the business
09:00  Support team reviews any failures; reruns by date after a fix
```

### ⚠️ Common production mistakes

- `TODAY()` instead of a run-date parameter (reruns produce wrong data).
- Hard-coded paths, librefs and passwords.
- No checks between steps, so failures propagate silently.
- Overwriting yesterday's outputs with no history or log retention.
- Changing production code directly "just this once".

### Exercises

1. **Level 1:** Add a standard header comment block to one of your programs.
2. **Level 2:** Move every hard-coded value in a program into a setup file or parameters.
3. **Level 3:** Write `%job_status` to record step name, start time, end time and status in a dataset.
4. **Level 4 — Interview:** "Describe how a SAS program moves from development to production."
5. **Level 5:** Package Mini Project 4 as a production job: Git folder layout, setup file, autocall
   macros, scheduler script, dated logs, DQ table and job-status table.

### ⭐ Interview questions

**Q. How does SAS code get to production in your team?**
- *Strong answer:* "We develop on masked data, keep code in Git, and test in SIT. Business users sign
  off in UAT, often with PROC COMPARE evidence against the old process. A release promotes the code to
  production, where an enterprise scheduler runs it in batch with a run-date parameter. Every job logs
  to a dated file, checks return codes between steps, writes data-quality and job-status results, and
  alerts support on failure."

*(If you have not yet worked on a production SAS team, describe this as the process you followed in
your projects or as how you understand it works. Do not claim experience you do not have; see Part
XII.)*

### Module wrap-up

- **I now know:** environments, release flow, scheduling, dependencies, logging, monitoring and
  deployment.
- **I can now:** describe and build production-style SAS jobs.
- **Next:** Part X — master references.

---

# Part X — Master References

Quick-reference tables for revision. Each links back to the module that explains the topic.

## X.1 SAS Functions Master Reference

For every function: what it does, an example with its input and output, the common mistake, and the
SQL Server and Python/Pandas equivalents.

### Character functions — what they do

| Function | Purpose | Example (input) | Output |
| --- | --- | --- | --- |
| `LENGTH(s)` | Length without trailing blanks (1 if blank) | `length('Mumbai  ')` | 6 |
| `LENGTHN(s)` | Same, but 0 if blank | `lengthn('  ')` | 0 |
| `LENGTHC(s)` | Length including trailing blanks | `lengthc('Mumbai  ')` | 8 |
| `SUBSTR(s, p, n)` | Part of a string | `substr('ACC1234567', 4, 4)` | `1234` |
| `SCAN(s, n, d)` | n-th word | `scan('a@b.com', 2, '@')` | `b.com` |
| `COUNT(s, sub)` | Times a substring appears | `count('ATM-ATM-POS', 'ATM')` | 2 |
| `INDEX(s, sub)` | Position of a substring (case-sensitive) | `index('NEFT/UPI', 'UPI')` | 6 |
| `FIND(s, sub, 'i')` | Position, with options (`i` = ignore case) | `find('upi pay', 'UPI', 'i')` | 1 |
| `UPCASE(s)` | Upper case | `upcase('mumbai')` | `MUMBAI` |
| `LOWCASE(s)` | Lower case | `lowcase('ATM')` | `atm` |
| `PROPCASE(s)` | First letter of each word capital | `propcase('ASHA RAO')` | `Asha Rao` |
| `COMPRESS(s, c, m)` | Remove (or keep, with `k`) characters | `compress('+91-98201', , 'kd')` | `9198201` |
| `STRIP(s)` | Remove leading and trailing blanks | `strip('  C101  ')` | `C101` |
| `TRIM(s)` | Remove trailing blanks | `trim('C101  ')` | `C101` |
| `CAT(a, b)` | Join exactly | `cat('A ', 'B')` | `A B` |
| `CATS(a, b)` | Join after stripping each | `cats(' A ', ' B ')` | `AB` |
| `CATT(a, b)` | Join after trimming trailing blanks | `catt('A  ', 'B')` | `AB` |
| `CATX(sep, a, b)` | Strip, join with a separator, skip blanks | `catx('-', 'BR1', '', '26')` | `BR1-26` |
| `TRANWRD(s, from, to)` | Replace a word or substring | `tranwrd('RD NO 5 ROAD', 'ROAD', 'RD')` | `RD NO 5 RD` |
| `TRANSLATE(s, to, from)` | Replace characters one for one | `translate('9-8/7', '  ', '-/')` | `9 8 7` |
| `INPUT(s, informat)` | Text to number or date | `input('1,250', comma8.)` | 1250 |
| `PUT(x, format)` | Number or date to text | `put(42, z5.)` | `00042` |

### Character functions — traps and equivalents

| Function | Common mistake | SQL Server | Python / Pandas |
| --- | --- | --- | --- |
| `LENGTH` | Expecting 0 for a blank value | `LEN(s)` | `len(s.rstrip())` / `s.str.len()` |
| `LENGTHN` | — | `LEN(s)` | `s.str.strip().str.len()` |
| `LENGTHC` | Confusing it with LENGTH | `DATALENGTH(s)` | `len(s)` |
| `SUBSTR` | Positions start at 1 (not 0 as in Python) | `SUBSTRING(s, p, n)` | `s.str[p-1:p-1+n]` |
| `SCAN` | Default delimiters include `.` `-` `/` | `STRING_SPLIT` / `PARSENAME` | `s.str.split(d).str[n-1]` |
| `COUNT` | Case-sensitive unless `'i'` is given | `(LEN(s) - LEN(REPLACE(s, sub, ''))) / LEN(sub)` | `s.str.count(sub)` |
| `INDEX` | Case-sensitive | `CHARINDEX(sub, s)` | `s.str.find(sub) + 1` |
| `FIND` | Forgetting the modifier argument | `CHARINDEX` with a collation | `s.str.lower().str.find(...) + 1` |
| `UPCASE` | Comparing mixed case without it | `UPPER(s)` | `s.str.upper()` |
| `LOWCASE` | — | `LOWER(s)` | `s.str.lower()` |
| `PROPCASE` | `O'brien`, `Mcdonald` | No built-in | `s.str.title()` |
| `COMPRESS` | Forgetting the empty second argument with modifiers | Nested `REPLACE` / `TRANSLATE` | `s.str.replace(r'\D', '', regex=True)` |
| `STRIP` | Expecting it to remove inner spaces (use COMPBL) | `TRIM(s)` (2017+) | `s.str.strip()` |
| `TRIM` | Expecting it to matter when assigning to a fixed-length variable | `RTRIM(s)` | `s.str.rstrip()` |
| `CAT` | Unwanted blanks in the result | `CONCAT(a, b)` | `a + b` |
| `CATS` | Default length 200 | `CONCAT(TRIM(a), TRIM(b))` | `a.str.strip() + b.str.strip()` |
| `CATT` | Leading blanks are kept | `CONCAT(RTRIM(a), RTRIM(b))` | `a.str.rstrip() + b` |
| `CATX` | Default length 200 | `CONCAT_WS(sep, a, b)` | `sep.join([...])` |
| `TRANWRD` | Default length 200 | `REPLACE(s, from, to)` | `s.str.replace(from, to)` |
| `TRANSLATE` | Swapping the `to` and `from` arguments | `TRANSLATE(s, from, to)` (opposite order!) | `str.maketrans` |
| `INPUT` | Using a format instead of an informat; invalid data notes | `CAST` / `TRY_CAST` | `pd.to_numeric`, `pd.to_datetime` |
| `PUT` | Result is text, often with leading blanks | `CAST(x AS VARCHAR)`, `FORMAT` | `str(x)`, `f"{x:05d}"` |

### Numeric functions — what they do

| Function | Purpose | Example (input) | Output |
| --- | --- | --- | --- |
| `SUM(a, b, ...)` | Add, ignoring missing | `sum(100, .)` | 100 |
| `MEAN(a, b, ...)` | Average, ignoring missing | `mean(10, ., 20)` | 15 |
| `MIN(...)` / `MAX(...)` | Smallest / largest, ignoring missing | `min(5, ., 3)` | 3 |
| `ROUND(x, unit)` | Round to a unit | `round(1234.567, 0.01)` | 1234.57 |
| `CEIL(x)` | Round up | `ceil(4.1)` | 5 |
| `FLOOR(x)` | Round down | `floor(-3.7)` | -4 |
| `INT(x)` | Drop the decimals | `int(-3.7)` | -3 |
| `ABS(x)` | Absolute value | `abs(-500)` | 500 |
| `MOD(a, b)` | Remainder | `mod(17, 5)` | 2 |
| `LAG(x)` | Value from the previous LAG call | `lag(amount)` on rows 5000, 2300 | ., 5000 |
| `DIF(x)` | `x - lag(x)` | `dif(amount)` on rows 5000, 2300 | ., -2700 |
| `RAND('uniform')` | Random number from 0 to 1 | `rand('uniform')` | e.g. 0.4127 |
| `RANUNI(seed)` | Older random number function | `ranuni(2026)` | e.g. 0.8812 |

### Numeric functions — traps and equivalents

| Function | Common mistake | SQL Server | Python / Pandas |
| --- | --- | --- | --- |
| `SUM` | Writing `sum(m1-m12)` without `OF` | `ISNULL(a,0) + ISNULL(b,0)` | `df[cols].sum(axis=1)` |
| `MEAN` | Expecting missing to count as 0 | `(a + b) / 2` with NULL handling | `df[cols].mean(axis=1)` |
| `MIN` / `MAX` | Using them down rows (they work across columns; use PROC MEANS or SQL aggregates for rows) | `LEAST` / `GREATEST` (2022+) | `df[cols].min(axis=1)` |
| `ROUND` | Expecting Python's round-half-to-even | `ROUND(x, 2)` | `round()` rounds halves to even |
| `CEIL` | — | `CEILING(x)` | `math.ceil`, `np.ceil` |
| `FLOOR` | Confusing it with INT for negatives | `FLOOR(x)` | `math.floor`, `np.floor` |
| `INT` | Confusing it with FLOOR for negatives | `CAST(x AS INT)` | `int(x)`, `np.trunc` |
| `ABS` | — | `ABS(x)` | `abs(x)`, `.abs()` |
| `MOD` | Sign of the result follows the first value | `a % b` | `a % b` (sign follows the divisor) |
| `LAG` | Calling it inside an IF; not resetting per group | `LAG(x) OVER (...)` | `.shift(1)` |
| `DIF` | Same as LAG | `x - LAG(x) OVER (...)` | `.diff()` |
| `RAND` | Not setting a seed with `CALL STREAMINIT` | `RAND()`, `NEWID()` | `np.random.default_rng(seed)` |
| `RANUNI` | Using it for new work (weaker method) | `RAND(seed)` | `random.random()` |

### Date and datetime functions — what they do

| Function | Purpose | Example (input) | Output |
| --- | --- | --- | --- |
| `TODAY()` | Today's date | `today()` | e.g. `05OCT2026` (24384) |
| `DATE()` | Same as TODAY | `date()` | e.g. `05OCT2026` |
| `MDY(m, d, y)` | Build a date | `mdy(9, 30, 2026)` | `30SEP2026` (24379) |
| `YMD` | ⚠️ **Not a SAS function.** Use `MDY` or `INPUT(..., YYMMDD10.)` | `input('2026-09-30', yymmdd10.)` | `30SEP2026` |
| `YEAR(d)` | Year | `year('30SEP2026'd)` | 2026 |
| `MONTH(d)` | Month | `month('30SEP2026'd)` | 9 |
| `DAY(d)` | Day of month | `day('30SEP2026'd)` | 30 |
| `INTCK(i, d1, d2)` | Number of interval boundaries crossed | `intck('month', '31JAN2026'd, '01FEB2026'd)` | 1 |
| `INTNX(i, d, n, a)` | Move by intervals, align to B/M/E/S | `intnx('month', '15JAN2026'd, 0, 'e')` | `31JAN2026` |
| `DHMS(d, h, m, s)` | Build a datetime | `dhms('02JAN2026'd, 10, 30, 0)` | `02JAN2026:10:30:00` |
| `DATEPART(dt)` | Date from a datetime | `datepart('02JAN2026:10:30:00'dt)` | `02JAN2026` |
| `TIMEPART(dt)` | Time from a datetime | `timepart('02JAN2026:10:30:00'dt)` | `10:30:00` (37800) |
| `DATETIME()` | Current date and time | `datetime()` | e.g. `05OCT2026:09:15:42` |

### Date functions — traps and equivalents

| Function | Common mistake | SQL Server | Python / Pandas |
| --- | --- | --- | --- |
| `TODAY` / `DATE` | Using it in scheduled jobs that may be rerun (pass a run date instead) | `CAST(GETDATE() AS DATE)` | `date.today()` |
| `MDY` | Argument order is month, day, year | `DATEFROMPARTS(y, m, d)` | `date(y, m, d)` |
| `YMD` | Expecting it to exist | `DATEFROMPARTS` | `date(y, m, d)` |
| `YEAR` / `MONTH` / `DAY` | Applying them to a datetime (use DATEPART first) | `YEAR(d)`, `MONTH(d)`, `DAY(d)` | `.dt.year`, `.dt.month`, `.dt.day` |
| `INTCK` | Expecting elapsed time; use `'c'` for complete periods | `DATEDIFF(month, d1, d2)` (same boundary logic) | month arithmetic / `relativedelta` |
| `INTNX` | Forgetting the alignment argument | `DATEADD`, `EOMONTH` | `pd.offsets.MonthEnd`, `relativedelta` |
| `DHMS` | Passing a datetime instead of a date as the first argument | `DATEADD(second, s, CAST(d AS DATETIME))` | `pd.Timestamp(...)` |
| `DATEPART` | Forgetting it, and comparing a datetime with a date constant | `CAST(dt AS DATE)` | `ts.normalize()`, `.dt.date` |
| `TIMEPART` | — | `CAST(dt AS TIME)` | `.dt.time` |
| `DATETIME` | Same rerun problem as TODAY | `GETDATE()` / `SYSDATETIME()` | `datetime.now()` |

## X.2 DATA Step Master Reference

How each DATA step statement works with the PDV (Module 7).

| Statement | What it does | When it acts | Effect on the PDV |
| --- | --- | --- | --- |
| `DATA` | Names the output dataset(s) | Compile | Creates the descriptor portion of each output |
| `SET` | Reads observations from SAS datasets | Execute | Loads one observation into the PDV per read; its variables are retained |
| `MERGE` | Joins datasets side by side | Execute | Loads matching observations; values kept within a BY group |
| `BY` | Groups processing | Compile and execute | Creates temporary `FIRST.` and `LAST.` variables |
| `IF ... THEN ... ELSE` | Conditional actions | Execute | Tests PDV values |
| Subsetting `IF` | Keeps rows that pass | Execute | Stops the iteration (no output) when false |
| `DO ... END` | Groups or repeats statements | Execute | Repeats work within one iteration |
| `KEEP` / `DROP` | Choose output variables | Compile | Variables stay in the PDV; only output is affected |
| `RENAME` | Rename output variables | Compile | Code still uses the old names |
| `WHERE` | Filters input rows | Before the PDV | Failing rows never reach the PDV |
| `OUTPUT` | Writes the PDV as a row | Execute | Turns off the implicit output at the end of the step |
| `RETAIN` | Keeps values between iterations | Compile (flag) and execute | Variable is not reset to missing |
| Sum statement `x + y;` | Running total | Execute | Retained, starts at 0, ignores missing |
| `ARRAY` | Names a group of variables | Compile | No new storage, just a reference (temporary arrays hold values) |
| `INFILE` | Names the raw file and reading options | Execute | Controls the input buffer |
| `INPUT` | Reads raw data | Execute | Moves values from the input buffer to the PDV |
| `DATALINES` / `CARDS` | In-line raw data | — | Treated as a raw file |
| `LENGTH` | Sets type and length | Compile | Must come before the first use |
| `FORMAT` | Display format | Compile | Stored in the descriptor portion |
| `INFORMAT` | Default reading informat | Compile | Used by INPUT |
| `LABEL` | Descriptive label | Compile | Stored in the descriptor portion |
| `DELETE` | Discards the current row | Execute | Returns to the top without output |
| `STOP` | Ends the step | Execute | Needed with POINT= |
| `PUT` | Writes to the Log or a file | Execute | Reads the PDV |

## X.3 PROC SQL Master Reference

| Feature | PROC SQL syntax | SAS-specific note | Module |
| --- | --- | --- | --- |
| SELECT / FROM | `select a, b from t;` | Plain SELECT prints a report | 27 |
| WHERE | `where a > 10` | Supports CONTAINS, LIKE, IS MISSING, =* | 27 |
| GROUP BY / HAVING | `group by a having sum(b) > 0` | Remerging if detail columns are selected | 29 |
| ORDER BY | `order by a desc` | Column numbers allowed (`order by 2`) | 29 |
| DISTINCT | `select distinct a` | | 27 |
| CASE / nested CASE | `case when ... then ... else ... end` | Result length is the longest value | 28 |
| INNER / LEFT / RIGHT / FULL JOIN | `from a left join b on a.k = b.k` | No sort needed; many-to-many gives all combinations | 31 |
| UNION / UNION ALL / INTERSECT / EXCEPT | `select ... union all select ...` | Matches columns by **position**; add `CORR` for by name | 31 |
| OUTER UNION | `outer union corr` | Keeps all columns of both | 31 |
| Subquery | `where k in (select k from b)` | | 27 |
| Correlated subquery | `where x > (select avg(x) from t b where b.g = a.g)` | Also used for UPDATE from another table | 26 |
| CALCULATED | `calculated gst > 100` | SAS only: reuse an alias | 27 |
| INTO | `select count(*) into :n trimmed` | Creates macro variables | 50 |
| INSERT | `insert into t values (...) values (...)` | Several VALUES clauses, no commas; also `SET` form | 25 |
| UPDATE | `update t set c = ... where ...` | No `UPDATE ... FROM ... JOIN` | 26 |
| DELETE | `delete from t where ...` | Rows marked deleted; file not shrunk | 26 |
| CREATE TABLE | `create table t (a num, b char(10));` / `as select` / `like` | Only numeric and character types | 25 |
| ALTER TABLE | `alter table t add c num; modify c format=8.2; drop c;` | No RENAME COLUMN (use PROC DATASETS) | 26 |
| DROP TABLE | `drop table a, b;` | No TRUNCATE (use `delete from` or `obs=0`) | 26 |
| VIEW | `create view v as select ...` | `USING LIBNAME` for portable views | 32 |
| INDEX | `create index k on t(k);` | Simple index name must equal the column name | 32 |
| COALESCE | `coalesce(a, b)` | Works for numbers and text | 30 |
| Aggregates | `count(*) sum avg min max n nmiss std` | `sum(a, b)` with 2+ arguments is a row function | 29, 30 |
| Functions | Any DATA step function | `put`, `input`, `intck`, `intnx`, `catx` ... | 30 |
| Limit rows | `proc sql outobs=10;` | No TOP | 25 |
| Pass-through | `connect to ...; select * from connection to ...` | Native database SQL inside | 11 |

**PROC SQL or DATA step?**

| Prefer PROC SQL when | Prefer the DATA step when |
| --- | --- |
| Joining tables, especially many-to-many or on different key names | Reading raw files (INFILE/INPUT) |
| Summarising with GROUP BY | Row-by-row logic: RETAIN, LAG, FIRST./LAST. |
| Querying databases (pushdown) | Writing several outputs in one pass |
| Creating macro variables with INTO | Arrays and loops over columns |
| The team knows SQL well | Complex conditional logic per row |

## X.4 SQL ↔ SAS ↔ Pandas Cheat Sheet

**Syntax side by side**

| Concept | SAS | MS SQL Server | Python / Pandas |
| --- | --- | --- | --- |
| Read a table | `set lib.t;` | `SELECT * FROM t` | `df` |
| Choose columns | `keep=a b` | `SELECT a, b` | `df[["a", "b"]]` |
| Filter rows | `where a > 10;` | `WHERE a > 10` | `df[df["a"] > 10]` |
| New column | `c = a * b;` | `a * b AS c` | `df["c"] = df["a"] * df["b"]` |
| Rename | `rename=(a=x)` | `a AS x` | `rename(columns={"a": "x"})` |
| Sort | `proc sort; by a descending b;` | `ORDER BY a, b DESC` | `sort_values(["a","b"], ascending=[True, False])` |
| Remove duplicate keys | `proc sort nodupkey; by k;` | `ROW_NUMBER() ... = 1` | `drop_duplicates("k")` |
| Group totals | `proc summary nway; class g; var x; output out=o sum=;` | `GROUP BY g` | `groupby("g")["x"].sum()` |
| Join | `merge a(in=x) b(in=y); by k; if x and y;` | `INNER JOIN` | `merge(a, b, on="k")` |
| Left join | `if x;` after MERGE | `LEFT JOIN` | `merge(..., how="left")` |
| Stack | `set a b;` | `UNION ALL` | `pd.concat([a, b])` |
| Case logic | `if/else`, `select/when` | `CASE WHEN` | `np.select` |
| Missing value | `.` and blank; `missing(x)` | `NULL`; `IS NULL` | `NaN`; `isna()` |
| Replace missing | `coalesce(a, 0)` | `COALESCE(a, 0)` | `fillna(0)` |
| Running total | `total + x;` with BY reset | `SUM(x) OVER (PARTITION BY ... ORDER BY ...)` | `groupby().cumsum()` |
| Previous row | `lag(x)` | `LAG(x) OVER (...)` | `shift(1)` |
| First / last per group | `first.g` / `last.g` | `ROW_NUMBER()` | `groupby().head(1)` / `tail(1)` |
| Rank | `proc rank ties=dense;` | `DENSE_RANK()` | `rank(method="dense")` |
| Pivot | `proc transpose; by id; id col; var v;` | `PIVOT` | `pivot_table()` |
| Unpivot | `proc transpose` (wide to long) | `UNPIVOT` | `melt()` |
| Display format | `format x comma12.;` | `FORMAT(x, 'N0')` | `"{:,.0f}".format` |
| Parameter | `%let x = 10;` → `&x` | `DECLARE @x` | `x = 10` |
| Reusable code | `%macro ... %mend;` | Stored procedure | `def` function |

**Traps and interview tips**

| Concept | Common mistake | Interview tip |
| --- | --- | --- |
| Filter | IF on a variable that WHERE could filter | Explain WHERE vs IF with the PDV |
| Missing values | Forgetting missing is lowest in SAS | Contrast with SQL NULL logic |
| Sort | Forgetting OUT= | Mention sort cost and CLASS as an alternative |
| Duplicates | NODUPRECS without `BY _ALL_` | NODUPKEY vs NODUPRECS |
| Join | Many-to-many MERGE | MERGE vs JOIN, and IN= flags |
| Stack | Different lengths across datasets | LENGTH before SET; PROC APPEND for speed |
| Group totals | Forgetting NWAY | `_TYPE_` and `_FREQ_` |
| Running total | Not resetting at FIRST. | RETAIN vs sum statement |
| Previous row | LAG inside IF | LAG is a queue, not "previous row" |
| Rank | Default TIES=MEAN gives 3.5 | Map TIES= options to SQL RANK and DENSE_RANK |
| Pivot | Duplicate ID values | BY / ID / VAR roles |
| Format | Thinking it changes the stored value | Format vs informat |
| Macro variables | Single quotes | Compile time vs execution time (CALL SYMPUT) |
| Macros | `%IF` on data values | `%IF` vs `IF` |
| Dates | Mixing dates and datetimes | Days since 1960 vs seconds since 1960 |
| SQL | Expecting TOP, window functions, TRUNCATE | Differences between PROC SQL and T-SQL |

### Modern SAS awareness

| Older practice | Current practice |
| --- | --- |
| SAS University Edition | SAS OnDemand for Academics (SAS Studio in the browser) |
| SAS/GRAPH `GCHART` and `GPLOT` | ODS Graphics: `SGPLOT`, `SGPANEL` |
| `RANUNI` | `RAND` with `CALL STREAMINIT` |
| `MONOTONIC()` for row numbers | DATA step `_N_` or a counter |
| `CALL SYMPUT` | `CALL SYMPUTX` |
| Plain-text passwords | Authentication domains or encoded passwords |
| Desktop SAS for production | Server-based SAS 9.4 or SAS Viya, run by schedulers |
| Only SAS code | SAS Viya runs SAS, Python and R side by side |

---

# Part XI — Interview Preparation

## XI.1 How to Answer a SAS Interview Question

A strong answer has four short parts:

1. **The concept** in one or two sentences.
2. **A small example** (a few rows, or one line of code).
3. **The trade-off** or trap ("but with many-to-many keys...").
4. **A production note** ("on 100 million rows I would...").

Interviewers in banks care about correctness first, then whether you understand *why* SAS behaves the
way it does, then whether you have thought about scale and production.

## XI.2 SAS Concepts Interviewers Compare with SQL

| Pair | The subtle difference to explain |
| --- | --- |
| **WHERE vs HAVING** | WHERE filters rows before grouping; HAVING filters groups. In PROC SQL, HAVING can use `CALCULATED` aliases; HAVING without GROUP BY treats the table as one group. |
| **IF vs WHERE** | A DATA step question, not SQL: WHERE acts before the PDV and cannot see new variables; subsetting IF acts after and can (Module 16). |
| **SET vs JOIN** | `SET a b;` **stacks** rows (like UNION ALL). It does not join. Joining in the DATA step is `MERGE`. |
| **MERGE vs JOIN** | MERGE needs sorted data, matches many-to-many row by row (not a Cartesian product), and later datasets overwrite same-named columns. SQL joins need no sort and produce every combination. |
| **PROC SORT vs ORDER BY** | PROC SORT rewrites the dataset in sorted order and records that order; ORDER BY only orders one query's result. PROC SORT can also remove duplicates (NODUPKEY). |
| **FIRST./LAST. vs window functions** | FIRST./LAST. are flags produced while reading sorted rows one by one; one DATA step can compute running totals, previous values and group totals together. SQL needs a window function for each. |
| **PROC SUMMARY vs GROUP BY** | PROC SUMMARY gives every level of subtotal in one pass (`_TYPE_`) plus medians and percentiles; GROUP BY gives one level (ROLLUP/CUBE for more). |
| **PROC RANK vs RANK / DENSE_RANK** | `TIES=LOW` matches `RANK()`, `TIES=DENSE` matches `DENSE_RANK()`, the default `TIES=MEAN` has no SQL equivalent. `GROUPS=` is like `NTILE` but keeps tied values together. |
| **RETAIN vs window logic** | RETAIN carries a value from row to row (state); `SUM() OVER (ORDER BY ...)` declares the result for each row. |
| **PROC TRANSPOSE vs PIVOT** | PIVOT needs the column list written out and an aggregate; PROC TRANSPOSE finds the columns from the data, but fails on duplicate ID values unless they are summarised first. |
| **SAS missing vs SQL NULL** | A SAS missing number is a real value that is **lower than any number** (`. < 0` is true). SQL NULL comparisons are unknown (the row drops out). A blank text value **is** missing in SAS, but `''` is not NULL in SQL Server. Both are ignored by aggregates. |
| **SAS FORMAT vs SQL formatting** | A SAS format is an attribute stored with the column and used by every procedure for display **and grouping**; the value is unchanged. SQL `FORMAT()` returns a new text value. |

## XI.3 Interview Question Bank

Each answer is the core of a strong reply. The module number points to the full explanation and
example.

### Basic

**B1. What is SAS and what are its main components?** *(Module 1)*
- *Testing:* overview. *Answer:* an analytics suite and language; Base SAS (DATA step, PROC SQL,
  macros, core procedures), SAS/STAT, SAS/ACCESS, SAS/CONNECT; interfaces such as Enterprise Guide and
  SAS Studio; the modern platform is SAS Viya. *Follow-up:* "Which interface have you used?"

**B2. DATA step vs PROC step?** *(Module 3)*
- *Answer:* DATA steps create or change datasets row by row through the PDV; PROC steps run ready-made
  procedures on datasets. *Follow-up:* "Which procedures end with QUIT?"

**B3. What is a library? WORK vs a permanent library?** *(Module 4)*
- *Answer:* a named location (folder or database) assigned with LIBNAME. WORK is deleted at the end of
  the session; permanent librefs point to folders that persist. One-level names mean WORK.

**B4. What data types does SAS have, and how are dates stored?** *(Modules 4, 23)*
- *Answer:* numeric and character only. Dates are numbers of days since 1 January 1960; datetimes are
  seconds since then; formats control display.

**B5. What does the SET statement do?** *(Module 5)*
- *Answer:* reads observations from SAS datasets into the PDV one at a time; several datasets are
  stacked; with BY they are interleaved; options include WHERE=, END=, NOBS= and POINT=.

**B6. KEEP statement vs KEEP= option?** *(Module 13)*
- *Answer:* the statement affects all outputs; the option affects one dataset and, on input, limits
  what is read into the PDV (faster). Order on input: DROP/KEEP, then RENAME, then WHERE.

**B7. Format vs informat?** *(Module 19)*
- *Answer:* an informat reads text into a value; a format displays a value. The stored value never
  changes.

**B8. How do you read a CSV file?** *(Modules 8, 10)*
- *Answer:* in production, INFILE with `DLM=',' DSD FIRSTOBS=2 TRUNCOVER` and INPUT with LENGTH and
  informats; for quick work, PROC IMPORT with `GUESSINGROWS=MAX`.

### Intermediate

**I1. Explain the PDV.** *(Module 7)*
- *Answer:* the one-row memory area built at compile time with every variable plus `_N_` and
  `_ERROR_`; at each iteration non-retained variables are reset, a row is read, statements run and the
  PDV is written out.

**I2. WHERE vs IF?** *(Module 16)*
- *Answer:* WHERE filters before the PDV (faster, indexes, special operators, works in PROCs, cannot use
  new variables); IF filters after (new variables, `_N_`, FIRST./LAST., IN=, raw data).

**I3. NODUPKEY vs NODUPRECS?** *(Module 18)*
- *Answer:* NODUPKEY removes duplicate BY values; NODUPRECS removes rows identical to the previous row,
  so sort BY _ALL_ to catch every duplicate.

**I4. MISSOVER vs TRUNCOVER, and what does DSD do?** *(Module 8)*
- *Answer:* both stop SAS jumping to the next line; MISSOVER blanks a partial value, TRUNCOVER keeps it.
  DSD treats consecutive delimiters as missing, removes quotes and allows delimiters inside quotes.

**I5. @ vs @@?** *(Module 9)*
- *Answer:* both hold the input line; `@` until the end of the current iteration, `@@` across
  iterations (several records per line).

**I6. SUM() vs the + operator?** *(Module 22)*
- *Answer:* + returns missing if any value is missing; SUM ignores missing values. Remember `OF` for
  variable lists.

**I7. INTCK vs INTNX?** *(Module 23)*
- *Answer:* INTCK counts interval boundaries between two dates (`'c'` for complete periods); INTNX
  moves a date by intervals with B/M/E/S alignment.

**I8. PROC MEANS vs PROC SUMMARY, and what is `_TYPE_`?** *(Module 41)*
- *Answer:* same engine; MEANS prints by default, SUMMARY needs OUTPUT. `_TYPE_` identifies the level
  of summary (0 = overall); NWAY keeps only the most detailed level.

### Advanced

**A1. MERGE vs SQL join, especially many-to-many?** *(Module 33)*
- *Answer:* MERGE needs sorted data and matches row by row within a key, so many-to-many gives wrong
  results (with a NOTE); SQL gives the Cartesian product per key. Same-named columns are overwritten in
  MERGE. Use IN= for join types.

**A2. Running total per customer, and one row per customer with the total?** *(Module 34)*
- *Answer:* sort by customer; `if first.cust_id then total = 0; total + amount;` for the running total;
  add `if last.cust_id then output;` for one row per customer.

**A3. Why can LAG give the wrong previous value?** *(Module 22)*
- *Answer:* LAG is a queue updated only when it executes; inside IF it skips rows. Call it on every row,
  then use the result conditionally, and reset at FIRST.

**A4. Why can't a CALL SYMPUT variable be used in the same step?** *(Module 50)*
- *Answer:* `&` references resolve at compile time; CALL SYMPUT runs at execution. Use SYMGET in the
  same step, or `&` in a later step. Prefer SYMPUTX.

**A5. %IF vs IF; how does %IF compare decimals?** *(Module 51)*
- *Answer:* %IF decides which code is generated, before execution, and sees only macro variables; IF
  acts on each row. %EVAL compares decimals as text, so use %SYSEVALF.

**A6. Explain macro quoting.** *(Module 52)*
- *Answer:* %STR / %NRSTR quote text you type (compile time; NRSTR also hides & and %); %BQUOTE /
  %SUPERQ quote resolved values from data (execution time); %SUPERQ never resolves the value.

**A7. Global vs local macro variables?** *(Module 48)*
- *Answer:* global for the session, local for a macro's run; `%let` inside a macro updates the nearest
  existing variable, so declare internal ones with %LOCAL.

**A8. What is a hash object and when would you use it instead of MERGE?** *(Module 33)*
- *Answer:* an in-memory lookup table loaded inside a DATA step; no sorting needed; ideal for looking up
  a small or medium table (watch lists, rates) from a large one.

### Scenario-based

**S1. You need the latest record per customer from 50 million rows.**
- *Approach:* `keep=` only the needed columns; sort by customer and descending timestamp (or by
  customer and timestamp and use `if last.`); PROC SORT NODUPKEY with DUPOUT= for audit. If the data is
  in a database, use `ROW_NUMBER()` in explicit pass-through and bring back only the result.

**S2. Two systems disagree on account balances. How do you reconcile them?**
- *Approach:* full join on account number with COALESCE on the key; classify only-in-A, only-in-B and
  both-but-different (with a tolerance); summarise counts and amounts per category; report and keep
  the detail. PROC COMPARE with ID for a value-by-value report.

**S3. A daily report must run with nobody watching.**
- *Approach:* macro with a run-date parameter from `-sysparm`; batch mode started by the scheduler;
  dated log; `&SYSERR` checks; DQ checks before reporting; non-zero exit on failure; email on
  completion (Module 55).

**S4. Flag customers with 3 or more transactions within 10 minutes.**
- *Approach:* sort by customer and datetime; RETAIN the previous two timestamps, reset at FIRST.;
  flag when the current time minus the time two transactions ago is at most 600 seconds (Module 34).

**S5. A source file has a trailer record with a row count and an amount total.**
- *Approach:* read with a trailing `@` to separate detail and trailer records; compare the loaded count
  and total with the trailer; stop the job if they differ (Modules 9, 58).

**S6. Split a 100-million-row dataset into one file per region.**
- *Approach:* get the region list with INTO; generate one DATA step with a multi-dataset DATA statement
  and `OUTPUT` per region, so the big table is read once (not once per region).

### Debugging

**D1. Many rows show missing values for a new variable, and the Log says "uninitialized".**
- *Cause:* a misspelt variable name, or a variable dropped on input. *Fix:* check PROC CONTENTS; fix the
  name.

**D2. The Log says "MERGE statement has more than one data set with repeats of BY values".**
- *Cause:* duplicate keys on both sides. *Fix:* deduplicate or use PROC SQL; never ignore it.

**D3. "Character values have been converted to numeric values".**
- *Cause:* text used in arithmetic. *Fix:* INPUT with an informat; check for invalid values.

**D4. "Apparent symbolic reference X not resolved".**
- *Cause:* typo, scope, CALL SYMPUT timing or single quotes. *Fix:* check each in that order; use %PUT
  _USER_.

**D5. "A lock is not available".**
- *Cause:* the dataset is open elsewhere. *Fix:* close it or wait; use `FILELOCKWAIT=`; schedule jobs so
  they do not collide.

### Performance

**P1. How do you speed up a slow job?** *(Module 57)* — Measure with FULLSTIMER, then move less data:
KEEP= and WHERE on input, filter early, avoid sorts, hash lookups, one pass with many outputs, PROC
APPEND, pushdown to the database.

**P2. When does an index help?** *(Module 32)* — For selective WHERE clauses and joins on large tables;
not for reading most of a table or for columns with few distinct values.

**P3. How do you avoid sorting?** *(Modules 18, 41)* — CLASS instead of BY; SQL GROUP BY; hash objects;
keep data sorted once; check the sort flag.

**P4. Implicit vs explicit pass-through?** *(Module 11)* — Implicit lets SAS translate a query for the
database when it can; explicit sends native SQL. Check with SASTRACE; use explicit for heavy work.

**P5. PROC APPEND vs SET to add rows?** *(Module 31)* — APPEND reads only the new data and adds it to the
end; SET rewrites the whole table.

## XI.4 Predict the Output

Try each one before reading the answers below. `work.txn` is the dataset from Module 5.

**Q1.**
```sas
data a;
    x = 10;
    y = x + .;
    z = sum(x, .);
run;
```

**Q2.** How many rows, and what is `i`?
```sas
data a;
    do i = 1 to 3;
    end;
run;
```

**Q3.**
```sas
data a;
    input name $;
    datalines;
Chandrashekhar
;
run;
```

**Q4.** Which rows?
```sas
data a;
    set work.txn(firstobs=3 obs=5);
run;
```

**Q5.** How many rows get `small = 1`?
```sas
data a;
    set work.txn;
    if amount < 10000 then small = 1;
run;
```

**Q6.**
```sas
data a;
    length flag $3;
    set work.txn;
    if amount > 50000 then flag = 'HIGH';
run;
```

**Q7.** Dataset `a` has 2 rows with key X; dataset `b` has 3 rows with key X. How many rows does
`merge a b; by key;` produce? How many does a PROC SQL inner join on `key` produce?

**Q8.**
```sas
%let x = 5 + 5;
%put &x;
%put %eval(&x);
```

**Q9.** (No macro variable `v` exists before this step.)
```sas
data _null_;
    call symputx('v', 'hello');
    put "&v";
run;
```

**Q10.**
```sas
data a;
    set work.txn;
    where channel = 'ONLINE';
    n + 1;
run;
```

**Q11.**
```sas
data a;
    input x @@;
    if x > 2 then y = lag(x);
    datalines;
1 5 2 7 9
;
run;
```

**Q12.** What is `r`?
```sas
data a;
    r = 7 / 2;
run;
```

### Answers

| Q | Answer | Why |
| --- | --- | --- |
| 1 | `y = .`, `z = 10` | `+` with a missing value gives missing (and a NOTE); SUM ignores missing |
| 2 | 1 row, `i = 4` | The DATA step runs once; the loop ends when `i` passes 3 |
| 3 | `Chandras` | List input gives text a length of 8 unless you set LENGTH |
| 4 | T003, T004, T005 (3 rows) | `OBS=5` is the last row number |
| 5 | 3 rows: T001, T003, T004 | T004's missing amount is lower than 10,000 |
| 6 | `HIG` for T002 and T006; blank for the rest | LENGTH fixed `flag` at 3 characters |
| 7 | MERGE: 3 rows; SQL: 6 rows | MERGE matches row by row; SQL forms every combination |
| 8 | `5 + 5`, then `10` | %LET stores text; %EVAL calculates |
| 9 | A warning that `V` is not resolved, and the text `&v` is written | `&v` resolved at compile time, before CALL SYMPUTX ran |
| 10 | 3 rows; `n` = 1, 2, 3 | WHERE rows never enter the step, and the sum statement counts the rest |
| 11 | `y` = ., ., ., 5, 7 | LAG runs only when `x > 2` (for 5, 7, 9), so it returns the previous **qualifying** value |
| 12 | 3.5 | SAS division is not integer division (SQL Server gives 3 for `7/2`) |

---

# Part XII — Capstone Project, Career and Study Modes

## XII.1 End-to-End Capstone Project: Card and UPI Fraud Analytics

This is the design for one resume-ready project that uses the whole course. It covers all 27 items
listed in section 19 of your prompt. Build it with **synthetic data** (generated with DATA step loops
and `RAND`), never with real customer data.

### 1. Business requirement

A retail bank with about 5 million customers processes about 10 million card and UPI transactions a
day. Fraud losses are rising. The bank needs a daily SAS process that:

- loads and validates the day's transactions,
- applies fraud rules and produces an alert queue for investigators,
- tracks fraud losses and rule performance, and
- produces daily and monthly management reports.

### 2. Stakeholder requirements

| Stakeholder | Needs |
| --- | --- |
| Fraud operations | Alert list by 07:00 every day, ranked by risk, with the reason for each alert |
| Risk management | Monthly fraud-loss trend by channel and merchant category; rule performance |
| Compliance | Evidence of controls: data-quality results, run logs, reproducible reruns |
| IT / production support | A job that runs unattended, fails safely and alerts on problems |

### 3. Source systems

| Source | Format | Read with |
| --- | --- | --- |
| Core banking: customers and accounts | Oracle tables | `LIBNAME ORACLE`, explicit pass-through (Module 11) |
| Card switch: authorisations | Fixed-width text file with a trailer record | `INFILE` / `INPUT`, trailing `@` (Modules 8–9) |
| UPI switch: transactions | Pipe-delimited file with a header | `INFILE ... DLM='\|' DSD` (Module 8) |
| Merchant master | SQL Server table | `LIBNAME ODBC` (Module 11) |
| Watch list from compliance | Excel workbook | `LIBNAME XLSX` (Module 10) |
| Confirmed fraud cases | CSV from the case-management system | `INFILE` / `INPUT` (Module 8) |

### 4. Raw datasets

| Dataset | Grain (one row per) |
| --- | --- |
| `raw.customers` | Customer |
| `raw.accounts` | Account |
| `raw.card_auth_YYYYMMDD` | Card authorisation |
| `raw.upi_txn_YYYYMMDD` | UPI transaction |
| `raw.merchants` | Merchant |
| `raw.watchlist` | Watch-listed customer or card |
| `raw.fraud_confirmed` | Confirmed fraud transaction |

### 5. Data dictionary (key fields)

| Field | Type / length | Format | Description | Rule |
| --- | --- | --- | --- | --- |
| `txn_id` | Char 20 | | Unique transaction ID | Not missing; unique per day |
| `cust_id` | Char 10 | | Customer ID | Must exist in `raw.customers` |
| `card_no_masked` | Char 16 | | Card number with only the last 4 digits visible | Never store the full number in reports |
| `txn_dt` | Numeric 8 | `DATETIME20.` | Transaction date and time | Not in the future |
| `amount` | Numeric 8 | `COMMA14.2` | Amount in rupees | Greater than 0 |
| `channel` | Char 6 | | POS, ONLINE, ATM, UPI | From the allowed list |
| `merchant_id` | Char 15 | | Merchant ID | Must exist in the merchant master (except ATM) |
| `city` | Char 30 | | Transaction city | Standardised spelling |
| `fraud_flag` | Numeric 3 | | 1 = confirmed fraud | 0 or 1 |

### 6–9. Ingestion, validation, cleaning and transformation

- **Ingestion:** DATA steps with explicit LENGTH and informats; no PROC IMPORT in production.
- **Validation:** control totals against the card file's trailer; DQ checks (missing keys, duplicates,
  invalid codes, future dates, orphans); rejected rows kept with a reason code (Module 58).
- **Cleaning:** standardise city and merchant names (Module 21); mask card numbers (Module 24).
- **Transformation:** hour of day, weekday, night flag, amount band, customer's 90-day average amount,
  days since the previous transaction (Modules 23 and 34).

### 10–20. Core SAS techniques used

| Technique | Where it is used in the project |
| --- | --- |
| DATA steps | Loading, cleaning, rules engine, multiple outputs in one pass |
| PROC SQL | Customer and merchant summaries, joins to the merchant master, INTO for macro lists |
| SAS functions | Text cleaning, masking, date arithmetic, LAG |
| BY-group processing | Per-card velocity rules |
| RETAIN | Previous transaction times and cities per card |
| FIRST./LAST. | Reset per card; first and last transaction of the day |
| PROC SORT | By card and datetime; NODUPKEY for duplicate transaction IDs |
| PROC SUMMARY / MEANS | Daily totals per customer, merchant and channel |
| PROC FREQ | DQ checks; fraud rate by channel and merchant category |
| PROC REPORT | Daily alert report and management summary |
| PROC TRANSPOSE | Monthly loss matrix: channels as rows, months as columns |

**Fraud rules (examples)**

| Rule | Logic |
| --- | --- |
| R1 Velocity | 3 or more transactions on one card within 10 minutes |
| R2 Amount spike | Amount more than 5 times the customer's 90-day average |
| R3 Impossible travel | Two different cities on the same card within 60 minutes |
| R4 Night high value | ONLINE, between 00:00 and 05:00, amount over ₹50,000 |
| R5 Watch list | Customer or card on the compliance watch list (hash lookup) |

### 21–24. Automation, error handling, logging and performance

- **Macro automation:** `%daily_fraud(run_date=)` driven by `-sysparm`; region and channel lists from
  data with INTO; month-end branch with %IF (Modules 47–55).
- **Error handling:** `%check_step` after every step; `OPTIONS ERRORABEND`; stop on control-total
  mismatch.
- **Logging:** a dated log per run; `%scan_log`; a job-status table with start, end, row counts and
  status.
- **Performance:** `keep=` and WHERE on input; hash lookup for the watch list; pass-through for Oracle;
  one pass with several outputs; PROC APPEND to the history table; measured with FULLSTIMER.

### 25. Final reporting datasets

| Dataset | Grain | Used by |
| --- | --- | --- |
| `rpt.fraud_alerts_daily` | Alert (transaction + rule) | Fraud operations queue |
| `rpt.fraud_daily_summary` | Day × channel | Daily report, dashboards |
| `rpt.fraud_monthly_matrix` | Channel × month | Risk management pack |
| `rpt.rule_performance` | Rule × month | Rule tuning |
| `rpt.dq_results` | Check × run date | Compliance evidence |

### 26. Business KPIs

| KPI | Definition |
| --- | --- |
| Alert volume | Number of alerts raised per day |
| Alert rate | Alerts ÷ transactions |
| Precision (hit rate) | Alerts later confirmed as fraud ÷ all alerts |
| Detection rate (recall) | Confirmed fraud transactions that were alerted ÷ all confirmed fraud transactions |
| False-positive ratio | Non-fraud alerts ÷ fraud alerts |
| Fraud loss | Total amount of confirmed fraud |
| Fraud loss rate (basis points) | Fraud loss ÷ total transaction value × 10,000 |
| Average detection time | Average hours from transaction to alert |
| Top merchants and channels | Ranked by fraud loss and fraud rate (PROC RANK) |

### 27. Executive summary (template)

Write this with **your own results** from the synthetic data. Do not copy these placeholders as if they
were real findings.

> **Daily fraud monitoring: month of <month>**
> The process ran on <n> of <n> business days, with all data-quality controls passed on <n> days.
> <n> alerts were raised (alert rate <x>%), of which <x>% were confirmed fraud. Rules R1 and R5
> produced the highest precision; R2 produced the most false positives and is recommended for
> re-tuning. Fraud loss was ₹<amount> (<x> bps of transaction value), concentrated in <channel> and
> merchant category <category>. Recommended actions: <1–3 actions>.

### Project folder structure

```text
sas-fraud-analytics/
    README.md                  what it does, how to run it, results
    config/setup.sas           librefs, options, sasautos, fmtsearch
    macros/                    one file per macro (autocall)
        set_run_date.sas  check_step.sas  dq_check.sas  scan_log.sas  daily_fraud.sas
    jobs/
        00_generate_synthetic_data.sas
        01_load.sas  02_validate.sas  03_transform.sas  04_rules.sas  05_report.sas
    run/run_daily_fraud.sh     batch script for the scheduler
    docs/data_dictionary.md    the table above, expanded
    output/                    sample reports produced from synthetic data
```

## XII.2 Career Guidance: Where SAS Fits

### SAS in a modern analytics stack

| Tool | Best at | Weaker at | Typical use in a bank |
| --- | --- | --- | --- |
| **SAS** | Validated, auditable processing of large data on disk; statistics; regulated models; mature scheduling | Licence cost; smaller open-source community; fewer modern machine-learning libraries | Risk models, regulatory reporting, fraud and AML batch processing |
| **SQL** | Querying and transforming data where it lives | Row-by-row logic, statistics, reporting | Data warehouses, marts, pushdown from SAS and Python |
| **Python** | Flexibility, machine learning, automation, free | Governance and validation take more effort | Modern data science, model development, APIs |
| **Pandas** | Fast in-memory analysis | Data bigger than memory | Exploration, feature engineering, prototypes |
| **Power BI** | Interactive dashboards | Heavy data processing | Management dashboards fed by SQL or SAS marts |
| **Excel** | Quick ad hoc analysis everyone can open | Scale, auditability | Business review, small reconciliations |

### When and why companies use SAS

- **Banks and insurers** use SAS because decades of risk, fraud and regulatory code run on it,
  regulators are familiar with it, and its outputs are reproducible and auditable.
- **SAS is stronger than Python** for: validated procedures with documented algorithms, very large
  row-by-row processing on disk without memory limits, built-in enterprise scheduling and metadata, and
  vendor support.
- **Python is stronger than SAS** for: modern machine learning, open-source libraries, cost, APIs and
  integration with cloud tools.
- **SQL fits** underneath both: data lives in databases, and good SAS and Python code pushes filtering
  and aggregation to SQL.
- **Integration:** SAS reads and writes databases through SAS/ACCESS, performs ETL in DATA steps and
  PROC SQL (or SAS Data Integration Studio), reports through ODS and Visual Analytics, and feeds marts
  that Power BI reads. SAS Viya runs SAS, Python and R side by side.
- **In risk and fraud analytics** SAS typically handles: credit scorecards and IFRS 9 / Basel models,
  daily fraud rules and alert queues, AML transaction monitoring, and regulatory returns.

### The SAS skills interviewers value most

1. DATA step logic and the PDV
2. PROC SQL, and knowing when to use it instead of the DATA step
3. BY-group processing: RETAIN, FIRST./LAST., LAG
4. MERGE vs JOIN, and lookups with hash objects or formats
5. Macros: parameters, INTO, CALL SYMPUTX, %DO, %IF, quoting and debugging
6. Core procedures: SORT, MEANS/SUMMARY, FREQ, REPORT, TRANSPOSE
7. Dates: INTCK, INTNX, and date vs datetime
8. Data quality and reconciliation
9. Performance and database pushdown
10. Production awareness: batch, scheduling, logs, error handling

**Certifications:** the standard ones are *SAS Certified Specialist: Base Programming Using SAS 9.4*
and *SAS Certified Professional: Advanced Programming Using SAS 9.4*. Check the SAS website for the
current names and exam content before booking.

## XII.3 Showing Your SAS Skills Honestly: Resume, LinkedIn, GitHub, Interviews

📌 **Do not exaggerate.** If you have not used SAS in a job, present it as **training and project
work**, not as work experience. Interviewers in banks check, and a single false claim can end an
interview.

### Resume (Projects or Skills section)

Good, honest examples (replace the numbers with your own measured results):

- *"Built an end-to-end SAS fraud-analytics project on 10 million synthetic card transactions using
  Base SAS, PROC SQL and macros: fixed-width file ingestion, data-quality checks with control totals,
  BY-group velocity rules, and automated PROC REPORT and ODS Excel outputs."*
- *"Automated a parameterised monthly risk report with SAS macros (INTO, CALL SYMPUTX, %DO loops),
  batch execution with run-date parameters, dated logs and return-code checks."*
- *"Reduced the project's run time from <X> to <Y> minutes by reading only required columns, replacing
  sort-and-merge lookups with hash objects, and using PROC APPEND for history tables."*

**Skills line:** `SAS (Base SAS, PROC SQL, Macros, ODS) — project experience` next to your real work
skills (SQL Server, Python, Pandas, Power BI).

❌ Avoid: "Expert in SAS", "5 years of SAS", or listing SAS under a job where you did not use it.

### LinkedIn

- **Headline:** *Data Analyst | SQL Server, Python, Power BI | Building SAS skills for banking and risk
  analytics*
- **About:** two or three sentences on your current work, then one sentence on the SAS projects and what
  they demonstrate, with a link to GitHub.
- **Featured:** the capstone README and a screenshot of a report produced from synthetic data.

### GitHub portfolio

- Use the folder structure above.
- Include only **synthetic** data and the program that generates it.
- The README should explain the business problem, the pipeline, the fraud rules, how to run it in SAS
  OnDemand for Academics, and the results.
- Never include real customer data, company code, server names or credentials.

### In interviews

Use honest framing: *"In my capstone project I processed 10 million synthetic transactions. The
velocity rule used RETAIN and FIRST.card_no after sorting by card and time. The first version took
<X> minutes; I measured it with FULLSTIMER and cut it to <Y> by..."* Specific, true details are far
more convincing than broad claims.

## XII.4 Study Modes

If you work through these notes with an AI mentor, these commands (from sections 39–43 of your prompt)
change how it responds:

| Say | You get |
| --- | --- |
| **NEXT** | The next module, after you finish the current one |
| **QUIZ** | MCQs, output prediction, debugging, code writing, SQL-to-SAS and Python-to-SAS conversion and scenarios, based only on modules you have finished; answers only after you submit yours |
| **INTERVIEW MODE** | One question at a time, scored out of 10, with corrections, an ideal answer and a harder follow-up |
| **REVISION** | A short but deep recap: key concepts, syntax, differences, mistakes, interview questions, code snippets and memory tricks |
| **CHEAT SHEET** | A structured reference with SAS syntax, MS SQL Server and Pandas equivalents, common mistakes and interview tips (Part X has one) |

### How your exercise answers are evaluated

When you submit an exercise solution, it is reviewed in seven steps:

1. Evaluate whether it works.
2. Identify the mistakes.
3. Explain why each mistake happened.
4. Give the corrected solution.
5. Give a better or faster solution if one exists.
6. Rate the answer from 0 to 10.
7. Say what to improve next.

## XII.5 Progress Tracker

Track each Part here, and each syllabus item in [section 0.7](#07-module-wise-topic-mapping-your-complete-syllabus-checklist).

| Part | Modules | Mini project | Status |
| --- | --- | --- | --- |
| I — Getting started | 1–7 | | ○ |
| II — Data in and out | 8–12 | | ○ |
| III — Core DATA step | 13–20 | Mini Project 1 | ○ |
| IV — Functions | 21–24 | | ○ |
| V — PROC SQL | 25–32 | Mini Project 2 | ○ |
| VI — Advanced DATA step | 33–39 | Mini Project 3 | ○ |
| VII — Reporting | 40–46 | | ○ |
| VIII — Macros and automation | 47–55 | Mini Project 4 | ○ |
| IX — Production skills | 56–59 | | ○ |
| X — Master references | — | | ○ |
| XI — Interview preparation | — | | ○ |
| XII — Capstone project | — | Capstone | ○ |

Legend: ✓ Completed · ◐ In progress · ○ Not started

---

**Where this came from:** the syllabus in `SAS_Contents.txt` and the teaching requirements in
`Promt.txt`. Every one of the 151 syllabus items is covered (see section 0.7). Code examples are
complete programs; anything that connects to external systems (databases, servers, Hadoop, email)
needs your organisation's connection details.
