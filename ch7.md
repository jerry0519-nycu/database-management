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
- Use semicolon **(;)** at the end of each SQL statement to separate each SQL statement **(不用每行都加)**
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

<details>
	<summary><strong>enum vs set</strong></summary>

| 項目     | `ENUM`                                     | `SET`                           |
| ------ | ------------------------------------------ | ------------------------------- |
| 值的選擇數量 | 只能選一個（單選）                                  | 可選多個（多選），但只能從指定的選項中組合           |
| 儲存方式   | 儲存單一值的索引                                   | 儲存多個值的位元組合（bit mask）            |
| 用途     | 欄位值限定為多個選項之一                               | 欄位值可包含多個選項的組合                   |
| 範例     | `ENUM('small','medium','large')`           | `SET('read','write','execute')` |
| 取值範圍   | 一個欄位只能有 `'small'` 或 `'medium'` 或 `'large'` | 一個欄位可以同時有 `'read,write'` 等組合    |

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
- 固定不變時間 → 用 `DATETIME`
- 需要時區轉換、自動時間戳 → 用 `TIMESTAMP`

| 類型       | `CURRENT_TIMESTAMP`               | `NOW()`                      |
| -------- | --------------------------------- | ---------------------------- |
| 作為預設值用   | ✅ 可用於 `DEFAULT CURRENT_TIMESTAMP` | ❌ 不能用 `DEFAULT NOW()`        |
| 作為查詢或運算用 | ✅ `SELECT CURRENT_TIMESTAMP;`     | ✅ `SELECT NOW();`            |
| 等價性      | ✅ `CURRENT_TIMESTAMP = NOW()` 等價  | ✅ 與 `CURRENT_TIMESTAMP` 相同效果 |

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
<details>
	<summary><strong>constraint用法</strong></summary>

#### CONSTRAINT 的基本語法

在 SQL 的 CREATE TABLE 語句中，CONSTRAINT 用於定義表級約束，其基本語法結構如下：

```sql
CONSTRAINT constraint_name constraint_type (column_list)
```

在範例中：
```sql
CONSTRAINT CUS_UI1 UNIQUE(CUS_LNAME,CUS_FNAME, CUS_PHONE)
```

這表示：
- 創建一個名為 `CUS_UI1` 的約束
- 約束類型是 `UNIQUE` (唯一性約束)
- 應用於 `CUS_LNAME`, `CUS_FNAME`, `CUS_PHONE` 這三個欄位的組合

## 為什麼不需要加上 } 符號

1. **SQL 語法標準**：SQL 使用分號 `;` 作為語句結束符號，而不是像程式語言那樣使用大括號 `{}` 來界定區塊。

2. **CREATE TABLE 結構**：CREATE TABLE 語句本身就是一個完整的語句，其內容由括號 `()` 包含，所有列定義和約束都在這對括號內完成。

3. **約束定義位置**：約束可以：
   - 直接寫在欄位定義後面（行內約束）
   - 或在所有欄位定義後單獨聲明（表級約束）
   兩種方式都不需要額外的結束符號。

## 其他常見約束類型

除了 UNIQUE 約束外，CONSTRAINT 還可用於定義：

```sql
-- 主鍵約束
CONSTRAINT PK_CUSTOMER PRIMARY KEY (CUS_CODE)
//不需要再加PRIMARY KEY (CUS_CODE)

-- 外鍵約束
CONSTRAINT FK_ORDERS_CUSTOMER FOREIGN KEY (CUS_CODE) REFERENCES CUSTOMER(CUS_CODE)

-- 檢查約束
CONSTRAINT CHK_BALANCE CHECK (CUS_BALANCE >= 0)

-- 默認值 (通常直接寫在列定義中，不用CONSTRAINT)
CUS_BALANCE NUMERIC(9,2) DEFAULT 0.00
```
SQL 語法使用分號 `;` 表示語句結束，而不是使用大括號，這是 SQL 標準語法的設計。
</details>

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

# Data Manipulation Commands
<img width="460" alt="image" src="https://github.com/user-attachments/assets/1b29de27-14d2-41fa-8162-006829885a23" />

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
<details>
	<summary><strong>SELECT結構</strong></summary>
	
# MySQL SELECT 語句結構解析

這是一個標準的 MySQL SELECT 查詢語句結構，用於從資料表中檢索資料。以下是每個部分的詳細解釋：

#### 基本結構
```sql
SELECT column1, column2, ...  -- 選擇要查詢的欄位
FROM table_name               -- 指定資料來源表
```

#### 可選子句

##### 1. WHERE 條件
```sql
[WHERE condition]
```
- **用途**：過濾記錄，只返回符合條件的行
- **範例**：`WHERE 年齡 > 18 AND 城市 = '台北'`

##### 2. GROUP BY 分組
```sql
[GROUP BY column]
```
- **用途**：將結果集按指定欄位分組，通常與聚合函數(如COUNT, SUM, AVG等)一起使用
- **範例**：`GROUP BY 部門` 會將相同部門的記錄分在同一組
- **SELECT 裡出現的欄位，如果沒有用 SUM()、AVG()、COUNT() 這種「聚合函數」，那它一定要在 GROUP BY 裡面**

##### 3. HAVING 篩選分組
```sql
[HAVING condition]
```
- **用途**：對GROUP BY產生的分組進行篩選（類似WHERE，但用於分組後）
- **範例**：`HAVING COUNT(*) > 5` 只顯示記錄數大於5的分組

##### 4. ORDER BY 排序
```sql
[ORDER BY column [ASC|DESC]]
```
- **用途**：對結果集進行排序
- **ASC**：升序（預設值）
- **DESC**：降序
- **範例**：`ORDER BY 成績 DESC, 姓名 ASC`

##### 5. LIMIT 限制結果數量
```sql
[LIMIT number OFFSET offset]
```
- **用途**：限制返回的記錄數量和起始位置
- **number**：要返回的最大記錄數
- **offset**：跳過的記錄數（從0開始）
- **簡寫**：`LIMIT offset, number` 與 `LIMIT number OFFSET offset` 等效
- **範例**：`LIMIT 10 OFFSET 20` 跳過前20筆，返回接下來的10筆記錄
</details>

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

<details>
	<summary><strong>中文表格</strong></summary>

| 子句 (Clause)               | 用途 (Purpose)            | 解釋 (Explanation)                                                                 |
|---------------------------|--------------------------|-----------------------------------------------------------------------------------|
| SELECT department, COUNT(*), AVG(salary) | 選擇要檢索的欄位        | 選取部門名稱、員工人數和平均薪資                                                  |
| FROM employees             | 資料來源表               | 從員工表中獲取資料                                                                |
| WHERE status = 'active'    | 篩選資料列               | 只包含目前狀態為「在職」的員工                                                    |
| GROUP BY department        | 分組                    | 按部門分組資料                                                                    |
| HAVING AVG(salary) > 50000 | 分組後篩選              | 只顯示平均薪資超過 50,000 的部門                                                  |
| ORDER BY avg_salary DESC   | 排序                    | 按平均薪資由高到低排序結果                                                        |
| LIMIT 5 OFFSET 10          | 分頁處理                | 跳過前 10 筆資料，返回接下來的 5 筆資料                                           |

</details>

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
<details>
	<summary><strong>Alias(別名)的本質與概念</strong></summary>
	
**Alias（別名）** 在 SQL 中是一種「**臨時命名**」的機制，用來簡化或重新定義資料庫物件（如表、欄位、計算結果）在查詢中的顯示名稱或引用方式。它的核心概念是：

#### **1. Alias 的本質**
- **不是永久修改**：只是「**當前查詢有效**」的暫時名稱，不影響資料庫實際結構。
- **不改變原始資料**：僅改變查詢結果的「顯示名稱」或「引用方式」。
- **純粹為了方便**：讓 SQL 更易讀、易寫，尤其在複雜查詢時特別有用。
  
#### **2. Alias 的兩種主要類型**
##### **(1) Column Alias（欄位別名）**
- **用途**：替換「欄位名稱」或「計算結果」的顯示名稱。
- **範例**：
  ```sql
  SELECT 
      employee_id AS "員工編號",
      salary * 12 AS "年薪"  -- 把計算結果命名為「年薪」
  FROM employees;
  ```

##### **(2) Table Alias（表格別名）**
- **用途**：簡化表名稱（尤其在多表 JOIN 時避免衝突）。
- **範例**：
  ```sql
  SELECT e.name, d.department_name
  FROM employees AS e  -- 把 employees 表簡稱為 e
  JOIN departments AS d ON e.dept_id = d.id;  -- departments 表簡稱為 d
  ```
#### **3. 為什麼需要 Alias？**
✅ **可讀性**：讓 SQL 更容易理解（例如 `AVG(salary) AS avg_salary` 比直接寫 `AVG(salary)` 直觀）。  
✅ **避免衝突**：在多表查詢時，用別名區分相同名稱的欄位（例如 `e.salary` vs `m.salary`）。  
✅ **簡化複雜計算**：替臨時計算的欄位賦予有意義的名稱，方便後續引用。  
✅ **支援特殊字元**：如果欄位名稱包含空格或保留字，可用別名替代（例如 `"總金額"`）。  

#### **4. 技術層面：Alias 如何運作？**
- **執行順序**：  
  SQL 引擎在解析查詢時，會先處理 `FROM`、`WHERE`、`GROUP BY` 等子句，最後才處理 `SELECT` 中的別名。  
  - 因此：
    - ✅ 可以在 `ORDER BY`、`HAVING` 使用別名（因為它們在 `SELECT` 之後執行）。  
    - ❌ **不能在 `WHERE` 使用別名**（因為 `WHERE` 在 `SELECT` 之前執行）。  

- **資料庫差異**：
  | 資料庫       | 別名語法範例                     | 注意事項                     |
  |-------------|--------------------------------|----------------------------|
  | MySQL       | `SELECT salary AS '薪資'`      | 可用單引號或雙引號           |
  | PostgreSQL  | `SELECT salary AS "薪資"`      | 嚴格區分大小寫，建議用雙引號 |
  | SQL Server  | `SELECT salary AS [薪資]`      | 常用方括號                 |
  | Oracle      | `SELECT salary AS "薪資"`      | 雙引號強制區分大小寫        |
#### **5. 經典應用場景**
##### **情境 1：計算並重新命名**
```sql
SELECT 
    product_name,
    price * quantity AS "總銷售額",
    (price * quantity) * 0.1 AS "稅金"
FROM orders;
```

##### **情境 2：多表 JOIN 時避免混淆**
```sql
SELECT 
    e.name AS "員工姓名",
    d.name AS "部門名稱"
FROM employees AS e
JOIN departments AS d ON e.dept_id = d.id;
```

##### **情境 3：搭配聚合函數與排序**
```sql
SELECT 
    department,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department
ORDER BY avg_salary DESC;  -- 用別名排序
```
#### **總結：Alias 是什麼？**
- **本質**：查詢中的「臨時命名」，不影響原始資料。  
- **用途**：提升可讀性、簡化複雜查詢、避免名稱衝突。  
- **限制**：不能在 `WHERE` 使用，且僅在當前查詢有效。  

</details>

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

<details>
	<summary><strong>SELECT DISTINCT用法</strong></summary>
	
`SELECT DISTINCT` 是 MySQL 中用來**去除查詢結果中重複值**的指令，它會返回指定欄位的唯一值（不重複的值）。
	
#### 基本語法

```sql
SELECT DISTINCT 欄位名1, 欄位名2, ...
FROM 表名
[WHERE 條件];
```

#### 實際範例

假設有一個「客戶」表：

| 客戶ID | 客戶姓名 | 城市     | 國家   |
|--------|----------|----------|--------|
| 1      | 張三     | 台北     | 台灣   |
| 2      | 李四     | 高雄     | 台灣   |
| 3      | 王五     | 台北     | 台灣   |
| 4      | John     | 紐約     | 美國   |
| 5      | Sarah    | 洛杉磯   | 美國   |

##### 範例1：查詢不重複的城市

```sql
SELECT DISTINCT 城市 FROM 客戶;
```

**結果：**
```
台北
高雄
紐約
洛杉磯
```

##### 範例2：查詢不重複的國家

```sql
SELECT DISTINCT 國家 FROM 客戶;
```

**結果：**
```
台灣
美國
```

##### 範例3：多欄位組合不重複

```sql
SELECT DISTINCT 城市, 國家 FROM 客戶;
```

**結果：**
```
台北    台灣
高雄    台灣
紐約    美國
洛杉磯  美國
```

#### 與一般 SELECT 的比較

不使用 DISTINCT：
```sql
SELECT 城市 FROM 客戶;
```
結果會包含重複的「台北」兩次

使用 DISTINCT：
```sql
SELECT DISTINCT 城市 FROM 客戶;
```
結果中「台北」只會出現一次

#### 注意事項
1. DISTINCT 作用於**所有選取的欄位**組合
2. 對 NULL 值的處理：DISTINCT 會將所有 NULL 視為相同值，只返回一個 NULL
3. 效能影響：DISTINCT 操作需要額外的排序和比較，可能降低查詢效能
4. 與 GROUP BY 的區別：DISTINCT 只是去除重複，不進行分組計算
</details>

# FROM Clause Options
- The FROM clause specifies table(s) which is involved
   - FROM子句是SQL查詢的基礎，它定義了查詢的數據來源
   	- 例如：`FROM customers` 表示從customers表中獲取數據
   	- 可以指定單個表或多個表（用逗號分隔或使用JOIN）
- Only columns in tables in FROM clause are available throughout the rest of the query
  - 只有在FROM子句中指定的資料表的欄位，才能在查詢的其他部分使用
  	- SELECT、WHERE、GROUP BY等子句只能引用FROM子句中出現的表欄位
  	- 如果嘗試使用不在FROM子句中的表欄位，會產生錯誤
  	- 例如：`SELECT customer_name FROM orders` 會出錯，如果orders表沒有customer_name欄位
- Multiple tables must be combined using a type of JOIN operation
	- 多個資料表必須透過某種JOIN操作來結合
   		- 當查詢需要從多個表獲取數據時，必須明確指定如何連接這些表
     		- INNER JOIN（內連接）：只返回匹配的行
     		- LEFT JOIN（左連接）：返回左表所有行，右表不匹配則為NULL
     		- RIGHT JOIN（右連接）：返回右表所有行，左表不匹配則為NULL
     		- FULL JOIN（全連接）：返回兩表所有行，不匹配則為NULL
   		- 舊式語法可以用逗號分隔表名，但這實際上是隱式的CROSS JOIN（笛卡爾積），通常不是我們想要的

# ORDER BY Clause Options

```sql
SELECT 	columnlist
FROM 		tablelist
[ORDER BY	columnlist [ASC|DESC] ]; ---升序/降序，非必要，不指定時，MySQL 會自動使用 ASC (升序) 作為預設值
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

<details>
	<summary><strong>字串比較</strong></summary>
	
##### 1. 單引號的意義
- 用於標示**文字字串**（包含字母、數字、符號的組合）
- 表示 `'1558-QW1'` 是一個整體的字串值，而不是數學運算

##### 2. 這個比較的實際行為
當您寫 `P_CODE < '1558-QW1'` 時：
- 資料庫會**逐字元比較**（從左到右）
- 比較是基於**字母順序**（ASCII/Unicode 值）
- 範例比較：
  - `'1000-AA'` < `'1558-QW1'`（第一個不同字元 '0' < '5'）
  - `'1558-QV9'` < `'1558-QW1'`（'V' < 'W'）
  - `'1558-QW'` < `'1558-QW1'`（較短的字串視為較小）

##### 3. 不同資料類型的比較方式
| 資料類型       | 格式範例       | 比較方式               |
|---------------|---------------|-----------------------|
| 數字（整數）   | `WHERE id < 10` | 數值大小比較          |
| 數字（浮點數） | `WHERE price < 9.99` | 數值大小比較      |
| 字串（文字）   | `WHERE code < '1558-QW1'` | 字典序比較      |
| 日期          | `WHERE date < '2023-01-01'` | 時間先後比較    |

##### 4. 常見應用場景
- 產品編號範圍查詢（如 `P_CODE BETWEEN '1000-AA' AND '2000-ZZ'`）
- 文字類型的序號過濾
- 分類代碼的範圍選擇

##### 5. 重要注意事項
- 在大多數資料庫中，字串比較是**區分大小寫**的（'A' 和 'a' 不同）
- 若要進行**不區分大小寫**的比較，通常需要用函數轉換：
  ```sql
  WHERE UPPER(P_CODE) < '1558-QW1'
  ```
- 如果是純數字組成的字串（如 `'123'`），比較結果可能與數字比較不同：
  - 字串比較：`'9'` > `'100'`（因為 '9' > '1'）
  - 數字比較：`9` < `100`
</details>

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

use parentheses and compare below two select statements
先執行括號內的運算 
SELECT P_DESCRIPT, P_PRICE, V_CODE
FROM PRODUCT
WHERE (V_CODE = 25595 OR V_CODE = 24288) AND P_PRICE > 100;

SELECT P_DESCRIPT, P_PRICE, V_CODE
FROM PRODUCT
WHERE V_CODE = 25595 OR V_CODE = 24288 AND P_PRICE > 100;
-- AND優先於OR --

SELECT *
FROM PRODUCT
WHERE NOT (V_CODE = 21344);
``` 
<details>
	<summary><strong>邏輯運算子順序表</strong></summary>

#### 標準執行順序（從高到低）
1. **括號 `( )`** - 最高優先級，強制先執行
2. **NOT 運算子**
3. **AND 運算子**
4. **OR 運算子** - 最低優先級

#### 優先級順序表

| 優先級 | 運算子 | 範例 | 等效寫法 |
|-------|--------|------|----------|
| 1 | 括號 | `WHERE (A OR B) AND C` | - |
| 2 | NOT | `WHERE NOT A = B` | `WHERE A <> B` |
| 3 | AND | `WHERE A AND B OR C` | `WHERE (A AND B) OR C` |
| 4 | OR | `WHERE A OR B AND C` | `WHERE A OR (B AND C)` |

#### 實際案例比較

##### 案例1：混合 AND 和 OR
```sql
-- 原始寫法（易混淆）
WHERE A OR B AND C

-- 實際執行順序（AND優先）
WHERE A OR (B AND C)
```

##### 案例2：明確使用括號
```sql
-- 明確優先順序
WHERE (A OR B) AND C
```

##### 案例3：包含 NOT
```sql
-- NOT 優先於 AND
WHERE NOT A = B AND C

-- 實際執行順序
WHERE (NOT A = B) AND C
```

#### 重要注意事項

1. **最佳實踐**：當混合使用不同運算子時，**永遠使用括號明確優先順序**，即使您記得優先級規則
   - 提高可讀性
   - 避免不同資料庫系統的細微差異
   - 減少未來維護時的誤解

2. **特殊情況**：
   - 相同運算子通常從左到右執行
     ```sql
     WHERE A AND B AND C  -- 執行順序：(A AND B) AND C
     ```
   - IN 運算子的優先級與 OR 相同
     ```sql
     WHERE A OR B IN (1,2)  -- 執行順序：A OR (B IN (1,2))
     ```

3. **效能影響**：
   - 資料庫優化器可能會重新排列條件順序以優化查詢
   - 但邏輯結果會保持與優先級規則一致
</details>

# Special Operators in WHERE Clause
- BETWEEN – Used to check whether an attribute value is within a range
- IN – Used to check whether an attribute value matches any value within a value list
- LIKE – Used to check whether an attribute value matches a given string pattern
- IS NULL – Used to check whether an attribute value is null
- NOT – Used to negate a condition

<details>
	<summary><strong>範例</strong></summary>
	
#### 1. BETWEEN - 範圍檢查

**用途**：檢查值是否在指定範圍內（包含邊界值）

```sql
-- 找出價格在 100 到 200 元之間的產品
SELECT * FROM PRODUCT
WHERE P_PRICE BETWEEN 100 AND 200;

-- 找出 2023 年 1 月入庫的產品
SELECT * FROM PRODUCT
WHERE P_INDATE BETWEEN '2023-01-01' AND '2023-01-31';
```

#### 2. IN - 值列表檢查

**用途**：檢查值是否匹配列表中的任一值

```sql
-- 找出供應商代碼為 21344、24288 或 25595 的產品
SELECT * FROM PRODUCT
WHERE V_CODE IN (21344, 24288, 25595);

-- 找出位於台北、台中或高雄的客戶
SELECT * FROM CUSTOMER
WHERE CUST_CITY IN ('台北', '台中', '高雄');
```

<details>
	<summary>BETWEEN vs IN舉例</summary>

```sql	
-- 使用BETWEEN：查詢價格在50到100元之間的產品
SELECT * FROM PRODUCT
WHERE P_PRICE BETWEEN 50.00 AND 100.00;
-- 等效於：P_PRICE >= 50.00 AND P_PRICE <= 100.00

-- 使用IN：查詢價格正好是50、75或100元的產品
SELECT * FROM PRODUCT
WHERE P_PRICE IN (50.00, 75.00, 100.00);
-- 等效於：P_PRICE = 50.00 OR P_PRICE = 75.00 OR P_PRICE = 100.00
```
</details>

#### 3. LIKE - 模式匹配

**用途**：檢查字串是否符合特定模式

```sql
-- 找出產品描述開頭為 "筆記型" 的產品
SELECT * FROM PRODUCT
WHERE P_DESCRIPT LIKE '筆記型%';

-- 找出產品代碼中包含 "USB" 的產品
SELECT * FROM PRODUCT
WHERE P_CODE LIKE '%USB%';

-- 找出電話號碼開頭是 "02"（台北地區）的客戶
SELECT * FROM CUSTOMER
WHERE CUST_PHONE LIKE '02%';

-- 精確匹配 5 個字元，第3個字元是 A 的產品代碼
SELECT * FROM PRODUCT
WHERE P_CODE LIKE '__A__';
```

| 比較項目  | `=`                     | `LIKE`                               |
| ----- | ----------------------- | ------------------------------------ |
| 用途    | 精準比對                    | 模糊比對                                 |
| 範例語法  | `WHERE name = 'Peter'`  | `WHERE name LIKE 'Pet%'`             |
| 結果    | 只有名字是完全等於 Peter 的資料會被選中 | 所有名字開頭是 Pet 的資料都會被選中（例如 Peter、Petra） |
| 通配符支援 | ❌ 不支援                   | ✅ 支援 `%` 和 `_`                       |

<details>
	<summary>%的用法</summary>

##### 1. 基本功能
- `%` 可以匹配**任意長度**的字元組合（包括零個字元）
- 類似於檔案搜尋中的 `*` 符號

##### 2. 不同位置的意義

| 模式範例       | 匹配說明                          | 實際例子                     |
|----------------|----------------------------------|-----------------------------|
| `'筆記型%'`    | 以「筆記型」**開頭**的字串        | 筆記型電腦、筆記型配件       |
| `'%電腦'`      | 以「電腦」**結尾**的字串          | 桌上型電腦、筆記型電腦       |
| `'%無線%'`     | **包含**「無線」的字串            | 無線滑鼠、藍牙無線耳機       |
| `'A%B'`        | 以 A **開頭**且以 B **結尾**      | A123B、ACB、AB              |

##### 3. 實際查詢範例

```sql
-- 找出所有「筆記型」開頭的產品
SELECT * FROM PRODUCT
WHERE P_DESCRIPT LIKE '筆記型%';

-- 找出所有「Pro」結尾的產品型號
SELECT * FROM PRODUCT
WHERE P_CODE LIKE '%Pro';

-- 找出描述中包含「無線」的產品（不論位置）
SELECT * FROM PRODUCT
WHERE P_DESCRIPT LIKE '%無線%';

-- 找出電話區號是「02」開頭的客戶
SELECT * FROM CUSTOMER
WHERE CUST_PHONE LIKE '02%';
```
**ex:若為'%hammer%'，則hand_hammer_tool、red hammer blade皆匹配**

##### `%` 與 `_` 的區別

另一個常用萬用字元是 `_`（底線），它與 `%` 的主要區別是：

| 萬用字元 | 功能                   | 範例            | 匹配範例        |
|---------|------------------------|----------------|----------------|
| `%`     | 匹配**零個或多個**字元 | `'A%'`         | A, AB, ABC     |
| `_`     | 匹配**恰好一個**字元   | `'A_'`         | AB, AC (不匹配 A) |
</details>

#### 4. IS NULL - 空值檢查

**用途**：檢查值是否為 NULL

```sql
-- 找出尚未設定供應商的產品
SELECT * FROM PRODUCT
WHERE V_CODE IS NULL;

-- 找出沒有填寫電子郵件的客戶
SELECT * FROM CUSTOMER
WHERE CUST_EMAIL IS NULL;
```

#### 5. NOT - 條件否定

**用途**：反轉條件的結果

```sql
-- 找出價格不在 100 到 200 元之間的產品
SELECT * FROM PRODUCT
WHERE P_PRICE NOT BETWEEN 100 AND 200;

-- 找出非台北、台中、高雄的客戶
SELECT * FROM CUSTOMER
WHERE CUST_CITY NOT IN ('台北', '台中', '高雄');

-- 找出產品描述不是以 "筆記型" 開頭的產品
SELECT * FROM PRODUCT
WHERE P_DESCRIPT NOT LIKE '筆記型%';

-- 找出已設定供應商的產品
SELECT * FROM PRODUCT
WHERE V_CODE IS NOT NULL;

-- 找出不是 21344 供應商的產品（兩種寫法等價）
SELECT * FROM PRODUCT
WHERE NOT V_CODE = 21344;
-- 或
SELECT * FROM PRODUCT
WHERE V_CODE <> 21344;
```
</details>

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

| 符號  | 意思                 | 用在哪裡         | 範例                                        |
| --- | ------------------ | ------------ | ----------------------------------------- |
| `*` | 所有欄位（全部欄位）         | `SELECT` 語句中 | `SELECT * FROM users;`（查詢所有欄位）            |
| `%` | 匹配 0 個或多個字元（模糊查詢）  | `LIKE` 條件中   | `WHERE name LIKE 'A%'`（找出以 A 開頭的名字）       |
| `_` | 匹配任意一個字元（固定長度模糊查詢） | `LIKE` 條件中   | `WHERE name LIKE 'A__'(兩個_)`（找出開頭是 A、接兩個字元的名字） |

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
    
<img width="450" alt="image" src="https://github.com/user-attachments/assets/25ba46ab-0288-4418-9f4a-00572ac1bf46" />

<img width="450" alt="image" src="https://github.com/user-attachments/assets/db552872-dcac-442b-8853-7127ced0ec71" />

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

# Illustrated by Relational Algebra Natural Join
PRODUCT -> SELECT -> PROJECT
<details>
	<summary><strong>圖示</strong></summary>
<img width="395" alt="image" src="https://github.com/user-attachments/assets/0e73505e-8b20-4bf9-b03e-ee01b07f5777" />
<img width="394" alt="image" src="https://github.com/user-attachments/assets/c52f8621-f1dd-4c8e-a9f1-86d140d77f90" />
<img width="390" alt="image" src="https://github.com/user-attachments/assets/133c9fc2-dd99-4105-8924-92b6c9ee362b" />
<img width="393" alt="image" src="https://github.com/user-attachments/assets/1a856f89-c22d-4dd2-a420-bb509227065f" />
</details>


# Example of JOIN ON
```sql
SELECT INVOICE.INV_NUMBER, PRODUCT.P_CODE, P_DESCRIPT, LINE_UNITS, LINE_PRICE
FROM INVOICE
JOIN LINE ON INVOICE.INV_NUMBER = LINE.INV_NUMBER 
JOIN PRODUCT ON LINE.P_CODE = PRODUCT.P_CODE;

-- Compare to JOIN USING
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

<details>
	<summary><strong>三者比較表</strong></summary>
	
| 比較項目        | JOIN ON (現代標準)               | JOIN USING (現代簡化版)         | Old-Style JOIN (傳統寫法)        |
|----------------|----------------------------------|----------------------------------|----------------------------------|
| **語法範例**    | `FROM A JOIN B ON A.id = B.id`   | `FROM A JOIN B USING(id)`        | `FROM A, B WHERE A.id = B.id`    |
| **連接條件**    | 明確用ON指定，靈活               | 自動匹配同名欄位                | 在WHERE子句中指定                |
| **欄位名稱**    | 可不同名 (`A.col1 = B.col2`)     | 必須完全相同                    | 可不同名                         |
| **結果欄位**    | 保留兩表原始欄位                 | 合併同名欄位為單一欄位          | 保留兩表原始欄位                 |
| **非等值連接**  | 支援 (`ON A.id = B.id AND A.date > B.date`) | 僅支援等值連接           | 支援                             |
| **可讀性**      | 高，連接條件明確                 | 最高，最簡潔                    | 低，條件混在WHERE中              |
| **維護性**      | 高                               | 高                              | 低                               |
| **執行效能**    | 相同                             | 相同                            | 相同                             |
| **推薦程度**    | ⭐⭐⭐⭐⭐ (最推薦)              | ⭐⭐⭐⭐ (同名欄位時推薦)        | ⭐ (不推薦，已淘汰)              |

#### 建議

1. **永遠避免使用 Old-Style JOIN**，因為：
   - 容易忘記寫WHERE條件導致笛卡爾積
   - 混合了連接條件和過濾條件，難以維護
   - 已被SQL標準淘汰

2. **優先使用 JOIN ON**：
   - 適用所有場景
   - 明確區分連接條件與過濾條件
   - 支援複雜連接邏輯

3. **當連接欄位同名時可考慮 USING**：
   - 使SQL更簡潔
   - 自動合併同名欄位
   - 但功能限制較多
</details>

# Outer Joins
Three types of outer join: Left (outer) join, Right (outer) join, Full (outer) join

# Left Outer Join
```sql
SELECT column-list
FROM table1 LEFT[OUTER] JOIN table2 ON join-condition --- OUTER可省略
SELECT P_CODE, VENDOR.V_CODE, V_NAME
FROM VENDOR 
LEFT JOIN PRODUCT ON VENDOR.V_CODE = PRODUCT.V_CODE; --- ON後面接的東西可以不同
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

**只有RIGHT/LEFT (OUTER) JOIN 沒有 OUTER JOIN**

# Cross Join
- A cross join performs a relational product (also known as the Cartesian product) of two tables.
- Despite the name, CROSS JOIN is not truly a join operation because it does not unite the rows of the tables based on a common attribute.
```sql
SELECT column-list FROM table1 CROSS JOIN table2

SELECT * FROM INVOICE CROSS JOIN LINE;
```

**例:A表有3筆資料，B表有4筆資料，cross join後會產生3 $\times$ 4=12筆資料**

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
SELECT E.EMP_NUM, E.EMP_LNAME, E.EMP_MGR, M.EMP_LNAME--E.EMP_NUM:從 E 這個表格中取 EMP_NUM 欄位的值
FROM EMP E
JOIN EMP M ON E.EMP_MGR = M.EMP_NUM;
```

#### 查詢功能說明

這個查詢的目的是：
- 列出每位員工的編號、姓氏
- 同時顯示該員工的**主管姓名**（而不只是主管編號）

#### 查詢分解

```sql
SELECT E.EMP_NUM, E.EMP_LNAME, E.EMP_MGR, M.EMP_LNAME
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.EMP_MGR = M.EMP_NUM;
```

#### 各部分的意義

| 部分 | 說明 |
|------|------|
| `EMPLOYEE E` | 為員工表建立別名 E (代表員工角度) |
| `EMPLOYEE M` | 為員工表建立別名 M (代表主管角度) |
| `E.EMP_MGR = M.EMP_NUM` | 連接條件：員工的主管編號 = 主管的員工編號 |
| `M.EMP_LNAME` | 顯示主管的姓氏 |

#### 實際運作方式

1. 資料庫會將 `EMPLOYEE` 表視為兩個邏輯表：
   - `E`：員工記錄
   - `M`：主管記錄

2. 對於每位員工，查找 `EMP_MGR` 欄位中指定的主管編號

3. 在主管表(`M`)中找到對應編號的記錄，獲取主管姓名

#### 範例結果
假設 `EMPLOYEE` 表有以下資料：

| EMP_NUM | EMP_LNAME | EMP_MGR |
|---------|-----------|---------|
| 100     | Smith     | NULL    |
| 101     | Johnson   | 100     |
| 102     | Williams  | 100     |
| 103     | Brown     | 101     |

查詢結果將會是：

| EMP_NUM | EMP_LNAME | EMP_MGR | EMP_LNAME (主管) |
|---------|-----------|---------|------------------|
| 101     | Johnson   | 100     | Smith            |
| 102     | Williams  | 100     | Smith            |
| 103     | Brown     | 101     | Johnson          |

注意：
- 員工 Smith (EMP_NUM=100) 不會出現在結果中，因為他沒有主管 (EMP_MGR=NULL)
- 如果想包含沒有主管的員工，應改用 `LEFT JOIN`

#### 這種查詢的常見應用

1. 組織層級結構展示
2. 員工-主管關係報表
3. 任何需要從同一表中關聯不同記錄的情況（如產品組件關係、文件版本關係等）

<details>
	<summary><strong>組織關係架構圖</strong></summary>
	
```
       Smith (100)
       /      \
      /        \
Johnson (101)  Williams (102)
     |
     |
 Brown (103)
```
</details>

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
GROUP BY V_CODE --SELECT 裡出現的欄位，如果沒有用 SUM()、AVG()、COUNT() 這種「聚合函數」，那它一定要在 GROUP BY 裡面
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
<details>
	<summary><strong>聚合函數(sum, min, count...) & group by</strong></summary>

#### ✅ 有聚合函數時，何時要 `GROUP BY`？
##### ▶ **1. 有聚合函數 + 有其他欄位 → 要 `GROUP BY`**

常見情況：

```sql
SELECT PROJ_NUM, SUM(ASSIGN_HOURS)
FROM ASSIGNMENT;
```

這樣會 **出錯**，因為你選了 `PROJ_NUM`（不是聚合函數），又用了 `SUM()`，但沒有告訴 SQL 要「怎麼分組」，SQL 不知道你想怎麼加總。

✅ 正確寫法是：

```sql
SELECT PROJ_NUM, SUM(ASSIGN_HOURS)
FROM ASSIGNMENT
GROUP BY PROJ_NUM;
```
##### ▶ **2. 只有聚合函數 → 不需要 `GROUP BY`**

```sql
SELECT SUM(ASSIGN_HOURS) FROM ASSIGNMENT;
```

這是合法的，表示**對整張表**做加總，不需要分組。

#### 📝 總結

| 條件          | 要加 `GROUP BY` 嗎？ | 說明        |
| ----------- | ---------------- | --------- |
| 只用聚合函數      | ❌ 不需要            | 對整張表加總    |
| 聚合函數 + 普通欄位 | ✅ 需要             | 要分組，不然會報錯 |
| 沒有聚合函數      | ❌ 不需要            | 正常查詢      |

</details>

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

<details>
	<summary><strong>HAVING的用法</strong></summary>

#### 基本語法結構

```sql
SELECT 欄位1, 聚合函數(欄位2)
FROM 資料表
GROUP BY 欄位1
HAVING 過濾條件;
```
`HAVING` 是 SQL 中用於過濾分組結果的關鍵字，通常與 `GROUP BY` 一起使用。
#### 與 WHERE 的主要區別

| 特性        | WHERE 子句               | HAVING 子句               |
|------------|--------------------------|--------------------------|
| **執行時機** | 在分組前過濾原始資料      | 在分組後過濾聚合結果      |
| **適用對象** | 原始資料列                | 分組後的聚合結果          |
| **使用聚合** | 不可直接使用聚合函數      | 必須使用聚合函數          |
| **效能影響** | 先過濾可減少處理資料量    | 需先完成分組計算          |

#### 實際應用範例

##### 範例1：基本過濾分組結果
```sql
-- 找出平均價格超過50元的供應商
SELECT V_CODE, AVG(P_PRICE) AS 平均價格
FROM PRODUCT
GROUP BY V_CODE
HAVING AVG(P_PRICE) > 50; --只能過濾聚合後的結果(例如AVG, COUNT...)
```

##### 範例2：多條件過濾
```sql
-- 找出產品數量大於2且平均價格低於100元的供應商
SELECT V_CODE, COUNT(*) AS 產品數量, AVG(P_PRICE) AS 平均價格
FROM PRODUCT
GROUP BY V_CODE
HAVING COUNT(*) > 2 AND AVG(P_PRICE) < 100;
```

##### 範例3：與WHERE組合使用
```sql
-- 先過濾2023年的產品，再找出總銷售額超過1萬元的類別
SELECT 類別, SUM(銷售額) AS 總銷售額
FROM 銷售資料
WHERE YEAR(銷售日期) = 2023
GROUP BY 類別
HAVING SUM(銷售額) > 10000;
```

#### 注意事項

1. **別名使用**：在HAVING中可以使用SELECT中定義的別名
   ```sql
   SELECT V_CODE, AVG(P_PRICE) AS avg_price
   FROM PRODUCT
   GROUP BY V_CODE
   HAVING avg_price > 50;  -- 直接使用別名
   ```

2. **效能優化**：
   - 盡量在WHERE中先過濾掉不需要的資料
   - 對分組欄位建立索引可提升效能

3. **語法順序**：
   ```sql
   SELECT → FROM → WHERE → GROUP BY → HAVING → ORDER BY → LIMIT
   ```

#### 常見錯誤

1. 在HAVING中使用非聚合欄位：
   ```sql
   -- 錯誤示範（V_NAME不是聚合欄位）
   SELECT V_CODE, V_NAME, AVG(P_PRICE)
   FROM PRODUCT
   GROUP BY V_CODE
   HAVING V_NAME LIKE 'A%';  -- 這會報錯
   ```

2. 混淆WHERE和HAVING的使用時機：
   ```sql
   -- 錯誤示範（應在WHERE中過濾）
   SELECT V_CODE, AVG(P_PRICE)
   FROM PRODUCT
   GROUP BY V_CODE
   HAVING P_PRICE > 10;  -- 這會報錯
   ```

</details>

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

<details>
	<summary><strong>錯誤舉例</strong></summary>

```sql
-- 查詢A 
SELECT V_CODE, V_NAME
FROM VENDOR
WHERE V_CODE NOT IN (
    SELECT V_CODE FROM PRODUCT WHERE V_CODE IS NOT NULL
);

-- 查詢B 
SELECT V_CODE, V_NAME
FROM VENDOR
WHERE V_CODE IN (
    SELECT V_CODE FROM PRODUCT WHERE V_CODE IS NULL
);
```

#### 關鍵差異

| 比較點         | 查詢A                          | 查詢B                          |
|----------------|-------------------------------|-------------------------------|
| **邏輯**       | 找出「沒有對應產品」的供應商    | 找出「產品記錄中V_CODE為NULL」的供應商 |
| **子查詢條件** | `WHERE V_CODE IS NOT NULL`     | `WHERE V_CODE IS NULL`         |
| **運算子**     | `NOT IN`                      | `IN`                          |
| **實際結果**   | 返回沒有產品的供應商           | 永遠返回空結果集               |

#### 為什麼查詢B無效？

1. 子查詢 `SELECT V_CODE FROM PRODUCT WHERE V_CODE IS NULL` 會：
   - 找出所有 PRODUCT 表中 V_CODE 為 NULL 的記錄
   - 但因為我們在 SELECT 只選 V_CODE，而 V_CODE 本身就是 NULL
   - 所以子查詢結果是一組 NULL 值（不是具體的供應商代碼）

2. 當使用 `IN` 或 `NOT IN` 與包含 NULL 的子查詢比較時：
   - SQL 的邏輯規定：任何與 NULL 的比較結果都是「未知」(UNKNOWN)，不是 TRUE
   - 所以 `V_CODE IN (NULL, NULL,...)` 永遠不會成立

#### 等價改寫

如果要用 `IN` 實現相同功能，應該這樣寫：

```sql
SELECT V_CODE, V_NAME
FROM VENDOR
WHERE V_CODE NOT IN (
    SELECT DISTINCT V_CODE FROM PRODUCT 
    WHERE V_CODE IS NOT NULL
)
AND V_CODE IS NOT NULL;
```

#### 實際建議

1. 查找「沒有關聯記錄」的項目時：
   - 使用 `NOT IN` + 排除子查詢中的 NULL（如查詢A）
   - 或使用 `NOT EXISTS`（更安全，能自動處理NULL）

2. 避免寫法：
   ```sql
   WHERE col IN (SELECT ... WHERE col IS NULL)
   ```
   這種模式幾乎總是邏輯錯誤

3. 最推薦的寫法是使用 `LEFT JOIN` + `IS NULL` 或 `NOT EXISTS`：
   ```sql
   -- 方法1: LEFT JOIN
   SELECT V.* 
   FROM VENDOR V
   LEFT JOIN PRODUCT P ON V.V_CODE = P.V_CODE
   WHERE P.V_CODE IS NULL;

   -- 方法2: NOT EXISTS
   SELECT V_CODE, V_NAME
   FROM VENDOR V
   WHERE NOT EXISTS (
       SELECT 1 FROM PRODUCT P 
       WHERE P.V_CODE = V.V_CODE
   );
   ```
</details>

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

--等價於:
SELECT P_CODE, P_QOH * P_PRICE AS TOTALVALUE
FROM PRODUCT
WHERE P_QOH * P_PRICE > (
    SELECT MAX(P_QOH * P_PRICE)
    FROM PRODUCT
    WHERE V_CODE IN (
        SELECT V_CODE
        FROM VENDOR
        WHERE V_STATE = 'FL'
    )
);
```

- <span class="small-text"> Greater than ALL" is equivalent to "greater than the highest product cost of the list </span>
- <span class="small-text"> ANY operator to compare a single value to a list of values and select only the rows for which the inventory cost is greater than any value in the list</span>
- <span class="small-text"> Use the equal to ANY operator, which would be the equivalent of the IN operator.</span>

<details>
	<summary><strong>All vs Any</strong></summary>

| 比較        | `ALL`（全部都要符合） | `ANY`（其中一個符合就好） |
| --------- | ------------- | --------------- |
| `x > ...` | x 要比**全部都大**  | x 要比**至少一個大**   |
| `x < ...` | x 要比**全部都小**  | x 要比**至少一個小**   |
| 結果範圍      | 通常會篩出「最極端」的幾筆 | 通常會篩出比較「寬鬆」的條件  |

補充:也可以用min或max
| 比較條件            | 意思           | 等效寫法                    |
| --------------- | ------------ | ----------------------- |
| `x > ALL (子查詢)` | x 要比「全部的值」大  | `x > (SELECT MAX(...))` |
| `x > ANY (子查詢)` | x 要比「至少一個值」大 | `x > (SELECT MIN(...))` |
| `x < ALL (子查詢)` | x 要比「全部的值」小  | `x < (SELECT MIN(...))` |
| `x < ANY (子查詢)` | x 要比「至少一個值」小 | `x < (SELECT MAX(...))` |

</details>

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

#### 1. 獨立子查詢（Inner Subquery / Non-correlated Subquery）

**特點**：
- 子查詢可以獨立執行，不依賴外部查詢
- 執行順序：先執行子查詢 → 將結果傳給外部查詢使用 → 執行外部查詢
- 效能較好，因為子查詢只執行一次

**範例**：
```sql
-- 找出價格高於平均價格的產品
SELECT * FROM PRODUCT
WHERE P_PRICE > (
    SELECT AVG(P_PRICE) FROM PRODUCT  -- 此子查詢可獨立執行
);
```

**執行流程**：
1. 先執行 `SELECT AVG(P_PRICE) FROM PRODUCT` 得到一個平均值（例如 50.00）
2. 然後執行外部查詢：`SELECT * FROM PRODUCT WHERE P_PRICE > 50.00`

#### 2. 關聯子查詢（Correlated Subquery）

**特點**：
- 子查詢**不能獨立執行**，依賴外部查詢的當前行
- 執行順序：
  - 先執行外部查詢取出第一行
  - 將該行的值傳給子查詢執行
  - 重複直到處理完所有行
- 效能較差，因為子查詢會執行多次（每行一次）

**範例**：
```sql
-- 找出各供應商中價格高於該供應商平均價格的產品
SELECT * FROM PRODUCT P1
WHERE P_PRICE > (
    SELECT AVG(P_PRICE) 
    FROM PRODUCT P2 
    WHERE P2.V_CODE = P1.V_CODE  -- 引用外部查詢的欄位
);
```

**執行流程**：
1. 從外部查詢 `PRODUCT P1` 取出第一行
2. 用該行的 `V_CODE` 值執行子查詢，計算該供應商的平均價格
3. 比較該行產品的價格是否 > 計算出的平均價
4. 重複以上步驟處理每一行

#### 比較表格

| 特性                | 獨立子查詢                          | 關聯子查詢                          |
|---------------------|-------------------------------------|-------------------------------------|
| **執行次數**         | 執行一次                            | 每行執行一次                        |
| **依賴性**           | 不依賴外部查詢                      | 依賴外部查詢的當前行                |
| **效能**             | 較好                                | 較差                                |
| **可讀性**           | 較簡單                              | 較複雜                              |
| **典型應用**         | 單一值比較                          | 行與行之間的比較                    |
| **EXISTS 使用**      | 不適用                              | 常用（如 `WHERE EXISTS`）           |

#### 實際應用建議
1. **優先使用獨立子查詢**：當業務邏輯允許時，因效能較好
2. **必要時使用關聯子查詢**：當需要比較行與行之間的關係時
3. **考慮改寫為 JOIN**：許多關聯子查詢可改寫為 JOIN，效能通常更好

| 判斷依據                  | 內部子查詢（Independent Subquery） | 相關子查詢（Correlated Subquery）      |
| --------------------- | --------------------------- | ------------------------------- |
| **子查詢內有沒有使用外層查詢的欄位？** | 沒有，子查詢完全獨立執行，沒有用外層表的欄位      | 有，子查詢裡會用到外層查詢表的欄位作為條件           |
| **執行時機**              | 子查詢先執行一次，結果傳給外層查詢           | 子查詢會為外層查詢的每一筆資料執行一次             |
| **語法結構**              | 子查詢是完整獨立的 SELECT，不依賴外層資料    | 子查詢裡的 WHERE 或其他子句中會引用外層的表或別名的欄位 |
| **執行效能**              | 通常較快（只執行一次）                 | 通常較慢（執行次數 = 外層查詢結果筆數）           |


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


| 指令                             | 功能說明          | 範例輸出（假設當下時間是 2025-05-31） |
| ------------------------------ | ------------- | ------------------------ |
| `SELECT PI();`                 | 回傳圓周率 π 值     | 3.141592653589793        |
| `SELECT UPPER("hello world");` | 將字串轉成大寫       | HELLO WORLD              |
| `SELECT ROUND(2.71828);`       | 四捨五入到整數       | 3                        |
| `SELECT ROUND(2.71828, 2);`    | 四捨五入到小數點後 2 位 | 2.72                     |
| `SELECT ROUND(PI());`          | 對 π 進行四捨五入    | 3                        |
| `SELECT NOW();`                | 回傳當前日期與時間     | 2025-05-31 14:23:45      |
| `SELECT CURDATE();`            | 回傳當前日期（不含時間）  | 2025-05-31               |
| `SELECT CURTIME();`            | 回傳當前時間（不含日期）  | 14:23:45                 |

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

| 函數                         | 說明                     | 範例輸出（假設資料）                                         |
| -------------------------- | ---------------------- | -------------------------------------------------- |
| `CONCAT(str1, str2)`       | 字串串接，把多個字串合成一個字串       | `CONCAT('John', ' ', 'Doe')` → "John Doe"          |
| `FORMAT(number, d)`        | 格式化數字，將數字格式化為字串，d是小數位數 | `FORMAT(12345.678, 0)` → "12,346" (四捨五入取整數並加千分位逗號) |
| `LEFT(str, n)`             | 從字串左邊擷取n個字元            | `LEFT('Smith', 3)` → "Smi"                         |
| `RIGHT(str, n)`            | 從字串右邊擷取n個字元            | `RIGHT('Smith', 3)` → "ith"                        |
| `UPPER(str)`               | 將字串轉成大寫                | `UPPER('abc')` → "ABC"                             |
| `LOWER(str)`               | 將字串轉成小寫                | `LOWER('ABC')` → "abc"                             |
| `SUBSTRING(str, pos, len)` | 從字串第pos位置開始擷取len個字元    | `SUBSTRING('abcdef', 2, 3)` → "bcd"                |
| `TRIM(str)`                | 去除字串兩端的空白              | `TRIM('  hello  ')` → "hello"                      |
| `LTRIM(str)`               | 去除字串左端的空白              | `LTRIM('  hello')` → "hello"                       |
| `RTRIM(str)`               | 去除字串右端的空白              | `RTRIM('hello  ')` → "hello"                       |

<details>
	<summary>圖片</summary>
	
# MySQL Date/Time Functions
<img width="523" alt="image" src="https://github.com/user-attachments/assets/e58279cd-3ffd-4bbf-adb8-640df18c2323" />
<img width="523" alt="image" src="https://github.com/user-attachments/assets/82dc3ebd-549d-4c39-a765-d20275d7489f" />

# MySQL Numeric Functions
<img width="523" alt="image" src="https://github.com/user-attachments/assets/884958b4-34cd-4645-a88b-6a12db467cc9" />

# MySQL Conversion Functions
<img width="523" alt="image" src="https://github.com/user-attachments/assets/e9a79e53-7ccc-4763-900d-11885682df54" />
<img width="523" alt="image" src="https://github.com/user-attachments/assets/7eb12e95-71d5-4ba4-a820-7ee36075e5c0" />

</details>

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

<details>
	<summary><strong>UNION vs UNION ALL</strong></summary>

 | 項目      | UNION             | UNION ALL        |
| ------- | ----------------- | ---------------- |
| 功能      | 合併兩個查詢結果並自動去除重複資料 | 合併兩個查詢結果，不去除重複資料 |
| 執行效率    | 較慢，因為需要去除重複並排序    | 較快，因為直接合併，不用去除重複資料   |
| 結果是否有重複 | 不會                | 可能會有重複           |
| 使用情境    | 想要合併且只要不重複的資料     | 想要合併且保留所有資料，包括重複 |
</details>

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

| 集合運算子          | 功能說明                | MySQL 不支持原因 | MySQL 替代方法                                          | 範例說明          |
| -------------- | ------------------- | ----------- | --------------------------------------------------- | ------------- |
| INTERSECT      | 取兩個查詢結果的交集（共有資料）    | MySQL 不支持   | 使用 `INNER JOIN` 或 `EXISTS`                          | 找出兩表中同時存在的資料  |
| EXCEPT / MINUS | 取第一個查詢結果中有、第二個沒有的資料 | MySQL 不支持   | 使用 `LEFT JOIN` + `WHERE ... IS NULL` 或 `NOT EXISTS` | 找出左表有但右表沒有的資料 |

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
