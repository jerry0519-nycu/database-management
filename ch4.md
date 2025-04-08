# Chapter4: Entity Relationship (ER) Modeling
- Data modeling is the first step in database design, as a bridge between real-world objects and the database model implemented in the computer.
- It is important to illustrate data-modeling details graphically through entity relationship diagrams (ERDs) to facilitate communication.
<div class="middle-grid">
    <img src="restricted/CFig02_05.jpg" alt="">
</div>

# Entity Relationship Model
- The entity relationship model (ERM) generate ERD (ER diagram)
- The ERD represents the <span class="blue-text">external model</span> as viewed by end users
- The ERD represents the <span class="blue-text">conceptual model</span> as viewed by database designer
- ERDs describe the database’s main components:
  - Entities
  - Attributes
  - Relationships

| 比較維度        | ERD (實體關係圖)                          | ERM (實體關係模型)                     |
|---------------|----------------------------------------|-------------------------------------|
| **全稱**       | Entity-Relationship Diagram            | Entity-Relationship Model           |
| **中文名稱**    | 實體關係圖                                | 實體關係模型                           |
| **本質**       | 圖形化表示工具                            | 概念性理論框架                        |
| **主要形式**    | 視覺化圖表（使用標準符號）                   | 抽象理論模型                          |
| **提出者**      | 基於Peter Chen的理論發展                   | Peter Chen (1976年)                  |
| **主要元素**    | 實體(矩形)、關係(菱形)、屬性(橢圓)等具體圖形元素 | 實體、屬性、關係等抽象概念               |
| **使用場景**    | 數據庫具體設計階段                         | 數據庫概念建模階段                     |
| **詳細程度**    | 包含具體實現細節                          | 僅描述抽象關係結構                     |
| **變更靈活性**  | 修改需要調整圖形                          | 理論調整不涉及圖形修改                 |
| **輸出結果**    | 可交付的設計圖檔                          | 概念性文檔描述                        |
| **使用者**      | 數據庫設計師、開發人員                      | 系統分析師、架構師                    |

# Entity
- An entity is an object of interest to the end user
- An entity in the ERM is a table (relation)
- In Crow’s Foot notation, an entity is represented by a rectangle
  - contains entity name
  - entity name is a noun usually written **in all capital letters**. It would depend on your naming convention

<img width="521" alt="image" src="https://github.com/user-attachments/assets/42fcddcd-486c-44d4-ab57-45ccb6c0a80f" />

# Attributes
- **Attributes** are characteristics of entities
- **Required attribute** (not null) and **optional attribute** (allow null)
- Attributes must have a **domain**, the set of possible values for a given attribute
- **Identifier** and **composite identifier** is one or more attributes that uniquely identify each row.
- **Simple attribute** (age, sex) and **composite attribute** (address, phone_number)
- **Single-valued attribute** (emp_id) and **multi-valued attributes** (car_color, emp_habit)
- **Derived attribute** whose value is calculated from other attributes (working_years)

| 屬性類型 | 定義 | 特徵 | 範例 | 補充說明 |
|---------|------|------|------|---------|
| **必要屬性<br>(Required Attribute)** | 必須有值的屬性 | 不可為NULL | 身分證號、訂單編號 | 通常用於關鍵識別字段 |
| **可選屬性<br>(Optional Attribute)** | 可為空的屬性 | 允許NULL | 中間名、備註 | 非強制性資料 |
| **值域<br>(Domain)** | 屬性允許值的集合 | 定義取值範圍 | 性別(男/女/其他)、月份(1-12) | 可設定檢查約束(CHECK) |
| **識別碼<br>(Identifier)** | 唯一識別實體的屬性 | 不可重複、不可為NULL | 學號、員工編號 | 相當於主鍵(Primary Key) |
| **複合識別碼<br>(Composite Identifier)** | 由多個屬性組成的識別碼 | 組合唯一 | (訂單ID+商品ID)、(學號+課程號) | 需要多個字段才能唯一識別 |
| **簡單屬性<br>(Simple Attribute)** | 不可再分的原子屬性 | 單一值、無結構 | 年齡、性別 | 數據庫直接存儲的基本字段 |
| **複合屬性<br>(Composite Attribute)** | 可分解為多個子屬性的屬性 | 具有層次結構 | 地址(省/市/區/路)、姓名(姓/名) | 可展開為多個數據庫字段 |
| **單值屬性<br>(Single-Valued Attribute)** | 每個實體只有一個值 | 一對一關係 | 出生日期、身分證號 | 最常見的屬性類型 |
| **多值屬性<br>(Multi-Valued Attribute)** | 每個實體可有多個值 | 一對多關係 | 聯絡電話、興趣嗜好 | 需要單獨建表或用特殊格式存儲 |
| **衍生屬性<br>(Derived Attribute)** | 由其他屬性計算得出的屬性 | 不需手動維護 | 年齡(根據生日計算)、年資 | 可定義為計算列或視圖 |
| **儲存屬性<br>(Stored Attribute)** | 直接存儲在數據庫中的屬性 | 基礎數據來源 | 出生日期、入職日期 | 衍生屬性的計算基礎 |
| **弱實體屬性<br>(Weak Entity Attribute)** | 依賴於其他實體的屬性 | 部分識別碼來自強實體 | 訂單項目(依賴訂單)、家屬(依賴員工) | 需要與強實體關聯 |

# Identifier and Composite identifier
<div class="grid">
    <img src="restricted/CFig04_02a.jpg" alt="">
</div>

- CLASS_CODE is a identifier
- (CRS_CODE, CLASS_SECTION) is a composite identifier

# Entity's Notation
Required attribute: bold font(粗體字)

PK: in a separated cell with bold and underline font

# Implementing Multi-valued Attributes
  - If necessary, replace multi-value attribute by creating several new attributes
  - If necessary, replace multi-value attribute by creating an new entity

1. **「用新增多個屬性來取代多值屬性」**
   - 當一個屬性可能包含多個值時（例如「電話號碼」可能有多個），可以將該屬性拆分成多個單值屬性（如 phone1, phone2, phone3...）
   - 適用情境：值的數量固定且很少（通常不超過3-4個）
   - 缺點：若值數量不固定會造成空間浪費或限制

2. **「用新增實體來取代多值屬性」**
   - 更正規的解決方案是建立一個新的實體（表）來存放這些多值屬性
   - 例如：原本的「客戶」表有多個電話號碼，就新增一個「客戶電話」表，用外鍵關聯
   - 優點：符合資料庫正規化原則（通常是1NF→2NF的過程），可靈活處理任意數量的值

舉例說明：
原始資料（含多值屬性）：
```
客戶(客戶ID, 姓名, 電話[多值])
```

方法1結果：
```
客戶(客戶ID, 姓名, 電話1, 電話2, 電話3)
```

方法2結果：
```
客戶(客戶ID, 姓名)
客戶電話(記錄ID, 客戶ID, 電話號碼)
```

<img width="521" alt="image" src="https://github.com/user-attachments/assets/2c32ecd2-a7f6-429a-b368-75f6ba9b0fa0" />

<img width="398" alt="image" src="https://github.com/user-attachments/assets/5b4a6c45-0477-4131-b23b-0a249a8d8d52" />

Q: What is the pros and cons between the two replacement approaches?
| Criteria | Creating Several New Attributes | Creating a New Entity |
|---------|---------------------------------|-----------------------|
| **Normalization** | Violates 1NF (First Normal Form) | Fully normalized (supports 1NF+) |
| **Scalability** | Poor (limited by predefined columns) | Excellent (unlimited rows can be added) |
| **Query Complexity** | Simpler queries (single table) | More complex (requires joins) |
| **Flexibility** | Rigid structure (fixed number of values) | Flexible (dynamic number of values) |
| **Storage Efficiency** | Wastes space for unused attributes | Space-efficient (only stores existing values) |
| **Data Integrity** | Hard to enforce (multiple columns to check) | Easier to enforce (single relationship) |
| **Example Implementation** | `phone1`, `phone2`, `phone3` columns | Separate `PhoneNumbers` table with FK |
| **Best Use Case** | When maximum number of values is small and fixed | When number of values is variable or large |
| **Maintenance** | Difficult (schema changes needed for more values) | Easy (just add more rows) |
| **Performance** | Faster reads (no joins) | Slower reads (requires joins) but better writes |

# Derived Attributes

<img width="519" alt="image" src="https://github.com/user-attachments/assets/02aa4f75-6f82-4f69-8757-11dfd6deea70" />

**derived attribute在ERD中使用虛線標註**


Q: What attribute is proper to use derived attributed, working_year or total_amount?
| 屬性名稱          | 推薦作為衍生屬性？ | 關鍵理由                                                                 | 潛在風險                                                                 |
|-------------------|-------------------|--------------------------------------------------------------------------|--------------------------------------------------------------------------|
| **`working_year`**<br>(年資) | ✅ **強烈建議**     | ▪ 基於固定數據（入職日期）<br>▪ 公式穩定（當前日期 - 入職日期）<br>▪ 低計算成本                     | ▪ 時區/閏年邊際案例需處理                                                 |
| **`total_amount`**<br>(總金額) | ⚠ **謹慎使用**     | ▪ 需即時聚合關聯數據（如訂單明細）<br>▪ 高頻變動可能影響效能<br>▪ 商業邏輯複雜度較高              | ▪ 數據一致性風險<br>▪ 需緩存機制<br>▪ 跨表交易可能導致計算延遲             |

# Relationship
- The entities that participate in a relationship are also known as <span class="blue-text">participants</span>
- A relationship is identified by a name that describes the relationship
- The relationship name is an active or passive <span class="blue-text">verb</span>
- <span class="blue-text">Connectivity</span> describes the relationship classification: 1:1, 1:M, and M:N
- <span class="blue-text">Cardinality</span> expresses the minimum and maximum number of entity occurrences associated with one occurrence of the related entity

#### **1. 參與者 (Participants)**  
- **定義**：參與關係的實體（Entity）  
- **範例**：  
  - 關係「學生_選修_課程」中，「學生」與「課程」即為參與者  
- **補充**：參與者必須是明確定義的實體，弱實體(Weak Entity)也可參與  

#### **2. 關係名稱 (Relationship Name)**  
- **定義**：用**動詞**描述實體間的互動  
- **命名規則**：  
  - **主動語態**：`客戶_下訂單_商品`  
  - **被動語態**：`商品_被訂購_客戶`（較少用）  
- **補充**：名稱應避免模糊（如「擁有」需明確為「員工_擁有_健保」或「公司_擁有_設備」）  

#### **3. 連接性 (Connectivity)**  
- **定義**：關係的**基本分類**  
- **三種類型**：  
  | 類型 | 說明 | 範例 |  
  |------|------|------|  
  | **1:1** | 一對一 | 員工_配發_公司手機 |  
  | **1:M** | 一對多 | 部門_包含_員工 |  
  | **M:N** | 多對多 | 學生_選修_課程 |  
- **補充**：M:N關係在實作時需拆解為關聯表（Junction Table）  

#### **4. 基數性 (Cardinality)**  
- **定義**：具體限制參與者的**最小與最大數量**  
- **表示法**：`(min, max)`  
  - **範例**：  
    - 一名學生「至少選修3門，至多選修6門」課程 → `(3,6)`  
    - 公司規定「員工可不分配或至多分配1台」筆電 → `(0,1)`  
- **補充**：  
  - 最小基數`(min=1)`表示**強制參與**  
  - 最大基數`(max=N)`表示**無上限**  


# Relationship's Notation
- (1, 4): one professor teach at least one and no more than four classes
- (1, 1): each class is taught by one and only one professor

# Existence Dependence
- Entity can be <span class="blue-text">strong</span> or <span class="blue-text">weak</span> depending on whether the entity can exist independently or not.
- A strong entity can exist apart from all of its related entities, it is <span class="blue-text">existence-independent</span>
- A weak entity is <span class="blue-text">existence-dependent</span> on another related entity occurrence
- Relationship 'EMPLOYEE claims DEPENDENT', the DEPENDENT entity is existence dependent on the EMPLOYEE entity. That is, DEPENDENT has a mandatory (NOT NULL) foreign key, EMP_NUM to link with EMPLOYEE. 

#### **1. 強實體 (Strong Entity)**  
- **定義**：  
  - 可獨立存在，**不依賴其他實體**  
  - 擁有**完整的主鍵（Primary Key）**  
- **特性**：  
  - **存在獨立性**：即使沒有關聯的實體，仍能存在  
  - **主鍵自足**：主鍵不包含其他實體的外鍵（Foreign Key）  
- **範例**：  
  - **`EMPLOYEE`（員工）**：員工資料可獨立存在，即使沒有部門或眷屬資料  
  - **`PRODUCT`（產品）**：產品資訊不需依賴訂單或供應商  

#### **2. 弱實體 (Weak Entity)**  
- **定義**：  
  - **必須依賴強實體才能存在**  
  - 主鍵通常包含強實體的外鍵（稱為**識別關係，Identifying Relationship**）  
- **特性**：  
  - **存在依賴性**：若關聯的強實體消失，弱實體也必須刪除  
  - **部分主鍵**：主鍵需結合強實體的外鍵（如 `(EMP_NUM, DEPENDENT_ID)`）  
- **範例**：  
  - **`DEPENDENT`（員工眷屬）**：眷屬必須對應到一名員工（`EMP_NUM` 為外鍵且 **NOT NULL**）  
  - **`ORDER_ITEM`（訂單明細）**：明細必須屬於某張訂單（`ORDER_ID` 為外鍵）  

#### **3. 區別**  
| 特徵                | 強實體                          | 弱實體                          |  
|---------------------|--------------------------------|--------------------------------|  
| **存在性**           | 獨立存在                        | 依賴強實體存在                   |  
| **主鍵**            | 自足（不包含外鍵）               | 需結合強實體的外鍵                |  
| **刪除影響**         | 不影響其他實體                  | 若強實體刪除，弱實體連帶刪除       |  
| **ER圖表示**        | 單一矩形                        | 矩形外框加粗（或雙矩形）           |  

#### **4. 實務範例：`EMPLOYEE` 與 `DEPENDENT`**  
- **關係**：`EMPLOYEE` **撫養** `DEPENDENT`  
  - **弱實體標記**：  
    - `DEPENDENT` 的主鍵為 `(EMP_NUM, DEPENDENT_ID)`  
    - `EMP_NUM` 是對 `EMPLOYEE` 的 **強制外鍵（NOT NULL）**  

#### **5. 特殊注意事項**  
- **弱實體的識別關係**：  
  - 在 ER 圖中，弱實體與強實體的關係線會加粗表示  

#### 判斷法
#### **1. 能否獨立存在？**  
- **強實體**：可以獨立存在（例如：學生、課程）。  
- **弱實體**：必須依賴強實體才能存在（例如：訂單明細必須依附於訂單）。  

#### **2. 主鍵（PK）是否包含外鍵（FK）？**  
- **強實體**：主鍵完全獨立（例如：`學號`）。  
- **弱實體**：主鍵需結合強實體的外鍵（例如：`(訂單ID, 明細編號)`）。  

若一個實體 **必須依賴其他實體才能被唯一識別**（主鍵含外鍵），就是 **弱實體**；否則就是 **強實體**。

# Weak Entity
- A weak entity is existence-dependent on a strong entity with a strong (identifying) relationship - requires a non-null FK from the related strong entity and form a composite PK.
  - DEPENDENT(<u><b>EMP_NUM, DEP_SID</b></u>, DEP_NAME, DEP_DOB), EMP_NUM is FK,
- A weak entity always has a **mandatory participation** to a strong entity (every row of the weak entity must be associated with one row of a strong entity because of non-null FK).

#### **1. 核心定義**
- **存在依賴性**：  
  ▸ 必須與強實體（Strong Entity）綁定才能存在  
  ▸ 範例：`員工(EMPLOYEE)` 與 `眷屬(DEPENDENT)`，刪除員工時眷屬自動刪除  

- **主鍵結構**：  
  ▸ **複合主鍵（Composite PK）** = **強實體的外鍵（FK）** + 弱實體自身的局部鍵  
  ▸ 範例：`DEPENDENT` 的主鍵為 `(EMP_NUM, DEP_SID)`  

# Strong Entity
- A strong entity has a PK that uniquely identifies each record without depending on other entity.
- EMPLOYEE(<u><b>EMP_NUM</b></u>, EMP_LNAME, EMP_FNAME, EMP_INITIAL, EMP_DOB, EMP_HIREDATE)
- **獨立存在性**  
  ▸ 無需依賴其他實體即可存在  
  ▸ 範例：`EMPLOYEE`（員工）資料可獨立存在，即使沒有部門或眷屬關聯  

- **主鍵特性**  
  ▸ 擁有**自足主鍵（Independent PK）**  
  ▸ 主鍵值**不包含其他實體的外鍵**  

# Example of Strong and Weak Entities
Considering two entities: EMPLOYEE (strong) and DEPENDENT (weak)
- DEPENDENT is weak because it has no sufficient PK by itself at the beginning
  - DEPENDENT(<u><b>DEP_SID</b></u>, DEP_NAME, DEP_DOB, EMP_NUM), EMP_NUM is FK, but when two employee is couple, their children will be duplicated
  - DEP_SID alone cannot uniquely identify a dependent.
- Need expand PK of DEPENDENT by combining EMP_NUM
  - DEPENDENT(<u><b>EMP_NUM, DEP_SID</b></u>, DEP_NAME, DEP_DOB) to build a strong (identifying) relationship with EMPLOYEE to uniquely identify each dependent.
- DEP_NUM is better than DEP_SID in terms of privacy
  - DEPENDENT(<u><b>EMP_NUM, DEP_NUM</b></u>, DEP_NAME, DEP_DOB), EMP_NUM is non-null FK
#### **1. 強實體 (Strong Entity) 特徵**  
✅ **獨立存在性**  
- 可以不依賴其他實體單獨存在  
- 範例：`EMPLOYEE`（員工）、`PRODUCT`（產品）  

✅ **主鍵自足性**  
- 擁有**獨立的主鍵**（不包含其他實體的外鍵）  

✅ **刪除不受限**  
- 刪除時不會連帶影響其他實體  

---

#### **2. 弱實體 (Weak Entity) 特徵**  
✅ **存在依賴性**  
- **必須依賴強實體才能存在**  
- 範例：`DEPENDENT`（眷屬）需綁定 `EMPLOYEE`  

✅ **複合主鍵結構**  
- 主鍵 = **強實體的外鍵** + 自身局部鍵  

✅ **強制參與關係**  
- 外鍵不可為 NULL (`NOT NULL`)  
- 關係線在 ER 圖中會加粗表示  

### **1. 強實體（EMPLOYEE）與弱實體（DEPENDENT）的定義**
- **`EMPLOYEE`（員工）**：  
  - **強實體**，因為它能獨立存在，且有自己的主鍵（如 `EMP_NUM`）。  
- **`DEPENDENT`（家屬）**：  
  - **弱實體**，因為它必須依附於員工（無法獨立存在），且 **無法僅靠自己的屬性唯一識別**。  

---

### **2. 原始設計的問題**
假設 `DEPENDENT` 初始設計為：  
```sql
DEPENDENT(DEP_SID, DEP_NAME, DEP_DOB, EMP_NUM)
```
- **`DEP_SID`（家屬身份證號）** 無法單獨作為主鍵，因為：  
  - 若兩個員工是夫妻（共用同一子女），會導致 `DEP_SID` 重複（同一子女被記錄多次）。  
  - 例如：員工A和員工B的孩子「王小華」的 `DEP_SID` 相同，但分屬不同員工。  
- **`EMP_NUM`（員工編號）是外鍵**，指向 `EMPLOYEE` 表，但未納入主鍵。  

**問題**：無法唯一識別「某位員工的某個家屬」。  

---

### **3. 解決方案：擴充主鍵（Combined PK）**
將 `EMP_NUM` 納入主鍵，形成 **複合主鍵**：  
```sql
DEPENDENT(EMP_NUM, DEP_SID, DEP_NAME, DEP_DOB)
```
- **複合主鍵 = `(EMP_NUM, DEP_SID)`**  
  - 確保同一員工的家屬 `DEP_SID` 不重複。  
  - 不同員工的家屬即使 `DEP_SID` 相同（如夫妻的孩子），也能透過 `EMP_NUM` 區分。  

---

### **4. 更優化的設計：改用 `DEP_NUM` 取代 `DEP_SID`**

- **隱私考量**：直接使用家屬身份證號（`DEP_SID`）可能涉及隱私問題。  
- **改用流水號 `DEP_NUM`**：  
  ```sql
  DEPENDENT(EMP_NUM, DEP_NUM, DEP_NAME, DEP_DOB)
  ```
  - **複合主鍵 = `(EMP_NUM, DEP_NUM)`**  
  - **`EMP_NUM` 為非空外鍵**（Non-null FK），確保依賴關係。  
  - 優點：  
    - 避免暴露敏感資訊（如身份證號）。  
    - 同一員工的家屬 `DEP_NUM` 可簡單設為 1, 2, 3...（如員工A的家屬1、家屬2）。  

---

### **5. 總結：弱實體的關鍵設計**
1. **必須與強實體關聯**（透過外鍵 `EMP_NUM`）。  
2. **主鍵需包含強實體的外鍵**（如 `(EMP_NUM, DEP_NUM)`）。  
3. **避免使用敏感資訊作為主鍵**（如改用流水號而非身份證號）。  

---

### **範例對比**
| 設計版本                | 主鍵                | 優缺點                          |
|-------------------------|---------------------|---------------------------------|
| 初始設計（`DEP_SID`）   | `DEP_SID`           | 隱私風險，無法處理重複家屬。     |
| 複合主鍵（`DEP_SID`）   | `(EMP_NUM, DEP_SID)`| 解決重複問題，但仍有隱私疑慮。   |
| 最佳設計（`DEP_NUM`）   | `(EMP_NUM, DEP_NUM)`| 隱私安全 + 唯一性保證。          |

---

### **ER 圖表示**
- **`EMPLOYEE`（強實體）**：□  
  - 主鍵：`EMP_NUM`  
- **`DEPENDENT`（弱實體）**：■  
  - 主鍵：`(EMP_NUM, DEP_NUM)`  
  - 外鍵：`EMP_NUM`（虛線指向 `EMPLOYEE`）  

# Illustrate Relationship Between Weak & Strong Entity
<img width="322" alt="image" src="https://github.com/user-attachments/assets/3a2ab6de-f78f-4de1-a427-d13800f390e3" />

# Relationship Strength
- <u>Relationship strength</u> can be strong or weak based on how to define PK of a related entity. 
- To implement a relationship, the PK of one entity (parent entity, normally on the “one” side of 1:M relationship) appears as a FK in the related entity (child entity, mostly the entity on the “many” side of 1:M relationship) to link two entities. 
  - <span class="blue-text"> Non-identifying(weak) Relationships </span>: if the PK of the "M side" entity does <u>NOT</u> contain a PK of the '1 side' entity
  - <span class="blue-text"> Identifying (strong) Relationships</span>: when the PK of the "M side" entity contains the PK of the "1 side" entity

# Illustration of Relationship Strength

<div class="middle-grid">
    <img src="restricted/CFig04_09.jpg" alt="">
    <img src="restricted/CFig04_10.jpg" alt="">
</div> 

- dotted line shows weak relationships; solid line shows strong relationships

# Implementation Strong / Weak Relationship in DBMS
- Use a strong relationship when:
	- The M-side entity is conceptually a part of the 1-side.
	- The M-side object should be destroyed when the 1-side is destroyed (e.g., an employee’s dependant).
- Use a weak relationship when:
  	- The M-site entity can exist independently of the 1-side.
	- The M-side object should not be deleted if the 1-side is deleted (e.g., an employee and a department).

# The Order to Load Tables Under 1:M Relationship 
- Keep in mind that the order in which the tables are created and loaded is very important.
- In the “COURSE generates CLASS” relationship, the COURSE table must be created before the CLASS table. After all, it would not be acceptable to have the CLASS table’s foreign key refer to a COURSE table that did not yet exist.
- Load the data of the “1” side first in a 1:M relationship to avoid the possibility of referential integrity errors.

# Relationship Participation
- Relationship participation is either <span class="blue-text">optional or mandatory</span>.
- Because of the bidirectional nature of relationships, it is necessary to determine the connectivity as well as max and min cardinalities of the relationship from COURSE to CLASS and from CLASS to COURSE. 
- **Optional participation** means that some rows may not participate into the relationship
- **Mandatory participation** means that each row must participate into the relationship

# Illustration of Relationship Participation

<img width="425" alt="image" src="https://github.com/user-attachments/assets/ba00e36c-f7a4-434c-a630-d0d0a5161e67" />

<img width="326" alt="image" src="https://github.com/user-attachments/assets/202852f2-82f2-460c-bf34-cda1c14a9e6b" />

<img width="322" alt="image" src="https://github.com/user-attachments/assets/dc4eda54-15c6-41c3-9d8b-b99bde164f8d" />

# Relationship Degree
![螢幕擷取畫面 2025-03-29 223108](https://github.com/user-attachments/assets/3c0f9b79-4658-473f-bbc7-cec133b9e146)

# Recursive Relationship
<img width="401" alt="image" src="https://github.com/user-attachments/assets/c28c7557-9744-45ca-9576-0d9764f7b3e0" />

# Associative (Composite) Entities
- The ER model uses the associative entity to represent an M:N relationship between two or more entities
- It is also called a composite or bridge entity and is a 1:M relationship with the parent entities
- It is composed of the primary key attributes of each parent entity
- The composite entity may also contain additional attributes that play no role in connective process

# Illustration of Associative Entities
STUDENT has CLASS is a M:N relationship

<img width="395" alt="image" src="https://github.com/user-attachments/assets/fcd0d25e-1f75-4e7e-88b7-d97d0a6e9f71" />

<img width="401" alt="image" src="https://github.com/user-attachments/assets/5a0ad621-cc5f-4963-acd6-c912549d7321" />

<img width="530" alt="image" src="https://github.com/user-attachments/assets/991758cf-8fac-4dae-a3c2-aea008733487" />

# Developing an ER Diagram
Building an ERD usually involves the following activities as a <span class="blue-text">iterative process</span>:
- Create a detailed description of the organization’s operations
  - Interview users
  - Investigate SOPs, Forms, Reports 
- Identify business rules based on the description of operations
- Identify main entities and relationships from the business rules
- Develop the initial ERD
- Identify the attributes and primary keys that adequately describe entities
- Revise and review the ERD

# Tiny College (TC) (1,2/10)
- Tiny College is divided into several schools.
  - A school is managed by a professor. 
  - Each professor can be the dean of only one school, or none of any school. 
- Each school has several departments.
  - The number of departments operated by a school is at least one to many
  - Each department belongs to only a single school
<img width="401" alt="image" src="https://github.com/user-attachments/assets/6f9449ff-2cff-4dc5-93b8-7d74a9a2c081" />

# Tiny College (TC) (3/10)
- Each department may offer courses.
  - Some departments that were classified as "research only," they would not offer courses; therefore, the COURSE entity would be optional to the DEPARTMENT entity.
<img width="393" alt="image" src="https://github.com/user-attachments/assets/cb9c6ea8-a06f-45fe-a54f-8c5486593122" />

# Tiny College (TC) (4/10)
- A course can be taught in several classes.
- A course may not be taught in some semester 
- A class is offered during a given semester. SEMESTER defines the year and the term that the class will be offered. 
- CLASS is optional to SEMESTER.
- CLASS is optional to COURSE.
<img width="395" alt="image" src="https://github.com/user-attachments/assets/54f61619-2ab4-4100-8aa8-801830dd8f29" />

# Tiny College (TC) (5/10)
- Each department should have one or more professors assigned to it. 
- One and only one of those professors chairs the department
- Not all professors are required to chair a department. 
- DEPARTMENT is optional to PROFESSOR in the "chairs" relationship.
<img width="400" alt="image" src="https://github.com/user-attachments/assets/26878276-627a-48e0-91bf-6fb1b0d6cf4a" />

# Tiny College (TC) (6/10)
- Each professor may teach up to four classes; each class is belong to a course.
- A professor may also be on a research contract and teach no classes at all.
<img width="393" alt="image" src="https://github.com/user-attachments/assets/139faf61-2b57-4714-a05e-869cce290843" />

# Tiny College (TC) (7/10)
- A student may enroll in several classes but take each class only once.
- Each student may enroll in up to six classes, and each class may have up to 35 students, (STUDENT and CLASS is M:N relationship ). 
- This M:N relationship must be divided into two 1:M relationships by ENROLL entity 
<img width="523" alt="image" src="https://github.com/user-attachments/assets/3d0a73ae-da1b-4b7c-9559-5b598435ab40" />

# Tiny College (TC) (8/10)
- Each department has several students whose major is offered by that department. <span class="red-text">(VAGUE!!)</span>
- Each student has only a single major associated with a single department.
- It is possible for a student not to declare a major field of study.
<img width="514" alt="image" src="https://github.com/user-attachments/assets/c3e18bf2-db4e-4c81-a281-022a1a46978b" />

# Tiny College (TC) (9/10)
- Each student has an advisor in his or her department
- Each advisor counsels several students.
- An advisor is also a professor, but not all professors advise students.
<img width="520" alt="image" src="https://github.com/user-attachments/assets/1bd44465-a324-4be6-a93d-01cb7fd4d180" />

# Tiny College (TC) (10/10)
- A class is taught in a room.
- Each room is located in a building.
- A building can contain many rooms. 
- Some buildings do not contain (class) rooms.
<img width="524" alt="image" src="https://github.com/user-attachments/assets/bd3d17a9-8b13-4290-9e5e-aac4a3e5df9f" />

# Tiny College (TC) (Summary: Entities)
PROFESSOR
COURSE
STUDENT
SCHOOL
CLASS
BUILDING
DEPARTMENT
SEMESTER
ROOM
ENROLL (the associative entity between STUDENT and CLASS)

# Summary: Components of ERM
<img width="521" alt="image" src="https://github.com/user-attachments/assets/c8b5ee72-2da8-45fd-b995-441cb495dd0e" />

# Summary: Completed ERD
![螢幕擷取畫面 2025-03-29 223806](https://github.com/user-attachments/assets/d10f3319-b653-487f-8ea2-300e9d8cc10a)

# Database Design Challenges: Conflicting Goals
- Database designers must often make design compromises that are triggered by conflicting <span class='blue-text'>GOALS</span>
  - Database design must conform to design standards
  - High processing speed may limit the number and complexity of logically desirable relationships
- However, a design that meets all requirements and design conventions are the most important goals

# Review Questions
### 1. Difference Between Weak Entity and Strong Entity
| Aspect            | Strong Entity                          | Weak Entity                            |
|-------------------|----------------------------------------|----------------------------------------|
| Existence         | Existence-independent                  | Existence-dependent on a strong entity |
| Primary Key       | Has its own independent PK             | PK includes FK from strong entity      |
| Deletion          | Can be deleted without cascading       | Deletion cascades from strong entity   |
| Example          | `EMPLOYEE(EMP_ID, name)`              | `DEPENDENT(EMP_ID, dep_num, name)`    |
| ER Notation      | Single rectangle                      | Double rectangle                       |

### 2. Difference Between Weak (Non-identifying) and Identifying (Strong) Relationship
| Aspect            | Identifying Relationship               | Non-identifying Relationship           |
|-------------------|----------------------------------------|----------------------------------------|
| FK in PK          | FK is part of child's PK               | FK is not part of child's PK           |
| Dependency        | Child cannot exist without parent      | Child can exist without parent         |
| Line Style       | Solid line with diamond (ER diagram)   | Dashed line (ER diagram)               |
| Example          | `ORDER(ord_id)` → `ORDER_ITEM(ord_id, item_id)` | `DEPARTMENT(dept_id)` → `EMPLOYEE(emp_id, dept_id)` |

### 3. Translating M:N Relationship in ERM
**Solution:** Convert to two 1:M relationships with an associative entity:
1. Original M:N: `STUDENT` ⟷ `COURSE`
2. After resolution:
   - `STUDENT` → `ENROLLMENT` ← `COURSE`
   - Associative entity `ENROLLMENT(enroll_id, student_id, course_id, grade, semester)`

**Implementation Rules:**
- The associative entity gets:
  - FKs from both original entities
  - Its own attributes (e.g., enrollment date, grade)
  - Optionally a surrogate PK (e.g., enroll_id)

# Homework #B
資料庫課程作業(B)

# Present Final Project Progress
- Date: 04/15 (專班) and 04/16 (資財)
- Duration: 5 minutes per team
- Approach: oral presentation and one word page only
- Agenda:
  - Project briefing and teaming
  - Expected deliverables 
  - Current progress
  - Support needed (if any)
