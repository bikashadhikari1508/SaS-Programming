# SAS (Statistical Analysis System) — Complete Learning Guide
### Sessions 1–8, explained in simple language

---

## Table of Contents

1. [Title and Scope](#1-title-and-scope)
2. [SAS Fundamentals and the SQL / Python / Excel Comparison](#2-sas-fundamentals-and-the-sql--python--excel-comparison)
3. [Session-wise Syllabus (Sessions 1–8)](#3-session-wise-syllabus)
   - [Session 1 — SAS Fundamentals and Data Import](#session-1--sas-fundamentals-and-data-import)
   - [Session 2 — Data Step Manipulation and Formats](#session-2--data-step-manipulation-and-formats)
   - [Session 3 — Data Input, Output and PDV](#session-3--data-input-output-and-pdv)
   - [Session 4 — Joins, Merging, Data Modeling and PROC SQL](#session-4--joins-merging-data-modeling-and-proc-sql)
   - [Session 5 — Transpose, RETAIN, Ranking, Loops and Arrays](#session-5--transpose-retain-ranking-loops-and-arrays)
   - [Session 6 — SAS Functions and Summary Reporting](#session-6--sas-functions-and-summary-reporting)
   - [Session 7 — PROC SQL Programming](#session-7--proc-sql-programming)
   - [Session 8 — SAS Macros and Automation](#session-8--sas-macros-and-automation)
4. [Essential SAS Syntax and Keyword Cheat Sheet](#4-essential-sas-syntax-and-keyword-cheat-sheet)
5. [DATA Step versus PROC Step](#5-data-step-versus-proc-step)
6. [SAS Functions Master Reference](#6-sas-functions-master-reference)
7. [SAS Data Import / Export Reference](#7-sas-data-import--export-reference)
8. [Decision Guide: DATA Step, PROC SORT, PROC SQL or Macro?](#8-decision-guide)
9. [Common SAS Errors and Troubleshooting](#9-common-sas-errors-and-troubleshooting)
10. [High-Priority Interview Questions](#10-high-priority-sas-interview-questions-with-concise-answers)
11. [Final Revision Checklist](#11-final-revision-checklist)

---

## 1. Title and Scope

**SAS** stands for **Statistical Analysis System**. It is software for reading data, cleaning it, analysing it and producing reports. Banks, hospitals, insurers and pharma companies use it because it handles large data reliably and its results are trusted.

**What this guide teaches**

- How to bring data into SAS (inline text, text/CSV files, Excel, databases)
- How to clean, filter, sort, combine and summarise data
- How to use functions, `PROC SQL` and macros to save time
- How to answer common SAS interview questions

**How each topic is written**

| Part | Meaning |
|---|---|
| **In simple words** | An everyday explanation first |
| **Definition / Purpose** | What it is and when to use it |
| **Syntax** | The pattern to type |
| **Example + Expected output** | A small program and what you should see |
| **Important rules** | Common mistakes, limits |
| **Comparison** | SQL / Python / Excel, only where it helps |
| **Interview takeaway** | Only for commonly asked topics |

**A note about environments.** SAS is sold in pieces. Some features need extra licensed products. This guide marks them like this:

| Tag | Meaning |
|---|---|
| ✅ **Base SAS** | Available in every normal SAS installation |
| 🔑 **Needs licence** | Needs another product, e.g. SAS/STAT, SAS/ACCESS, SAS/CONNECT |
| 🌐 **Environment-dependent** | Depends on how your company set SAS up (operating system, version, Viya, server rules) |

**A note about the code.** File paths such as `/home/user/data` are placeholders. Replace them with your own folders. Passwords are never typed in code in this guide; use placeholders or your company's secure method.

---

## 2. SAS Fundamentals and the SQL / Python / Excel Comparison

### 2.1 SAS in one picture

Think of SAS as an **Excel workbook you control by writing instructions instead of clicking**.

```
 Raw data  ──►  DATA step (build / change the table)  ──►  PROC steps (report / analyse)  ──►  Output
 (file, DB)         "cook the ingredients"                      "serve the dish"
```

### 2.2 Main SAS components (simple view)

| Component | In plain words | Tag |
|---|---|---|
| **Base SAS** | The language itself: DATA step, `PROC SORT`, `PROC PRINT`, `PROC MEANS`, `PROC SQL`, macros, ODS | ✅ |
| **SAS/STAT** | Advanced statistics (regression, survey sampling such as `PROC SURVEYSELECT`) | 🔑 |
| **SAS/GRAPH** | Older graphics (`PROC GCHART`). Newer `PROC SGPLOT` is in Base SAS | 🔑 |
| **SAS/ACCESS** | Connectors to databases (Oracle, SQL Server, Hadoop) and to Excel/Access (PC Files) | 🔑 |
| **SAS/CONNECT** | Talk to a remote SAS server (`PROC UPLOAD`, `PROC DOWNLOAD`) | 🔑 |
| **SAS Enterprise Guide / SAS Studio** | Screens (front-ends) where you write and run SAS code | 🌐 |
| **SAS Viya** | Newer cloud-ready SAS platform; same language, extra engines (CAS) | 🌐 |

### 2.3 Concept comparison: SAS vs SQL vs Python/Pandas vs Excel

> These are **close equivalents, not identical twins.** For example, a SAS *library* is only a named pointer to a folder (or a database connection). It is not always a database.

| Concept | SAS | SQL | Python / Pandas | Excel |
|---|---|---|---|---|
| Place holding data | **Library** (`LIBNAME` shortcut to a folder or DB) | Database / schema | Folder / file path | Folder / workbook |
| Table | **Dataset** | Table | DataFrame | Worksheet |
| Column | **Variable** | Column | Column / Series | Column |
| Row | **Observation** | Row / record | Row | Row |
| Filtering | `WHERE`, subsetting `IF` | `WHERE` | `df[df.salary > 50000]` | Filter / `FILTER()` |
| Sorting | `PROC SORT` | `ORDER BY` | `sort_values()` | Sort |
| Grouping & totals | `PROC MEANS`, `PROC SQL GROUP BY` | `GROUP BY` | `groupby().agg()` | PivotTable / `SUMIFS` |
| Join | `MERGE`, `PROC SQL JOIN` | `JOIN` | `merge()` | `XLOOKUP` / `VLOOKUP` |
| Stack tables | `SET a b;`, `PROC APPEND` | `UNION ALL` | `pd.concat()` | Copy-paste / Power Query append |
| Data types | Only **numeric** and **character** | Many (INT, VARCHAR, DATE…) | int, float, str, datetime | General, Number, Text, Date |
| Missing values | `.` numeric, blank character | `NULL` | `NaN` / `None` | Empty cell |
| If-then logic | `IF/THEN/ELSE`, `SELECT/WHEN` | `CASE WHEN` | `np.where()`, `apply` | `IF()` |
| Character functions | `UPCASE`, `SUBSTR`, `SCAN`… | `UPPER`, `SUBSTR`… | `.str.upper()`… | `UPPER`, `MID`… |
| Numeric functions | `ROUND`, `SUM`, `MEAN`… | `ROUND`, `SUM`, `AVG` | `round()`, `sum()` | `ROUND`, `SUM` |
| Date/time functions | `TODAY`, `INTNX`, `INTCK` | `CURRENT_DATE`, `DATEADD`/`DATEDIFF` (vary by database) | `pd.Timestamp`, `DateOffset` | `TODAY`, `EDATE`, `DATEDIF` |
| Row number / rank | Counter in DATA step, `PROC RANK` | `ROW_NUMBER() OVER`, `RANK() OVER` | `rank()`, `cumcount()` | `RANK`, `ROW()` |
| Reshape | `PROC TRANSPOSE` | `PIVOT` / `UNPIVOT` (varies) | `pivot`, `melt` | PivotTable, Power Query |
| Summary statistics | `PROC MEANS`, `PROC UNIVARIATE` | `COUNT`, `AVG`, … | `describe()` | Data Analysis ToolPak |
| Import / Export | `PROC IMPORT/EXPORT`, `INFILE`, `LIBNAME` | `COPY`, `BULK INSERT` (varies) | `read_csv`, `to_csv` | Open / Save As |

### 2.4 Function comparison table

| Purpose | SAS | SQL (common/ANSI style) | Python / Pandas | Excel | Example (SAS) |
|---|---|---|---|---|---|
| Upper case | `UPCASE(x)` | `UPPER(x)` | `s.str.upper()` | `UPPER(A1)` | `UPCASE("sas")` → `SAS` |
| Remove spaces at both ends | `STRIP(x)` | `TRIM(x)` | `s.str.strip()` | `TRIM(A1)` | `STRIP("  hi ")` → `hi` |
| Part of text | `SUBSTR(x,start,len)` | `SUBSTR(x,start,len)` | `s.str[0:3]` | `MID(A1,1,3)` | `SUBSTR("Mumbai",1,3)` → `Mum` |
| Position of text | `FIND(x,"a")` | `POSITION`/`INSTR` (varies) | `s.str.find("a")` | `FIND("a",A1)` | `FIND("Mumbai","b")` → `4` |
| Replace text | `TRANWRD(x,old,new)` | `REPLACE(x,old,new)` | `s.str.replace(old,new)` | `SUBSTITUTE` | `TRANWRD("a-b","-","_")` → `a_b` |
| Join text | `CATX("-",a,b)` | `a \|\| '-' \|\| b` / `CONCAT` | `a + "-" + b` | `TEXTJOIN("-",TRUE,A1,B1)` | `CATX("-","A","B")` → `A-B` |
| Round | `ROUND(x,0.01)` | `ROUND(x,2)` | `round(x,2)` | `ROUND(A1,2)` | `ROUND(3.14159,0.01)` → `3.14` |
| Sum ignoring missing | `SUM(a,b)` | `COALESCE(a,0)+COALESCE(b,0)` | `df[['a','b']].sum(axis=1)` | `SUM(A1:B1)` | `SUM(5,.)` → `5` |
| Today's date | `TODAY()` | `CURRENT_DATE` | `pd.Timestamp.today()` | `TODAY()` | `d = TODAY();` |
| Year of a date | `YEAR(d)` | `EXTRACT(YEAR FROM d)` | `s.dt.year` | `YEAR(A1)` | `YEAR('15JAN2025'd)` → `2025` |
| Add months | `INTNX('month',d,3)` | `DATEADD`/`+ INTERVAL` (varies) | `s + pd.DateOffset(months=3)` | `EDATE(A1,3)` | `INTNX('month','15JAN2025'd,3,'same')` → 15APR2025 |
| Count months between | `INTCK('month',d1,d2)` | `DATEDIFF` (varies) | `(y2-y1)*12 + m2-m1` | `DATEDIF(A1,B1,"m")` | see Session 6 |
| Is missing? | `MISSING(x)` | `x IS NULL` | `s.isna()` | `ISBLANK(A1)` | `MISSING(.)` → `1` |
| Text → number | `INPUT(x,8.)` | `CAST(x AS INT)` | `pd.to_numeric(s)` | `VALUE(A1)` | `INPUT("123",8.)` → `123` |
| Number → text | `PUT(x,8.)` | `CAST(x AS VARCHAR)` | `s.astype(str)` | `TEXT(A1,"0")` | `PUT(123,8.)` → `"     123"` |

**Differences that matter**

- **Missing values:** SAS numeric missing `.` is treated as **smaller than any number** in comparisons (`if salary < 1000` is true for a missing salary!). SQL `NULL` comparisons give "unknown". Pandas `NaN` comparisons give `False`.
- **Dates:** SAS stores a date as a **number of days since 01JAN1960**. A format such as `DATE9.` only changes how it *looks*.
- **Arguments:** `TRANSLATE(x, to, from)` takes the *new* characters first; `TRANWRD(x, from, to)` takes the *old* text first. SAS `SUBSTR` starts counting at **1**, Python at **0**.
- **ROUND:** In SAS the second argument is the **unit** (`0.01`), not the number of decimal places (`2`).

### 2.5 The four sample datasets used everywhere in this guide

Type this once. Later sessions reuse these tables. Run it as-is in SAS.

```sas
/* EMPLOYEE : 7 rows. Neha has a MISSING salary on purpose */
data employee;
    input employee_id employee_name :$12. department :$10. salary hire_date :date9.;
    format hire_date date9. salary comma10.;
    datalines;
101 Asha  HR    45000 15JAN2020
102 Ravi  IT    62000 03MAR2019
103 Meena IT    58000 21JUL2021
104 John  Sales 51000 10NOV2018
105 Priya Sales 49000 05JUN2022
106 Karan HR    47000 01AUG2023
107 Neha  IT        . 12DEC2023
;
run;

/* CUSTOMER : 5 rows. Customer 4 has a MISSING credit limit */
data customer;
    input customer_id customer_name :$15. city :$10. credit_limit;
    datalines;
1 Alpha_Corp   Mumbai  50000
2 Beta_Traders Delhi   30000
3 Gamma_Stores Mumbai  70000
4 Delta_Mart   Chennai     .
5 Echo_Retail  Pune    20000
;
run;

/* ORDERS : 6 rows. Order 5006 belongs to customer 6, who is NOT in CUSTOMER */
data orders;
    input order_id customer_id order_date :date9. amount;
    format order_date date9.;
    datalines;
5001 1 05JAN2025 1200
5002 1 17JAN2025  800
5003 2 20JAN2025 1500
5004 3 02FEB2025 2200
5005 3 14FEB2025  400
5006 6 20FEB2025  900
;
run;

/* SALES : 6 rows */
data sales;
    input product_id :$3. region :$5. sales_amount transaction_date :date9.;
    format transaction_date date9.;
    datalines;
P1 East 1000 10JAN2025
P1 West  800 12JAN2025
P2 East  600 15JAN2025
P2 West  900 03FEB2025
P3 East  300 14FEB2025
P3 West  450 20FEB2025
;
run;
```

The data was designed with deliberate "traps": a missing salary, a missing credit limit, customers with no orders (4 and 5), and an order with no customer (5006). These make joins and missing-value behaviour easy to see.

---

## 3. SESSION-WISE SYLLABUS

### SESSION 1 — SAS FUNDAMENTALS AND DATA IMPORT

**Topics in this session:** 1.1 What is SAS · 1.2 SAS PC / Studio / Enterprise Guide · 1.3 Terminology · 1.4 First dataset · 1.5 Basic program explained · 1.6 Interface windows · 1.7 Shortcut keys · 1.8 Fixed-width files · 1.9 Libraries · 1.10 Naming rules · 1.11 Variable types, lengths, missing values · 1.12 DATA step vs PROC step · 1.13 PROC IMPORT · 1.14 PROC CONTENTS and friends · 1.15 Dataset from dataset · 1.16 PROC COPY · 1.17 Keywords · 1.18 Statement comparison · 1.19 Inline vs external vs import

---

#### 1.1 What is SAS and what are its primary components?

**In simple words:** SAS is a tool where you write short instructions ("programs") and SAS reads your data, changes it, and prints results.

- **Definition:** SAS is a programming language plus a software suite for data management, analytics and reporting.
- **Purpose:** Turn raw data into clean tables, statistics and reports that others can trust.
- **Primary components:** see the component table in [Section 2.2](#22-main-sas-components-simple-view) (Base SAS, SAS/STAT, SAS/ACCESS, SAS/CONNECT, SAS/GRAPH, front-ends, Viya).

**Two facts to remember:** SAS has only two data types (numeric and character), and every program is built from **DATA steps** and **PROC steps**.

---

#### 1.2 SAS PC, SAS University Edition / Studio, SAS Enterprise Guide

| Tool | What it is (simple) | Notes |
|---|---|---|
| **SAS PC (Display Manager / "SAS 9.4 for Windows")** | The classic desktop SAS with Editor, Log and Output windows | Installed on your PC; windows are separate |
| **SAS University Edition** | A *free learning* version that ran in a virtual machine and opened in a browser | 🌐 **Retired by SAS.** Use **SAS OnDemand for Academics** (free, browser-based SAS Studio) instead |
| **SAS Studio** | Browser-based SAS editor: code, log, results, and a point-and-click "Tasks" area | Common in companies and in Viya |
| **SAS Enterprise Guide (EG)** | Desktop app that works with a SAS server; supports code *and* drag-and-drop "projects" | Common in banks/insurers; works with a remote SAS server |

All of them run the **same SAS language**. Menus and shortcuts differ.

---

#### 1.3 SAS programming fundamentals and terminology

| Term | Plain meaning | Example |
|---|---|---|
| **Statement** | One instruction, always ends with `;` | `set employee;` |
| **Step** | A block of statements; a DATA step or a PROC step | `data ...; ... run;` |
| **Dataset (data set)** | A SAS table | `work.employee` |
| **Variable** | A column | `salary` |
| **Observation** | A row | The row for Asha |
| **Library** | A named shortcut to a folder holding datasets | `work`, `sashelp` |
| **Option** | A setting that changes how a statement/step behaves | `data=employee`, `obs=5` |
| **Format** | How a value is *displayed* | `date9.` shows 23756 as `15JAN2025` |
| **Informat** | How raw text is *read* | `date9.` reads `15JAN2025` as 23756 |
| **Global statement** | Works outside steps | `libname`, `options`, `title` |
| **Comment** | Ignored by SAS | `/* note */` or `* note;` |
| **Log** | Messages: notes, warnings, errors | Always read it after every run |

**Two built-in libraries every user meets**

- `WORK` — temporary library. Everything in it is **deleted when SAS closes**. If you write `data employee;` (no library), it goes to `WORK`.
- `SASHELP` — read-only sample datasets such as `sashelp.class`, `sashelp.cars`.

---

#### 1.4 Your first SAS dataset

- **Definition:** Creating a dataset means telling SAS the column names and giving it the values.
- **Purpose:** The starting point of every analysis.

**Syntax**

```sas
DATA dataset_name;
    INPUT var1 var2 $ var3;    /* $ after a name = character variable */
    DATALINES;
    ...data lines...
    ;
RUN;
```

**Example** (uses the EMPLOYEE data from Section 2.5 in simplified form)

```sas
data first_ds;
    input employee_id employee_name $ department $ salary;
    datalines;
101 Asha HR 45000
102 Ravi IT 62000
103 Meena IT 58000
;
run;

proc print data=first_ds;
run;
```

**Expected output**

| Obs | employee_id | employee_name | department | salary |
|---:|---:|---|---|---:|
| 1 | 101 | Asha | HR | 45000 |
| 2 | 102 | Ravi | IT | 62000 |
| 3 | 103 | Meena | IT | 58000 |

---

#### 1.5 Explanation of a basic SAS program (line by line)

```sas
data first_ds;                                   /* (1) */
    input employee_id employee_name $ department $ salary;   /* (2) */
    datalines;                                   /* (3) */
101 Asha HR 45000
;                                                /* (4) */
run;                                             /* (5) */

proc print data=first_ds;                        /* (6) */
run;                                             /* (7) */
```

| # | What it says in plain words |
|---|---|
| 1 | "Start building a new table called `first_ds` (saved in WORK)." |
| 2 | "Here are the columns, in order. A `$` means that column holds text." |
| 3 | "My data is typed right below." |
| 4 | A lone `;` ends the data lines. |
| 5 | "Run the DATA step now." |
| 6 | "Start a print procedure on `first_ds`." |
| 7 | "Run it." |

**Important rules**

- Every statement ends with `;`. A missing semicolon is the number-one beginner error.
- SAS is **not case sensitive** for code and names (`DATA` = `data`), **but data values are case sensitive** (`"HR"` ≠ `"hr"`).
- A step ends at `RUN;` (or at the next `DATA`/`PROC`). `PROC SQL` ends at `QUIT;`.
- With list input, a **character variable defaults to length 8** and longer values are cut. Fix with a length or informat: `employee_name :$12.`.

---

#### 1.6 SAS interface windows and their functions

**SAS PC (Display Manager)**

| Window | What it does |
|---|---|
| **Editor** (Program Editor / Enhanced Editor) | Where you type code |
| **Log** | Shows notes, warnings, errors, run times. **Check it every time** |
| **Output** | Text results (when listing output is on) |
| **Results** | Tree of everything produced; double-click to open HTML/PDF results |
| **Explorer** | Browse libraries and datasets |
| **Libraries / Active Libraries** | Shows which libraries are assigned |

**SAS Studio / Enterprise Guide equivalents**

| Display Manager | SAS Studio | Enterprise Guide |
|---|---|---|
| Editor | **Code** tab | Program window |
| Log | **Log** tab | Log tab |
| Output / Results | **Results** tab | Results tab |
| Explorer / Libraries | **Libraries** pane (left) | Server List / Libraries in Servers |

**Log colour code (very useful):** blue = `NOTE`, green = `WARNING` (in some versions), red = `ERROR`. Fix **errors first**, then read warnings.

---

#### 1.7 Useful SAS shortcut keys

🌐 Shortcuts vary by version and operating system. Treat these as typical defaults.

| Action | Display Manager (Windows) | SAS Studio |
|---|---|---|
| Run / submit code | **F3** or **F8** | **F3** (runs selected code or whole program) |
| Jump to Editor | **F5** | click **Code** tab |
| Jump to Log | **F6** | click **Log** tab |
| Jump to Output | **F7** | click **Results** tab |
| Clear Log / Output | **Ctrl+E** while in that window | trash/clear icon |
| Comment selected lines | **Ctrl+/** | **Ctrl+/** |
| Uncomment selected lines | **Ctrl+Shift+/** | **Ctrl+Shift+/** |
| Show key definitions | **F9** (KEYS window) | — |
| Select and run part of code | Highlight, then **F3/F8** | Highlight, then **F3** |

---

#### 1.8 Reading fixed-width text files

**In simple words:** In a fixed-width file every field always sits in the **same columns**, like a printed form. Instead of looking for spaces, you tell SAS: "name is in columns 4 to 13."

- **Definition:** A *fixed-width* (fixed-column) file has each field occupying a set range of character positions.
- **Purpose:** Many mainframe, bank and government files come this way, and values may contain spaces.

**Sample file `emp_fixed.txt`** (positions: ID 1–3, name 4–13, department 14–18, salary 19–23)

```
101Asha      HR   45000
102Ravi      IT   62000
103Meena     IT   58000
```

**Syntax (column input)**

```sas
INFILE "path/to/file.txt";
INPUT variable [$] start_col-end_col ... ;
```

**Example**

```sas
filename empfix "/home/user/data/emp_fixed.txt";   /* placeholder path */

data emp_fixed;
    infile empfix;
    input employee_id 1-3
          employee_name $ 4-13
          department $ 14-18
          salary 19-23;
run;

proc print data=emp_fixed noobs;
run;
```

**Expected output**

| employee_id | employee_name | department | salary |
|---:|---|---|---:|
| 101 | Asha | HR | 45000 |
| 102 | Ravi | IT | 62000 |
| 103 | Meena | IT | 58000 |

**Important rules**

- With column input, `$ 4-13` automatically sets the **length** to 10; no truncation surprise.
- Alternative: **formatted input** with a pointer: `input @1 id 3. @4 name $10. @14 dept $5. @19 salary 5.;`
- If lines are shorter than expected, add `TRUNCOVER` to `INFILE` (see Session 3).

---

#### 1.9 SAS libraries and library naming rules

**In simple words:** A library is a **nickname for a folder**. Instead of typing a long path each time, you type `mylib.employee`.

- **Definition:** A library is a storage location (usually a folder, sometimes a database connection) given a short name (a *libref*).
- **Purpose:** Save datasets permanently and refer to them easily.

**Syntax**

```sas
LIBNAME libref "path-to-folder";
LIBNAME libref CLEAR;           /* remove the nickname (does not delete files) */
```

**Example**

```sas
libname mylib "/home/user/sasdata";      /* nickname for a folder */

data mylib.employee;                      /* permanent dataset */
    set work.first_ds;
run;
```

Now `mylib.employee` stays on disk after you close SAS. The nickname `mylib` itself disappears when SAS closes, so you must run `LIBNAME` again in each session.

**Library naming rules (libref)**

| Rule | Detail |
|---|---|
| Length | **1 to 8 characters** |
| First character | A letter or underscore |
| Other characters | Letters, digits, underscore only |
| Reserved | Don't reuse `WORK`, `SASHELP`, `SASUSER` |

**Two-level name:** `libref.dataset`. If you give only one level (`employee`), SAS uses `WORK`.

**Related:** `PROC DATASETS` can also list and manage a library (see 1.14).

---

#### 1.10 Dataset and variable naming rules

| Rule | Datasets | Variables |
|---|---|---|
| Max length | **32 characters** | **32 characters** |
| Start with | Letter or underscore | Letter or underscore |
| Allowed characters | Letters, digits, underscore | Letters, digits, underscore |
| Spaces / special characters | Not allowed (normally) | Not allowed (normally) |
| Case | Not case sensitive (stored as you typed it) | Not case sensitive |

✅ Good names: `employee_id`, `Sales2025`, `_temp`
❌ Bad names: `2025sales` (starts with a digit), `emp-id` (hyphen), `first name` (space)

🌐 **Special case:** with `OPTIONS VALIDVARNAME=ANY;` you may use spaces/special characters by writing a **name literal**: `'First Name'n`. Avoid this in new work; it causes trouble later. `PROC IMPORT` may convert such headers into underscores depending on `VALIDVARNAME`.

---

#### 1.11 SAS variable types, lengths, values and missing values

**Only two types**

| Type | Holds | Default length | Looks like |
|---|---|---|---|
| **Numeric** | Numbers, **and dates/times** (as numbers) | 8 bytes (all numerics) | `45000` |
| **Character** | Letters, digits-as-text, symbols | 8 characters (list input) up to 32,767 | `"HR"` |

**Length**

- Character length decides how many characters are stored. If the first value is `"HR"` and a later one is `"Marketing"`, a too-short length **cuts** the long value.
- Numeric length is 8 bytes by default; you rarely change it.
- Set length **before** you use the variable: `length department $ 12;`

**Missing values**

| Type | Missing is shown as | Test |
|---|---|---|
| Numeric | `.` (dot) | `if salary = . ;` or `if missing(salary);` |
| Character | blank `" "` | `if name = " ";` or `if missing(name);` |
| Special numeric missing | `.A` to `.Z`, `._` | used for coded reasons (e.g. "refused") |

**Behaviour to remember**

- A missing numeric is **smaller than every number**: `salary < 1000` is TRUE when salary is `.`.
- Arithmetic with a missing value gives missing: `5 + . = .`.
- `SUM(5, .)` gives `5` (ignores missing). Details in Session 6.

**Automatic variables** SAS creates inside a DATA step: `_N_` (loop counter of the data step), `_ERROR_` (1 if an error occurred on that row), and with `BY` or `IN=` extra ones such as `FIRST.var`, `LAST.var`. They are **not** saved in the output dataset.

**Variable attributes** (name, type, length, format, informat, label) are shown by `PROC CONTENTS`.

---

#### 1.12 DATA step and PROC step

| | **DATA step** | **PROC step** |
|---|---|---|
| Simple meaning | *Makes or changes* data | *Uses* data (report, sort, statistics) |
| Starts with | `DATA name;` | `PROC procedure-name ...;` |
| Typical statements | `SET`, `INPUT`, `IF`, assignment, `OUTPUT`, `KEEP`, `DROP` | `VAR`, `BY`, `CLASS`, `TABLES`, `OUTPUT` (varies by procedure) |
| Works | Row by row (loops through rows) | On the whole dataset at once |
| Ends with | `RUN;` | `RUN;` (`QUIT;` for `PROC SQL`, `PROC DATASETS`) |
| Creates | A dataset (always) | Reports; sometimes datasets via `OUT=` |

**Interview takeaway:** *"What is the difference between a DATA step and a PROC step?"* → A DATA step creates/transforms datasets with row-wise processing; a PROC step calls a prebuilt procedure to analyse, report or manage data.

(Full side-by-side comparison in [Section 5](#5-data-step-versus-proc-step).)

---

#### 1.13 Reading TXT, CSV and Excel files using PROC IMPORT

**In simple words:** `PROC IMPORT` is the "Open file" button. SAS opens the file, guesses column types, and builds a dataset.

- **Definition:** A procedure that reads an external structured file and creates a SAS dataset.
- **Purpose:** Fastest way to load clean, rectangular files.

**Syntax**

```sas
PROC IMPORT DATAFILE="file path"
            OUT=library.dataset
            DBMS=file-type
            REPLACE;
    GETNAMES=YES;          /* first row has column names */
RUN;
```

| DBMS= | Reads | Tag |
|---|---|---|
| `CSV` | Comma-separated file | ✅ Base SAS |
| `TAB` | Tab-separated file | ✅ Base SAS |
| `DLM` + `DELIMITER=` (e.g. a pipe character) | Any other single delimiter | ✅ Base SAS |
| `XLSX` | Excel `.xlsx` | 🔑 Usually needs **SAS/ACCESS Interface to PC Files** (check your licence) |
| `EXCEL` | Excel via Windows drivers | 🌐 Windows only; bitness (32/64-bit) issues are common |

**Examples**

```sas
/* CSV */
proc import datafile="/home/user/data/customers.csv"
            out=work.customers_csv
            dbms=csv replace;
    getnames=yes;
    guessingrows=max;      /* look at all rows before deciding types */
run;

/* TXT, tab separated */
proc import datafile="/home/user/data/customers.txt"
            out=work.customers_txt
            dbms=tab replace;
    getnames=yes;
run;

/* TXT with a pipe | delimiter */
proc import datafile="/home/user/data/customers_pipe.txt"
            out=work.customers_pipe
            dbms=dlm replace;
    delimiter='|';
    getnames=yes;
run;

/* Excel, one sheet */
proc import datafile="/home/user/data/sales.xlsx"
            out=work.sales_xl
            dbms=xlsx replace;
    sheet="Q1";
    getnames=yes;
run;
```

**Important rules**

- `REPLACE` overwrites an existing output dataset; without it SAS refuses.
- `PROC IMPORT` **guesses** types and lengths from the first rows (`GUESSINGROWS=` controls how many). A column of codes like `007` may become numeric `7`, and a long text may be cut. If control matters, read with a DATA step (Session 3).
- Messy Excel (merged cells, titles above the header) imports badly. Clean the file or use `RANGE=` (e.g. `range="Q1$A3:D100";`).

**Interview takeaway:** *"When is PROC IMPORT a bad idea?"* → When files are messy, when types must be exact (IDs, leading zeros, dates), or for jobs that run daily on changing files; a DATA step with `INFILE` gives full control.

---

#### 1.14 Describing datasets and libraries: PROC CONTENTS and related procedures

**In simple words:** These are your "properties" windows. They tell you what columns exist, their types and lengths, and how many rows there are, **without printing the data**.

**Syntax and examples**

```sas
/* Describe ONE dataset: variables, types, lengths, formats, number of rows */
proc contents data=work.employee;
run;

/* Short list of variables only */
proc contents data=work.employee short;
run;

/* List ALL datasets in a library (no variable details) */
proc contents data=work._all_ nods;
run;

/* Same info as a dataset you can query */
proc contents data=work.employee out=work.emp_vars noprint;
run;

/* Look inside a library with PROC DATASETS */
proc datasets library=work;
    contents data=employee;
quit;

/* Peek at the data */
proc print data=work.employee (obs=5);   /* first 5 rows */
run;

/* Summary dictionary tables via PROC SQL */
proc sql;
    select memname, nobs
    from dictionary.tables
    where libname = "WORK";
quit;
```

**What PROC CONTENTS shows**

| Section | Tells you |
|---|---|
| Data Set Name, Observations, Variables | Table name, row count, column count |
| Engine/Host information | Where and how it is stored |
| Alphabetic List of Variables | Name, Type (Num/Char), Len, Format, Informat, Label |
| Sort information (if any) | Whether the dataset is sorted and by what |

**Related tools**

| Tool | Use |
|---|---|
| `PROC PRINT` | Show rows |
| `PROC DATASETS` | List, rename, delete, modify attributes of datasets |
| `DICTIONARY.TABLES / COLUMNS` (in `PROC SQL`) or `SASHELP.VTABLE / VCOLUMN` | Metadata as queryable tables |
| `PROC FREQ`, `PROC MEANS` | Quick data profiling (Session 6) |

---

#### 1.15 Creating a dataset from an existing dataset

**In simple words:** "Make a copy of this table (maybe with changes)."

**Syntax**

```sas
DATA new_dataset;
    SET existing_dataset;
    /* optional changes */
RUN;
```

**Example: copy with a new calculated column**

```sas
data work.emp_bonus;
    set work.employee;
    bonus = salary * 0.10;      /* new variable */
run;
```

**Expected output (first rows)**

| employee_id | employee_name | department | salary | hire_date | bonus |
|---:|---|---|---:|---|---:|
| 101 | Asha | HR | 45,000 | 15JAN2020 | 4500 |
| 102 | Ravi | IT | 62,000 | 03MAR2019 | 6200 |
| … | | | | | |
| 107 | Neha | IT | . | 12DEC2023 | . |

Note Neha: `. * 0.10` is missing (`.`), not zero.

**Other ways:** `PROC SQL` → `create table work.emp2 as select * from work.employee;`. Details in Sessions 4 and 7.

---

#### 1.16 Copying datasets between libraries (PROC COPY and other methods)

```sas
libname src "/home/user/source";
libname tgt "/home/user/target";

/* Method 1: PROC COPY - whole library or selected datasets */
proc copy in=src out=tgt memtype=data;
    select employee customer;        /* leave out SELECT to copy everything */
run;

/* Method 2: DATA step - one dataset, can also change it */
data tgt.employee;
    set src.employee;
run;

/* Method 3: PROC SQL */
proc sql;
    create table tgt.customer as
    select * from src.customer;
quit;

/* Method 4: PROC DATASETS COPY */
proc datasets library=src nolist;
    copy out=tgt;
    select employee;
quit;
```

| Method | Best when |
|---|---|
| `PROC COPY` | Copying as-is (keeps indexes, attributes); fastest for many datasets |
| DATA step | You also want to filter or modify while copying |
| `PROC SQL` | You prefer SQL, or want to join while copying |
| `PROC DATASETS` | You are already managing the library |

`MEMTYPE=DATA` restricts the copy to datasets (not catalogs or views).

---

#### 1.17 Essential SAS keywords and their meanings

| Keyword | Meaning |
|---|---|
| `DATA` | Begins a DATA step; names the output dataset |
| `SET` | Reads an existing SAS dataset into a DATA step |
| `MERGE` | Combines datasets side by side by key |
| `INPUT` | Describes how to read raw data into variables |
| `INFILE` | Names an external file to read |
| `DATALINES` / `CARDS` | Marks data typed inside the program |
| `RUN` | Executes the step |
| `QUIT` | Ends `PROC SQL` / `PROC DATASETS` |
| `PROC` | Starts a procedure |
| `LIBNAME` | Creates a library nickname |
| `FILENAME` | Creates a nickname for an external file |
| `FORMAT` | Chooses how a value is shown |
| `INFORMAT` | Chooses how raw text is read |
| `LENGTH` | Sets storage length of a variable |
| `LABEL` | Gives a variable a readable description |
| `KEEP` / `DROP` | Choose columns to keep / remove |
| `WHERE` | Filter rows before they enter the step |
| `BY` | Process in groups / sort order |
| `OUTPUT` | Write the current row to the output dataset |
| `TITLE` / `FOOTNOTE` | Text at top / bottom of output |
| `OPTIONS` | Change global SAS settings |

---

#### 1.18 Comparison: LIBNAME, DATA, SET, INPUT, INFILE, PROC IMPORT, PROC CONTENTS, PROC PRINT, PROC EXPORT, PROC COPY, FORMAT, INFORMAT, RUN, CARDS, DATALINES

| Statement / procedure | Type | Job in one line | Mini example |
|---|---|---|---|
| `LIBNAME` | Global statement | Nickname for a folder/database | `libname mylib "/data";` |
| `DATA` | Step start | Start creating a dataset | `data work.a;` |
| `SET` | DATA step statement | Read an existing dataset | `set work.employee;` |
| `INPUT` | DATA step statement | Read raw values into variables | `input id name $;` |
| `INFILE` | DATA step statement | Point to an external file | `infile "emp.txt" dsd;` |
| `PROC IMPORT` | Procedure | Load a structured file quickly | `proc import datafile=... out=... dbms=csv;` |
| `PROC CONTENTS` | Procedure | Describe a dataset/library | `proc contents data=work.employee;` |
| `PROC PRINT` | Procedure | Display rows | `proc print data=work.employee;` |
| `PROC EXPORT` | Procedure | Write a dataset to CSV/Excel/etc. | `proc export data=... outfile=... dbms=csv;` |
| `PROC COPY` | Procedure | Copy datasets between libraries | `proc copy in=a out=b;` |
| `FORMAT` | Statement | Change **display** of values | `format hire_date date9.;` |
| `INFORMAT` | Statement | Change how raw text is **read** | `informat hire_date date9.;` |
| `RUN` | Step terminator | Execute the step | `run;` |
| `CARDS` | DATA step statement | Old name for `DATALINES` (identical) | `cards;` |
| `DATALINES` | DATA step statement | Data lines typed in the program | `datalines;` |

**Format vs Informat in one sentence:** *informat = text → stored value; format = stored value → displayed text.* Example: informat `date9.` turns `15JAN2025` into **23756**; format `date9.` turns **23756** back into `15JAN2025`.

---

#### 1.19 Inline data vs external files vs structured imports

| Method | Where the data lives | Tool | Best for |
|---|---|---|---|
| **Reading inline data** | Inside your program, under `DATALINES;` | `DATA` + `INPUT` + `DATALINES` | Small demos, test data |
| **Reading an external file** | Separate text file on disk | `DATA` + `INFILE` + `INPUT` | Full control: custom layouts, fixed width, messy delimiters |
| **Importing a structured file** | CSV/TXT/Excel with a clean header row | `PROC IMPORT` (or `LIBNAME XLSX`) | Quick loading of tidy files |

**Rule of thumb:** *Tidy file, one-time job → `PROC IMPORT`. Repeating or messy job → `INFILE`/`INPUT`.*

---

### SESSION 2 — DATA STEP MANIPULATION AND FORMATS

**Topics in this session:** 2.1 SET · 2.2 SAS programming steps and processing order · 2.3 KEEP/DROP · 2.4 RENAME · 2.5 WHERE (statement and option) · 2.6 WHERE operators and operands · 2.7 PROC SORT · 2.8 Removing duplicates · 2.9 List reports and ODS · 2.10 IF-THEN, IF-THEN-DO · 2.11 Many datasets from one source · 2.12 Formats and informats · 2.13 PROC FORMAT · 2.14 Permanent formats · 2.15 IF vs WHERE

All examples use the EMPLOYEE dataset from [Section 2.5](#25-the-four-sample-datasets-used-everywhere-in-this-guide).

---

#### 2.1 SET statement

**In simple words:** `SET` says "open this existing table and hand me its rows one at a time."

- **Definition:** A DATA step statement that reads observations from one or more existing SAS datasets.
- **Purpose:** Copy, modify, filter, stack, or interleave datasets.

**Syntax**

```sas
DATA output_ds;
    SET input_ds1 <input_ds2 ...> <(dataset options)>;
    ...statements...
RUN;
```

**Example**

```sas
data emp_copy;
    set employee;
    annual_salary = salary * 12;      /* treat salary as monthly pay for this example */
run;
```

**Important rules**

- The variables of the input dataset come along automatically (unless you `DROP`/`KEEP` them).
- Several datasets in one `SET` are **stacked** (Session 4).
- `SET` with `BY` reads datasets **interleaved** in sorted order (data must be sorted).

---

#### 2.2 SAS programming steps and processing order (only what you need)

Every DATA step runs in two phases:

| Phase | What SAS does | What you notice |
|---|---|---|
| **Compile** | Checks syntax, builds the **Program Data Vector (PDV)** (a one-row work area), decides variable names, types and lengths | Syntax errors, "variable not found", length decisions |
| **Execute** | Loops: read a row → run your statements top to bottom → write the row → repeat | Calculations, `IF` logic, output |

**Why it matters:** A variable's **type and length are fixed at compile time from where it is first seen.** If `grade = "Low"` appears first, `grade` becomes length 3 and `"Medium"` would be cut. Use a `LENGTH` statement first.

*(The PDV is explained fully with a worked example in Session 3.)*

---

#### 2.3 KEEP and DROP (statements and dataset options)

**In simple words:** Choose which columns to **keep** or **throw away**.

| Form | Where written | Effect |
|---|---|---|
| **Statement** `KEEP a b;` / `DROP a b;` | Inside the DATA step | Applies to **every** output dataset of that step |
| **Dataset option on output** `data x(keep=a b);` | On the dataset being created | Applies to **that** dataset only |
| **Dataset option on input** `set y(keep=a b);` | On the dataset being read | Columns are **never read** (faster, and you can't use the dropped ones in the step) |

**Examples (all valid)**

```sas
/* (a) KEEP statement */
data emp_a;
    set employee;
    keep employee_id employee_name salary;
run;

/* (b) DROP statement */
data emp_b;
    set employee;
    drop hire_date department;
run;

/* (c) KEEP= option on the OUTPUT dataset */
data emp_c(keep=employee_id bonus);
    set employee;
    bonus = salary * 0.10;          /* salary is used, but not saved */
run;

/* (d) DROP= option on the INPUT dataset */
data emp_d;
    set employee(drop=hire_date);
run;
```

**Expected result for (c) (first rows)**

| employee_id | bonus |
|---:|---:|
| 101 | 4500 |
| 102 | 6200 |
| 103 | 5800 |

**Important rules**

- You **cannot use** a variable in calculations if you dropped it with an *input* `DROP=`/`KEEP=`.
- Statement versions apply to the output; use the option version when different output datasets need different columns.
- Prefer `KEEP` when keeping a few columns and `DROP` when removing a few.

---

#### 2.4 RENAME (statement and dataset option)

| Form | Example | When names change |
|---|---|---|
| **Statement** | `rename salary = monthly_pay;` | At the **end** of the step. Inside the step you still use the **old** name |
| **Option on output** | `data x(rename=(salary=monthly_pay));` | At output. Inside the step you use the old name |
| **Option on input** | `set employee(rename=(salary=monthly_pay));` | **Immediately** on reading. Inside the step you use the **new** name |

```sas
/* Statement */
data emp_r1;
    set employee;
    rename salary = monthly_pay  employee_name = name;
run;

/* Option on input: the new name is used in the step */
data emp_r2;
    set employee(rename=(salary=monthly_pay));
    yearly_pay = monthly_pay * 12;
run;

/* Option on output with KEEP: KEEP is applied first, so use OLD names in KEEP */
data emp_r3(keep=employee_id salary rename=(salary=monthly_pay));
    set employee;
run;
```

**Important rules**

- Several renames in one option: `rename=(a=x b=y)`; inside the parentheses, **no commas**.
- You cannot rename to a name that already exists in the dataset.

---

#### 2.5 WHERE (statement and dataset option)

**In simple words:** "Only let rows through that pass this test." It works like a gate at the entrance.

```sas
/* WHERE statement */
data it_emp;
    set employee;
    where department = "IT";
run;

/* WHERE= dataset option */
data it_emp2;
    set employee(where=(department = "IT"));
run;

/* WHERE in a PROC step: filter just for this report */
proc print data=employee;
    where salary > 50000;
run;
```

**Expected output of the `IT` filter**

| employee_id | employee_name | department | salary | hire_date |
|---:|---|---|---:|---|
| 102 | Ravi | IT | 62,000 | 03MAR2019 |
| 103 | Meena | IT | 58,000 | 21JUL2021 |
| 107 | Neha | IT | . | 12DEC2023 |

**Where you can use it:** DATA steps, almost all PROC steps, and as a dataset option (including in `PROC SQL` `FROM` clauses).

---

#### 2.6 WHERE operators and operands

**Operands** are the things being compared: variables, constants (`50000`, `"IT"`), expressions, and most functions.

| Type | Operators | Example | Result on EMPLOYEE |
|---|---|---|---|
| Comparison | `=` `^=` `>` `<` `>=` `<=` (or `EQ NE GT LT GE LE`) | `where salary >= 50000;` | Ravi, Meena, John |
| Logical | `AND` `OR` `NOT` | `where department="IT" and salary > 60000;` | Ravi |
| List | `IN (...)` | `where department in ("HR","Sales");` | Asha, John, Priya, Karan |
| Range (inclusive) | `BETWEEN a AND b` | `where salary between 45000 and 50000;` | Asha, Priya, Karan |
| Pattern | `LIKE` with `%` (any text) and `_` (one char) | `where employee_name like "P%";` | Priya |
| Contains text | `CONTAINS` or `?` | `where employee_name contains "ee";` | Meena |
| Missing | `IS MISSING` / `IS NULL` | `where salary is missing;` | Neha |
| Sounds like | `=*` | `where employee_name =* "Rawi";` | Ravi (approximate sound match) |
| Add a condition | `SAME AND` | `where department="IT"; where same and salary>60000;` | Ravi |

**Important rules**

- Text comparisons are **case sensitive**: `"it"` does not match `"IT"`. Use `where upcase(department)="IT";`.
- **Missing numbers are the smallest values.** `where salary < 50000;` includes Neha (missing)! Write `where salary < 50000 and salary is not missing;` or `where . < salary < 50000;`.
- `WHERE` **cannot use a variable created in the same DATA step** (see 2.15).
- If you write several `WHERE` statements, the **last one replaces** the earlier ones; use `WHERE SAME AND` to add conditions.

---

#### 2.7 PROC SORT and sorting by multiple variables

**In simple words:** Re-arrange the rows of a table in a chosen order.

- **Definition:** A procedure that orders a dataset by one or more `BY` variables.
- **Purpose:** Prepare data for `MERGE`, `FIRST./LAST.`, duplicate removal, or readable reports.

**Syntax**

```sas
PROC SORT DATA=input_ds <OUT=output_ds> <NODUPKEY> <DUPOUT=ds>;
    BY <DESCENDING> var1 <DESCENDING> var2 ...;
RUN;
```

**Example: department A→Z, then salary high→low**

```sas
proc sort data=employee out=emp_sorted;
    by department descending salary;
run;
```

**Expected output**

| department | employee_name | salary |
|---|---|---:|
| HR | Karan | 47,000 |
| HR | Asha | 45,000 |
| IT | Ravi | 62,000 |
| IT | Meena | 58,000 |
| IT | Neha | . |
| Sales | John | 51,000 |
| Sales | Priya | 49,000 |

**Important rules**

- `DESCENDING` applies **only to the variable right after it**. Write it before each variable that needs it.
- **Always use `OUT=`** unless you really want to overwrite the original dataset.
- Missing values sort **first** in ascending order and **last** in descending order (Neha above).
- Character sorting is case-sensitive by ASCII order on most systems (uppercase before lowercase).
- `PROC SORT` is Base SAS. In `PROC SQL` use `ORDER BY`.

---

#### 2.8 Removing duplicates: NODUPKEY and NODUPRECS

**In simple words:** `NODUPKEY` = "keep only the **first** row for each key." `NODUPRECS` = "remove a row that is **exactly identical** to the row just before it."

| Option | Compares | Keeps |
|---|---|---|
| `NODUPKEY` | Only the `BY` variables | The **first** observation of each `BY` value |
| `NODUPRECS` (or `NODUP`) | **All variables** of **adjacent** rows | One copy of consecutive identical rows |

**Example A: `NODUPKEY`, one row per department**

```sas
/* Step 1: put the highest salary first inside each department */
proc sort data=employee out=emp_top;
    by department descending salary;
run;

/* Step 2: keep the first row of each department = the top earner */
proc sort data=emp_top out=dept_top nodupkey dupout=dept_dups;
    by department;
run;
```

| department | employee_name | salary |
|---|---|---:|
| HR | Karan | 47,000 |
| IT | Ravi | 62,000 |
| Sales | John | 51,000 |

`dept_dups` holds the 4 removed rows. **Why two steps?** If you wrote `by department descending salary` together with `NODUPKEY`, the *key* would be department **and** salary, so almost nothing would count as a duplicate.

**Example B: `NODUPRECS`, remove exact duplicate rows**

```sas
data dup_demo;
    input id name :$8. dept :$6.;
    datalines;
1 Asha HR
2 Ravi IT
1 Asha HR
3 Meena IT
2 Ravi IT
;
run;

proc sort data=dup_demo out=clean noduprecs dupout=removed;
    by _all_;                /* sort by every variable so identical rows sit together */
run;
```

Result `clean`: ids 1, 2, 3 (one row each). `removed`: 2 rows (the extra `1 Asha HR` and `2 Ravi IT`).

**How sorting affects duplicate removal**

- `NODUPKEY` keeps the **first** row in each group, so **the order of rows before the sort decides which row survives** (SAS keeps the original relative order within a `BY` group by default). Sort first by the column that decides "best".
- `NODUPRECS` only compares **neighbours**. If identical rows are not next to each other, they are **not** removed. Sorting `BY _ALL_` makes identical rows neighbours.

---

#### 2.9 List reports and ODS fundamentals

**List report with `PROC PRINT`**

```sas
title "HR and IT Employees";
footnote "Source: EMPLOYEE table";
proc print data=employee noobs label;
    where department in ("HR","IT");
    var employee_id employee_name department salary;
    sum salary;
    label employee_name = "Employee Name";
run;
title; footnote;                 /* clear them afterwards */
```

**Expected output**

| employee_id | Employee Name | department | salary |
|---:|---|---|---:|
| 101 | Asha | HR | 45,000 |
| 102 | Ravi | IT | 62,000 |
| 103 | Meena | IT | 58,000 |
| 106 | Karan | HR | 47,000 |
| 107 | Neha | IT | . |
| | | | **212,000** |

| `PROC PRINT` option/statement | Use |
|---|---|
| `NOOBS` | Hide the Obs column |
| `LABEL` | Show variable labels instead of names |
| `VAR` | Choose and order columns |
| `ID` | Use a variable as the row identifier |
| `BY` | Separate groups (needs sorted data) |
| `SUM` | Column totals (ignores missing) |
| `(OBS=n)` | Print first n rows |

**ODS (Output Delivery System): how results leave SAS**

**In simple words:** ODS decides *where* your results go (screen, PDF, Excel, HTML) and how they look. You open a "destination", run your procedures, then close it.

```sas
ods pdf file="/home/user/out/emp_report.pdf";
    proc print data=employee noobs; run;
ods pdf close;

ods excel file="/home/user/out/emp_report.xlsx" options(sheet_name="Employees");
    proc print data=employee noobs; run;
ods excel close;

ods html file="/home/user/out/emp_report.html";
    proc means data=employee mean max; var salary; run;
ods html close;
```

| ODS feature | Meaning |
|---|---|
| Destinations | `HTML`, `PDF`, `RTF`, `EXCEL` (🌐 SAS 9.4 and later), `CSV`, `LISTING` |
| `ODS ... CLOSE` | Always close, or the file may be incomplete |
| `ODS TRACE ON;` | Writes the names of output tables to the log |
| `ODS OUTPUT table=ds;` | Saves a procedure's printed table as a dataset |
| `ODS SELECT` / `ODS EXCLUDE` | Show/hide specific tables |

---

#### 2.10 IF-THEN and IF-THEN-DO

**Syntax**

```sas
IF condition THEN statement;
ELSE IF condition THEN statement;
ELSE statement;

IF condition THEN DO;
    ...several statements...
END;
ELSE DO;
    ...
END;
```

**Example: grade with a missing salary handled first**

```sas
data emp_grade;
    set employee;
    length grade $ 7;                         /* set length BEFORE assigning */
    if missing(salary)       then grade = "Unknown";
    else if salary >= 60000  then grade = "High";
    else if salary >= 50000  then grade = "Medium";
    else                          grade = "Low";
run;
```

| employee_name | salary | grade |
|---|---:|---|
| Asha | 45,000 | Low |
| Ravi | 62,000 | High |
| Meena | 58,000 | Medium |
| John | 51,000 | Medium |
| Priya | 49,000 | Low |
| Karan | 47,000 | Low |
| Neha | . | Unknown |

**Example: `IF-THEN-DO` with several actions**

```sas
data emp_bonus;
    set employee;
    length team $ 8;
    if department = "IT" then do;
        bonus = salary * 0.15;
        team  = "Tech";
    end;
    else do;
        bonus = salary * 0.05;
        team  = "Business";
    end;
run;
```

**Important rules**

- Conditions run **top to bottom; the first true one wins** when you use `ELSE IF`.
- Without `ELSE`, every `IF` is tested separately.
- A missing numeric counts as smaller than any number. Test `missing()` first.
- `IF ... THEN` does **not** use `end;` for a single statement; `DO ... END;` is only needed for several.
- Compare with `SELECT/WHEN` for many categories (see Section 4).

---

#### 2.11 Creating multiple datasets from one source

```sas
data it_emp hr_emp other_emp;
    set employee;
    if      department = "IT" then output it_emp;
    else if department = "HR" then output hr_emp;
    else                           output other_emp;
run;
```

| Dataset | Rows |
|---|---:|
| `it_emp` | 3 (Ravi, Meena, Neha) |
| `hr_emp` | 2 (Asha, Karan) |
| `other_emp` | 2 (John, Priya) |

**Important rules**

- Without any `OUTPUT` statement, **every row goes to every listed dataset**.
- Once you write an explicit `OUTPUT dataset;`, SAS **stops** writing rows automatically; only what you output is saved.
- Use dataset options for different columns in each: `data it_emp(keep=employee_id salary) hr_emp(drop=salary);`.

---

#### 2.12 SAS formats and informats

**In simple words:** The computer keeps a **raw value**. A **format** is the *costume* it wears when displayed. An **informat** is the *translator* that reads text and converts it to the raw value.

| | Informat | Format |
|---|---|---|
| Direction | Text → stored value | Stored value → displayed text |
| Used in | `INPUT` statement, `INFORMAT` statement, `INPUT()` function | `FORMAT` statement, `PUT()` function, `PROC` steps |
| Example | `date9.` reads `15JAN2025` → 23756 | `date9.` shows 23756 as `15JAN2025` |
| Changes the stored data? | Yes (decides what is stored) | **No**, only appearance |

**Shape of a name:** letters + width + dot + decimals, e.g. `comma10.2`, `$12.`, `date9.` The **dot is mandatory**.

| Format / informat | Meaning | Value 1234567.891 or date 23756 shows as |
|---|---|---|
| `8.` / `8.2` | Plain number | `1234568` / `1234567.89` |
| `comma12.2` | Thousands separators | `1,234,567.89` |
| `dollar12.2` | Dollar sign + commas | `$1,234,567.89` |
| `percent8.1` | Percentage (value 0.256) | `25.6%` |
| `$10.` | Character, width 10 | text |
| `date9.` | DDMMMYYYY | `15JAN2025` |
| `ddmmyy10.` | DD/MM/YYYY | `15/01/2025` |
| `mmddyy10.` | MM/DD/YYYY | `01/15/2025` |
| `yymmdd10.` | YYYY-MM-DD | `2025-01-15` |
| `monyy7.` | Month-year | `JAN2025` |
| `worddate18.` | Words | `January 15, 2025` |
| `time8.` | HH:MM:SS | `14:30:00` |
| `datetime20.` | Date and time | `15JAN2025:14:30:00` |

**Example**

```sas
data fmt_demo;
    input txt_date :date9. amount;
    shown_ddmmyy = txt_date;
    shown_money  = amount;
    format txt_date date9.
           shown_ddmmyy ddmmyy10.
           shown_money dollar12.2;
    datalines;
15JAN2025 1234567.891
;
run;
```

| txt_date | shown_ddmmyy | shown_money |
|---|---|---|
| 15JAN2025 | 15/01/2025 | $1,234,567.89 |

All three show different **faces of the same stored numbers** (23756 and 1234567.891).

**Important rules**

- If your file has dates as `15/01/2025`, use informat `ddmmyy10.`; as `01/15/2025`, use `mmddyy10.`. The **wrong informat gives missing values or wrong dates.**
- Put a format in a DATA step to make it **permanent with the dataset**; put it in a PROC step to apply **only to that report**.
- Rounding in a format affects display only; the stored value is unchanged. Use `ROUND()` to change the value.

---

#### 2.13 User-defined formats with PROC FORMAT

**In simple words:** Create your own "lookup labels": show `HR` as "Human Resources", or turn salary numbers into bands, **without changing the data**.

**Syntax**

```sas
PROC FORMAT <LIBRARY=lib>;
    VALUE <$>fmtname   value-or-range = "label" ... ;
    INVALUE fmtname    "text" = number ... ;
    PICTURE fmtname    range = 'template' ... ;
RUN;
```

A character format name starts with `$`. Format names cannot end in a digit and have no more than 32 characters.

**Example**

```sas
proc format;
    value $deptfmt
        "HR"    = "Human Resources"
        "IT"    = "Information Technology"
        "Sales" = "Sales and Marketing"
        other   = "Other";

    value salband
        low -< 50000     = "Below 50K"
        50000 -< 60000   = "50K to under 60K"
        60000 - high     = "60K and above"
        .                = "Not available";
run;

proc print data=employee noobs;
    var employee_name department salary;
    format department $deptfmt. salary salband.;
run;
```

**Expected output**

| employee_name | department | salary |
|---|---|---|
| Asha | Human Resources | Below 50K |
| Ravi | Information Technology | 60K and above |
| Meena | Information Technology | 50K to under 60K |
| John | Sales and Marketing | 50K to under 60K |
| Priya | Sales and Marketing | Below 50K |
| Karan | Human Resources | Below 50K |
| Neha | Information Technology | Not available |

**Reading the range symbols**

| Symbol | Meaning |
|---|---|
| `a - b` | From a to b, both included |
| `a -< b` | From a up to but **not including** b |
| `low`, `high` | Smallest / largest possible value (`low` does **not** include missing numerics) |
| `other` | Everything not listed |
| `,` | Several values in one label: `"HR","Admin" = "Support"` |

**Informat example:** `INVALUE` turns text into numbers while reading.

```sas
proc format;
    invalue ratein "A"=4  "B"=3  "C"=2  other=.;
run;
data scores;
    input student $ grade_letter :ratein.;
    datalines;
Anil A
Beena C
;
run;
```

**Important rules**

- Ranges must **not overlap**.
- Applying a format to a variable never changes the stored value; grouping by a formatted variable in `PROC FREQ`/`MEANS` groups by the **displayed** label.
- A format must exist when you use it, otherwise `ERROR: Format ... not found`.

---

#### 2.14 Storing and reusing permanent formats

By default, formats you create live in `WORK.FORMATS` and **vanish when SAS closes**. To reuse them:

```sas
libname myfmt "/home/user/formats";            /* a folder to hold the format catalog */

proc format library=myfmt;                     /* saved as myfmt.formats */
    value $deptfmt "HR"="Human Resources" "IT"="Information Technology" other="Other";
run;

/* In any later session, tell SAS where to look: */
options fmtsearch=(myfmt work);

proc print data=employee;
    format department $deptfmt.;
run;
```

| Need | Tool |
|---|---|
| Save formats permanently | `PROC FORMAT LIBRARY=lib;` |
| Make SAS find them | `OPTIONS FMTSEARCH=(lib work);` |
| Move formats as data | `CNTLOUT=` (catalog → dataset) and `CNTLIN=` (dataset → catalog) |
| Open a dataset whose format catalog is missing | `OPTIONS NOFMTERR;` (shows raw values instead of failing) |

**Tip:** If you attach a user-defined format to variables in a **permanent dataset**, anyone opening that dataset needs access to the format catalog.

---

#### 2.15 IF versus WHERE

| | **WHERE** | **Subsetting IF** |
|---|---|---|
| Where it works | DATA step, **PROC steps**, dataset option | **DATA step only** |
| When it filters | **Before** a row enters the PDV (at the door) | **After** the row is read and earlier statements have run |
| Can use a variable **created in the same step** | **No** | **Yes** |
| Speed | Usually faster (fewer rows read) | Reads all rows first |
| Special operators (`IN`, `BETWEEN`, `LIKE`, `CONTAINS`, `IS MISSING`) | **Yes** | Standard comparisons and `IN` |
| With `MERGE` | Filters inputs **before** merging | Filters the merged result **after** |
| Several in one step | Last `WHERE` replaces earlier unless `SAME AND` | All `IF`s apply |

**Example showing the difference**

```sas
/* Works: IF can use a variable created above it */
data high_bonus;
    set employee;
    bonus = salary * 0.10;
    if bonus > 5000;              /* subsetting IF: keeps the row only if true */
run;
/* Rows kept: Ravi (6200), Meena (5800), John (5100) */

/* Fails: WHERE cannot see 'bonus' */
data high_bonus2;
    set employee;
    bonus = salary * 0.10;
    where bonus > 5000;           /* ERROR: Variable bonus is not on file WORK.EMPLOYEE */
run;
```

**Interview takeaway:** *"IF vs WHERE?"* → `WHERE` filters rows as they are read (works in PROC steps, faster, cannot use newly created variables); subsetting `IF` filters after the row is in the PDV (DATA step only, can use new variables). Do not confuse the two kinds of `IF`: `IF cond;` (no `THEN`) is the subsetting IF that drops rows, while `IF cond THEN ...;` only runs a statement conditionally and keeps every row.

---

### SESSION 3 — DATA INPUT, OUTPUT AND PDV

**Topics in this session:** 3.1 `INFILE` options toolkit · 3.2 Delimited files and custom delimiters · 3.3 Reading/writing TXT and CSV · 3.4 Reading/writing Excel · 3.5 Reading multiple Excel sheets · 3.6 PROC IMPORT vs DATA step · 3.7 Access, SQL Server and Oracle · 3.8 PROC DOWNLOAD / PROC UPLOAD · 3.9 HDFS / Hadoop · 3.10 `@` and `@@` · 3.11 Unstructured text → structured data · 3.12 Program Data Vector (PDV) · 3.13 Random observations · 3.14 Reading selected observations

> 🌐 **Reminder:** Database, Excel (XLSX), Hadoop and remote-server features depend on **licensed SAS components and your environment's setup**. If an example fails with "engine not found" or "not licensed", ask your SAS administrator which products are installed. Run `proc setinit; run;` to see licensed products in the log.

---

#### 3.1 The INFILE options toolkit

`INFILE` points a DATA step to an external text file; options control **how lines are read**.

| Option | Plain meaning |
|---|---|
| `DLM="," ` / `DLM="09"x` | The character separating values (`09`x = tab) |
| `DLMSTR="\|\|"` | A multi-character delimiter |
| `DSD` | "Delimiter-sensitive data": two delimiters in a row = a **missing value**; text inside **quotes** is one value (quotes removed); default delimiter becomes comma |
| `FIRSTOBS=n` | Start reading at line **n** (use `2` to skip a header line) |
| `OBS=n` | Stop after line **n** (counts file lines, including the header) |
| `MISSOVER` | If a line ends early, set unread variables to **missing** |
| `TRUNCOVER` | If a line ends early, keep a **partial** last value and set the rest missing |
| `PAD` | Pad short records with blanks (for fixed-width files) |
| `LRECL=n` | Maximum line length (raise it for very long lines; default is often 256 or 32767 depending on system) |
| `FLOWOVER` | (Default) if the line ends early, continue on the **next line**. Usually a surprise |
| `STOPOVER` | Treat a short line as an **error** and stop |
| `END=flag` | Creates a flag that becomes 1 on the last line |
| `ENCODING="utf-8"` | Tell SAS the file's character encoding |

**MISSOVER vs TRUNCOVER**

| Situation: field is `$10.` at columns 11–20, but the line ends at column 15 | Result |
|---|---|
| `MISSOVER` | Field = **missing** (SAS wanted 10 characters, did not get them) |
| `TRUNCOVER` | Field = the **5 characters that exist** |

> Use **`TRUNCOVER`** as the safe default for fixed-width and formatted input; use `MISSOVER` for plain list input where missing is the right answer.

---

#### 3.2 Delimited files and custom delimiters

**In simple words:** In a delimited file, a special character (comma, pipe, tab…) separates the fields.

| File type | `INFILE` options |
|---|---|
| Comma-separated (CSV) | `dsd` (default delimiter is a comma) |
| Pipe-separated | `dlm="\|" dsd` |
| Tab-separated | `dlm="09"x dsd` |
| Space-separated | nothing extra (space is the default delimiter) |
| Several delimiters allowed (comma or semicolon) | `dlm=",;"` |
| Multi-character delimiter (two pipes) | `dlmstr="\|\|"` |

**Why DSD matters:** Without it, an empty value (`,,`) would be skipped and the next value would slide into the wrong column. And a quoted comma such as `"Meena, K"` would split into two values.

**Example: a custom pipe-delimited file `emp_pipe.txt`**

```
employee_id|employee_name|department|salary
101|Asha|HR|45000
102|Ravi|IT|62000
103|Meena|IT|
```

```sas
filename emppipe "/home/user/data/emp_pipe.txt";

data emp_pipe;
    infile emppipe dlm="|" dsd firstobs=2 truncover;
    input employee_id employee_name :$12. department :$10. salary;
run;
```

| employee_id | employee_name | department | salary |
|---:|---|---|---:|
| 101 | Asha | HR | 45000 |
| 102 | Ravi | IT | 62000 |
| 103 | Meena | IT | . |

The empty last field becomes missing (`.`) because of `DSD` + `TRUNCOVER`.

---

#### 3.3 Reading and writing TXT and CSV files

**Reading a CSV with a DATA step (full control)**

File `employees.csv`:

```
employee_id,employee_name,department,salary,hire_date
101,Asha,HR,45000,15JAN2020
102,Ravi,IT,62000,03MAR2019
103,"Meena, K",IT,,21JUL2021
```

```sas
filename empcsv "/home/user/data/employees.csv";

data emp_csv;
    infile empcsv dsd dlm="," firstobs=2 truncover;
    input employee_id
          employee_name :$20.        /* :$20. = read as text, up to 20 characters */
          department    :$10.
          salary
          hire_date     :date9.;
    format hire_date date9.;
run;
```

| employee_id | employee_name | department | salary | hire_date |
|---:|---|---|---:|---|
| 101 | Asha | HR | 45000 | 15JAN2020 |
| 102 | Ravi | IT | 62000 | 03MAR2019 |
| 103 | Meena, K | IT | . | 21JUL2021 |

The **colon modifier** (`:`) in `employee_name :$20.` means "read until the next delimiter, but allow up to 20 characters". Without it, `$20.` would read exactly 20 columns and swallow the next fields.

**Reading only part of the file**

```sas
data first_two;
    infile empcsv dsd firstobs=2 obs=3 truncover;   /* file lines 2 and 3 only */
    input employee_id employee_name :$20. department :$10. salary hire_date :date9.;
run;
```

**Writing a delimited text file (`FILE` + `PUT`)**

```sas
data _null_;                                  /* _NULL_ = do not create a dataset */
    set employee;
    file "/home/user/out/emp_out.txt" dlm="|";
    if _n_ = 1 then put "id|name|department|salary";    /* header line */
    put employee_id employee_name department salary;
run;
```

Result file:

```
id|name|department|salary
101|Asha|HR|45000
102|Ravi|IT|62000
...
107|Neha|IT|.
```

**Writing a CSV file with PROC EXPORT**

```sas
proc export data=work.employee
            outfile="/home/user/out/employee.csv"
            dbms=csv replace;
run;
```

**Important rules**

- `PROC EXPORT` to CSV writes dates **using the variable's format** (`15JAN2020`); strip or apply formats if the receiver needs `YYYY-MM-DD`.
- In a `FILE`/`PUT` job, add `dsd` to `FILE` if values may contain commas: `file "x.csv" dsd;`.
- Missing numerics are written as `.` by `PUT`; use `PROC EXPORT` or `options missing=' ';` for blanks.

---

#### 3.4 Reading and writing Excel files

🔑 Excel `.xlsx` access (the `XLSX` engine and `DBMS=XLSX`) normally needs **SAS/ACCESS Interface to PC Files**. Check your licence.

**Method 1: `LIBNAME XLSX` (treat the workbook like a library; each sheet is a dataset)**

```sas
libname xl xlsx "/home/user/data/sales_book.xlsx";

proc contents data=xl._all_ nods;   /* lists the sheets */
run;

data work.q1_sales;                  /* READ sheet Q1 */
    set xl.Q1;
run;

data xl.employee_copy;               /* WRITE a new sheet into the workbook */
    set work.employee;
run;

libname xl clear;                    /* ALWAYS clear: releases the file lock */
```

Sheet names with spaces: `xl.'Sales Q1'n`.

**Method 2: `PROC IMPORT` / `PROC EXPORT`**

```sas
/* Read one sheet */
proc import datafile="/home/user/data/sales_book.xlsx"
            out=work.q1_sales dbms=xlsx replace;
    sheet="Q1";
    getnames=yes;
run;

/* Write a dataset to one sheet */
proc export data=work.employee
            outfile="/home/user/out/report.xlsx"
            dbms=xlsx replace;
    sheet="Employees";
run;
```

**No PC Files licence? Alternatives:** save the workbook as CSV and use `INFILE`/`PROC IMPORT DBMS=CSV` (Base SAS); for *writing* formatted reports to Excel, `ODS EXCEL` (Base SAS, 9.4+) works. It produces a report layout, not a raw data dump.

**Important rules**

- Excel column headers become variable names; spaces turn into underscores (depends on `VALIDVARNAME`).
- A column with mixed numbers and text can import as character or with missing values. Clean the sheet first.
- Close the workbook in Excel before SAS writes to it, or you get a file-lock error.

---

#### 3.5 Reading multiple Excel sheets

Suppose `quarters.xlsx` has sheets `Q1`, `Q2`, `Q3` with the same columns.

**Method A: stack them with `SET` (known sheet names)**

```sas
libname xl xlsx "/home/user/data/quarters.xlsx";

data work.all_quarters;
    length sheet_name $ 32;
    set xl.Q1 xl.Q2 xl.Q3 indsname=src;   /* INDSNAME= records which dataset a row came from */
    sheet_name = scan(src, 2, ".");        /* "XL.Q1" -> "Q1" */
run;

libname xl clear;
```

**Method B: unknown sheet names, loop with a macro** (full macro explained in Session 8)

```sas
proc sql noprint;
    select memname into :sheets separated by " "
    from dictionary.tables
    where libname = "XL";
quit;

%macro read_all;
    %local i s;
    %do i = 1 %to %sysfunc(countw(&sheets));
        %let s = %scan(&sheets, &i);
        proc append base=work.all_quarters data=xl.&s force; run;
    %end;
%mend;
%read_all
```

**Tip:** `PROC APPEND` is explained in Session 4; the macro pieces in Session 8.

---

#### 3.6 When to use PROC IMPORT and when to use a DATA step

| Question | `PROC IMPORT` | `DATA` step + `INFILE`/`INPUT` |
|---|---|---|
| Speed to write | Very fast, 5 lines | More lines |
| Control of **types** (IDs with leading zeros, dates) | Low; SAS **guesses** | **Full control** with informats |
| Control of **lengths** | Guessed from sample rows | You set them |
| Handles odd layouts (multi-line records, header text, fixed width) | No | **Yes** |
| Best for | One-time load of a tidy file | Repeated/production jobs, messy files |
| Risk | Types may change when new data arrives | Needs code changes if layout changes |

**Rule:** For a **daily job**, use a DATA step (the same file layout gives the same dataset every day).

---

#### 3.7 Access databases, SQL Server and Oracle

**In simple words:** With the right "engine", a database looks like a SAS library. You `SET` a table as if it were a SAS dataset.

🔑 Each connection needs the matching **SAS/ACCESS** product, plus the database client/drivers installed and configured (🌐 environment-specific).

```sas
/* Microsoft Access (Windows, PC Files) */
libname acc access "C:\data\sales.accdb";

/* SQL Server through ODBC: replace placeholders with your site's values */
libname sqlsrv odbc dsn="MyDsn" schema=dbo user="your_user" password="XXXXXXXX";

/* Oracle */
libname ora oracle user="your_user" password="XXXXXXXX" path="your_tns_alias" schema=hr;

/* Use like normal SAS data */
proc print data=ora.employees (obs=5); run;

libname ora clear;
```

> 🔒 **Security:** Never leave real passwords in code. Use your site's secure method (for example `authdomain=`, a protected include file, or an encoded password from `PROC PWENCODE`).

**Explicit pass-through: send native database SQL and get the result back**

```sas
proc sql;
    connect to oracle (user="your_user" password="XXXXXXXX" path="your_tns_alias");

    create table work.high_paid as
    select * from connection to oracle
        ( select employee_id, salary            /* this part is ORACLE SQL */
          from hr.employees
          where salary > 5000 );

    disconnect from oracle;
quit;
```

| Approach | Meaning | When |
|---|---|---|
| **LIBNAME engine** | Database tables look like SAS datasets | Everyday use; SAS often translates your `WHERE`/joins to database SQL automatically ("implicit pass-through") |
| **Explicit pass-through** | You write database-native SQL inside `CONNECT TO ... ( ... )` | Need DBMS-only functions, hints, or stored procedures |
| **Import into SAS first** | `create table work.x as select * from ora.t` | Small tables you will use repeatedly |

---

#### 3.8 PROC DOWNLOAD and PROC UPLOAD

**In simple words:** Move datasets **between your local SAS session and a remote SAS server** (copy down or copy up).

🔑 Requires **SAS/CONNECT** on both machines. 🌐 Needs server addresses, ports and authentication that your administrator provides.

```sas
options comamid=tcp;
%let remote_srv = server.example.com 7551;     /* placeholder: host and port */
signon remote_srv user=your_id;                /* you will be prompted for a password */

rsubmit;                                       /* the next lines run on the REMOTE server */
    libname remlib "/remote/data";
    proc download data=remlib.sales out=work.sales_local;     /* remote -> local */
    run;
endrsubmit;

rsubmit;
    proc upload data=work.employee out=remlib.employee_copy;  /* local -> remote */
    run;
endrsubmit;

signoff;
```

| Procedure | Direction |
|---|---|
| `PROC DOWNLOAD` | Remote → Local |
| `PROC UPLOAD` | Local → Remote |

Syntax details (`SIGNON` scripts, `INLIB=`/`OUTLIB=`, `CONNECTREMOTE=`) vary by version and site; follow your SAS/CONNECT documentation.

---

#### 3.9 HDFS connectivity and SAS environment requirements

**In simple words:** HDFS is Hadoop's big-data file system. SAS can read/write files there, or talk to Hive tables.

| Goal | What you need |
|---|---|
| Read/write **files** in HDFS | Base SAS + Hadoop client JAR files and config files; set `SAS_HADOOP_JAR_PATH` and `SAS_HADOOP_CONFIG_PATH` |
| Query **Hive** tables with `LIBNAME` | 🔑 **SAS/ACCESS Interface to Hadoop** + a reachable Hive server |
| Run HDFS commands from SAS | `PROC HADOOP` (needs the Hadoop client setup) |

```sas
/* Tell SAS where the Hadoop client files are (paths set by your administrator) */
options set=SAS_HADOOP_JAR_PATH="/opt/hadoop/jars";
options set=SAS_HADOOP_CONFIG_PATH="/opt/hadoop/conf";

/* Read a CSV stored in HDFS */
filename hdfsin hadoop "/user/analyst/sales.csv";

data work.sales_hdfs;
    infile hdfsin dsd firstobs=2 truncover;
    input product_id :$3. region :$5. sales_amount;
run;

/* Query Hive tables (needs SAS/ACCESS to Hadoop) */
libname hv hadoop server="hive-host.example.com" port=10000 schema=default user="your_user";
proc sql;  select count(*) from hv.sales;  quit;
```

If these fail, the cause is almost always the environment (missing JARs, wrong paths, firewall, Kerberos login), not the SAS code.

---

#### 3.10 Using `@` and `@@` in the INPUT statement

**In simple words:** Normally, after each `INPUT`, SAS jumps to the next line. These "line holders" tell SAS to **stay on the current line**.

| Symbol | Name | Holds the line until… | Typical use |
|---|---|---|---|
| `@` (single trailing) | Hold for the **next INPUT in the same row-iteration** | The DATA step iteration ends | Read a "record type" first, then decide how to read the rest |
| `@@` (double trailing) | Hold across **iterations** | The line is fully used up | **Several observations on one line** |

**Example 1: single `@` (peek, then decide)**

```sas
data mixed;
    length cust_name $ 10 emp_name $ 8;
    input rec_type $ @;                    /* read the first value and HOLD the line */
    if rec_type = "E" then input emp_id emp_name $ salary;
    else if rec_type = "C" then input cust_id cust_name $;
    datalines;
E 101 Asha 45000
C 1 Alpha
E 102 Ravi 62000
;
run;
```

| rec_type | emp_id | emp_name | salary | cust_id | cust_name |
|---|---:|---|---:|---:|---|
| E | 101 | Asha | 45000 | . | |
| C | . | | . | 1 | Alpha |
| E | 102 | Ravi | 62000 | . | |

**Example 2: double `@@` (many observations per line)**

```sas
data scores;
    input student_id score @@;
    datalines;
1 80 2 75 3 90
4 60 5 88
;
run;
```

| student_id | score |
|---:|---:|
| 1 | 80 |
| 2 | 75 |
| 3 | 90 |
| 4 | 60 |
| 5 | 88 |

Five observations came from two lines.

**Important rules**

- `@` is released automatically at the end of the iteration; `@@` is released only when the line is used up.
- If the data has an odd number of values, `@@` can trigger "SAS went to a new line when INPUT statement reached past the end of a line" and pair values wrongly. Always check counts.
- Don't mix `@@` with `MISSOVER`/`TRUNCOVER` carelessly; test the result.
- Don't confuse these with `@n` (column pointer, e.g. `input @10 salary 5.;`).

---

#### 3.11 Converting unstructured text into structured datasets

**In simple words:** Read each messy line as **one long text value**, then cut it into pieces using text functions.

**Raw lines (a log file)**

```
2025-01-15 ORDER=5001 CUST=1 AMT=1200
2025-01-17 ORDER=5002 CUST=1 AMT=800
```

```sas
data order_log;
    infile datalines truncover;
    length line $ 80;
    input line $char80.;                          /* the whole line, as text */

    log_date    = input(scan(line, 1, " "), yymmdd10.);
    order_id    = input(scan(scan(line, 2, " "), 2, "="), 8.);
    customer_id = input(scan(scan(line, 3, " "), 2, "="), 8.);
    amount      = input(scan(scan(line, 4, " "), 2, "="), 8.);

    format log_date date9.;
    drop line;
    datalines;
2025-01-15 ORDER=5001 CUST=1 AMT=1200
2025-01-17 ORDER=5002 CUST=1 AMT=800
;
run;
```

| log_date | order_id | customer_id | amount |
|---|---:|---:|---:|
| 15JAN2025 | 5001 | 1 | 1200 |
| 17JAN2025 | 5002 | 1 | 800 |

**How it works:** `SCAN(line,2," ")` gives `ORDER=5001`; scanning that again with `"="` gives `5001`; `INPUT(...,8.)` converts the text to a number.

**Tools for this job:** `SCAN`, `SUBSTR`, `FIND`/`INDEX`, `COMPRESS`, `TRANWRD` (Session 6), and Perl regular expressions `PRXPARSE`/`PRXMATCH`/`PRXPOSN` for complex patterns.

---

#### 3.12 Program Data Vector (PDV), explained with an example

**In simple words:** The PDV is a **one-row notepad in memory**. SAS reads one row at a time onto the notepad, runs your statements on it, then writes the notepad as one row of the new dataset, wipes the notepad (partly), and repeats.

**Example**

```sas
data pdv_demo;
    set employee(obs=2);
    bonus = salary * 0.10;
run;
```

**Phase 1: compile.** SAS builds the PDV columns: `_N_`, `_ERROR_`, `employee_id`, `employee_name`, `department`, `salary`, `hire_date`, `bonus`.

**Phase 2: execute (step by step)**

| Moment | `_N_` | employee_id | employee_name | department | salary | hire_date | bonus |
|---|---:|---:|---|---|---:|---:|---:|
| Iteration 1 starts | 1 | . | (blank) | (blank) | . | . | . |
| After `SET` reads row 1 | 1 | 101 | Asha | HR | 45000 | 21929 | . |
| After `bonus = ...` | 1 | 101 | Asha | HR | 45000 | 21929 | **4500** |
| End of step: row written to `pdv_demo` | | | | | | | |
| Iteration 2 starts | 2 | 101 | Asha | HR | 45000 | 21929 | **. (reset)** |
| After `SET` reads row 2 | 2 | **102** | **Ravi** | **IT** | **62000** | **21611** | . |
| After `bonus = ...` | 2 | 102 | Ravi | IT | 62000 | 21611 | **6200** |
| End of step: row written | | | | | | | |
| Iteration 3 | `SET` finds no more rows (`OBS=2`) → **step ends** | | | | | | |

(Dates are stored as numbers: 21929 = 15JAN2020, 21611 = 03MAR2019.)

**What this teaches**

1. `_N_` counts iterations. `_N_` and `_ERROR_` are in the PDV but **not written** to the dataset.
2. Variables **read by `SET`** keep their values between iterations until `SET` overwrites them.
3. Variables **created by assignment** (like `bonus`) are **reset to missing** at the start of each iteration. This is why `RETAIN` exists (Session 5).
4. The **first** appearance of a variable decides its **type and length** (compile time).
5. At the end of the DATA step code, SAS performs an **implicit `OUTPUT`** then an implicit return to the top. An explicit `OUTPUT` statement switches off the automatic output.

**Other PDV items:** `FIRST.var` / `LAST.var` (with `BY`), flags from `IN=`, and `END=` flags are also placed in the PDV but are not saved.

**Interview takeaway:** *"What is the PDV?"* → A memory area SAS builds at compile time; each DATA step iteration loads one row into it, applies your statements, and writes it to the output dataset.

---

#### 3.13 Selecting random observations

**Method 1: `PROC SURVEYSELECT`** (🔑 SAS/STAT)

```sas
proc surveyselect data=employee
                  out=emp_sample
                  method=srs        /* simple random sampling without replacement */
                  sampsize=3        /* EXACTLY 3 rows */
                  seed=12345;       /* same seed = same sample every time */
run;
```

| Option | Meaning |
|---|---|
| `METHOD=SRS` | Simple random sample without replacement |
| `SAMPSIZE=n` | **Exact** number of rows to select (use this when the size must be precise) |
| `SAMPRATE=p` | Fraction of rows (e.g. `0.2` = 20%); the count is **derived** from the rate, not typed by you |
| `METHOD=BERNOULLI` + `RATE=` | Each row is chosen independently, so the **sample size varies** from run to run |
| `SEED=n` | Makes the sample **repeatable** |
| `OUTALL` | Output all rows with a flag column `Selected` |
| `STRATA` | Sample separately within groups (data must be sorted by that variable) |

The result has 3 rows; *which* 3 depends on the seed and SAS version, so your rows may differ from someone else's.

**Method 2: Base SAS only (no SAS/STAT), exact size**

```sas
data work.tmp;
    call streaminit(12345);              /* set the random seed */
    set employee;
    r = rand("uniform");                 /* random number 0-1 per row */
run;

proc sort data=work.tmp;  by r;  run;    /* shuffle */

data work.emp_sample3;
    set work.tmp(obs=3 drop=r);          /* take the first 3 shuffled rows */
run;
```

**Important rules**

- Without a seed, you get a different sample each run, which cannot be reproduced. Always set one in reports and tests.
- `SAMPSIZE` larger than the number of rows gives an error (for `METHOD=SRS`).

---

#### 3.14 Reading selected observations from one dataset into another

| Goal | Code | Rows read from EMPLOYEE (1 Asha, 2 Ravi, 3 Meena, 4 John, 5 Priya, 6 Karan, 7 Neha) |
|---|---|---|
| A **range** of rows | `set employee(firstobs=3 obs=5);` | Meena, John, Priya |
| First *n* rows | `set employee(obs=3);` | Asha, Ravi, Meena |
| By **condition** | `set employee(where=(department="IT"));` | Ravi, Meena, Neha |
| Specific positions by counter | `set employee; if _n_ in (1,3,5);` | Asha, Meena, Priya (reads all rows) |
| **Direct access** by row number | see below | Ravi, John, Karan |

**Direct access with `POINT=`**

```sas
data picked;
    do row = 2, 4, 6;
        set employee point=row;     /* jump straight to that row number */
        output;
    end;
    stop;                           /* REQUIRED: SAS never sees "end of file" with POINT= */
run;
```

**Important rules**

- `OBS=` is the **last row number to read**, not the count. `firstobs=3 obs=5` reads **3 rows** (3, 4, 5).
- With `POINT=`, **always** add `STOP;`, or the step loops forever.
- `WHERE=` filters **before** reading (efficient); `IF _N_ ...` reads everything first.
- Datasets that live in databases (and views) may not support `POINT=`.

---

### SESSION 4 — JOINS, MERGING, DATA MODELING AND PROC SQL

**Groups in this session:** **A.** Vertical joins and appending · **B.** Horizontal joins and merging · **C.** Keys, relationships and data modeling · **D.** PROC SQL (tables, schema changes, views, stored procedures)

Session 7 builds on part D with a practical query-by-query reference; here you learn the building blocks.

---

#### PART A — Vertical joins and appending

**In simple words:** Vertical = **stacking tables on top of each other** (same kind of columns, more rows). Think "paste the February sheet under the January sheet".

### 4.1 Concatenating with the SET statement

**Syntax**

```sas
DATA combined;
    SET ds1 ds2 ds3;
RUN;
```

**Example: stack January and February sales**

```sas
data sales_jan;  set sales;  where month(transaction_date) = 1;  run;   /* 3 rows */
data sales_feb;  set sales;  where month(transaction_date) = 2;  run;   /* 3 rows */

data sales_all;
    set sales_jan sales_feb;        /* rows of sales_jan first, then sales_feb */
run;
```

**Expected output (6 rows)**

| product_id | region | sales_amount | transaction_date |
|---|---|---:|---|
| P1 | East | 1000 | 10JAN2025 |
| P1 | West | 800 | 12JAN2025 |
| P2 | East | 600 | 15JAN2025 |
| P2 | West | 900 | 03FEB2025 |
| P3 | East | 300 | 14FEB2025 |
| P3 | West | 450 | 20FEB2025 |

**Important rules**

- Variables are matched **by name**, not by position.
- **Order of datasets** in `SET` = order of rows in the result.
- With a `BY` statement (`set a b; by product_id;`), rows are **interleaved** in sorted order (inputs must be sorted).
- Add `INDSNAME=src` to record which dataset each row came from.

### 4.2 PROC APPEND and its important behaviour

**In simple words:** Add the new rows to the **end of a big table** without re-reading the big table, so it is much faster for big history tables.

```sas
proc append base=sales_all            /* the big table that grows */
            data=sales_new;           /* the small table of new rows */
run;
```

| Behaviour | Detail |
|---|---|
| Speed | Reads only `DATA=` (the new rows), **not** the whole `BASE=` |
| `BASE=` does not exist | SAS **creates** it from `DATA=` |
| `DATA=` has a variable **not in** `BASE=` | **ERROR**, nothing appended, unless you add `FORCE` (the extra variable is **dropped**) |
| `BASE=` has a variable **not in** `DATA=` | OK. Those values are **missing** in the new rows |
| Character variable **longer** in `DATA=` than in `BASE=` | ERROR unless `FORCE` (values are **truncated**) |
| **Type** mismatch (number vs text) | Problem: fix the types first (`FORCE` can silently lose the column) |

**`SET` vs `PROC APPEND`**

| | `DATA ...; SET a b;` | `PROC APPEND` |
|---|---|---|
| Creates a new dataset | Yes (a full new copy) | No; **adds to the existing** `BASE=` |
| Reads the big dataset | Yes (slow for big data) | No (fast) |
| Can change values while stacking | Yes | No |
| Handles different structures | Gracefully (fills missing) | Strict; needs `FORCE` |

### 4.3 Different column structures and missing columns

```sas
data sales_feb_disc;
    set sales_feb;
    discount = 0.05;                   /* extra column only in this table */
run;

data sales_mixed;
    set sales_jan sales_feb_disc;
run;
```

| product_id | region | sales_amount | transaction_date | discount |
|---|---|---:|---|---:|
| P1 | East | 1000 | 10JAN2025 | . |
| P1 | West | 800 | 12JAN2025 | . |
| P2 | East | 600 | 15JAN2025 | . |
| P2 | West | 900 | 03FEB2025 | 0.05 |
| P3 | East | 300 | 14FEB2025 | 0.05 |
| P3 | West | 450 | 20FEB2025 | 0.05 |

**Rules for mismatches (SET)**

| Mismatch | What SAS does |
|---|---|
| Column missing in some datasets | Fills **missing** (`.` or blank) |
| Same name, **different type** | **ERROR** ("variable has been defined as both character and numeric"). Convert with `INPUT()` / `PUT()` first |
| Same character name, **different length** | The **first dataset's** length wins; longer values from later datasets are **cut off**. Set `LENGTH` first to be safe |
| Same name but different **label/format** | First dataset's attributes win |
| Different **column names** for the same thing | Use `RENAME=` so they match before stacking: `set a b(rename=(amt=amount));` |

### 4.4 Industry examples

| Industry | Vertical combine |
|---|---|
| Retail | Append each day's store transactions to a master sales history |
| Banking | Stack monthly account snapshots into a time series |
| Healthcare | Combine patient visit files from several hospitals (rename/convert so columns match) |
| Insurance | Combine regional claims datasets before fraud analysis |

---

#### PART B — Horizontal joins and merging

**In simple words:** Horizontal = **adding columns by matching a key**, like `VLOOKUP`: bring customer details next to each order.

### 4.5 SAS MERGE with BY, and the sorting requirement

**Syntax**

```sas
PROC SORT DATA=a; BY key; RUN;
PROC SORT DATA=b; BY key; RUN;

DATA merged;
    MERGE a(IN=ina) b(IN=inb);
    BY key;
    ...
RUN;
```

- `IN=name` creates a temporary 1/0 flag: **1 if that dataset contributed to the current row**. Flags are not saved in the output.
- **Both datasets must be sorted by the `BY` variables** (or already in that order); otherwise: `ERROR: BY variables are not properly sorted`.
- `BY` variables must have **the same name and type** in both datasets (rename if needed).

**Example data**: CUSTOMER (ids 1–5) and ORDERS (customers 1, 1, 2, 3, 3, **6**).

**Join types with MERGE**

| Join | Code | Rows you get |
|---|---|---|
| **Inner** (match in both) | `if ina and inb;` | 5 orders (5001–5005) with customer details |
| **Left** (all customers) | `if ina;` | Inner rows + customers **4, 5** (no order) |
| **Right** (all orders) | `if inb;` | Inner rows + order **5006** (no customer) |
| **Full** (everything) | *(no IF)* | 8 rows: 5 matches + customers 4, 5 + order 5006 |
| Only unmatched on the left | `if ina and not inb;` | Customers 4 and 5 |
| Only unmatched on the right | `if inb and not ina;` | Order 5006 |

```sas
proc sort data=customer out=cust_s;  by customer_id;  run;
proc sort data=orders   out=ord_s;   by customer_id;  run;

data cust_orders_inner;
    merge cust_s(in=c) ord_s(in=o);
    by customer_id;
    if c and o;                               /* inner join */
run;
```

**Expected output**

| customer_id | customer_name | city | credit_limit | order_id | order_date | amount |
|---:|---|---|---:|---:|---|---:|
| 1 | Alpha_Corp | Mumbai | 50000 | 5001 | 05JAN2025 | 1200 |
| 1 | Alpha_Corp | Mumbai | 50000 | 5002 | 17JAN2025 | 800 |
| 2 | Beta_Traders | Delhi | 30000 | 5003 | 20JAN2025 | 1500 |
| 3 | Gamma_Stores | Mumbai | 70000 | 5004 | 02FEB2025 | 2200 |
| 3 | Gamma_Stores | Mumbai | 70000 | 5005 | 14FEB2025 | 400 |

**Other important rules**

- **Same-named non-key variables** in both datasets: the value from the **later** dataset in the `MERGE` overwrites the earlier one. Rename one to keep both.
- `MERGE` **without `BY`** just glues row 1 to row 1, row 2 to row 2 ("one-to-one reading"). This is almost always a mistake.
- Variable order in the output: the columns of the first dataset first.

### 4.6 DATA step MERGE versus PROC SQL joins

| | DATA step `MERGE` | `PROC SQL` join |
|---|---|---|
| Needs sorting first | **Yes** | **No** |
| Key column names | Must be **identical** | Can differ (`on a.cust = b.customer_id`) |
| Many-to-many with repeats | **Matches row-by-row** (not all combinations) | **All combinations** (Cartesian within key) |
| Join conditions | Equality on `BY` variables only | Any condition (`>`, `between`, …) |
| Can add new calculations in the same step | Yes (DATA step logic) | Yes (expressions, `CASE`) |
| Output | Key shown once | You choose columns; both key columns may appear (use `COALESCE`) |
| Typical use | Large sorted data, sequential logic (`FIRST.`, `RETAIN`) | Ad hoc joins, conditions, multiple tables at once |

### 4.7 Duplicate keys: MERGE is not the same as a SQL JOIN

```sas
data a;  input id x;  datalines;
1 10
1 20
2 30
;
run;
data b;  input id y;  datalines;
1 100
1 200
3 300
;
run;

/* DATA step MERGE */
data m;  merge a b;  by id;  run;

/* SQL FULL JOIN */
proc sql;
    create table j as
    select coalesce(a.id, b.id) as id, a.x, b.y
    from a full join b on a.id = b.id
    order by id, x, y;
quit;
```

**MERGE result: 4 rows (id 1's rows are paired one-to-one, in order)**

| id | x | y |
|---:|---:|---:|
| 1 | 10 | 100 |
| 1 | 20 | 200 |
| 2 | 30 | . |
| 3 | . | 300 |

**SQL result: 6 rows (id 1 is every x with every y: 2 × 2 = 4 rows)**

| id | x | y |
|---:|---:|---:|
| 1 | 10 | 100 |
| 1 | 10 | 200 |
| 1 | 20 | 100 |
| 1 | 20 | 200 |
| 2 | 30 | . |
| 3 | . | 300 |

**Another surprise:** if dataset A has 3 rows for an id and B has 2, `MERGE` keeps the **last value of B** and reuses it for A's third row. (`y` for the third row = 200.) SAS prints the log note *"MERGE statement has more than one data set with repeats of BY values"* when both sides repeat. Treat that note as a warning.

**Interview takeaway:** *"Is MERGE the same as a JOIN?"* → No. For repeated keys on both sides, `MERGE` pairs rows sequentially, while SQL returns all combinations.

### 4.8 INNER, LEFT, RIGHT and FULL JOIN in PROC SQL

```sas
proc sql;
    /* INNER: only matches */
    select c.customer_id, c.customer_name, o.order_id, o.amount
    from customer as c inner join orders as o
         on c.customer_id = o.customer_id;

    /* LEFT: all customers, orders if any */
    select c.customer_id, c.customer_name, o.order_id, o.amount
    from customer as c left join orders as o
         on c.customer_id = o.customer_id
    order by c.customer_id, o.order_id;

    /* RIGHT: all orders, customer details if any */
    select coalesce(c.customer_id, o.customer_id) as customer_id,
           c.customer_name, o.order_id, o.amount
    from customer as c right join orders as o
         on c.customer_id = o.customer_id;

    /* FULL: everything from both */
    select coalesce(c.customer_id, o.customer_id) as customer_id,
           c.customer_name, o.order_id, o.amount
    from customer as c full join orders as o
         on c.customer_id = o.customer_id
    order by 1, 3;
quit;
```

**LEFT JOIN result (7 rows)**

| customer_id | customer_name | order_id | amount |
|---:|---|---:|---:|
| 1 | Alpha_Corp | 5001 | 1200 |
| 1 | Alpha_Corp | 5002 | 800 |
| 2 | Beta_Traders | 5003 | 1500 |
| 3 | Gamma_Stores | 5004 | 2200 |
| 3 | Gamma_Stores | 5005 | 400 |
| 4 | Delta_Mart | . | . |
| 5 | Echo_Retail | . | . |

**FULL JOIN adds one more row** compared with the left join: `6 | (blank) | 5006 | 900`, giving 8 rows.

| Join | Keeps |
|---|---|
| `INNER JOIN` | Only rows with a match in both |
| `LEFT JOIN` | All left rows + matching right rows (right columns missing if none) |
| `RIGHT JOIN` | All right rows + matching left rows |
| `FULL JOIN` | All rows from both sides |

### 4.9 Unmatched observations and anti-join patterns

**In simple words:** "Which customers never ordered?" = rows in the left table with **no partner** on the right. This is an **anti-join**.

```sas
/* Pattern 1: LEFT JOIN + IS NULL */
proc sql;
    select c.customer_id, c.customer_name
    from customer as c left join orders as o
         on c.customer_id = o.customer_id
    where o.order_id is null;
quit;

/* Pattern 2: NOT EXISTS (behaves the same in SAS and databases) */
proc sql;
    select customer_id, customer_name
    from customer as c
    where not exists (select 1 from orders as o
                      where o.customer_id = c.customer_id);
quit;

/* Pattern 3: NOT IN (works, but see the note below about missing values) */
proc sql;
    select customer_id, customer_name
    from customer
    where customer_id not in (select customer_id from orders);
quit;

/* DATA step version */
data no_orders;
    merge cust_s(in=c) ord_s(in=o);
    by customer_id;
    if c and not o;
run;
```

All four return **customers 4 (Delta_Mart) and 5 (Echo_Retail)**.

Orders **without** a customer (data-quality problem): `... from orders o left join customer c on ... where c.customer_id is null;` → order **5006**.

> **`NOT IN` and missing values:** in database SQL, `NOT IN` returns **no rows at all** if the subquery returns a `NULL`. SAS datasets treat a missing value as an ordinary value, so results can **differ between SAS data and a database**. `NOT EXISTS` and the `LEFT JOIN ... IS NULL` pattern behave the same everywhere, so prefer them.

### 4.10 Multiple-column joins

Join on **two keys** at once. Extra dataset TARGETS:

```sas
data targets;
    input product_id :$3. region :$5. target_amount;
    datalines;
P1 East 900
P1 West 1000
P2 East 500
P3 West 400
;
run;

proc sql;
    select s.product_id, s.region, s.sales_amount, t.target_amount
    from sales as s left join targets as t
         on s.product_id = t.product_id and s.region = t.region
    order by s.product_id, s.region;
quit;
```

| product_id | region | sales_amount | target_amount |
|---|---|---:|---:|
| P1 | East | 1000 | 900 |
| P1 | West | 800 | 1000 |
| P2 | East | 600 | 500 |
| P2 | West | 900 | . |
| P3 | East | 300 | . |
| P3 | West | 450 | 400 |

DATA step equivalent: sort both by `product_id region` and write `by product_id region;`.

### 4.11 Self joins and cross joins

**Self join:** join a table **to itself**, e.g. employee → manager.

```sas
data emp_mgr;
    input emp_id name :$8. manager_id;
    datalines;
1 Asha .
2 Ravi 1
3 Meena 1
4 John 2
;
run;

proc sql;
    select e.name as employee, m.name as manager
    from emp_mgr as e left join emp_mgr as m
         on e.manager_id = m.emp_id;
quit;
```

| employee | manager |
|---|---|
| Asha | (blank) |
| Ravi | Asha |
| Meena | Asha |
| John | Ravi |

The same table needs **two different aliases** (`e` and `m`).

**Cross join:** every row of A with every row of B (A × B). Use it to build all combinations.

```sas
proc sql;
    select r.region, p.product_id
    from (select distinct region from sales)     as r
         cross join
         (select distinct product_id from sales) as p
    order by r.region, p.product_id;
quit;
```

Result: **6 rows** (2 regions × 3 products): East-P1, East-P2, East-P3, West-P1, West-P2, West-P3.

> A join with **no `ON` condition** silently becomes a cross join and can create huge tables.

### 4.12 Subqueries with practical examples

A **subquery** is a query inside another query.

```sas
proc sql;
    /* 1. Scalar subquery: employees paid above the company average */
    select employee_name, salary
    from employee
    where salary > (select avg(salary) from employee);

    /* 2. IN subquery: customers who placed an order over 1000 */
    select customer_name
    from customer
    where customer_id in (select customer_id from orders where amount > 1000);

    /* 3. Correlated EXISTS: customers who have at least one order */
    select customer_name
    from customer as c
    where exists (select 1 from orders as o where o.customer_id = c.customer_id);

    /* 4. Inline view: total ordered per customer, then join to names */
    select c.customer_name, t.total_amount
    from customer as c
         inner join (select customer_id, sum(amount) as total_amount
                     from orders group by customer_id) as t
         on c.customer_id = t.customer_id;
quit;
```

| Query | Result |
|---|---|
| 1 | Ravi (62,000), Meena (58,000). The average is 52,000 (the missing salary is ignored) |
| 2 | Alpha_Corp, Beta_Traders, Gamma_Stores |
| 3 | Alpha_Corp, Beta_Traders, Gamma_Stores |
| 4 | Alpha_Corp 2000, Beta_Traders 1500, Gamma_Stores 2600 |

---

#### PART C — Keys, relationships and data modeling

### 4.13 Primary and foreign keys

| Term | Plain meaning | Example |
|---|---|---|
| **Primary key (PK)** | Column(s) that **uniquely identify** each row; never missing | `customer_id` in CUSTOMER |
| **Foreign key (FK)** | A column that **points to** a primary key in another table | `customer_id` in ORDERS |
| **Referential integrity** | Every FK value must exist as a PK in the parent | Order 5006 **breaks** it (customer 6 does not exist) |

SAS datasets do **not** enforce keys unless you define constraints (see the constraints example at the end of 4.27). Many SAS tables are "flat files" with duplicate keys, so always check with `PROC SQL`: `select customer_id, count(*) from customer group by 1 having count(*) > 1;`.

### 4.14 One-to-one, one-to-many and many-to-many

| Relationship | Meaning | Example | Join behaviour |
|---|---|---|---|
| **One-to-one** | 1 row ↔ 1 row | EMPLOYEE ↔ EMPLOYEE_BADGE | Result rows = same count |
| **One-to-many** | 1 parent ↔ many children | 1 CUSTOMER → many ORDERS | Parent values repeat on each child row |
| **Many-to-many** | Many ↔ many | ORDERS ↔ PRODUCTS (an order has many products; a product is in many orders) | Needs a **bridge table** (ORDER_ITEMS) holding both keys; joining without it **multiplies** rows |

```
 CUSTOMER 1 ───< ORDERS >───< ORDER_ITEMS >─── 1 PRODUCT
 (parent)       (one-to-many)   (bridge for many-to-many)
```

### 4.15 Fact and dimension tables

| | **Fact table** | **Dimension table** |
|---|---|---|
| Stores | **Events / measurements** (numbers to add up) | **Descriptions** (who, what, where, when) |
| Example here | ORDERS, SALES (`amount`, `sales_amount`) | CUSTOMER, PRODUCT, REGION, a calendar table |
| Size | Large, grows daily | Smaller, changes slowly |
| Keys | Foreign keys to every dimension | Primary key |

### 4.16 Star schema and snowflake schema

```
STAR SCHEMA                                SNOWFLAKE SCHEMA

   CUSTOMER      PRODUCT                   CUSTOMER      PRODUCT ──► CATEGORY ──► DEPARTMENT
        \          /                            \          /
         \        /                              \        /
          SALES_FACT                              SALES_FACT
         /        \                              /        \
     REGION      CALENDAR                    REGION      CALENDAR
```

| | **Star** | **Snowflake** |
|---|---|---|
| Dimensions | **Flat** (denormalised: one wide table per dimension) | **Split** into sub-tables (normalised) |
| Joins needed | Fewer, faster queries | More joins |
| Storage / duplication | Some repeated text | Less repetition |
| Best for | Reporting and BI | Complex hierarchies, strict data quality |

### 4.17 Industry-oriented data modeling examples

| Industry | Fact table | Dimensions |
|---|---|---|
| Retail | SALES (amount, quantity) | PRODUCT, STORE/REGION, CUSTOMER, DATE |
| Banking | TRANSACTIONS (amount) | ACCOUNT, CUSTOMER, BRANCH, DATE, TRANSACTION_TYPE |
| Healthcare | VISITS / CLAIMS (cost, length of stay) | PATIENT, DOCTOR, HOSPITAL, DIAGNOSIS, DATE |
| Insurance | CLAIMS (claim amount) | POLICY, CUSTOMER, AGENT, DATE |

**A tiny star-schema query using this guide's data:** total order amount by city (fact ORDERS, dimension CUSTOMER).

```sas
proc sql;
    select c.city, sum(o.amount) as total_amount
    from orders as o inner join customer as c
         on o.customer_id = c.customer_id
    group by c.city
    order by total_amount desc;
quit;
```

| city | total_amount |
|---|---:|
| Mumbai | 4600 |
| Delhi | 1500 |

(Mumbai = customer 1: 1200+800, plus customer 3: 2200+400 = 4600. Order 5006 is dropped by the inner join because customer 6 has no dimension row.)

---

#### PART D — PROC SQL

**In simple words:** `PROC SQL` lets you use SQL inside SAS. The tables are SAS datasets. Every `PROC SQL` block ends with **`QUIT;`** (not `RUN;`), and each statement ends with `;`.

### 4.18 Creating tables and inserting values

```sas
proc sql;
    /* Define a table: name, type and length of each column */
    create table work.product (
        product_id   char(3),
        product_name char(15),
        category     char(12),
        unit_price   num format=8.2
    );

    /* Insert method 1: VALUES (one row per clause; order of columns = table order) */
    insert into work.product
        values ('P1', 'Pen',      'Stationery', 10.50)
        values ('P2', 'Notebook', 'Stationery', 45.00);

    /* Insert method 2: SET (name each column; order does not matter) */
    insert into work.product
        set product_id='P3', product_name='Marker', category='Stationery', unit_price=25;

    /* Insert method 3: rows from a query */
    insert into work.product
        select 'P4', 'Stapler', 'Office', 120 from work.product(obs=1);
quit;
```

| product_id | product_name | category | unit_price |
|---|---|---|---:|
| P1 | Pen | Stationery | 10.50 |
| P2 | Notebook | Stationery | 45.00 |
| P3 | Marker | Stationery | 25.00 |
| P4 | Stapler | Office | 120.00 |

| SAS type word | Meaning |
|---|---|
| `char(n)` / `varchar(n)` | Text; `n` = length |
| `num` / `numeric` / `integer` / `decimal` | All stored as SAS numeric |
| `date` | Numeric, with a date format (`date9.` by default) |

### 4.19 Adding, dropping and modifying columns; renaming columns

```sas
proc sql;
    alter table work.product add stock_qty num;               /* add a column (values missing) */
    alter table work.product modify unit_price num format=10.2;  /* change format/length */
    alter table work.product drop stock_qty;                  /* drop a column */
quit;
```

**Renaming a column: `PROC SQL` has no `ALTER TABLE ... RENAME` in Base SAS.** Use one of these:

```sas
/* (a) PROC DATASETS: rename in place */
proc datasets library=work nolist;
    modify product;
    rename unit_price = price;
quit;

/* (b) Alias while building a new table */
proc sql;
    create table work.product2 as
    select product_id, product_name, category, price as unit_price
    from work.product;
quit;

/* (c) Dataset option RENAME= */
proc sql;
    create table work.product3 as
    select * from work.product(rename=(price=unit_price));
quit;
```

Check syntax against your SAS version and engine. For databases (🌐), rename and other schema changes depend on what the **database engine** allows.

### 4.20 Dropping, deleting and truncating

| Statement | What it does | Table structure | Rows |
|---|---|---|---|
| `CREATE TABLE ... AS SELECT` | Builds a **new** table from a query | New table | New rows |
| `INSERT INTO` | **Adds** rows | Unchanged | Added |
| `UPDATE ... SET ... WHERE` | **Changes values** in existing rows | Unchanged | Same count |
| `DELETE FROM ... WHERE` | **Removes rows** (no `WHERE` = all rows) | **Kept** | Removed |
| `DROP TABLE` | Deletes the **whole table** | **Gone** | Gone |
| `TRUNCATE TABLE` | Quickly empties a table | Kept | All removed. 🌐 **Not supported by `PROC SQL` on SAS datasets.** Available in many databases (use explicit pass-through) |

```sas
proc sql;
    delete from work.product where product_id = 'P4';   /* remove selected rows */
    delete from work.product;                           /* remove ALL rows, keep structure (SAS's way to "truncate") */
    drop table work.product3;                           /* delete the table itself */
quit;
```

> `DELETE` with no `WHERE` removes **every row**. `DROP TABLE` cannot be undone. Always test with a copy.

### 4.21 Creating tables from existing tables; with filtered records; sorting and summarising

```sas
proc sql;
    /* Copy structure AND data */
    create table work.emp_copy as select * from employee;

    /* Copy structure only (zero rows) */
    create table work.emp_empty like employee;

    /* Filtered copy */
    create table work.it_emp as
    select employee_id, employee_name, salary
    from employee
    where department = 'IT'
    order by salary desc;

    /* Summary table */
    create table work.dept_summary as
    select department,
           count(*)       as headcount,
           avg(salary)    as avg_salary format=comma10.0,
           sum(salary)    as total_salary format=comma10.0
    from employee
    group by department
    order by department;
quit;
```

**`dept_summary` result**

| department | headcount | avg_salary | total_salary |
|---|---:|---:|---:|
| HR | 2 | 46,000 | 92,000 |
| IT | 3 | 60,000 | 120,000 |
| Sales | 2 | 50,000 | 100,000 |

Notice: `count(*)` counts **all rows** (IT = 3 including Neha), but `avg(salary)` and `sum(salary)` **ignore the missing** salary (IT average = (62,000 + 58,000) / 2 = 60,000). Use `count(salary)` to count only non-missing values.

### 4.22 WHERE versus HAVING

| | `WHERE` | `HAVING` |
|---|---|---|
| Filters | **Rows**, **before** grouping | **Groups**, **after** grouping |
| Can use summary functions (`avg`, `sum`) | **No** | **Yes** |
| Speed | Faster (fewer rows to group) | Slower |

```sas
proc sql;
    select department, avg(salary) as avg_salary
    from employee
    where hire_date >= '01JAN2018'd           /* row filter: before grouping */
    group by department
    having avg(salary) > 48000;               /* group filter: after grouping */
quit;
```

| department | avg_salary |
|---|---:|
| IT | 60000 |
| Sales | 50000 |

(HR averages 46,000 and is dropped by `HAVING`. Every employee was hired on or after 01JAN2018, so here `WHERE` removes nobody; it is shown only to illustrate the order: filter rows first, then group, then filter groups.)

`'01JAN2018'd` is a **date literal**: SAS converts it to the number 21185 (days since 01JAN1960).

### 4.23 CASE-WHEN and nested CASE

```sas
proc sql;
    select employee_name, department, salary,
           case
               when salary is null     then 'Unknown'
               when salary >= 60000    then 'High'
               when salary >= 50000    then 'Medium'
               else                         'Low'
           end as salary_band,

           /* Nested CASE */
           case department
               when 'IT' then
                    case when salary >= 60000 then 'IT-Senior' else 'IT-Regular' end
               else 'Non-IT'
           end as team_level
    from employee;
quit;
```

| employee_name | department | salary | salary_band | team_level |
|---|---|---:|---|---|
| Asha | HR | 45,000 | Low | Non-IT |
| Ravi | IT | 62,000 | High | IT-Senior |
| Meena | IT | 58,000 | Medium | IT-Regular |
| John | Sales | 51,000 | Medium | Non-IT |
| Priya | Sales | 49,000 | Low | Non-IT |
| Karan | HR | 47,000 | Low | Non-IT |
| Neha | IT | . | Unknown | IT-Regular |

**Rules:** `CASE` checks `WHEN`s **in order** and stops at the first true one. Always test for missing **first**. Without an `ELSE`, unmatched rows get missing.

### 4.24 Calculated columns and CALCULATED

```sas
proc sql;
    select employee_name,
           salary,
           salary * 0.10            as bonus,
           salary + calculated bonus as total_pay      /* reuse the alias in the same SELECT */
    from employee
    where calculated bonus > 5000;                     /* ... and in WHERE */
quit;
```

| employee_name | salary | bonus | total_pay |
|---|---:|---:|---:|
| Ravi | 62,000 | 6200 | 68200 |
| Meena | 58,000 | 5800 | 63800 |
| John | 51,000 | 5100 | 56100 |

`CALCULATED` is a **SAS extension** to SQL. Standard SQL does not allow using an alias in the same `SELECT`/`WHERE`; you would repeat the expression or use a subquery.

### 4.25 COALESCE and missing-value handling

`COALESCE(a, b, c)` returns the **first non-missing** argument.

```sas
proc sql;
    select customer_name,
           credit_limit,
           coalesce(credit_limit, 0)               as credit_clean,
           coalesce(credit_limit, 10000)           as credit_default
    from customer;
quit;
```

| customer_name | credit_limit | credit_clean | credit_default |
|---|---:|---:|---:|
| Alpha_Corp | 50,000 | 50,000 | 50,000 |
| Beta_Traders | 30,000 | 30,000 | 30,000 |
| Gamma_Stores | 70,000 | 70,000 | 70,000 |
| Delta_Mart | . | 0 | 10,000 |
| Echo_Retail | 20,000 | 20,000 | 20,000 |

| Missing-value tool | Use |
|---|---|
| `IS MISSING` / `IS NULL` | Test in `WHERE`/`CASE` |
| `COALESCE(x, default)` | Replace missing with a default |
| `COALESCEC(x, "text")` | Character version (mainly for the DATA step) |
| `count(*)` vs `count(x)` | All rows vs non-missing values |
| `sum`, `avg`, `min`, `max` | **Ignore** missing |

**Warning:** `COALESCE` arguments must be the **same type** (all numeric or all character).

### 4.26 Character, numeric and datetime functions in PROC SQL

Most **SAS functions work inside `PROC SQL`**. A short taster (full tables in Session 6 and Session 7):

```sas
proc sql;
    select employee_name,
           upcase(employee_name)                    as name_upper,
           substr(employee_name, 1, 3)              as first3,
           round(salary / 12, 0.01)                 as monthly,
           year(hire_date)                          as hire_year,
           intck('year', hire_date, '31DEC2025'd)   as years_to_2025
    from employee
    where employee_id = 101;
quit;
```

| employee_name | name_upper | first3 | monthly | hire_year | years_to_2025 |
|---|---|---|---:|---:|---:|
| Asha | ASHA | Ash | 3750 | 2020 | 5 |

### 4.27 SQL views, and "stored procedures"

**View = a saved query.** It stores the **instructions**, not the data. Each time you use it, SAS runs the query on the **current** data.

```sas
proc sql;
    create view work.v_it_employees as
    select employee_id, employee_name, salary
    from employee
    where department = 'IT';

    select * from work.v_it_employees;       /* runs the query now */
    describe view work.v_it_employees;       /* prints the saved query in the log */
    drop view work.v_it_employees;
quit;
```

| | **Table (physical)** | **View (virtual)** |
|---|---|---|
| Stores data | **Yes** | **No**, only the query |
| Shows latest source data | Only as of when it was built | **Always** current |
| Speed to read | Fast | Re-runs the query every time |
| Disk space | Uses space | Almost none |
| Good for | Results reused many times | Always-fresh reports, hiding complexity, security (expose some columns only) |

> A view's source tables must still **exist and be reachable** (same library paths) when the view is used.

**Stored procedures**

- **`PROC SQL` does not create stored procedures.** The term belongs to **databases** (Oracle, SQL Server…), which store a named block of SQL on the server.
- From SAS you can **call** a database's stored procedure only through **explicit pass-through**, and only if your account allows it (🌐 🔑 depends on the database engine and SAS/ACCESS).

```sas
proc sql;
    connect to oracle (user="your_user" password="XXXXXXXX" path="your_tns_alias");
    execute (begin refresh_sales_summary; end;) by oracle;     /* runs the DB's own code */
    disconnect from oracle;
quit;
```

| Often confused | Meaning |
|---|---|
| **Database stored procedure** | Code saved **inside the database**, written in the database's language (PL/SQL, T-SQL) |
| **SAS procedure (`PROC`)** | A built-in SAS program such as `PROC SORT`, `PROC MEANS`; **not** the same thing |
| **SAS macro** | SAS's way to save reusable code (Session 8) |
| **SAS Stored Process** | A SAS server feature to run saved SAS programs from web apps (🌐 SAS Metadata / Viya environments) |

**Constraints (optional, to model keys in SAS)**

```sas
proc sql;
    create table work.dim_customer (
        customer_id   num,
        customer_name char(15) not null,
        constraint pk_cust primary key (customer_id)
    );
quit;
```

---

### SESSION 5 — TRANSPOSE, RETAIN, RANKING, LOOPS AND ARRAYS

**Topics in this session:** 5.1 PROC TRANSPOSE · 5.2 BY, ID, VAR, PREFIX · 5.3 Transposing several variables · 5.4 RETAIN · 5.5 SUM statement vs ordinary addition · 5.6 PROC COMPARE · 5.7 UPDATE · 5.8 FIRST. and LAST. · 5.9 PROC RANK · 5.10 FIRST./LAST. vs PROC RANK · 5.11 Row numbers (all the ways) · 5.12 Random sampling · 5.13 Every alternate observation · 5.14 DO loops · 5.15 Arrays

---

#### 5.1 PROC TRANSPOSE: rows to columns and columns to rows

**In simple words:** Turn a "tall" table (one row per product per month) into a "wide" table (one row per product, one column per month), or back again. Like a PivotTable (long→wide) and "Unpivot" (wide→long).

- **Definition:** `PROC TRANSPOSE` rotates the values of selected variables into new variables/observations.
- **Purpose:** Reshape data for reporting (wide) or for analysis and graphs (long).

**Starting data: monthly totals from SALES (long format)**

```sas
data sales_long;
    input product_id :$3. month :$3. amount;
    datalines;
P1 Jan 1800
P2 Jan 600
P2 Feb 900
P3 Feb 750
;
run;
```

**Long → wide (rows to columns)**

```sas
proc sort data=sales_long;  by product_id;  run;       /* BY variables must be sorted */

proc transpose data=sales_long
               out=sales_wide(drop=_name_)
               prefix=m_;
    by product_id;
    id month;
    var amount;
run;
```

| product_id | m_Jan | m_Feb |
|---|---:|---:|
| P1 | 1800 | . |
| P2 | 600 | 900 |
| P3 | . | 750 |

Cells with no matching row become **missing**.

**Wide → long (columns to rows)**

```sas
proc transpose data=sales_wide
               out=sales_long2(rename=(col1=amount))
               name=month;                 /* NAME= names the column that holds the old variable names */
    by product_id;
    var m_Jan m_Feb;
run;
```

| product_id | month | amount |
|---|---|---:|
| P1 | m_Jan | 1800 |
| P1 | m_Feb | . |
| P2 | m_Jan | 600 |
| P2 | m_Feb | 900 |
| P3 | m_Jan | . |
| P3 | m_Feb | 750 |

(Remove missing rows afterwards with `where amount is not missing;` if you do not want them.)

---

#### 5.2 BY, ID, VAR and PREFIX options

| Statement / option | Meaning | In the example above |
|---|---|---|
| `VAR` | Variables whose **values** are rotated | `amount` (long→wide); `m_Jan m_Feb` (wide→long) |
| `BY` | One output row per BY group; data must be **sorted** by it | `product_id` |
| `ID` | The variable whose **values become the new column names** | `month` → `Jan`, `Feb` |
| `PREFIX=` | Text put **in front of** the new column names | `m_` → `m_Jan` |
| `NAME=` | Name of the column that stores the **old variable names** (default `_NAME_`) | `month` |
| `OUT=` | Output dataset | `sales_wide` |
| `LET` | If an ID value repeats, keep the last one instead of failing | rarely needed |

**Important rules**

- With **no `ID`**, new columns are named `COL1`, `COL2`, … (and `PREFIX=` changes `COL`).
- An `ID` value must be **unique within a BY group**, or SAS errors ("ID value occurs twice"). De-duplicate first.
- ID values must make valid column names (e.g. `2025` does not; add a prefix such as `y_`).
- By default **only numeric** variables are transposed, unless you name character variables in `VAR`.
- A `_NAME_` column appears in the output unless you drop it, and `_LABEL_` too if the variables have labels.

---

#### 5.3 Transposing multiple variables

```sas
data scores;
    input student $ math science;
    datalines;
Anil  80 75
Beena 70 90
;
run;

proc transpose data=scores out=scores_t;
    id student;
    var math science;
run;
```

| _NAME_ | Anil | Beena |
|---|---:|---:|
| math | 80 | 70 |
| science | 75 | 90 |

With **several `VAR` variables and a `BY` variable**, you get one output row per `BY` group **per variable**, with `_NAME_` telling you which variable each row came from.

---

#### 5.4 RETAIN statement

**In simple words:** Normally SAS clears new variables at the start of every row. `RETAIN` says **"don't clear; remember the value from the previous row."**

- **Definition:** Keeps a variable's value across DATA step iterations instead of resetting it to missing.
- **Purpose:** Running totals, carrying values down, counting, comparing to the previous row.

**Syntax**

```sas
RETAIN variable <initial-value>;
```

**Example: running total of order amounts**

```sas
data orders_run;
    set orders;
    retain running_total 0;                     /* start at 0 */
    running_total = running_total + amount;
run;
```

| order_id | amount | running_total |
|---:|---:|---:|
| 5001 | 1200 | 1200 |
| 5002 | 800 | 2000 |
| 5003 | 1500 | 3500 |
| 5004 | 2200 | 5700 |
| 5005 | 400 | 6100 |
| 5006 | 900 | 7000 |

**Important rules (initialization)**

- **Without an initial value**, a retained variable starts as **missing**, so `missing + amount` stays missing. Always give a start value (`retain running_total 0;`) when you add to it.
- The initial value is set **once**, before the first row, not at every row.
- To restart per group, **reset it** at the first row of the group: `if first.customer_id then running_total = 0;`.
- Variables that come from a `SET`/`MERGE` dataset are **already retained** automatically; you do not need `RETAIN` for them.
- `RETAIN` only affects variables **you create**.

---

#### 5.5 SUM statement versus ordinary addition

**Syntax of the sum statement:** `variable + expression;` (no equals sign)

It does three things automatically: **(1)** initialises the variable to **0**, **(2)** **retains** it, **(3)** **ignores missing** values in the expression.

```sas
data cum_salary;
    set employee;
    total_sumstmt + salary;                 /* sum statement */

    retain total_plus 0;
    total_plus = total_plus + salary;       /* ordinary addition with RETAIN */
run;
```

| employee_name | salary | total_sumstmt | total_plus |
|---|---:|---:|---:|
| Asha | 45,000 | 45,000 | 45,000 |
| Ravi | 62,000 | 107,000 | 107,000 |
| Meena | 58,000 | 165,000 | 165,000 |
| John | 51,000 | 216,000 | 216,000 |
| Priya | 49,000 | 265,000 | 265,000 |
| Karan | 47,000 | 312,000 | 312,000 |
| **Neha** | **.** | **312,000** | **.** |

Neha's missing salary: the **sum statement keeps going** (312,000), while ordinary addition makes the total **missing** (and every later row would stay missing).

| Way to add | Missing handling | Retains value? | Starts at |
|---|---|---|---|
| `x = x + y;` | Result becomes **missing** if either is missing | **No** (unless `RETAIN`) | Missing |
| `x + y;` (sum statement) | **Ignores** missing `y` | **Yes** (automatic) | **0** |
| `x = sum(x, y);` | **Ignores** missing | **No** (unless `RETAIN`) | n/a |

---

#### 5.6 PROC COMPARE

**In simple words:** "Spot the difference" between two datasets (a before/after check, or testing that a new program gives the same result as the old one).

```sas
data emp_v2;
    set employee;
    if employee_id = 102 then salary = 65000;       /* change a number */
    if employee_id = 105 then department = "HR";    /* change a text */
run;

proc compare base=employee compare=emp_v2
             out=diffs outnoequal outbase outcomp outdif;
    id employee_id;                                 /* match rows by this key, not by position */
run;
```

**What the report tells you**

| Report section | Meaning |
|---|---|
| Data Set Summary | Names, number of variables and observations of each |
| Variables Summary | Variables in common, only in BASE, only in COMPARE |
| Observation Summary | Observations in common / only in one |
| Values Comparison Summary | **Number of variables with unequal values** (here: `salary`, `department`) and the number of unequal values |
| Listing of differences | For each unequal value: the BASE value, the COMPARE value, and the difference |

For this example, `salary` has 1 unequal value (Ravi: 62000 vs 65000, difference 3000) and `department` has 1 (Priya: Sales vs HR). The `OUT=` dataset `diffs` contains only the rows that differ (`OUTNOEQUAL`).

| Option | Use |
|---|---|
| `ID var` | Match rows by key (data must be sorted by it) |
| `OUT=` + `OUTBASE OUTCOMP OUTDIF` | Save base rows, compare rows, and differences |
| `CRITERION=` / `METHOD=` | Tolerance for "equal" numbers (e.g. rounding) |
| `LISTALL` | Print every variable/obs, even matches |

---

#### 5.7 UPDATE statement and its use cases

**In simple words:** `UPDATE` applies **corrections** (a transaction file) onto a **master** table. It only overwrites with values that are **not missing**, so a blank in the correction means "leave unchanged".

```sas
data cust_updates;
    input customer_id city :$10. credit_limit;
    datalines;
2 .          40000
4 Bangalore  25000
5 Hyderabad  .
;
run;

data customer_new;
    update customer cust_updates;        /* master first, then transactions */
    by customer_id;
run;
```

| customer_id | customer_name | city | credit_limit | What happened |
|---:|---|---|---:|---|
| 1 | Alpha_Corp | Mumbai | 50,000 | No transaction |
| 2 | Beta_Traders | Delhi | **40,000** | City blank in update, so Delhi kept; limit changed |
| 3 | Gamma_Stores | Mumbai | 70,000 | No transaction |
| 4 | Delta_Mart | **Bangalore** | **25,000** | Both filled in |
| 5 | Echo_Retail | **Hyderabad** | 20,000 | Limit blank in update, so 20,000 kept |

**Important rules**

- Both datasets must be **sorted by the `BY` variable**.
- The **master must have one row per key**; the transaction dataset may have several rows per key (applied in order).
- Keys that are only in the transaction dataset are **added** as new rows.
- `UPDATE` does **not** write the output until the last transaction of each key is applied (unlike `MERGE`).
- To let missing values overwrite, use `update customer cust_updates updatemode=nomissingcheck;`.

| Tool | Use for |
|---|---|
| `UPDATE` | Apply a file of corrections to a master, ignoring blanks |
| `MERGE` | Combine columns; missing values **do** overwrite (right-most wins) |
| `MODIFY` | Change a dataset **in place** without rewriting it |
| `PROC SQL UPDATE` | Change specific rows with a condition (Session 7) |

---

#### 5.8 FIRST. and LAST. BY-group processing

**In simple words:** When data is sorted into groups, SAS gives you two flags for each row: **"Am I the first row of my group?"** (`FIRST.`) and **"Am I the last?"** (`LAST.`). Use them to pick one row per group or to total within a group.

**The flags (data sorted by department)**

```sas
proc sort data=employee out=emp_s;  by department;  run;

data flags;
    set emp_s;
    by department;
    is_first = first.department;
    is_last  = last.department;
run;
```

| employee_name | department | is_first | is_last |
|---|---|---:|---:|
| Asha | HR | 1 | 0 |
| Karan | HR | 0 | 1 |
| Ravi | IT | 1 | 0 |
| Meena | IT | 0 | 0 |
| Neha | IT | 0 | 1 |
| John | Sales | 1 | 0 |
| Priya | Sales | 0 | 1 |

**Example: totals per department**

```sas
data dept_stats;
    set emp_s;
    by department;
    if first.department then do;       /* new group: reset */
        total = 0;
        count = 0;
    end;
    total + salary;                    /* sum statement: retains, ignores missing */
    count + 1;
    if last.department;                /* keep one row per group */
    keep department total count;
run;
```

| department | total | count |
|---|---:|---:|
| HR | 92,000 | 2 |
| IT | 120,000 | 3 |
| Sales | 100,000 | 2 |

**Common uses:** keep the first/last row per group (e.g. the latest transaction per customer), group totals, counters per group, flagging group boundaries.

**Important rules**

- The data must be **sorted by the BY variables** (or at least grouped). Otherwise: `ERROR: BY variables are not properly sorted`. `BY var NOTSORTED;` allows data that is grouped but not in order.
- `FIRST.`/`LAST.` are **temporary** (not saved). Copy them to real variables if you need them.
- With several `BY` variables, `FIRST.var2` is also 1 whenever `FIRST.var1` is 1 (a new outer group restarts the inner group).
- For "latest row per customer": sort by `customer_id order_date`, then `if last.customer_id;`.

---

#### 5.9 PROC RANK

**In simple words:** Give each row a **rank number** (1st, 2nd, 3rd…) based on a variable's value.

```sas
proc rank data=employee out=emp_rank descending ties=low;
    var salary;
    ranks salary_rank;
run;
```

| employee_name | salary | salary_rank |
|---|---:|---:|
| Asha | 45,000 | 6 |
| Ravi | 62,000 | 1 |
| Meena | 58,000 | 2 |
| John | 51,000 | 3 |
| Priya | 49,000 | 4 |
| Karan | 47,000 | 5 |
| Neha | . | . |

**Within a group (needs sorted data):**

```sas
proc sort data=employee out=emp_s;  by department;  run;
proc rank data=emp_s out=emp_rank_dept descending;
    by department;
    var salary;
    ranks dept_rank;
run;
```

Ranks: HR → Karan 1, Asha 2; IT → Ravi 1, Meena 2, Neha missing; Sales → John 1, Priya 2.

| Option / statement | Meaning |
|---|---|
| `VAR` / `RANKS` | Variable to rank / name of the new rank variable |
| `DESCENDING` | Largest value gets rank **1** (default: smallest = 1) |
| `TIES=` | `MEAN` (default; tied rows share the **average** rank, e.g. 2.5), `LOW`, `HIGH`, `DENSE` |
| `GROUPS=n` | Split into *n* equal groups (0 to n−1), such as quartiles with `GROUPS=4` |
| `PERCENT`, `FRACTION` | Rank as percentage/fraction instead |
| `BY` | Rank within groups |

**Important rules**

- **Missing values are not ranked**; they stay missing.
- The default `TIES=MEAN` can give **decimal ranks** (2.5). Choose `TIES=LOW` for 1, 2, 2, 4 style.
- `PROC RANK` does **not sort** the output; row order stays as in the input.

---

#### 5.10 FIRST./LAST. versus PROC RANK

| | `FIRST.` / `LAST.` (DATA step) | `PROC RANK` |
|---|---|---|
| Idea | Boundaries of sorted groups | Position by **value** |
| Needs sorting by | The **group** (and by the value if you want "top") | Only if using `BY` |
| Ties | Picks exactly **one** row (the first or last in sort order) | Tied rows get the **same** rank (according to `TIES=`) |
| Result | Usually **fewer rows** (one per group) | **All rows**, with an extra rank column |
| Best for | "Latest record per customer", group totals, counters | "Top 3 by salary", percentiles, quartile groups |

**Top earner per department, two ways**

```sas
/* (a) FIRST. approach: exactly one row per department */
proc sort data=employee out=emp_s;  by department descending salary;  run;
data top_a;  set emp_s;  by department;  if first.department;  run;

/* (b) RANK approach: ties could return several rows */
proc rank data=emp_s out=emp_r descending ties=low;  by department;  var salary;  ranks r;  run;
data top_b;  set emp_r;  where r = 1;  run;
```

Both give Karan (HR), Ravi (IT), John (Sales). If two people tied for the top salary, (a) returns one and (b) returns both.

---

#### 5.11 Creating row numbers (and which method to choose)

| Method | Code | Notes |
|---|---|---|
| **DATA step counter** | `row_num + 1;` (sum statement) | Simple, reliable, follows the order of rows being written |
| `_N_` | `row_num = _N_;` | Counts DATA step iterations; **not** a true row number if rows are deleted before it, or if you read several datasets |
| **BY-group counter** | `if first.department then seq = 0; seq + 1;` | Numbers rows within each group (sorted data) |
| `PROC RANK` | see 5.9 | Ranks by **value**, with tie rules; not by position |
| `PROC SQL` with `monotonic()` | `select monotonic() as rn, * from employee;` | 🌐 **Undocumented function**; can give wrong results with joins, `WHERE`, `ORDER BY`. **Do not use it in production code** |
| `PROC SQL NUMBER` option | `proc sql number; select * from employee;` | Only **displays** a row column in the printout; it cannot be saved |
| `ROW_NUMBER() OVER (PARTITION BY ... ORDER BY ...)` | Window function | ❌ **Not supported by Base SAS `PROC SQL`** in standard 9.4. 🌐 Works when you **pass the query to a database** that supports it (explicit pass-through), and may be available in some Viya SQL engines (`PROC FEDSQL`/CAS). Check your version |

**Example: overall and by-group row numbers**

```sas
proc sort data=employee out=emp_s;  by department;  run;

data emp_rows;
    set emp_s;
    by department;
    row_num + 1;                                 /* overall */
    if first.department then seq = 0;            /* restart each department */
    seq + 1;
run;
```

| employee_name | department | row_num | seq |
|---|---|---:|---:|
| Asha | HR | 1 | 1 |
| Karan | HR | 2 | 2 |
| Ravi | IT | 3 | 1 |
| Meena | IT | 4 | 2 |
| Neha | IT | 5 | 3 |
| John | Sales | 6 | 1 |
| Priya | Sales | 7 | 2 |

**Window-function pass-through (only where the database supports it)**

```sas
proc sql;
    connect to oracle (user="your_user" password="XXXXXXXX" path="your_tns_alias");
    create table work.ranked as
    select * from connection to oracle
      ( select employee_id, department, salary,
               row_number() over (partition by department order by salary desc) as rn
        from hr.employees );
    disconnect from oracle;
quit;
```

---

#### 5.12 Random sampling

Covered in detail in [3.13](#313-selecting-random-observations) (`PROC SURVEYSELECT` with `SEED=`, `SAMPSIZE=` for an exact size, and a Base SAS shuffle-and-take method). A quick **approximate** percentage in a DATA step:

```sas
data sample_30pct;
    call streaminit(2025);
    set employee;
    if rand("uniform") < 0.30;      /* keeps roughly 30% of rows; the exact count varies */
run;
```

Use `SAMPSIZE=` (or the shuffle method) when you need an **exact** count.

---

#### 5.13 Selecting every alternate observation

```sas
/* Odd rows: 1, 3, 5, 7 */
data odd_rows;
    set employee;
    if mod(_N_, 2) = 1;
run;
/* Asha, Meena, Priya, Neha */

/* Even rows: 2, 4, 6 */
data even_rows;
    set employee;
    if mod(_N_, 2) = 0;
run;
/* Ravi, John, Karan */

/* Faster for big data: jump straight to rows 1, 3, 5, ... */
data every_other;
    do p = 1 to nobs by 2;
        set employee point=p nobs=nobs;
        output;
    end;
    stop;                              /* required with POINT= */
run;
```

`MOD(a, b)` is the **remainder** after dividing `a` by `b`. `mod(_N_,2)` is 1 for odd rows and 0 for even rows. For every *k*-th row use `mod(_N_, k) = 0`.

---

#### 5.14 DO loops and iterative processing

**In simple words:** A DO loop repeats a block of statements.

| Loop | Syntax | Checks the condition | Runs at least once? |
|---|---|---|---|
| **Iterative** | `do i = 1 to 5; ... end;` | Counter limit | If the range is not empty |
| **DO WHILE** | `do while (cond); ... end;` | **Before** each pass | **No** (may run zero times) |
| **DO UNTIL** | `do until (cond); ... end;` | **After** each pass | **Yes** |
| **List** | `do i = 2, 4, 6; ... end;` | n/a | Yes |

**Example 1: iterative DO (compound growth; 1,000 at 5% for 3 years)**

```sas
data growth;
    balance = 1000;
    do year = 1 to 3;
        balance = balance * 1.05;
        output;                          /* write a row for each year */
    end;
run;
```

| year | balance |
|---:|---:|
| 1 | 1050 |
| 2 | 1102.5 |
| 3 | 1157.625 |

**Example 2: DO UNTIL (years until the money doubles)**

```sas
data double_it;
    balance = 1000;
    years = 0;
    do until (balance >= 2000);
        balance = balance * 1.05;
        years + 1;
    end;
run;
```

Result: `years = 15`, `balance ≈ 2078.93`.

**Example 3: a loop with a step size and early exit**

```sas
data loop_demo;
    do i = 10 to 1 by -3;      /* 10, 7, 4, 1 */
        if i = 4 then leave;   /* LEAVE exits the loop; CONTINUE skips to the next pass */
        output;
    end;
run;
```

Rows: `i = 10` and `i = 7` only.

**Important rules**

- A DATA step with **no `SET`/`INPUT`** runs its code **once**, so a loop inside it builds the whole table.
- Without `OUTPUT` inside the loop, only the **final** row is written.
- A `DO WHILE/UNTIL` whose condition never becomes true runs **forever**. Always change something the condition tests.
- Don't confuse the **DATA step loop** (SAS reading row after row, automatic) with a **`DO` loop** (your own repeated code inside one row).

---

#### 5.15 SAS arrays and practical examples

**In simple words:** An array is a **temporary nickname for a group of variables**, so you can loop through them with a counter instead of repeating the same line for each one.

**Syntax**

```sas
ARRAY array_name{n} var1-varN;            /* numeric */
ARRAY array_name{n} $ length var1-varN;   /* character */
```

**Example 1: replace missing scores with 0 and total them**

```sas
data scores_wide;
    input student_id q1 q2 q3 q4;
    datalines;
1 80 70 90 60
2 55  . 75 85
;
run;

data scores_clean;
    set scores_wide;
    array q{4} q1-q4;                    /* q{1}=q1, q{2}=q2 ... */
    do i = 1 to dim(q);                  /* DIM() = number of elements */
        if missing(q{i}) then q{i} = 0;
    end;
    total = sum(of q{*});                /* OF + {*} = all elements */
    drop i;
run;
```

| student_id | q1 | q2 | q3 | q4 | total |
|---:|---:|---:|---:|---:|---:|
| 1 | 80 | 70 | 90 | 60 | 300 |
| 2 | 55 | 0 | 75 | 85 | 215 |

**Example 2: wide → long with an array (alternative to `PROC TRANSPOSE`)**

```sas
data scores_long;
    set scores_wide;
    array q{4} q1-q4;
    do question = 1 to 4;
        score = q{question};
        output;
    end;
    keep student_id question score;
run;
```

Result: **8 rows** (2 students × 4 questions): `(1,1,80) (1,2,70) (1,3,90) (1,4,60) (2,1,55) (2,2,.) (2,3,75) (2,4,85)`.

**Example 3: temporary array of constants (lookup)**

```sas
data employee_tax;
    set employee;
    array rate{3} _temporary_ (0.05 0.10 0.15);     /* values kept, not saved as variables */
    if salary >= 60000 then tax = salary * rate{3};
    else if salary >= 50000 then tax = salary * rate{2};
    else tax = salary * rate{1};
run;
```

**Important rules**

- Index **starts at 1** by default; use `array a{0:3}` for a custom range.
- All variables in one array must be the **same type** (all numeric or all character).
- Array names are **not variables**: you cannot put them in `KEEP`, `DROP` or `PROC` steps. Use the underlying variables.
- An index outside the range, such as `q{5}` for a 4-element array, causes `ERROR: Array subscript out of range`.
- `_TEMPORARY_` arrays are retained automatically and **not written** to the output dataset.
- Arrays exist **only during the DATA step**; there is no array in `PROC SQL`.

---

### SESSION 6 — SAS FUNCTIONS AND SUMMARY REPORTING

**Part A. Functions:** 6.1 What a function is · 6.2 Character functions · 6.3 Numeric functions · 6.4 SUM() vs `+` vs the sum statement · 6.5 Dates, times and datetimes · 6.6 Date/time functions · 6.7 Formats and informats for dates

**Part B. Summary reports:** 6.8 PROC MEANS · 6.9 PROC SUMMARY · 6.10 PROC UNIVARIATE · 6.11 PROC FREQ · 6.12 PROC REPORT · 6.13 PROC TABULATE · 6.14 Basic charts · 6.15 Which procedure to choose

---

#### PART A — SAS functions

#### 6.1 What is a function?

**In simple words:** A function is a **ready-made calculator**: you give it values (arguments) in brackets, it gives back one result. Example: `upcase("sas")` returns `SAS`.

```sas
new_variable = function_name(argument1, argument2, ...);
```

Functions work in the **DATA step**, in `WHERE`, and in `PROC SQL`. They do **not** change the original variable unless you assign the result back to it.

**One trap to know early:** when a character function creates a **new** variable, its **length** may be unexpected (for example `SCAN`, `CATS`, `CATX` give a length of up to 200). Set the length first: `length first_name $ 20;`.

---

#### 6.2 Character functions

Results that are text are shown in quotes so that blanks are visible.

| Function | Syntax | What it does | Example | Output |
|---|---|---|---|---|
| `UPCASE` | `UPCASE(x)` | To UPPER CASE | `upcase("sas guide")` | `"SAS GUIDE"` |
| `LOWCASE` | `LOWCASE(x)` | To lower case | `lowcase("SAS Guide")` | `"sas guide"` |
| `PROPCASE` | `PROPCASE(x)` | First Letter Of Each Word Capital | `propcase("john smith")` | `"John Smith"` |
| `STRIP` | `STRIP(x)` | Removes **leading and trailing** blanks | `strip("  hi  ")` | `"hi"` |
| `TRIM` | `TRIM(x)` | Removes **trailing** blanks only | `trim("hi   ")` | `"hi"` |
| `LEFT` | `LEFT(x)` | Moves leading blanks to the **end** (left-aligns) | `left("  hi")` | `"hi  "` |
| `RIGHT` | `RIGHT(x)` | Moves trailing blanks to the **front** (right-aligns) | `right("hi  ")` | `"  hi"` |
| `LENGTH` | `LENGTH(x)` | Length **without trailing blanks** (a blank string gives **1**) | `length("Mumbai  ")` | `6` |
| `LENGTHN` | `LENGTHN(x)` | Same, but a blank string gives **0** | `lengthn(" ")` | `0` |
| `SUBSTR` | `SUBSTR(x, start, len)` | Cuts out part of text (counting starts at **1**) | `substr("Mumbai", 1, 3)` | `"Mum"` |
| `SCAN` | `SCAN(x, n, delimiters)` | The **n-th word**; negative *n* counts from the right | `scan("Asha Rao Kumar", 2)` / `scan("a,b,c", -1, ",")` | `"Rao"` / `"c"` |
| `FIND` | `FIND(x, find, modifiers, start)` | **Position** of text (0 if absent). Modifier `i` ignores case | `find("Mumbai", "M", "i")` | `1` |
| `INDEX` | `INDEX(x, find)` | Position of text (case-sensitive; simpler `FIND`) | `index("Mumbai", "b")` | `4` |
| `COMPRESS` | `COMPRESS(x, chars, modifiers)` | **Removes** characters (blanks if none given) | `compress("a-b c", "- ")` | `"abc"` |
| `COMPBL` | `COMPBL(x)` | Squeezes several blanks into **one** | `compbl("a    b   c")` | `"a b c"` |
| `CAT` | `CAT(a, b, ...)` | Joins text **as is** (no trimming) | `cat("a ", "b")` | `"a b"` |
| `CATS` | `CATS(a, b, ...)` | Joins after **stripping** both ends of each | `cats(" a ", " b ")` | `"ab"` |
| `CATT` | `CATT(a, b, ...)` | Joins after **trimming trailing** blanks | `catt("a ", "b ")` | `"ab"` |
| `CATX` | `CATX(sep, a, b, ...)` | Joins with a **separator**, stripped; skips missing values | `catx("-", "A", "B", "C")` | `"A-B-C"` |
| `TRANWRD` | `TRANWRD(x, from, to)` | Replaces a **word/phrase** | `tranwrd("I like cats", "cats", "dogs")` | `"I like dogs"` |
| `TRANSLATE` | `TRANSLATE(x, to, from)` | Replaces **single characters** (note the order: **to** first, then **from**) | `translate("a-b-c", "_", "-")` | `"a_b_c"` |

**`SCAN` default delimiters:** space and many punctuation marks (`. < ( + & ! $ * ) ; - / , %` etc.). Always pass your own delimiter when you mean a specific one, for example `scan(name, 1, " ")`.

**`SUBSTR` extras:** `SUBSTR(x, 4)` gives everything from position 4; on the left of `=` it **replaces** part of a variable: `substr(code, 1, 2) = "ZZ";`.

**Example program**

```sas
data char_demo;
    length full_name $ 30 first_name $ 15 initials $ 3;
    full_name  = "  asha   rao ";
    full_name  = propcase(compbl(strip(full_name)));       /* "Asha Rao" */
    first_name = scan(full_name, 1, " ");                   /* "Asha" */
    initials   = cats(substr(full_name, 1, 1), substr(scan(full_name, 2, " "), 1, 1));   /* "AR" */
run;
```

| full_name | first_name | initials |
|---|---|---|
| Asha Rao | Asha | AR |

**Important rules**

- Comparing text pads the shorter value with blanks, so `"HR"` equals `"HR   "`, but **case matters** (`"hr"` ≠ `"HR"`).
- Use `STRIP` instead of `TRIM(LEFT(x))`; it does the same in one call.
- Functions with **missing text** return blank (or `0` / `.` for functions returning numbers, such as `FIND`).

---

#### 6.3 Numeric functions

| Function | Syntax | What it does | Example | Output |
|---|---|---|---|---|
| `SUM` | `SUM(a, b, ...)` | Adds, **ignoring missing** values | `sum(2, ., 5)` | `7` |
| `MEAN` | `MEAN(a, b, ...)` | Average of non-missing values | `mean(2, ., 4)` | `3` |
| `MIN` / `MAX` | `MIN(a, b, ...)` | Smallest / largest non-missing | `min(3, ., 1)` / `max(3, ., 9)` | `1` / `9` |
| `N` / `NMISS` | `N(a, b, ...)` | Count of non-missing / missing values | `n(2, ., 4)` / `nmiss(2, ., 4)` | `2` / `1` |
| `ROUND` | `ROUND(x, unit)` | Rounds to the nearest **unit** (default 1) | `round(3.14159, 0.01)` / `round(1234, 100)` | `3.14` / `1200` |
| `CEIL` | `CEIL(x)` | Next whole number **up** | `ceil(2.1)` | `3` |
| `FLOOR` | `FLOOR(x)` | Next whole number **down** | `floor(2.9)` | `2` |
| `INT` | `INT(x)` | Drops decimals (toward zero) | `int(-2.7)` | `-2` |
| `ABS` | `ABS(x)` | Removes the minus sign | `abs(-5)` | `5` |
| `MOD` | `MOD(a, b)` | **Remainder** of a ÷ b | `mod(10, 3)` | `1` |
| `SQRT` | `SQRT(x)` | Square root | `sqrt(16)` | `4` |
| `LOG` | `LOG(x)` | **Natural** log (`LOG10` for base 10) | `log(100)` | `4.60517` |
| `EXP` | `EXP(x)` | *e* raised to *x* | `exp(1)` | `2.71828` |
| `RAND` | `RAND("uniform")` | Random number from a distribution (use `CALL STREAMINIT(seed)` first to repeat) | `rand("uniform")` | a number between 0 and 1 |

**Two ways to compute an average of three columns**

```sas
avg_a = (q1 + q2 + q3) / 3;     /* any missing makes avg_a missing */
avg_b = mean(q1, q2, q3);       /* ignores missing; averages what is present */
```

**Important rules**

- Arithmetic operators (`+ - * /`) return **missing** if any operand is missing; functions like `SUM`, `MEAN`, `MIN`, `MAX` **skip** missing values.
- `ROUND(x, 0.01)` uses a **unit**, not a count of decimals.
- Use `SUM(of q1-q4)` to sum a variable list; `SUM(q1-q4)` would subtract!
- `MIN`/`MAX` with **several variables in a row** are DATA step functions; in `PROC SQL`, `MIN(x)`/`MAX(x)` with **one argument** are summary functions over rows (use `MIN(a,b)` for across columns).

---

#### 6.4 Difference among SUM(), the `+` operator and the sum statement

| | `SUM(a, b)` | `a + b` | `total + a;` (sum **statement**) |
|---|---|---|---|
| What it is | Function | Operator | DATA step statement |
| Missing values | **Ignored** | Result **missing** | **Ignored** |
| Remembers value across rows | No | No | **Yes** (automatic `RETAIN`) |
| Starts at | n/a | n/a | **0** |
| Example with `a = 5`, `b = .` | `5` | `.` | adds 5 to `total` |
| All arguments missing | `.` (missing) | `.` | `total` unchanged |

---

#### 6.5 SAS date values, datetime values, formats and informats

**In simple words:** SAS stores dates as **plain numbers** (a counter), and **formats** make them readable.

| Kind | Stored as | Counted from | Example value | Shown with format |
|---|---|---|---:|---|
| **Date** | **Days** | 01JAN1960 (= 0) | 23756 | `date9.` → `15JAN2025` |
| **Time** | **Seconds** since midnight | 00:00:00 | 52200 | `time8.` → `14:30:00` |
| **Datetime** | **Seconds** | 01JAN1960 00:00:00 | 2052570600 | `datetime20.` → `15JAN2025:14:30:00` |

**Facts to remember**

- Dates **before** 1960 are **negative** numbers (31DEC1959 = −1).
- You can add and subtract dates: `due_date = order_date + 30;` and `days_open = close_date - open_date;`.
- **Date literals:** `'15JAN2025'd` (date), `'14:30:00't` (time), `'15JAN2025:14:30:00'dt` (datetime). The quotes and the letter are required.
- Convert datetime → date with `DATEPART()`, datetime → time with `TIMEPART()`.
- **Reading** a date from text needs an **informat** (`date9.`, `ddmmyy10.`, `mmddyy10.`, `yymmdd10.`, or `anydtdte.` for mixed styles).
- Two-digit years such as `15/01/25` are interpreted using the system option `YEARCUTOFF=` (default 1926 in modern SAS: 26–99 → 19xx, 00–25 → 20xx). Prefer four-digit years.

---

#### 6.6 Date, time and datetime functions

Using `d = '15JAN2025'd` (value 23756, a Wednesday) and `dt = '15JAN2025:14:30:00'dt`.

| Function | Syntax | What it does | Example | Output |
|---|---|---|---|---|
| `TODAY` / `DATE` | `TODAY()` | Today's date | `today()` | today's date as a number (apply a date format to read it) |
| `TIME` | `TIME()` | Current time (seconds since midnight) | `time()` | seconds since midnight, e.g. 52200 = 14:30:00 |
| `DATETIME` | `DATETIME()` | Current date and time | `datetime()` | a datetime value |
| `MDY` | `MDY(month, day, year)` | **Builds** a date from parts | `mdy(1, 15, 2025)` | `23756` → 15JAN2025 |
| `DHMS` | `DHMS(date, h, m, s)` | Builds a **datetime** from a date + time parts | `dhms(d, 14, 30, 0)` | `2052570600` → 15JAN2025:14:30:00 |
| `HMS` | `HMS(h, m, s)` | Builds a **time** | `hms(14, 30, 0)` | `52200` → 14:30:00 |
| `YEAR` | `YEAR(d)` | Year | `year(d)` | `2025` |
| `MONTH` | `MONTH(d)` | Month number | `month(d)` | `1` |
| `DAY` | `DAY(d)` | Day of month | `day(d)` | `15` |
| `QTR` | `QTR(d)` | Quarter (1–4) | `qtr(d)` | `1` |
| `WEEK` | `WEEK(d <,'U'\|'V'\|'W'>)` | Week of the year (default rule `U`: weeks start on **Sunday**) | `week(d)` | `2` |
| `WEEKDAY` | `WEEKDAY(d)` | Day of week: **1 = Sunday … 7 = Saturday** | `weekday(d)` | `4` (Wednesday) |
| `DATEPART` | `DATEPART(dt)` | Date part of a datetime | `datepart(dt)` | `23756` |
| `TIMEPART` | `TIMEPART(dt)` | Time part of a datetime | `timepart(dt)` | `52200` |
| `INTNX` | `INTNX(interval, start, n <,alignment>)` | **Moves** a date forward/back *n* intervals | see below | see below |
| `INTCK` | `INTCK(interval, from, to)` | **Counts** interval boundaries between two dates | see below | see below |
| `YRDIF` | `YRDIF(start, end, basis)` | Difference in **years** (decimal) | `yrdif('15JAN2020'd, '15JAN2025'd, 'ACT/ACT')` | `5` |

**INTNX: "move a date"**

| Call | Output |
|---|---|
| `intnx('month', d, 1)` (default alignment = **b**eginning) | `01FEB2025` (23773) |
| `intnx('month', d, 1, 'same')` (same day) | `15FEB2025` (23787) |
| `intnx('month', d, 0, 'end')` (end of this month) | `31JAN2025` (23772) |
| `intnx('week', d, 0)` (start of this week, Sunday) | `12JAN2025` (23753) |
| `intnx('year', d, -1, 'same')` | `15JAN2024` |

Alignment values: `'b'` (beginning, default), `'m'` (middle), `'e'` (end), `'s'` (same day).

**INTCK: "count boundaries crossed"**

| Call | Output | Why |
|---|---|---|
| `intck('month', '15JAN2025'd, '01MAR2025'd)` | `2` | Crosses **1 Feb** and **1 Mar** |
| `intck('day', '15JAN2025'd, '01MAR2025'd)` | `45` | Day difference |
| `intck('year', '31DEC2024'd, '01JAN2025'd)` | `1` | Only **one day** apart, but it **crosses a year boundary** |

> `INTCK` does **not** count completed intervals. For true age in whole years, use `floor(yrdif(birth_date, today(), 'AGE'))`.

**Example program**

```sas
data date_demo;
    set employee(obs=2 keep=employee_name hire_date);
    hire_year    = year(hire_date);
    hire_qtr     = qtr(hire_date);
    anniversary  = intnx('year', hire_date, 1, 'same');
    years_served = floor(yrdif(hire_date, '31DEC2025'd, 'AGE'));
    format anniversary date9.;
run;
```

| employee_name | hire_date | hire_year | hire_qtr | anniversary | years_served |
|---|---|---:|---:|---|---:|
| Asha | 15JAN2020 | 2020 | 1 | 15JAN2021 | 5 |
| Ravi | 03MAR2019 | 2019 | 1 | 03MAR2020 | 6 |

---

#### 6.7 Converting between text and numbers or dates

| Task | Function | Example | Result |
|---|---|---|---|
| Text → number | `INPUT(text, informat)` | `input("1,250", comma8.)` | `1250` |
| Text → date | `INPUT(text, date-informat)` | `input("15/01/2025", ddmmyy10.)` | `23756` |
| Number → text | `PUT(number, format)` | `put(23756, date9.)` | `"15JAN2025"` |
| Number → text with a pattern | `PUT(x, z5.)` | `put(42, z5.)` | `"00042"` (leading zeros) |

`INPUT` and `PUT` are the main SAS conversion tools. Mnemonic: **`INPUT` brings text in as a number; `PUT` sends a number out as text.**

---

#### PART B — Summary reports and procedures

All examples use EMPLOYEE (salary mean = 52,000, median = 50,000 over the six non-missing values).

#### 6.8 PROC MEANS

- **Purpose:** Quick **summary statistics** (count, mean, min, max, sum…) overall or by group. **Prints** a table by default.
- **Default statistics:** `N`, `MEAN`, `STD`, `MIN`, `MAX`.

```sas
proc means data=employee n nmiss sum mean min max median maxdec=0;
    class department;
    var salary;
run;
```

| department | N Obs | N | N Miss | Sum | Mean | Minimum | Maximum | Median |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| HR | 2 | 2 | 0 | 92,000 | 46,000 | 45,000 | 47,000 | 46,000 |
| IT | 3 | 2 | 1 | 120,000 | 60,000 | 58,000 | 62,000 | 60,000 |
| Sales | 2 | 2 | 0 | 100,000 | 50,000 | 49,000 | 51,000 | 50,000 |

`N Obs` = rows in the group (IT has 3), `N` = non-missing values (IT has 2).

**Saving the results as a dataset**

```sas
proc means data=employee noprint nway;
    class department;
    var salary;
    output out=dept_stats(drop=_type_ _freq_)
           n=n_salary  nmiss=n_missing  sum=total_salary  mean=avg_salary;
run;
```

| department | n_salary | n_missing | total_salary | avg_salary |
|---|---:|---:|---:|---:|
| HR | 2 | 0 | 92000 | 46000 |
| IT | 2 | 1 | 120000 | 60000 |
| Sales | 2 | 0 | 100000 | 50000 |

| Statement / option | Meaning |
|---|---|
| `VAR` | Numeric variables to summarise |
| `CLASS` | Group variables (**no sorting needed**; one combined table) |
| `BY` | Group variables (**data must be sorted**; separate table per group) |
| `OUTPUT OUT=` | Save statistics to a dataset: `stat=newname` |
| Statistics keywords | `N NMISS SUM MEAN MIN MAX MEDIAN STD VAR RANGE P25 P75 CLM` |
| `MAXDEC=n` | Decimal places printed |
| `NWAY` | In the output, keep only the **full combination** of all CLASS variables |
| `NOPRINT` | Don't print the table |
| `_TYPE_`, `_FREQ_` | Automatic output columns: grouping level and row count |

**CLASS vs BY:** `CLASS` needs no sort and shows one combined table; `BY` needs sorted data and gives a separate table for each group.

---

#### 6.9 PROC SUMMARY

- **Purpose:** The **same** statistics as `PROC MEANS`, but it **does not print** by default; it is made for **creating output datasets**.
- Add `PRINT` to see a table.

```sas
proc summary data=employee nway;
    class department;
    var salary;
    output out=dept_totals sum=total_salary;
run;
```

**MEANS vs SUMMARY:** Same engine, same options. Use `MEANS` to **look** at statistics; use `SUMMARY` to **create** a table from them.

---

#### 6.10 PROC UNIVARIATE

- **Purpose:** A **detailed look at one variable's distribution**: shape, spread, extreme values, percentiles, normality tests, histograms.

```sas
proc univariate data=employee;
    var salary;
    histogram salary / normal;      /* draws a histogram with a normal curve */
run;
```

**Main output sections**

| Section | Tells you |
|---|---|
| Moments | N, mean (52,000), std deviation (6,633.25), variance, skewness, kurtosis |
| Basic Statistical Measures | Mean, **median (50,000)**, mode, range, interquartile range |
| Tests for Location | Is the mean different from 0? |
| Quantiles | Min, Q1, median, Q3, max, and percentiles (1%, 5%, 10%, 90%, 95%, 99%) |
| Extreme Observations | Lowest and highest values with their row numbers |
| Missing Values | Count of missing values (1 for `salary`) |

| Option | Meaning |
|---|---|
| `NORMAL` | Tests for normality |
| `PLOT` | Simple stem-and-leaf and box plot |
| `FREQ` | Frequency table of the values |
| `CLASS var` | Separate analysis per group |
| `OUTPUT OUT= pctlpts=… pctlpre=…` | Save chosen percentiles to a dataset |

---

#### 6.11 PROC FREQ

- **Purpose:** **Counts** and percentages of **categories** (frequency tables), and cross-tabulations.

```sas
proc freq data=employee;
    tables department / nocum;
run;
```

| department | Frequency | Percent |
|---|---:|---:|
| HR | 2 | 28.57 |
| IT | 3 | 42.86 |
| Sales | 2 | 28.57 |

**Cross-tabulation (two variables) with options**

```sas
proc freq data=sales;
    tables region*product_id / nocol norow nopercent;
run;
```

| Option (after `/`) | Meaning |
|---|---|
| `NOCUM` | Hide cumulative columns |
| `NOPERCENT`, `NOROW`, `NOCOL` | Hide percent / row percent / column percent in a cross-tab |
| `MISSING` | **Count missing values as a category** (by default they are excluded) |
| `LIST` | Print a cross-tab as a list instead of a grid |
| `OUT=dataset` | Save counts (and percents) to a dataset |
| `CHISQ` | Chi-square test of association |
| `ORDER=FREQ` | Sort categories by count instead of alphabetically |
| `WEIGHT var;` | Add up a variable instead of counting rows |

`PROC FREQ` is the tool for **text/category** variables; `PROC MEANS` is for **numbers**.

**Quick duplicate check:** `tables customer_id / noprint out=chk(where=(count>1));` lists keys that appear more than once.

---

#### 6.12 PROC REPORT

- **Purpose:** A **flexible, formatted report** where you decide each column's role, titles, totals and calculated columns. Like designing a PivotTable plus a printable layout.

```sas
proc report data=employee nowd;
    column department salary salary=avg_sal;
    define department / group "Department";
    define salary     / analysis sum  "Total Salary"   format=comma10.;
    define avg_sal    / analysis mean "Average Salary" format=comma10.;
    rbreak after / summarize;                         /* grand total row */
run;
```

| Department | Total Salary | Average Salary |
|---|---:|---:|
| HR | 92,000 | 46,000 |
| IT | 120,000 | 60,000 |
| Sales | 100,000 | 50,000 |
| (grand row) | 312,000 | 52,000 |

**Column roles in `DEFINE`**

| Usage | Meaning |
|---|---|
| `DISPLAY` | Show each row as is (default for character variables) |
| `GROUP` | Combine rows with the same value into one line |
| `ORDER` | Sort rows by this variable, show every row |
| `ACROSS` | Values become **column headings** (like a pivot) |
| `ANALYSIS` | Numbers to summarise (`sum`, `mean`, …); default for numeric variables |
| `COMPUTED` | A column you calculate yourself in a `COMPUTE` block |

**Computed column example**

```sas
proc report data=employee nowd;
    column employee_name salary bonus;
    define employee_name / display "Employee";
    define salary / display format=comma10.;
    define bonus  / computed format=comma10. "Bonus (10%)";
    compute bonus;
        bonus = salary * 0.10;
    endcomp;
run;
```

---

#### 6.13 PROC TABULATE

- **Purpose:** **Multi-level summary tables** (counts, sums, means) arranged exactly as you describe in a `TABLE` statement: `rows , columns`.

```sas
proc tabulate data=employee;
    class department;
    var salary;
    table department all,                         /* ROWS: each department + overall "All" */
          salary * (n sum mean) * f=comma10.;     /* COLUMNS: statistics, formatted */
run;
```

| | N | Sum | Mean |
|---|---:|---:|---:|
| HR | 2 | 92,000 | 46,000 |
| IT | 2 | 120,000 | 60,000 |
| Sales | 2 | 100,000 | 50,000 |
| All | 6 | 312,000 | 52,000 |

**Reading the `TABLE` statement**

| Symbol | Meaning |
|---|---|
| `,` | Separates **rows** (first) from **columns** (second) |
| `*` | **Nests** one thing inside another |
| (space) | Puts items **side by side** (concatenation) |
| `ALL` | Adds a total |
| `CLASS` | Categories (group variables); `VAR` = numbers to analyse |

---

#### 6.14 Basic SAS charts

**`PROC SGPLOT`** (✅ Base SAS, ODS Graphics) is the modern way.

```sas
proc sgplot data=employee;
    vbar department / response=salary stat=mean;     /* bar = average salary per department */
    title "Average salary by department";
run;
title;
```

Result: three bars: HR 46,000, IT 60,000, Sales 50,000.

| Chart | Statement | Typical use |
|---|---|---|
| Vertical / horizontal bar | `VBAR` / `HBAR` | Compare categories |
| Histogram | `HISTOGRAM salary;` | Distribution of one number |
| Line over time | `SERIES x=date y=amount;` or `VLINE` | Trends |
| Scatter | `SCATTER x=… y=…;` | Relationship between two numbers |
| Box plot | `VBOX salary / category=department;` | Compare spread between groups |

Other tools: `PROC CHART` (✅ simple text-style bars: `proc chart data=employee; vbar department / sumvar=salary type=mean; run;`), and `PROC GCHART`/`GPLOT` (🔑 SAS/GRAPH, older style).

---

#### 6.15 Which procedure should I choose?

| I want to… | Use | Instead of |
|---|---|---|
| See count/mean/min/max of numbers, by group | `PROC MEANS` | writing your own `PROC SQL GROUP BY` |
| **Create a dataset** of statistics | `PROC SUMMARY` (or `MEANS` with `NOPRINT`) | printing and copying |
| Check shape, percentiles, outliers, normality | `PROC UNIVARIATE` | `MEANS` (too shallow) |
| Count categories, cross-tabs, percentages, chi-square | `PROC FREQ` | `MEANS` (numbers only) |
| Build a **custom, polished report** with calculated columns | `PROC REPORT` | `PROC PRINT` |
| Build a **compact multi-way summary table** | `PROC TABULATE` | several `PROC MEANS` runs |
| Draw a quick chart | `PROC SGPLOT` | older `PROC CHART` |
| Just list rows | `PROC PRINT` | (Session 2) |

**Interview takeaway:** *"PROC MEANS vs PROC SUMMARY?"* → Same statistics and options. `MEANS` prints by default; `SUMMARY` does not (add `PRINT`). *"CLASS vs BY?"* → `CLASS` needs no sorting and gives a combined table; `BY` requires sorted data and gives separate sections.

---

### SESSION 7 — PROC SQL PROGRAMMING

**How this session differs from Session 4:** Session 4 taught the *building blocks* (joins vs MERGE, data modeling, schema changes, views). **This session is a practical query workbook**: you start with simple queries on the CUSTOMER / ORDERS / EMPLOYEE / SALES tables and build up to reporting queries. Where a topic was fully explained earlier, you get a short cross-reference and **new** examples instead of a repeat.

**Steps:** 7.1 Orientation · 7.2 Create tables and insert · 7.3 Tables from tables · 7.4 Select and filter · 7.5 Aliases · 7.6 Expressions and calculated fields · 7.7 WHERE operators · 7.8 CASE and nested CASE · 7.9 GROUP BY and summary functions · 7.10 WHERE vs HAVING · 7.11 Logical processing order · 7.12 Row numbers · 7.13 UPDATE and DELETE · 7.14 Appending tables · 7.15 Merging tables · 7.16 CALCULATED · 7.17 COALESCE · 7.18 Functions by example · 7.19 Views · 7.20 Stored procedures and environment limits

---

#### 7.1 Orientation: what is "standard SQL" and what is "SAS only"?

```sas
proc sql <options>;
    statement;        /* each statement ends with ; */
    statement;
quit;                 /* PROC SQL runs statements immediately; QUIT ends it */
```

| Category | Meaning | Examples |
|---|---|---|
| **Standard SQL** | Works in most databases | `SELECT`, `WHERE`, `GROUP BY`, `HAVING`, joins, `CASE`, `UNION`, `INSERT`, `UPDATE`, `DELETE` |
| **SAS `PROC SQL` extensions** | Work **only** in SAS | `CALCULATED`, `INTO :macro`, `OUTOBS=`, dataset options on tables (`orders(where=(...))`), formats and labels in `SELECT`, `OUTER UNION CORR`, using almost any **SAS function** |
| **DBMS-specific** | Work **only inside the database** (via pass-through) | Oracle `NVL`, `SYSDATE`; SQL Server `GETDATE()`, `ISNULL`; window functions like `ROW_NUMBER() OVER`; stored procedures; `TRUNCATE` |

**Useful `PROC SQL` options and helpers**

| Item | Meaning |
|---|---|
| `NOPRINT` | Run without printing results (use when only creating tables/macros) |
| `OUTOBS=n` | Stop after *n* output rows (quick preview) |
| `INOBS=n` | Read only *n* input rows (fast testing) |
| `NUMBER` | Show a row-number column in the printed result |
| `FEEDBACK` | Show the expanded query (e.g. what `*` became) in the log |
| `NOEXEC` / `EXEC` | Check syntax without running |
| `&SQLOBS`, `&SQLRC` | Automatic macro variables: rows produced, return code |
| `DICTIONARY.TABLES`, `DICTIONARY.COLUMNS` | Metadata tables for libraries, tables, columns |

---

#### 7.2 Creating tables and inserting values

Full explanation in [4.18](#418-creating-tables-and-inserting-values). **New in this session:** labels and formats, and verifying the result.

```sas
proc sql;
    create table work.returns (
        return_id   num      label='Return ID',
        order_id    num      label='Order ID',
        return_date num      format=date9. label='Return Date',
        reason      char(20) label='Reason'
    );

    insert into work.returns
        values (1, 5002, '20JAN2025'd, 'Damaged')
        values (2, 5005, '20FEB2025'd, 'Wrong item');

    describe table work.returns;          /* prints the table definition in the log */
    select * from work.returns;
quit;
```

| return_id | order_id | return_date | reason |
|---:|---:|---|---|
| 1 | 5002 | 20JAN2025 | Damaged |
| 2 | 5005 | 20FEB2025 | Wrong item |

Dates are inserted as **date literals** (`'20JAN2025'd`), never as plain text.

---

#### 7.3 Creating tables from existing tables

```sas
proc sql;
    create table work.orders_2025_q1 as
    select order_id, customer_id, order_date,
           amount          as order_amount,       /* renamed while copying */
           amount * 0.18   as tax format=comma10.2
    from orders
    where order_date between '01JAN2025'd and '31MAR2025'd;

    create table work.orders_copy as select * from orders;      /* data copy */
    create table work.orders_shell like orders;                  /* structure only */
quit;
```

| Form | Result |
|---|---|
| `CREATE TABLE x AS SELECT ...` | New table with the **result of a query** |
| `CREATE TABLE x LIKE y` | **Empty** table with the same columns as `y` |
| `INSERT INTO x SELECT ...` | Add the query result to an **existing** table |

A table created with `AS SELECT` has **no printed output**; use `select * from work.orders_2025_q1;` to view it.

---

#### 7.4 Selecting and filtering observations

```sas
proc sql outobs=3;
    title "Top 3 orders by amount";
    select order_id, customer_id, amount
    from orders
    order by amount desc;
quit;
title;
```

| order_id | customer_id | amount |
|---:|---:|---:|
| 5004 | 3 | 2200 |
| 5003 | 2 | 1500 |
| 5001 | 1 | 1200 |

| Task | Query |
|---|---|
| Unique values | `select distinct city from customer;` → Mumbai, Delhi, Chennai, Pune |
| Count unique values | `select count(distinct city) as n_cities from customer;` → 4 |
| Filter | `select * from orders where order_date >= '01FEB2025'd;` → 5004, 5005, 5006 |
| Sort | `order by city, credit_limit desc` (sorts by the first, then the second) |
| Sort by column position | `order by 2 desc` (second column in the `SELECT` list) |
| Rename/label in output | `select amount as order_amount label='Order Amount'` |

**Rules:** `ORDER BY` is the **last** clause. Missing numbers sort **first** (ascending). `SELECT *` is fine for exploring; list the columns in production code.

---

#### 7.5 Table aliases and column aliases

```sas
proc sql;
    select c.customer_name  as customer,          /* column alias */
           o.order_id       as order_no,
           o.amount         as order_amount
    from customer as c                            /* table alias */
         inner join orders as o
         on c.customer_id = o.customer_id
    where o.amount >= 1000;
quit;
```

| customer | order_no | order_amount |
|---|---:|---:|
| Alpha_Corp | 5001 | 1200 |
| Beta_Traders | 5003 | 1500 |
| Gamma_Stores | 5004 | 2200 |

| Alias type | Why | Rule |
|---|---|---|
| **Table alias** (`customer as c`) | Short names; **required** to tell columns apart in joins and self joins | `AS` is optional but clear; once you alias a table, use the alias everywhere |
| **Column alias** (`amount as order_amount`) | Rename an output column or name a calculation | Cannot be used in `WHERE` **unless** you write `CALCULATED order_amount` (7.16) |
| Ambiguous columns | A column in two tables must be written `c.customer_id` or SAS errors | |

---

#### 7.6 Expressions and calculated fields

```sas
proc sql;
    select order_id,
           amount,
           amount * 0.18                         as tax,
           amount + calculated tax               as total_with_tax,
           put(order_date, monname3.)            as month_name,
           catx(' - ', 'Order', put(order_id,4.)) as label_text
    from orders
    where order_id in (5001, 5002);
quit;
```

| order_id | amount | tax | total_with_tax | month_name | label_text |
|---:|---:|---:|---:|---|---|
| 5001 | 1200 | 216 | 1416 | Jan | Order - 5001 |
| 5002 | 800 | 144 | 944 | Jan | Order - 5002 |

Expressions can use `+ - * /`, `**` (power), `||` (join text), SAS functions, and `CASE`. **A missing value in arithmetic gives missing.**

---

#### 7.7 WHERE operators and operands in PROC SQL

| Kind | Operator | Example | Note |
|---|---|---|---|
| Compare | `= <> ^= > < >= <=` (`EQ NE GT LT GE LE`) | `amount <> 400` | `<>` and `^=` both mean "not equal" |
| List | `IN (...)`, `NOT IN` | `city in ('Mumbai','Pune')` | |
| Range | `BETWEEN a AND b` (inclusive) | `amount between 800 and 1500` | |
| Pattern | `LIKE` with `%` and `_` | `customer_name like 'G%'` | |
| Missing | `IS NULL` / `IS MISSING`, `IS NOT NULL` | `credit_limit is null` | Works for both numeric and character |
| Text search | `CONTAINS` (or `?`) | `customer_name contains 'Mart'` | 🌐 SAS extension |
| Sounds like | `=*` | `customer_name =* 'Alfa_Corp'` | 🌐 SAS extension |
| Subquery | `IN`, `EXISTS`, `ANY`, `ALL`, scalar `( select ... )` | 4.12 | |
| Logic | `AND`, `OR`, `NOT` | `city = 'Mumbai' and credit_limit > 60000` | `AND` is evaluated before `OR`; use brackets |

**Operands** can be columns, constants (`1000`, `'Mumbai'`, `'01JAN2025'd`), expressions, functions, or subquery results.

```sas
proc sql;
    select customer_name, city, credit_limit
    from customer
    where (city = 'Mumbai' or city = 'Pune')
      and (credit_limit > 25000 or credit_limit is null);
quit;
```

Result: Alpha_Corp (Mumbai, 50,000) and Gamma_Stores (Mumbai, 70,000). Echo_Retail (Pune, 20,000) fails the credit condition.

> **Missing-value trap (SAS-specific):** in `PROC SQL`, a missing number is treated as the **smallest** value, so `where credit_limit < 25000` **includes** Delta_Mart (missing). Add `and credit_limit is not null` when that is not wanted.

---

#### 7.8 CASE-WHEN and nested CASE (new example)

Basics are in [4.23](#423-case-when-and-nested-case). Here: bucketing and a nested rule on ORDERS.

```sas
proc sql;
    select order_id, amount, order_date,
           case
               when amount >= 1000 then
                    case when order_date >= '01FEB2025'd then 'Large-Feb'
                         else 'Large-Jan' end
               else 'Small'
           end as order_class
    from orders
    order by order_id;
quit;
```

| order_id | amount | order_date | order_class |
|---:|---:|---|---|
| 5001 | 1200 | 05JAN2025 | Large-Jan |
| 5002 | 800 | 17JAN2025 | Small |
| 5003 | 1500 | 20JAN2025 | Large-Jan |
| 5004 | 2200 | 02FEB2025 | Large-Feb |
| 5005 | 400 | 14FEB2025 | Small |
| 5006 | 900 | 20FEB2025 | Small |

**Counting with `CASE` (a pivot trick):**

```sas
proc sql;
    select sum(case when amount >= 1000 then 1 else 0 end) as n_large,
           sum(case when amount <  1000 then 1 else 0 end) as n_small
    from orders;
quit;
```

→ `n_large = 3`, `n_small = 3`.

---

#### 7.9 GROUP BY and summary functions

```sas
proc sql;
    select customer_id,
           count(*)              as n_orders,
           sum(amount)           as total_amount,
           avg(amount)           as avg_amount,
           max(amount)           as largest
    from orders
    group by customer_id
    order by total_amount desc;
quit;
```

| customer_id | n_orders | total_amount | avg_amount | largest |
|---:|---:|---:|---:|---:|
| 3 | 2 | 2600 | 1300 | 2200 |
| 1 | 2 | 2000 | 1000 | 1200 |
| 2 | 1 | 1500 | 1500 | 1500 |
| 6 | 1 | 900 | 900 | 900 |

| Summary function | Meaning |
|---|---|
| `COUNT(*)` | Number of rows |
| `COUNT(col)` | Number of **non-missing** values |
| `COUNT(DISTINCT col)` | Number of different values |
| `SUM`, `AVG` (or `MEAN`), `MIN`, `MAX` | Aggregates; **missing values are ignored** |
| `STD`, `VAR`, `NMISS`, `FREQ`, `RANGE` | SAS extras |

**Grouping rules**

- Every `SELECT` column that is **not** inside a summary function should be in `GROUP BY`.
- `GROUP BY 1, 2` uses column positions; `GROUP BY city, month` uses names.
- **SAS-specific "remerge":** if you select a detail column **and** a summary function without `GROUP BY`, SAS *remerges* the summary onto each row (with a log note) instead of failing. Standard SQL would give an error. It is handy for percentages:

```sas
proc sql;
    select order_id, amount,
           round(amount / sum(amount) * 100, 0.01) as pct_of_total
    from orders;
quit;
```

| order_id | amount | pct_of_total |
|---:|---:|---:|
| 5001 | 1200 | 17.14 |
| 5002 | 800 | 11.43 |
| 5003 | 1500 | 21.43 |
| 5004 | 2200 | 31.43 |
| 5005 | 400 | 5.71 |
| 5006 | 900 | 12.86 |

- **One argument vs several:** `MAX(amount)` is a summary over **rows**; `MAX(a, b, c)` (several arguments) works **across columns** in the same row.

---

#### 7.10 WHERE versus HAVING (new example)

Concepts in [4.22](#422-where-versus-having). Using both together:

```sas
proc sql;
    select customer_id, count(*) as n_orders, sum(amount) as total_amount
    from orders
    where order_date >= '15JAN2025'd          /* 1. keep only orders from 15 Jan onward */
    group by customer_id
    having sum(amount) > 1500;                /* 2. keep only customers whose total > 1500 */
quit;
```

| customer_id | n_orders | total_amount |
|---:|---:|---:|
| 3 | 2 | 2600 |

(After `WHERE`, totals are: customer 1 = 800, 2 = 1500, 3 = 2600, 6 = 900. Only customer 3 exceeds 1500.)

**Rule of thumb:** *Condition on a raw column → `WHERE`. Condition on a total/average/count → `HAVING`.*

---

#### 7.11 SQL clause execution and logical processing order

**In simple words:** You **write** `SELECT` first, but SQL **thinks** about the query in a different order. This is the **logical** order (how to reason about the result), **not** the physical steps SAS uses internally. SAS may optimise and reorder work as long as the result is the same.

| Logical step | Clause | What happens | Consequence |
|---:|---|---|---|
| 1 | `FROM` / `JOIN ... ON` | Pick the tables and combine them | Joins happen **before** any filtering by `WHERE` |
| 2 | `WHERE` | Filter **rows** | Cannot use summary functions; cannot use `SELECT` aliases (except with `CALCULATED`) |
| 3 | `GROUP BY` | Make groups | |
| 4 | `HAVING` | Filter **groups** | Can use summary functions |
| 5 | `SELECT` | Compute the output columns and aliases; `DISTINCT` | Aliases are born here |
| 6 | `ORDER BY` | Sort the result | **Can** use `SELECT` aliases, because they exist by now |
| 7 | `OUTOBS=` | Limit the rows shown | Limits **output**, after sorting |

```
 FROM / JOIN  →  WHERE  →  GROUP BY  →  HAVING  →  SELECT  →  ORDER BY  →  (OUTOBS)
```

**Why it matters (examples)**

| Mistake | Cause |
|---|---|
| `where total_amount > 1000` fails when `total_amount` is a `SUM(...) AS` alias | `WHERE` runs **before** `SELECT` and before grouping. Use `HAVING sum(amount) > 1000` |
| `order by total_amount` works | `ORDER BY` runs **after** `SELECT` |
| Filtering in `WHERE` is faster than in `HAVING` | Fewer rows reach `GROUP BY` |
| In a `LEFT JOIN`, a `WHERE` on the **right** table can silently turn it into an inner join | `WHERE` runs after the join and removes the NULL rows. Put the condition in `ON` instead |

**Interview takeaway:** *"In what order does SQL logically process a query?"* → FROM/JOIN → WHERE → GROUP BY → HAVING → SELECT → ORDER BY.

---

#### 7.12 Adding row numbers in PROC SQL

Method comparison is in [5.11](#511-creating-row-numbers-and-which-method-to-choose). In `PROC SQL`:

| Goal | How | Status |
|---|---|---|
| Show numbers in the printed result | `proc sql number; select ... ;` | ✅ Display only; not saved |
| Save a row number column | `monotonic() as rn` | 🌐 **Undocumented**; avoid in production |
| Save a row number (recommended) | Create the table in SQL, then add the number in a DATA step: `row_num + 1;` | ✅ Reliable |
| Number within groups (`ROW_NUMBER() OVER`) | Not in Base `PROC SQL`; use a DATA step with `FIRST.`, or pass the query to a database | ❌ in Base SAS |

**Recommended pattern**

```sas
proc sql;
    create table work.orders_sorted as
    select * from orders order by amount desc;
quit;

data work.orders_ranked;
    set work.orders_sorted;
    rank_by_amount + 1;           /* sum statement = running counter */
run;
```

| order_id | amount | rank_by_amount |
|---:|---:|---:|
| 5004 | 2200 | 1 |
| 5003 | 1500 | 2 |
| 5001 | 1200 | 3 |
| 5006 | 900 | 4 |
| 5002 | 800 | 5 |
| 5005 | 400 | 6 |

---

#### 7.13 UPDATE and DELETE (practice on a copy)

Statement overview is in [4.20](#420-dropping-deleting-and-truncating). Always practise on a **copy**:

```sas
proc sql;
    create table work.orders_edit as select * from orders;

    /* 1. one row */
    update work.orders_edit
        set amount = amount * 1.10
        where order_id = 5001;                          /* 1200 -> 1320 */

    /* 2. conditional change with CASE */
    update work.orders_edit
        set amount = case when amount < 1000 then amount + 50 else amount end;
                                                          /* 800->850, 400->450, 900->950 */

    /* 3. delete "orphan" orders that have no matching customer */
    delete from work.orders_edit
        where customer_id not in (select customer_id from customer);   /* removes 5006 */

    /* 4. fill missing credit limits using a subquery */
    create table work.customer_edit as select * from customer;
    update work.customer_edit
        set credit_limit = (select avg(credit_limit) from customer)
        where credit_limit is null;                       /* Delta_Mart gets 42,500 */
quit;
```

**Result of `work.orders_edit`**

| order_id | customer_id | amount |
|---:|---:|---:|
| 5001 | 1 | 1320 |
| 5002 | 1 | 850 |
| 5003 | 2 | 1500 |
| 5004 | 3 | 2200 |
| 5005 | 3 | 450 |

The log tells you **how many rows changed** (for example `NOTE: 1 row was updated in WORK.ORDERS_EDIT`). Read it.

> `UPDATE`/`DELETE` **without `WHERE`** changes or removes **every row**. There is no undo.

---

#### 7.14 Appending tables

| Goal | PROC SQL | Notes |
|---|---|---|
| Add rows into an existing table | `insert into big select * from small;` | Matches columns **by position** |
| Stack two queries into a new table | `select ... union all select ...` | Keeps duplicates; **by position** |
| Stack, remove duplicates | `union` | Sorts and removes duplicate rows (slower) |
| Stack **by column name** | `outer union corr` | 🌐 SAS extension; missing columns become missing |
| Rows in A but not in B | `except` | |
| Rows in both | `intersect` | |

**Warning:** SQL set operators combine columns **by position**, while the DATA step `SET` combines **by name**. Keep column order identical.

```sas
proc sql;
    create table work.sales_all2 as
    select * from sales_jan
    union all
    select * from sales_feb;                       /* 6 rows */

    /* Set operations on customer ids */
    select customer_id from customer
    except
    select customer_id from orders;                /* 4, 5 : customers who never ordered */

    select customer_id from customer
    intersect
    select customer_id from orders;                /* 1, 2, 3 */

    select customer_id from customer
    union
    select customer_id from orders;                /* 1, 2, 3, 4, 5, 6 (duplicates removed) */
quit;
```

(`SALES_JAN`/`SALES_FEB` are from [4.1](#41-concatenating-with-the-set-statement).) For appending large history tables, `PROC APPEND` is faster than rewriting everything (4.2).

---

#### 7.15 Merging tables (joins) in practice

Join types and `MERGE` differences are in [4.5 to 4.12](#part-b--horizontal-joins-and-merging). A realistic reporting query: **customer overview including customers with no orders**.

```sas
proc sql;
    select c.customer_id, c.customer_name, c.city,
           coalesce(o.n_orders, 0)     as n_orders,
           coalesce(o.total_amount, 0) as total_amount
    from customer as c
         left join
         (select customer_id, count(*) as n_orders, sum(amount) as total_amount
          from orders
          group by customer_id) as o
         on c.customer_id = o.customer_id
    order by c.customer_id;
quit;
```

| customer_id | customer_name | city | n_orders | total_amount |
|---:|---|---|---:|---:|
| 1 | Alpha_Corp | Mumbai | 2 | 2000 |
| 2 | Beta_Traders | Delhi | 1 | 1500 |
| 3 | Gamma_Stores | Mumbai | 2 | 2600 |
| 4 | Delta_Mart | Chennai | 0 | 0 |
| 5 | Echo_Retail | Pune | 0 | 0 |

**Pattern:** aggregate **first** (inline view), then join. This avoids double-counting that happens when you join detail rows and then sum.

**Tips**

- Prefer explicit `JOIN ... ON` to the old style `from a, b where a.k = b.k`.
- **Missing keys:** in `PROC SQL` on SAS datasets (and in a DATA step `MERGE`), a missing key **matches another missing key**. In most databases `NULL` never equals `NULL`. Remove rows with missing keys before joining if you do not want them to match.
- Check row counts before and after a join to catch accidental duplication (4.7).

---

#### 7.16 CALCULATED keyword (new example)

Reuse a computed column **in the same query** (SAS extension; see [4.24](#424-calculated-columns-and-calculated)). Here, in a comparison against the company average:

```sas
proc sql;
    select department,
           avg(salary)                                           as avg_salary,
           calculated avg_salary
               - (select avg(salary) from employee)              as diff_from_company
    from employee
    group by department
    order by calculated diff_from_company desc;
quit;
```

| department | avg_salary | diff_from_company |
|---|---:|---:|
| IT | 60000 | 8000 |
| Sales | 50000 | -2000 |
| HR | 46000 | -6000 |

(Company average = 52,000.) `CALCULATED` works in `SELECT`, `WHERE`, `HAVING`, `ORDER BY`, and `GROUP BY`. It refers **only to aliases from the same `SELECT`**, not to columns of other queries.

---

#### 7.17 COALESCE (new example)

Basic use is in [4.25](#425-coalesce-and-missing-value-handling). A deeper point: **how you treat missing values changes the answer.**

```sas
proc sql;
    select avg(salary)                                      as avg_ignoring_missing,
           avg(coalesce(salary, 0))                         as avg_missing_as_zero,
           nmiss(salary)                                    as n_missing
    from employee;
quit;
```

| avg_ignoring_missing | avg_missing_as_zero | n_missing |
|---:|---:|---:|
| 52000 | 44571.43 | 1 |

**Filling with a calculated value:**

```sas
proc sql;
    select employee_name,
           coalesce(salary, (select avg(salary) from employee)) as salary_filled
    from employee
    where employee_name = 'Neha';          /* -> 52000 */
quit;
```

`COALESCE(a, b, c, ...)` takes **many** arguments and returns the first non-missing. All must be the **same type**.

---

#### 7.18 Character, numeric and datetime SQL functions, by example

Most SAS functions can be used inside `PROC SQL`. Standard SQL has its own spellings; **in `PROC SQL` use the SAS spelling** (full function reference in Session 6).

```sas
proc sql;
    /* Character */
    select customer_name,
           upcase(customer_name)             as name_upper,
           scan(customer_name, 1, '_')       as first_word,
           length(strip(customer_name))      as name_len
    from customer
    where customer_id = 1;

    /* Numeric */
    select order_id, amount,
           round(amount * 0.18, 0.01)        as tax,
           ceil(amount / 1000)               as thousand_block,
           mod(order_id, 2)                  as odd_flag
    from orders
    where order_id in (5001, 5004);

    /* Date / datetime */
    select order_id, order_date,
           month(order_date)                                  as order_month,
           intnx('month', order_date, 1, 'b')                 as next_month_start format=date9.,
           intck('day', order_date, '28FEB2025'd)             as days_to_feb_end
    from orders
    where order_id in (5001, 5004);
quit;
```

| customer_name | name_upper | first_word | name_len |
|---|---|---|---:|
| Alpha_Corp | ALPHA_CORP | Alpha | 10 |

| order_id | amount | tax | thousand_block | odd_flag |
|---:|---:|---:|---:|---:|
| 5001 | 1200 | 216 | 2 | 1 |
| 5004 | 2200 | 396 | 3 | 0 |

| order_id | order_date | order_month | next_month_start | days_to_feb_end |
|---:|---|---:|---|---:|
| 5001 | 05JAN2025 | 1 | 01FEB2025 | 54 |
| 5004 | 02FEB2025 | 2 | 01MAR2025 | 26 |

**Functions by origin**

| Need | SAS (works in PROC SQL) | Standard SQL / DBMS spelling (**only** via pass-through) |
|---|---|---|
| Today's date | `today()` | `CURRENT_DATE`, `SYSDATE` (Oracle), `GETDATE()` (SQL Server) |
| Replace missing | `coalesce(x, 0)` | `NVL(x,0)` (Oracle), `ISNULL(x,0)` (SQL Server) |
| Substring | `substr(x, 1, 3)` | `SUBSTRING(x FROM 1 FOR 3)` |
| Date difference | `intck('day', d1, d2)` | `DATEDIFF(day, d1, d2)` |
| Add months | `intnx('month', d, 3, 'same')` | `ADD_MONTHS(d, 3)`, `DATEADD(...)` |
| Text → number | `input(x, 8.)` | `CAST(x AS INT)` |

If you write a DBMS-only function in a normal `PROC SQL` query against a SAS dataset, you get an error such as *"Function GETDATE could not be located"*.

---

#### 7.19 Views (practical use)

Concepts and table-vs-view comparison are in [4.27](#427-sql-views-and-stored-procedures). A practical use: **a reusable "customer summary" that is always current**.

```sas
proc sql;
    create view work.v_customer_summary as
    select c.customer_id, c.customer_name, c.city,
           count(o.order_id)           as n_orders,
           coalesce(sum(o.amount), 0)  as total_amount
    from customer as c left join orders as o
         on c.customer_id = o.customer_id
    group by c.customer_id, c.customer_name, c.city;

    select * from work.v_customer_summary where n_orders > 0;
quit;
```

| customer_id | customer_name | city | n_orders | total_amount |
|---:|---|---|---:|---:|
| 1 | Alpha_Corp | Mumbai | 2 | 2000 |
| 2 | Beta_Traders | Delhi | 1 | 1500 |
| 3 | Gamma_Stores | Mumbai | 2 | 2600 |

Add an order tomorrow and the same `select * from work.v_customer_summary` shows it. No rebuild is needed.

| Practical rule | Detail |
|---|---|
| **Use a view when** | You want fresh results, hide complexity, or restrict columns for users |
| **Use a table when** | The query is slow, results are reused many times, or you need a fixed snapshot |
| Views and `WORK` | A view stored in `WORK` disappears at the end of the session |
| Library paths | The tables the view reads must still be reachable (same `LIBNAME`s) when the view runs |
| Find views | `select * from dictionary.views where libname='WORK';` |

---

#### 7.20 Stored procedures and environment limitations

| Question | Answer |
|---|---|
| Does `PROC SQL` create stored procedures? | **No.** It has no `CREATE PROCEDURE`. |
| Can SAS run my **database's** stored procedure? | **Yes**, through explicit pass-through (`EXECUTE (...) BY dbms;`), if you have the right **SAS/ACCESS** product and database permissions |
| What replaces stored procedures in SAS? | **SAS macros** (`%macro`) or stored programs you `%INCLUDE` (Session 8) |
| Does the code work the same everywhere? | **No.** `PROC SQL` on SAS datasets, on a database library, and in Viya/CAS can differ in supported syntax, functions and speed |

```sas
proc sql;
    connect to sqlsvr (datasrc="MyDsn" user="your_user" password="XXXXXXXX");
    execute (exec dbo.refresh_daily_sales) by sqlsvr;     /* database's own stored procedure */
    disconnect from sqlsvr;
quit;
```

**Environment checklist before trusting a query**

1. Is the table a **SAS dataset** or a **database table**? (Some `UPDATE`/`DELETE`/`TRUNCATE` rules differ.)
2. Does the function exist in **SAS**, or only in the database?
3. Does your SAS version support the feature (for example `OUTER UNION CORR`, newer functions)? 🌐
4. Is the **SAS/ACCESS** licence installed for the database in question? 🔑

---

### SESSION 8 — SAS MACROS AND AUTOMATION

**Topics in this session:** 8.1 Automation basics and the macro processor · 8.2 Macro variables · 8.3 `%LET` · 8.4 Practical uses of macro variables · 8.5 Macro programs: structure and invocation · 8.6 Positional and keyword parameters · 8.7 `%GLOBAL` and `%LOCAL` · 8.8 `PROC SQL INTO` · 8.9 `%DO` loops · 8.10 `CALL SYMPUT` / `CALL SYMPUTX` · 8.11 `%IF %THEN` · 8.12 Macro functions · 8.13 Debugging options · 8.14 Inspecting macro variables · 8.15 `%INCLUDE` · 8.16 Storing reusable macros · 8.17 Reporting automation example · 8.18 Industry examples · 8.19 Scheduling

**The five required examples are:** simple macro (8.5) · parameterized macro (8.6) · macro loop (8.9) · conditional macro (8.11) · reporting automation (8.17).

---

#### 8.1 SAS automation fundamentals, and the macro processor versus DATA step execution

**In simple words:** Automation = **write the code once, reuse it many times with different inputs** (another department, another month, another file). The SAS **macro language** is a *text-substitution tool*: you write code with blanks to fill in, and SAS fills them in **before** running anything.

**Two different engines (very important)**

| | **Macro processor** | **SAS compiler / DATA step execution** |
|---|---|---|
| What it handles | **Text**: `%` statements, `&` variables | **Data**: rows, variables, values |
| When it runs | **First**, as your code is read | **After** the macro processor has produced plain SAS code |
| Triggers | `%` and `&` | `DATA`, `PROC`, `RUN` |
| Sees DATA step variables? | **No** (they don't exist yet) | Yes |

```
 Your code with %macros and &variables
        │
        ▼   MACRO PROCESSOR  (find-and-replace, loops that GENERATE code)
 Plain SAS code (what you'd have typed by hand)
        │
        ▼   SAS compiler and execution
 Data, reports, logs
```

**Consequences**

- `%if &x > 5` compares **macro variable text**. It **cannot** test a column such as `salary` (the data hasn't been read yet).
- A `%do` loop **writes code several times**. It does not loop over rows. (Row loops are DATA step `do` loops, Session 5.)
- To pass a value *from data into the macro world*, use `CALL SYMPUTX` or `PROC SQL INTO` (8.8, 8.10).

| Symbol | Meaning |
|---|---|
| `&name` | **Use** (resolve) macro variable `name` |
| `%name` | **Call** a macro or run a macro statement/function |
| `%let`, `%if`, `%do`, `%macro`, `%mend` | Macro statements |

---

#### 8.2 Macro variables

**In simple words:** A macro variable is a **named piece of text** that SAS substitutes wherever you write `&name`. It always holds **text** (even if it looks like a number).

| Type | Created by | Examples |
|---|---|---|
| **User-defined** | `%LET`, `INTO`, `CALL SYMPUTX`, macro parameters | `&dept`, `&n_emp` |
| **Automatic** (SAS creates them) | SAS itself | see table below |

**Common automatic macro variables**

| Variable | Holds | Example value |
|---|---|---|
| `&SYSDATE9` | Date the SAS session started (`DDMMMYYYY`) | `29OCT2026` |
| `&SYSDAY` | Day name | `Thursday` |
| `&SYSTIME` | Start time | `21:49` |
| `&SYSUSERID` | User id | `analyst1` |
| `&SYSVER` | SAS version | `9.4` |
| `&SYSLAST` | Name of the last dataset created | `WORK.EMP_TOP` |
| `&SYSERR`, `&SYSCC` | Return codes (0 = fine; 4 = warning; higher = error) | `0` |
| `&SQLOBS`, `&SQLRC` | Rows produced / return code of the last `PROC SQL` | `7` |

**Resolving rules**

| Situation | Write | Result |
|---|---|---|
| Normal use | `"&dept"` | `"IT"` |
| **Single quotes block resolution** | `'&dept'` | literally `&dept` (not replaced!) |
| Text right after the name | `&dept_total` looks for a variable named `dept_total` | Use a **period** as an end marker: `&dept._total` → `IT_total` |
| Period that belongs to the text (file extension) | `report_&dept..pdf` | `report_IT.pdf` (first `.` ends the name, second `.` is literal) |

---

#### 8.3 %LET

```sas
%let dept = IT;                                  /* text, no quotes needed */
%let min_salary = 55000;
%let today_txt = %sysfunc(today(), date9.);      /* use a function result */

%put dept is &dept, min_salary is &min_salary;   /* prints to the log */
```

Log: `dept is IT, min_salary is 55000`

**Rules**

- Leading and trailing blanks are **removed**. Quotes are **kept as part of the value**, so write `%let dept = IT;`, not `%let dept = "IT";` (then use `"&dept"` where quotes are needed).
- `%let` can be used **in open code** (anywhere) and **inside macros**.
- The right-hand side is text; arithmetic needs `%eval()` / `%sysevalf()` (8.12).

---

#### 8.4 Practical uses of macro variables

```sas
%let dept   = IT;
%let minsal = 55000;
%let rpt_dt = %sysfunc(today(), yymmddn8.);        /* e.g. 20261029 */

title "Employees in &dept earning at least &minsal";
proc print data=employee noobs;
    where department = "&dept" and salary >= &minsal;
    var employee_name salary;
run;
title;
```

| employee_name | salary |
|---|---:|
| Ravi | 62,000 |
| Meena | 58,000 |

| Use | Example |
|---|---|
| Change one value, not ten places | `where region = "&region"` |
| Folder paths | `libname mylib "&project_path/data";` |
| Date stamped file names | `ods pdf file="/home/user/out/report_&rpt_dt..pdf";` |
| Titles that update themselves | `title "Sales as of &sysdate9";` |
| Reuse a calculated value | `%let cutoff = %sysfunc(intnx(month, %sysfunc(today()), -3, b));` |

---

#### 8.5 Macro programs: structure and invocation

**Syntax**

```sas
%MACRO macro_name(parameter1, parameter2=default);
    ...SAS code and macro statements...
%MEND macro_name;

%macro_name(value1, parameter2=value2)       /* invocation: starts with %, no semicolon needed */
```

**Example 1 of 5: a simple reusable macro (no parameters)**

```sas
%macro top5_earners;
    proc sort data=employee out=work.emp_top;
        by descending salary;
    run;
    proc print data=work.emp_top(obs=5) noobs;
        var employee_name salary;
        title "Top 5 earners";
    run;
    title;
%mend top5_earners;

%top5_earners
```

| employee_name | salary |
|---|---:|
| Ravi | 62,000 |
| Meena | 58,000 |
| John | 51,000 |
| Priya | 49,000 |
| Karan | 47,000 |

**How it works**

1. SAS stores the macro text when it reaches `%mend` (**definition**: nothing runs yet).
2. When you call `%top5_earners`, the macro processor pastes the code and SAS runs it (**invocation**).
3. A `;` after the call is harmless but unnecessary.
4. Name the `%mend` the same as the `%macro` (good practice; it catches missing `%mend`s).

---

#### 8.6 Positional and keyword macro parameters

**Example 2 of 5: a parameterized macro**

```sas
%macro dept_report(dept, minsal=0);
    title "&dept employees earning at least &minsal";
    proc print data=employee noobs;
        where department = "&dept" and salary >= &minsal;
        var employee_name salary;
    run;
    title;
%mend dept_report;

%dept_report(IT)                           /* positional only: minsal uses its default 0 */
%dept_report(IT, minsal=60000)             /* positional + keyword */
%dept_report(minsal=50000, dept=Sales)     /* keyword form of both: any order */
```

**Results**

| Call | Rows shown |
|---|---|
| `%dept_report(IT)` | Ravi 62,000, Meena 58,000 (Neha is missing; a missing number is *smaller* than 0 and is dropped) |
| `%dept_report(IT, minsal=60000)` | Ravi 62,000 |
| `%dept_report(minsal=50000, dept=Sales)` | John 51,000 |

| | **Positional** | **Keyword** |
|---|---|---|
| Definition | `%macro m(a, b);` | `%macro m(a=, b=10);` |
| Call | `%m(1, 2)`; **order matters** | `%m(b=2, a=1)`; **any order** |
| Defaults | No | **Yes** (`b=10`) |
| Readability | Short | Self-documenting; best when there are many parameters |
| Mixed | Positional parameters must come **first**, then keyword ones | |

**Rules:** Parameter values are **text**. To pass a comma, use quoting: `%m(%str(a,b))`. Parameters are **local** to the macro.

---

#### 8.7 %GLOBAL and %LOCAL

| | **Global** | **Local** |
|---|---|---|
| Visible | Everywhere in the SAS session | **Only inside** the macro that created it |
| Created by | `%LET` in open code, `%GLOBAL`, `INTO`/`SYMPUTX` at global scope | `%LOCAL`, macro parameters, `%LET` inside a macro (if no global of that name exists) |
| Lifetime | Until the session ends | Until the macro finishes |

```sas
%let total = 100;                      /* global */

%macro demo;
    %local total;                      /* protect the global: make a private copy */
    %let total = 5;
    %put Inside macro:  &total;        /* 5 */
%mend demo;

%demo
%put Outside macro: &total;            /* 100, global value untouched */
```

Without `%local total;`, the `%let` inside the macro would **overwrite the global** `total` (Outside would print 5). That is a classic bug.

**Create a global variable from inside a macro**

```sas
%macro get_count(ds);
    %global row_count;
    proc sql noprint;  select count(*) into :row_count trimmed from &ds;  quit;
%mend get_count;

%get_count(employee)
%put Rows: &row_count;                 /* 7 */
```

**Good practice:** declare loop counters and helper variables with `%local` (for example `%local i;`).

---

#### 8.8 PROC SQL INTO: creating macro variables from data

**In simple words:** Ask a question with SQL and **store the answer in a macro variable**.

```sas
proc sql noprint;
    /* one value */
    select count(*)                      into :n_emp   trimmed from employee;
    select avg(salary) format=comma10.0  into :avg_sal trimmed from employee;

    /* several values into numbered variables: dept1, dept2, ... */
    select distinct department into :dept1 - :dept3 from employee order by department;

    /* a whole list in one variable */
    select distinct department into :dept_list separated by ", " from employee order by department;
quit;

%put &n_emp employees, average &avg_sal;      /* 7 employees, average 52,000 */
%put &dept1 &dept2 &dept3;                     /* HR IT Sales */
%put &dept_list;                               /* HR, IT, Sales */
```

| Form | Meaning |
|---|---|
| `INTO :var` | Stores the **first row's** value |
| `INTO :v1 - :vN` | Stores row 1 in `v1`, row 2 in `v2`, … |
| `INTO :var SEPARATED BY ", "` | Stores **all** rows in one variable, joined |
| `TRIMMED` | Removes the leading blanks SAS adds to numbers |
| `&SQLOBS` | Right after the query: the number of rows retrieved |

**Count first, then loop** (works for any number of groups):

```sas
proc sql noprint;
    select count(distinct department) into :n_dept trimmed from employee;
    select distinct department into :dept1 - :dept&n_dept from employee order by department;
quit;
```

---

#### 8.9 %DO loops

Macro `%DO` loops **generate code repeatedly**. They work **only inside a macro**.

```sas
%macro by_dept;
    %local i;
    proc sql noprint;
        select count(distinct department) into :n_dept trimmed from employee;
        select distinct department into :dept1 - :dept&n_dept from employee order by department;
    quit;

    %do i = 1 %to &n_dept;
        title "Department: &&dept&i";
        proc means data=employee n sum mean maxdec=0;
            where department = "&&dept&i";
            var salary;
        run;
    %end;
    title;
%mend by_dept;

%by_dept
```

This runs `PROC MEANS` **three times** (HR, IT, Sales).

**Understanding `&&dept&i`** (the macro processor reads it twice)

| Pass | What happens when `i = 2` |
|---|---|
| Start | `&&dept&i` |
| Pass 1 | `&&` becomes `&`; `&i` becomes `2` → `&dept2` |
| Pass 2 | `&dept2` becomes `IT` |

**Loop types**

| Statement | Meaning |
|---|---|
| `%do i = 1 %to 10 %by 2; ... %end;` | Counted loop |
| `%do %while (&x < 5); ... %end;` | Repeats **while** true (check first) |
| `%do %until (&x >= 5); ... %end;` | Repeats **until** true (runs at least once) |

**Example 3 of 5: a macro loop (generating file names)**

```sas
%macro load_months(start=1, end=3);
    %local m mm;
    %do m = &start %to &end;
        %let mm = %sysfunc(putn(&m, z2.));            /* 1 -> 01 */
        proc import datafile="/home/user/data/sales_2025&mm..csv"
                    out=work.sales_&mm dbms=csv replace;
            getnames=yes;
        run;
        proc append base=work.sales_all data=work.sales_&mm force;
        run;
    %end;
%mend load_months;

%load_months(start=1, end=3)         /* reads sales_202501.csv, sales_202502.csv, sales_202503.csv */
```

(`&mm..csv`: the first period ends the variable name, the second is the dot of `.csv`.)

---

#### 8.10 CALL SYMPUT and CALL SYMPUTX

**In simple words:** They **copy a DATA step value into a macro variable while the DATA step runs**.

```sas
data _null_;
    set employee end=last;
    where department = "IT";
    total + salary;                                  /* running total, missing ignored */
    if last then call symputx("it_total", total);
run;

%put IT payroll is &it_total;                        /* 120000 */
```

| | `CALL SYMPUT` | `CALL SYMPUTX` (**prefer**) |
|---|---|---|
| Removes leading/trailing blanks | **No** (a number can arrive as `"      120000"`) | **Yes** |
| Number → text conversion note in log | Yes (noisy) | No |
| Choose scope | Not easily | Third argument: `"G"` global, `"L"` local, `"F"` default |
| Available since | Older versions | SAS 9 |

```sas
call symputx("it_total", total, "G");               /* force global */
```

**Timing rule (classic interview point)**

A macro variable created by `CALL SYMPUTX` is **not available as `&var` inside the same DATA step**, because `&var` is resolved *before* the step runs. Use it **after the step ends**, or use `symget("var")` inside the step.

**`%LET` vs `CALL SYMPUTX` vs `INTO`**

| Tool | Value comes from | When it runs |
|---|---|---|
| `%LET` | Text you type (or a macro function) | Macro-processing time |
| `CALL SYMPUTX` | A DATA step variable | While the DATA step **executes** |
| `PROC SQL INTO` | A query result | While `PROC SQL` runs |

---

#### 8.11 Conditional execution with %IF and %THEN

```sas
%macro run_report(dept=ALL);
    %if &dept = ALL %then %do;
        proc print data=employee noobs;  var employee_name department salary;  run;
    %end;
    %else %do;
        proc print data=employee noobs;
            where department = "&dept";
            var employee_name department salary;
        run;
    %end;
%mend run_report;

%run_report()               /* all 7 employees */
%run_report(dept=HR)        /* Asha and Karan */
```

**Example 4 of 5: a conditional macro that checks first (safe printing)**

```sas
%macro safe_print(ds);
    %if %sysfunc(exist(&ds)) %then %do;
        proc print data=&ds(obs=5) noobs;  run;
    %end;
    %else %put WARNING: Dataset &ds does not exist, nothing printed.;
%mend safe_print;

%safe_print(work.employee)       /* prints 5 rows */
%safe_print(work.nothing)        /* log shows the WARNING, no error */
```

**Rules**

| Rule | Detail |
|---|---|
| `%IF` tests **macro text**, not data columns | `%if &dept = HR` ✓; `%if department = "HR"` ✗ for a column |
| **No quotes** around text | `%if &dept = HR` (`"HR"` would include the quote marks in the comparison) |
| Text comparison is **case-sensitive** | Use `%upcase(&dept)` to be safe |
| Whole numbers compare numerically | `%if &n > 5`. For decimals use `%sysevalf(&x > 2.5)` |
| `%THEN %DO; ... %END;` | Needed when you run **several** statements |
| `%ELSE` pairs with the nearest `%IF` | |
| Open-code `%IF` (outside a macro) | 🌐 Allowed only from SAS **9.4M5** onward; otherwise put it in a macro |

**Do not confuse** `%IF` (macro: decides **what code to generate**) with `IF` (DATA step: decides **what to do with each row**).

---

#### 8.12 Macro functions

| Function | Purpose | Example | Result |
|---|---|---|---|
| `%UPCASE(x)` / `%LOWCASE(x)` | Change case | `%upcase(asha)` | `ASHA` |
| `%SUBSTR(x, start, len)` | Part of text | `%substr(&sysdate9, 6, 4)` | `2026` (for `29OCT2026`) |
| `%SCAN(x, n, delim)` | n-th word | `%scan(HR IT Sales, 2)` | `IT` |
| `%INDEX(x, find)` | Position of text | `%index(Mumbai, b)` | `4` |
| `%LENGTH(x)` | Length of text | `%length(Mumbai)` | `6` |
| `%EVAL(expr)` | **Integer** arithmetic and comparisons | `%eval(2 + 3)` | `5` |
| `%SYSEVALF(expr)` | **Decimal** arithmetic | `%sysevalf(2.5 * 2)` | `5` |
| `%SYSFUNC(func(args), fmt)` | Use **DATA step functions** in macro code | `%sysfunc(today(), date9.)` | `29OCT2026` |
| `%STR(text)` / `%NRSTR(text)` | **Hide** special characters (`;` `,` `'`) / also hide `&` and `%` | `%let list = %str(a,b);` | text with the comma |
| `%QUOTE`, `%BQUOTE` | Quote values at **run time** (for values that may contain `'`, `,`, `;`) | `%bquote(&name)` | safe text |
| `%SYMEXIST(name)` | Does the macro variable exist? | `%symexist(dept)` | `1` or `0` |

**Example: using a DATA step function in macro code**

```sas
%let today_txt = %sysfunc(today(), yymmdd10.);                       /* 2026-10-29 */
%let first_of_month = %sysfunc(intnx(month, %sysfunc(today()), 0, b), date9.);
%put Today=&today_txt, month started on &first_of_month;
```

Inside `%sysfunc`, **do not put quotes** around character arguments such as `month` and `b`.

---

#### 8.13 Macro debugging options

```sas
options mprint mlogic symbolgen;       /* turn ON */
%dept_report(IT, minsal=60000)
options nomprint nomlogic nosymbolgen; /* turn OFF (logs get long!) */
```

| Option | Shows in the log | Use it to find |
|---|---|---|
| `MPRINT` | The **SAS code the macro generated** | "What code actually ran?" |
| `MLOGIC` | Macro **execution flow**: parameter values, `%IF` results, `%DO` counters | Wrong branch, loop not running |
| `SYMBOLGEN` | **Each `&variable` resolution** (`SYMBOLGEN: Macro variable DEPT resolves to IT`) | Wrong or missing values, quote problems |
| `SOURCE2` | Code brought in by `%INCLUDE` | |
| `MERROR` (default on) | Warns about an unresolved `&var` or unknown `%macro` | Typos |

**Log excerpt** with `MPRINT`:

```
MPRINT(DEPT_REPORT):   title "IT employees earning at least 60000";
MPRINT(DEPT_REPORT):   proc print data=employee noobs;
MPRINT(DEPT_REPORT):   where department = "IT" and salary >= 60000;
```

**Other helpers:** `%put &=dept;` (prints `DEPT=IT`), your own messages `%put ERROR: ...;` / `%put WARNING: ...;`, and checking `&SYSCC` / `&SYSERR` after important steps.

**Common problems**

| Symptom | Likely cause |
|---|---|
| `WARNING: Apparent symbolic reference X not resolved` | Typo, or the variable doesn't exist/was local |
| `&var` printed literally | Used **single quotes** |
| `ERROR: A character operand was found in the %EVAL function` | Comparing decimals/text with `%eval`; use `%sysevalf` or quotes |
| Macro doesn't run | Missing `%mend`, or the macro was **not defined** in this session |

---

#### 8.14 Inspecting macro variables

```sas
%put &dept;                 /* one variable */
%put &=dept &=minsal;       /* shows names too: DEPT=IT MINSAL=55000 */
%put _user_;                /* all user-defined, with scope */
%put _global_;              /* all global ones */
%put _local_;               /* local ones (inside a macro) */
%put _automatic_;           /* SAS-created ones */
%put _all_;                 /* everything */

proc sql;
    select name, scope, value from dictionary.macros where scope = "GLOBAL";
quit;
```

`SASHELP.VMACRO` shows the same information.

---

#### 8.15 %INCLUDE

**In simple words:** "Run this other `.sas` file here, as if I had typed it." Used for **setup files** (library names, macros) shared by many programs.

```sas
%include "/home/user/sas/setup.sas";                 /* a file path */
%include "/home/user/sas/macros/dept_report.sas" / source2;   /* also echo the code to the log */

filename mypgm "/home/user/sas/programs";
%include mypgm(load_data.sas);                       /* fileref + member */
```

| Rule | Detail |
|---|---|
| Runs the file's code **in your session** | Its `LIBNAME`s, macros and datasets become available |
| Can be placed **anywhere a statement can start** | Not in the middle of another statement |
| Paths | 🌐 Absolute paths differ between Windows and Linux/UNIX; keep them in a macro variable such as `%let proj = /home/user/sas;` |
| Typical use | A `main.sas` that starts with `%include "&proj/setup.sas";` |

---

#### 8.16 Storing and reusing macros

| Method | How | Good for |
|---|---|---|
| **1. Put macros in a `.sas` file and `%INCLUDE` it** | `%include "&proj/macros.sas";` | Simple; one file with many macros |
| **2. Autocall library** | One file per macro; the **file name must match the macro name** (`dept_report.sas` contains `%macro dept_report`). Then: `options mautosource sasautos=("/home/user/sas/macros" sasautos);` | Teams; macros load **only when first called** |
| **3. Stored compiled macros** | `libname mac "/home/user/sas/mac"; options mstored sasmstore=mac; %macro dept_report(dept) / store; ... %mend;` | Speed, or hiding source code |

**Autocall example**

```sas
/* File /home/user/sas/macros/count_missing.sas */
%macro count_missing(ds, var);
    %local nm;
    proc sql noprint;
        select nmiss(&var) into :nm trimmed from &ds;
    quit;
    %put NOTE: &var has &nm missing values in &ds..;
%mend count_missing;

/* In any program: */
options mautosource sasautos=("/home/user/sas/macros" sasautos);
%count_missing(employee, salary)       /* NOTE: salary has 1 missing values in employee. */
```

---

#### 8.17 Practical reporting automation (loop + parameters + date-stamped files), example 5 of 5

**Goal:** One PDF salary report per department, named with today's date, from a single program.

```sas
%let out_dir = /home/user/out;                          /* change once */
%let rpt_dt  = %sysfunc(today(), yymmddn8.);            /* 20261029 */

/* 1. ONE report (parameterised) */
%macro dept_pdf(dept);
    ods pdf file="&out_dir/salary_&dept._&rpt_dt..pdf" style=journal;
    title "Salary summary: &dept (as of &rpt_dt)";
    proc means data=employee n nmiss sum mean maxdec=0;
        where department = "&dept";
        var salary;
    run;
    proc print data=employee noobs;
        where department = "&dept";
        var employee_name hire_date salary;
        format hire_date date9. salary comma10.;
    run;
    title;
    ods pdf close;
%mend dept_pdf;

/* 2. LOOP over every department found in the data */
%macro run_all;
    %local i;
    proc sql noprint;
        select count(distinct department) into :n_dept trimmed from employee;
        select distinct department into :dept1 - :dept&n_dept from employee order by department;
    quit;
    %do i = 1 %to &n_dept;
        %dept_pdf(&&dept&i)
    %end;
    %put NOTE: &n_dept reports written to &out_dir;
%mend run_all;

%run_all
```

**Files created:** `salary_HR_20261029.pdf`, `salary_IT_20261029.pdf`, `salary_Sales_20261029.pdf`. If a new department appears in the data tomorrow, a new report appears **with no code change**.

**Alternative loop with no macro loop: `CALL EXECUTE`** (data-driven calls)

```sas
proc sql;  create table work.depts as select distinct department from employee;  quit;

data _null_;
    set work.depts;
    call execute(cats('%nrstr(%dept_pdf)(', department, ')'));     /* queue one macro call per row */
run;
```

**Report-quality checklist:** Always `ods ... close;` (even after errors), clear titles with `title;`, avoid spaces in file names, and check the log for `ERROR`/`WARNING` before sending the files.

---

#### 8.18 Industry-oriented macro examples

| Industry | Use of macros |
|---|---|
| **Banking** | A branch-level daily exposure report: `%branch_report(branch=MUMBAI01)` run for every branch from a list |
| **Retail** | Monthly sales file loader (`%load_months`) appending 12 files into one history table |
| **Healthcare** | Same data-quality checks (`%count_missing`) run on every extract before analysis |
| **Insurance** | A claims validation macro with `%if &syscc > 4 %then ...` to stop the flow on errors |
| **Any** | One `%include`d setup file for libraries and paths, so moving from test to production changes **one line** |

**Data-quality macro, ready to reuse (with a conditional stop)**

```sas
%macro check_ds(ds, var, max_missing=0);
    %local nm;
    proc sql noprint;
        select nmiss(&var) into :nm trimmed from &ds;
    quit;
    %if &nm > &max_missing %then %do;
        %put ERROR: &var in &ds has &nm missing values (limit &max_missing).;
    %end;
    %else %put NOTE: &var in &ds passed the missing-value check.;
%mend check_ds;

%check_ds(employee, salary)                     /* ERROR: salary in employee has 1 missing values (limit 0). */
%check_ds(employee, salary, max_missing=1)      /* NOTE: ... passed ... */
```

---

#### 8.19 Macro scheduling

**Important:** Defining or calling a macro **does not schedule anything**. A macro runs only when some program **calls it**, and a program runs only when something **starts SAS**. Scheduling needs a **scheduler** or an environment that runs jobs for you.

| Environment | How scheduling is done | Tag |
|---|---|---|
| **Windows** | Windows Task Scheduler runs `sas.exe -sysin program.sas -log program.log` | 🌐 |
| **Linux/UNIX** | `cron` entry running SAS in batch mode | 🌐 |
| **SAS Enterprise Guide** | Can schedule a project through the operating system scheduler | 🌐 |
| **SAS Management Console / Schedule Manager** or **LSF Process Manager** | Server-side scheduling for SAS 9.4 platforms | 🔑 🌐 |
| **SAS Viya** | Jobs and Flows / Job Scheduling in the Viya platform | 🌐 |
| **External schedulers** | Control-M, Autosys, Airflow, etc. call SAS | 🌐 |

**Linux example: run the report every weekday at 07:00 (cron)**

```
0 7 * * 1-5  /opt/sas/sas -sysin /home/user/sas/main.sas -log /home/user/logs/main.log
```

(`main.sas` would contain `%include "&proj/setup.sas";` and `%run_all`.) Exact paths and options depend on your installation.

**Scheduling checklist**

1. The program must run **without anyone clicking** (no prompts, no interactive windows).
2. Use **absolute paths** and your own `LIBNAME`s inside the program.
3. Write a **log file** and check it (or send an alert when `&SYSCC > 4`).
4. Use **date macro variables** (`&sysdate9`, `%sysfunc(today())`) for file names.
5. Ensure the scheduler's account has permission to the data and output folders.

**Interview takeaways**

- *"Difference between `&x` and `%x`?"* → `&x` resolves a **macro variable**; `%x` **calls** a macro or macro statement.
- *"Why `&&dept&i`?"* → Two-pass resolution lets you build a variable name from a counter and then read its value.
- *"`SYMPUT` vs `SYMPUTX`?"* → `SYMPUTX` trims blanks, has no conversion notes, and can set the scope. Prefer it.
- *"Can `%IF` test a data column?"* → No. `%IF` runs **before** the data exists; use the DATA step `IF`.
- *"Where is a macro variable created inside a macro stored?"* → Local scope, unless a global of the same name already exists (then the global is changed) or it was declared `%GLOBAL`.

---

## 4. Essential SAS Syntax and Keyword Cheat Sheet

#### 4.1 Program skeletons

```sas
/* ---------- DATA step ---------- */
libname mylib "/path/to/folder";               /* global statement */
options nocenter;                              /* global option    */

data mylib.result(keep=a b rename=(a=x));      /* output dataset + options */
    set mylib.input(where=(flag=1) obs=100);   /* input  dataset + options */
    length status $ 10;                        /* attributes before first use */
    format d date9.;                           /* display format */
    if score >= 50 then status = "Pass";
    else status = "Fail";
    total + score;                             /* sum statement */
    output;                                    /* optional explicit output */
run;

/* ---------- PROC step ---------- */
proc sort data=mylib.result out=work.sorted nodupkey;
    by x descending y;
run;

proc print data=work.sorted(obs=10) noobs label;
    var x y;
    where x > 5;
    title "Title";
run;

/* ---------- PROC SQL ---------- */
proc sql;
    create table work.t as
    select a.k, sum(b.v) as total
    from a left join b on a.k = b.k
    where a.flag = 1
    group by a.k
    having calculated total > 100
    order by total desc;
quit;

/* ---------- Macro ---------- */
%let dept = IT;
%macro demo(p1, p2=10);
    %if &p1 = X %then %do;  ...  %end;
%mend demo;
%demo(X)
```

#### 4.2 Core statements

| Statement | Used in | Purpose | Session |
|---|---|---|---|
| `DATA` / `RUN` | DATA step | Start / execute a step | 1 |
| `SET` | DATA step | Read existing dataset(s); stack | 2, 4 |
| `MERGE` + `BY` | DATA step | Side-by-side by key | 4 |
| `UPDATE` + `BY` | DATA step | Apply corrections to a master | 5 |
| `INPUT`, `INFILE`, `DATALINES`/`CARDS` | DATA step | Read raw data | 1, 3 |
| `FILE`, `PUT` | DATA step | Write raw data/text | 3 |
| `LENGTH`, `FORMAT`, `INFORMAT`, `LABEL` | DATA step | Set variable attributes | 1, 2 |
| `KEEP`, `DROP`, `RENAME` | DATA step | Choose / rename columns | 2 |
| `WHERE` | DATA / PROC | Filter before reading rows | 2 |
| `IF cond;` | DATA step | **Subsetting** IF (drops rows) | 2 |
| `IF ... THEN ... ELSE` | DATA step | Conditional logic | 2 |
| `DO ... END` / `DO i = 1 TO n` | DATA step | Group statements / loop | 2, 5 |
| `SELECT ... WHEN ... OTHERWISE ... END` | DATA step | Many-way choice | below |
| `ARRAY` | DATA step | Name a group of variables | 5 |
| `RETAIN` | DATA step | Keep a value across rows | 5 |
| `var + expr;` | DATA step | Sum statement | 5 |
| `OUTPUT` | DATA step | Write the current row | 2 |
| `BY` (with `FIRST.`/`LAST.`) | DATA / PROC | Group processing | 5 |
| `STOP`, `LEAVE`, `CONTINUE`, `DELETE`, `RETURN` | DATA step | Control flow | 3, 5 |
| `LIBNAME`, `FILENAME` | Global | Nicknames for folders/files/databases | 1, 3 |
| `OPTIONS` | Global | Session settings | 2, 8 |
| `TITLE`, `FOOTNOTE` | Global | Report headings | 2 |
| `%INCLUDE` | Global | Run another program file | 8 |

**`SELECT/WHEN` (a tidy alternative to many `ELSE IF`s)**

```sas
select (department);
    when ("HR")          team = "Support";
    when ("IT", "Sales") team = "Core";
    otherwise            team = "Other";
end;
```

#### 4.3 Dataset options (inside brackets after a dataset name)

| Option | Example | Effect |
|---|---|---|
| `KEEP=` / `DROP=` | `set a(keep=id name)` | Choose columns |
| `RENAME=` | `a(rename=(old=new))` | Rename columns |
| `WHERE=` | `a(where=(x > 5))` | Filter rows |
| `OBS=` / `FIRSTOBS=` | `a(firstobs=3 obs=10)` | Row range (last row / first row) |
| `IN=` | `merge a(in=ina) b` | Flag: did this dataset contribute? |
| `INDSNAME=` | `set a b indsname=src` | Record the source dataset (on the `SET` statement) |
| `END=` | `set a end=last` | Flag for the last row (on the `SET` statement) |
| `POINT=` / `NOBS=` | `set a point=p nobs=n` | Direct access / number of rows (on `SET`) |
| `LABEL=` | `data x(label="My table")` | Dataset description |

#### 4.4 Operators and special values

| Kind | Symbols |
|---|---|
| Arithmetic | `+ - * / **` |
| Comparison | `= ^= ~= <> > < >= <=` and `EQ NE GT LT GE LE`, `IN (...)` |
| Logical | `AND` (`&`), `OR` (`\|`), `NOT` (`^`) |
| Text join | `\|\|` |
| Missing (numeric) | `.` and special `.A`–`.Z`, `._` |
| Missing (character) | `" "` |
| Special `WHERE` operators | `BETWEEN`, `LIKE`, `CONTAINS`, `IS MISSING`, `IS NULL`, `=*`, `SAME AND` |
| Date literals | `'15JAN2025'd`, `'14:30:00't`, `'15JAN2025:14:30:00'dt` |
| Variable lists | `q1-q4`, `_numeric_`, `_character_`, `_all_`, `name:` (prefix list) |
| Comments | `/* block */`, `* line;` (ends at `;`) |

**Order of evaluation:** `**` first; then `* /`; then `+ -`; then comparisons; then `AND`; then `OR`. Use brackets to be sure.

#### 4.5 Frequently used procedures

| Procedure | One-line purpose | Session |
|---|---|---|
| `PROC PRINT` | List rows | 2 |
| `PROC SORT` | Sort; remove duplicates | 2 |
| `PROC CONTENTS` / `DATASETS` | Describe / manage datasets | 1 |
| `PROC COPY` | Copy datasets between libraries | 1 |
| `PROC IMPORT` / `EXPORT` | Read / write CSV, Excel… | 1, 3 |
| `PROC FORMAT` | User-defined formats | 2 |
| `PROC APPEND` | Add rows to a big dataset | 4 |
| `PROC SQL` | SQL queries, tables, views | 4, 7 |
| `PROC TRANSPOSE` | Rows ↔ columns | 5 |
| `PROC COMPARE` | Compare two datasets | 5 |
| `PROC RANK` | Rank values | 5 |
| `PROC MEANS` / `SUMMARY` | Descriptive statistics | 6 |
| `PROC UNIVARIATE` | Distribution details | 6 |
| `PROC FREQ` | Category counts, cross-tabs | 6 |
| `PROC REPORT` / `TABULATE` | Formatted summary reports | 6 |
| `PROC SGPLOT` | Charts | 6 |
| `PROC SURVEYSELECT` 🔑 | Random samples (SAS/STAT) | 3 |
| `PROC DOWNLOAD` / `UPLOAD` 🔑 | Remote copies (SAS/CONNECT) | 3 |

#### 4.6 Common formats and informats

| Name | Type | Example |
|---|---|---|
| `w.` / `w.d` | Numeric | `8.2` |
| `COMMAw.d`, `DOLLARw.d`, `PERCENTw.d` | Numeric display | `comma10.2` |
| `$w.` | Character | `$20.` |
| `DATE9.`, `DDMMYY10.`, `MMDDYY10.`, `YYMMDD10.`, `MONYY7.`, `WORDDATE.` | Date | `date9.` |
| `TIME8.`, `DATETIME20.` | Time / datetime | |
| `Zw.` | Leading zeros | `z5.` |
| `ANYDTDTE.` | Informat: guesses date style | |

---

## 5. DATA Step versus PROC Step

| Feature | **DATA step** | **PROC step** | **PROC SQL** (special case) |
|---|---|---|---|
| Starts with | `DATA name;` | `PROC name;` | `PROC SQL;` |
| Ends with | `RUN;` | `RUN;` | `QUIT;` |
| Main job | Create/transform datasets, read raw files, write files | Run a prebuilt task (sort, summarise, report, analyse) | SQL queries and table management |
| How it processes | **Row by row** in a loop (PDV) | Whole dataset, using internal code | **Set-based**: whole result at once |
| You write | Programming logic (`IF`, `DO`, arrays, `RETAIN`) | Options and statements for that procedure | SQL clauses |
| Output | A dataset (always) | Report, and optionally datasets (`OUT=`) | Report and/or tables/views |
| Sees `FIRST.`/`LAST.`, `_N_`, PDV | **Yes** | No | No |
| Sorting needed for `BY`/merge | Yes | Yes (for `BY`) | **No** |
| Best at | Sequential logic, row-wise calculations, complex conditions, reading messy files | Quick standard tasks | Joins, summaries, subqueries, set operations |
| Weak at | Many-table joins, ad hoc summaries | Anything unusual | Row-to-row logic (previous row, running totals) |
| Typical errors | Missing semicolon, wrong length, no `OUTPUT` logic | Wrong option name, unsorted `BY` data | Missing `QUIT`, ambiguous columns, wrong `GROUP BY` |

**Rule of thumb:** *Need to look at the previous row, retain a value or loop within a row → DATA step. Need to join, summarise or filter with SQL logic → `PROC SQL`. Need a standard statistic or report → the matching `PROC`.*

---

## 6. SAS Functions Master Reference

Detailed syntax, examples and outputs are in [Session 6](#session-6--sas-functions-and-summary-reporting). This is the **quick-lookup index**. Functions are **not repeated** here.

#### 6.1 "I want to…" lookup

| I want to… | Use | Notes |
|---|---|---|
| Change case | `UPCASE`, `LOWCASE`, `PROPCASE` | |
| Remove blanks | `STRIP` (both ends), `TRIM` (right), `COMPBL` (inner), `COMPRESS` (remove any characters) | |
| Cut / split text | `SUBSTR` (by position), `SCAN` (by word), | `SCAN` default length of result is 200 |
| Find text | `FIND` (flexible), `INDEX` (simple) | 0 = not found |
| Replace text | `TRANWRD` (words), `TRANSLATE` (characters) | `TRANSLATE(x, to, from)` |
| Join text | `CATX` (with separator), `CATS`, `CATT`, `CAT` | Prefer `CATX`/`CATS` |
| Measure text | `LENGTH`, `LENGTHN` | |
| Add / ignore missing | `SUM`, `MEAN`, `MIN`, `MAX`, `N`, `NMISS` | Skip missing values |
| Round | `ROUND`, `CEIL`, `FLOOR`, `INT` | `ROUND(x, 0.01)` |
| Remainder / power / root | `MOD`, `**`, `SQRT`, `LOG`, `EXP`, `ABS` | |
| Random numbers | `RAND`, `CALL STREAMINIT` | Set a seed to repeat |
| Build a date | `MDY`, `INPUT(text, informat)` | |
| Take a date apart | `YEAR`, `MONTH`, `DAY`, `QTR`, `WEEK`, `WEEKDAY` | `WEEKDAY`: 1 = Sunday |
| Current date/time | `TODAY`, `DATE`, `TIME`, `DATETIME` | |
| Move a date | `INTNX(interval, date, n, alignment)` | |
| Count intervals | `INTCK(interval, from, to)` | Counts **boundaries** |
| Age / year difference | `YRDIF(from, to, 'AGE')` or `'ACT/ACT'` | |
| Date ↔ datetime | `DATEPART`, `TIMEPART`, `DHMS`, `HMS` | |
| Text ↔ number | `INPUT(text, informat)`, `PUT(value, format)` | |
| Test for missing | `MISSING(x)` | Works for numeric and character |
| First non-missing | `COALESCE` (numeric/SQL), `COALESCEC` (character) | |
| Look up a value | `PUT(key, $fmt.)` with a user-defined format | Fast lookup table |

#### 6.2 Missing-value behaviour at a glance

| Operation | Numeric missing in, result |
|---|---|
| `a + b`, `a * b`, `a / b` | **Missing** |
| `SUM(a,b)`, `MEAN(a,b)`, `MIN`, `MAX` | **Ignores** missing |
| `a < 5` (a missing) | **True** (missing is the smallest value) |
| `ROUND(.)`, `SQRT(.)`, `LOG(.)` | Missing (log note: *Missing values were generated*) |
| `PROC SQL` `SUM/AVG/MIN/MAX/COUNT(col)` | Ignore missing; `COUNT(*)` counts all rows |
| Sort order | Missing **first** when ascending |

#### 6.3 Interval names for `INTNX` / `INTCK`

`DAY`, `WEEK`, `MONTH`, `QTR`, `YEAR`, `WEEKDAY`, `SEMIYEAR`, plus time intervals for datetimes: `DTDAY`, `DTMONTH`, `HOUR`, `MINUTE`, `SECOND`. Prefix `dt` is for datetime values, for example `intnx('dtmonth', datetime, 1)`.

---

## 7. SAS Data Import / Export Reference

#### 7.1 Importing (getting data **into** SAS)

| Source | Recommended method | Licence | Where explained |
|---|---|---|---|
| Typed in the program | `DATA` + `INPUT` + `DATALINES` | ✅ Base | 1.4 |
| Fixed-width text | `INFILE` + column / formatted `INPUT` | ✅ Base | 1.8 |
| CSV (clean) | `PROC IMPORT DBMS=CSV` | ✅ Base | 1.13 |
| CSV / delimited (messy or repeated job) | `INFILE ... DSD DLM= TRUNCOVER` | ✅ Base | 3.2, 3.3 |
| Tab / pipe delimited | `PROC IMPORT DBMS=TAB/DLM` or `INFILE DLM=` | ✅ Base | 1.13, 3.2 |
| Excel `.xlsx` | `LIBNAME XLSX` or `PROC IMPORT DBMS=XLSX` | 🔑 PC Files (usually) | 3.4, 3.5 |
| Excel via CSV (no licence) | Save as CSV, then import | ✅ Base | 3.3 |
| Microsoft Access | `LIBNAME ACCESS` / ODBC | 🔑 | 3.7 |
| Oracle, SQL Server, others | `LIBNAME ORACLE/SQLSVR/ODBC`, or pass-through | 🔑 SAS/ACCESS | 3.7 |
| Hive / Hadoop | `LIBNAME HADOOP` | 🔑 SAS/ACCESS to Hadoop | 3.9 |
| Files in HDFS | `FILENAME HADOOP` + `INFILE` | ✅ Base + Hadoop client setup 🌐 | 3.9 |
| Remote SAS server | `PROC DOWNLOAD` | 🔑 SAS/CONNECT | 3.8 |
| Other SAS libraries | `LIBNAME` + `SET` / `PROC COPY` | ✅ Base | 1.16 |
| JSON | `LIBNAME ... JSON` engine | ✅ Base 9.4 (🌐 version) | |
| Unstructured text | `INPUT line $char200.;` + `SCAN`/`SUBSTR`/`PRX` | ✅ Base | 3.11 |

#### 7.2 Exporting (getting data **out of** SAS)

| Target | Method | Example |
|---|---|---|
| CSV | `PROC EXPORT DBMS=CSV` | `proc export data=employee outfile="/out/emp.csv" dbms=csv replace; run;` |
| Delimited text, custom layout | `DATA _NULL_; FILE ... DLM="\|"; PUT ...;` | 3.3 |
| Excel data | `PROC EXPORT DBMS=XLSX` 🔑 or `LIBNAME XLSX` 🔑 | `proc export data=employee outfile="/out/emp.xlsx" dbms=xlsx replace; sheet="Emp"; run;` |
| Excel report (formatted) | `ODS EXCEL` (Base 9.4+) | `ods excel file="/out/r.xlsx"; proc print ...; ods excel close;` |
| PDF / HTML / RTF report | `ODS PDF` / `ODS HTML` / `ODS RTF` | 2.9 |
| Database table | `LIBNAME` + `DATA db.t; SET work.t;` | 3.7 |
| Remote SAS server | `PROC UPLOAD` 🔑 | 3.8 |
| Another SAS library | `PROC COPY` / `DATA` + `SET` | 1.16 |

#### 7.3 Reading checklist (after every import)

1. `PROC CONTENTS` → are **types** right (IDs as text, amounts as numbers, dates as dates)?
2. `PROC PRINT (obs=10)` → does it look right?
3. Row count equals the source count?
4. `PROC MEANS ... NMISS` / `PROC FREQ ... / MISSING` → unexpected missing values?
5. Any `NOTE: Invalid data` or `Invalid numeric data` messages in the log?

---

## 8. Decision Guide

#### 8.1 Which tool should I use?

| Task | Best tool | Why |
|---|---|---|
| Add a calculated column | DATA step (or `PROC SQL`) | Either works; DATA step is simpler for many `IF`s |
| Filter rows | `WHERE` (DATA/PROC) or `PROC SQL WHERE` | `WHERE` is faster than subsetting `IF` |
| Sort | `PROC SORT` (or `ORDER BY`) | `PROC SORT` creates a sorted dataset others can `MERGE` |
| Remove duplicates | `PROC SORT NODUPKEY` / `NODUPRECS` | Keep first per key; control which row with the sort order |
| Stack tables | `SET` / `PROC APPEND` / `UNION ALL` | `PROC APPEND` is fastest for adding to a big table |
| Join on a key | `PROC SQL JOIN` | No sorting; flexible conditions; many tables |
| Join sorted, big files with sequential logic | DATA step `MERGE` | Efficient; supports `IN=`, `FIRST.` |
| Many-to-many join | `PROC SQL` | `MERGE` does **not** make all combinations |
| Group totals (just view) | `PROC MEANS` / `PROC TABULATE` | One line of code |
| Group totals as a dataset | `PROC SUMMARY` / `PROC SQL GROUP BY` | |
| Running total / previous row | DATA step (`RETAIN`, sum statement, `LAG`) | Row-to-row logic |
| First/last per group | DATA step `FIRST.`/`LAST.` | Needs sorted data |
| Rank | `PROC RANK` (or DATA step counter) | Ties are handled |
| Rows ↔ columns | `PROC TRANSPOSE` (or arrays) | |
| Repeat the same task for many values | **Macro** (`%DO`, `INTO`) | Write once, reuse |
| Same program, different parameters | **Macro** with parameters | |
| Run daily without clicking | Scheduler + batch SAS + macro | 8.19 |
| Read a messy text file | DATA step `INFILE`/`INPUT` | Full control |
| Read a tidy file once | `PROC IMPORT` | Fast |
| Check a result against a previous version | `PROC COMPARE` | |
| Fresh results that always follow the source | `PROC SQL` **view** | No stored data |

#### 8.2 Quick decision questions

1. **Do I need to remember something from the previous row?** → DATA step.
2. **Am I combining tables, or summarising with groups and conditions?** → `PROC SQL`.
3. **Do I just need a standard statistic or report?** → The matching `PROC` (`MEANS`, `FREQ`, `REPORT`…).
4. **Will I do the same thing again and again?** → Wrap it in a **macro**.
5. **Is the data very large?** → Filter early (`WHERE=`), keep only needed columns (`KEEP=`), use `PROC APPEND`, avoid unnecessary sorts.

#### 8.3 Habits that prevent most problems

- Use `OUT=` in `PROC SORT` (do not overwrite the original).
- Put `LENGTH` before the first use of a character variable.
- Test for missing **before** comparing numbers.
- Check the **log** after every run; filter with: `ERROR`, `WARNING`, `Invalid`, `uninitialized`, `converted`, `repeats of BY values`.
- Check row counts before and after merges/joins.
- Develop with small samples: `OBS=`, `INOBS=`, `OUTOBS=`.

---

## 9. Common SAS Errors and Troubleshooting

**How to read the log:** blue/black `NOTE` = information (still read them!), green `WARNING`, red `ERROR`. Find the **first** error; later errors are often just consequences. The error is usually at or **before** the underlined position.

| Message (shortened) | Likely cause | Fix |
|---|---|---|
| `ERROR 22-322: Syntax error, expecting one of the following...` | Missing semicolon, misspelt keyword, unbalanced bracket or quote | Check the statement **above** the underlined spot |
| `ERROR 76-322: Syntax error, statement will be ignored` | Follows an earlier error | Fix the first error |
| `ERROR: Variable X not found` | Typo, or the variable was dropped/renamed earlier | Check spelling, `KEEP`/`DROP`/`RENAME` |
| `ERROR: Variable X is not on file WORK.Y` | `WHERE` uses a variable created in the same step | Use a subsetting `IF` instead |
| `ERROR: File WORK.X.DATA does not exist` | Dataset not created yet, wrong name, wrong library | Run the earlier step; check names |
| `ERROR: Libref MYLIB is not assigned` | `LIBNAME` not run in this session | Run `LIBNAME` first |
| `NOTE: Variable X is uninitialized` | Typo created a new, empty variable | Fix the name |
| `NOTE: Invalid numeric data, 'abc'` | Text read where a number was expected (wrong informat/delimiter) | Read as character, or fix the layout |
| `NOTE: Character values have been converted to numeric` (or reverse) | Automatic type conversion | Convert explicitly with `INPUT()`/`PUT()` |
| `NOTE: Missing values were generated as a result of performing an operation on missing values` | `+ - * /` with a missing value | Use `SUM()` or handle missing |
| `ERROR: Variable X has been defined as both character and numeric` | Stacking/merging datasets with different types | Convert one type first (`INPUT`/`PUT`), rename if needed |
| `WARNING: Multiple lengths were specified for the variable X` | Different lengths in inputs: **risk of truncation** | Set `LENGTH` before `SET`/`MERGE` |
| `ERROR: BY variables are not properly sorted` | Data not sorted by the `BY` variables | `PROC SORT` first (or `NOTSORTED` if grouped) |
| `NOTE: MERGE statement has more than one data set with repeats of BY values` | Duplicate keys on **both** sides | Check keys; consider `PROC SQL`; de-duplicate |
| `NOTE: SAS went to a new line when INPUT statement reached past the end of a line` | Short lines/missing values with fixed fields | Add `TRUNCOVER` (or `MISSOVER`) |
| `ERROR: Physical file does not exist` | Wrong path or file name; case matters on Linux | Check path/permissions |
| `ERROR: Array subscript out of range` | Index beyond the array size | Use `DIM()` in the loop limit |
| `NOTE: Division by zero detected` | Divisor is 0 | Test the divisor first |
| `WARNING: Apparent symbolic reference X not resolved` | Macro variable missing, misspelt or out of scope | Define it; check `%GLOBAL`/`%LOCAL` |
| `WARNING: Apparent invocation of macro X not resolved` | Macro not defined (or misspelt) | Run the `%macro` code first; check `%include` |
| `ERROR: Ambiguous reference, column X is in more than one table` | Same column name in joined tables | Prefix with an alias: `a.x` |
| `ERROR: The following columns were not found in the contributing tables` | Wrong column name in `PROC SQL` | Check spelling; use `DESCRIBE TABLE` |
| `ERROR: Format X not found or couldn't be loaded` | User-defined format catalog not available | Point to it with `OPTIONS FMTSEARCH=`, or `NOFMTERR` |
| `ERROR: ... engine ... cannot be found` / product not licensed | Excel/database engine not licensed or not installed | Check `PROC SETINIT`; ask your administrator; use CSV |
| `ERROR: ... file is in use` / lock | Excel file open, or another job writing | Close the file; clear the `LIBNAME` (`libname xl clear;`) |
| `NOTE: The data set X has 0 observations` | Filter too strict, text case mismatch (`"it"` vs `"IT"`), wrong date literal | Check `WHERE`; use `UPCASE()` |
| SAS seems to **hang** / "running" forever | Missing `RUN;`/`QUIT;`, or an infinite `DO WHILE` loop | Add `RUN;`; break the session; fix the loop condition |
| Everything after a point turns into text/log messages like `quoted string ... more than 262 characters` | **Unbalanced quote** | Submit `'; run;` or `"; run;` to close it, or restart the SAS session |

**Symptoms without an error message**

| Symptom | Cause |
|---|---|
| Text cut off | Default length 8 in list input (use `:$12.`) or the first value set a short length |
| Dates show as 5-digit numbers | No date format applied |
| Dates read as missing or wrong | Wrong informat (day/month order) |
| Counts too high after a join | Duplicate keys; many-to-one became many-to-many |
| Totals differ between `PROC MEANS` and your own sums | Missing values handled differently (`+` vs `SUM`) |
| Rows disappeared after `PROC SORT NODUPKEY` | NODUPKEY keeps only the first row per key (check with `DUPOUT=`) |
| Original dataset changed unexpectedly | `PROC SORT` without `OUT=`, or `DATA x; set x;` |

---

## 10. High-Priority SAS Interview Questions with Concise Answers

#### Fundamentals (Session 1)

1. **What is SAS?** A software suite and language for data management, analysis and reporting; Base SAS, SAS/STAT, SAS/ACCESS, etc. are its components.
2. **DATA step vs PROC step?** DATA step creates/transforms data row by row; PROC step runs a prebuilt procedure to analyse, report or manage data.
3. **What are WORK and permanent libraries?** `WORK` is temporary (cleared at session end); a `LIBNAME` pointing to a folder gives permanent storage.
4. **How many data types does SAS have?** Two: numeric (also dates) and character.
5. **How are missing values represented and tested?** Numeric `.`, character blank; test with `MISSING(x)` or `x = .` / `x = " "`. A missing number is smaller than any number.
6. **Format vs informat?** Informat reads text into a stored value; format changes how a stored value is displayed.
7. **How does SAS store dates?** Days since 01JAN1960 (datetimes as seconds).

#### Data step (Sessions 2–3)

8. **What is the PDV?** A one-row memory area built at compile time; each iteration loads a row, runs statements, writes the row.
9. **KEEP/DROP/RENAME: statement vs option?** Statements apply to all output datasets of the step; options apply to one dataset and can also be used on input to limit what is read.
10. **WHERE vs IF?** `WHERE` filters before the row reaches the PDV (works in PROC steps, faster, cannot use new variables); subsetting `IF` filters after (DATA step only, can use new variables).
11. **NODUPKEY vs NODUPRECS?** `NODUPKEY` keeps the first row per `BY` key; `NODUPRECS` removes entire rows identical to the **previous** row (sort so duplicates are adjacent).
12. **DSD, MISSOVER, TRUNCOVER?** `DSD` = consecutive delimiters mean missing and quotes are handled; `MISSOVER` = short line → missing; `TRUNCOVER` = short line → keep the partial value.
13. **`@` vs `@@`?** `@` holds the line for the next `INPUT` in the same iteration; `@@` holds it across iterations (several observations per line).
14. **When use PROC IMPORT vs a DATA step?** `PROC IMPORT` for tidy one-off files; DATA step for control over types/lengths, messy layouts and repeat jobs.
15. **How to get an exact random sample?** `PROC SURVEYSELECT METHOD=SRS SAMPSIZE=n SEED=…` (SAS/STAT), or shuffle with `RAND` and take the first *n*.

#### Combining data (Session 4)

16. **SET vs MERGE?** `SET` stacks datasets (rows); `MERGE` + `BY` combines columns by key (needs sorted data).
17. **Is MERGE the same as a SQL JOIN?** No. With repeated keys on both sides `MERGE` pairs rows sequentially, while SQL returns every combination.
18. **PROC APPEND vs SET?** `PROC APPEND` adds to an existing base dataset without reading it (fast); `SET` rewrites a new dataset.
19. **How to find customers with no orders?** Anti-join: `LEFT JOIN ... WHERE o.key IS NULL`, `NOT EXISTS`, or `MERGE` with `IF a AND NOT b`.
20. **Fact vs dimension; star vs snowflake?** Fact = measurable events; dimensions = descriptive context. Star has flat dimensions; snowflake splits dimensions into sub-tables.
21. **Table vs view?** A table stores data; a view stores the query and always shows current data.
22. **Does PROC SQL support stored procedures?** No. Database stored procedures can be called through explicit pass-through; SAS macros are the SAS-side reuse tool.
23. **Truncate a table in PROC SQL?** `TRUNCATE` is not supported for SAS datasets; use `DELETE FROM table;` (keeps structure). `DROP TABLE` removes it entirely.

#### Processing and functions (Sessions 5–6)

24. **RETAIN vs the sum statement?** `RETAIN` keeps a value across rows (start value must be given); the sum statement `x + y;` auto-retains, starts at 0 and ignores missing.
25. **FIRST. and LAST.?** Temporary flags for the first/last row of each `BY` group; data must be sorted by the `BY` variables.
26. **FIRST./LAST. vs PROC RANK?** FIRST./LAST. picks one boundary row per group; RANK numbers rows by value, with tie handling.
27. **How do you create row numbers?** `n + 1;` (sum statement); within groups reset at `FIRST.`. `monotonic()` is undocumented; `ROW_NUMBER() OVER` is not in Base `PROC SQL`.
28. **PROC TRANSPOSE options?** `BY` (group), `ID` (new column names), `VAR` (values to rotate), `PREFIX=`, `NAME=`.
29. **SUM(a,b) vs a+b?** `SUM` ignores missing; `+` returns missing if any operand is missing.
30. **INTCK vs INTNX?** `INTCK` counts interval boundaries between dates; `INTNX` moves a date by *n* intervals.
31. **PROC MEANS vs PROC SUMMARY; CLASS vs BY?** Same statistics; `MEANS` prints by default, `SUMMARY` does not. `CLASS` needs no sorting and gives one table; `BY` needs sorted data and gives sections.
32. **PROC FREQ vs PROC MEANS?** `FREQ` counts categories; `MEANS` summarises numeric values.

#### PROC SQL and macros (Sessions 7–8)

33. **WHERE vs HAVING?** `WHERE` filters rows before grouping; `HAVING` filters groups after, and can use summary functions.
34. **Logical order of processing in SQL?** FROM/JOIN → WHERE → GROUP BY → HAVING → SELECT → ORDER BY.
35. **What does CALCULATED do?** Lets you reuse a column alias from the same `SELECT` in `SELECT`, `WHERE`, `HAVING` and `ORDER BY` (a SAS extension).
36. **`&x` vs `%x`?** `&x` resolves a macro variable; `%x` calls a macro or macro statement.
37. **What is `&&dept&i`?** Two-pass resolution: first `&dept` + counter → `&dept2`, then its value.
38. **CALL SYMPUT vs CALL SYMPUTX?** `SYMPUTX` trims blanks, avoids conversion notes and can set scope; prefer it.
39. **Why can't `%IF` test a data column?** The macro processor runs before the data step executes, so columns don't exist yet.
40. **How do you schedule a macro?** A macro can't schedule itself; start SAS in batch mode from cron/Task Scheduler/Control-M/Viya jobs and call the macro in the program.

#### Scenario questions (short code)

**A. Second highest salary**

```sas
proc sql;
    select max(salary) as second_highest
    from employee
    where salary < (select max(salary) from employee);      /* 58000 */
quit;
```

**B. Find duplicate keys**

```sas
proc sql;
    select customer_id, count(*) as n
    from orders
    group by customer_id
    having count(*) > 1;                                    /* customers 1 and 3 */
quit;
```

**C. Latest order per customer**

```sas
proc sort data=orders out=ord_s;  by customer_id order_date;  run;
data latest;  set ord_s;  by customer_id;  if last.customer_id;  run;
```

**D. Convert a character date `"15/01/2025"` to a SAS date**

```sas
sas_date = input(txt_date, ddmmyy10.);
format sas_date date9.;                    /* 15JAN2025 */
```

**E. Count missing values in all numeric variables**

```sas
proc means data=employee n nmiss;  run;
```

**F. Cumulative amount per customer**

```sas
proc sort data=orders out=ord_s;  by customer_id order_date;  run;
data ord_cum;
    set ord_s;
    by customer_id;
    if first.customer_id then cum_amount = 0;
    cum_amount + amount;
run;
```

---

## 11. Final Revision Checklist

#### Session 1: fundamentals and import
- [ ] I can explain Base SAS, SAS/STAT, SAS/ACCESS, SAS Studio, EG and Viya
- [ ] I know library and variable naming rules (8 / 32 characters)
- [ ] I can read inline, fixed-width, delimited and Excel data
- [ ] I can describe data with `PROC CONTENTS` and copy with `PROC COPY`
- [ ] I know missing values, types, lengths and `LIBNAME`/`FILENAME`

#### Session 2: data step and formats
- [ ] `KEEP`/`DROP`/`RENAME` as statements and options
- [ ] `WHERE` operators; `WHERE` vs subsetting `IF`
- [ ] `PROC SORT` with `BY`, `DESCENDING`, `NODUPKEY`, `NODUPRECS`
- [ ] `IF-THEN-DO`, multiple output datasets
- [ ] Formats vs informats; `PROC FORMAT`; permanent formats (`FMTSEARCH`)
- [ ] `PROC PRINT` and ODS basics

#### Session 3: input, output and PDV
- [ ] `INFILE` options: `DSD`, `DLM=`, `MISSOVER`, `TRUNCOVER`, `FIRSTOBS=`, `OBS=`
- [ ] `@` and `@@`; parsing unstructured text
- [ ] Excel sheets, Access/SQL Server/Oracle, HDFS, `DOWNLOAD`/`UPLOAD` (and their licences)
- [ ] The PDV, step by step
- [ ] Random samples (`SEED=`, exact `SAMPSIZE=`); `POINT=`, `FIRSTOBS=/OBS=`

#### Session 4: joins, modeling, PROC SQL
- [ ] `SET` stacking, `PROC APPEND` behaviour
- [ ] `MERGE` with `BY` and `IN=`; sorting requirements
- [ ] Inner/left/right/full/self/cross joins; anti-joins; subqueries
- [ ] `MERGE` ≠ `JOIN` with duplicate keys
- [ ] PK/FK; 1:1, 1:M, M:M; fact/dimension; star/snowflake
- [ ] `CREATE`, `INSERT`, `UPDATE`, `DELETE`, `DROP`, `ALTER`; no `TRUNCATE` in `PROC SQL` for SAS data
- [ ] Views vs tables; stored procedures are database features

#### Session 5: transpose, retain, ranking, loops, arrays
- [ ] `PROC TRANSPOSE` (`BY`, `ID`, `VAR`, `PREFIX`, `NAME`)
- [ ] `RETAIN` initialisation; sum statement vs `+`
- [ ] `PROC COMPARE`, `UPDATE`
- [ ] `FIRST.`/`LAST.` (sorted data)
- [ ] `PROC RANK` and tie handling; row-number methods
- [ ] Alternate rows (`MOD`), `DO` loops, arrays (`DIM`, `_TEMPORARY_`)

#### Session 6: functions and summaries
- [ ] Character, numeric, date functions (`SCAN`, `SUBSTR`, `CATX`, `INTNX`, `INTCK`, `YRDIF`)
- [ ] Dates as day counts; datetimes as seconds
- [ ] `PROC MEANS`, `SUMMARY`, `UNIVARIATE`, `FREQ`, `REPORT`, `TABULATE`, `SGPLOT`
- [ ] When to choose which procedure

#### Session 7: PROC SQL practice
- [ ] Aliases, expressions, `CASE`, `GROUP BY`, `HAVING`
- [ ] Logical processing order (not physical)
- [ ] `UPDATE`/`DELETE` on copies; set operators; views
- [ ] `CALCULATED`, `COALESCE`, SAS vs DBMS functions
- [ ] Row numbers and the window-function limits

#### Session 8: macros
- [ ] Macro processor vs DATA step execution
- [ ] `%LET`, `&var`, `%GLOBAL`/`%LOCAL`
- [ ] Positional vs keyword parameters
- [ ] `INTO`, `CALL SYMPUTX`, `&&var&i`, `%DO`, `%IF`
- [ ] `MPRINT`, `MLOGIC`, `SYMBOLGEN`, `%PUT _user_`
- [ ] `%INCLUDE`, autocall, stored macros
- [ ] Scheduling needs an external scheduler

#### Before every submission
- [ ] Read the **log** (errors, warnings, and notes about missing values, conversions, merge repeats)
- [ ] Check row counts before and after joins and merges
- [ ] Check types and lengths of key variables
- [ ] Use `OUT=` so originals stay intact

---

*End of guide.*
