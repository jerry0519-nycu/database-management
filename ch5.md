# Chapter5: Advanced Data Modeling
- Illustrate extended entity relationship (EER) model.
- Describe the characteristics of good primary keys and how to select them.
- Data-modeling design cases

# Nulls Created by Unique Attributes
<img width="515" alt="image" src="https://github.com/user-attachments/assets/7789cc16-bade-451a-8a2f-ce9afda98c03" />

# Extended (Enhanced) Entity Relationship Model (EERM)
- EERM is the result of adding more object-oriented concept to the original ER model
- A diagram that uses the EERM is called EER diagram (EERD)

| 比較項目         | 物件導向程式設計 (OOP)                | 程序式程式設計                     |
|------------------|---------------------------------------|-----------------------------------|
| 核心單元         | 物件 (Object)                         | 函數 (Function)                   |
| 程式組織方式     | 物件與互動關係                        | 線性執行的函數序列                |
| 數據與行為關係   | 封裝在一起 (屬性+方法)                | 分離 (數據結構+操作函數)          |
| 程式執行流程     | 由物件互動決定                        | 明確的線性執行順序                |
| 代碼重用機制     | 繼承、組合、多型                      | 函數調用、代碼複製                |
| 主要特性         | 封裝、繼承、多型、抽象                | 無特別特性                        |
| 現實世界建模     | 直觀 (模擬真實物件)                   | 較不直觀                          |
| 典型應用場景     | 大型商業系統、GUI開發                 | 小型工具、算法實現、系統程式       |
| 代表語言         | Java, C++, C#, Python (OOP部分)       | C, Pascal, BASIC                  |
| 維護性           | 較高 (結構清晰)                       | 較低 (規模增大時)                 |
| 學習曲線         | 較陡峭                                | 較平緩                            |

# Entity Supertypes and Subtypes
- The grouping of employees into various types provides the following two benefits:
  - It avoids unnecessary nulls in attributes when some employees have characteristics that are not shared by other employees
  - It enables a particular employee type to participate in relationships that are unique to that employee type
- The entity supertype (EMPLOYEE) contains common characteristics
- The entity subtype (PILOT, MECHANIC, ACCOUNTANT) contains unique characteristics of each entity subtype

### **Entity Supertypes and Subtypes（實體超類型與子類型）的核心概念**

#### **1. 基本定義**
- **Entity Supertype（實體超類型）**  
  代表一組相關實體的「通用父類別」，包含所有子類型共有的屬性（例如：`EMPLOYEE` 是所有員工的通用類別）。  
- **Entity Subtype（實體子類型）**  
  代表超類別的「具體分類」，包含獨有的屬性或關係（例如：`PILOT`、`MECHANIC`、`ACCOUNTANT` 是 `EMPLOYEE` 的子類型）。  

#### **2. 主要目的與優點**
##### **(1) 避免不必要的 NULL 值**  
- **問題**：若所有員工屬性都放在單一表中，某些欄位會出現 NULL（例如：`飛行執照號碼` 對會計師是無意義的）。  
- **解決**：將特有屬性拆分到子類型中，僅在需要時儲存。  
  - `EMPLOYEE` 表：`員工ID`, `姓名`, `入職日期`（共同屬性）。  
  - `PILOT` 表：`員工ID`, `飛行執照號碼`（僅飛行員需要）。  

##### **(2) 支持子類型專屬的關係**  
- **問題**：單一表無法限制特定關係（例如：只有飛行員可以參與「執飛航班」的關聯）。  
- **解決**：子類型可獨立參與關係。  
  - 只有 `PILOT` 子類型能關聯到 `FLIGHT` 表。  
  - `ACCOUNTANT` 子類型能關聯到 `BUDGET` 表。


- **超類型**：集中管理共通屬性，減少冗余。  
- **子類型**：處理差異化需求，避免 NULL，支持專屬關聯。  
- **本質**：資料庫中的「繼承」概念，類似物件導向程式設計的父類與子類。  


# Characteristics of EERD
- Support attribute **inheritance**
  - Subtypes inherit primary key from supertype
  - Subtypes inherit all attributes and relationships from its supertypes
- Have a special supertype attribute as the **subtype discriminator**, commonly use equality comparison

# Specialization Hierarchy Example
<img width="523" alt="image" src="https://github.com/user-attachments/assets/21c73400-3587-408f-bbf5-a8f54ea025ee" />

## **1. 結構拆解**
### **(1) 超類型（Supertype）**
- **實體名稱**：`EMPLOYEE`  
- **共用屬性**（所有子類型繼承）：  
  ```plaintext
  PK  EMP_NUM          (員工編號，主鍵)
      EMP_LNAME        (姓氏)
      EMP_FNAME        (名字)
      EMP_INITIAL      (縮寫)
      EMP_HIRE_DATE    (入職日期)
      EMP_TYPE         (子類型辨識符，用於區分類別)
  ```

### **(2) 子類型（Subtypes）**
| 子類型       | 辨識符（EMP_TYPE） | 特有屬性                          | 說明                     |
|--------------|--------------------|----------------------------------|--------------------------|
| **PILOT**    | "P"                | `PIL_LICENSE`, `PIL_RATINGS`, `PIL_MED_TYPE` | 飛行員的執照、評級、體檢類型 |
| **MECHANIC** | "M"                | `MEC_TITLE`, `MEC_CERT`          | 機械師的職稱、認證         |
| **ACCOUNTANT**| "A"                | `ACT_TITLE`, `ACT_CPA_DATE`      | 會計師的職稱、CPA 認證日期  |

### **(3) 繼承的關係（Inherited Relationship）**
- **`DEPENDENT`（家屬）** 與 `EMPLOYEE` 的關聯：  
  - 家屬表的主鍵是 `(EMP_NUM, DPNT_NUM)`，其中 `EMP_NUM` 是外鍵，指向 `EMPLOYEE`。  
  - **所有子類型（飛行員、機械師、會計師）都自動繼承此關係**（即所有員工都可以有家屬）。

## **2. 關鍵設計概念**
### **(1) 子類型辨識符（Subtype Discriminator）**
- **欄位**：`EMP_TYPE`（值為 "P"、"M"、"A"）。  
- **作用**：決定一個 `EMPLOYEE` 實例屬於哪個子類型。  
- **實現方式**：  
  - 應用層邏輯：根據 `EMP_TYPE` 查詢對應子類型表。  
  - 資料庫觸發器：自動插入/更新子類型表。  

### **(2) 約束類型**
| 約束                  | 說明                                                                 |
|-----------------------|----------------------------------------------------------------------|
| **Disjoint（互斥）**  | 一個員工只能屬於一個子類型（例如：不能同時是飛行員和機械師）。         |
| **Overlapping（重疊）** | 允許一個員工屬於多個子類型（需額外設計，此圖未採用）。                |
| **Partial（部分）**   | 允許員工不屬於任何子類型（僅存在於超類型中）。                        |
| **Complete（完全）**  | 所有員工必須屬於至少一個子類型（此圖未明確標示，需根據業務規則決定）。 |

### **(3) 繼承的屬性與關係**
- **屬性繼承**：子類型自動擁有超類型的所有屬性（如 `EMP_NUM`, `EMP_LNAME`）。  
- **關係繼承**：子類型自動參與超類型的關係（如與 `DEPENDENT` 的關聯）。  

# Entity Clustering (封裝的概念)
- OFFERING: SEMESTER + COURSE + CLASS
- LOCATION: ROOM + BUILDING

![螢幕擷取畫面 2025-03-30 161655](https://github.com/user-attachments/assets/c60935ac-9344-48cf-9e65-8b6b6acb55ce)

# Entity Integrity: Selecting Primary Keys
- The most important characteristic of an entity is its primary key (a single attribute or a combination of attributes), which uniquely identifies each entity instance.
- The primary key’s function is to guarantee entity integrity
- Primary keys and foreign keys work together to implement relationships in the relational model
- The importance of properly selecting the primary key has a direct bearing on the efficiency and effectiveness of database implementation

# Natural Keys and Primary Keys
- A natural key is a real-world identifier used to uniquely identify real-world objects, which forms part of end user day-to-day business vocabulary
- Usually, if an entity has a natural identifier, a data modeler uses it as the primary key of the entity being modeled
- 自然鍵是指現實世界中用於唯一識別物件的真實識別符，且屬於終端使用者日常業務詞彙的一部分(例如:員工編號、學號等)。
- 通常，若實體具備自然識別符，資料建模者會直接將其作為該實體的主鍵（Primary Key）。
  
Q: Guess the pros and cons of using nature key?
[7 Database Design Mistake](https://youtu.be/s6m8Aby2at8?si=LsJyqtws-hEz2UyN)

以下為自影片歸納之內容，面板可按三角形展開
<details>
<summary><strong>1. 使用業務相關字段作為主鍵</strong></summary>

**問題**：業務相關的字段（如稅號或公司編號）可能會更改，且通常沒有對這些字段的控制。  
**解決方案**：創建一個名為「主鍵」的新字段（例如「id」或「table_name_ID」），用於唯一標識記錄，並保證不會改變。
</details>

<details>
<summary><strong>2. 存儲重複數據</strong></summary>

**問題**：重複存儲某些數據（如年齡）會導致數據不一致，因為其需要依賴於其他字段計算。  
**解決方案**：只存儲必要的字段，直接從其他字段（如出生日期）計算所需數據，而非重複存儲。
</details>

<details>
<summary><strong>3. 在表名中使用空格或引號</strong></summary>

**問題**：在表名中使用空格或引號會導致查詢語句複雜，且容易出錯。  
**解決方案**：避免在表名中使用空格，使用下劃線（如「customer_order」）來分隔單詞。
</details>

<details>
<summary><strong>4. 缺乏或不良的參照完整性</strong></summary>

**問題**：數據庫中的數據質量和有效性得不到保證，可能存在缺失值或不唯一的數據。  
**解決方案**：設置資料庫約束，如主鍵、外鍵和唯一約束，以強制執行數據完整性和規則。
</details>

<details>
<summary><strong>5. 在單一字段中存儲多個信息</strong></summary>

**問題**：將地址等複雜信息存儲在一個字段中，導致無法進行有效的數據驗證和查詢。  
**解決方案**：將地址分解為多個字段（如街道、城市、郵遞區號等）以提升數據質量與查詢效率。
</details>

<details>
<summary><strong>6. 在不同列存儲不同的可選數據類型</strong></summary>

**問題**：將不同類型的電話號碼（如家庭、工作或手機）存儲在不同的列中，可能導致某些列為空。  
**解決方案**：創建一個專門的電話號碼表，並使用外鍵關聯客戶ID，這樣每個客戶可以有多個電話號碼。
</details>

<details>
<summary><strong>7. 使用錯誤的數據類型和大小</strong></summary>

**問題**：不正確的數據類型選擇會導致存儲效率低下和數據集的性能問題。  
**解決方案**：根據數據的使用情況選擇合適的數據類型與大小，使用數據庫的內置類型來保證數據有效性與性能。
</details>

# Primary Key Guidelines
- Unique values
- No change over time 
- Preferably single-attribute
- Preferably numeric: auto-numbering
- Security-compliant: social secure ID is not good

# When to Use Composite Primary Keys
- As identifiers of composite (bridge, associate) entities, in which each primary key combination is allowed once in M:N relationship
- As identifiers of weak entities, in which the weak entity has a strong identifying relationship with the parent entity

### **何時使用複合主鍵**  
1. **作為複合實體（橋接實體/關聯實體）的識別符**  
   - 用於多對多（M:N）關係中，確保每個主鍵組合僅出現一次。  
2. **作為弱實體的識別符**  
   - 用於弱實體與父實體的強識別關係中。  

<img width="467" alt="image" src="https://github.com/user-attachments/assets/e55f2f25-806a-4890-bed4-78c5896c928f" />

# When to Use Surrogate Primary Keys (代理鍵)
- A surrogate key is a primary key created by the database designer to simplify the identification of entity instances 
- Surrogate key has no business meaning, with advantages like unique, stability, performance

#### **1. 定義**  
代理鍵是由資料庫設計者人工建立的**主鍵**，僅用於**唯一識別實體實例**，**本身不具業務意義**（如自動遞增的數字、UUID）。  

#### **2. 核心特性**  
| 特性          | 說明                                                                 |
|---------------|----------------------------------------------------------------------|
| **無業務意義** | 不反映現實業務邏輯（如 `ID = 1` 無法解讀為客戶編號或訂單日期）。       |
| **絕對唯一**   | 由系統保證唯一性（如 `AUTO_INCREMENT` 或 `GUID`）。                   |
| **高度穩定**   | 永不變動（與自然鍵不同，不受業務規則修改影響）。                       |
| **效能優勢**   | 通常為整數或簡潔格式，提升索引效率與聯結速度。                         |

#### **3. 使用時機**  
- 自然鍵過長（如身分證號+日期組合）。  
- 自然鍵可能變動（如公司重整業務編號規則）。  
- 多對多關聯表中簡化複合主鍵結構。  

<img width="472" alt="image" src="https://github.com/user-attachments/assets/321009bf-e64e-46d4-8980-87de39bfc704" />

# Design Case 1: Implementing 1:1 Relationships
- Foreign keys work with primary keys to properly implement relationships in the relational model
- The basic rule is to put the primary key of the parent entity on the dependent entity as a foreign key
- Options for selecting and placing the foreign key include the following:
  - Place a foreign key in both entities
  - Place a foreign key in one of the entities 

# Design Case 1: Illustration
A 1:1 relationship:
- An EMPLOYEE manages zero or one DEPARTMENT
- Each DEPARTMENT is managed by one EMPLOYEE
<img width="465" alt="image" src="https://github.com/user-attachments/assets/3c1d194c-2a22-47e9-bcc5-38a06e8ec779" />

Design comparison
- Fig 1: proper design
- Fig 2: generate many null values
- Fig 3: duplicated work

<img width="518" alt="image" src="https://github.com/user-attachments/assets/0630fabf-5f67-4397-b3ed-a4ba0dc66ec2" />

# Design Case 2: Maintaining Salary History of Time-Variant Data
- <span class="small-text">Time-variant data refers to data whose values change over time and the data changes must be retained</span>
- <span class="small-text">Modeling time-variant data, need a new entity with 1:M relationship to the original entity </span>
- <span class="small-text">This new entity contains the new value, the date of the change, and any other pertinent attribute</span>
- <span class="small-text">Question: What is (1) current salary and (2) salary raise history of an employee within a time period</span>
- <span class="small-text">Discussion: in relationship emp_sal_hist, what cardinality salary_hist is? (0,M) or (1,M) </span>
<img width="470" alt="image" src="https://github.com/user-attachments/assets/2655dac5-bdef-4c4f-9807-2264246f6b6e" />
<img width="473" alt="image" src="https://github.com/user-attachments/assets/3e8bf0af-17dd-4e05-9bf6-5abbb0f80620" />
<img width="469" alt="image" src="https://github.com/user-attachments/assets/fc942565-cb60-444d-af18-6f740cf13b7e" />

# Design Case 3: Fan Traps
- A design **trap** occurs when a relationship is improperly or incompletely identified, which is not consistent with the real world
- The most common design trap is fan trap, a type of join path between three tables when a "1-to-M" join links a table which is in turn linked by another "1-to-M" join
- It produces an association among other entities not expressed in the model
 <img width="358" alt="image" src="https://github.com/user-attachments/assets/ae792d04-d766-4ce9-b5a7-8aeb016e8022" />

- Question: Which team the player Jordan belongs to ? 

# Illustration of Design Case 3
<img width="466" alt="image" src="https://github.com/user-attachments/assets/6ac1ae7d-c3d6-4a14-bf52-8b4112dc00b9" />

Exists a **transitive** relationship between DIVISION and PLAYER via the TEAM entity

# Design Case 4:  Redundant Relationships
- Redundant relationships occur when there are multiple relationship paths between related entities
- The main concern is that they remain consistent across the model
- Some designs use redundant relationships as a way to simplify the design
<img width="472" alt="image" src="https://github.com/user-attachments/assets/f4a21f8f-07f2-4bc7-a841-1c3786d0064f" />


# Review Questions
### 1. What is an entity supertype, and why is it used?

An **entity supertype** is a generic entity that contains common characteristics shared by all its subtypes in a specialization hierarchy. It is used to:
- Avoid unnecessary NULL values in attributes when some entity instances have characteristics that others don't.
- Enable specific subtypes to participate in relationships unique to them (e.g., only pilots can be assigned to flights).
- Centralize shared attributes (e.g., all employees have `EMP_NUM`, `EMP_NAME`) while allowing subtypes (e.g., `PILOT`, `ACCOUNTANT`) to define specialized attributes.
- Support attribute and relationship inheritance, where subtypes automatically inherit all attributes and relationships from their supertype.

Example:  
The `EMPLOYEE` supertype (with shared attributes like `EMP_NUM`) has subtypes like `PILOT` (with unique attributes such as `PIL_LICENSE`).


### 2. What is the most common design trap, and how does it occur?

The most common design trap is a **fan trap**. It occurs when:  
- A "1-to-M" relationship links a table that is itself linked by another "1-to-M" relationship, creating an ambiguous join path between three tables.  
- This produces unintended associations among entities not explicitly modeled.  

**Example**:  
In a model where `DIVISION` has many `TEAM`s, and `TEAM` has many `PLAYER`s, querying "Which division does Jordan belong to?" requires joining all three tables. Without proper design, the direct path from `PLAYER` to `DIVISION` is unclear, leading to misinterpretation.  

**Solution**:  
Ensure transitive relationships are explicitly modeled or resolved by restructuring the schema.

### 3. Describe the characteristics of good primary keys and how to select them.

A good primary key should have the following characteristics:  
1. **Uniqueness**: Guarantees each entity instance is uniquely identifiable (e.g., `EMP_NUM`).  
2. **Stability**: Should not change over time (e.g., avoid using phone numbers or email addresses).  
3. **Simplicity**: Preferably a single attribute and numeric (e.g., auto-incremented integers for efficiency).  
4. **Security-compliant**: Should not expose sensitive information (e.g., avoid SSNs).  

**Selection Guidelines**:  
- **Natural keys** (e.g., `EMPLOYEE_ID`) can be used if they meet the above criteria.  
- **Surrogate keys** (e.g., auto-generated `ID`) are preferred when natural keys are unstable or complex.  
- **Composite keys** are used for:  
  - Bridge entities in M:N relationships (e.g., `(STUDENT_ID, COURSE_ID)` in an enrollment table).  
  - Weak entities (e.g., `(EMP_NUM, DEPENDENT_NUM)` for dependents).  

**Example**:  
In the `EMPLOYEE` table, `EMP_NUM` (a surrogate key) is better than `EMP_SSN` (sensitive) or `EMP_NAME` (non-unique).

