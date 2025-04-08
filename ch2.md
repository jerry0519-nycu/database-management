# Chapter 2: Data Models
- Data modeling is to build data models, which is the first step in the database design journey, <span class="brown-text">serving as a bridge</span> between real-world objects and the computer database.
- One big problem of database design is that designers, programmers, and end users see data in different ways, which introduce <span class="brown-text">misunderstanding</span> and increase communication cost.
- <span class="brown-text">Database designers </span>must obtain a precise description (<span class="brown-text">data model</span>) of the data's nature and environments within the organization to reduce communication efforts.
- 資料建模是建立資料模型的過程，它是資料庫設計過程中的第一步，作為現實世界物件與電腦資料庫之間的橋樑。
- 資料庫設計的一大問題是設計師、程式員和最終使用者對資料的看法不同，這會引起誤解並增加溝通成本。
- 資料庫設計師必須獲得有關資料的性質和在組織內環境的準確描述（資料模型），以減少溝通的努力。

# Data Modeling and Data Models
- Data modeling refers to the <span class="brown-text">process</span> of creating a specific data model for a determined problem domain (mini-world). 
- Data modeling is an iterative, progressive process.
- A <span class="brown-text">data model</span> is a relatively simple representation of more complex real-world objects
  - Entity (table)
  - Attribute (column)
  - Relationship (linkage between tables)
  - Constraint
- 資料建模是指為特定問題領域（迷你世界）創建具體資料模型的過程。  
- 資料建模是一個迭代且逐步進行的過程。  
- 資料模型是對更複雜的現實世界物件的一個相對簡單的表示。  
  - 實體（表格）  
  - 屬性（欄位）  
  - 關聯（表格之間的連結）  
  - 約束

1. 實體（Entity）= 表（Table）
- 定義：實體代表現實世界中的一個對象，通常在關聯式資料庫中對應到一張表（table）。
- 範例：在一個學生管理系統中，「學生（Student）」可以是一個實體，對應到一張Student 表。
  另一個實體可以是「課程（Course）」表。
  
2. 屬性（Attribute）= 欄位（Column）
- 定義：屬性是實體的特徵或屬性，在資料庫表中對應到欄位（column）。
- 範例：
在 Student 表中，可以有以下欄位：Student_ID（學生編號）、Name（姓名）、Age（年齡）、Major（主修科目）
這些欄位代表「學生」這個實體的各種屬性。

3. 關聯（Relationship）= 表與表之間的連結
- 定義：關聯描述兩個或多個實體之間的關係，在資料庫中通常透過 **外鍵（Foreign Key）** 來實現。
- 範例：學生（Student）和課程（Course）之間的關係：
一個學生可以修多門課（一對多關係）。
一門課可以有多個學生選修（多對多關係）。
  - 通常，我們會建立一張 **選課表（Enrollment）** 來存儲這種關係，其中包含：
    - Student_ID（對應 Student 表）
    - Course_ID（對應 Course 表）
4. 約束（Constraint）= 限制條件
- 定義：約束是一組規則，確保數據的一致性和完整性。
- 常見約束類型：
  - 主鍵（Primary Key, PK）：唯一標識表中的每一行，例如 Student_ID 不能重複。
  - 外鍵（Foreign Key, FK）：確保兩個表之間的關聯，例如 Enrollment 表中的 Student_ID 必須存在於 Student 表中。
  - 唯一性約束（UNIQUE）：確保某個欄位的值不重複，例如學生的學號不能重複。
  - 非空約束（NOT NULL）：確保欄位不能為空，例如 Name 欄位不能為空值。

#### 總結
| 概念	| 對應資料庫元素 |	功能 |
|-------|---------------|------|
|實體（Entity）|表（Table）|代表現實世界的對象，如學生或課程|
|屬性（Attribute）|欄位（Column）|代表實體的特徵，如姓名、學號
|關聯（Relationship）|表之間的外鍵關係|連結不同表，如學生和課程的選修關係
|約束（Constraint）|限制條件|確保數據正確，如主鍵、外鍵、唯一性等

# The Importance of Data Models
- Data models are a <span class="brown-text">communication tool</span>
  - End users know the business rule running in real world
  - Developers develop aps to manage data and transform data into information
  - People view data in different ways
    - Managers want a universal view of data
    - Staffs need details of data
- A good database system environment requires an overall database design based on an appropriate data model
- No appropriate data model, no good database system environment

- 資料模型是溝通工具  
  - 最終使用者了解現實世界中的業務規則  
  - 開發者開發應用程式來管理資料並將資料轉換為資訊  
  - 人們對資料的看法不同  
    - 管理者希望擁有資料的整體視圖  
    - 員工需要資料的細節  
  - 一個好的資料庫系統環境需要基於適當資料模型的整體資料庫設計  
  - 沒有適當的資料模型，就沒有好的資料庫系統環境

# Data Model Basic Building Blocks
- An <span class="brown-text">entity</span> is a person, thing or event about which data will be collected and stored
- An <span class="brown-text">attribute</span> is a characteristic (property) of an entity
- A <span class="brown-text">relationship</span> describes an association among entities
  - One-to-many (1:M or 1..*): PAINTER paints PAINTING
  - Many-to-many (M:N or \*..\*): EMPLOYEE learn SKILL
  - One-to-one (1:1 or 1..1): EMPLOYEE manage STORE
- A <span class="brown-text">constraint</span> is a restriction placed on the data to help data integrity
  - An employee’s salary must have values between 6,000 and 350,000
  - Each class must have one and only one teacher
 
- 實體是指將收集和儲存資料的對象，可以是人、事物或事件  
- 屬性是實體的特徵（屬性）  
- 關聯描述實體之間的聯繫  
  - 一對多（1:M 或 1..*）：畫家（PAINTER）畫畫（PAINTING）  
  - 多對多（M:N 或 *..*）：員工（EMPLOYEE）學習技能（SKILL）  
  - 一對一（1:1 或 1..1）：員工（EMPLOYEE）管理商店（STORE）  
- 約束是對資料施加的限制，以達成資料完整性  
  - 員工的薪資必須在 6,000 和 350,000 之間  
  - 每個班級必須有且只有一位老師

# Business Rules
- A **business rule** is a brief, precise, and unambiguous description of a policy, procedure, or principle within a specific organization
  - made from company managers, policy makers, department managers, and written procedures
  - used to define entities, attributes, relationships, and constraints
- Example: A customer may generate many invoices' may be translated into data model
  - Customer and invoice are objects of interest and should be represented by respective <span class="brown-text">entities</span>
  - There is a **'generate'** <span class="brown-text">relationship</span> between customer and invoice
  - The generate relationship is one-to-many (1:M)

- 業務規則是對特定組織內政策、程序或原則的簡短、精確且明確的描述，  
  - 由公司經理、政策制定者、部門經理和書面程序制定。  
  - 用來定義實體、屬性、關聯和約束。  
- 範例： "一個顧客可能會產生多個發票" 可以轉換成資料模型。  
  - 顧客和發票是關注的對象，應該分別由相應的實體表示。  
  - 顧客和發票之間存在一個 "生成" 的關聯。  
  - 這個生成關聯是一對多（1:M）的關係。

# Naming Conventions
- Names should be descriptive and familiar to the users
- A good naming convention can 
  - Make less confusion and reduce errors
  - Promote code consistently and readability 
- Follow organization practice or develop at the start of project by considering
  - Should table name and column name be singular or plural? (student or students)
  - Should prefix tables or columns? (name or prod_name)
  - Should use capital letters for naming? (cap_cap, capCap or CapCap)
  - Which terminology should be selected? (user, person or people)

- 名稱應該具描述性並且對使用者熟悉  
- 良好的命名規範可以：  
  - 減少混淆並降低錯誤  
  - 促進代碼的一致性和可讀性  
  - 跟隨組織的慣例，或在專案開始時就考慮並制定規範  

- 應考慮以下問題：  
  - 表格名稱和欄位名稱應該是單數還是複數？（例如：student 還是 students）  
  - 是否應該為表格或欄位添加前綴？（例如：name 還是 prod_name）  
  - 命名時應該使用大寫字母嗎？（例如：cap_cap、capCap 還是 CapCap）  
  - 應該選擇哪種術語？（例如：user、person 還是 people）

# Supplement - Naming Conventions
[Udemy Video of naming conventions](https://youtu.be/xFs8H_YHqHc?si=2m55anO7oxjQ6a8h)
[Naming conventions of MySQL](https://medium.com/@centizennationwide/mysql-naming-conventions-e3a6f6219efe)

Encapsulation throughout this video: This tutorial focuses on database table and field naming conventions, emphasizing the importance of consistency and a well-defined approach. It discusses various formats, the significance of terminology, and the need for guidelines at the project's start. Ultimately, a clear naming convention enhances collaboration and efficiency in database management.

# The Evolution of Data Models
Data models represent a lot of thought as to what a database is, what it should do, the types of structures that it should employ, and the technology that would be used to implement these structures


<img width="478" alt="image" src="https://github.com/user-attachments/assets/bb41ae3b-6af5-4a22-914b-7f25fdff5a48" />


### **主要資料模型的演進**  

資料模型的發展經歷了幾個重要階段，從最早的層次模型到現代的 NoSQL 和雲端資料庫，這些模型的演變反映了技術進步與業務需求的變化。以下是主要資料模型的演進過程：  

---

### **1. 層次式資料模型（Hierarchical Model，1960s）**  
- 這是最早的資料庫模型，由 IBM 在 1960 年代開發（如 IMS 資料庫）。  
- **結構**：數據以**樹狀結構**組織，父節點可以有多個子節點，但每個子節點只能有一個父節點（類似目錄與檔案的關係）。  
- **優點**：存取速度快，適合固定結構的數據，如銀行交易記錄。  
- **缺點**：不靈活，數據關聯難以修改，不適合多對多關係。  
- **應用**：早期銀行系統、製造業。  

![image](https://github.com/user-attachments/assets/de39bbe9-1352-4cd8-a652-96180b58e9b7)

---

### **2. 網狀資料模型（Network Model，1970s）**  
- 由 CODASYL（Conference on Data Systems Languages）於 1970 年代開發，試圖解決層次模型的限制。  
- **結構**：採用**圖結構**，允許一個節點有多個父節點，支援多對多關係。  
- **優點**：比層次模型靈活，適合複雜數據關係。  
- **缺點**：查詢需要透過指標（pointers）導航，管理困難。  
- **應用**：政府、企業系統，如早期的航班預訂系統。  

![bg right:50% w:600 network model](https://www.myreadingroom.co.in/images/stories/docs/dbms/Network%20Data%20Model.JPG)

在網路模型中，使用者將網路資料庫視為一組具有**一對多（1:M）關係**的記錄集合。然而，與層次模型不同，網路模型允許**一條記錄擁有多個父節點**。  

- **層次模型（Hierarchical Model）**：  
  - 資料以**樹狀結構**組織，每條記錄（子節點）只能有一個父節點。  
  - 例如：公司組織架構（一個部門下有多個員工，但每個員工只能屬於一個部門）。  

- **網路模型（Network Model）**：  
  - 資料以**圖形結構**組織，允許**多對多關係**，一條記錄可連結到多個父節點。  
  - 例如：學生選課系統（一個學生可選多門課，一門課也可被多個學生選修）。  

### 對比：
| 特性                | 層次模型                     | 網路模型                     |
|---------------------|----------------------------|----------------------------|
| **結構**            | 樹狀（單一父節點）           | 圖形（多父節點）             |
| **靈活性**          | 低（固定層級）               | 高（複雜關聯）               |
| **應用場景**        | 早期銀行系統、固定階層資料   | 複雜關聯資料（如訂單系統）   |  

網路模型解決了層次模型在表達複雜關聯上的限制，但因其複雜性，後續逐漸被關聯式模型（Relational Model）取代。

---

### **3. 關聯式資料模型（Relational Model，1980s - 1990s）**  
- 由 E.F. Codd 於 1970 年代提出，1980 年代開始流行，至今仍是主流。  
- **結構**：數據存儲在**表格（table）**中，每個表有**欄（column）**與**行（row）**，不同表之間透過 **外鍵（Foreign Key）** 建立關聯。  
- **優點**：
  - 具備**SQL（Structured Query Language）**，易於操作與管理。  
  - 符合數據正規化（Normalization），減少冗餘，確保一致性。  
  - 強大的數據完整性與事務管理（ACID）。  
- **缺點**：  
  - 擴展性有限（Scaling Up），大規模數據處理效能下降。  
  - 結構固定，對非結構化數據（如 JSON、圖像）支援不佳。  
- **應用**：幾乎所有企業應用，如銀行、電商、ERP 系統。  
- **代表資料庫**：MySQL、PostgreSQL、Oracle、SQL Server。
*:SQL（Structured Query Language，結構化查詢語言） 是一種專門用於管理和操作關聯式資料庫（RDBMS）的標準化程式語言。它允許使用者對資料庫進行查詢（Query）、新增（Insert）、修改（Update）、刪除（Delete）等操作，並管理資料庫結構（如創建表、設定權限等）。

---

### **4. 物件導向資料模型（Object-Oriented Model，1990s）**  
- 1990 年代興起，整合物件導向程式設計（OOP）與資料庫技術。  
- **結構**：數據以 **物件（Object）** 的方式存儲，支援封裝、繼承等 OOP 特性。  
- **優點**：  
  - 適合複雜數據類型，如多媒體、地理資訊系統（GIS）。  
  - 更適合與物件導向程式語言（如 Java、C++）整合。  
- **缺點**：查詢效率不如關聯式資料庫，且不易推廣。  
- **應用**：工程設計、CAD 軟體、3D 模型存儲。  
- **代表資料庫**：db4o、ObjectDB。  

![image](https://github.com/user-attachments/assets/579f39bc-8204-4185-b7eb-3f403eb7ca71)

| 比較項目       | 物件導向 (OOP)                          | 關聯式資料庫 (SQL)                     |
|----------------|----------------------------------------|----------------------------------------|
| **怎麼存資料**  | 用「物件」存，物件可以包物件<br>（例如公司物件裡面包部門物件） | 用「表格」存，表格之間用ID關聯<br>（例如公司表和部門表用公司ID連結） |
| **關係處理**    | 直接寫在程式碼裡<br>`公司.部門 = 新部門` | 要另外建關聯表<br>`公司表`↔`公司部門關聯表`↔`部門表` |
| **查詢資料**    | 像寫程式一樣直接呼叫<br>`公司.取得所有部門()` | 要寫SQL指令<br>`SELECT * FROM 部門 WHERE 公司ID=123` |
| **適合情境**    | 用在程式語言裡<br>(如Java/Python物件) | 用在資料庫系統<br>(如MySQL/Oracle) |
| **優點**       | 寫程式時很直覺                         | 處理大量資料時效率高                   |
| **缺點**       | 存到資料庫時要轉換                     | 要一直寫JOIN聯表查詢                   |

### **比喻**
- **物件導向**像「便當盒」：
  - 主菜、配菜都放在同一個盒子裡
  - 打開就直接看到所有東西

- **關聯式資料庫**像「自助餐餐檯」：
  - 飯、菜、湯都分開放
  - 要自己拿盤子把想吃的組合起來

---

### **5. NoSQL 資料模型（2000s - 至今）**  
- 由於 Web 2.0、大數據（Big Data）、雲端運算興起，NoSQL（Not Only SQL）資料庫在 2000 年代後期興起。  
- **結構**：根據不同需求，NoSQL 分為四種類型：
  1. **Key-Value 存儲（鍵值型）**：類似字典，如 Redis。  
  2. **文檔型（Document-based）**：存儲 JSON 或 BSON，如 MongoDB。  
  3. **列存儲（Column-family）**：適合大數據分析，如 Apache Cassandra。  
  4. **圖形資料庫（Graph Database）**：處理社交網絡關係，如 Neo4j。  
- **優點**：
  - 支援非結構化或半結構化數據，如 JSON、XML。  
  - 高擴展性（Scaling Out），可分佈式存儲。  
  - 適用於即時數據、大數據處理。  
- **缺點**：
  - 缺乏標準化語言（不像 SQL），不同 NoSQL 系統間不兼容。  
  - 一般不支援 ACID 事務，適合最終一致性（Eventual Consistency）。  
- **應用**：社交媒體（Facebook、Twitter）、電商（Amazon）、物聯網（IoT）。  
- **代表資料庫**：MongoDB、Cassandra、Redis、Neo4j。  

---

### **6. 雲端與新興資料庫技術（2020s - 至今）**  
- 現代資料庫進一步發展，結合雲端運算、AI、自動化管理等技術。  
- **發展趨勢**：
  - **雲端原生資料庫（Cloud-native Database）**：如 Amazon Aurora、Google Spanner。  
  - **NewSQL**（結合 SQL 與 NoSQL 優勢）：如 CockroachDB、Google Spanner。  
  - **分佈式資料庫（Distributed Database）**：適合全球部署，如 TiDB、YugabyteDB。  
  - **AI/機器學習與資料庫整合**：如 Snowflake 提供智能數據分析。  


| 時代 | 資料模型 | 特點 | 代表技術 |  
|------|---------|------|---------|  
| 1960s | 層次式（Hierarchical） | 樹狀結構，固定格式 | IBM IMS |  
| 1970s | 網狀（Network） | 多對多關聯，需用指標 | CODASYL |  
| 1980s | 關聯式（Relational） | 表格結構，SQL，ACID | MySQL、PostgreSQL、Oracle |  
| 1990s | 物件導向（Object-Oriented） | 物件存儲，OOP 整合 | ObjectDB、db4o |  
| 2000s | NoSQL | 非結構化，高擴展性 | MongoDB、Cassandra、Redis |  
| 2020s | 雲端/分佈式 | 雲端原生、AI 整合 | Spanner、TiDB、Snowflake |  


| 世代 | 時期 | 資料模型 | 代表技術 | 關鍵特性 |
|------|------|----------|----------|----------|
| **第一代** | 1960s-1970s | 檔案系統 | IBM VSAM | 無關聯性，僅管理單一檔案 |
| **第二代** | 1970s | 層次式/網狀 | IMS, IDS-II | 樹狀/圖形結構，需手動導航 | 
| **第三代** | 1980s | 關聯式 | MySQL, Oracle | 表格結構，SQL標準化查詢 |
| **第四代** | 1990s | 物件導向 | DB2 UDB | 支援物件繼承、封裝 | 
| **第五代** | 2000s | XML/混合式 | MongoDB | 半結構化資料，NoSQL興起 | 
| **新興模型** | 2010s-現在 | NoSQL | Cassandra, Redis | 分散式、高擴展性 | 

---

### **生活化比喻**  
1. **檔案系統** → **紙本檔案櫃**  
   - 每份文件獨立存放，要找關聯得自己翻箱倒櫃。  
2. **層次式(Hierarchical)/網狀模型(Network)** → **家族族譜**  
   - 層次式：像嚴格的家族樹（爸爸→兒子→孫子）。  
   - 網狀式：像複雜的社交關係（一個人可有多個上司和朋友）。  
3. **關聯式模型** → **Excel表格**  
   - 所有資料整齊分欄分列，用「編號」連結不同表格（如訂單表連客戶表）。  
4. **物件導向模型** → **樂高積木**  
   - 每個積木（物件）可嵌套其他積木，組裝方式自由（如公司物件包含部門物件）。  
5. **NoSQL** → **便利貼牆**  
   - 資料像便利貼隨意貼，形式不拘（文檔、鍵值、圖形），適合快速擴充。  

資料模型的發展趨勢從早期**結構化、高一致性**的設計，逐漸轉向**靈活性、高擴展性**的架構，未來隨著 AI、大數據、雲端技術的進步，資料庫將更加智能化與自動化。

![螢幕擷取畫面 2025-03-27 221430](https://github.com/user-attachments/assets/dcf51438-6ade-4b41-89fd-247a6abdd244)

# Database Concepts Inherited from Network Model
- The <span class="brown-text">**schema**</span> is the conceptual and structural definition of a whole database. Once you claim the schema of a database, it must now no longer be modified often because it will distort the data organization inside the Database. 
- The <span class="brown-text">**data manipulation language (DML)**</span> defines the way to insert, read, update, delete data in database
- A <span class="brown-text">**schema data definition language (DDL)**</span> enables the DBA to define the schema components (create, drop, alter table, create index or trigger)

- 架構是整個資料庫的概念性和結構性定義。一旦確定了資料庫的架構，就不應該經常修改，因為這會扭曲資料庫內部的資料組織。  
- 資料操作語言（DML）定義了如何在資料庫中插入、讀取、更新和刪除資料。
- 資料定義語言（DDL）使資料庫管理員（DBA）能夠定義架構組件（例如：創建、刪除、修改表格，創建索引或觸發器）。
  
# Relational Model
The relational model’s foundation is a mathematical concept known as a relation, which is introduced by Edgar F. Codd in 1969.
- Relation: a table with columns and rows.
- Attribute: a named column of a relation.
- Domain: the set of allowable values for one or more attributes.
- Tuple: a row of a relation
  
![bg right:40% w:500 relational model](https://www.w3schools.in/wp-content/uploads/2016/08/Relational-Model-Terms.png?ezimgfmt=rs:503x343/rscb53/ng:webp/ngcb52)

- 關聯：一個包含欄位和列的表格。  
- 屬性：關聯中的一個命名欄位。  
- 域：一個或多個屬性的可允許值的集合。
- 元組 : 資料表中的一行


| 術語 | 對應資料庫概念 | 範例 | **Domain（值域）** |  
|------------|--------------|------|------------------|  
| **Relation** | 資料表（Table） | `Student` | - |  
| **Attribute** | 欄位（Column） | `Student_ID`, `Name`, `Age`, `Major` | `Student_ID`: 字串（如 "S001"）<br>`Age`: 整數（18~30） |  
| **Tuple** | 資料列（Row） | `(S001, 張小明, 20, 資工系)` | 必須符合各欄位的 Domain 限制 |  


  
# Relational Diagram

<img width="630" alt="image" src="https://github.com/user-attachments/assets/b21f3909-0cce-405a-b8b8-1f80072ce88d" />


# Supplement of Relational Model
- Relation schema
- Relational database schema
- Degree of a relation
- Cardinality of a relation
- Relation state (or relation instance)
  
[Relational model terminology](https://youtu.be/Q45sr5p_NmQ?si=cr53etNXoX1BIpLf)

#### 1. Relation Schema (關聯綱要)
- **定義**：描述關聯的結構，包含關聯名稱和屬性集合
- **表示法**：R(A₁, A₂,..., Aₙ)
  - 例如：學生(學號, 姓名, 年齡, 系所)
- **特點**：
  - 不包含實際數據
  - 定義屬性的域名(數據類型)和約束條件
  - 類似於"表格的藍圖"

#### 2. Relational Database Schema (資料庫綱要)
- **定義**：一組關聯綱要的集合，加上完整性約束
- **組成**：
  - 多個關聯綱要
  - 屬性間的映射關係
  - 完整性約束(主鍵、外鍵等)
- **範例**：
  - 學生(學號, 姓名, 年齡, 系所)
  - 課程(課程編號, 課程名, 學分)
  - 選課(學號, 課程編號, 成績)

#### 3. Degree of a Relation (關聯的維度/屬性數)
- **定義**：關聯中屬性的數量
- **計算**：計算關聯綱要中的屬性個數
- **範例**：
  - 學生(學號, 姓名, 年齡, 系所) → 維度=4
  - 課程(課程編號, 課程名) → 維度=2

#### 4. Cardinality of a Relation (關聯的基數/元組數)
- **定義**：關聯實例中的元組(記錄)數量
- **特性**：
  - 隨數據增刪動態變化
  - 不同時間點可能不同
- **範例**：
  - 學生表有100條記錄 → 基數=100
  - 課程表有30條記錄 → 基數=30

#### 5. Relation State/Instance (關聯狀態/實例)
- **定義**：特定時間點關聯中的元組集合
- **特性**：
  - 關聯的具體數據內容
  - 隨時間變化而改變
  - 必須符合關聯綱要的定義
- **範例**：
  ```
  學生實例：
  | 學號 | 姓名 | 年齡 | 系所 |
  |------|------|------|------|
  | S001 | 王明 | 20   | 資工 |
  | S002 | 李華 | 21   | 電機 |
  ```

#### 概念對照表
| 術語 | 中文 | 說明 | 範例 |
|------|------|------|------|
| Relation Schema | 關聯綱要 | 表格結構定義 | 學生(學號,姓名,年齡) |
| Database Schema | 資料庫綱要 | 整個資料庫的結構定義 | 學生+課程+選課表結構 |
| Degree | 維度 | 屬性(欄位)數量 | 學生表有4個屬性 |
| Cardinality | 基數 | 記錄(元組)數量 | 學生表有100筆資料 |
| Relation Instance | 關聯實例 | 特定時間的數據內容 | 當前學生表的所有記錄 |


# Entity Relationship Model
- Although the relational model was a vast improvement over the hierarchical and network models, it still lacked the features that would make it an effective database design tool.
- Database designers prefer to use a graphical tool in which entities and their relationships are pictured.
- The <span class="brown-text">**entity relationship model (ERM)**</span> using *graphical representations* to model database components has become a widely accepted standard for data modeling.
- The relational data model and ERM combined to provide the foundation for tightly structured database design

- 儘管關聯模型比層次模型和網絡模型有了很大的改進，但它仍然缺乏一些特徵，無法成為一個有效的資料庫設計工具。  
- 資料庫設計師更偏好使用圖形工具來描繪實體及其關聯。  
- 實體關聯模型（ERM）利用圖形表示來建模資料庫組件，已成為資料建模的廣泛接受標準。  
- 關聯資料模型和實體關聯模型的結合，為緊密結構化的資料庫設計提供了基礎。

# Entity Relationship Model Notation
- Entity – an entity is represented in the ERD by a rectangle (entity box)
- Attributes – each entity consists of a set of attributes that describes particular characteristics of the entity
- Relationships – relationships describe associations among data

<img width="466" alt="image" src="https://github.com/user-attachments/assets/014237d8-e410-4a75-877b-7f8c1337206a" />


- 實體（Entity）– 實體在實體關聯圖（ERD）中由矩形（實體框）表示。  
- 屬性（Attributes）– 每個實體由一組屬性組成，這些屬性描述了實體的特定特徵。  
- 關聯（Relationships）– 關聯描述了資料之間的聯繫。

# Crow's Foot Notations

**Four basic types of cardinality constraints:**

![bg right:50% w:600 Crow's Foot notation](https://discourse.omnigroup.com/uploads/default/original/2X/5/54b713a5fe9dc79b458b8afe1a5a148320ba132d.gif)

#### **1. Exactly One (嚴格一個)**
- **符號表示**：`1` 或 `|`（直線）
- **意義**：  
  必須存在**且僅存在一個**對應實體。  
- **範例**：  
  「每位學生 **必須** 屬於 **一個且只有一個** 班級」  
  （學生:班級 = 1:1 強制關係）

#### **2. Zero or One (零或一個)**
- **符號表示**：`0..1` 或 `○—|`（圓圈加直線）  
- **意義**：  
  最多存在一個對應實體，也可能不存在。  
- **範例**：  
  「一位員工 **可能** 分配至 **至多一個** 專案，也可能未分配」  
  （員工:專案 = 0或1的選擇性關係）

#### **3. Zero, One, or More (零、一或多個)**
- **符號表示**：`*` 或 `○—<`（烏鴉腳符號）  
- **意義**：  
  對應實體的數量沒有限制（可以不存在、存在一個或多個）。  
- **範例**：  
  「一位顧客 **可以沒有** 訂單，也可以有 **多筆** 訂單」  
  （顧客:訂單 = 1:N 的常見關係）

#### **4. One or More (至少一個)**
- **符號表示**：`1..*` 或 `|—<`（直線加烏鴉腳）  
- **意義**：  
  必須存在 **至少一個**，且允許多個對應實體。  
- **範例**：  
  「一門課程 **必須有** **至少一位** 學生選修，也可以有多位」  
  （課程:學生 = 強制的1:N關係）


# Relational Model vs Entity Relationship Model
ER Model first, then converted into Relational Model for DBMS implementation.

|Aspect	| ER Model	| Relational Model
|-------|-----------|-----------------
Used For|	Conceptual database design|	Logical database implementation
Representation|	ER Diagram (graphical)|	Tables (relational schema)
Elements|	Entities, Attributes, Relationships|	Tables, Attributes, Tuples
Constraints|	Cardinality in ER Diagram|	Primary/Foreign keys, SQL constraints
Conversion|	Converted to Relational Model|	Implemented in DBMS


| 方面         | ER 模型                  | 關聯模型                  |
|--------------|--------------------------|--------------------------|
| 用途         | 概念性資料庫設計          | 邏輯性資料庫實現          |
| 表示方式     | ER 圖（圖形化）          | 表格（關聯綱要）          |
| 元素         | 實體、屬性、關係          | 表格、屬性、元組          |
| 約束         | ER 圖中的基數約束         | 主鍵/外鍵、SQL 約束       |
| 轉換         | 轉換為關聯模型            | 在 DBMS 中實現            |

# Object-Oriented Model
In the object-oriented data model (OODM), both data and its relationship are contained in a single structure known as an object
- **Object**: an abstraction of a real-world entity
- **Attributes**: describe the properties of an object
- **Method**: represents a real-world action
- **Class**: a collection of similar objects with shared structure and behavior
- **Inheritance**: an object within the *class hierarchy* to inherit the attributes and methods of the classes above it. (class EMPLOYEE and CUSTOMER can be created as subclasses inherit from the class PERSON)
- OODM are typically depicted using Unified Modeling Language (UML) class diagrams

在物件導向資料模型（OODM）中，資料及其關聯都包含在一個稱為物件的單一結構中。  
- 物件（Object）：現實世界實體的抽象表示。  
- 屬性（Attributes）：描述物件的特徵。  
- 方法（Method）：表示現實世界的動作。  
- 類別（Class）：一組具有相似結構和行為的物件的集合。  
- 繼承（Inheritance）：類別層次結構中的物件可以繼承其上層類別的屬性和方法。（例如：可以創建員工（EMPLOYEE）和顧客（CUSTOMER）作為子類，繼承自人員（PERSON）類別）  
- OODM 通常使用統一建模語言（UML）類別圖來表示。

# OODM Diagram
<img width="464" alt="image" src="https://github.com/user-attachments/assets/84dc3562-68f3-430c-8193-b1b1d6f6b627" />

| 差異點 | UML 類別圖 | ER 模型 |
|---|---|---|
| **是否含方法** | ✅ 有（如計算金額） | ❌ 無 |
| **關聯描述** | 強調「行為」<br>（如「下單」動作） | 強調「結構」<br>（如「客戶-訂單」關係） |
| **多重性標註** | 用數字（`1..*`） | 用符號（如 `o{`） |
| **細節程度** | 高（連程式邏輯都畫） | 低（只存資料結構） |


# ERDM and O/R DBMS
- The extended relational data model (ERDM) adds many of the OO model’s features within the simpler relational database structure
- A DBMS based on the ERDM is an object/relational database management system (O/R DBMS)
  
- 擴展關聯資料模型（ERDM）在較簡單的關聯資料庫結構中加入了許多物件導向模型（OO模型）的特徵。  
- 基於ERDM的資料庫管理系統（DBMS）稱為物件/關聯資料庫管理系統（O/R DBMS）。

# Comparison of RDBMS, OODBMS and O/R DBMS

Feature	|RDBMS|	OODBMS|	O/R DBMS
--------|------------------|--------------------------|-------------------
Tables & SQL	|✅ Yes	|❌ No|	✅ Yes
Objects & Classes	|❌ No	|✅ Yes|	✅ Yes
Inheritance	|❌ No|	✅ Yes|	✅ Yes
Encapsulation (Methods in DB)|	❌ No|	✅ Yes|	✅ Yes
Complex Data Types	|❌ No|	✅ Yes|	✅ Yes

1. **關聯式資料庫 (RDBMS) - 用表格存資料，靠 SQL 查詢的傳統資料庫**  
   - **代表產品**：MySQL、Oracle、SQL Server  
   - **核心優勢**：標準化 SQL 查詢、交易完整性（ACID）  
   - **限制**：無法直接儲存物件，需拆解成表格（ORM 轉換）
   - ERD主要用於RDBMS的設計，另外兩者較不適用

2. **物件導向資料庫 (OODBMS) - 直接存物件，適合複雜結構的現代資料庫**  
   - **代表產品**：MongoDB（文檔型）、Neo4j（圖形資料庫）  
   - **核心優勢**：原生支援物件儲存，適合複雜資料結構  
   - **限制**：缺乏標準查詢語言，學習曲線較陡  

3. **物件/關聯混合資料庫 (O/R DBMS) - 能同時用 SQL 查表格，也能存物件的兩用資料庫**  
   - **代表產品**：PostgreSQL、Oracle 12c+  
   - **核心優勢**：同時支援 SQL 和物件特性（如 JSON 欄位、自訂類型）  
   - **典型應用**：需要兼顧傳統表格與現代物件儲存的系統  

---

### **選擇建議**
- **用 RDBMS 當你的資料...**  
  ✅ 高度結構化  
  ✅ 需要複雜 JOIN 查詢  
  ✅ 重視交易完整性（如銀行系統）  

- **用 OODBMS 當你的資料...**  
  ✅ 結構多變（如社交媒體貼文）  
  ✅ 有複雜階層（如 CAD 設計圖）  
  ✅ 需要高效能讀寫（如 IoT 即時數據）  

- **用 O/R DBMS 當你...**  
  ✅ 既要 SQL 查詢又要物件靈活性  
  ✅ 逐步遷移舊系統到現代架構  

<details>
  <summary><strong>三種資料庫舉例</strong></summary>
  
### **情境描述**  
假設我們需要儲存以下資訊：  
1. **學生**：學號、姓名、年齡、聯絡電話（可能有多筆）。  
2. **課程**：課程代碼、名稱、學分。  
3. **選課記錄**：學生與課程的關聯，包含成績。  

## **1. RDBMS（關聯式資料庫）**
**核心**：用 **表格（Table）** 儲存資料，透過外來鍵（Foreign Key）建立關聯。  

### **資料表設計**  
#### **學生表（Students）**
| student_id (PK) | name  | age |
|------------------|-------|-----|
| "S001"          | "張三" | 20  |
| "S002"          | "李四" | 22  |

#### **聯絡電話表（Phones）**
| phone_id (PK) | student_id (FK) | phone_number |
|---------------|------------------|--------------|
| 1             | "S001"           | "0912345678" |
| 2             | "S001"           | "0223456789" |

#### **課程表（Courses）**
| course_id (PK) | name       | credits |
|----------------|------------|---------|
| "C101"         | "資料庫"    | 3       |
| "C102"         | "演算法"    | 4       |

#### **選課記錄表（Enrollments）**
| enrollment_id (PK) | student_id (FK) | course_id (FK) | grade |
|--------------------|------------------|----------------|-------|
| 1                  | "S001"           | "C101"         | 85    |
| 2                  | "S001"           | "C102"         | 90    |

### **特點**  
- **正規化**：資料拆分成多個表格，避免冗餘。  
- **查詢方式**：需使用 **JOIN** 操作（例如：查詢「張三的成績」需關聯 `Students`、`Enrollments`、`Courses`）。  
- **缺點**：處理複雜物件（如學生的多筆電話）需額外表格，查詢效率可能較低。  

## **2. OODBMS（物件導向資料庫）**
**核心**：直接儲存 **物件（Object）**，支援繼承、聚合等 OOP 特性。  

### **物件設計**  
#### **學生類別（Student）**
```java
class Student {
  String student_id;
  String name;
  int age;
  List<String> phones;  // 直接儲存多筆電話（無需拆表）
  List<Enrollment> enrollments;  // 儲存選課記錄（物件引用）
}
```

#### **課程類別（Course）**
```java
class Course {
  String course_id;
  String name;
  int credits;
}
```

#### **選課記錄類別（Enrollment）**
```java
class Enrollment {
  Student student;  // 直接引用學生物件
  Course course;    // 直接引用課程物件
  int grade;
}
```

### **實際儲存範例**  
```json
// 學生張三的物件
{
  "student_id": "S001",
  "name": "張三",
  "age": 20,
  "phones": ["0912345678", "0223456789"],
  "enrollments": [
    {
      "course": {"course_id": "C101", "name": "資料庫", "credits": 3},
      "grade": 85
    },
    {
      "course": {"course_id": "C102", "name": "演算法", "credits": 4},
      "grade": 90
    }
  ]
}
```

### **特點**  
- **無需正規化**：物件內可直接嵌套資料（如 `phones` 是陣列，`enrollments` 是物件列表）。  
- **查詢直接**：例如「取得張三的所有課程」只需讀取 `Student` 物件，無需 JOIN。  
- **缺點**：複雜查詢（如「全校成績 > 90 的學生」）可能效能較差，且標準化程度低。  

## **3. ORDBMS（物件關聯式資料庫）**
**核心**：結合 RDBMS 的表格結構 + OODBMS 的物件特性（如自訂型別、陣列）。  

### **資料表設計（以 PostgreSQL 為例）**  
#### **自訂型別（Type）**
```sql
CREATE TYPE phone_type AS (number VARCHAR(20));
CREATE TYPE enrollment_type AS (
  course_id VARCHAR(10),
  grade INT
);
```

#### **學生表（Students）**
```sql
CREATE TABLE Students (
  student_id VARCHAR(10) PRIMARY KEY,
  name VARCHAR(50),
  age INT,
  phones phone_type[],  -- 儲存電話陣列（無需拆表）
  enrollments enrollment_type[]  -- 儲存選課記錄陣列
);
```

#### **課程表（Courses）**
```sql
CREATE TABLE Courses (
  course_id VARCHAR(10) PRIMARY KEY,
  name VARCHAR(50),
  credits INT
);
```

### **實際資料範例**  
```sql
-- 插入學生資料（含嵌套物件）
INSERT INTO Students VALUES (
  'S001', '張三', 20,
  ARRAY[('0912345678'), ('0223456789')]::phone_type[],
  ARRAY[('C101', 85), ('C102', 90)]::enrollment_type[]
);
```

### **特點**  
- **混合優勢**：  
  - 保留表格結構（支援 SQL 查詢）。  
  - 允許欄位儲存複雜資料（如陣列、JSON）。  
- **查詢範例**：  
  ```sql
  -- 查詢張三的所有電話
  SELECT unnest(phones) FROM Students WHERE student_id = 'S001';
  
  -- 查詢成績 > 85 的課程（需解開嵌套陣列）
  SELECT course_id, grade 
  FROM Students, unnest(enrollments) AS e 
  WHERE student_id = 'S001' AND e.grade > 85;
  ```
- **缺點**：查詢嵌套資料時語法較複雜。  

### **實際應用建議**  
- **RDBMS**：需要嚴格 ACID 的交易系統（如銀行）。  
- **OODBMS**：遊戲、CAD 等需高效讀寫物件的場景。  
- **ORDBMS**：需部分物件特性但不想放棄 SQL 的系統（如地理資訊系統）。  

</details>

Products of O/R DBMS
- <span class="small-text">PostgreSQL (most commonly used O/R DBMS)</span>
-	<span class="small-text">Oracle Database (with Object-Relational Features)</span>
- <span class="small-text">Microsoft SQL Server (limited Object-Relational capabilities)</span>

# Emerging Data Models: Big Data and NoSQL
- **Big Data** refers to a movement to find new and better ways to manage large amounts which DBMS can not manage
- Big Data characteristics (3 Vs) : volume, velocity, and variety
- Most frequently used Big Data technologies
  - Hadoop: an **ecosystem** provides a collection of softwares to operate big data
  - Hadoop Distributed File System (HDFS) is a fault-tolerant **file storage** system
  - MapReduce is an distributed **computational framework**
  - NoSQL database is a large-scale distributed **database system** that stores unstructured and semi-structured data in efficient ways

- 大資料（Big Data）指的是尋找新的、更好的方式來管理資料庫管理系統（DBMS）無法處理的大量資料的運動。  
- 大資料的特徵（三個V）：  
  - **數量（Volume）**  
  - **速度（Velocity）**  
  - **多樣性（Variety）**

- 最常用的大資料技術：  
  - **Hadoop**：一個生態系統，提供一組軟體來操作大資料。  
  - **Hadoop 分布式檔案系統（HDFS）**：一個容錯的檔案儲存系統。  
  - **MapReduce**：一個分布式計算框架。  
  - **NoSQL資料庫**：一種大規模分布式資料庫系統，以高效方式儲存非結構化和半結構化資料。

# NoSQL Databases
- Schemaless
- Horizontal scalability
- Distributed data store
- Lower cost
- Non-relational
- Handle large volume of data

# RDBMS (Relational DBMS) vs NoSQL
|RDBMS|NoSQL
|-----|-----
|Structured data with a rigid schema | Unstructured, Semi-structured data with a flexible schema
|Storage in rows and columns | Data are stored in Key/Value pairs database, Columnar database, Document database, Graph Database.
|Scale up (變強) |Scale out (變多)
|SQL server, Oracle, mySQL|MongoDB, HBase, Cassandra
|SQL language|Solution-specific method

# Degrees of Data Abstraction
- External, Conceptual, Internal and Physical levels

<img width="464" alt="image" src="https://github.com/user-attachments/assets/4d4b7cd5-6fde-4b49-9767-4f39cb5d6397" />


# External Model
- The end users’ view of the data environment
- Use **ER diagrams** to represent the external model
- The external views represent **subsets** of the database
  - Easy to scope and communicate specific data required to support targeted end users
  - Ensure **security** constraints in the database design

<img width="519" alt="image" src="https://github.com/user-attachments/assets/a484b8f4-0bb1-4314-8290-916cb33a154a" />


# Conceptual Model
- A **global view** of the entire database by the entire organization
- Use **ER diagrams** to represent the conceptual model
- Identify and high-level describe main data objects
- Independent of both software and hardware
- The term **conceptual design** refers to creating a conceptual data model by ER diagrams

<img width="394" alt="image" src="https://github.com/user-attachments/assets/4bd3bc6c-eb36-4048-ab1c-237b704a36f4" />


# Internal Model
- Use the database constructs of the chosen DBMS to match the conceptual model’s characteristics and constraints to build the internal model
- The term **logical design** refers to creating a logical data model by a set of SQL statements
- Software dependent and hardware independent

<img width="394" alt="image" src="https://github.com/user-attachments/assets/23251db9-079d-4e44-ae5d-052d25877e2f" />


# Physical Model
- Operates at the lowest level of abstraction, describing which physical storage device the data is saved and how to access the data
- The term **physical design** refers to define data storage organization, security control, performance measure
- Both software and hardware dependent

# Levels of Data Abstraction 
<img width="518" alt="image" src="https://github.com/user-attachments/assets/3a8d6f94-b019-4743-8dde-72d3dd6ec3e0" />


| 層級         | 抽象化程度 | 關注焦點                  | 獨立於           | 主要使用者       | 實際範例                     |
|--------------|------------|---------------------------|------------------|------------------|------------------------------|
| **外部層**<br>(External)    | 最高       | 終端使用者視角<br>(如報表、畫面) | 硬體與軟體       | 應用程式開發者   | 銷售報表、會員管理後台       |
| **概念層**<br>(Conceptual) | 高         | 全局資料結構<br>(ER 模型)      | 硬體與軟體       | 資料庫設計師     | 企業級 ER 圖                 |
| **內部層**<br>(Internal)   | 中         | 特定資料庫模型實作<br>(如 SQL Schema) | 硬體             | DBA              | MySQL 的 InnoDB 儲存引擎設定  |
| **實體層**<br>(Physical)   | 最低       | 硬體儲存細節<br>(磁碟、索引)    | 無（依賴硬體與軟體） | 系統工程師       | 硬碟分區、索引的 B+ Tree 結構 |


# Review Questions
1. **Why data models are important?**  
Data models are important because they serve as a communication tool between different stakeholders (end users, developers, managers) who view data differently. They provide a precise description of data's nature and environment, reducing misunderstandings and ensuring consistency in database design. A well-designed data model is essential for creating an efficient and scalable database system.

2. **What are the data model basic building blocks?**  
- **Entity**: A person, thing, or event about which data is collected (e.g., a table in a database).  
- **Attribute**: A characteristic or property of an entity (e.g., a column in a table).  
- **Relationship**: An association between entities (e.g., one-to-many, many-to-many, one-to-one).  
- **Constraint**: A restriction on data to ensure integrity (e.g., salary range, mandatory fields).  

3. **How have the major data models evolved?**  
Major data models have evolved from hierarchical (tree structure, 1960s) and network (graph structure, 1970s) models to relational (tables with SQL, 1980s–1990s), object-oriented (objects with inheritance, 1990s), and NoSQL (flexible schemas, 2000s–present). Modern trends include cloud-native databases, NewSQL, and AI-integrated systems.  

4. **Explain NoSQL characteristics.**  
- **Schemaless**: Flexible data structures (e.g., JSON, key-value pairs).  
- **Horizontally scalable**: Distributed across servers for high volume.  
- **Non-relational**: No fixed tables or joins.  
- **Optimized for big data**: Handle unstructured/semi-structured data efficiently.  
- **Types**: Key-value (Redis), document (MongoDB), columnar (Cassandra), graph (Neo4j).  

5. **What are the four levels of data abstraction?**
- **External Model**: End-user views (subsets of data, represented as ER diagrams).  
- **Conceptual Model**: Global organizational view (ER diagrams, hardware/software independent).  
- **Internal Model**: DBMS-specific implementation (SQL logical design).  
- **Physical Model**: Lowest level (storage details, hardware/software dependent).

# Homework #1
資料庫課程作業(A)
