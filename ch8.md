# Chapter8: Advanced SQL
- Learn how to create a table and modify columns and constrains
- Learn how to manipulate the contents of the data, using SQL commands to insert, update, and delete rows of data 
- Learn how to use triggers and stored procedures to perform actions when a specific event occurs.
- Learn how SQL facilitates the application of business procedures when it is embedded in a programming language (Python as example).  

# Steps to Develop Database
1. Design ER model
2. Create database 
3. Create database **schema** (a logical group of database objects, like tables and indexes)
4. Insert data

# Create Table Syntax
```sql
CREATE TABLE tablename (
column1 data type [constraint] [,
column2 data type [constraint] ] [,
PRIMARY KEY (column1 [, column2]) ] [,
FOREIGN KEY (column1 [, column2]) REFERENCES tablename (column1 [, column2])] [,
CONSTRAINT constraint ] );
```

# Creating VENDOR Table
```sql
CREATE TABLE VENDOR (
V_CODE 		INTEGER,
V_NAME 		VARCHAR(35) NOT NULL,
V_CONTACT 	VARCHAR(15) NOT NULL,
V_AREACODE 	CHAR(3) NOT NULL,
V_PHONE 	CHAR(8) NOT NULL,
V_STATE 	CHAR(2) NOT NULL,
V_ORDER 	CHAR(1) NOT NULL,
PRIMARY KEY (V_CODE)); 
```

# Creating PRODUCT Table
```sql
CREATE TABLE PRODUCT (
P_CODE 	        VARCHAR(10),
P_DESCRIPT 	VARCHAR(35) NOT NULL,
P_INDATE 	DATETIME NOT NULL,
P_QOH 	        INTEGER NOT NULL,
P_MIN 		INTEGER NOT NULL,
P_PRICE 	NUMERIC(8,2) NOT NULL,
P_DISCOUNT 	NUMERIC(4,2) NOT NULL,
V_CODE 		INTEGER,
PRIMARY KEY (P_CODE)
FOREIGN KEY (V_CODE) REFERENCES VENDOR (V_CODE));
```

# The Order of Related Table Creation
- Because the PRODUCT table contains a foreign key that references the VENDOR table, create the VENDOR table first
- “M” side of a relationship always references the “1” side. Therefore, in a 1:M relationship, we always create the table for the “1” side first.
- Data insertion follow the same rule

<details>
  <summary><strong>整理</strong></summary>
  
### 1. 表格建立順序規則
- **「1」方優先原則**：在 1:M（一對多）關係中，必須先建立「1」方的表格（被參考的表），再建立「M」方（包含外來鍵的表格）。
  - *範例*：先建立 `VENDOR`（供應商，1方），再建立 `PRODUCT`（產品，M方），因為產品表需要引用供應商表的 `V_CODE` 作為外來鍵。

### 2. 外來鍵約束的依賴性
- **參考完整性限制**：外來鍵（Foreign Key）必須指向一個已存在的「主鍵」（Primary Key），因此被參考的表（父表）必須先存在。
  - *技術原因*：SQL 引擎會驗證外來鍵關係，若先建立「M」方表格會因找不到被參考的「1」方表格而報錯。

### 3. 資料插入順序
- **資料插入的層級性**：必須先向「1」方表格插入資料，才能在「M」方表格插入關聯資料。
  - *範例*：需先插入供應商資料（如 `V_CODE=123`），才能插入該供應商提供的產品資料（其 `V_CODE` 必須是已存在的值）。

### 4. 資料類型選擇原則
- **固定長度 vs 可變長度**：
  - 使用 `CHAR(n)` 當資料長度固定（如州代碼 `CA`、電話號碼），以提升存取效率。
  - 使用 `VARCHAR(n)` 當資料長度變化大（如姓名、地址），以節省儲存空間。

### 5. 實務設計建議
- **避免循環參考**：若表格 A 參考表格 B，表格 B 又參考表格 A，需特別處理（如延遲約束檢查）。
- **刪除時的級聯操作**：刪除「1」方資料時，需決定是否連動刪除「M」方資料（`ON DELETE CASCADE`）。


</details>

# Set SQL Constraints when Table Creating
- <span class="blue-text">PRIMARY KEY </span>constraint : not null and unique
- <span class="blue-text">FOREIGN KEY </span>constraint
  <span class="small-text">
  - You cannot delete a vendor from the VENDOR table if at least one product row references that vendor
  - *FOREIGN KEY (V_CODE) REFERENCES VENDOR (V_CODE) ON UPDATE CASCADE*
  - If you make a change in any VENDOR’s V_CODE that change is automatically applied to PRODUCT to maintain referential integrity
  </span>
- <span class="blue-text">NOT NULL</span> constraint
- <span class="blue-text">UNIQUE</span> constraint
- <span class="blue-text">DEFAULT</span> constraint
- <span class="blue-text">CHECK constraint</span>: validate data when an attribute value is entered
  <span class="small-text">
  - CUS_AREACODE CHAR(3) DEFAULT '615' NOT NULL CHECK(CUS_AREACODE IN ('615', '713', '931'))

<details>
  <summary><strong>On delete/On Update Cascade</strong></summary>
    
#### **1. ON DELETE CASCADE（級聯刪除）**
##### **作用**
當 **父表（1 方）** 的某筆記錄被刪除時，**自動刪除子表（M 方）** 中所有關聯的記錄。

##### **適用場景**
- 當父表的記錄被刪除時，子表的關聯記錄 **不再有意義**，應該一起刪除。
- 例如：
  - 刪除一個 `VENDOR`（供應商）時，自動刪除該供應商的所有 `PRODUCT`（產品）記錄。

##### **語法**
```sql
CREATE TABLE PRODUCT (
    P_ID INT PRIMARY KEY,
    P_NAME VARCHAR(50),
    V_CODE INT,
    FOREIGN KEY (V_CODE) 
        REFERENCES VENDOR(V_CODE) 
        ON DELETE CASCADE  -- 當 VENDOR 的某筆記錄被刪除，PRODUCT 的關聯記錄也會被刪除
);
```

##### **範例**
假設 `VENDOR` 表有一筆 `V_CODE = 101` 的供應商，並且 `PRODUCT` 表有 3 筆產品記錄關聯到它：
```sql
-- 刪除 VENDOR 的 V_CODE=101
DELETE FROM VENDOR WHERE V_CODE = 101;
```
**結果**：
- `VENDOR` 表中 `V_CODE=101` 的記錄被刪除。
- `PRODUCT` 表中所有 `V_CODE=101` 的產品記錄 **也會自動被刪除**。

#### **2. ON UPDATE CASCADE（級聯更新）**
##### **作用**
當 **父表（1 方）** 的 **主鍵（Primary Key）** 被修改時，**自動更新子表（M 方）** 的外來鍵值，使關聯性保持正確。

##### **適用場景**
- 當父表的主鍵需要變更時，子表的關聯外來鍵 **自動同步更新**。
- 例如：
  - 修改 `VENDOR` 的 `V_CODE`（供應商代碼）時，`PRODUCT` 表的 `V_CODE` 也會自動更新。

##### **語法**
```sql
CREATE TABLE PRODUCT (
    P_ID INT PRIMARY KEY,
    P_NAME VARCHAR(50),
    V_CODE INT,
    FOREIGN KEY (V_CODE) 
        REFERENCES VENDOR(V_CODE) 
        ON UPDATE CASCADE  -- 當 VENDOR 的 V_CODE 被修改，PRODUCT 的 V_CODE 也會自動更新
);
```

##### **範例**
假設 `VENDOR` 表的 `V_CODE=101` 被修改為 `V_CODE=999`：
```sql
-- 更新 VENDOR 的 V_CODE
UPDATE VENDOR SET V_CODE = 999 WHERE V_CODE = 101;
```
**結果**：
- `VENDOR` 表的 `V_CODE` 從 `101` 變成 `999`。
- `PRODUCT` 表中所有原本 `V_CODE=101` 的記錄，**自動變成 `V_CODE=999`**。
</details>

# Create Table INVOICE, LINE to Illustrate Constrains 
```sql
CREATE TABLE IF NOT EXISTS INVOICE (
  INV_NUMBER  INTEGER,
  CUS_CODE	INTEGER NOT NULL,
  INV_DATE  DATE NOT NULL,
  PRIMARY KEY (INV_NUMBER),
  FOREIGN KEY (CUS_CODE) REFERENCES CUSTOMER (CUS_CODE), 
  CONSTRAINT INV_CK1 CHECK (INV_DATE > '2012-01-01'));
  
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

# Create a Table with a SELECT Statement
- SQL provides a way to rapidly create a new table based on selected columns and rows of an existing table using a subquery
- All of the data rows returned by the SELECT statement are copied automatically
```sql
CREATE TABLE IF NOT EXISTS PART AS 
    SELECT P_CODE AS PART_CODE, P_DESCRIPT AS PART_DESCRIPT, P_PRICE AS PART_PRICE, V_CODE
    FROM PRODUCT;
```

##### **語句拆解**
```sql
CREATE TABLE IF NOT EXISTS PART AS 
    SELECT P_CODE AS PART_CODE, P_DESCRIPT AS PART_DESCRIPT, P_PRICE AS PART_PRICE, V_CODE
    FROM PRODUCT;
```

1. **`CREATE TABLE IF NOT EXISTS PART`**  
   - 創建一個名為 `PART` 的新表。
   - `IF NOT EXISTS` 是條件判斷，僅當 `PART` 表不存在時才執行創建，避免重複建表導致錯誤。

2. **`AS SELECT ... FROM PRODUCT`**  
   - 新表 `PART` 的結構和數據來源於 `SELECT` 查詢的結果。
   - 這裡是從 `PRODUCT` 表中選取 4 個欄位，並對其中 3 個欄位進行 **重新命名**（Alias）。

3. **欄位映射關係**：
   | 原欄位 (`PRODUCT`) | 新欄位 (`PART`) | 說明                     |
   |---------------------|------------------|--------------------------|
   | `P_CODE`            | `PART_CODE`      | 產品編號，改名為零件編號  |
   | `P_DESCRIPT`        | `PART_DESCRIPT`  | 產品描述，改名為零件描述  |
   | `P_PRICE`           | `PART_PRICE`     | 產品價格，改名為零件價格  |
   | `V_CODE`            | `V_CODE`         | 供應商代碼（保持原名）    |

##### **執行結果**
1. **新表結構**：  
   `PART` 表將包含 4 個欄位：
   - `PART_CODE`（來自 `P_CODE`）
   - `PART_DESCRIPT`（來自 `P_DESCRIPT`）
   - `PART_PRICE`（來自 `P_PRICE`）
   - `V_CODE`（直接複製，未改名）

2. **數據內容**：  
   `PART` 表的數據是 `PRODUCT` 表中所有記錄的 **完整複製**（但僅包含選定的 4 個欄位）。

3. **約束與索引**：  
   - 新表 `PART` **不會自動繼承** 原表 `PRODUCT` 的主鍵、外來鍵或索引。
   - 如需約束，需額外手動添加（例如：`ALTER TABLE PART ADD PRIMARY KEY (PART_CODE);`）。

##### **適用場景**
這種語法常用於：
1. **快速備份或子集提取**：從大表中提取部分欄位或數據創建新表。
2. **欄位名稱調整**：在複製數據時重新命名欄位，使結構更符合新需求。
3. **臨時表創建**：為特定分析任務創建中間表，避免影響原表。

##### **注意事項**
1. **數據一致性**：  
   - 新表 `PART` 的數據是執行時的 **靜態快照**，後續原表 `PRODUCT` 的更新不會同步到 `PART`。
   - 若需動態同步，應改用 **視圖（VIEW）** 而非實體表。

2. **外來鍵問題**：  
   - 如果 `PRODUCT` 表的 `V_CODE` 是外來鍵，新表 `PART` 的 `V_CODE` **不會自動繼承外來鍵約束**，需手動添加：
     ```sql
     ALTER TABLE PART 
     ADD FOREIGN KEY (V_CODE) REFERENCES VENDOR(V_CODE);
     ```

3. **性能考量**：  
   - 當 `PRODUCT` 表數據量龐大時，此操作可能耗時，建議在離峰時段執行。

##### **延伸應用**
如果想 **僅複製結構不複製數據**（創建空表）：
```sql
CREATE TABLE IF NOT EXISTS PART AS 
    SELECT P_CODE AS PART_CODE, P_DESCRIPT AS PART_DESCRIPT, P_PRICE AS PART_PRICE, V_CODE
    FROM PRODUCT
    WHERE 1=0;  -- 條件永遠不成立，故不複製數據
```

# SQL Index
- Indexes can be used to improve the efficiency of searches (**索引類似書本的目錄**)
and to avoid duplicate column values
```sql
CREATE INDEX P_INDATEX ON PRODUCT(P_INDATE);
--在 PRODUCT 表的 P_INDATE 欄位上建立一個 普通索引（允許重複值）。加速對 P_INDATE 的查詢（如 WHERE P_INDATE = '2023-01-01' 或排序操作）。
DROP INDEX P_INDATEX ON PRODUCT;
CREATE UNIQUE INDEX P_CODEX ON PRODUCT(P_CODE);
--加速查詢、限制唯一性
DROP INDEX P_CODEX ON PRODUCT;
CREATE INDEX PROD_PRICEX ON PRODUCT(P_PRICE DESC);
--優化按 P_PRICE DESC（價格降序）的查詢
DROP INDEX PROD_PRICEX ON PRODUCT;
```
# MySQL Index
- MySQL allows several types of indexes like primary key index, unique index, normal index (non-unique index, ordinary index, index without constraints) and full-text index.
- The indexes improve SELECT queries speed tremendously. but, they do have some considerable disadvantages as well.
- Advantage
  - Query optimization
  - Uniqueness help to avoid duplicate row data.
- Disadvantage
  - Indexes take up disk space
  - Slow down the speed of writing queries, such as INSERT, UPDATE and DELETE

<details>
  <summary><strong>舉例</strong></summary>
  
#### **範例數據表 `PRODUCT` (假設有 10,000 筆資料)**
| P_CODE  | P_NAME      | P_PRICE | P_INDATE   | V_CODE |
|---------|------------|---------|------------|--------|
| P001    | Laptop     | 1200    | 2023-01-01 | V100   |
| P002    | Phone      | 800     | 2023-02-15 | V101   |
| P003    | Tablet     | 600     | 2023-03-10 | V100   |
| ... (共 10,000 筆) ... |

#### **情境 1：普通索引加速查詢（WHERE 條件）**
##### **無索引時**
```sql
SELECT * FROM PRODUCT WHERE P_NAME = 'Phone';
```
- **執行方式**：資料庫必須 **逐筆掃描 10,000 筆記錄**（全表掃描，效能差）。
- **耗時**：約 100 ms（假設）。

##### **有索引時**
```sql
-- 先建立索引
CREATE INDEX IDX_P_NAME ON PRODUCT(P_NAME);

-- 再次執行相同查詢
SELECT * FROM PRODUCT WHERE P_NAME = 'Phone';
```
- **執行方式**：資料庫直接從索引樹查找 `P_NAME = 'Phone'`，**只需讀取 1 筆記錄**。
- **耗時**：約 1 ms（提升 100 倍速度）。

#### **情境 2：唯一索引避免重複（INSERT 檢查）**
##### **無唯一索引時**
```sql
INSERT INTO PRODUCT (P_CODE, P_NAME) VALUES ('P001', 'Gaming PC');
```
- **執行方式**：資料庫需掃描所有 `P_CODE` 確認是否重複（全表掃描）。
- **問題**：若資料量大，檢查會很慢，且可能意外插入重複值。

##### **有唯一索引時**
```sql
-- 先建立唯一索引
CREATE UNIQUE INDEX UQ_P_CODE ON PRODUCT(P_CODE);

-- 嘗試插入重複值
INSERT INTO PRODUCT (P_CODE, P_NAME) VALUES ('P001', 'Gaming PC');
```
- **執行方式**：資料庫透過索引 **立即檢查 `P_CODE` 是否存在**。
- **結果**：直接報錯 `Duplicate entry 'P001'`，避免資料不一致。

#### **情境 3：降序索引優化排序（ORDER BY）**
##### **無索引時**
```sql
SELECT * FROM PRODUCT ORDER BY P_PRICE DESC LIMIT 10;
```
- **執行方式**：資料庫需 **先排序 10,000 筆記錄**，再回傳前 10 筆。
- **耗時**：約 500 ms（需臨時排序，效能差）。

##### **有降序索引時**
```sql
-- 先建立降序索引
CREATE INDEX IDX_PRICE_DESC ON PRODUCT(P_PRICE DESC);

-- 再次執行查詢
SELECT * FROM PRODUCT ORDER BY P_PRICE DESC LIMIT 10;
```
- **執行方式**：資料庫 **直接從索引按價格降序讀取前 10 筆**（無需額外排序）。
- **耗時**：約 5 ms（提升 100 倍速度）。
</details>
  
# Illustrate Index
<img width="650" alt="image" src="https://github.com/user-attachments/assets/aabae70f-cfcf-4420-a255-1c19278ffa89" />
<img width="450" alt="image" src="https://github.com/user-attachments/assets/9fd00a84-d5ca-4208-a3b8-92320d47aaf5" />

# Altering Table Structures
- All changes in the table structure are made by using the ALTER TABLE command with three options: ADD, MODIFY, and DROP
- Changing a column’s data type
- Changing a column’s data characteristics
- Adding a column
- Adding primary key, foreign key, and check constraints
- Dropping a column
- Deleting a table from the database

# Changing a Column’s Data Type
```sql
ALTER TABLE PRODUCT
    MODIFY V_CODE CHAR(5);

ALTER TABLE PRODUCT
    MODIFY P_DESCRIPT VARCHAR(10);    

-- if V_CODE is a FOREIGN KEY, it will fail. (可能會破壞referential integrity)
-- if V_CODE contains data that cannot be converted, it will fail.
-- if data truncation occurs, it will fail
```
# Changing a Column’s Data Characteristics
```sql
ALTER TABLE PRODUCT
MODIFY P_PRICE DECIMAL(9,2);
```
- Some DBMSs impose limitations on changing data type or data characteristics.
  - Increase (but not decrease) the size of a column
  - Attribute changes can be made only when there is no data in the attribute.

# Adding a Column
```sql
ALTER TABLE PRODUCT
    ADD P_SALECODE CHAR(1);
```
- Do not add NOT NULL as constrain
- **新增非空欄位（NOT NULL）時，必須要有預設值或立刻給所有舊資料填值，否則會失敗**

# Adding Primary Key, Foreign Key, and Check Constraints
```sql
CREATE TABLE IF NOT EXISTS PART AS 
    SELECT P_CODE AS PART_CODE, P_DESCRIPT AS PART_DESCRIPT, P_PRICE AS PART_PRICE, V_CODE
    FROM PRODUCT;

ALTER TABLE PART
    ADD PRIMARY KEY (PART_CODE);

ALTER TABLE PART
    ADD FOREIGN KEY (V_CODE) REFERENCES VENDOR (V_CODE);

ALTER TABLE PART
    ADD CHECK (PART_PRICE >= 0);

ALTER TABLE PART
    ADD PRIMARY KEY (PART_CODE),
    ADD FOREIGN KEY (V_CODE) REFERENCES VENDOR (V_CODE),    
    ADD CHECK (PART_ PRICE >= 0);
```

# Dropping a Column
```sql
ALTER TABLE VENDOR
    DROP COLUMN V_ORDER;
```

# Dropping a Table
```sql
DROP TABLE PART;
```

# Data Manipulation Commands (INSERT)
```sql
INSERT INTO tablename VALUES (value1, value2, …, valuen)

INSERT INTO VENDOR
    VALUES (21225,'Bryson, Inc.','Smithson','615','223-3234','TN','Y');
INSERT INTO VENDOR
    VALUES (21226,'Superloo, Inc.','Flushing','904','215-8995','FL','N');

SELECT * FROM VENDOR

INSERT INTO PRODUCT
    VALUES ('BRT-345','Titanium drill bit','18-Oct-15', 75, 10, 4.50, 0.06, NULL);

INSERT INTO PRODUCT(P_CODE, P_DESCRIPT) 
    VALUES ('BRT-345','Titaniumdrill bit');    
```

# Inserting Table Rows with a SELECT Subquery
```sql
CREATE TABLE PART (
  PART_CODE CHAR(8),
  PART_DESCRIPT CHAR(35),
  PART_ PRICE DECIMAL(8,2),
  V_CODE INTEGER,
  PRIMARY KEY (PART_CODE));

INSERT INTO PART (PART_CODE, PART_DESCRIPT, PART_PRICE, V_CODE)
  SELECT P_CODE, P_DESCRIPT, P_PRICE, V_CODE
  FROM PRODUCT;
```

# Saving Table Changes
- Any changes made to the table contents are not saved on disk until you (1)close database (2)close the program you are using (3) use the COMMIT command
- The COMMIT command permanently saves all changes—such as rows added, attributes modified, and rows deleted made to any table in the database.
- The COMMIT command’s purpose is not just to save changes. The ultimate purpose of the COMMIT and ROLLBACK commands is to ensure database update integrity in transaction management.
- By default, MySQL also automatically commits changes with each command. However, if START TRANSACTION or BEGIN is placed at the beginning of a series of commands, MySQL will delay committing the commands until the COMMIT or ROLLBACK command is issued.

1. **任何對資料表的修改，在以下情況之前不會實際儲存到硬碟：**  
   - (1) 關閉資料庫  
   - (2) 關閉正在使用的程式  
   - (3) 執行 `COMMIT` 命令  

2. **`COMMIT` 命令的功能：**  
   - 永久保存所有變更（例如新增資料列、修改屬性、刪除資料列）。  
   - 不僅僅是「儲存變更」，其核心目的是與 `ROLLBACK` 共同確保 **交易管理（Transaction Management）中的資料完整性**。  

3. **MySQL 的預設行為：**  
   - 預設情況下，MySQL 會自動提交（Auto-Commit）每一條指令的變更。  
   - 但如果使用 `START TRANSACTION` 或 `BEGIN` 開啟一個交易，MySQL 會暫停自動提交，直到明確執行 `COMMIT`（確認）或 `ROLLBACK`（撤銷）。  

##### **關鍵概念解釋**  

##### **1. 交易的原子性（Atomicity）**  
- **`COMMIT` 和 `ROLLBACK` 的作用**：  
  - 將多個操作捆綁為一個「不可分割的單元」（交易）。  
  - 只有執行 `COMMIT` 後，所有變更才會永久生效；若中途失敗，可用 `ROLLBACK` 撤銷所有未提交的變更。  
  - **範例**：  
    ```sql
    START TRANSACTION;  -- 開始交易
    UPDATE accounts SET balance = balance - 100 WHERE user = 'A';  -- A 轉出 100
    UPDATE accounts SET balance = balance + 100 WHERE user = 'B';  -- B 收到 100
    COMMIT;  -- 確認交易（兩筆操作同時生效）
    ```
    - 如果沒有 `COMMIT`，第二條 SQL 失敗時，第一條操作也會被撤銷，避免金額不一致。  

##### **2. MySQL 的自動提交（Auto-Commit）**  
- **預設行為**：  
  - 每執行一條 SQL（如 `INSERT`、`UPDATE`），MySQL 會自動執行隱含的 `COMMIT`，變更立即生效。  
  - **優點**：簡單易用；**缺點**：無法撤銷已執行的操作。  

- **手動控制交易**：  
  - 使用 `START TRANSACTION` 關閉自動提交，後續操作需明確 `COMMIT` 或 `ROLLBACK`。  
  - **範例**：  
    ```sql
    SET autocommit = 0;  -- 關閉自動提交（等同 START TRANSACTION）
    DELETE FROM orders WHERE date < '2020-01-01';
    ROLLBACK;  -- 發現刪錯資料，撤銷操作
    ```

##### **3. 何時需要手動 `COMMIT`？**  
- **確保資料一致性**：例如銀行轉帳、庫存扣減等需多步驟完成的業務邏輯。  
- **批次處理大量資料**：避免部分成功、部分失敗的混亂狀態。  

##### 結論:
- **`COMMIT` = 確認變更**，**`ROLLBACK` = 撤銷變更**，兩者共同維護交易完整性。  
- MySQL 預設自動提交，但重要操作建議用 `START TRANSACTION` 明確控制交易範圍。  
- 實際應用中，ORM 框架（如 Django、Hibernate）通常會自動處理交易，但開發者仍需理解底層機制。
  
# Updating Table Rows
```sql
UPDATE PRODUCT
SET P_INDATE = '2022-01-18'
WHERE P_CODE = '13-Q2/P2';

UPDATE PRODUCT
SET P_INDATE = '2022-01-18', P_PRICE = 17.99, P_MIN = 10
WHERE P_CODE = '13-Q2/P2';

UPDATE PRODUCT
SET P_SALECODE = '1'
WHERE P_CODE IN ('2232/QWE', '2232/QTY');

-- SET SQL_SAFE_UPDATES = 0;
UPDATE PRODUCT
SET P_PRICE = P_PRICE * 1.10
WHERE P_PRICE < 50.00
```

# Deleting Table Rows
```sql
DELETE FROM PRODUCT
WHERE P_CODE = 'BRT-345';
```

# Restoring Table Contents
The ROLLBACK command is used to restore the database table contents to the condition that existed after the last COMMIT statements.

# Transaction Example
A transaction: Jacky transfer $100 to Andy
```sql
CREATE TABLE IF NOT EXISTS ACCOUNT (
  ACCT_NUM  CHAR(5),
  OWNER_NAME  VARCHAR(15),
  BALANCE DECIMAL(9,2),
  PRIMARY KEY (ACCT_NUM));
INSERT INTO ACCOUNT VALUES ('00001','Jacky', 1000);
INSERT INTO ACCOUNT VALUES ('00002','Andy', 500);
SET AUTOCOMMIT = 0;
UPDATE ACCOUNT SET BALANCE = (BALANCE - 100)
WHERE ACCT_NUM = '00001';
UPDATE ACCOUNT SET BALANCE = (BALANCE + 100)
WHERE ACCT_NUM = '00002';
ROLLBACK;
COMMIT;
SET AUTOCOMMIT = 1;
```
##### **1. 程式碼流程總覽**
這段 SQL 模擬「銀行轉帳」交易流程：
1. 建立帳戶表格並存入兩筆資料（Jacky 帳戶 1000 元、Andy 帳戶 500 元）
2. **關閉自動提交**（`SET AUTOCOMMIT = 0`）開始手動控制交易
3. 執行轉帳：
   - 從 Jacky 帳戶扣 100 元
   - 向 Andy 帳戶加 100 元
4. 先執行 `ROLLBACK`（撤銷變更），再執行 `COMMIT`（確認變更）
5. 最後恢復自動提交（`SET AUTOCOMMIT = 1`）

#### **2. ROLLBACK 的作用**
##### **當執行到 `ROLLBACK` 時：**
```sql
UPDATE ACCOUNT SET BALANCE = (BALANCE - 100) WHERE ACCT_NUM = '00001';  -- Jacky: 1000→900
UPDATE ACCOUNT SET BALANCE = (BALANCE + 100) WHERE ACCT_NUM = '00002';  -- Andy: 500→600
ROLLBACK;  -- 關鍵動作！
```
- **所有尚未提交的變更會被撤銷**  
  - Jacky 的餘額恢復為 **1000 元**（原本已扣到 900）  
  - Andy 的餘額恢復為 **500 元**（原本已加到 600）  
- **資料庫狀態回到交易開始前**，如同轉帳從未發生。  

##### **使用時機**  
- 發現操作錯誤時（例如轉錯帳號、金額輸入錯誤）  
- 交易中途發生系統錯誤，確保資料一致性  

#### **3. COMMIT 的作用**
##### **當執行到 `COMMIT` 時：**
```sql
UPDATE ACCOUNT SET BALANCE = (BALANCE - 100) WHERE ACCT_NUM = '00001';  -- Jacky: 1000→900
UPDATE ACCOUNT SET BALANCE = (BALANCE + 100) WHERE ACCT_NUM = '00002';  -- Andy: 500→600
COMMIT;  -- 關鍵動作！
```
- **永久保存所有變更**  
  - Jacky 的餘額 **確定變為 900 元**  
  - Andy 的餘額 **確定變為 600 元**  
- 變更會寫入硬碟，即使程式關閉或斷電也不會消失  

##### **使用時機**  
- 確認所有操作正確無誤後  
- 交易完整執行完畢時（例如轉帳雙方餘額都更新成功）  


#### **4. 對照範例說明**
##### **情境：轉帳過程發生錯誤**
```sql
START TRANSACTION;
UPDATE ACCOUNT SET BALANCE = BALANCE - 100 WHERE ACCT_NUM = '00001';  -- 成功
UPDATE ACCOUNT SET BALANCE = BALANCE + 100 WHERE ACCT_NUM = '99999';  -- 帳號不存在，失敗！
ROLLBACK;  -- 自動撤銷第一筆扣款，Jacky 的錢不會消失！
```
- 如果沒有 `ROLLBACK`，Jacky 會被扣款但 Andy 沒收到錢，導致資料不一致。

#### **5. 為什麼需要手動控制交易？**
- **預設自動提交的風險**：  
  ```sql
  SET AUTOCOMMIT = 1;  -- MySQL 預設
  UPDATE ACCOUNT SET BALANCE = BALANCE - 100 WHERE ACCT_NUM = '00001';  -- 立刻生效，無法撤銷！
  ```
  - 若第二筆操作失敗，第一筆扣款已無法挽回。  

- **手動交易的正確寫法**：  
  ```sql
  SET AUTOCOMMIT = 0;
  START TRANSACTION;
  -- 執行多筆操作...
  COMMIT;  -- 或 ROLLBACK;
  SET AUTOCOMMIT = 1;
  ```

<details>
  <summary><strong>實務中的正確寫法</strong></summary>
  
##### **1. 這樣寫的「實際效果」**
- **`ROLLBACK` 會直接撤銷前面的所有更新**：  
  - Jacky 的餘額恢復為 **1000 元**（不會變成 900）  
  - Andy 的餘額恢復為 **500 元**（不會變成 600）  
- **接著的 `COMMIT` 會提交「空操作」**：  
  - 因為 `ROLLBACK` 已經清空了交易內的變更，此時提交不會改變任何資料。  
- **最終結果**：資料庫內容與交易開始前完全一致，如同沒執行過任何操作。

##### **2.實務中的寫法**
```sql
SET AUTOCOMMIT = 0;
START TRANSACTION;

-- 嘗試轉帳
UPDATE ACCOUNT SET BALANCE = BALANCE - 100 WHERE ACCT_NUM = '00001';  -- Jacky 扣款
UPDATE ACCOUNT SET BALANCE = BALANCE + 100 WHERE ACCT_NUM = '00002';  -- Andy 收款

-- 檢查是否成功
IF (沒有錯誤) THEN
    COMMIT;  -- 確認轉帳
    PRINT '轉帳成功';
ELSE
    ROLLBACK;  -- 撤銷轉帳
    PRINT '轉帳失敗，已復原';
END IF;

SET AUTOCOMMIT = 1;
```
</details>

# Virtual Tables: Creating a View
- A view is a virtual table based on a SELECT query that is saved as an object in the database
- View（視圖） 是一種虛擬資料表，它是根據一個 SELECT 查詢語句所建立的。這個查詢會被儲存在資料庫中，以後就可以像查詢資料表一樣來查詢這個 View。
- A base table is the table on which a view is based
- View 是根據「基礎資料表（Base Table）」來產生的，View 本身不儲存資料，它只是從一個或多個實際存在的資料表中讀取資料。
  
```sql
CREATE VIEW PROD_STATS AS
SELECT V_CODE, 
       SUM(P_QOH*P_PRICE) AS TOTCOST, 
       MAX(P_QOH) AS MAXQTY, 
       MIN(P_QOH) AS MINQTY, 
       AVG(P_QOH) AS AVGQTY
FROM PRODUCT
GROUP BY V_CODE;

SELECT * 
FROM PROD_STATS
--建立一個名為 PROD_STATS 的 View，它會把 PRODUCT 資料表裡的資料依照供應商代號（V_CODE）分組，計算各供應商的商品統計資訊
```

<details>
  <summary><strong>VIEW的特性</strong></summary>
    
| 特點            | 說明                                                            |
| ------------- | ------------------------------------------------------------- |
| **即時更新**   | View 不儲存資料，它每次查詢時都會根據底層資料表（base table）的最新資料自動更新。<br>→ 不怕資料過時。 |
| **節省空間**   | View 只是儲存 SQL 語法，不會重複儲存查詢結果資料。                                |
| **增加安全性** | 可以用 View 控制使用者能看到哪些欄位或資料，避免直接開放整個 base table。                 |
| **簡化複雜查詢** | 把複雜的 SELECT 包起來，下次只要 `SELECT * FROM view_name` 就好，增加可讀性與維護性。  |
</details>

# MySQL View
In MySQL, a VIEW is a virtual table based on the result of a SELECT query. It does not store data, but presents data from one or more tables in a structured way.

Rule / Feature | Description
---------------|------------
Virtual Table | Views do not store data — only the SQL logic is saved.
Read-Only or Updatable | Simple views (from one table, no aggregates, no DISTINCT, no GROUP BY, etc.) are usually updatable. Complex views are read-only.
Column Aliases Allowed | You can rename columns in the view. <br>CREATE VIEW view_name (alias1, alias2) AS SELECT col1, col2 FROM table_name;
Nested Views | Allow to create a view based on another view.
View Dependencies | Dropping an base table breaks the view.
Indexed Views Not Supported | Views in MySQL cannot have indexes.

| 規則 / 特性                              | 說明                                                                                             |
| ------------------------------------ | ---------------------------------------------------------------------------------------------- |
| 虛擬資料表（Virtual Table）                 | View（視圖）本身**不儲存資料**，它只儲存 SQL 查詢邏輯。                                                             |
| 唯讀或可更新（Read-Only or Updatable）       | 簡單的視圖（例如只從一個資料表選擇，沒有聚合函數、`DISTINCT`、`GROUP BY` 等）通常是**可更新**的；但複雜的視圖則是**唯讀**。                   |
| 可使用欄位別名（Column Aliases Allowed）      | 你可以在建立視圖時**重新命名欄位**。<br>例如：<br>`CREATE VIEW view_name (別名1, 別名2) AS SELECT 欄位1, 欄位2 FROM 資料表;` |
| 可巢狀視圖（Nested Views）                  | 可以建立**以其他視圖為基礎的視圖**（即視圖套視圖）。                                                                   |
| 視圖的相依性（View Dependencies）            | **如果刪除視圖所依賴的資料表**（base table），這個視圖會失效（無法再使用）。                                                  |
| 不支援索引視圖（Indexed Views Not Supported） | 在 MySQL 中，**視圖不能建立索引**（不像某些其他資料庫，例如 SQL Server）。                                               |

# Auto Increment in MySQL
- In MySQL, you may set one and only one column with the AUTO_INCREMENT property. If you set one, the column must be defined as the primary key of the table

```sql
-- In MySQL
create table arena (
    arena_id          int  auto_increment, --自動產生流水號，一個資料表只能有一個欄位能設，設完變主鍵
    arena_name        varchar(100),
    location          varchar(100),
    seating_capacity  int,
    primary key (arena_id));
-- Loading the data without having to manage arena_id column
insert into arena (arena_name, location, seating_capacity)
values ('Madison Square Garden', 'New York', 20000); --第一筆給 arena_id = 1
insert into arena (arena_name, location, seating_capacity)
values ('Dean Smith Center', 'North Carolina', null); --第二筆給 arena_id = 2
```

# Sequences in Oracle
- In Oracle, a sequence is an object for generating unique segment values for a column

```sql
-- In Oracle
CREATE SEQUENCE CUS_CODE_SEQ START WITH 20010 NO CACHE;

INSERT INTO CUSTOMER
VALUES (CUS_CODE_SEQ.NEXTVAL, 'Connery', 'Sean', NULL, '615', '898-2007', 0.00);
```

# Procedural SQL
- <span class="blue-text">Procedural SQL </span>is an extension of SQL that adds procedural programming capabilities (variables, if, loop) to SQL and is designed to run inside the database
- Procedural code is executed as a unit by the DBMS when it is invoked by the end user
- End users can use procedural SQL to create the following:
  - Stored function (or user defined function)
  - Stored procedures
  - Triggers

# State_Population Table
```sql
create database population;
use population;
create table state_population(state varchar(100), population  int);
insert into state_population values ('New York',	19299981);
insert into state_population values ('Texas',			29730311);
insert into state_population values ('California',39613493);
insert into state_population values ('Florida', 	21944577);
insert into state_population values ('New Jersey', 9267130);
insert into state_population values ('Massachusetts', 6893000);
insert into state_population values ('Rhode Island', 1097379);
```

# Procedural SQL Used in Stored Function
```sql
use population;
drop function if exists f_get_state_population;

delimiter //
create function f_get_state_population(state_param varchar(100))
    returns int  -- returns an integer: population
    deterministic -- always return the same output for the same input (important for caching and optimization)
    reads sql data -- read data from the database, not modify it
    begin
        declare population_var int; -- local variable to store the retrieved population.
        select  population
            into    population_var
            from    state_population
            where   state = state_param;
        return(population_var);
    end//
delimiter ;

-- Call function
select f_get_state_population('New York');

-- Call function from a WHERE clause
select  *
from    state_population
where   population > f_get_state_population('New York');
```

# Stored Procedures
- A stored procedure is a named collection of procedural and SQL statements
- Stored procedures substantially reduce network traffic and increase performance
- Stored procedures help reduce code duplication by means of code isolation and code sharing 

# Country_Population Table
```sql
use population;
create table county_population (state char(50), county varchar(100), population int);

insert into county_population values ('New York',	'Kings',		2736074);
insert into county_population values ('New York',	'Queens',		2405464);
insert into county_population values ('New York',	'New York',		1694251);
insert into county_population values ('New York',	'Suffolk',		1525920);
insert into county_population values ('New York',	'Bronx',		1472654);
insert into county_population values ('New York',	'Nassau',		1395774);
insert into county_population values ('New York',	'Westchester',	1004457);
```

# Procedural SQL Used in Stored Procedures
```sql
use population;
drop procedure if exists p_set_and_show_state_population;

delimiter //
create procedure p_set_and_show_state_population(in state_param varchar(100))
    begin
        declare population_var int;
        delete from state_population where state = state_param;
        select sum(population) into   population_var
            from   county_population
            where  state = state_param;
        insert into state_population(state,population) values(state_param, population_var);
        select concat('Setting the population for ', state_param, ' of ', population_var);
    end//
delimiter ;

-- Call the p_set_and_show_state_population() procedure
set SQL_SAFE_UPDATES = 0;
call p_set_and_show_state_population('New York');
set SQL_SAFE_UPDATES = 1;
```
# Compare Stored Function and Stored Procedure
Use Case | Stored Procedure | Stored Function
---------|------------------------|----------------------
Modify data (INSERT, UPDATE, DELETE)?|Yes|No (only SELECT)
Return value?|Out parameters|Return statement
Use inside a SELECT statement?|No|Yes
DETERMINISTIC / NOT DETERMINISTIC?|Optional|Yes
Invocation| CALL statement |within SQL statements

# Conditional Execution
```sql
use population;
drop procedure if exists p_compare_population;
delimiter //
create procedure p_compare_population(in state_param varchar(100))
    begin
        declare state_population_var int;
        declare county_population_var int;
        select  population into state_population_var
            from    state_population
            where   state = state_param;
        select sum(population) into county_population_var
            from   county_population
            where  state = state_param;
        if (state_population_var = county_population_var) then
            select 'The population values match';
        else
            select 'The population values are different';
        end if; -- If you want to display one of THREE messages, use the if/elseif/else
    end//
delimiter ;
call p_compare_population('New York'); -- Call the p_compare_population() procedure
```

# Iteration or Looping
```sql
use population;
drop procedure if exists p_more_sensible_loop;
delimiter //
create procedure p_more_sensible_loop()
    begin
        declare cnt int default 0;
        msl: loop
            select concat('Looping Again ', cnt);
            set cnt = cnt + 1;
            if cnt = 3 then 
                leave msl;
            end if;
        end loop msl;
    end//
delimiter ;

-- Call the procedure p_more_sensible_loop()
call p_more_sensible_loop();
```

# SELECT Processing with Cursors
- A cursor is a special construct used to hold data rows returned by a SQL query
- To create an explicit cursor, you use the following syntax:
  DECLARE cursor_name CURSOR FOR select-query;
- Cursor-style processing involves retrieving data from the cursor one row at a time and copied to variables

# Cursor Example (p_split_big_ny_counties.sql)
```sql
use population;
drop procedure if exists p_split_big_ny_counties;
delimiter //
create procedure p_split_big_ny_counties()
    begin
        declare  v_state       varchar(100);
        declare  v_county      varchar(100);
        declare  v_population  int;
        declare done bool default false;
        declare county_cursor cursor for select  state, county, population
                                         from    county_population
                                         where   state = 'New York' and population > 2000000;
        declare continue handler for not found set done = true;   
        open county_cursor;
        fetch_loop: loop
            fetch county_cursor into v_state, v_county, v_population;
            if done then
                leave fetch_loop;
            end if;
            set @cnt = 1;
            
            split_loop: loop
                insert into county_population (state, county, population)
                    values (v_state,concat(v_county,'-',@cnt), round(v_population/2));
                set @cnt = @cnt + 1;
                if @cnt > 2 then
                    leave split_loop;
                end if;
            end loop split_loop;
    
            -- delete the original county
            delete from county_population where state = v_state and county = v_county;
        end loop fetch_loop;
        close county_cursor;
end//
delimiter ;
set SQL_SAFE_UPDATES = 0;
call p_split_big_ny_counties;
set SQL_SAFE_UPDATES = 1;

```
# Stored Procedures with Parameters
- One of the most valuable features of working with stored procedures is their ability to use parameters
- A parameter is a value that is provided to the program at the time of execution
<div class="middle-grid">
    <img src="restricted/CFig08_21.jpg" alt="">
</div>

# Procedural SQL Used in Triggers
A trigger is a procedural SQL code automatically invoked by the relational DBMS when a data manipulation event occurs
- Trigger is invoked before or after a row is inserted, updated, or deleted (not select)
  - Fire trigger after rows are changed: audit data
  - Fire trigger before rows are changed: affect data
- A trigger is associated with a database table
- Each database table may have one or more triggers
- A trigger is executed as part of the transaction that triggered it
- Triggers are critical to proper database operation and management

# Triggers After Row Changed That Audit Data
Using triggers to track changes to a table (payable) by creating another audit table (payable_audit) that logs who change what and when.
- After insert triggers
- After delete triggers
- After update triggers

# Accounting Database
Table payable and payable_audit
```sql
create database accounting;
use accounting;
create table payable
	(payable_id  int,
	 company  varchar(100),
	 amount  numeric(8,2),
	 service  varchar(100));
insert into payable
	(	payable_id, company, amount, service)
values
	(1, 'Acme HVAC', 		 	 123.32,	'Repair of Air Conditioner'),
	(2, 'Initech Printers',		1459.00,	'New Printers'),
	(3, 'Hooli Cleaning',		4398.55,	'Janitorial Services');
create table payable_audit
	(audit_datetime	datetime,
	audit_user varchar(50),
	audit_change varchar(500));
```
# After Insert Triggers
Naming convention: tr_payable_ai = trigger payable after insert
```sql
drop trigger if exists tr_payable_ai;
delimiter //
create trigger tr_payable_ai after insert on payable
for each row
begin
  insert into payable_audit
	(audit_datetime,
   audit_user,
   audit_change)
  values
  (now(), user(), 
	 concat(
	   'New row for payable_id ', new.payable_id,
		 '. Company: ', new.company,
		 '. Amount: ', new.amount,
		 '. Service: ', new.service));
end//
delimiter ;
```

# Test Trigger: tr_payable_ai
```sql
-- Insert a row into the payable table to test the insert trigger
insert into payable
	(payable_id, company, amount, service)
values
	(4, 'Sirius Painting', 451.45, 'Painting the lobby');
	
-- Did a row get logged in the payable_audit table showing what was inserted into the payable table?
select * from payable_audit;
```

# After Delete Triggers
```sql
use accounting;
drop trigger if exists tr_payable_ad;
delimiter //
create trigger tr_payable_ad after delete on payable
for each row
begin
  insert into payable_audit
    (audit_datetime, audit_user, audit_change)
  values
    (now(), user(),
     concat(
        'Deleted row for payable_id ', old.payable_id,
        '. Company: ', old.company,
        '. Amount: ', old.amount,
        '. Service: ', old.service));
end//
delimiter ;	
```
# Test Trigger: tr_payable_ad
```sql
delete from payable where company = 'Sirius Painting';

select * from payable_audit;
```

# After Update Triggers
```sql
delimiter //
create trigger tr_payable_au after update on payable
for each row
begin
  set @change_msg = 
	concat('Updated row for payable_id ', old.payable_id);
  if (old.company != new.company) then
    set @change_msg = 
	  concat(@change_msg, '. Company changed from ', old.company, ' to ', new.company);
  end if;
  if (old.amount != new.amount) then
    set @change_msg = 
	  concat(@change_msg, '. Amount changed from ', old.amount, ' to ', new.amount);
  end if;
  if (old.service != new.service) then
    set @change_msg = 
	  concat(@change_msg, '. Service changed from ', old.service, ' to ', new.service);
  end if;
  insert into payable_audit
	(audit_datetime, audit_user, audit_change)
  values(now(), user(), @change_msg);
end//
delimiter ;
```

# Test Trigger: tr_payable_au
```sql
update payable
set    amount = 100000,
       company = 'House of Larry'
where  payable_id = 3;

-- Did the update get logged?
select * from payable_audit;
```

# Triggers Before Row Changed That Affect Data
- Before insert triggers
- Before delete triggers
- Before update triggers

# Bank Database
Table credit
```sql
create database bank;

use bank;

create table credit
	(
	customer_id		int,
	customer_name	varchar(100),
	credit_score	int
	);
```

# Before Insert Trigger
```sql
drop trigger if exists tr_credit_bi;
delimiter //
create trigger tr_credit_bi before insert on credit
for each row
begin
  if (new.credit_score < 300) then
	set new.credit_score = 300;
  end if;
  
  if (new.credit_score > 850) then
	set new.credit_score = 850;
  end if;
 end//

delimiter ;
```

# Test Trigger tr_credit_bi
```sql
insert into credit
	(
	customer_id,
	customer_name,
	credit_score
	)
values
	(1,	'Milton Megabucks',	  987),
	(2,	'Patty Po', 		  145),
	(3, 'Vinny Middle-Class', 702);
```

# Before Update Trigger
```sql
drop trigger if exists tr_credit_bu;
delimiter //
create trigger tr_credit_bu before update on credit
for each row
begin
  if (new.credit_score < 300) then
	set new.credit_score = 300;
  end if;
  
  if (new.credit_score > 850) then
	set new.credit_score = 850;
  end if;
 end//

delimiter ;
```

# Test Trigger tr_credit_bu
```sql
set sql_safe_updates = 0;

update credit
set credit_score = 1111
where customer_id = 3;

set sql_safe_updates = 1;

```

# Before Delete Trigger
```sql
use bank;
delimiter //

create trigger tr_credit_bd
before delete on credit
for each row
begin
  if (old.credit_score > 750) then
  --- Raises a custom error to prevent deletion.
  --- '45000' is a custom error state in MySQL, meaning “unhandled user-defined exception”.
    signal sqlstate '45000'
    set message_text = 'Cannot delete scores over 750';
  end if;

end//

delimiter ;
```

# Test Trigger tr_credit_bd
```sql
set sql_safe_updates = 0;

delete from credit where customer_id = 1;
delete from credit where customer_id = 2;

set sql_safe_updates = 1;
```

# Embedded SQL
- Embedded SQL are SQL statements contained within an application programming language like Python, C, COBOL
```python
connection = mysql.connector.connect(host_name, user_name, password)
cursor = connection.cursor()

query = '''
SELECT P_CODE, P_DESCRIPT, P_PRICE FROM PRODUCT
WHERE V_CODE IN (25595, 23118, 21225);'''
cursor.execute(query)

results = cursor.fetchall()
for result in results:
    print(result)
```

# Python Embedded SQL
- Install library: <u>pip3 install mysql-connector-python</u>
- Append library path
- Import library
- Build connection
- Create tables
- Create / Read / Update / Delete rows
- Close connection
[Score manipulate](../Lecture-Database/files/ipynb/scores.ipynb)



# Static SQL vs Dynamic SQL
- Static SQL: embedded SQL which the SQL statements do not change while the application is running
```python
cur.execute("""CREATE TABLE IF NOT EXISTS Name
               (first_name TEXT, last_name TEXT)""")
```
- Dynamic SQL: a program generate SQL statements responding to ad hoc queries
```python
name_list = [('Smith', 'John'), ('Johnson', 'Jane'), ('Lee', 'Samantha'), 
('Patel', 'Raj'), ('Hernandez', 'Maria')]

cur.executemany(""" INSERT INTO Name (first_name, last_name) VALUES (%s, %s)""", name_list)
```

# Python MySQL Connector Error Types
Error Type | Error Code Example | Cause
-----------|--------------------|-------
InterfaceError | 2003: Can't connect to MySQL | Connection failure
DatabaseError | 1049: Unknown database | Database does not exist
DataError | 1264: Out of range value | Invalid data type
OperationalError | 2006: MySQL server has gone away | Server issue or timeout
IntegrityError | 1062: Duplicate entry | Primary key violation
ProgrammingError | 1064: SQL syntax error | Invalid SQL syntax
NotSupportedError | 1235: Feature not supported | Unsupported SQL feature
InternalError | 1054: Unknown column | Internal MySQL issue

# Review Questions
- What is the purpose of a CHECK constraint?
- What is the difference between an INSERT command and an UPDATE command?
- What is a stored procedure, and why is it particularly useful?

# Recap SQL Statement
[W3 School SQL Quiz](https://www.w3schools.com/mysql/mysql_quiz.asp)

# Homework #D
資料庫課程作業(D)

# Tips and Tricks
- Working in wrong database
- Using the wrong server
- Leaving where clauses incomplete
- Running partial SQL statement
- Transaction
- Supporting on existing system

# Tip - Working in wrong database

You used Workbench to create an employee table in  distribution database?? Did you?

```sql
create database distribution;
create table employee(
    employee_id int primary key,
    employee_name varchar (100),
    tee_shirt_size varchar (3));
```
```sql
-- ALT1
use distribution;
create table employee (...)
-- ALT2
create table distribution.employee(...);
-- Show database
select database();
show databases;
```
# Tip - Using the Wrong Server
- Sometimes, SQL statements can be executed against the wrong MySQL server. Companies often set up different servers for production and development. 
- It's not unusual for a developer to have two windows open: one connected to the production server and one connected to the development server. If you're not careful, you can make changes in the wrong window.
- Purposely separate development and production environment
  - authorized to different team and people (不同團隊及工程師)
  - operated by different PC or notebook (不同工作電腦)
  - open by different working window (不同工作視窗)
  - connected by different names shown in tabs (不同工作分頁)

# Tip - Leaving Where Clauses Incomplete
Looking at a Ford Focus on the lot, you notice that you have it listed a green, but its color is actually closer to blue. You decide to update its color from green to blue in the database.
```sql
-- it update 3 rows. that is wrong
update inventory
set color = 'blue'
where mfg = 'Ford' and model = 'Focus';
```
```sql
-- step1 - verify where clause by select
select * 
from inventory
where mfg = 'Ford' and model = 'Focus' and color='green';
-- step2: create update statement using correct where clause
update inventory
set color = 'blue'
where mfg = 'Ford' and model = 'Focus' and color='green';
```

# Running Partial SQL Statements
- Execute the selected portion of the script or everything, if there is no selection: Provides a simple way to execute the entire query or a subset of the query.
- Execute the statement under the keyboard cursor: Uses the position the keyboard cursor to identify and execute the query.
```sql
delete from inventory  -- only select this line, then click 'Execute the selected portion'
where vin='4XBCX68RFWE532566'
```
<div class="grid">
    <img src="files/image/mysql_wb_toolbar.png">
</div>
<br>

[Workbench toolbar](https://dev.mysql.com/doc/workbench/en/wb-sql-editor-toolbar.html)

# Supporting an Existing System
In workbench, choose menu "Database" to select "Reverse Engineer" function

# Most Common Database Design
- business field as primary key
- storing redundant data
- spaces or quotes in table names
- poor or no referential integrity
- multiple pieces of information in a single field
- storing optional types of data in different columns
- using the wrong data types and sizes
<br>
[Vedio: Learn 7 of the most common database design mistakes](https://youtu.be/s6m8Aby2at8?si=9xPGZqbksCEIi6pi)

# MySQL Shell
MySQL command line client tool that run SQL, Python or JavaScript commands
> mysqlsh -h localhost -D database_name_here -u user_name_here
> \sql
> select * from employee;
> \quit
