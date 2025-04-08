# Chapter6: Normalization of Database Tables
- Good database design must be matched to good table structures. 
- Learn to evaluate and design good table structures to **control data redundancies** thereby avoiding data anomalies.
- The process that yields such desirable results is known as **normalization**.

# Self-Taught Resource
- https://www.databasestar.com/mysql-database/
- https://www.databasestar.com/database-design/
- https://www.databasestar.com/programmer-jokes/
- https://www.databasestar.com/vip/
- https://youtube.com/@decomplexify?si=I5sEMNUZOJcSpiCX
- Personal reference: [https://www.youtube.com/watch?v=qxA5Dma6wEg&t=2144s&ab_channel=Eric](url)


# Database Tables and Normalization
- <span class="blue-text">**Normalization**</span> is a process for adjusting table structures to <span class="brown-text">**minimize data redundancies**</span> 
  - Reduce data anomalies(不規則)
  - Assigns attributes to tables based on functional dependency
- Normalization goes through a series of stages called normal forms

<img width="543" alt="image" src="https://github.com/user-attachments/assets/de05fdc3-6c0b-4f4f-aec0-6118d634837c" />

# Why Normalize a Database
- Prevent the same data from being stored in more than one place (insert anomaly)
- Prevent updates being made to some data but not others (update anomaly)
- Prevent data not being deleted when it is supposed to be, or from data being lost when it is not supposed to be (delete anomaly)
- Ensure the data is accurate
- Reduce the storage space that a database takes up
- Ensure the queries on a database run as fast as possible

# Data Redundancies Issues - A Sample Table

Student ID|Student Name|Fees Paid|Course Name|Class 1|Class 2|Class 3
----------|------------|---------|-----------|-------|-------|-------
1|John Smith|200|Economics|Economics 1|Biology 1
2|Maria Griffin|500|Computer Science|Biology 1|Business Intro|Programming 2
3|Susan Johnson|400|Medicine|Biology 2		
4|Matt Long|850|Dentistry

- Attributes: student names, paid fees, registered classes
- It is not a normalized table (has multiple columns for the same type of data (class)), and there are a few issues with this

# Data Redundancies Issues - Insert Anomaly
- If we want to add a new student but did not know their course name

Student ID|Student Name|Fees Paid|Course Name|Class 1|Class 2|Class 3
----------|------------|---------|-----------|-------|-------|-------
1|John Smith|200|Economics|Economics 1|Biology 1
2|Maria Griffin|500|Computer Science|Biology 1|Business Intro|Programming 2
3|Susan Johnson|400|Medicine|Biology 2		
4|Matt Long|850|Dentistry
5|Jared Oldham|0|?

- We would be adding incomplete data to our table, which can cause issues when trying to analyze this data.

# Data Redundancies Issues - Update Anomaly
- If the class Biology 1 was changed to “Intro to Biology”. We would have to query all of the columns that could have this Class field and rename each one that was found.

Student ID|Student Name|Fees Paid|Course Name|Class 1|Class 2|Class 3
----------|------------|---------|-----------|-------|-------|-------
1|John Smith|200|Economics|Economics 1|Biology 1
2|Maria Griffin|500|Computer Science|Biology 1|Business Intro|Programming 2
3|Susan Johnson|400|Medicine|Biology 2		
4|Matt Long|850|Dentistry

- There’s a risk that we miss out on a value, which would cause issues.
- Ideally, we would only update the value once, in one location.

# Data Redundancies Issues - Delete Anomaly
- If Susan Johnson quits and her record needs to be deleted from the system. We could delete her row

Student ID|Student Name|Fees Paid|Course Name|Class 1|Class 2|Class 3
----------|------------|---------|-----------|-------|-------|-------
1|John Smith|200|Economics|Economics 1|Biology 1
2|Maria Griffin|500|Computer Science|Biology 1|Business Intro|Programming 2
**3**|**Susan Johnson**|**400**|**Medicine**|**Biology 2**		
4|Matt Long|850|Dentistry

- But, if we delete this row, we lose the record of the Biology 2 class, because it’s not stored anywhere else. The same can be said for the Medicine course.
- We should be able to delete one type of data or one record without having impacts on other records we don’t want to delete.

# A Sample Report Layout
![螢幕擷取畫面 2025-03-31 200234](https://github.com/user-attachments/assets/d19f06c0-d415-462a-bfe4-47bd56d75fac)

# Poor Table Structure

<img width="750" alt="image" src="https://github.com/user-attachments/assets/98dfb0e2-42e1-4749-94be-26c234bfcbbf" />

- Data inconsistency
- Difficult to update
- Data redundant

# Enough Normalization
- From a structural point of view, higher normal forms are better than lower normal forms
- For most purposes in business database design, 3NF is as high as you need to go in the normalization process
- Denormalization produces a lower normal form to increase performance but greater data redundancy

# The Need for Normalization
- Database designers commonly use normalization in the following two situations:
  - When designing a new database structure
  - To analyze the relationship among the attributes within each entity and determine if the structure can be improved through normalization
- The main goal of normalization is to eliminate data anomalies by eliminating unnecessary <span class="blue-text">data redundancies</span>
- Normalization uses the concept of <span class="blue-text">functional dependencies, FD</span> to identify which attribute determines other attributes

# The Objectives of Normalization
- Each table represents a single subject
- Each row/column intersection contains only one value and not a group of values
- No data item will be unnecessarily stored in more than one table.
- Data is updated in only one place
- All non-prime attributes in a table are dependent on the primary key
- Each table has no insertion, update, or deletion anomalies
- Ensure that all tables are in at least in 3NF in business environment
- Work one table at a time, identifying FD of a table
- 每個表格代表一個單一的主題
- 每個行與列的交叉點僅包含一個值，而不是一組值  
- 沒有任何數據項會不必要地存儲在多個表格中  
- 數據只在一個地方進行更新  
- 表格中的所有非主屬性都依賴於主鍵  
- 每個表格都沒有插入、更新或刪除異常  
- 確保在商業環境中，所有表格至少符合第三範式(3NF)  
- 一次處理一個表格，識別表格中的函數依賴(FD)關係  

# Normal Forms
<img width="518" alt="image" src="https://github.com/user-attachments/assets/1970cd56-a2dd-4c97-882f-dfadcc1c56aa" />

# Normalization Base: Functional Dependency (FD)
- Normalization starts by identifying **functional dependencies** of a given table
- <span class="blue-text">FD X&rarr;Y</span>: the values of Y are determined by the values of X. (X, Y is a set of attributes)
- <span class="blue-text">X&rarr;Y is full FD </span>, if no attribute can be removed from X and still keep the dependency.
- Example: 
  - PROJ_NUM → PROJ_ NAME (read as PROJ_ NUM functionally determines PROJ_NAME)
  - Attribute PROJ_NUM is known as the determinant attribute
  - Attribute PROJ_NAME is known as the dependent attribute.

# FD Type: Partial Functional Dependency
When there is a FD in which the determinant is only part of the PK
- <span class="blue-text">X&rarr;Y is a partial FD </span> if X is a subset of PK.

Example
- Give a table having PK (A, B), there is a FD (B &rarr; C), we say it is a partial FD because B is a subset of PK 

**FD `X → Y`** 表示：  
- **`X` 的值決定了 `Y` 的值**（`Y` 依賴於 `X`）。  
- 其中，`X` 和 `Y` 可以是單個屬性(attribute)或一組屬性。  

#### **範例：**  
`PROJ_NUM → PROJ_NAME`  
- 讀作：**「PROJ_NUM 函數決定 PROJ_NAME」**  
- 表示：**只要知道專案編號(PROJ_NUM)，就能唯一確定專案名稱(PROJ_NAME)**。  

- **完全函數依賴(Full FD)**：  
  - 在 `X → Y` 中，`X` 的**任何一個屬性都不能被移除**，否則依賴關係就不成立。  
  - 即 `Y` 完全依賴於整個 `X`，而不是 `X` 的子集。  

#### **範例：**  
假設有一個表格 `PROJECT(PROJ_NUM, PROJ_NAME, DEPT_NUM)`，其中：  
- `PROJ_NUM → PROJ_NAME`（專案編號決定專案名稱）  
- `PROJ_NUM → DEPT_NUM`（專案編號決定部門編號）  

如果 `PROJ_NAME` 和 `DEPT_NUM` 都**只依賴於 `PROJ_NUM`**（而非 `PROJ_NUM` 和其他屬性的組合），則這些 FD 都是**完全函數依賴**。  
但如果存在 `(PROJ_NUM, EMP_ID) → HOURS_WORKED`（專案編號+員工ID 決定工時），而 `HOURS_WORKED` 不能僅由 `PROJ_NUM` 或 `EMP_ID` 單獨決定，則這是一個**部分函數依賴**（因為需要兩者才能決定工時）。  


# FD Type: Transitive Functional Dependency
When a attribute is dependent on another attribute which is not part of PK
- Transitive FD is more difficult to identify among a set of data
- They occur only when a FD exists among non-prime attributes
Example
- Given primary key: X, there are two FDs X → Z and X → Y
- After investigating, we find that there is a FD Y → Z, which can support X determine Z because (X → Y) + (Y → Z) can make (X → Z) that is, x can determine the value of Z via Y. 
- Y → Z signals that there is a <span class="blue-text">transitive FD</span> because Y is not a PK.

當一個**非主屬性(non-prime attribute)** 依賴於另一個**非主屬性**（而非直接依賴於主鍵）時，就會產生**遞移函數依賴(Transitive FD)**。這種情況會導致資料冗餘，並可能引發更新異常(update anomalies)，因此需要透過正規化（如 3NF）來消除。  

## **1. 什麼是遞移函數依賴？**  
假設有一個表格，其主鍵是 `X`，並且存在以下函數依賴(FD)：  
1. `X → Y`（主鍵決定 `Y`）  
2. `X → Z`（主鍵決定 `Z`）  
3. 進一步檢查後發現，**`Y → Z`**（`Y` 也決定 `Z`）  

由於 `Y` 不是主鍵，而 `Z` 卻依賴於 `Y`，這就形成了**遞移依賴**，因為：  
- `X` 決定 `Y`  
- `Y` 決定 `Z`  
- 因此，`X` **間接**決定 `Z`（`X → Y → Z`）  

這種情況意味著 `Z` 並非**完全直接依賴於主鍵 `X`**，而是透過 `Y` 間接依賴，這違反了 **3NF (第三正規化)** 的規則。  


## **2. 遞移依賴的範例**  
假設有一個 **`EMPLOYEE`** 表格，結構如下：  

| **EMP_ID (PK)** | **DEPT_ID** | **DEPT_NAME** | **DEPT_LOCATION** |
|---------------|-----------|-------------|-----------------|
| E001          | D01       | Marketing   | New York        |
| E002          | D02       | Sales       | Chicago         |
| E003          | D01       | Marketing   | New York        |

### **函數依賴分析：**
1. **主鍵是 `EMP_ID`**（每個員工 ID 唯一識別一筆記錄）。  
2. 基本 FD：  
   - `EMP_ID → DEPT_ID`（員工 ID 決定部門 ID）  
   - `EMP_ID → DEPT_NAME`（員工 ID 決定部門名稱）  
   - `EMP_ID → DEPT_LOCATION`（員工 ID 決定部門地點）  
3. 但進一步觀察發現：  
   - `DEPT_ID → DEPT_NAME`（部門 ID 決定部門名稱）  
   - `DEPT_ID → DEPT_LOCATION`（部門 ID 決定部門地點）  

### **問題：**
- `DEPT_NAME` 和 `DEPT_LOCATION` 實際上**依賴於 `DEPT_ID`**，而不是直接依賴於主鍵 `EMP_ID`。  
- 這導致：  
  - **冗餘**（同一個部門的名稱和地點重複存儲多次）。  
  - **更新異常**（如果 Marketing 部門的地點變更，必須修改多筆記錄）。  

### **這是一個遞移依賴，因為：**
```
EMP_ID → DEPT_ID → (DEPT_NAME, DEPT_LOCATION)
```
`DEPT_NAME` 和 `DEPT_LOCATION` **間接依賴**於 `EMP_ID`，而不是直接依賴。  


# Why Do We Do Database Normalization?
![bg right:70% w:100%](https://cdn.hackr.io/uploads/posts/attachments/1666888816mdnYlrMoEE.png)

# Conversion to First Normal Form (1NF)
A table in 1NF means
- All key attributes are well defined 
- There are no repeating groups
- All attributes are dependent on the primary key

Converting to 1NF starts with three steps
1. Eliminate the repeating groups 
2. Identify the primary key 
3. Identify all dependencies

# Conversion to First Normal Form (1NF) - Supplement
- Row order do not convey any information
- There is no mixed data types within a column

# 1NF Step1 - Eliminate Repeating Groups
Repeating group: a group of entries existing for a single key value

<img width="402" alt="image" src="https://github.com/user-attachments/assets/c0f1cfcf-b88a-48b0-999d-8e13c36b25f0" />

# 1NF Step2 - Identify PK 
PK: an identifier composed of one or more attributes that uniquely identifies a row

# 1NF Step3 - Identify all Dependencies
According to PK (PROJ_NUM, EMP_NUM), we can find a dependency exist (PROJ_NUM, EMP_NUM) → (PROJ_NAME, EMP_NAME, JOB_CLASS, CHG_HOUR, HOURS) and derive it into two partial FD and one transitive FD
- Partial FD: PROJ_NUM → PROJ_NAME (because PROJ_NUM is a part of PK)
- Partial FD: EMP_NUM → EMP_NAME, JOB_CLASS, CHG_HOUR, <span class="brown-text">(not HOURS)</span> (because EMP_NUM is a part of PK)
- Transitive FD: JOB_CLASS → CHG_HOUR (because JOB_CLASS is not part of PK )
 

以下是一個未正規化的表格 `PROJECT_ASSIGNMENT`，包含重複群組(Repeating Groups)，我們將逐步進行 **1NF 正規化**，並分析其中的函數依賴關係。  

## **原始表格（未正規化）**  
| **PROJ_NUM** | **PROJ_NAME** | **EMP_NUM** | **EMP_NAME** | **JOB_CLASS** | **CHG_HOUR** | **HOURS** |
|-------------|-------------|-----------|------------|-------------|------------|--------|
| P001        | Apollo      | E101      | Smith      | Engineer    | 50         | 10     |
|             |             | E102      | Lee        | Analyst     | 45         | 15     |
| P002        | Gemini      | E103      | Wong       | DBA         | 60         | 20     |

### **問題分析：**
1. **重複群組(Repeating Groups)**  
   - 同一個專案（如 P001）下有多個員工（E101, E102），但 `PROJ_NAME` 重複儲存。  
   - 這違反 **1NF**，因為每個行列交叉點應只存單一值，且不應有重複的數據組。  


## **Step 1: 消除重複群組 (Eliminate Repeating Groups)**  
將重複的數據展開，使每一行代表一個獨立的記錄。  

### **修正後表格（符合 1NF）**  
| **PROJ_NUM** | **PROJ_NAME** | **EMP_NUM** | **EMP_NAME** | **JOB_CLASS** | **CHG_HOUR** | **HOURS** |
|-------------|-------------|-----------|------------|-------------|------------|--------|
| P001        | Apollo      | E101      | Smith      | Engineer    | 50         | 10     |
| P001        | Apollo      | E102      | Lee        | Analyst     | 45         | 15     |
| P002        | Gemini      | E103      | Wong       | DBA         | 60         | 20     |

**改進：**  
- 每筆記錄現在是獨立的，沒有重複群組。  
- 但仍有冗餘（如 `PROJ_NAME` 重複儲存）。  


## **Step 2: 識別主鍵 (Identify Primary Key, PK)**  
主鍵應能唯一識別每一筆記錄。  
- 單一屬性（如 `EMP_NUM`）無法唯一識別，因為同一員工可能參與多個專案。  
- 因此，主鍵應是 **複合主鍵(Composite PK)**：  
  - **`(PROJ_NUM, EMP_NUM)`**（專案編號 + 員工編號）  


## **Step 3: 識別所有函數依賴 (Identify All Dependencies)**  
根據主鍵 `(PROJ_NUM, EMP_NUM)`，分析其他屬性的依賴關係：  

### **完整依賴（Full FD）**  
- `(PROJ_NUM, EMP_NUM) → HOURS`  
  - 工時(`HOURS`)由專案和員工共同決定（完全依賴於主鍵）。  

### **部分依賴（Partial FD）**  
- `PROJ_NUM → PROJ_NAME`  
  - 專案名稱(`PROJ_NAME`)僅依賴於 `PROJ_NUM`（主鍵的一部分），屬於部分依賴。  
- `EMP_NUM → (EMP_NAME, JOB_CLASS, CHG_HOUR)`  
  - 員工姓名、職位類別、時薪僅依賴於 `EMP_NUM`（主鍵的一部分），屬於部分依賴。  

### **遞移依賴（Transitive FD）**  
- `JOB_CLASS → CHG_HOUR`  
  - 時薪(`CHG_HOUR`)依賴於職位類別(`JOB_CLASS`)，而 `JOB_CLASS` 不是主鍵，屬於遞移依賴。  

# Dependency Diagram
Dependency diagram shows all dependencies found within given table structure
<img width="524" alt="image" src="https://github.com/user-attachments/assets/45c18fc4-318f-447b-ae4b-2f496b11f273" />

# After 1NF
- All relational tables satisfy 1NF requirements
  - All key attributes are defined
  - There are no repeating groups in the table
  - All attributes are dependent on the primary key
- Some tables may contain partial and transitive FDs

# Conversion to Second Normal Form (2NF)
A table in the second normal form means
- it is in 1NF
- it does not include partial FD

Conversion to 2NF occurs only when the 1NF has a composite primary key
- If the 1NF has a single-attribute primary key, then the table is automatically in 2NF

Converting to 2NF starts with two steps
1. Make new tables to eliminate partial FD
2. Reassign corresponding dependent attributes

# 2NF Step1 - Make New Tables to Eliminate Partial FD
- Separate composite PK (PROJ_NUM + EMP_NUM) into different PKs
  - PK1: PROJ_NUM
  - PK2: EMP_NUM
  - PK3: PROJ_NUM + EMP_NUM
- Create tables based on new PK
  - Table1: PROJECT, PK is PROJ_NUM
  - Table2: EMPLOYEE, PK is EMP_NUM
  - Table3: ASSIGNMENT, PK is PROJ_NUM + EMP_NUM

# 2NF Step2 - Reassign Corresponding Dependent Attributes
- Table PROJECT(**PROJ_NUM**, PROJ_NAME)
- Table EMPLOYEE(**EMP_NUM**, EMP_NAME, JOB_CLASS, CHG_HOUR)
- Table ASSIGNMENT(**PROJ_NUM**, **EMP_NUM**, <span class="brown-text">ASSIGN_HOUR</span>)
(any attributes that are not dependent in partial FD will remain in the original table)

# Dependency Diagram
<img width="518" alt="image" src="https://github.com/user-attachments/assets/cf8def2f-7d88-4d2e-82b7-1888823818e1" />

# After 2NF
- All relational tables satisfy 2NF requirements
  - it is in 1NF
  - it does not include partial FD
  - If the 1NF has a single-attribute primary key, then the table is automatically in 2NF
- Some tables may contain transitive FD

在 **1NF** 的基礎上，我們已經：  
1. 消除重複群組（確保每個行列交叉點只存單一值）。  
2. 定義主鍵 `(PROJ_NUM, EMP_NUM)`。  
3. 識別出部分依賴（Partial FD）和遞移依賴（Transitive FD）。  

接下來，我們要進行 **2NF 正規化**，目標是：  
**消除非主屬性對主鍵的「部分依賴」**，即確保所有非主屬性必須**完全依賴於整個主鍵**（而非僅依賴主鍵的一部分）。  

## **Step 1: 檢查部分依賴 (Partial Dependencies)**  
在當前表格中，存在以下部分依賴：  
1. `PROJ_NUM → PROJ_NAME`  
   - `PROJ_NAME` 僅依賴於主鍵的一部分（`PROJ_NUM`）。  
2. `EMP_NUM → (EMP_NAME, JOB_CLASS, CHG_HOUR)`  
   - `EMP_NAME`, `JOB_CLASS`, `CHG_HOUR` 僅依賴於主鍵的一部分（`EMP_NUM`）。  

**這些部分依賴違反 2NF**  

## **Step 2: 分解表格 (Decompose Tables)**  
為解決部分依賴，我們將原始表格拆分為多個表格，確保：  
- 每個非主屬性**完全依賴於整個主鍵**。  
- 部分依賴的屬性被移到獨立的表格中。  

### **原始表格（1NF）**  
`PROJECT_ASSIGNMENT`  
| **PROJ_NUM** (PK) | **EMP_NUM** (PK) | **PROJ_NAME** | **EMP_NAME** | **JOB_CLASS** | **CHG_HOUR** | **HOURS** |
|------------------|----------------|--------------|-------------|--------------|-------------|---------|
| P001             | E101           | Apollo       | Smith       | Engineer     | 50          | 10      |
| P001             | E102           | Apollo       | Lee         | Analyst      | 45          | 15      |
| P002             | E103           | Gemini       | Wong        | DBA          | 60          | 20      |

### **拆分步驟：**
1. **移除 `PROJ_NAME`（依賴於 `PROJ_NUM`）→ 新建 `PROJECT` 表格**。  
2. **移除 `EMP_NAME`, `JOB_CLASS`, `CHG_HOUR`（依賴於 `EMP_NUM`）→ 新建 `EMPLOYEE` 表格**。  
3. **保留 `HOURS`（完全依賴於複合主鍵 `(PROJ_NUM, EMP_NUM)`）→ 保留在 `ASSIGNMENT` 表格**。  


### **修正後的 2NF 表格結構**  
#### **Table 1: `PROJECT`**  
| **PROJ_NUM** (PK) | **PROJ_NAME** |
|------------------|--------------|
| P001             | Apollo       |
| P002             | Gemini       |

- **主鍵**：`PROJ_NUM`  
- **函數依賴**：`PROJ_NUM → PROJ_NAME`（完全依賴，符合 2NF）。  

#### **Table 2: `EMPLOYEE`**  
| **EMP_NUM** (PK) | **EMP_NAME** | **JOB_CLASS** | **CHG_HOUR** |
|----------------|-------------|--------------|-------------|
| E101           | Smith       | Engineer     | 50          |
| E102           | Lee         | Analyst      | 45          |
| E103           | Wong        | DBA          | 60          |

- **主鍵**：`EMP_NUM`  
- **函數依賴**：  
  - `EMP_NUM → (EMP_NAME, JOB_CLASS, CHG_HOUR)`（完全依賴，符合 2NF）。  
  - 但仍存在遞移依賴 `JOB_CLASS → CHG_HOUR`（需在 3NF 解決）。  

#### **Table 3: `ASSIGNMENT`**  
| **PROJ_NUM** (FK) | **EMP_NUM** (FK) | **HOURS** |
|------------------|----------------|---------|
| P001             | E101           | 10      |
| P001             | E102           | 15      |
| P002             | E103           | 20      |

- **主鍵**：`(PROJ_NUM, EMP_NUM)`  
- **外鍵**：  
  - `PROJ_NUM` 參照 `PROJECT(PROJ_NUM)`  
  - `EMP_NUM` 參照 `EMPLOYEE(EMP_NUM)`  
- **函數依賴**：  
  - `(PROJ_NUM, EMP_NUM) → HOURS`（完全依賴，符合 2NF）。  

# Conversion to Third Normal Form (3NF)
A table in the third normal form means
- it is in 2NF
- it does not include transitive FD

Converting to 3NF starts with two steps
1. Make new tables to eliminate transitive FD 
2. Reassign corresponding dependent attributes

# 3NF Step1 - Make New Tables to Eliminate Transitive FD
A transitive FD: JOB_CLASS → CHG_HOUR 
- Make determinant (JOB_CLASS) as a PK of a new table
- Create tables based on new PK
  - Table JOB(**JOB_CLASS**, CHG_HOUR)

# 3NF Step2 - Reassign Corresponding Dependent Attributes
- Table EMPLOYEE(<u>**EMP_NUM**</u>, EMP_NAME, JOB_CLASS)
- Table JOB(<u>**JOB_CLASS**</u>, CHG_HOUR)
- Table PROJECT(<u>**PROJ_NUM**</u>, PROJ_NAME)
- Table ASSIGNMENT(<u>**PROJ_NUM**, **EMP_NUM**</u>, ASSIGN_HOUR)

# Dependency Diagram
<img width="524" alt="image" src="https://github.com/user-attachments/assets/5a9f688a-e475-49db-96c3-4e874a0eeba0" />

# After 3NF
- it is in 2NF
- it does not include transitive FD

在 **2NF** 的基礎上，我們已經：
1. 消除了非主屬性對主鍵的部分依賴
2. 將數據拆分為三個表格：PROJECT、EMPLOYEE 和 ASSIGNMENT

現在我們需要進行 **3NF 正規化**，目標是：
**消除非主屬性之間的遞移依賴**，即確保所有非主屬性都必須直接依賴於主鍵，而不是通過其他非主屬性間接依賴。


## **Step 1: 檢查遞移依賴 (Transitive Dependencies)**
在當前的 `EMPLOYEE` 表格中，存在以下依賴關係：
1. `EMP_NUM → (EMP_NAME, JOB_CLASS, CHG_HOUR)`（主鍵直接決定）
2. `JOB_CLASS → CHG_HOUR`（非主屬性之間的依賴）

**這是一個典型的遞移依賴**，因為：
- `CHG_HOUR` 實際上是由 `JOB_CLASS` 決定
- 而 `JOB_CLASS` 又由 `EMP_NUM` 決定
- 形成 `EMP_NUM → JOB_CLASS → CHG_HOUR` 的間接依賴鏈

這違反了 3NF 的原則


## **Step 2: 分解表格 (Decompose Tables)**
為解決遞移依賴，我們需要：
1. 將 `JOB_CLASS` 和 `CHG_HOUR` 拆分到新表格
2. 在 `EMPLOYEE` 表格中只保留直接依賴於主鍵的屬性

### **原始 2NF 表格結構**
#### **Table: EMPLOYEE (2NF)**
| **EMP_NUM** (PK) | **EMP_NAME** | **JOB_CLASS** | **CHG_HOUR** |
|-----------------|-------------|--------------|-------------|
| E101            | Smith       | Engineer     | 50          |
| E102            | Lee         | Analyst      | 45          |
| E103            | Wong        | DBA          | 60          |

### **修正後的 3NF 表格結構**
#### **Table 1: EMPLOYEE (3NF)**
| **EMP_NUM** (PK) | **EMP_NAME** | **JOB_CLASS** (FK) |
|-----------------|-------------|-------------------|
| E101            | Smith       | Engineer          |
| E102            | Lee         | Analyst           |
| E103            | Wong        | DBA               |

#### **Table 2: JOB (新增表格)**
| **JOB_CLASS** (PK) | **CHG_HOUR** |
|-------------------|-------------|
| Engineer          | 50          |
| Analyst           | 45          |
| DBA               | 60          |

#### **Table 3: ASSIGNMENT (保持不變)**
| **PROJ_NUM** (FK) | **EMP_NUM** (FK) | **HOURS** |
|------------------|----------------|---------|
| P001             | E101           | 10      |
| P001             | E102           | 15      |
| P002             | E103           | 20      |

#### **Table 4: PROJECT (保持不變)**
| **PROJ_NUM** (PK) | **PROJ_NAME** |
|------------------|--------------|
| P001             | Apollo       |
| P002             | Gemini       |


# Improving the design
- Normalization form only focus on avoiding data redundancy
- Beyond normalization, there are still various issues we need to address
  1. Minimize data entry errors
  2. Evaluate naming conventions
  3. Refine attribute atomicity
  4. Identify new attributes
  5. Identify new relationships
  6. Refine primary keys as required for data granularity
  7. Maintain historical accuracy
  8. Evaluate using derived attributes

# Minimize data entry errors
- When a new database designer on board, we need insert a record in EMPLOYEE table. Thus, we enter data into JOB_CLASS. 
- However, sometime we may enter either Database Designer, DB Designer or database designer. It easily makes data entry errors
- Reduce the data enter errors by adding a <span class="brown-text">surrogate key</span> JOB_CODE <br>   JOB_CODE → JOB_CLASS, CHG_HOUR 
- Table JOB(<u>**JOB_CODE**</u>, JOB_CLASS, CHG_HOUR)
- Surrogate key is an artificial key introduced by DB designer
  - simplify PK design
  - usually numeric
  - often generated automatically by DBMS

#### **問題背景**
當新入職的資料庫設計師需要被加入`EMPLOYEE`表時，我們需要在`JOB_CLASS`欄位輸入職位名稱。然而，人工輸入可能導致不一致的情況，例如：
- "Database Designer"
- "DB Designer"  
- "database designer"

這些不一致的寫法會造成**數據輸入錯誤**，並導致後續查詢和分析困難。


### **解決方案：引入代理鍵(Surrogate Key)**
#### **1. 什麼是代理鍵？**
- **人工建立的替代鍵**：由資料庫設計師額外添加的欄位，不具業務意義
- **簡化主鍵設計**：
  - 通常使用簡單的數字（如1, 2, 3...）
  - 可由資料庫自動生成（如AUTO_INCREMENT）
- **取代自然鍵(Natural Key)**：避免使用可能變動或重複的業務欄位（如職稱、姓名）作為主鍵

#### **2. 修改後的`JOB`表結構**
| **JOB_CODE** (PK, Surrogate Key) | **JOB_CLASS**         | **CHG_HOUR** |
|--------------------------------|----------------------|-------------|
| 1                              | Database Designer    | 70          |
| 2                              | Engineer             | 50          |
| 3                              | Analyst              | 45          |

#### **3. 對應的`EMPLOYEE`表結構**
| **EMP_NUM** (PK) | **EMP_NAME** | **JOB_CODE** (FK) |
|-----------------|-------------|------------------|
| E101            | Smith       | 2                |
| E102            | Lee         | 3                |
| E103            | Wong        | 1                |


### **改進後的優點**
1. **統一數據輸入**：
   - 只需選擇`JOB_CODE`（如輸入"1"），避免手動鍵入職稱
   - 完全消除拼寫不一致問題

2. **提高效率**：
   - 數字類型的代理鍵比文字欄位更節省存儲空間
   - 在關聯查詢時，數字比對速度更快

3. **業務靈活性**：
   - 即使職稱未來需要修改（如"DB Designer"改為"Database Architect"），只需在`JOB`表中更新一次，無需修改所有員工記錄
   - 代理鍵（數字）永遠不變，確保關聯完整性

### **代理鍵 vs 自然鍵 比較**
| 特性                | 代理鍵 (JOB_CODE)       | 自然鍵 (JOB_CLASS)       |
|---------------------|------------------------|-------------------------|
| **鍵值內容**         | 無意義數字（如1,2,3）  | 業務相關值（如職稱）    |
| **變動性**          | 永不改變               | 可能隨業務需求改變      |
| **輸入錯誤風險**     | 極低（選擇數字即可）    | 高（需手動輸入文字）    |
| **儲存效率**        | 高（通常4 bytes）       | 低（文字佔用更多空間）  |



# Evaluate Naming Conventions
- CHG_HOUR changed to JOB_CHG_HOUR
- JOB_CLASS changed to JOB_DESCRIPTION
- HOURS changed to ASSIGN_HOURS

# Refine Attribute atomicity(原子性)
- Atomicity: not being able to be divided into small units
- An atomic attribute is an attribute that cannot be further subdivided
- EMP_NAME divided into EMP_LNAME, EMP_FNAME, EMP_INITIAL

# Identify New attributes
- Consider if any other attributes could be added into table
- Social Security Number, Hire Date,....

# Identify New Relationships
- Add EMP_NUM attribute into PROJECT as a foreign key to keep project manager information

# Refine PKs as Required for Data Granularity (1/3)
- How often an employee reports hours work on a project and at what level of granularity (many times per day, once a day, once a week, at the end of project)
- <span class="brown-text">Granularity</span> refers to the level of detail represented by the values stored in a table’s row


- After 3NF
  ASSIGNMENT(<u>**PROJ_NUM**, **EMP_NUM**</u>, ASSIGN_HOUR)
  
PROJ_NUM|EMP_NUM|ASSIGN_HOUR
--------|-------|-----------
15|103|2.6
18|118|1.4

Report hours at the end of project

# Refine PKs as Required for Data Granularity (2/3)

- Add ASSIGN_DATE attribute
  ASSIGNMENT(<u>**PROJ_NUM**, **EMP_NUM**, **ASSIGN_DATE**</u>, ASSIGN_HOUR)

<style scoped>
table {
  font-size: 25px;
}
</style>
PROJ_NUM|EMP_NUM|ASSIGN_DATE|ASSIGN_HOUR
--------|-------|-----------|-----------
15|103|06-Mar-22|2.6
18|118|06-Mar-22|1.4

Report hours once a day

# Refine PKs as Required for Data Granularity (3/3)
- Add ASSIGN_NUM as a surrogate key
  ASSIGNMENT(<u>**ASSIGN_NUM**</u>, PROJ_NUM, EMP_NUM, ASSIGN_DATE, ASSIGN_HOUR)

<style scoped>
table {
  font-size: 25px;
}
</style>
ASSIGN_NUM|PROJ_NUM|EMP_NUM|ASSIGN_DATE|ASSIGN_HOUR
--------|--------|-------|-----------|-----------
1001|15|103|06-Mar-22|2.6
1002|18|118|06-Mar-22|1.4

- Report hours anytime
- Lower granularity yields greater flexibility


#### **1. 初始設計（專案結束後回報工時）**
**表格結構**  
`ASSIGNMENT(PROJ_NUM, EMP_NUM, ASSIGN_HOUR)`  

| PROJ_NUM | EMP_NUM | ASSIGN_HOUR |
|----------|---------|-------------|
| 15       | 103     | 2.6         |
| 18       | 118     | 1.4         |

**特性**  
- **主鍵**：`(PROJ_NUM, EMP_NUM)`  
- **粒度**：每個員工在整個專案期間的**總工時**  
- **限制**：無法記錄每日/每時段工時  


#### **2. 增加日期屬性（每日回報工時）**  
**表格結構**  
`ASSIGNMENT(PROJ_NUM, EMP_NUM, ASSIGN_DATE, ASSIGN_HOUR)`  

| PROJ_NUM | EMP_NUM | ASSIGN_DATE | ASSIGN_HOUR |
|----------|---------|-------------|-------------|
| 15       | 103     | 06-Mar-22   | 2.6         |
| 18       | 118     | 06-Mar-22   | 1.4         |

**改進**  
- **主鍵**：`(PROJ_NUM, EMP_NUM, ASSIGN_DATE)`  
- **粒度**：可記錄**每日工時**  
- **新問題**：  
  - 若同一天需記錄多筆工時（如上午/下午）會衝突  
  - 複合主鍵過於複雜  


#### **3. 引入代理鍵（彈性記錄任意時段工時）**  
**表格結構**  
`ASSIGNMENT(ASSIGN_NUM, PROJ_NUM, EMP_NUM, ASSIGN_DATE, ASSIGN_HOUR)`  

| ASSIGN_NUM | PROJ_NUM | EMP_NUM | ASSIGN_DATE | ASSIGN_HOUR |
|------------|----------|---------|-------------|-------------|
| 1001       | 15       | 103     | 06-Mar-22   | 2.6         |
| 1002       | 18       | 118     | 06-Mar-22   | 1.4         |

**最終優化**  
- **主鍵**：`ASSIGN_NUM`（代理鍵）  
- **粒度**：可記錄**任意時段工時**（半日、小時等）  
- **優勢**：  
  - 完全解除主鍵對粒度的限制  
  - 無需修改主鍵即可新增更細粒度數據  
  - 簡化關聯查詢（用單一數字鍵取代多欄位組合鍵）  


### **粒度與主鍵設計的權衡**
| 設計版本         | 主鍵                     | 數據粒度               | 靈活性           | 適用場景               |
|------------------|--------------------------|-----------------------|------------------|-----------------------|
| 初始設計         | `(PROJ_NUM, EMP_NUM)`    | 專案總工時            | 低               | 專案結算後一次性回報  |
| 增加日期         | `(PROJ_NUM, EMP_NUM, DATE)` | 每日工時              | 中               | 每日工時報表          |
| **代理鍵設計**   | `ASSIGN_NUM`             | **任意時段工時**      | **高**           | 即時工時追蹤系統      |


### **結論**
1. **代理鍵解放粒度限制**  
   - 透過人工生成的`ASSIGN_NUM`，徹底分離「業務邏輯」與「主鍵結構」  
   - 未來可隨時新增更細粒度欄位（如`ASSIGN_START_TIME`）而不影響既有關聯  

2. **效能與維護平衡**  
   - 代理鍵簡化索引設計（整數比多欄位組合鍵更高效）  
   - 避免因業務需求變動（如新增時間粒度）而重構主鍵  

# Maintain historical accuracy
- Add job charge per hour (ASSIGN_CHG_HOUR) into ASSIGNMENT table is important to maintain historical accuracy of the data
- JOB_CHG_HOUR in JOB and ASSIGN_CHG_HOUR in ASSIGNMENT. they may the same in a time period. 
- Due to salary raise, JOB_CHG_HOUR will be changed
- ASSIGN_CHG_HOUR keep historical data and only reflect the charge hour whey employee report hours

# Evaluate Using Derived Attributes
- For simplify coding or improve performance, database designer will introduce derived attributes
- The derived attribute ASSIGN_CHARGE comes from a transitive dependency
- (ASSIGN_HOURS + ASSIGN_CHG_HOUR) → ASSIGN_CHARGE

# The Completed Database After Design Improvement

![螢幕擷取畫面 2025-03-31 202831](https://github.com/user-attachments/assets/2538d602-2c71-4cbd-a1e1-44dc2469bb21)

<img width="513" alt="image" src="https://github.com/user-attachments/assets/52db2e45-d1dd-4bde-8513-552c1cad6d56" />

# Surrogate Key Considerations
- Surrogate keys are used by designers when the primary key is considered to be unsuitable
- A surrogate key is a system-defined attribute generally created and managed via the DBMS
- Usually it is a numeric value which is automatically incremented for each new row

# Higher-Level Normal Forms
- Tables in 3NF will perform suitably for business transactional databases
- Higher normal forms are sometimes useful for theoretical interest or statistical research
- Higher-level normal forms: Boyce-Codd normal form (BCNF), 4NF and 5NF

# Normalization and Database Design
- Normalization should be part of the design process
- Proposed entities must meet the required normal form before table structures are created
- Principles and normalization procedures should be written when redesigning and modifying databases
- ERD should be updated through the iterative process

# Denormalization
- Important database design goals include the following:
  - Creation of normalized relations 
  - Considering processing requirements and speed
- A problem with normalization is that joining a larger number of tables takes additional input/output (I/O) operations, thereby reducing system speed
- Defects in unnormalized tables include the following:
  - Data updates are less efficient because tables are larger
  - Indexing is more cumbersome
  - lead to data redundancy

### **反正規化（Denormalization）的權衡與實務應用**

#### **1. 正規化 vs. 反正規化的核心矛盾**
| 特性               | 正規化 (Normalization)       | 反正規化 (Denormalization)  |
|--------------------|-----------------------------|----------------------------|
| **設計目標**       | 消除冗餘、確保數據一致性     | 提升查詢性能               |
| **表格數量**       | 多（高度拆分）              | 少（合併表格）             |
| **I/O 操作**       | 需大量 JOIN（速度較慢）      | 單表查詢（速度較快）       |
| **更新效率**       | 高（數據只存一份）          | 低（需同步更新多處）       |
| **適用場景**       | OLTP 系統（頻繁增刪改）     | OLAP 系統（複雜查詢）      |

---

#### **2. 反正規化的典型缺陷**
即使能提升查詢速度，反正規化仍會帶來以下問題：
- **數據冗餘（Data Redundancy）**  
  同一數據存儲在多處，浪費空間且增加維護成本。  
  *範例：若將客戶姓名直接存於訂單表，當客戶改名時需批量更新所有相關訂單。*

- **更新異常（Update Anomalies）**  
  需額外機制確保數據同步，否則會產生不一致。  
  *範例：產品單價反正規化到訂單明細後，若原價變動，歷史訂單金額可能錯誤。*

- **索引複雜度（Cumbersome Indexing）**  
  合併後的表格欄位增多，導致索引體積龐大、維護成本高。

---

#### **3. 何時該考慮反正規化？**
##### **適用情境**  
✅ **報表系統**：需快速聚合大量數據（如每日銷售統計）  
✅ **讀多寫少**：數據幾乎不變動（如產品目錄的歷史快照）  
✅ **性能瓶頸**：JOIN 操作已明顯拖慢關鍵查詢  

Denormalization（非正規化）是在資料庫設計中，為了提高查詢效能而故意增加冗餘數據的做法。以下用一個具體的例子來說明：  

### **範例：電商訂單系統**  

#### **1. 正規化的表格設計（第三正規化，3NF）**  
假設我們有一個電商平台，顧客可以下訂單，每張訂單可以包含多個商品。我們用以下的表格設計來存儲數據：  

- **Customers（顧客）**
  | CustomerID | Name  | Email            |
  |------------|-------|-----------------|
  | 101        | 小明  | ming@gmail.com  |
  | 102        | 小華  | hua@gmail.com   |

- **Orders（訂單）**
  | OrderID | CustomerID | OrderDate  |
  |---------|------------|------------|
  | 5001    | 101        | 2025-03-31 |
  | 5002    | 102        | 2025-03-30 |

- **OrderDetails（訂單詳情）**
  | OrderID | ProductID | Quantity | Price  |
  |---------|----------|---------|--------|
  | 5001    | A001     | 2       | 100    |
  | 5001    | B002     | 1       | 50     |
  | 5002    | A001     | 1       | 100    |

- **Products（產品）**
  | ProductID | ProductName | Category  |
  |----------|-------------|-----------|
  | A001     | 鉛筆        | 文具      |
  | B002     | 橡皮擦      | 文具      |

這種設計是標準的正規化數據庫，每張表只存放必要的資訊，減少重複數據，並且透過關聯鍵（如 CustomerID、OrderID）來連結不同表格。  

#### **2. 非正規化（Denormalization）後的表格設計**  
如果我們經常需要查詢「某位顧客的所有訂單詳情」，則可能會選擇非正規化，將數據合併到一張表中，以減少 JOIN 操作，提高查詢速度。  

- **DenormalizedOrders（非正規化訂單）**
  | OrderID | CustomerID | CustomerName | Email          | OrderDate  | ProductID | ProductName | Quantity | Price  |
  |---------|-----------|--------------|---------------|------------|----------|-------------|---------|--------|
  | 5001    | 101       | 小明         | ming@gmail.com | 2025-03-31 | A001     | 鉛筆        | 2       | 100    |
  | 5001    | 101       | 小明         | ming@gmail.com | 2025-03-31 | B002     | 橡皮擦      | 1       | 50     |
  | 5002    | 102       | 小華         | hua@gmail.com  | 2025-03-30 | A001     | 鉛筆        | 1       | 100    |

這張表合併了 Customers、Orders、OrderDetails 和 Products 的數據，因此當我們查詢某位顧客的訂單時，只需要讀取這一張表，而不需要 JOIN 其他表。  

### **Denormalization 的優缺點**  

✅ **優點**：
- 減少 JOIN 操作，提高查詢速度，適合讀取頻繁的應用（如報表或搜尋）。  
- 查詢變得更簡單，開發成本降低。  

❌ **缺點**：
- 數據冗餘變多，增加了儲存空間需求。  
- 更新數據時（如修改商品名稱），可能需要修改多筆記錄，容易出錯。  

非正規化適用於 **讀取頻率高但寫入較少的情境**，如分析報表或搜尋系統，而 **正規化適合經常寫入和修改數據的系統**，如交易數據庫。

# Data Modeling Checklist
![image](https://github.com/user-attachments/assets/db0d600c-6d9b-484f-a041-75b4d62dd4db)

# Review Questions
Normalization is the process of organizing a relational database to reduce redundancy and improve data integrity. It involves dividing large tables into smaller, more manageable ones while establishing relationships between them. The goal is to minimize data duplication and ensure consistency by following a series of normal forms, each with specific rules to refine the structure.  

A table is in First Normal Form (1NF) if it has a primary key, and all its attributes contain atomic (indivisible) values. This means that each column holds only one value per row, and there are no repeating groups or arrays. For example, if a customer table contains multiple phone numbers stored in a single column, it violates 1NF because phone numbers should be stored in separate rows or a related table.  

A table is in Second Normal Form (2NF) if it is already in 1NF and all non-key attributes are fully functionally dependent on the entire primary key. This means that if the primary key is composite (made of multiple columns), no non-key attribute should depend on only part of it. To achieve 2NF, partial dependencies must be removed by placing them in separate tables. For example, in an order details table with a composite primary key (OrderID, ProductID), if ProductName depends only on ProductID and not the full key, it should be moved to a separate product table.  

A table is in Third Normal Form (3NF) if it is in 2NF and there are no transitive dependencies, meaning non-key attributes do not depend on other non-key attributes. Every non-key attribute should depend only on the primary key. If a table contains a column like EmployeeDepartment and another column like DepartmentManager, where DepartmentManager depends on EmployeeDepartment rather than the primary key, this violates 3NF. To fix this, the department-related information should be placed in a separate department table.
# Homework: Contracting Company
1. Read section 6-7 Normalization and Database Design
2. Design database schemas for Contracting Company, including but not limited to
  - Business rules
  - Evolving history of ER diagram in terms of normal forms
  - 1NF, 2NF, 3NF conversion, dependency diagram and reason
  - At least 3 sample records of each table to illustrate PK and FK among tables to demonstrate their relationships.
  - Check your design by Table 6.7 Data Modeling Checklist
