
# Chapter 1: Database Systems
- Organizations use data to keep track of their day-to-day operations. Such data is used to generate information, which in turn is the basis for good decisions. 
- Data is likely to be managed most efficiently when it is stored in a database.

# Why Database
- Databases evolved from the need to manage **large amounts** of data in an **organized and efficient** manner
- Databases is everywhere

<img width="766" alt="image" src="https://github.com/user-attachments/assets/ba9f6941-3004-4b2b-bc35-5f85d3681a13" />

# DIKW Pyramid
- **Data** consists of **raw facts**
- **Information** is about adding context to reveal the **meaning of data**
- **Knowledge** is about **how to use** the information
- **Wisdom** is about **when to take** action
![bg right:50% w:600 DIKW Pyramid](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*s5EFf2e8t0wqCAnSglUt_Q.png)

# Data versus Information
- Information is the result of processing raw data to reveal the meaning of data
- **Data management** is a discipline that focuses on the proper generation, storage, and retrieval of data

<img width="571" alt="image" src="https://github.com/user-attachments/assets/9198ac43-f66b-458e-b9f7-a2e111606ddb" />

# Introducing the Database
- A **database** is a collection of related data.
  - represent a **mini-world** to reflect some aspect of the real world
  - **logically coherent** collection of data with some inherent meaning
  - is designed, built, and populated with data for **a specific purpose**
- A **database management system (DBMS)** is a collection of programs that manages the database **structure** and **controls access** to the data stored in the database. Here, the database refers to a **shared, integrated** computer structure.
- Examples of DBMS: MySQL, Microsoft SQL Server, Oracle Database, MongoDB, Cassandra, Neo4j, ...

# Role and Advantages of DBMS
- DBMS presents the end user with a single, integrated view of the data in the database
- DBMS advantages:
  - Improved data sharing
  - Improved data security
  - Better data integration
  - Minimized data inconsistency
  - Improved data access

<img width="567" alt="image" src="https://github.com/user-attachments/assets/68965ea5-3520-405a-ab3b-5ff150868019" />

# Types of DBMS
- by # of users: single-user, multiple-user 
- by location: centralized, distributed, cloud
- by time sensitive: online transaction processing (OLTP), online analytical processing (OLAP)
- by data characteristics: SQL store structured data, NoSQL store unstructured and semi-structured data

# Why Should We Learn Database Design
- **Database design** refers to the activities that focus on the design of the database structure that will be used to store and manage end-user data
- Poorly designed databases can lead to slow performance, data integrity issues, security vulnerabilities, and challenges in scaling applications.

<img width="562" alt="image" src="https://github.com/user-attachments/assets/b6aced62-b47e-4954-8775-9b698f9e3b4c" />

# Database System Design Process
- <span class="brown-text">Requirements & Analysis</span>
 <span class="small-text">Discover users requirements, analyze what data should be maintained</span>
- <span class="brown-text">Database design</span>
  - <span class="small-text">Conceptual model</span>
  - <span class="small-text">Choice of a DBMS</span>
  - <span class="small-text">Logical model</span>
  - <span class="small-text">Physical model</span>
- <span class="brown-text">System design</span>: <span class="small-text">design system functionality and user interface</span>
- <span class="brown-text">Implementation</span>: <span class="small-text">realize physical model on running environment and optimize performance</span>

![bg right:30% w:400](https://techforumugm.files.wordpress.com/2020/03/dd01.png?w=816&h=352&crop=1)

# Database Design Process

<img width="516" alt="image" src="https://github.com/user-attachments/assets/b86fed6b-97c7-4d97-b022-0345e3fb0878" />

# A Good Database Design Following Database Design Process

<img width="529" alt="image" src="https://github.com/user-attachments/assets/985ca65e-faff-4af1-b260-a40aa4c1c044" />

# Database System Environment
Collect, store, manage, and use of data within a database environment, including:
- <span class='small-text'>Hardware</span>
- <span class='small-text'>Software</span>
- <span class='small-text'>People</span>
- <span class='small-text'>Procedures</span>
- <span class='small-text'>Data</span>

<img width="500" alt="image" src="https://github.com/user-attachments/assets/3f10914c-ff75-49f8-89d1-e8f4cb5e0e48" />

# DBMS Functions
- Data dictionary management to store definitions of data elements and their relationships
- Data storage management
- Security management
- Transaction management and concurrent control
- Backup and recovery management
- Data integrity management
- SQL languages (structured query language)
- Database communication API (application programming interfaces)
  
<img width="524" alt="image" src="https://github.com/user-attachments/assets/f984de03-c2da-4fa1-a766-0107519c20ea" />

# Disadvantages of DBMS
- Increased costs
- Management complexity
- Maintaining currency (operation expertise and man power)
- Vendor dependency (vendor lock-in)
- Frequent upgrade/replacement cycles

# Database Professional Career

Job Title|Description|Sample Skills Required
---------|-----------|----------------------
Developer | Develop application | Programming, SQL
DBA| Design, manage DBMS | DBMS fundamentals, SQL
Database Designer | Design data models | Domain knowledge, data modeling, DBMS fundamentals, SQL
Data Security Officer | Enforce data security rules| DBMS fundamentals, data security
Data Analyst / Data Scientist| Analyze varied data to generate insights and prediction| Data analysis, statistics, SQL / programming, ML / AI, data visualization

# When Not to Use a DBMS
- When costs can not be justified: H/W, S/W, operations  
- When a DBMS may be unnecessary: simple applications, limited users
- When a DBMS may be infeasible: embedded systems
- When no DBMS may suffice: real-time requests, complexity of data, special operation

# Review Questions
- What is a database 
- What is a DBMS
- Which database professional career you are interested in?
