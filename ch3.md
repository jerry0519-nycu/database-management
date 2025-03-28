# Chapter3: The Relational Database Model
- Learn about relational database structures like tables, attributes, primary key, foreign key and relationships.
- Learn about how **entity relationship diagrams (ERDs)** can be used to put relational database structures together.

# Tables and Their Characteristics
- A <span class="blue-text">table (relation)</span> is a two-dimensional structure composed of rows and columns
- Each <span class="blue-text">row (tuple)</span> represents a single entity occurrence within the entity set
- Each <span class="blue-text">column (attribute) </span> has a distinct column name
- Each intersection of a row and column represents a single <span class="blue-text">data value</span>
- All values in a column must conform to the same <span class="blue-text">data format</span>
- Each column has a specific allowable values known as the <span class="blue-text">attribute domain</span>
- Each table must have <span class="blue-text">primary key (PK) </span> that uniquely identifies each row
- A <span class="blue-text">foreign key (FK)</span> is a primary key of one table that has been placed in another table to illustrate the relationship among tables
- The order of the rows and columns is meaningless

| 術語          | 英文               | 定義說明                                                                 | 範例                                                                 |
|-------------------|-----------------------|--------------------------------------------------------------------------|----------------------------------------------------------------------|
| **表格（表）**     | Table / Relation      | 二維結構，由行和列組成，儲存特定類型的資料                                  | `學生表(學號, 姓名, 年齡)`                                           |
| **行（記錄）**     | Row / Tuple           | 代表一個實體的具體實例                                                     | `(S001, 王小明, 20)` → 一筆學生資料                                  |
| **列（欄位）**     | Column / Attribute    | 描述實體的特徵，有唯一名稱                                                 | `姓名`、`年齡` 是學生表的欄位                                        |
| **儲存格值**       | Cell Value            | 行與列交叉處的單一資料值                                                   | 學生表第1行「姓名」欄的值可能是 `王小明`                              |
| **欄位格式限制**   | Data Format           | 同一欄位的所有值必須符合相同資料類型                                         | `年齡` 欄位必須是整數，不可混雜文字                                   |
| **值域**           | Attribute Domain      | 欄位允許的取值範圍                                                         | `年齡` 欄位的值域可能是 `18~100`                                     |
| **主鍵**           | Primary Key (PK)      | 唯一識別每一行的欄位（不可重複、不可為空）                                   | `學號` 可作為學生表的主鍵                                            |
| **外鍵**           | Foreign Key (FK)      | 引用其他表主鍵的欄位，用來建立表間關聯                                       | `選課表` 中的 `學號` 是外鍵，引用 `學生表` 的主鍵                      |
| **行列順序無意義** | Order Independence    | 資料的邏輯意義不受行列物理排序影響                                           | 無論學生表的記錄按學號或姓名排序，查詢結果邏輯不變                     |


# Relational Database Theory - Functional Dependencies 
- **Functional dependence** means that the value of one or more attributes determines the value of one or more other attributes
- Definition in relational database theory 
  - Given a relation R and attribute sets X, Y ⊆ R , X is said to functionally determine Y (written X → Y) if each X value is associated with precisely one Y value. 
  - X is called the **determinant** or **the key**
  - Y is called the **dependent**
- X → Y ⇔ 對於 R 中的任意兩個元組（記錄）t1 和 t2，若 t1[X] = t2[X]，則必有 t1[Y] = t2[Y]。
  
# Example 1 of Functional Dependence

<img width="394" alt="image" src="https://github.com/user-attachments/assets/b047d14c-f9af-40d7-8c31-1f007e8d5326" />

- StudentID value determinate Semester values. The fact can be expressed by a functional dependency:
**StudentID → Semester**.
- If a row was added (StudentID = 1234 and Semester = 5), then the functional dependency would no longer exist.

# Example 2 of Functional Dependence

<img width="520" alt="image" src="https://github.com/user-attachments/assets/b7f6645a-cc91-4ab4-8733-1095cda79ad1" />

- STU_NUM → STU_LNAME
- STU_NUM → (STU_LNAME, STU_FNAME, STU_GPA)
- (STU_FNAME, STU_LNAME, STU_INIT, STU_PHONE) → (STU_DOB, STU_HRS, STU_GPA)
- STU_NUM → STU_GPA
- (STU_NUM, STU_LNAME) → STU_GPA

# Full Functional Dependence
- <span class="blue-text">Full functional dependence</span>: an attribute is functionally dependent on a composite key but not on any subset of the composite key.
- STU_NUM → STU_GPA is a full functional dependence 
- (STU_NUM, STU_LNAME) → STU_GPA is a functional dependence, but NOT a full functional dependence

#### **1. 定義**
- **功能相依性（Functional Dependence）**：  
  若屬性集合 `X` 能唯一決定屬性 `Y`（記作 `X → Y`），則稱 `Y` 功能依賴於 `X`。  
  - 例：`學號 → GPA`（透過學號可確定唯一 GPA 值）。

- **完全功能相依性（Full Functional Dependence）**：  
  `Y` 必須依賴於 `X` 的**全部屬性**，且不能僅依賴於 `X` 的任意子集。  
  - **關鍵點**：`X` 必須是**最小集合**，刪除 `X` 中任一屬性都會破壞依賴關係。

#### **2. 範例解析**
| 依賴關係 | 類型 | 原因 |
|----------|------|------|
| **`STU_NUM → STU_GPA`** | **完全功能相依** | GPA 僅由學號唯一決定，無需其他屬性輔助。 |
| **`(STU_NUM, STU_LNAME) → STU_GPA`** | **功能相依（非完全）** | GPA 實際僅需 `STU_NUM` 即可決定，姓氏是冗餘的。 |

**驗證邏輯**：  
1. 刪除 `STU_LNAME` 後，`STU_NUM → STU_GPA` 仍成立 → 證明 `STU_LNAME` 非必要。  
2. 因此，`(STU_NUM, STU_LNAME)` 不是最小決定集合。

# Types of Keys
- A key consists of attribute(s) that determine other attributes. 
  - Determinants in functional dependencies is a key.
  - Eg. invoice number identifies all of the invoice attributes, like invoice date and customer name.
  - Composite key: a key composed of more than one attribute
- Key types
  - Superkey: uniquely identify each entity
  - Candidate key: a minimal Superkey (no extra attributes)
  - PK: choice a candidate key as PK to ensure each row in a table is uniquely identifiable
  - FK: establish relationships among tables

| **鍵類型**       | **定義**                                                                 | **特點**                                                                 | **範例**                                                                 |
|------------------|--------------------------------------------------------------------------|--------------------------------------------------------------------------|--------------------------------------------------------------------------|
| **Superkey**<br>（超鍵） | 能「唯一識別」表中每筆記錄的「屬性組合」<br>（可能包含多餘屬性）。                     | - 不要求最小化<br>- 可能包含非必要屬性                                   | `(學號, 姓名, 電話)`<br>（學號已可唯一識別，姓名和電話是多餘的）             |
| **Candidate Key**<br>（候選鍵） | 是「最小化」的 Superkey<br>（移除任一屬性後，無法再唯一識別記錄）。                     | - 無冗餘屬性<br>- 一個表可能有多個候選鍵                                 | `學號` 或 `身分證字號`<br>（兩者皆能唯一識別學生，且無多餘屬性）               |
| **Primary Key (PK)**<br>（主鍵） | 從候選鍵中「選擇一個」作為正式的唯一識別依據。                                       | - 不可為 `NULL`<br>- 值不可重複<br>- 用於建立索引                       | 選擇 `學號` 而非 `身分證字號` 作為主鍵                                       |
| **Foreign Key (FK)**<br>（外鍵） | 是「其他表的主鍵」的引用，<br>用於建立表之間的關聯。                                  | - 值必須匹配主鍵或為 `NULL`<br>- 確保關聯完整性                         | `選課表` 中的 `學號` 是外鍵，引用 `學生表` 的主鍵                              |

**主鍵永遠不能更改、且值只能唯一**

# Example of Keys
- Superkey: STU_NUM, (STU_NUM, STU_LNAME), (STU_FNAME, STU_LNAME, STU_INIT)
- Candidate key: STU_NUM, (STU_FNAME, STU_LNAME, STU_INIT)
- Primary key: STU_NUM
- FK: DEPT_CODE, PROF_NUM 

# Example of a Simple Relational Database
<img width="501" alt="image" src="https://github.com/user-attachments/assets/8c3aa0c1-fbfa-4c0b-99ab-5f8a3297f6b6" />

# Relational Database Keys Comparison
Key Type| Definition
--------|-----------
Super key|Attribute(s) that uniquely identifies each row
Candidate key| Minimal Superkey without extra attributes
Primary key| Select from candidate keys. Uniquely identify row and cannot be NULL
Foreign key | Is a PK of one table that has been placed in another table to illustrate the relationship among tables

# Integrity Rules (完整性規則)
RDBMS rely on integrity rules to ensure data consistency, accuracy, and reliability to prevent errors and enforce business constraints.
- **Entity integrity**
- **Referential Integrity** 
  
# Integrity Rules - Entity Integrity
- Rule: Every table must have a PK, and its value cannot be NULL.
- Reason: Ensures that each row in a table is uniquely identifiable, preventing duplicate or missing records.
- Impact w/o it: A db with missing or duplicate keys could lead to data inconsistency.
- Example: When invoice number is a PK, duplicated invoice numbers or empty invoices number is not allowed. 

# Integrity Rules - Referential Integrity
- Rule: A FK must reference a valid PK in another table.
- Reason: Maintains valid relationships between tables and prevents orphaned records.
- Impact w/o it: If a referenced record is deleted without checking dependencies, it can lead to dangling references.
- Example:  A customer might not yet have an assigned sales representative (allow null), but it will be impossible to have an invalid sales representative (must reference).

| **比較項目**       | **實體完整性 (Entity Integrity)**                              | **參考完整性 (Referential Integrity)**                          |
|--------------------|---------------------------------------------------------------|----------------------------------------------------------------|
| **核心規則**       | 每個表格必須有主鍵（PK），且主鍵值不可為 `NULL`。               | 外鍵（FK）必須引用另一個表格中「已存在」的主鍵值（**或為 `NULL`**）。  |
| **目的**           | 確保每筆記錄都能被唯一識別，避免重複或缺失。                    | 維持表格間關聯的有效性，防止「孤兒記錄」或無效引用。              |
| **違反的後果**     | - 重複主鍵：無法區分不同記錄。<br>- 主鍵為 `NULL`：記錄無法被識別。 | - 外鍵引用不存在的值：關聯斷裂（如訂單找不到對應客戶）。           |
| **範例**           | **發票表**：<br>- 發票號碼（PK）不可重複或為空。                | **訂單表**：<br>- 客戶編號（FK）必須存在於客戶表中（或允許為 `NULL`）。 |
| **技術實現**       | 透過 `PRIMARY KEY` 約束實現。                                   | 透過 `FOREIGN KEY` 約束實現，可搭配 `ON DELETE CASCADE` 等動作。  |
| **例外處理**       | 無例外，主鍵絕對不可為 `NULL`。                                 | 可設定外鍵為 `NULL`，表示「暫無關聯」（如未分配銷售代表的客戶）。   |

# Illustration of Integrity Rules
<img width="465" alt="image" src="https://github.com/user-attachments/assets/79b22ac6-49d3-4c89-93b4-0664d4664e9a" />

# Relational Database Theory - Relational Algebra
- **Relational algebra** defines the theoretical way of manipulating table contents using relational operators.
- Eight main relational operators: SELECT, PROJECT, JOIN, INTERSECT, UNION, DIFFERENCE, PRODUCT, and DIVIDE

# Relational Set Operators (SELECT)
SELECT is an operator used to select a subset of rows

<img width="518" alt="image" src="https://github.com/user-attachments/assets/6c6dae2b-d152-4ffa-a9a0-4773abf8552e" />

# Relational Set Operators (PROJECT)
PROJECT is an operator used to select a subset of columns
<img width="518" alt="image" src="https://github.com/user-attachments/assets/a1b2bd18-586e-417d-8e5a-28d015ecf4b6" />

# Relational Set Operators (UNION)
UNION is an operator used to merge two tables into a new table, dropping duplicate rows
<img width="517" alt="image" src="https://github.com/user-attachments/assets/55641d3b-2e49-4a70-8c26-6bf1b7466cfe" />

# Relational Set Operators (INTERSECT)
INTERSECT is an operator used to yield only the rows that are common to two union-compatible tables
<img width="512" alt="image" src="https://github.com/user-attachments/assets/279f9698-ee2a-4cf3-ac26-a2329ed4854e" />

# Relational Set Operators (DIFFERENCE)
DIFFERENCE is an operator used to yield all rows from one table that are not found in another union-compatible table
<img width="511" alt="image" src="https://github.com/user-attachments/assets/091b732b-80ae-4df0-9909-de3d6647d1e2" />

# Relational Set Operators (PRODUCT)
PRODUCT is an operator used to yield all possible pairs of rows from two tables
<img width="511" alt="image" src="https://github.com/user-attachments/assets/47d9d268-13ff-45f1-b22e-3c5c740beaca" />

# Relational Set Operators (JOIN)
JOIN allows information to be intelligently combined from two or more tables
- **Inner join** – only returns matched records from the tables that are being joined
  - Natural join links tables by selecting only the rows with common values in their common attributes <span class="red-text">(generally DISCOURAGED in practice)</span>
  - Equijoin – links tables on the basis of an equality condition that compares specified columns of each table
  - Theta join – links tables using an inequality comparison operator
- **Left outer join**: yields all of the rows in the first table, including those that do not have a matching value in the second table 
- Right outer join: yields all of the rows in the second table, including those that do not have matching values in the first table

# Natural Join
PRODUCT -> SELECT -> PROJECT

<img width="600" alt="image" src="https://github.com/user-attachments/assets/b28fad39-967b-4db6-8b8e-12d346afd5d6" />

1. First, a PRODUCT of the tables is created, yielding the results shown in
Figure 3.11.

<img width="600" alt="image" src="https://github.com/user-attachments/assets/c9a8e10f-5f82-4593-b392-65e551157493" />

2. Second, a SELECT is performed on the output of Step 1 to yield only the rows for
which the AGENT_CODE values are equal. The common columns are referred to
as the join columns. Step 2 yields the results shown in Figure 3.12.

<img width="600" alt="image" src="https://github.com/user-attachments/assets/ab10c5c9-f3d6-42a8-a7df-2c3a869336db" />

3. A PROJECT is performed on the results of Step 2 to yield a single copy of each
attribute, thereby eliminating duplicate columns. Step 3 yields the output shown
in Figure 3.13.

<img width="600" alt="image" src="https://github.com/user-attachments/assets/1f879314-67d8-4280-a8ce-d910b4b86f9f" />


# Left Outer Join

<img width="600" alt="image" src="https://github.com/user-attachments/assets/b28fad39-967b-4db6-8b8e-12d346afd5d6" />

<img width="600" alt="image" src="https://github.com/user-attachments/assets/756d51b7-c6f6-4774-a42c-23b5f37f6678" />

A left outer join yields all of the rows in the CUSTOMER table, including those
that do not have a matching value in the AGENT table. An example of such a join is
shown in Figure 3.14.
# Right Outer Join

<img width="600" alt="image" src="https://github.com/user-attachments/assets/b28fad39-967b-4db6-8b8e-12d346afd5d6" />

<img width="600" alt="image" src="https://github.com/user-attachments/assets/9966b52f-bb7b-4dbc-ac52-dc815d380769" />

A right outer join yields all of the rows in the AGENT table, including those that
do not have matching values in the CUSTOMER table. An example of such a join is
shown in Figure 3.15.


| JOIN 類型       | 定義                                                                 | 結果特點                                                                 |                        
|----------------|----------------------------------------------------------------------|--------------------------------------------------------------------------|
| **Inner Join** <br>(內連接) | 只返回兩表中「匹配成功」的記錄                                         | 結果集較小，僅包含有關聯的數據                                           | 
| **Natural Join** <br>(自然連接) | 自動根據「同名同值」欄位連接（不建議使用）                            | 可能意外連接多餘欄位，可讀性差                                           | 
| **Equijoin** <br>(等值連接) | 明確指定「等值條件」的內連接（最常用）                                | 清晰可控，可自訂連接條件                                                 | 
| **Theta Join** <br>(θ連接) | 使用「不等式」連接（如 >, <）                                        | 用於非等值關係分析                                                       | 
| **Left Outer Join** <br>(左外連接) | 返回左表全部記錄 + 右表匹配記錄（無匹配則右表欄位為 NULL）            | 確保左表數據不遺失                                                       |
| **Right Outer Join** <br>(右外連接) | 返回右表全部記錄 + 左表匹配記錄（無匹配則左表欄位為 NULL）            | 確保右表數據不遺失                                                       | 
| **Full Outer Join** <br>(全外連接) | 返回兩表所有記錄（無匹配則對面表欄位為 NULL）                         | 最完整的結果集，但效能較差                                               | 

### **Left Outer Join 與 Right Outer Join 圖解比較**

#### **1. 基本定義對比**
| 操作類型          | 核心邏輯                                                                 | 結果集特點                                                                 |
|------------------|--------------------------------------------------------------------------|--------------------------------------------------------------------------|
| **Left Outer Join** <br>(左外連接) | 保留「左表」所有記錄，右表無匹配則填 `NULL`                               | 確保左表資料不遺失（即使無關聯）                                           |
| **Right Outer Join** <br>(右外連接) | 保留「右表」所有記錄，左表無匹配則填 `NULL`                               | 確保右表資料不遺失（即使無關聯）                                           |


##### **原始表格數據**
- **CUSTOMER 表** (左表)  
  | CUS_CODE | CUS_LNAME | AGENT_CODE |
  |----------|-----------|------------|
  | 1132445  | Walter    | 231        |
  | 1217782  | Adares    | 125        |
  | ...      | ...       | ...        |

- **AGENT 表** (右表)  
  | AGENT_CODE | AGENT_PHONE   |
  |------------|---------------|
  | 125        | 6152439887    |
  | 333        | 9041234445    | ← 無對應客戶 |

##### **Left Outer Join 結果**
- **保留所有客戶**，無代理的客戶仍列出（`AGENT_*` 欄位為 `NULL`）  
  | CUS_CODE | CUS_LNAME | AGENT_CODE (CUSTOMER) | AGENT_CODE (AGENT) | AGENT_PHONE   |
  |----------|-----------|-----------------------|--------------------|---------------|
  | 1542211  | Smithson  | **421**               | NULL               | NULL          | ← 代理 421 不存在 |
  | ...      | ...       | ...                   | ...                | ...           |

##### **Right Outer Join 結果**
- **保留所有代理**，無客戶的代理仍列出（`CUS_*` 欄位為 `NULL`）  
  | CUS_CODE | CUS_LNAME | AGENT_CODE (CUSTOMER) | AGENT_CODE (AGENT) | AGENT_PHONE   |
  |----------|-----------|-----------------------|--------------------|---------------|
  | NULL     | NULL      | NULL                  | **333**            | 9041234445    | ← 代理 333 無客戶 |
  | ...      | ...       | ...                   | ...                | ...           |


# Relational Set Operators (DIVIDE)
The DIVIDE operator is used to answer questions about one set of data being associated with all values of data in another set of data
- Determine which customers (on the left), if any, purchased every product shown in P_CODE table (in the middle).

<img width="600" alt="image" src="https://github.com/user-attachments/assets/e0a08374-ee2a-499b-9a20-1f9a4ca4b0dd" />


**DIVIDE** 是關聯式資料庫中的一種集合運算，用於解決「**滿足所有條件**」的查詢問題，類似於「**反向的乘法**」。以下是逐步說明：
#### **1. 核心概念**  
- **作用**：找出「**符合所有指定關聯條件**」的記錄。  
- **生活化比喻**：  
  - 像「找出**修過所有必修課**的學生」或「**供應所有指定產品**的供應商」。  
- **數學意義**：  
  若 `A ÷ B = C`，則 `C × B ⊆ A`（C 與 B 的組合必須完全包含於 A 中）。

#### **2. 實際範例**  
假設有以下表格：  
- **STUDENT_COURSE（學生選課表）**  
  | STUDENT_ID | COURSE_ID |  
  |------------|-----------|  
  | S001       | C101      |  
  | S001       | C102      |  
  | S002       | C101      | ← 只修了 C101  
  | S003       | C101      |  
  | S003       | C102      | ← 修了 C101 和 C102  

- **REQUIRED_COURSES（必修課表）**  
  | COURSE_ID |  
  |-----------|  
  | C101      |  
  | C102      |  

**問題**：找出修過「所有必修課」的學生。  
**DIVIDE 操作結果**：  
| STUDENT_ID |  
|------------|  
| S001       |  
| S003       |  

#### **3. 與其他 JOIN 的區別**  
| 操作        | 用途                          | 範例                              |  
|------------|-------------------------------|-----------------------------------|  
| **INNER JOIN** | 找出兩表「匹配」的記錄          | 找出「有選課的學生」               |  
| **DIVIDE**    | 找出「滿足所有子條件」的記錄    | 找出「修過所有必修課的學生」       |  


| 操作 | 符號 | 作用 | 輸入 | 輸出 | 主要用途 |
|------|------|------|------|------|--------|
| **Select** (選擇) | σ | 選出符合條件的行 | 一個表 | 一個較小的表 | 篩選資料 |
| **Project** (投影) | π | 選出特定的列 | 一個表 | 只有指定列的新表 | 取出需要的欄位 |
| **Product** (笛卡兒積) | × | 兩個表的所有組合 | 兩個表 | 新表，包含所有可能的組合 | 搭配 Join 使用 |
| **Union** (聯集) | ∪ | 合併兩個表，不重複 | 兩個結構相同的表 | 合併後的新表 | 合併資料 |
| **Difference** (差集) | − | 找出 A 表有但 B 表沒有的資料 | 兩個結構相同的表 | 只包含 A 有 B 沒有的資料 | 比較差異 |
| **Join** (連接) | ⨝ | 依條件合併兩表 | 兩個表 | 符合條件的組合新表 | 連結相關資料 |
| **Divide** (除法) | ÷ | 找出符合所有條件的資料 | 兩個表，B 是 A 的子集 | 符合條件的資料 | 找滿足條件的組合 |

# Data Dictionary and the System Catalog
- **Data dictionary** describes all tables in the DB created by the user and designer
- **System catalog** describes all objects within the database
  - Homonym – same name is used to label different attributes 
  - Synonym – different names are used to describe the same attribute. 
  - Both homonym and synonym should be avoided whenever possible 

![螢幕擷取畫面 2025-03-28 152530](https://github.com/user-attachments/assets/5366ab25-87e8-4f7d-a672-e5a673187ba0)

#### **1. 系統目錄（System Catalog）**  
- **定義**：資料庫的「資料字典」，記錄所有物件（如表、欄位、索引）的定義與 metadata。  
- **功能**：  
  - 儲存表格結構、約束條件、權限設定等資訊。  
  - 讓 DBMS 管理查詢優化與完整性檢查。  
- **範例**：  
  - 查詢 `INFORMATION_SCHEMA.TABLES`（MySQL）或 `pg_catalog`（PostgreSQL）可看到所有表定義。

#### **2. 同音異義（Homonym）**  
- **定義**：**相同名稱**被用來標示**不同屬性**（可能在不同表中）。  
- **問題**：  
  - 造成混淆，例如：`ID` 在 `客戶表` 是客戶編號，在 `訂單表` 是訂單編號。  
  - 查詢時需明確指定來源（如 `客戶.ID` vs `訂單.ID`）。  
- **解決方法**：  
  - 使用明確命名（如 `CUST_ID`、`ORDER_ID`）。  

#### **3. 同義詞（Synonym）**  
- **定義**：**不同名稱**被用來描述**相同屬性**（如 `客戶編號` 與 `客戶ID`）。  
- **問題**：  
  - 降低可讀性，增加維護成本（需記住多種名稱）。  
  - 例如：`CUST_ID`（客戶表）與 `CLIENT_NO`（報表系統）實際指向同一資料。  
- **解決方法**：  
  - 統一命名（全系統使用 `CUST_ID`）。
  
| 問題類型   | 影響                                                                 | 實際案例                                                                 |
|------------|----------------------------------------------------------------------|--------------------------------------------------------------------------|
| **Homonym** | 查詢錯誤、JOIN 衝突                                                  | 兩表都有 `NAME` 欄位，`JOIN` 時需用別名（如 `A.NAME` vs `B.NAME`）。      |
| **Synonym** | 維護困難、文件與程式不一致                                            | 開發者需記住 `CUST_ID`、`CLIENT_ID`、`USER_NO` 其實是同一欄位。           |


# Relationships within the Relational Database 
- The one-to-many (1:M) relationship is the norm for relational databases 
- In the one-to-one (1:1) relationship, one entity can be related to one and only one other entity and vice versa 
- The many-to-many (M:N) relationship can be implemented by creating a new entity in 1:M relationships with the original entities

# 1:M Relationship

<img width="405" alt="image" src="https://github.com/user-attachments/assets/073254ef-109b-4c4d-a1ed-e35918edf4ef" />

<img width="522" alt="image" src="https://github.com/user-attachments/assets/a7833152-d36a-488c-8c43-92bc419a7541" />

<img width="397" alt="image" src="https://github.com/user-attachments/assets/a19f03c4-67a9-4fb0-8dde-e2956bfdd191" />

<img width="522" alt="image" src="https://github.com/user-attachments/assets/d725df3f-07d8-4e7d-823e-bc53cac5a718" />


# 1:1 Relationship
- 1:1 a professor only chair one department
- 1:M a department employee many professors

<img width="399" alt="image" src="https://github.com/user-attachments/assets/965b2734-96b8-4289-9a66-2665c235ce03" />

![螢幕擷取畫面 2025-03-28 153239](https://github.com/user-attachments/assets/db591ad8-0ef0-4917-a887-fa0a24275918)

# M:N Relationship
- A M:N relationship is not supported directly in the relational environment.
- M:N relationship can be implemented by creating a new entity in 1:M relationships with the original entities
- In Fig 3.24, the tables create many data redundancies and relational operation become complex and less efficiency  

<img width="396" alt="image" src="https://github.com/user-attachments/assets/2fa1bbec-6c3f-4b94-ac31-63d02e8e1f4c" />

### **關聯類型比較表：一對多（1:M）、一對一（1:1）、多對多（M:N）**

| **比較維度**       | **一對多（1:M）**                                                                 | **一對一（1:1）**                                                                 | **多對多（M:N）**                                                                 |
|--------------------|----------------------------------------------------------------------------------|----------------------------------------------------------------------------------|----------------------------------------------------------------------------------|
| **定義**           | 一個實體（A）的單一實例關聯到多個實體（B）的實例，但（B）的實例只能關聯到一個（A）實例。 | 一個實體（A）的單一實例僅關聯到一個實體（B）的實例，反之亦然。                      | 一個實體（A）的單一實例可關聯到多個實體（B）的實例，且（B）的實例也可關聯到多個（A）實例。 |
| **資料庫實現**     | 在「多」方表格（B）中加入「一」方表格（A）的主鍵作為外鍵。                           | 在任一表格中加入另一表格的主鍵作為外鍵（通常合併為單一表格）。                       | 需建立「關聯表」（Junction Table）儲存兩表主鍵的組合。                              |
| **範例**           | - 一位客戶（A）可有多筆訂單（B）<br>- 訂單表包含 `客戶ID` 外鍵。                     | - 一位員工（A）對應一個員工證（B）<br>- 員工證表包含 `員工ID` 外鍵（或反向）。        | - 學生（A）選修多門課程（B）<br>- 需建立「選課表」記錄 `學生ID` 和 `課程ID`。          |



# Introduce Composite Entry into M:N Relationship
Table ENROLL is a composite entry (bridge entry, associative entry, link table) to help convert M:N to 1:M

<img width="519" alt="image" src="https://github.com/user-attachments/assets/a545f287-66fc-4052-a0f0-d08354e45cba" />

<img width="521" alt="image" src="https://github.com/user-attachments/assets/6fa5c9ba-49ee-430f-b53b-a71155290447" />

<img width="399" alt="image" src="https://github.com/user-attachments/assets/d56b150b-719c-4631-9285-d23f74183b29" />

# Data Redundancy Revisited
- The relational database control of data redundancies through use of foreign keys
- Data redundancy should be controlled except performance and historical data

#### **1. 關聯式資料庫如何控制冗餘？**  
- **核心機制**：透過**外鍵（Foreign Key, FK）** 建立表間關聯，避免重複儲存相同資料。  
- **範例**：  
  - 在 `訂單表` 中儲存 `客戶ID`（FK），而非直接重複客戶姓名、地址等資料。  
  - 需查詢客戶資訊時，再用 `JOIN` 連結 `客戶表`。  

#### **2. 為何要控制冗餘？**  
| **問題**          | **說明**                                                                 |
|-------------------|-------------------------------------------------------------------------|
| **更新異常**       | 若資料重複儲存，修改時需同步多處（如客戶改名需更新所有訂單中的客戶姓名）。 |
| **儲存空間浪費**   | 相同資料在多處重複佔用空間。                                            |
| **一致性風險**     | 部分資料可能未同步更新，導致矛盾（如訂單中的客戶姓名與主表不同）。        |

#### **3. 何時「允許」冗餘？**  
- **效能優化**：  
  - 高頻查詢的衍生數據（如訂單總金額）可冗餘儲存，避免即時計算。  
- **歷史資料保留**：  
  - 需凍結的記錄（如發票明細）應冗餘儲存，即使主表資料變更也不影響。  


# Index to Increase Performance
- An index is an orderly arrangement to logically access rows in a table
- The index key is the reference point that leads to data location identified by the key
- A table can have many indexes, but each index is associated with only one table
- The index key can have multiple attributes

#### **1. 索引是什麼？**
- **定義**：資料庫中的一種「**有序結構**」，用於**快速定位**表格中的特定資料列，類似書籍的目錄。
- **核心目的**：避免全表掃描（Full Table Scan），大幅提升查詢效能。


#### **2. 關鍵特性解析**
| 特性 | 說明 | 實際案例 |
|------|------|----------|
| **有序結構** | 索引按特定欄位值排序儲存（如 B+Tree 結構） | 對 `學號` 建立索引後，查詢 `學號=S001` 可直接跳轉到目標位置，無需逐筆檢查。 |
| **索引鍵（Index Key）** | 用於建立索引的欄位或欄位組合，是查詢的參考點 | `(姓名, 年齡)` 可作為複合索引鍵。 |
| **一表多索引** | 一個表格可建立多個索引，但每個索引只能屬於一個表 | `學生表` 可同時有 `學號索引` 和 `姓名索引`。 |
| **多屬性索引鍵** | 索引可基於多個欄位（複合索引） | 對 `(城市, 郵遞區號)` 建立聯合索引，加速「城市+郵遞區號」的查詢。 |


# Review Questions
1. **What are the integrity rules in RDBMS?**  
   - **Entity Integrity Rule**: Every table must have a **Primary Key (PK)**, and the values in this key **cannot be NULL**. This ensures that each row is uniquely identifiable.  
   - **Referential Integrity Rule**: A **Foreign Key (FK)** in one table must reference a **valid Primary Key (PK)** in another table. This maintains consistent relationships between tables and prevents orphaned records.  

2. **Describe relational database operators to manipulate relational table contents.**  
   - **SELECT (σ)**: Filters rows based on a condition.  
   - **PROJECT (π)**: Selects specific columns from a table.  
   - **PRODUCT (×)**: Combines all rows from two tables, producing a Cartesian product.  
   - **JOIN (⨝)**: Combines rows from two tables based on a matching column.  
   - **UNION (∪)**: Merges two tables, keeping only unique rows.  
   - **INTERSECT (∩)**: Returns rows that are common in both tables.  
   - **DIFFERENCE (-)**: Returns rows that exist in one table but not in the other.  
   - **DIVIDE (÷)**: Used to find values in one table that match all values in another.  

3. **Describe how to deal with an M:N relationship.**  
   - **M:N relationships cannot be directly implemented** in a relational database.  
   - To convert an M:N relationship, create a **bridge table (associative table)** that connects the two original tables using **Foreign Keys (FKs)**.  
   - This bridge table breaks the M:N relationship into **two 1:M relationships**, improving efficiency and avoiding redundancy.  
   - Example: A **Student** can enroll in multiple **Courses**, and each **Course** can have multiple **Students**. The solution is to create an **ENROLLMENT** table with **Student_ID** and **Course_ID** as Foreign Keys.  
