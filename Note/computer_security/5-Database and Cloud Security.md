---
title: "Computer Security Principles and Practice"
permalink: /Computer-Security-Principles-and-Practice/5-Database-and-Cloud-Security/
layout: default
---
# 5-Database and Cloud Security

[https://www.youtube.com/watch?v=RZLsUL1zL4I](https://www.youtube.com/watch?v=RZLsUL1zL4I)

# 5.1 The Need for Database Security

*   Why does database security fall behind the increased reliance on databases?
    *   imbalance between the complexity of DBMS (Database Management Systems) and security techniques (DBMS複雜但不安全)
        *   DBMS: complex, many new features and services
    *   Sophisticated interaction protocol: SQL （SQL是複雜的協議）
        *   Much more complex than HTTP
    *   Mismatch between requirements and capabilities （需求與能力不匹配）
        *   Administrators: limited knowledge of security or limited understanding of DBMS
    *   Heterogeneous mixture of database, enterprise, and OS platforms （資料庫、企業和作業系統平台的異質混合）
        *   Database: Oracle, IBM, Microsoft, etc.
        *   Enterprise: Oracle E-Business Suite, Siebel, etc.
        *   OS: UNIX, Linux, Windows, etc.

# 5.2 Database Management Systems

## Database

*   Structured collection of data stored for use by one or more apps
*   Contains the relationships between data items and groups of data items (資料跟資料群組的關聯)
*   Can sometimes contain sensitive data that needs to be secured
*   Query language
    *   Provides a uniform interface to the database



> Database management system (DBMS)  
> • Suite of programs for constructing and maintaining the database  
> (用於建置和維護資料庫的程式套件)  
> • Offers ad hoc query facilities to multiple users and applications  
> (為多個使用者和應用程式提供臨時查詢功能)



## DBMS Architecture

*   DDL (Data Definition Language): defines the database logical structure and procedural properties
    *   a set of database description tables
*   DML (Data Manipulation Language): provides a powerful set of tools for app developers
    *   Query languages
*   Security requirements: beyond the capability of typical OS-based security Why?
    *   OS: typically control read and write access to entire files
    *   Database: ?



![](https://t3764800.p.clickup-attachments.com/t3764800/3ce3530e-51c8-4537-80c7-5ded663ee9de/Screenshot_20231125_143609_Adobe%20Acrobat.jpg)

# 5.3 Relational Databases

*   Constructed from tables of data
    *   Each column holds a particular type of data
    *   Each row contains a specific value of each column
    *   Ideally has one column where all values are unique, forming an identifier/key for that row
        *   Used as the primary key
*   Have multiple tables linked by identifiers
*   Use a query language to access data items meeting specified criteria



*   Using multiple tables related to one another by a designated key
    *   Phone Number serves as a primary key

![](https://t3764800.p.clickup-attachments.com/t3764800/158ade9b-0249-4290-b8ff-34b3d9c1c361/Screenshot_20231125_152251_Adobe%20Acrobat.jpg)

## Elements of a Relational Database System

⚫ Relation/table/file

⚫ Tuple/row/record

⚫ Attribute/column/field

| formal name | Common Name | Also Known as |
| ---| ---| --- |
| Relation | Table | File |
| Tuple | Row | Record |
| Attribute | Column | Field |



| primary key | • Uniquely identifies a row<br>• Consists of one or more column names |
| ---| --- |
| Foreign key | • Links one table to attributes in another |
| View/virtual table | Result of a query that returns selected rows and columns from one or more tables |

![](https://t3764800.p.clickup-attachments.com/t3764800/04fdceb7-35e3-4a21-bbf3-f7961d517c7f/Screenshot_20231125_153205_Adobe%20Acrobat.jpg)



![](https://t3764800.p.clickup-attachments.com/t3764800/7d0328f8-202d-473b-a013-1d301fec5446/Screenshot_20231125_153326_Adobe%20Acrobat.jpg)

## Structured Query Language (SQL)

*   Originally developed by IBM in the mid-1970s
*   Standardized language to define, manipulate, and query data in a relational database
*   Several similar versions of ANSI/ISO standard
*   All follow the same basic syntax and semantics



SQL statements can be used to:

*   Create tables
*   Insert and delete data in tables
*   Create views
*   Retrieve data with query statements

# 5.4 SQL Injection Attacks

*   One of the most prevalent and dangerous network-based security threats
    *   Imperva Web Application Attack Report, July 2013 \[IMPE13\]
        *   SQLi attacks ranked 1st or 2nd in total number of attack incidents, …
        *   Observed at a single Web site: 94,057 SQL injection attack requests in one day
    *   Open Web Application Security Project’s 2013 report \[OWAS13\]
        *   Top risk from ten most critical Web app security risks
    *   Veracode 2016 State of Software Security Report \[VERA16\]
        *   35% apps affected by SQLi attacks
        *   Account for 26% of all reported breaches
    *   Trustwave 2013 Global Security Report \[TRUS16\]
        *   One of the top two intrusion techniques
        *   Poor coding practices → SQLi attacks remain more than 15 years

SQLi

*   Designed to exploit the nature of Web app pages
*   Sends malicious SQL commands to the database server
*   Most common attack goal is bulk extraction（取得） of data
*   Depending on the environment, SQLi can also be exploited to
    *   Modify or delete data
    *   Execute arbitrary OS commands
    *   Launch DoS attacks

## A Typical SQLi Attack

*   Hacker injects an SQL command to a database: sending the command to the Web server
    *   Database server executes the malicious command and returns data
    *   Web app dynamically generates a page with the data



1. Hacker finds a vulnerability in a custom Web application and injects an SQL command to a database by sending the command to the Web server. The command is injected into traffic that will be accepted by the firewall.
2. The Web server receives the malicious code and sends it to the Web application server.
3. The Web application server receives the malicious code from the Web server and sends it to the database server.
4. The database server executes the malicious code on the database. The database returns data from credit cards table.
5. The Web application server dynamically generates a page with data including credit card details from the database.
6. The Web server sends the credit card details to the hacker.

![](https://t3764800.p.clickup-attachments.com/t3764800/86eeb0f1-5652-4af5-90a3-2014bc982658/Screenshot_20231127_212703_Adobe%20Acrobat.jpg)

## The Injection Technique

*   Typical SQLi attacks: prematurely terminating a text string and appending a new command
    *   Comment mark “--”: subsequent text is ignored at execution time
    *   e.g., consider a script that build an SQL query by combining predefined strings with text entered by a user

```sql
var Shipcity;
ShipCity = Request.form (“ShipCity”);
var sql = “select * from OrdersTable where
ShipCity = ‘” + ShipCity + “‘ ”;

normal input
ShipCity = Redmond;
SELECT * FROM OrdersTable WHERE ShipCity = ‘Redmond’
===============================================================
malicious input
ShipCity = Boston’; DROP table OrdersTable--;
//註解掉原語法的「＇」
SELECT * FROM OrdersTable WHERE ShipCity = ‘Redmond’; DROP table OrdersTable--


```



## SQLi Attack Avenues and Types

*   User input
    *   Injects SQL commands by providing suitably crafted user input
*   Physical user input
    *   Attacks outside the realm of Web requests
    *   e.g., conventional barcodes and RFID tags
*   Server variables(e.g., HTTP headers and network protocol headers)
    *   If these variables are logged to a database without sanitization, this could create an SQL injection vulnerability
    *   attackers can forge the values that are placed in HTTP and network headers, they can exploit this vulnerability by placing data directly into the headers
*   Second-order injection
    *   incomplete prevention mechanisms against SQL injection attacks
    *   第一步，攻擊者將惡意 SQL 語句隱藏在應用程式允許輸入的數據中，例如會員帳號、商品名稱等字段中。當這些數據被存儲到資料庫中時，惡意 SQL 語句也會被保存下來。
    *   第二步，攻擊者通過另一個操作，例如修改個人資料或購買商品，觸發應用程式從資料庫中提取數據。當應用程式提取這些數據時，會將存儲在資料庫中的惡意 SQL 語句作為查詢條件，從而觸發 SQL 注入攻擊。
*   Cookies
    *   restore the client’s state information
    *   alter cookies such that when the application server builds an SQL query based on the cookie’s content, the structure and function of the query is modified

### SQLi Example I: from User Input

*   Consider a general verification SQL command

```sql
strSQL = “SELECT * FROM users WHERE (name = ‘” + username + “’) and (pw = ‘” + password + “’);

username: 1’ OR ‘1’=‘1
password: 1’ OR ‘1’=‘1
```

*   Target: “SELECT \* FROM users;”
*   Try it online: [https://www.w3schools.com/sql/trysql.asp?filename=trysql\_comment\_single\_2](https://www.w3schools.com/sql/trysql.asp?filename=trysql_comment_single_2)



### SQLi Example II: from Server Variables

*   Web apps use the variables in a variety of ways, such as logging usage statistics
*   An SQL injection vulnerability: they are logged to a database without sanitization(未經衛生處理而登入db)
    *   Attackers can forge the values that are placed in HTTP and network headers
*   Example: the header of a request HTTP
    *   How is it used for SQL?



```sql
“SELECT user.password FROM admins
WHERE
user=‘“.sanitize($_POST[‘user’].”’
AND
password=‘”.md5($_POST[‘password’]).”’
AND
ip_adr=‘”.ip_adr().”’”
```



![](https://t3764800.p.clickup-attachments.com/t3764800/a384f3df-a225-4454-9996-742a20630707/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/ec0301d9-7879-4aa8-a3b7-994f55d688f1/image.png)



*   Example: the header of a request HTTP
    *   How is it used for SQL?

```sql
“SELECT user.password FROM admins WHERE user=‘“.sanitize($_POST[‘user’].”’ AND password=‘”.md5($_POST[‘password’]).”’ AND ip_adr=‘”.ip_adr().”’”
```

HTTP\_X\_FORWARDED\_FOR is not properly sanitized.

```javascript
function ip_adr() {
  if (isset($_SERVER['HTTP_X_FORWARDED_FOR'])) {
    $ip_adr = $_SERVER['HTTP_X_FORWARDED_FOR']; }
  else { $ip_adr = $_SERVER["REMOTE_ADDR"]; }
  return $ip_adr;
}

HTTP_X_FORWARDED_FOR is not properly sanitized. （HTTP_X_FORWARDED_FOR沒有被過濾)
```

How to launch an SQLi attack with “HTTP\_X\_FORWARDED\_FOR”?

`X_FORWARDED_FOR :127.0.0.1' or 1=1#` ➝ 用這個condition都會是true



### SQLi Example III: from Second-order Injection

*   Relying on data already present in the system or database to trigger an SQLi attack
*   Consider a Web-based app which stores usernames alongside other session information
*   Given a session identifier such as a cookie
    *   Seek to retrieve the current username and use it in turn to receive SSN (social security number)

```sql
“SELECT username FROM sessiontable WHERE session=‘”$_POST[‘sessionid’].”’”
“SELECT ssn FROM users WHERE username=‘”$_POST[‘username’].”’”
```

_How to launch an SQLi attack with existing data?_

`username: XXX' OR username='JANE`

### Three Categories of SQLi Attacks

*   In-band attacks(帶內攻擊)
    *   利用跟系統正常服務的互動造成data leakage
    *   use the same communication channel for injecting SQL codes and retrieving results
    *   The retrieved data are presented directly in application web pages
    *   Tautology (同義反覆)
        *   This form of attack injects code in one or more conditional statements so that they always evaluate to be true(這種技巧涉及將代碼注入到一個或多個條件語句中，使其總是為真。這允許攻擊者的代碼繞過預期的邏輯並在不考慮用戶輸入的情況下執行)
        ```sql
        WHERE (1=1) -- 因為同義反覆，之後的合法代碼被忽略
        $query = “SELECT info FROM user WHERE name =
            ’$_GET[“name”]’ AND pwd = ‘$_GET[“pwd”]’”;
        SELECT info FROM users WHERE name = ‘ ‘ OR 1=1 -- AND pwpd = ‘ ‘
        ```
    *   End-of-line comment(**行尾註釋**)
        *   After injecting code into a particular field, legitimate code that follows are nullified through usage of end of line comments(這種技巧涉及將惡意代碼注入特定字段，然後使用行尾註釋使任何後續的合法代碼失效)
        ```sql
        username = 'admin' -- 後面的合法代碼被註釋掉
        ```
    *   Piggybacked queries(**附加查詢**)
        *   The attacker adds additional queries beyond the intended query, piggy-backing the attack on top of a legitimate request(在合法查詢的末尾添加額外的查詢。這允許攻擊者使用單個請求執行多個查詢，有可能擷取敏感信息或操縱數據)
        ```sql
        SELECT * FROM users; -- 攻擊者的查詢附加在合法的查詢上
        ```
*   Out-of-band attacks(帶外攻擊)
    *   經由簡訊或email
    *   use a different channel
    *   Data are retrieved using a different channel, e.g., email instead of web pages
    *   Used when there are limitations on information retrieval
        *   But, outbound connectivity from the data server is lax
*   Inferential attacks（推理攻擊）
    *   不斷重試
    *   No actual transfer of data, but reconstructing the information by sending particular request and observing results(它不涉及實際的數據傳輸，而是通過發送特定請求並觀察結果來重構信息)
    *   Reconstruct the information by sending particular requests and observing the resulting behavior of the Website/database server
        *   Illegal/logically incorrect queries (**非法/邏輯錯誤的查詢**)
            *   Default error page is overly descriptive (**過於詳盡的錯誤頁面**)
            *   Collect important information about the type and structure of the backend database of a Web application (**收集關於後端數據庫的類型和結構的重要信息**)
            *   Considered as a preliminary, information-gathering step for other attacks (通過收集的信息，為下一次攻擊做鋪墊。)
        *   Blind SQL injection
            *   都是透過觀察應用程序的行為來推測數據，需要透過一連串的「是/否」問題來逐步拼湊出答案
            *   Like asking true/false questions
            *   Infers the data present in a database system, even when the system is sufficiently secure to not display any erroneous information back to the attacker

## SQLi Countermeasures

### **defensive coding**

**Manual coding practices****:**

*       *   **Input validation****:** Check user input for expected format (e.g., numeric input should only contain digits) to prevent errors that attackers can exploit.
    *   **Pattern matching****:** Identify and reject abnormal input patterns that might indicate an attack.

> Manual defensive coding practices
>
> Parameterized query insertion
>
> SQL DOM -codegen

```java
using (SqlConnection conn = new Sq1Connection(NorthwindConnectionstring))
{
  string query = "SELECT * FROM Products WHERE ProductID = @Id";
  SqlCommand cmd = new Sq1Command(query, conn);
  cmd.Parameters.AddwithValue("@Id", Request.Querystring["Id"]);
  conn.Open();
  using (SqlDataReader rdr = cmd.ExecuteReader())
  {
    DetailsView1.DataSource - rdr;
    DetailsView1.DataBind();
  }
}



```

**Parameterized query insertion****:**

*       *   Separate user input from the query structure. This prevents attackers from modifying the query and injecting malicious code.
    *   Use type-checking APIs to ensure proper data handling and validation.

**SQL DOM****:**

*       *   SQL DOM is a set of classes that enables automated data type validation and escaping \[MCCL05\].
    *   Encapsulate database queries for safe and reliable access.
    *   Offers a type-checked API to enforce input filtering and rigorous type checking.

### Detection

**Signature-based****:**

*       *   Matches specific attack patterns.
    *   Requires constant updates and may not work against new attack variants.

**Anomaly-based****:**

*       *   Learns normal user behavior and detects deviations.
    *   Training phase needed to establish baseline of normal behavior.

**Code analysis****:**

*       *   Uses test suites to simulate various SQLi attacks and assess system response.
    *   Can be comprehensive but requires development and maintenance of the test suite.

### Run-time prevention

• Check queries at runtime to see if they conform to a model of expected queries

# 5.5 Database Access Control

*   Assumption: users have been authenticated
    *   They have access to the entire database or just portions of it
*   Commercial and open-source DBMSs: DAC or RBAC
*   Typically support a range of administrative policies
    *   Centralized administration
        *   Small number of privileged users may grant and revoke access rights
    *   Ownership-based administration
        *   A table’s creator may grant and revoke access rights to the table
    *   Decentralized administration
        *   A table’s owner may grant and revoke authorization rights to other users
        *   Other users are allowed to grant and revoke access rights to the table

## SQL-Based Access Definition

*   Two commands for managing access rights:
    ```dpr
    GRANT             { privileges | role }
    [ON               table]
    TO                { user | role | PUBLIC }
    [IDENTIFIED BY    password]
    [WITH             GRANT  OPTION]
    > GRANT SELECT ON ANY TABLE TO Bob
    > GRANT SELECT ON my_table TO PUBLIC
      -- 任何人都可以查詢 my_table 表格中的數據
    REVOKE             { privileges | role }
    [ON                table]
    FROM               { user | role | PUBLIC }
    > REVOKE SELECT ON ANY TABLE FROM Bob
    ```
*   `TO` clause : specifies the user or role to which the rights are granted
*   `PUBLIC` value : indicates any user has the specified access rights (任何人都擁有指定的存取權限)
*   `IDENTIFIED BY` clause : specifies a **_password_** that must be used to revoke the access rights of this GRANT command
*   `GRANT OPTION` : indicates that the grantee can grant this access right to other users, with or without the grant option (grantee是否可以將這些權限進一步授予其他使用者)
    *   **`WITH GRANT OPTION`****：** 如果使用 `WITH GRANT OPTION`，受授人就可以將授予的權限分發給其他使用者，就像他們自己擁有這些權限一樣。他們甚至可以選擇是否將 `GRANT OPTION` 包含在他們的子授予中，這就形成了權限的層級傳遞。
    *   **`WITHOUT GRANT OPTION`** **(默認)：** 如果沒有使用 `WITH GRANT OPTION`，受授人就只能自己使用這些權限，不能將它們分發給其他人。



*   Typical access rights are:
    *   SELECT, INSERT, UPDATE, DELETE, REFERENCES

## Cascading Authorizations

*   Grant/Revoke options: enable/disable an access right to cascade through a number of users
*   Revoke convention
    *   When user A revokes an access right, any cascaded access right is also revoked
    *   Unless that access right would exist even if the original grant from A had never occurred
    *   假設 Bob 撤回 David 的權限。David 仍然擁有存取權限，因為它是在 t = 50 時由 Chris 授予的。然而，David 在從 Bob 接收權限（包括授權選項）之後，又將其授予了 Ellen。大多數實施方式規定，在這種情况下，當 Bob 撤回 David 的存取權限时，Ellen 和 Jim 的存取權限也會被撤回。由於 David 在從 Chris 獲得包含授權選項的存取權限後才將權限授予 Frank，因此 Frank 的存取權限仍然保留。

![](https://t3764800.p.clickup-attachments.com/t3764800/e67da8fd-5f60-452f-a797-423816f42b35/Screen%20Shot%202023-12-03%20at%2012.09.43%20PM.png)

## Role-Based Access Control

*   RBAC eases administrative burden and improves security
*   A database RBAC needs to provide the following capabilities
    *   Create and delete roles
    *   Define permissions for a role
    *   Assign and cancel assignment of users to roles
*   In a discretionary access control environment, Categories of database users
    *   **Application owner:** An end user who owns database objects as part of an application
    *   **End user other than application owner:** An end user who operates on database objects via a particular application but does not own any of the database objects
    *   **Administrator:** User who has administrative responsibility for part or all of the database.

### Microsoft SQL Server

*   three types of roles:
    1. fixed roles
        1. Server roles : fixed server roles defined at the server level and exist independently of any user database
        2. database roles :**Fixed database roles** operate at the level of an individual database
            1. designed to assist a DBA with delegating administrative responsibilities.
    2. user-defined roles : can then be assigned access rights to portions of the database
        1. two types of user-defined roles: Standard and application
            1. standard role: an authorized user can assign other users to the role
            2. application role : associated with an application rather than with a group of users and requires a password
                1. e.g. you can use an application role with its own password to allow the particular user to obtain and modify any data only during specific hours

![](https://t3764800.p.clickup-attachments.com/t3764800/f338b01c-2f88-4012-a7d9-6babe257aa82/Screen%20Shot%202023-12-03%20at%2012.23.43%20PM.png)

# 5.6 Inference

*   The process of performing authorized queries and deducing unauthorized information from the legitimate responses 從收到的合法回應中推斷出未經授權的資訊的過程。當多個資料項的組合比單一資料項更敏感時，或當資料項的組合可用於推斷較高敏感度的資料時，就會出現推斷問題
    *   Combination of a number of data items: more sensitive than individual items
*   **Metadata**: knowledge about correlations(關聯) or dependencies among data items
*   **Inference** **channel**: information transfer path by which unauthorized data is obtained



Figure 5.8a shows an Inventory table with four columns.

Figure 5.8b shows two views, defined in SQL as follows:

Figure 5.8c. This violates the access control policy that the relationship of attributes Item and Cost must not be disclosed.

```sql
CREATE view V1 AS
SELECT Availability, Cost
FROM Inventory
WHERE Department = “hardware”
```



```sql
CREATE view V2 AS
SELECT Item, Department
FROM Inventory
WHERE Department = “hardware”
```

![](https://t3764800.p.clickup-attachments.com/t3764800/eaf0d9bb-76fe-451e-aec4-780027e58379/Screen%20Shot%202023-12-03%20at%2012.33.15%20PM.png)

*   Users of the views are not authorized to access the relationship between Salary and Name
*   However, it can be referred by the combination of the views
    *   Knowledge of the table structure is needed



## Inference Detection: Two Approaches

*   Inference detection during database design
    *   Removes an inference channel by altering the database structure
        *   E.g., splitting a table into multiple tables or more fine-grained access control
    *   Availability reduction: unnecessarily stricter access controls
*   Inference detection at query time
    *   Eliminate an inference channel violation during a query or series of queries
*   For either of them, some inference detection algorithm is needed
    *   Difficult problem and ongoing research

### Example: Inference Problem and Solution

*   Consider a database containing personnel information, including names, addresses, and salaries of employees
    *   Clerk: name, address, and salary information
    *   Administrator: name, address, salary information, and association of names/salaries
*   Solution: construct three tables

```scss
Employees (Emp#, Name, Address)
Salaries (S#, Salary)
Emp-Salary (Emp#, S#)
```

*   ![](https://t3764800.p.clickup-attachments.com/t3764800/a771d1e2-fdd6-4e4a-a611-d6ea5d06e1d2/image.png)

**_What if a new attribute, employee start date, is needed? Where should it be added?_**

```scss
Employees (Emp#, Name, Address)
Salaries (S#, Salary, Start-Date)
Emp-Salary (Emp#, S#)
```



*   add the start-date column to the Employees table rather than to the Salaries table.

```bash
Employees (Emp#, Name, Address, Start-Date)
Salaries (S#, Salary)
Emp-Salary (Emp#, S#)
```

# 5.7 Database Encryption

*   Database is typically the most valuable information resource for any organization
    *   Protected by multiple layers of security
        *   Firewalls, authentication, general access control systems, DB access control systems, etc.
        *   Encryption becomes the last line of defense in database security
*   Can be applied to the entire database, at the record level (rows), the attribute level (columns), or level of the individual field (specific fields)
*   Disadvantages
    *   Inflexibility: difficult to perform record searching
    *   Key management: authorized users must have access to the decryption key for the data for which they have access
*   Four entities are involved:
    *   **Data owner** – organization that produces data to be made available for controlled release
    *   **User** – human entity that presents queries to the system
    *   **Client** – frontend that transforms user queries into queries on the encrypted data stored on the server
    *   **Server** – an organization that receives the encrypted data from a data owner and makes them available for distribution to clients



A user at the client can retrieve a record from the database with the following sequence:

1. The user issues an SQL query for fields from one or more records with a specific value of the primary key.
2. The query processor at the client encrypts the primary key, modifies the SQL query accordingly, and transmits the query to the server.
3. The server processes the query using the encrypted value of the primary key and returns the appropriate record or records.
4. The query processor decrypts the data and returns the results.



![](https://t3764800.p.clickup-attachments.com/t3764800/7a1606ef-a0c4-4bc3-a18b-231e9837fcfb/Screen%20Shot%202023-12-03%20at%204.25.10%20PM.png)

### Example for a Straightforward Approach

**For example, consider this query, which was introduced in Section 5.1, on the**

database of Figure 5.4a:

```sql
 SELECT Ename, Eid, Ephone
        FROM Employee
        WHERE Did = 15
```

*   Assume the encryption key 𝑘 is used
*   the encrypted value of the Did 15 is 𝐸(𝑘, 15) = 1000110111001110
*   The query processing at the client could transform the query to

```sql
    SELECT Ename, Eid, Ephone
        FROM Employee
        WHERE Did = 1000110111001110
```

![](https://t3764800.p.clickup-attachments.com/t3764800/ccbab78c-adcf-4742-b885-ce87ce6ea51e/Screen%20Shot%202023-12-03%20at%204.34.12%20PM.png)

*   Pro
    *   straightforward but
*   Cons
    *   lacks flexibility
        *   The user wants to retrieve data based on a specific attribute value (salary < $70K)
        *   The data is encrypted, making direct comparison impossible.
        *   The encryption scrambles the original order of the values, so even if decryption were possible, sorting wouldn't be reliable

### More Flexible Approach

*   Each record (row) of a table is encrypted as a block
    *   R𝑖: a continuous block 𝐵𝑖 = (𝑥𝑖1 || 𝑥𝑖2 ||⋯||𝑥𝑖𝑀)
    *   All of the attribute values: concatenated together to form a single binary block
    *   Data retrieval: attribute indexes are associated with each table



*   Suppose employee ID (_eid_) values lie in the range \[1, 1000\]
    *   divide these values into five partitions: \[1, 200\], \[201, 400\], \[401, 600\], \[601, 800\], and \[801, 1000\]
*   assign index values 1, 2, 3, 4, and 5, respectively
*   For a text field, we can derive an index from the first letter of the attribute value.
*   Similar partitioning schemes can be used for each of the attributes



*   Table 5.3b shows the resulting table. The values in the first column represent the encrypted values for each row. The actual values depend on the encryption algorithm and the encryption key.

![](https://t3764800.p.clickup-attachments.com/t3764800/93afd833-9208-4b55-abb2-8186b7cd7455/Screen%20Shot%202023-12-03%20at%204.57.03%20PM.png)

*   with _eid <_ 300. The query processor requests all records with _I_(_eid_) = 2. These are returned by the server.
    *   The query processor decrypts all rows returned, discards those that do not match the original query, and returns the requested unencrypted data to the user.
*   Cons
    *   provide a certain amount of information to an attacker, namely a rough relative ordering of rows by a given attribute

# Cloud Security

*   NIST SP-800-145 defines cloud computing as:
*   “A model for enabling ubiquitous(無所不再), convenient, on- demand network access to a shared pool of configurable computing resources (e.g., networks, servers, storage, applications, and services) that can be rapidly provisioned and released with minimal management effort or service provider interaction.“

## Cloud Computing Elements

![](https://t3764800.p.clickup-attachments.com/t3764800/520bb582-3c53-45e2-af7a-a6f956d269aa/Screen%20Shot%202023-12-03%20at%205.14.25%20PM.png)

## Cloud Service Models

*   Software as a service (SaaS)
    *   e.g., using software installed on clouds via web browsers
*   Platform as a service (PaaS)
    *   e.g., enabling customers to developing their own applications running on operating systems provided by clouds
*   Infrastructure as a service (IaaS)
    *   e.g., enabling customers to install their own operating systems (Amazon EC2 and Windows Azure)
    *   Clouds provide hardware (virtualization of hardware)

![](https://t3764800.p.clickup-attachments.com/t3764800/f5aebf24-eae0-48d4-a7b2-7a7a9d11a707/Screen%20Shot%202023-12-03%20at%205.16.35%20PM.png)![](https://t3764800.p.clickup-attachments.com/t3764800/b6f9ffa9-4e2a-473d-8cee-acae2dc61272/Screen%20Shot%202023-12-03%20at%205.16.45%20PM.png)![](https://t3764800.p.clickup-attachments.com/t3764800/668f1dd6-74ed-4362-a17a-746b235c0c44/Screen%20Shot%202023-12-03%20at%205.17.23%20PM.png)



## Containers vs. Virtual Machines

![](https://t3764800.p.clickup-attachments.com/t3764800/d919d1a8-30f0-47f9-a01a-9518f7ae937e/Screen%20Shot%202023-12-03%20at%205.18.05%20PM.png)

Here's a breakdown of the key differences between containers and virtual machines:

**Virtualization level****:**

*   **Containers:** Share the host operating system kernel with other containers. This makes them lightweight and fast to start, but also less isolated from each other.
*   **VMs:** Each VM has its own guest operating system (OS) on top of the host OS, creating a more isolated environment. This isolation comes at the cost of increased overhead and slower startup times.

**Resource allocation****:**

*   **Containers:** Allocate resources dynamically based on their needs, making them efficient and scalable.
*   **VMs:** Typically have pre-allocated resources, which can lead to inefficient resource utilization if not configured optimally.

**Application packaging:**

*   **Containers:** Package an application with its dependencies and libraries into a single unit called an image. This makes them portable and easy to deploy.
*   **VMs:** Package an entire OS with the application and its dependencies, making them more complex to set up and manage.

**Use cases:**

*   **Containers:** Ideal for microservices architectures, cloud-native deployments, and running multiple isolated applications on a single host.
*   **VMs:** Better suited for legacy applications, resource-intensive workloads, and situations requiring strong isolation and security.

**Here's a table summarizing the key differences:**

| Feature | Containers | Virtual Machines |
| ---| ---| --- |
| Virtualization level | Shared kernel | Guest OS |
| Isolation | Lower | High |
| Resource allocation | Dynamic | Pre-allocated |
| Packaging | Image | Entire OS + application |
| Startup time | Fast | Slow |
| Scalability | High | Moderate |
| Use cases | Microservices, cloud-native, multi-tenant | Legacy apps, resource-intensive, high isolation |

Ultimately, the choice between containers and VMs depends on your specific needs and priorities. Consider factors like isolation requirements, resource utilization, and application compatibility when making your decision.

## Typical Cloud Computing Context

![](https://t3764800.p.clickup-attachments.com/t3764800/20e754c4-82a3-43a7-9bbe-216e68e79f40/Screen%20Shot%202023-12-03%20at%205.22.25%20PM.png)

## NIST Cloud Computing Reference Architecture

![](https://t3764800.p.clickup-attachments.com/t3764800/3773e37e-46d1-4f81-bfa6-cf3aba62e610/Screen%20Shot%202023-12-03%20at%205.23.17%20PM.png)

## Cloud Security Risks and Countermeasures

*   Abuse and nefarious(惡毒的) use of cloud computing
    *   **Causes**: easy to register; free limited trial periods
    *   **Countermeasures**: (1) stricter initial registration process; (2) monitoring fraud traffic
*   Insecure interfaces and APIs
    *   **Causes**: a set of interfaces and APIs are exposed to customers
    *   **Countermeasures**: (1) analyzing security model; (2) ensuring strong authentication and access control; (3) understanding the dependency chain
*   Malicious insiders
    *   **Causes**: certain necessary roles are extremely high-risk
    *   **Countermeasures**: (1) strengthen management; (2) transparency; (3) security breach notification
*   Shared technology issues
    *   **Causes**: sharing infrastructure in IaaS; the underlying components were not designed to offer strong isolation properties for a multi-tenant architecture
    *   Typical solution: using isolated VM for clients, but still vulnerable
    *   **Countermeasures**: (1) best security practices for installation/configuration; (2) monitoring, scanning, and auditing; (3) strong authentication and access control
*   Data loss or leakage
    *   **Countermeasures**: (1) Strong API access control; (2) data integrity protection; (3) data protection analysis; (4) strengthen management
*   Account or service hijacking
    *   **Causes**: stolen credentials
    *   **Countermeasures**: (1) better management: prohibit the sharing of account credentials; (2) strong two-factor authentication; (3) monitoring
*   Unknown risk profile
*   **Countermeasures**: (1) disclosure of applicable logs and data; (2) partial/full disclosure of infrastructure details; (3) monitoring and alerting on necessary information

## Cloud Security as a Service (SecaaS)

*   Offloading of security functions
    *   Authentication, anti-virus, antimalware/spyware, intrusion detection, security event management, etc.
*   Definition by Cloud Security Alliance (CSA)
    *   the provision of security apps and services via the cloud either to cloud-based infrastructure and software or from the cloud to the customers’ systems

![](https://t3764800.p.clickup-attachments.com/t3764800/077ff64f-f54f-421d-818e-631d0dfa404f/Screen%20Shot%202023-12-03%20at%205.28.14%20PM.png)

## Elements of Cloud Security as a Service

![](https://t3764800.p.clickup-attachments.com/t3764800/a0db3761-bb93-43af-98e4-e1c29a27edeb/Screen%20Shot%202023-12-03%20at%205.30.28%20PM.png)

# 5.8 Data Center Security

> teacher doesn't teach this section

## Data Center Elements

> teacher doesn't teach this section

## Data Center Security Considerations

> teacher doesn't teach this section

## TIA-492

> teacher doesn't teach this section

# 5.9 Key Terms, Review Questions, and Problems

1. **5.1**  Define the terms _database_, _database management system_, and _query language_.
2. **5.2**  What is a relational database and what are its principal ingredients?
3. **5.3**  What is an SQL injection attack?
4. **5.4**  What are the implications of an SQL injection attack?
5. **5.5**  List the categories for grouping different types of SQLi attacks.
6. **5.6**  Why is RBAC considered fit for database access control?
7. **5.7**  State the different levels at which encryption can be applied to a database.
8. **5.8**  List and briefly define four data center availability tiers.
