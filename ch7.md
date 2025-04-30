# Introduction to MySQL
- MySQL is a relational database management system (RDBMS)
- MySQL is open-source and free
- MySQL is ideal for both small and large applications
- MySQL is very fast, reliable, scalable, and easy to use
- MySQL is cross-platform
- MySQL is compliant with the ANSI SQL standard
- MySQL was first released in 1995
- MySQL is developed, distributed, and supported by Oracle Corporation
- MySQL is named after co-founder Monty Widenius's daughter, My

# SQL Statement in MySQL
- SQL keywords are NOT case sensitive: select is the same as SELECT **(不分大小寫)**
- Use semicolon **(;)** at the end of each SQL statement to separate each SQL statement
- Some of The Most Important SQL Commands
	- INSERT INTO - [C]reates new data into a database
	- SELECT - [R]eads data from a database
	- UPDATE - [U]pdates data in a database
	- DELETE - [D]eletes data from a database
	- CREATE DATABASE - creates a new database; ALTER DATABASE - modifies a database
	- CREATE TABLE - creates a new table; ALTER TABLE - modifies a table; DROP TABLE - deletes a table
	- CREATE INDEX - creates an index (search key); DROP INDEX - deletes an index</span>

<details>
<summary><strong>整理表格</strong></summary>
	
| SQL 指令          | CRUD 分類 | 功能描述                             |
|-------------------|-----------|--------------------------------------|
| INSERT INTO       | [C]reate  | 新增資料至資料庫                     |
| SELECT           | [R]ead    | 從資料庫讀取資料                     |
| UPDATE           | [U]pdate  | 更新資料庫中的資料                   |
| DELETE           | [D]elete  | 從資料庫刪除資料                     |
| CREATE DATABASE  | -         | 建立新資料庫                         |
| ALTER DATABASE   | -         | 修改資料庫結構                       |
| CREATE TABLE     | -         | 建立新資料表                         |
| ALTER TABLE      | -         | 修改資料表結構                       |
| DROP TABLE       | -         | 刪除資料表                           |
| CREATE INDEX     | -         | 建立索引（搜尋鍵值）                 |
| DROP INDEX       | -         | 刪除索引                             |
</details>

 
# Chapter7: Introduction to Structured Query Language (SQL)
- SQL is composed of commands that enable users
  -  create database and table structures
  -  perform various types of data manipulation
  -  execute data administration
  -  query the database to extract useful information.
- All RDBMS supports SQL, and many software vendors have developed extensions to the basic SQL command set.

# SQL Basics
- Described in ANSI/ISO SQL
  - The American National Standards Institute (ANSI) prescribes a standard SQL.
  - International Organization for Standardization (ISO) also accept.
- SQL functions fit into several broad categories:
  - Data manipulation language (DML): INSERT, SELECT, UPDATE, DELETE
  - Data definition language (DDL): CREATE TABLE
  - Transaction control language (TCL): COMMIT, ROLLBACK
  - Data control language (DCL): GRANT, REVOKE
- SQL is a nonprocedural language, including many set operators

### **1. SQL 的標準化機構**
- **ANSI（美國國家標準協會）**  
  制定標準化的 SQL 語法，確保不同資料庫系統有一致的基礎規範。
- **ISO（國際標準化組織）**  
  國際上採納的 SQL 標準，與 ANSI 標準高度兼容，促進全球通用性。

> 📌 **關鍵點**：ANSI/ISO SQL 是資料庫系統的「共通語言」，但各廠商（如 Oracle、MySQL）可能會有額外擴充功能。


### **2. SQL 的功能分類**
根據 ANSI/ISO 標準，SQL 指令分為四大類別：

| 分類名稱                 | 英文全稱                     | 主要指令範例               | 功能說明                           |
|--------------------------|-----------------------------|----------------------------|------------------------------------|
| **資料操作語言 (DML)**   | Data Manipulation Language  | `INSERT`, `SELECT`, `UPDATE`, `DELETE` | 處理資料的「增刪改查」（CRUD）。   |
| **資料定義語言 (DDL)**   | Data Definition Language    | `CREATE TABLE`, `ALTER TABLE`, `DROP TABLE` | 定義或修改資料庫結構（如表格、索引）。 |
| **交易控制語言 (TCL)**   | Transaction Control Language| `COMMIT`, `ROLLBACK`, `SAVEPOINT`      | 管理資料庫交易（確保資料一致性）。 |
| **資料控制語言 (DCL)**   | Data Control Language       | `GRANT`, `REVOKE`          | 控制用戶權限（如存取限制）。       |

### **3. SQL 的特性**
- **非程序式語言（Nonprocedural）**  
  使用者只需聲明「要做什麼」（例如 `SELECT * FROM users`），不需指定「如何做」（如迴圈或步驟），由資料庫引擎自行優化執行。
- **集合操作（Set Operators）**  
  支援對「資料集合」進行操作（如 `UNION`、`INTERSECT`），而非逐筆處理。

# SQL Data Manipulation Commands

<img width="450" alt="image" src="https://github.com/user-attachments/assets/7b3e458e-1295-4e16-a285-52e35c3105f2" />

# SQL Data Definition Commands

<img width="450" alt="image" src="https://github.com/user-attachments/assets/f5fe3759-2839-417c-9279-d24492e9cb83" />

# Basic Data Types
- Numeric
- Character
- Date

<img width="450" alt="image" src="https://github.com/user-attachments/assets/c78604e7-d408-4f01-9f1f-f7677f5ae5eb" />

# MySQL Data Types
- String: char, text, binary, blob
- Numeric: integer, fixed-point, floating point, boolean
- Date: date, time, datetime

# MySQL String Data Types

Data Type|Description|Max Size|Use Case Example
---------|-----------|----------|----------------
CHAR(n) | Fixed-length string (right-padded with spaces) | 255 chars |country codes
VARCHAR(n) | Variable-length string | 64K bytes | names, emails, titles
TEXT | Large text data | by subtype | articles, comments, blog
BINARY(n) |Fixed-length binary data |255 bytes | Binary tokens, hashes
VARBINARY(n) | Variable-length binary data | 64K bytes | Compressed data
BLOB | Large binary data| by subtype | Images, files, multimedia
ENUM | A string object with a predefined set of possible values | 64K values | Status like ('pending', 'shipped')
SET | A string object that can store multiple predefined values (comma-separated)| 64 members | Tags like ("sports", "music","tech")


<details>
<summary><strong>中文表格</strong></summary>

| 資料型別      | 說明描述                                      | 最大容量      | 使用案例範例                 | 舉例值                       |
|---------------|-----------------------------------------------|---------------|------------------------------|------------------------------|
| `CHAR(n)`     | 固定長度字串（右側補空格）                     | 255 字元      | 國家代碼、固定長度編號       | `'TWN'`、`'A0001'`           |
| `VARCHAR(n)`  | 可變長度字串                                   | 約 64KB       | 姓名、電子郵件、標題         | `'王小明'`、`'test@mail.com'`|
| `TEXT`        | 大型文字數據                                   | 依子類型決定   | 文章、評論、部落格內容       | `'這是一篇心得分享……'`        |
| `BINARY(n)`   | 固定長度二進位數據                             | 255 位元組    | 二進位令牌、雜湊值           | `0x4F6B3A2C…`（16進位表示）  |
| `VARBINARY(n)`| 可變長度二進位數據                             | 約 64KB       | 壓縮數據、加密內容           | `0x8A3CFF21…`（16進位表示）  |
| `BLOB`        | 大型二進位數據                                 | 依子類型決定   | 圖片、檔案、多媒體           | JPG 圖片檔、PDF 文件等        |
| `ENUM`        | 預定義值的字串物件（單選）                     | 最多 64K 個值 | 狀態值（如 '待處理','已發貨'）| `'已發貨'`、`'處理中'`       |
| `SET`         | 可儲存多個預定義值的字串物件（逗號分隔）       | 最多 64 個成員| 標籤（如 "運動","科技"）     | `'運動,科技'`、`'音樂'`      |
</details>

<details>
	<summary><strong>CHAR vs VARCHAR vs integer</strong></summary>
	
| 項目               | `CHAR(n)`（固定長度字串）             | `VARCHAR(n)`（可變長度字串）              | `INTEGER`（整數）                         |
|--------------------|----------------------------------------|--------------------------------------------|-------------------------------------------|
| **資料型別**       | 字串                                   | 字串                                       | 整數                                       |
| **長度行為**       | 固定長度，不足會自動在右邊補空格       | 可變長度，依實際字元數儲存                 | 固定長度（4 bytes，儲存整數值）            |
| **儲存空間**       | 較大（即使字串短也會填補空白）         | 節省空間，僅儲存實際字串長度               | 固定 4 bytes，適用整數值範圍             |
| **存取效率**       | 較快（固定長度有利於索引）             | 較慢（長度不固定，需額外處理）            | 非常快，專門儲存數值                       |
| **適用情境**       | 固定格式字串（如國家代碼、身分證號）   | 長度不固定字串（如姓名、電子郵件）        | 整數數據（如年齡、數量、識別碼）         |
| **最大長度/範圍**  | 最多 255 字元                          | 最多 65,535 bytes（含行內其他欄位）        | -2,147,483,648 到 2,147,483,647            |
| **例子**           | `CHAR(2)`：'TW'、'US'、'JP'（固定2位） | `VARCHAR(50)`：'Alice'、'bob@example.com' | `INTEGER`：25、1001、123456               |

- 用 CHAR：當欄位內容長度固定且查詢頻繁，例如：國家代碼、性別代號、郵遞區號。
- 用 VARCHAR：當欄位內容長度不一，如：姓名、地址、電子郵件。
- 用 INTEGER：當儲存數值數據時，適用於年齡、數量、識別碼等數字型資料。
</details>
	
[List of MySQL Data Types](https://www.w3schools.com/mysql/mysql_datatypes.asp)

# MySQL Numeric Data Types - Integer

Data Type | Storage | Range | Example Use Case
----------|---------|-------|-----------------
TINYINT | 1 byte | -128 to 127 | Status flags (0 = off, 1 = on)
SMALLINT | 2 bytes | -32,768 to 32,767 | Age field
MEDIUMINT | 3 bytes | -8,388,608 to 8,388,607 | Moderate row IDs or counts
INT/INTEGER | 4 bytes | -2.1B to 2.1B | User IDs, product IDs
BIGINT | 8 bytes | -9.2 quintillion to -9.2 quintillion| Order numbers, financial records

---

### **1. TINYINT**  
- **儲存空間**：1 位元組（8 bits）  
- **數值範圍**：  
  - **有符號 (Signed)**：-128 ～ 127  
  - **無符號 (Unsigned)**：0 ～ 255  
- **使用案例**：  
  適用於儲存小範圍的狀態標記，例如：  
  - 開關狀態（0 = 關閉，1 = 開啟）  
  - 布林值替代（1 = 真，0 = 假）  

### **2. SMALLINT**  
- **儲存空間**：2 位元組（16 bits）  
- **數值範圍**：  
  - **有符號**：-32,768 ～ 32,767  
  - **無符號**：0 ～ 65,535  
- **使用案例**：  
  適合中等範圍的整數，例如：  
  - 年齡（0～120 歲）  
  - 小型計數器（如訂單數量）  

### **3. MEDIUMINT**  
- **儲存空間**：3 位元組（24 bits）  
- **數值範圍**：  
  - **有符號**：-8,388,608 ～ 8,388,607  
  - **無符號**：0 ～ 16,777,215  
- **使用案例**：  
  用於較大的 ID 或計數，但不需要用到 `INT` 的情況，例如：  
  - 中型資料表的流水號  
  - 網站每日訪問次數統計  

### **4. INT / INTEGER**  
- **儲存空間**：4 位元組（32 bits）  
- **數值範圍**：  
  - **有符號**：-2,147,483,648 ～ 2,147,483,647（約 ±21 億）  
  - **無符號**：0 ～ 4,294,967,295  
- **使用案例**：  
  最常用的整數型別，適用於：  
  - 用戶 ID、商品 ID  
  - 時間戳記（Unix Timestamp）  
  - 大多數業務邏輯的數字儲存  

### **5. BIGINT**  
- **儲存空間**：8 位元組（64 bits）  
- **數值範圍**：  
  - **有符號**：-9,223,372,036,854,775,808 ～ 9,223,372,036,854,775,807（約 ±922 京）  
  - **無符號**：0 ～ 18,446,744,073,709,551,615  
- **使用案例**：  
  用於極大範圍的數值，例如：  
  - 金融交易紀錄（避免溢位）  
  - 分散式系統的全域唯一 ID（如 Snowflake ID）  
  - 大型電商平台的訂單編號  


### **補充說明**  
1. **有符號 vs 無符號**：  
   - 若確定數值不會為負數，使用 `UNSIGNED` 可擴大正數範圍。  
   - 例如 `TINYINT UNSIGNED` 的範圍是 0～255（而非 -128～127）。  

2. **選擇原則**：  
   - 根據「預期數值範圍」選擇最小夠用的型別，可節省儲存空間並提升效能。  
   - 例如「年齡」用 `SMALLINT` 就足夠，沒必要用 `INT`。  

3. **資料庫差異**：  
   - 部分資料庫（如 MySQL、PostgreSQL）對這些型別的實現可能略有不同，需參考官方文件。  

# MySQL Numeric Data Types - Decimal Type

- Exact, stored as string-like binary, no precision loss
-  **精確儲存**：以類似字串的二進位格式儲存，不會有四捨五入或精度誤差的問題。這點對財務應用非常關鍵，例如不能讓 $0.01 的誤差累積。
- Slower for math operations
- **數學運算較慢**：因為不是直接以浮點數方式儲存，運算時需要額外轉換與處理，因此效能比不上 `FLOAT` 或 `DOUBLE`。
- DECIMAL(10, 2): 12345678.90
- **範例說明**：`DECIMAL(10, 2)` 代表這個數字可以最多有 10 位數，其中小數點後有 2 位，例如 `12345678.90` 是合法的，但 `123456789.01` 就會超出範圍。
- Financial data, money, tax, rates
- **使用場景**：特別適合處理**財務數據**，例如金額、稅率、利率等，這些場合都需要高精度、不能有誤差的計算。

Data Type | Description | Example
----------|-------------|------------------
DECIMAL(5,2) | 5 digits total, 2 after decimal precise | -999.99 ~ 999.99
NUMERIC(5,2) | Alias of DECIMAL

# MySQL Numeric Data Types - Floating-Point Type
- **Approximate, stored as binary float, can lose precision**  
  ⚠️ **近似值**：以二進位浮點數格式儲存，**無法保證每個數值都精確表示**，在某些位數後可能會有誤差，例如 `0.1 + 0.2 ≠ 0.3`。
- **Faster and uses less storage**  
  🚀 **速度快、佔用空間小**：由於硬體直接支援浮點運算，因此在需要大量數值運算時非常有效率，也比 `DECIMAL` 節省儲存空間。
- **DOUBLE -> 3.14159265358979**  
  🔍 **範例說明**：`DOUBLE` 可以表示非常長的浮點數，例如圓周率的多位數表示，但仍然是近似值而非精確儲存。
- **Scientific data, measurements**  
  🔬 **使用場景**：適合**科學計算、測量數據、感測器資料**等，不強求每一位數精確但需要浮點範圍大的情境。
 
Data Type | Storage | Example Use Case | Precision
----------|---------|------------------|----------
FLOAT | 4 bytes |  Weight: 12.34 | ~7 digits
DOUBLE | 8 bytes | GPS coordinates: 25.036793, 121.564558 | ~15 to 16 digits

<details>
	<summary><strong>decimal vs floating-point</strong></summary>
| 項目                         | `DECIMAL(p, s)`                      | `FLOAT` / `DOUBLE`（浮點數型別）                  |
|------------------------------|--------------------------------------|--------------------------------------------------|
| **精確度**                  | ✅ 精確儲存，無誤差                   | ❌ 近似值，可能出現精度誤差                       |
| **儲存方式**                | 類似字串的二進位格式                 | 二進位浮點格式                                    |
| **數學運算效率**            | 慢（需額外處理）                     | 快（硬體支援）                                   |
| **儲存空間**                | 較大                                 | 較小（FLOAT 約 4 bytes，DOUBLE 約 8 bytes）     |
| **適用場景**                | 財務數據（錢、稅、利率）             | 科學數據（測量值、感測器讀數、統計分析）         |
| **範例**                    | `DECIMAL(10, 2)` → `12345678.90`     | `DOUBLE` → `3.14159265358979`                    |
| **是否支援小數位控制**      | ✅ 可以指定精度與小數位              | ❌ 無法保證控制到第幾位小數                        |
| **ANSI SQL 標準支援**       | ✅ 標準明確支援                       | ✅ 標準支援但注意精度問題                         |
 
- **處理錢** → 用 `DECIMAL`（絕不能出錯）  
- **處理科學、統計、感測器資料** → 用 `FLOAT` / `DOUBLE`（需要速度與範圍）
</details>

# MySQL Numeric Data Types - Boolean Type
Data Type | Example Use Case
----------|----------------
BOOLEAN | TRUE or FALSE
BOOL | same as BOOLEAN

# MySQL Date and Time Data Types
Data Type | Format  | Example Value | Use Case
----------|---------|---------------|---------
DATE | YYYY-MM-DD | '2025-04-22' | birthdays
DATETIME | YYYY-MM-DD HH:MM:SS | '2025-04-22 13:45:00' | Exact date & time of an event
TIMESTAMP | YYYY-MM-DD HH:MM:SS | '2025-04-22 05:00:00' | Auto-tracking changes, auditing
TIME | HH:MM:SS | '14:30:00' | Duration, business hours
YEAR | YYYY | '2025' | product release year

| 資料型別（Data Type） | 格式（Format）            | 範例值（Example Value）     | 使用情境（Use Case）                   |
|------------------------|----------------------------|------------------------------|-----------------------------------------|
| `DATE`                 | `YYYY-MM-DD`               | `'2025-04-22'`               | 生日、日期欄位                          |
| `DATETIME`             | `YYYY-MM-DD HH:MM:SS`      | `'2025-04-22 13:45:00'`      | 活動的精確日期與時間                    |
| `TIMESTAMP`            | `YYYY-MM-DD HH:MM:SS`      | `'2025-04-22 05:00:00'`      | 自動紀錄變更時間、審核紀錄              |
| `TIME`                 | `HH:MM:SS`                 | `'14:30:00'`                 | 時段長度、營業時間                      |
| `YEAR`                 | `YYYY`                     | `'2025'`                     | 產品上市年份、年份欄位                  |

<details>
	<summary><strong>datetime vs timestamp</strong></summary>
	
| 項目             | `DATETIME`                            | `TIMESTAMP`                               |
|------------------|----------------------------------------|-------------------------------------------|
| **格式**         | `YYYY-MM-DD HH:MM:SS`                 | `YYYY-MM-DD HH:MM:SS`                     |
| **儲存方式**     | 絕對時間（與時區無關）               | 相對時間（會依據伺服器時區轉換）         |
| **範圍**         | `'1000-01-01 00:00:00'` ~ `'9999-12-31 23:59:59'` | `'1970-01-01 00:00:01'` ~ `'2038-01-19 03:14:07'`（Unix 時間範圍） |
| **是否受時區影響** | ❌ 不受影響                           | ✅ 儲存時會根據時區轉為 UTC，查詢時轉回 |
| **自動更新支援** | ❌ 不自動更新                         | ✅ 可設為 `DEFAULT CURRENT_TIMESTAMP` 或 `ON UPDATE` 自動更新 |
| **儲存空間**     | 8 bytes                               | 4 bytes（舊版）/ 7 bytes（新版）          |
| **適用情境**     | 儲存事件發生的絕對時間（如生日）      | 紀錄資料建立/修改時間、自動追蹤變更       |
</details>

# Steps to Develop Database
1. Design ER model (Fig 7.1 or Fig 8.1)
2. Create database 
3. Create database **schema** (a logical group of database objects, like tables and indexes)
4. Insert data

# Step1A: Analyze Biz Rules to Design ER Model
- A customer may generate many invoices. Each invoice is generated by one customer.
- An invoice contains one or more invoice lines. Each invoice line is associated with
one invoice.
- Each invoice line references one product. A product may be found in many invoice lines.
- A vendor may supply many products. Some vendors do not yet supply products.
- If a product is vendor-supplied, it is supplied by only a single vendor.
- Some products are not supplied by a vendor.

# Step1B: Deliver ER Diagram

<img width="450" alt="image" src="https://github.com/user-attachments/assets/a475f138-5404-41a1-964e-2fe43a4a9efb" />

# Step1C: Data Dictionary

<img width="464" alt="image" src="https://github.com/user-attachments/assets/335bf377-1eec-4a97-b21c-38d9585c1507" />

<details>
	<summary><strong>常見DDL指令</strong></summary>
| 指令        | 說明                                  | 範例                                           |
|-------------|----------------------------------------|------------------------------------------------|
| `CREATE`    | 建立資料庫、資料表、索引、檢視等      | `CREATE TABLE students (id INT, name VARCHAR(50));` |
| `ALTER`     | 修改現有的資料表（加欄位、改型別等）   | `ALTER TABLE students ADD email VARCHAR(100);`    |
| `DROP`      | 刪除資料表或資料庫                    | `DROP TABLE students;`                           |
| `TRUNCATE`  | 清空資料表內容，但保留表的結構         | `TRUNCATE TABLE students;`                       |
| `RENAME`    | 更改資料表名稱                        | `RENAME TABLE students TO learners;`            |
</details>
	


# Step2: Create Database (MySQL syntax) (DDL)
```sql
CREATE DATABASE [IF NOT EXISTS] database_name;
```
Database (schema) name: IIM_SALECO or EPPS_SALECO
```sql
CREATE DATABASE EPPS_SALECO;
CREATE DATABASE IF NOT EXISTS EPPS_SALECO;
USE EPPS_SALECO;
```
# Step3: Create Database Tables (MySQL syntax) (DDL)
```sql
CREATE TABLE [IF NOT EXISTS] table_name (
  column_name1 data_type [column_constraints],
  column_name2 data_type [column_constraints],
  ...
  [table_constraints]
);
```

# Create VENDOR Table
```sql
CREATE TABLE IF NOT EXISTS VENDOR (
  V_CODE INT,
  V_NAME VARCHAR(35) NOT NULL,
  V_CONTACT VARCHAR(25) NOT NULL,
  V_AREACODE CHAR(3) NOT NULL,
  V_PHONE CHAR(8) NOT NULL,
  V_STATE CHAR(2) NOT NULL,
  V_ORDER CHAR(1) NOT NULL,
  PRIMARY KEY (V_CODE)
);
```

# Create PRODUCT Table
```sql
CREATE TABLE IF NOT EXISTS PRODUCT (
  P_CODE VARCHAR(10),
  P_DESCRIPT VARCHAR(35) NOT NULL,
  P_INDATE DATE NOT NULL,
  P_QOH SMALLINT NOT NULL,
  P_MIN SMALLINT NOT NULL,
  P_PRICE DECIMAL(8,2) NOT NULL,
  P_DISCOUNT DECIMAL(5,2) NOT NULL,
  V_CODE INT,
  PRIMARY KEY (P_CODE),
  FOREIGN KEY (V_CODE) REFERENCES VENDOR (V_CODE)
);
```
# Create CUSTOMER Table
```sql
CREATE TABLE CUSTOMER (
  CUS_CODE	INTEGER,
  CUS_LNAME	VARCHAR(15) NOT NULL,
  CUS_FNAME	VARCHAR(15) NOT NULL,
  CUS_INITIAL	CHAR(1),
  CUS_AREACODE 	CHAR(3),
  CUS_PHONE	CHAR(8) NOT NULL,
  CUS_BALANCE	NUMERIC(9,2) DEFAULT 0.00,
  PRIMARY KEY (CUS_CODE),
  CONSTRAINT CUS_UI1 UNIQUE(CUS_LNAME,CUS_FNAME, CUS_PHONE));
```

# Create INVOICE Table
```sql
CREATE TABLE IF NOT EXISTS INVOICE (
  INV_NUMBER  INTEGER,
  CUS_CODE	INTEGER NOT NULL,
  INV_DATE  DATE NOT NULL,
  PRIMARY KEY (INV_NUMBER),
  FOREIGN KEY (CUS_CODE) REFERENCES CUSTOMER (CUS_CODE), 
  CONSTRAINT INV_CK1 CHECK (INV_DATE > '2012-01-01'));
```
# Create LINE Table
```sql
CREATE TABLE LINE (
  INV_NUMBER 	INTEGER NOT NULL,
  LINE_NUMBER	NUMERIC(2,0) NOT NULL,
  P_CODE		VARCHAR(10) NOT NULL,
  LINE_UNITS	NUMERIC(9,2) DEFAULT 0.00 NOT NULL,
  LINE_PRICE	NUMERIC(9,2) DEFAULT 0.00 NOT NULL,
  PRIMARY KEY (INV_NUMBER,LINE_NUMBER),
  FOREIGN KEY (INV_NUMBER) REFERENCES INVOICE (INV_NUMBER) ON DELETE CASCADE,
  FOREIGN KEY (P_CODE) REFERENCES PRODUCT(P_CODE),
  CONSTRAINT LINE_UI1 UNIQUE(INV_NUMBER, P_CODE));
```


# STEP4: Insert Data (MySQL Syntax) (DML)
```sql
/* basic syntax */
INSERT INTO table_name (column1, column2, ..., columnN)
VALUES (value1, value2, ..., valueN);

/* insert multiple rows */
INSERT INTO table_name (column1, column2)
VALUES 
  (value1a, value2a),
  (value1b, value2b),
  (value1c, value2c);

/* insert without specifying columns (must match column order) */
INSERT INTO table_name
VALUES (value1, value2, ..., valueN);
```

# Insert Into VENDOR Table
```sql
INSERT INTO VENDOR VALUES(21225,'Bryson, Inc.'    ,'Smithson','615','223-3234','TN','Y');
INSERT INTO VENDOR VALUES(21226,'SuperLoo, Inc.'  ,'Flushing','904','215-8995','FL','N');
INSERT INTO VENDOR VALUES(21231,'D&E Supply'      ,'Singh'   ,'615','228-3245','TN','Y');
INSERT INTO VENDOR VALUES(21344,'Gomez Bros.'     ,'Ortega'  ,'615','889-2546','KY','N');
INSERT INTO VENDOR VALUES(22567,'Dome Supply'     ,'Smith'   ,'901','678-1419','GA','N');
INSERT INTO VENDOR VALUES(23119,'Randsets Ltd.'   ,'Anderson','901','678-3998','GA','Y');
INSERT INTO VENDOR VALUES(24004,'Brackman Bros.'  ,'Browning','615','228-1410','TN','N');
INSERT INTO VENDOR VALUES(24288,'ORDVA, Inc.'     ,'Hakford' ,'615','898-1234','TN','Y');
INSERT INTO VENDOR VALUES(25443,'B&K, Inc.'       ,'Smith'   ,'904','227-0093','FL','N');
INSERT INTO VENDOR VALUES(25501,'Damal Supplies'  ,'Smythe'  ,'615','890-3529','TN','N');
INSERT INTO VENDOR VALUES(25595,'Rubicon Systems' ,'Orton'   ,'904','456-0092','FL','Y');
```  

# Insert Into PRODUCT table
```sql
INSERT INTO PRODUCT VALUES('11QER/31','Power painter, 15 psi., 3-nozzle'     ,'2021-11-03',  8,  5,109.99,0.00,25595);
INSERT INTO PRODUCT VALUES('13-Q2/P2','7.25-in. pwr. saw blade'              ,'2021-12-13', 32, 15, 14.99,0.05,21344);
INSERT INTO PRODUCT VALUES('14-Q1/L3','9.00-in. pwr. saw blade'              ,'2021-11-13', 18, 12, 17.49,0.00,21344);
INSERT INTO PRODUCT VALUES('1546-QQ2','Hrd. cloth, 1/4-in., 2x50'            ,'2022-01-15', 15,  8, 39.95,0.00,23119);
INSERT INTO PRODUCT VALUES('1558-QW1','Hrd. cloth, 1/2-in., 3x50'            ,'2022-01-15', 23,  5, 43.99,0.00,23119);
INSERT INTO PRODUCT VALUES('2232/QTY','B&D jigsaw, 12-in. blade'             ,'2021-12-30',  8,  5,109.92,0.05,24288);
INSERT INTO PRODUCT VALUES('2232/QWE','B&D jigsaw, 8-in. blade'              ,'2021-12-24',  6,  5, 99.87,0.05,24288);
INSERT INTO PRODUCT VALUES('2238/QPD','B&D cordless drill, 1/2-in.'          ,'2022-01-20', 12,  5, 38.95,0.05,25595);
INSERT INTO PRODUCT VALUES('23109-HB','Claw hammer'                          ,'2022-01-20', 23, 10,  9.95,0.10,21225);
INSERT INTO PRODUCT VALUES('23114-AA','Sledge hammer, 12 lb.'                ,'2022-01-02',  8,  5, 14.40,0.05,NULL);
INSERT INTO PRODUCT VALUES('54778-2T','Rat-tail file, 1/8-in. fine'          ,'2021-12-15', 43, 20,  4.99,0.00,21344);
INSERT INTO PRODUCT VALUES('89-WRE-Q','Hicut chain saw, 16 in.'              ,'2022-02-07', 11,  5,256.99,0.05,24288);
INSERT INTO PRODUCT VALUES('PVC23DRT','PVC pipe, 3.5-in., 8-ft'              ,'2022-02-20',188, 75,  5.87,0.00,NULL);
INSERT INTO PRODUCT VALUES('SM-18277','1.25-in. metal screw, 25'             ,'2022-03-01',172, 75,  6.99,0.00,21225);
INSERT INTO PRODUCT VALUES('SW-23116','2.5-in. wd. screw, 50'                ,'2022-02-24',237,100,  8.45,0.00,21231);
INSERT INTO PRODUCT VALUES('WR3/TT3' ,'Steel matting, 4''x8''x1/6", .5" mesh','2022-01-17', 18,  5,119.95,0.10,25595);
```

# Insert Into CUSTOMER Table
```sql
/* CUSTOMER rows					*/
INSERT INTO CUSTOMER VALUES(10010,'Ramas'   ,'Alfred','A' ,'615','844-2573',0);
INSERT INTO CUSTOMER VALUES(10011,'Dunne'   ,'Leona' ,'K' ,'713','894-1238',0);
INSERT INTO CUSTOMER VALUES(10012,'Smith'   ,'Kathy' ,'W' ,'615','894-2285',345.86);
INSERT INTO CUSTOMER VALUES(10013,'Olowski' ,'Paul'  ,'F' ,'615','894-2180',536.75);
INSERT INTO CUSTOMER VALUES(10014,'Orlando' ,'Myron' ,NULL,'615','222-1672',0);
INSERT INTO CUSTOMER VALUES(10015,'O''Brian','Amy'   ,'B' ,'713','442-3381',0);
INSERT INTO CUSTOMER VALUES(10016,'Brown'   ,'James' ,'G' ,'615','297-1228',221.19);
INSERT INTO CUSTOMER VALUES(10017,'Williams','George',NULL,'615','290-2556',768.93);
INSERT INTO CUSTOMER VALUES(10018,'Farriss' ,'Anne'  ,'G' ,'713','382-7185',216.55);
INSERT INTO CUSTOMER VALUES(10019,'Smith'   ,'Olette','K' ,'615','297-3809',0);
```

# Insert Into INVOICE Table
```sql
INSERT INTO INVOICE VALUES(1001,10014,'2022-01-16');
INSERT INTO INVOICE VALUES(1002,10011,'2022-01-16');
INSERT INTO INVOICE VALUES(1003,10012,'2022-01-16');
INSERT INTO INVOICE VALUES(1004,10011,'2022-01-17');
INSERT INTO INVOICE VALUES(1005,10018,'2022-01-17');
INSERT INTO INVOICE VALUES(1006,10014,'2022-01-17');
INSERT INTO INVOICE VALUES(1007,10015,'2022-01-17');
INSERT INTO INVOICE VALUES(1008,10011,'2022-01-17');
```

# Insert Into LINE Table
```sql
INSERT INTO LINE VALUES(1001,1,'13-Q2/P2',1,14.99);
INSERT INTO LINE VALUES(1001,2,'23109-HB',1,9.95);
INSERT INTO LINE VALUES(1002,1,'54778-2T',2,4.99);
INSERT INTO LINE VALUES(1003,1,'2238/QPD',1,38.95);
INSERT INTO LINE VALUES(1003,2,'1546-QQ2',1,39.95);
INSERT INTO LINE VALUES(1003,3,'13-Q2/P2',5,14.99);
INSERT INTO LINE VALUES(1004,1,'54778-2T',3,4.99);
INSERT INTO LINE VALUES(1004,2,'23109-HB',2,9.95);
INSERT INTO LINE VALUES(1005,1,'PVC23DRT',12,5.87);
INSERT INTO LINE VALUES(1006,1,'SM-18277',3,6.99);
INSERT INTO LINE VALUES(1006,2,'2232/QTY',1,109.92);
INSERT INTO LINE VALUES(1006,3,'23109-HB',1,9.95);
INSERT INTO LINE VALUES(1006,4,'89-WRE-Q',1,256.99);
INSERT INTO LINE VALUES(1007,1,'13-Q2/P2',2,14.99);
INSERT INTO LINE VALUES(1007,2,'54778-2T',1,4.99);
INSERT INTO LINE VALUES(1008,1,'PVC23DRT',5,5.87);
INSERT INTO LINE VALUES(1008,2,'WR3/TT3',3,119.95);
INSERT INTO LINE VALUES(1008,3,'23109-HB',1,9.95);
```

# Data in Database
![bg right:70% w:90%](restricted/CFig08_02.jpg)

# Basic SELECT Syntax (DML)
```sql
SELECT column1, column2, ...
FROM table_name
[WHERE condition]
[GROUP BY column]
[HAVING condition]
[ORDER BY column [ASC|DESC]]
[LIMIT number OFFSET offset];
```

# A Complete SELECT Statement
```sql
SELECT department, COUNT(*) AS employee_count, AVG(salary) AS avg_salary
FROM employees
WHERE status = 'active'
GROUP BY department
HAVING AVG(salary) > 50000
ORDER BY avg_salary DESC
LIMIT 5 OFFSET 10;
```

# Explanation of SELECT Statement

Clause|Purpose|Explanation
------|-------|-----------
SELECT department, COUNT(*), AVG(salary) | Columns to retrieve | Selects the department, number of employees, and average salary
FROM employees | Table source | Uses the employees table
WHERE status = 'active' | Filter rows | Only include employees who are currently active
GROUP BY department | Grouping | Groups rows by department
HAVING AVG(salary) > 50000 | Group filter | Only show departments where the average salary is above 50,000
ORDER BY avg_salary DESC | Sort | Sorts the result by average salary in descending order
LIMIT 5 OFFSET 10 | Pagination | Skips the first 10 rows and returns the next 5

# SELECT Clause
- SELECT – specifies the attributes to be returned (column name or *)
- FROM – specifies the table(s)
- WHERE – filters the rows of data
- GROUP BY – groups the rows of data into collections based on columns
- HAVING – filters the groups formed by GROUP BY clause
- ORDER BY – sorts the final query result rows in ascending or descending order by columns

# Select an Entire PRODUCT Table
```sql
SELECT * 
FROM EPPS_SALECO.PRODUCT;

USE EPPS_SALECO;
SELECT * 
FROM PRODUCT;
```

# Select with a Column List
```sql
SELECT P_CODE, P_DESCRIPT, P_PRICE, P_QOH 
FROM EPPS_SALECO.PRODUCT;
```

# Using Column Aliases
```sql
SELECT P_CODE, P_DESCRIPT AS DESCRIPTION, P_PRICE AS "UNIT PRICE", P_QOH AS QTY  
FROM PRODUCT;
```

# Using Computed Columns
```sql
SELECT P_DESCRIPT AS DESCRIPTION, P_PRICE AS "UNIT PRICE", P_QOH AS QTY, P_QOH * P_PRICE AS "TOTAL VALUE"  
FROM PRODUCT;
```
# Numeric Calculation
```sql
SELECT 
P_PRICE as ORG_PRICE,
P_DISCOUNT as DISCOUNT,
P_PRICE * (1 - P_DISCOUNT) as PROD_PRICE 
FROM PRODUCT;
```

# Date Arithmetic
```sql
SELECT NOW() + INTERVAL 7 DAY;
SELECT CURDATE() - INTERVAL 1 MONTH;
SELECT '2025-04-01' + INTERVAL 1 DAY;
```

# Listing Unique Values
```sql
SELECT DISTINCT V_CODE
FROM PRODUCT;
```

# FROM Clause Options
- The FROM clause specifies table(s) which is involved
- Only columns in tables in FROM clause are available throughout the rest of the query
- Multiple tables must be combined using a type of JOIN operation

# ORDER BY Clause Options

```sql
SELECT 	columnlist
FROM 		tablelist
[ORDER BY	columnlist [ASC|DESC] ];
```  
```sql
SELECT P_CODE, P_DESCRIPT, P_QOH, P_PRICE
FROM PRODUCT
ORDER BY P_PRICE;
```
```sql
SELECT P_CODE, P_DESCRIPT, P_QOH, P_PRICE
FROM PRODUCT
ORDER BY P_PRICE DESC;
```
```sql
SELECT EMP_LNAME, EMP_FNAME, EMP_INITIAL, EMP_PHONE
FROM EMPLOYEE
ORDER BY EMP_LNAME, EMP_FNAME, EMP_INITIAL;
```

# WHERE Clause Options
- Comparison operator: =, <, <=, >, >=, <> or !=
```sql
SELECT columnlist
FROM tablelist
[WHERE conditionlist ];
```

# Using Comparison Operator on Numeric Attribute 
```sql
SELECT P_DESCRIPT, P_INDATE, P_PRICE, V_CODE
FROM PRODUCT
WHERE V_CODE = 21344;

SELECT P_DESCRIPT, P_QOH, P_MIN, P_PRICE
FROM PRODUCT
WHERE P_PRICE <= 10;
```

# Using Comparison Operator on Character Attribute  
```sql
SELECT P_CODE, P_DESCRIPT, P_QOH, P_MIN, P_PRICE
FROM PRODUCT
WHERE P_CODE < '1558-QW1';
```
# Using Comparison Operator on Date Attribute  
```sql
SELECT P_DESCRIPT, P_QOH, P_MIN, P_PRICE, P_INDATE
FROM PRODUCT
WHERE P_INDATE >= '2021-11-05';
```
# Logical Operators: AND, OR and NOT
```sql
SELECT P_DESCRIPT, P_INDATE, P_PRICE, V_CODE
FROM PRODUCT
WHERE P_PRICE < 50 AND P_INDATE > '2021-01-01';

/* use parentheses and compare below two select statements */
SELECT P_DESCRIPT, P_PRICE, V_CODE
FROM PRODUCT
WHERE (V_CODE = 25595 OR V_CODE = 24288) AND P_PRICE > 100;

SELECT P_DESCRIPT, P_PRICE, V_CODE
FROM PRODUCT
WHERE V_CODE = 25595 OR V_CODE = 24288 AND P_PRICE > 100;
-- AND before OR --

SELECT *
FROM PRODUCT
WHERE NOT (V_CODE = 21344);
``` 

# Special Operators in WHERE Clause
- BETWEEN – Used to check whether an attribute value is within a range
- IN – Used to check whether an attribute value matches any value within a value list
- LIKE – Used to check whether an attribute value matches a given string pattern
- IS NULL – Used to check whether an attribute value is null
- NOT – Used to negate a condition

# Illustrations of Special Operators
```sql
SELECT * FROM PRODUCT
WHERE P_PRICE BETWEEN 50.00 AND 100.00;

SELECT * FROM PRODUCT
WHERE V_CODE IN (21344, 24288);

SELECT V_NAME, V_CONTACT, V_AREACODE, V_PHONE FROM VENDOR
WHERE V_CONTACT LIKE 'Smith%';

/* wildcard % for zero or more chars, _ for any one char */
SELECT P_CODE, P_DESCRIPT, V_CODE FROM PRODUCT
WHERE V_CODE IS NULL;

SELECT V_NAME, V_CONTACT, V_AREACODE, V_PHONE FROM VENDOR
WHERE UPPER(V_CONTACT) NOT LIKE 'SMITH%';
```

# Use Wildcard in Expression
A wildcard character is a symbol that can be used as a general substitute for other characters or commands
  - \* : all columns
  - % : matches zero or more characters
  - _ : matches exactly one character

```sql
SELECT * FROM PRODUCT WHERE P_CODE LIKE '15%';
SELECT * FROM PRODUCT WHERE P_CODE LIKE '2232/Q__';
```

# MySQL Comparison Operators
Symbol or keyword(s) | Description
---------------------|-------------
=, !=, <> | Equal, Not equal
\>, >=, <, <= | Great / Less than or equal to
is null, is not null | check null or not
between and, not between and | within a range
in, not in | match a value in a list
like, not like | match a pattern

# MySQL Booleans or Conditions
Conditions: not, and, or
Booleans
```sql
create table bachelor (name	varchar(100), employed_flag bool);
	
insert into bachelor(name, employed_flag)
values ('Hector Handsome', true),('Frank Freeloader', false);
select * from bachelor where employed_flag is true;
select * from bachelor where employed_flag;
select * from bachelor where employed_flag = true;
select * from bachelor where employed_flag != false;
select * from bachelor where employed_flag = 1;
select * from bachelor where employed_flag != 0;
```

# JOIN Operations
JOIN operators are used to combine data from multiple tables
- Inner joins return only rows from the tables that match on a common value
- Outer joins return the same matched rows as the inner join, plus unmatched rows from one table or the other
  - Left (outer) join
  - Right (outer) join
  - Full (outer) join

# JOIN Illustration
<div class="grid">
    <img src="files/image/four_join_types.jpg" alt="">
    <img src="files/image/join_example.jpg" alt="">
</div>

# Three Ways to Do Inner Join (Join)
```sql
-- JOIN USING
SELECT column-list FROM table1 JOIN table2 USING (common-column)

-- JOIN ON
SELECT column-list FROM table1 JOIN table2 ON join-condition

-- Old-style JOIN
SELECT column-list FROM table1, table2 WHERE table1.column = table2.column
```
- In practice, **JOIN ON** is typically considered as a preference.

# Example of JOIN USING
```sql
SELECT P_CODE, P_DESCRIPT, V_CODE, V_NAME, V_AREACODE, V_PHONE
FROM PRODUCT JOIN VENDOR USING (V_CODE);
```
# Example of JOIN ON
```sql
SELECT INVOICE.INV_NUMBER, PRODUCT.P_CODE, P_DESCRIPT, LINE_UNITS, LINE_PRICE
FROM INVOICE
JOIN LINE ON INVOICE.INV_NUMBER = LINE.INV_NUMBER 
JOIN PRODUCT ON LINE.P_CODE = PRODUCT.P_CODE;

-- Compare to JOIN ON
SELECT INV_NUMBER, P_CODE, P_DESCRIPT, LINE_UNITS, LINE_PRICE
FROM INVOICE 
JOIN LINE USING(INV_NUMBER) 
JOIN PRODUCT USING(P_CODE);
```

# Example of Old-Style JOIN
```sql
SELECT P_CODE, P_DESCRIPT, P_PRICE, V_NAME
FROM PRODUCT, VENDOR
WHERE PRODUCT.V_CODE = VENDOR.V_CODE;

-- Compare to JOIN USING
SELECT P_CODE, P_DESCRIPT, P_PRICE, V_NAME
FROM PRODUCT JOIN VENDOR USING(V_CODE);

-- Compare to JOIN ON
SELECT P_CODE, P_DESCRIPT, P_PRICE, V_NAME
FROM PRODUCT JOIN VENDOR ON PRODUCT.V_CODE = VENDOR.V_CODE;
```
- The task of joining the tables is split across both the FROM and WHERE which makes complex queries more difficult to maintain
- They are susceptible to undetected errors

# Illustrate Why Old-Style Join is Not Preferred
```sql
-- Get wrong result and easy to find no condition when join PRODUCT
SELECT CUS_FNAME, CUS_LNAME, V_NAME
FROM CUSTOMER
JOIN INVOICE ON CUSTOMER.CUS_CODE = INVOICE.CUS_CODE
JOIN LINE ON INVOICE.INV_NUMBER = LINE.INV_NUMBER
JOIN PRODUCT
JOIN VENDOR ON PRODUCT.V_CODE = VENDOR.V_CODE
WHERE V_STATE = 'TN';

-- Get wrong result and hard to debug
SELECT CUS_FNAME, CUS_LNAME, V_NAME
FROM CUSTOMER, INVOICE, LINE, PRODUCT, VENDOR
WHERE V_STATE = 'TN' 
AND CUSTOMER.CUS_CODE = INVOICE.CUS_CODE 
AND INVOICE.INV_NUMBER = LINE.INV_NUMBER
AND PRODUCT.V_CODE = VENDOR.V_CODE;
```

# Outer Joins
Three types of outer join: Left (outer) join, Right (outer) join, Full (outer) join

# Left Outer Join
```sql
SELECT column-list
FROM table1 LEFT[OUTER] JOIN table2 ON join-condition

SELECT P_CODE, VENDOR.V_CODE, V_NAME
FROM VENDOR 
LEFT JOIN PRODUCT ON VENDOR.V_CODE = PRODUCT.V_CODE;
```

# Right Outer Join
```sql
SELECT column-list
FROM table1 RIGHT[OUTER] JOIN table2 ON join-condition

SELECT P_CODE, VENDOR.V_CODE, V_NAME
FROM VENDOR 
RIGHT JOIN PRODUCT ON VENDOR.V_CODE = PRODUCT.V_CODE;

SELECT VENDOR.V_CODE, V_NAME, P_CODE
FROM PRODUCT 
RIGHT JOIN VENDOR ON PRODUCT.V_CODE = VENDOR.V_CODE
WHERE P_CODE IS NULL;
```

# Full Outer Join (Not Support in MySQL)
```sql
SELECT column-list
FROM table1 FULL[OUTER] JOIN table2 ON join-condition

SELECT P_CODE, VENDOR.V_CODE, V_NAME
FROM VENDOR
FULL JOIN PRODUCT ON VENDOR.V_CODE = PRODUCT.V_CODE;
```
<div class="middle-grid">
    <img src="restricted/CFig07_33.jpg" alt="">
</div>

# Cross Join
- A cross join performs a relational product (also known as the Cartesian product) of two tables.
- Despite the name, CROSS JOIN is not truly a join operation because it does not unite the rows of the tables based on a common attribute.
```sql
SELECT column-list FROM table1 CROSS JOIN table2

SELECT * FROM INVOICE CROSS JOIN LINE;
```

# JOINs in MySQL
![bg right:70% w:90%](files/image/mysql_join.jpg)

# Joining Tables with an Alias
Using a table alias allows the database programmer to improve the maintainability

```sql
SELECT P_DESCRIPT, P_PRICE, V_NAME, V_CONTACT, V_AREACODE, V_PHONE
FROM
PRODUCT P 
JOIN VENDOR V ON P.V_CODE = V.V_CODE;
```

# Recursive Joins
A query that joins a table to itself
```sql
SELECT E.EMP_NUM, E.EMP_LNAME, E.EMP_MGR, M.EMP_LNAME
FROM EMP E
JOIN EMP M ON E.EMP_MGR = M.EMP_NUM;
```

# Aggregate Processing
SQL provides useful aggregate functions that count, find minimum and maximum values, calculate averages, etc.
- Count
- MIN and MAX
- SUM and AVG

# Count
```sql
SELECT COUNT(P_CODE)
FROM PRODUCT;

SELECT COUNT(P_PRICE)
FROM PRODUCT
WHERE P_PRICE < 10;

-- count how many V_CODE in PRODUCT which is not NULL
SELECT COUNT(V_CODE)
FROM PRODUCT;

-- count how many rows in the table
SELECT COUNT(*)
FROM PRODUCT;

SELECT COUNT(DISTINCT V_CODE) AS "COUNT DISTINCT"
FROM PRODUCT;
```
# MIN and MAX
The MIN and MAX functions help you find answers to problems such as the highest and lowest (maximum and minimum) prices in the PRODUCT table.
```sql
SELECT MAX(P_PRICE) AS MAXPRICE, MIN(P_PRICE) as MINPRICE
FROM PRODUCT;
```

# SUM and AVG
```sql
SELECT SUM(CUS_BALANCE) AS TOTAL_BALANCE
FROM CUSTOMER;

SELECT SUM(P_QOH * P_PRICE) as TOTAL_VALUE
FROM PRODUCT;

SELECT AVG(P_PRICE) AS AVG_PRICE
FROM PRODUCT;
```
# Grouping Data (1)
```sql
SELECT columnlist
FROM tablelist
[WHERE conditionlist]
[GROUP BY columnlist]
[ORDER BY columnlist [ASC|DESC]];

SELECT V_CODE, AVG(P_PRICE) AS AVG_PRICE
FROM PRODUCT
GROUP BY V_CODE;

SELECT VENDOR.V_CODE, V_NAME, COUNT(P_CODE) AS NUMPRODS, AVG(P_PRICE) AS AVGPRICE
FROM PRODUCT JOIN VENDOR ON PRODUCT.V_CODE = VENDOR.V_CODE
GROUP BY V_CODE
ORDER BY V_NAME;
```

# Grouping Data (2)
```sql
-- Get execution error
SELECT VENDOR.V_CODE, V_NAME, P_QOH, COUNT(P_CODE) AS NUMPRODS, AVG(P_PRICE) AS AVGPRICE
FROM PRODUCT JOIN VENDOR ON PRODUCT.V_CODE = VENDOR.V_CODE
GROUP BY V_CODE
ORDER BY V_NAME;

-- Fixed 1: sum of P_QOH
SELECT VENDOR.V_CODE, V_NAME, SUM(P_QOH), COUNT(P_CODE) AS NUMPRODS, AVG(P_PRICE) AS AVGPRICE
FROM PRODUCT JOIN VENDOR ON PRODUCT.V_CODE = VENDOR.V_CODE
GROUP BY V_CODE
ORDER BY V_NAME;

-- Fixed 2: put P_QOH into group by
SELECT VENDOR.V_CODE, V_NAME, P_QOH, COUNT(P_CODE) AS NUMPRODS, AVG(P_PRICE) AS AVGPRICE
FROM PRODUCT JOIN VENDOR ON PRODUCT.V_CODE = VENDOR.V_CODE
GROUP BY V_CODE, P_QOH
ORDER BY V_NAME;
```

# HAVING Clause
```sql
SELECT columnlist FROM tablelist
[WHERE conditionlist]
[GROUP BY columnlist]
[HAVING conditionlist]
[ORDER BY columnlist [ASC|DESC]];

SELECT V_CODE, COUNT(P_CODE) AS NUMPRODS
FROM PRODUCT
GROUP BY V_CODE
HAVING AVG(P_PRICE) < 10
ORDER BY V_CODE;

SELECT P.V_CODE, V_NAME, SUM(P_QOH * P_PRICE) AS TOTCOST
FROM PRODUCT P JOIN VENDOR V ON P.V_CODE = V.V_CODE
WHERE P_DISCOUNT > 0
GROUP BY V_CODE, V_NAME
HAVING (SUM(P_QOH * P_PRICE) > 500)
ORDER BY SUM(P_QOH * P_PRICE) DESC;
```

# Subqueries
We want to generate a list of vendors who do not provide products.
```sql
-- Right outer join
SELECT VENDOR.V_CODE, V_NAME 
FROM PRODUCT
RIGHT JOIN VENDOR ON PRODUCT.V_CODE = VENDOR.V_CODE
WHERE P_CODE IS NULL;

-- Subquery
SELECT V_CODE, V_NAME
FROM VENDOR
WHERE V_CODE NOT IN (
    SELECT V_CODE FROM PRODUCT WHERE V_CODE IS NOT NULL);
```

# WHERE Subqueries
```sql
-- List all customers who order a claw hammer
SELECT P_CODE, P_PRICE
FROM PRODUCT
WHERE P_PRICE >= 
    (SELECT AVG(P_PRICE) FROM PRODUCT);

SELECT DISTINCT CUS_CODE, CUS_LNAME, CUS_FNAME
FROM CUSTOMER
JOIN INVOICE USING (CUS_CODE)
JOIN LINE USING (INV_NUMBER)
JOIN PRODUCT USING (P_CODE)
WHERE P_CODE = (
    SELECT P_CODE
    FROM PRODUCT
    WHERE P_DESCRIPT = 'Claw hammer');

SELECT DISTINCT CUSTOMER.CUS_CODE, CUS_LNAME, CUS_FNAME
FROM CUSTOMER
JOIN INVOICE ON CUSTOMER.CUS_CODE = INVOICE.CUS_CODE
JOIN LINE ON INVOICE.INV_NUMBER = LINE.INV_NUMBER
JOIN PRODUCT ON PRODUCT.P_CODE = LINE.P_CODE
WHERE P_DESCRIPT = 'Claw hammer';    
```

# IN Subqueries
List all customers who have purchased hammers, saws, or saw blades.
```sql
SELECT DISTINCT CUSTOMER.CUS_CODE, CUS_LNAME, CUS_FNAME
FROM CUSTOMER
JOIN INVOICE ON CUSTOMER.CUS_CODE = INVOICE.CUS_CODE
JOIN LINE ON INVOICE.INV_NUMBER = LINE.INV_NUMBER
JOIN PRODUCT ON LINE.P_CODE = PRODUCT.P_CODE
WHERE PRODUCT.P_CODE IN
  (SELECT P_CODE 
   FROM PRODUCT
   WHERE P_DESCRIPT LIKE '%hammer%' OR P_DESCRIPT LIKE '%saw%');
```

# HAVING Subqueries
List all products with a total quantity sold greater than the average quantity sold
```sql
SELECT P_CODE, SUM(LINE_UNITS) AS TOTALUNITS
FROM LINE
GROUP BY P_CODE
HAVING SUM(LINE_UNITS) > (SELECT AVG(LINE_UNITS) FROM LINE);
```

# Multirow Subquery Operators: ALL and any
Which products cost more than all individual products provided by vendors from Florida
```sql
SELECT P_CODE, P_QOH * P_PRICE AS TOTALVALUE
FROM PRODUCT
WHERE P_QOH * P_PRICE > 
    ALL (SELECT P_QOH * P_PRICE
         FROM PRODUCT
         WHERE V_CODE IN 
         (SELECT V_CODE
          FROM VENDOR 
          WHERE V_STATE = 'FL'));
```

- <span class="small-text"> Greater than ALL" is equivalent to "greater than the highest product cost of the list </span>
- <span class="small-text"> ANY operator to compare a single value to a list of values and select only the rows for which the inventory cost is greater than any value in the list</span>
- <span class="small-text"> Use the equal to ANY operator, which would be the equivalent of the IN operator.</span>

# FROM Subqueries
List all customers who purchased both products ('13-Q2/P2', '23109-HB'), not just one.
```sql
SELECT DISTINCT CUSTOMER.CUS_CODE, CUSTOMER.CUS_LNAME
FROM CUSTOMER
JOIN
    (SELECT INVOICE.CUS_CODE
     FROM INVOICE
     JOIN LINE ON INVOICE.INV_NUMBER = LINE.INV_NUMBER
     WHERE P_CODE = '13-Q2/P2') CP1
ON CUSTOMER.CUS_CODE = CP1.CUS_CODE
JOIN
    (SELECT INVOICE.CUS_CODE
     FROM INVOICE
     JOIN LINE ON INVOICE.INV_NUMBER = LINE.INV_NUMBER
     WHERE P_CODE = '23109-HB') CP2
ON CP1.CUS_CODE = CP2.CUS_CODE;
```

# Attribute List Subqueries (1)
List the difference between each product's price and the average product price
```sql
SELECT 
  P_CODE, P_PRICE,
  (SELECT AVG(P_PRICE) FROM PRODUCT) AS AVGPRICE,
  P_PRICE - (SELECT AVG(P_PRICE) FROM PRODUCT) AS DIFF
FROM PRODUCT;
```

# Attribute List Subqueries (2)
List the product code, the total sales by product, and the contribution by employee of each product's sales.
```sql
SELECT
P_CODE, 
SUM(LINE_UNITS * LINE_PRICE) AS SALES,
(SELECT COUNT(*) FROM EMPLOYEE) AS ECOUNT,
SUM(LINE_UNITS * LINE_PRICE)/(SELECT COUNT(*) FROM EMPLOYEE) AS CONTRIB
FROM LINE
GROUP BY P_CODE;

SELECT P_CODE, SALES, ECOUNT, SALES/ECOUNT AS CONTRIB
FROM (SELECT P_CODE, 
             SUM(LINE_UNITS * LINE_PRICE) AS SALES,
             (SELECT COUNT(*) FROM EMPLOYEE) AS ECOUNT 
      FROM LINE
      GROUP BY P_CODE) AS T;
```

# Correlated Subqueries (Definition)
- <span class="blue-text">Inner subquery</span>
  - Inner subqueries execute independently. 
  - The inner sub-query executes first; its **output** is used by the outer query, which then executes until the
last outer query finishes (the first SQL statement in the code).
- <span class="blue-text">Correalted subquery</span>
  -  A subquery that executes once for each row in the outer query.
  -  The inner query is related to the outer query
  -  The inner query references a column of the outer subquery.
  1. It initiates the outer query.
  2. For each row of the outer query result set, it executes the inner query by passing the outer row to the inner query.

# Correlated Subqueries (Example)
List all product sales in which the units sold value is greater than the average units sold value for that product (as opposed to the average for all products).
1. Compute the average units sold for a product.
2. Compare the average computed in Step 1 to the units sold in each sale row, and then select only the rows in which the number of units sold is greater.

# Correlated Subqueries (SQL)
```sql
SELECT INV_NUMBER, P_CODE, LINE_UNITS
FROM LINE LS
WHERE LS.LINE_UNITS > (SELECT AVG(LINE_UNITS)
                       FROM LINE LA
                       WHERE LA.P_CODE = LS.P_CODE);

SELECT INV_NUMBER, P_CODE, LINE_UNITS, (SELECT AVG(LINE_UNITS)
                                        FROM LINE LX
                                        WHERE LX.P_CODE = LS.P_CODE) AS AVG
FROM LINE LS
WHERE LS.LINE_UNITS > (SELECT AVG(LINE_UNITS)
                       FROM LINE LA
                       WHERE LA.P_CODE = LS.P_CODE);                            
```
# Correlated Subqueries (Exists)
```sql
-- list all vendors, but only if there are products to order.
SELECT *
FROM VENDOR
WHERE EXISTS (SELECT * FROM PRODUCT WHERE P_QOH <= P_MIN * 2);

-- list the names of all customers who have placed an order lately.
SELECT CUS_CODE, CUS_LNAME, CUS_FNAME
FROM CUSTOMER
WHERE EXISTS (SELECT CUS_CODE 
              FROM INVOICE
              WHERE INVOICE.CUS_CODE = CUSTOMER.CUS_CODE);
```

# Correlated Subqueries (Example of Exists)
Suppose that you want to know what vendors you must contact to order products that are approaching the minimum quantity-on-hand value that is less than double the minimum quantity.

```sql
SELECT V_CODE, V_NAME
FROM VENDOR
WHERE EXISTS (SELECT *
              FROM PRODUCT
              WHERE P_QOH < P_MIN * 2 AND VENDOR.V_CODE = PRODUCT.V_CODE);
```

# Built-in SQL Functions
- Basic Functions
```sql
SELECT pi();
SELECT UPPER("hello world");
SELECT ROUND(2.71828);
SELECT ROUND(2.71828, 2);
SELECT ROUND(PI());
SELECT NOW();
SELECT CURDATE();
SELECT CURTIME();
```
- Aggregate Functions: count(), max(), min(), sum(), avg()

# MySQL String Functions
```sql
SELECT CONCAT(EMP_FNAME, " ", EMP_LNAME)
FROM EMP;
SELECT FORMAT(P_QOH * P_PRICE, 0) as Total_Value
FROM PRODUCT
-- LEFT and RIGHT
SELECT LEFT(EMP_LNAME, 3)
FROM EMP;
-- UPPER and LOWER
SELECT UPPER(LEFT(EMP_LNAME, 3))
FROM EMP;
-- Others: SUBSTRING, TRIM, LTRIM, RTRIM
```
# MySQL Date/Time Functions
<div class="middle-grid">
    <img src="restricted/CTable07_10a.jpg" alt="">
    <img src="restricted/CTable07_10b.jpg" alt="">
</div>

# MySQL Numeric Functions
<div class="middle-grid">
    <img src="restricted/CTable07_11.jpg" alt="">
</div>

# MySQL Conversion Functions
<div class="middle-grid">
    <img src="restricted/CTable07_13a.jpg" alt="">
    <img src="restricted/CTable07_13b.jpg" alt="">
</div>

# Relational Set Operators (UNION)
```sql
SELECT CUS_LNAME, CUS_FNAME, CUS_INITIAL, CUS_AREACODE, CUS_PHONE
FROM CUSTOMER
UNION
SELECT CUS_LNAME, CUS_FNAME, CUS_INITIAL, CUS_AREACODE, CUS_PHONE
FROM CUSTOMER_2;
```
<div class="middle-grid">
    <img src="restricted/CFig07_61.jpg" alt="">
</div>

# Relational Set Operators (UNION ALL)
```sql
SELECT CUS_LNAME, CUS_FNAME, CUS_INITIAL, CUS_AREACODE, CUS_PHONE
FROM CUSTOMER
UNION ALL
SELECT CUS_LNAME, CUS_FNAME, CUS_INITIAL, CUS_AREACODE, CUS_PHONE
FROM CUSTOMER_2;
```
<div class="middle-grid">
    <img src="restricted/CFig07_62.jpg" alt="">
</div>

# Relational Set Operators (INTERSECT)
List the customer codes for all customers who are in area code 615 and who have made purchases. (If a customer has made a purchase, there must be an invoice record for that customer.)

```sql
-- MySQL does not support INTERSECT
SELECT CUS_CODE FROM CUSTOMER WHERE CUS_AREACODE = "615"
INTERSECT
SELECT DISTINCT CUS_CODE FROM INVOICE;

-- Use Join instead of
SELECT DISTINCT C.CUS_CODE
FROM CUSTOMER C
INNER JOIN INVOICE I ON C.CUS_CODE = I.CUS_CODE
WHERE C.CUS_AREACODE = '615';
```
# Relational Set Operators (MINUS / EXCEPT)
```sql
-- MySQL does not support MINUS
SELECT CUS_LNAME, CUS_FNAME, CUS_INITIAL, CUS_AREACODE, CUS_PHONE
FROM CUSTOMER
MINUS
SELECT CUS_LNAME, CUS_FNAME, CUS_INITIAL, CUS_AREACODE, CUS_PHONE
FROM CUSTOMER_2;

-- Use Join instead of
SELECT C.CUS_LNAME, C.CUS_FNAME, C.CUS_INITIAL, C.CUS_AREACODE, C.CUS_PHONE
FROM CUSTOMER C
LEFT JOIN CUSTOMER_2 C2 
ON C.CUS_LNAME = C2.CUS_LNAME 
AND C.CUS_FNAME = C2.CUS_FNAME
AND C.CUS_INITIAL = C2.CUS_INITIAL
AND C.CUS_AREACODE = C2.CUS_AREACODE
AND C.CUS_PHONE = C2.CUS_PHONE
WHERE C2.CUS_LNAME IS NULL;
```

# Crafting SELECT Queries
- Know Your Data: the importance of understanding the data model that you are working in cannot be overstated
- Know the Problem: understand the question you are attempting to answer
- Build clauses in the following order
  - FROM
  - WHERE
  - GROUP BY
  - HAVING
  - SELECT
  - ORDER BY

# Review Questions
- Explain the difference between an ORDER BY clause and a GROUP BY clause.
- What three join types are included in the OUTER JOIN classification? 
- What are the four categories of SQL functions
