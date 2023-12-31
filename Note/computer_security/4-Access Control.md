---
title: "Computer Security Principles and Practice"
permalink: /Computer-Security-Principles-and-Practice/4-Access-Control/
layout: default
---

# 4-Access Control

[https://www.youtube.com/watch?v=t0m6aCQPTMs&t=5s](https://www.youtube.com/watch?v=t0m6aCQPTMs&t=5s)[https://www.youtube.com/watch?v=4-tKLcGGdBY&t=12s](https://www.youtube.com/watch?v=4-tKLcGGdBY&t=12s)

#   

# **4.1  Access Control**

Definition of Computer Security (RFC 4949)

*   Measures that implement and assure security services in a computer system, particularly those that assure access control service.

_Access control: the central element of computer security_

*   Prevent unauthorized users from gaining access to resources
*   Prevent legitimate users from accessing resources in an unauthorized manner
*   Enable legitimate users to access resources in an authorized manner

> 1\. NISTIR 7298 (Glossary of Key Information Security Terms, May 2013), defines  
> access control as the process of granting or denying specific requests to: (1)  
> obtain and use information and related information processing services; and  
> (2) enter specific physical facilities.  
> 2\. RFC 4949, Internet Security Glossary, defines access control as a process by  
> which use of system resources is regulated according to a security policy and  
> is permitted only by authorized entities (users, programs, processes, or other  
> systems) according to that policy



## Access Control Principle

*   Access control implements a security policy that specifies who or what (e.g., in the case of a process) may have access to each specific system resource, and the type of access that is permitted in each instance.

### Access Control Context

*   Authentication (驗證)
    *   Verifying that user/system
    *   credentials are valid （憑證是否合法）
*   Authorization （授權）
    *   Granting a right or permission to a system entity to access a system resource
*   Audit（審查）
    *   An independent examination of system records and activities（系統活動和記錄的獨立評估）
        *   Test adequacy(足夠) of system controls
        *   Ensure compliance with established policy and operational procedures
        *   Detect breaches(違反) in security
        *   Recommend any indicated(暗示、指示) changes in control, policy and procedures

![](https://t3764800.p.clickup-attachments.com/t3764800/3d4e25ec-67f8-48b4-ad36-31183584aa6d/image.png)

*   access control mechanism mediates between a user (or a process executing on behalf of a user) and system resources
*   authentication function determines whether the user is permitted to access the system
*   access control function determines if the specific requested access by this user is permitted
*   security administrator maintains an authorization database that specifies what type of access to which resources is allowed for this user.
*   access control function consults(ask) this database to determine whether to grant access.
*   auditing function monitors and keeps a record of user accesses to system resources.

## Access Control Policies

*   [Discretionary access control](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4582?block=block-46646f5c-2fb7-4584-94b0-72dfd7898769) (DAC, 自主存取控制)
    *   Based on the requestor’s identity (基於請求者的身份)
    *   Access on rules stating(訪問規則規定) what requestors are (or are not) allowed to do
    *   Why discretionary?
        *   An entity might have access rights to enable another entity to access some resource(一個實體可能擁有訪問權限，允許另一個實體訪問某些資源)
*   Mandatory access control (MAC, 強制存取控制) ➝ CH24
    *   Based on security clearances of system entities(基於系統實體的安全許可)
    *   Access on security labels of resources(訪問資源的安全標籤)
    *   Why mandatory?
        *   An entity that has clearance to access a resource may not enable another entity to access that resource(具有訪問資源權限的實體可能無法允許另一個實體訪問該資源)
*   [Role-based access control](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4582?block=block-d48440f9-4f3b-49cb-ad70-1e563c7c64b1) (RBAC)
    *   Based on the users’ roles (基於用户的角色)
    *   Access on rules stating what accesses are allowed to given roles (訪問規則規定了給定角色允許哪些訪問)
    *   符合RBAC的模型包括：
        *   靜態角色和動態角色
        *   角色繼承
        *   權限委派
*   [Attribute-based access control](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4582?block=block-2f406adb-6934-491e-bdf9-d2b543181ed1) (ABAC)
    *   Based on the users’ attributes, the accessed resource, and current environmental conditions(基於用户的屬性、訪問的資源和當前環境條件)

ABAC模型的主要組成部分是：

*       *   資源：受保護的數據或服務
    *   主體：嘗試訪問資源的實體
    *   環境：訪問請求的環境條件
    *   屬性：資源、主體和環境的屬性
    *   策略：定義訪問控制規則的策略
    *   策略執行點（PEP）：執行策略的組件
    *   策略信息點（PIP）：提供策略決策所需信息的組件



# **4.2  Subjects, Objects, and Access Rights**

![](https://t3764800.p.clickup-attachments.com/t3764800/763fb747-bc31-4057-bb56-3680d9aa876f/image.png)

basic elements of access control are: subject, object, and access right.

*   subject: an entity capable of accessing object
    *   three classes of subject:
        *   Owner: creator of resource,etc. file.
        *   Group: membership in the group is sufficient to exercise these access rights
        *   World: users who are able to access the system ( but not owner and group for this resource).
    *   object: A resource to which access is controlled
        *   records, blocks, pages, segments, files...
        *   The number and types of objects depends on the environment in which access control operates ➝tradeoff between security and complexity, processing burden, and ease of use.(越多access control的object，越考慮相對的複雜度越高)
    *   Access Right: describes the way which a subject may access an object(描述一個subject可能存取object的方法)
        *   Read: User may view information in a system resource (e.g., a file, selected records in a file, selected fields within a record, or some combination). Read access includes the ability to copy or print.
        *   Write: User may add, modify, or delete data in system resource (e.g., files, records, programs). Write access includes read access.
        *   Execute: User may execute specified programs.
        *   Delete: User may delete certain system resources, such as files or records.
        *   Create: User may create new files, records, or fields.
        *   Search: User may list the files in a directory or otherwise search the directory.

# **4.3  Discretionary Access Control (DAC)**

*   discretionary access control : enable another entity to access some resource
*   A general approach to DAC: access matrix
    *   Use case : operating system, database management system
    *   Subjects vs. Objects
    *   Each entry: [access right](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4582?block=block-bef2dcc4-f62c-4cb7-a1d7-bda0a86e146d) (一個實體可能擁有訪問權限，允許另一個實體訪問某些資源))
    *   An access control matrix(矩陣) is a table that specifies the access rights of each subject (user or process) for each object (resource).
    *   Subjects (user) are listed on one dimension of the matrix
    *   objects (file) are listed on the other dimension.
    *   matrix indicates the access rights of the corresponding subject for the corresponding object.
    *   _access matrix is usually sparse and is implemented by decomposition in one of two ways. （_**訪問矩陣通常是稀疏的，並通過以下兩種方式之一進行分解來實現。**_）_
        *   [**access control lists**](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4582?block=block-10119324-4e9b-41f9-b00b-0ff0d68fb831) [(ACLs)](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4582?block=block-10119324-4e9b-41f9-b00b-0ff0d68fb831)
        *   [**capability tickets**](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4582?block=block-24755299-8a52-4275-821e-3bec1e9eee38)

![](https://t3764800.p.clickup-attachments.com/t3764800/72764f51-d27f-4fa3-a673-4c6bd70cdf72/image.png)

*   Access control lists (ACL): decomposed by columns (objects) （**按列（對象）分解**）
    *   For each object, an ACL lists users and their permitted access rights （對於每個對象，ACL 列出用戶及其允許的訪問權限）
    *   Default set of rights（默認權限集）: users that are not explicitly listed （未明確列出的用戶）
    *   Convenient: determining which subjects have which access rights to a particular resource （方便確定哪些subjects對特定資源具有哪些訪問權限）
        *   each ACL provides the information for a given resource
        *   useful way to organize and store access control information
    *   Inconvenient: determining the access rights available to a specific user（**不方便**確定特定用戶可用的訪問權限）
    *   **_ACLs are organized by resource, not by user_**

![](https://t3764800.p.clickup-attachments.com/t3764800/2fb5da37-1b11-43ea-9038-aaa000ad95f5/image.png)

*   Capability tickets: decomposed by rows (subjects) (**按行（**subjects (user)**）分解**)
    *   A capability ticket specifies authorized objects and operations for a particular user(capability ticket指定特定用戶的授權 object(file) 和操作)
    *   Convenient/Inconvenient: opposite to ACLs
*   Have greater security problem than ACLs. Why? （比ACL嚴重安全性問題）
    *   Tickets may be dispersed（驅散） around the system
        *   Integrity of the ticket must be protected, guaranteed, and unforgeable（難忘的）
    *   Two solutions
        *   OS holds all tickets on behalf of users
        *   An unforgeable token in the capability
            *   large random password
            *   cryptographic message authentication code
*   **_easy to determine the set of access rights that a given user has, but more difficult to determine the list of users with specific access rights for a specific resource. (_**易於確定給定用戶擁有的訪問權限集，但更難確定具有特定訪問權限的特定資源的用戶列表。**_)_**

![](https://t3764800.p.clickup-attachments.com/t3764800/67b15547-eb43-44bc-8b7e-d113e00b7d71/Screen%20Shot%202023-11-09%20at%202.29.56%20PM.png)

Another Approach: Authorization Table \[SAND94\]

*   Not sparse and more convenient than either ACLs or capability lists （Authorization table**不像access matrix那樣稀疏，但也比 ACL 或 capability ticket更方便****）**
    *   **Sorting** **or accessing the table by** **subject is equivalent to a capability list**
    *   **Sorting** **or accessing the table by** **object is equivalent to an ACL** 
*   A relational database can easily implement an authorization table of this type (**關聯數據庫可以輕鬆實現此類授權表。**)
    *   **An authorization table contains one row for one access right of one subject to one resource** - Each row in an authorization table contains the following information:
        *   The subject that is granted the access right
        *   The object(resource) that the access right applies to
        *   The access right that is granted
*   Any drawback?

![](https://t3764800.p.clickup-attachments.com/t3764800/5d5994aa-d715-4f15-9a93-2c8a77dcde12/Screen%20Shot%202023-11-09%20at%202.47.12%20PM.png)

## An Access Control Model

define the protection state of a system to be the set of information, at a given point in time, that specifies the access rights for each subject with respect to each object.

**（定義系統的 Protection State 為在特定時間點指定每個主體對每個對象的訪問權限的信息集）**

Access Control Model 解決以下三個需求，提供DAC**系統的通用邏輯描述。**

*   Three requirements
    *   Representing the protection state（**保護狀態**）
    *   Enforcing access rights（**強制訪問權限**）
    *   Allowing subjects to alter the protection state in certain ways （**允許Subject 以某些方式更改保護狀態**）
*   Concepts
    *   As usual: a set of subjects, objects, and rules
    *   New: protection states
*   Protection states
    *   Processes: delete, stop (block), and wake up
    *   Devices: read/write, operation control, and block/unblock
    *   Memory locations or regions: read/write
    *   Subjects: grant or delete access rights of objects

### **Extended Access Control Matrix**

*   _A_\[_S_, _X_\] contains strings, called access attributes, that **specify the access rights of subject** **_S_** **to object** **_X_**.
*   _S_1 may read file _F_1, because ‘read’ appears in _A_\[_S_1, _F_1\].

![](https://t3764800.p.clickup-attachments.com/t3764800/f1f79adf-559c-4704-a5ea-f317326b3654/Screen%20Shot%202023-11-09%20at%203.22.45%20PM.png)

### **Access Control Function**

*   Every access by a subject to an object is mediated by the controller for that object (每個 Subject 對 Object 的訪問都由該 Object 的 Controller 進行仲裁)
    *   access matrix controller : controls updates to the matrix
*   Decisions are based on access matrix monitor
*   The module evaluates each request by a subject to access an object to determine if the access right exists. （**該module通過評估 Subject 訪問 object 的每個請求來確定訪問權限是否存在。**）
*   access attempt triggers the following steps:
    1. **A subject** **_S_****0 issues a request of type a for object** **_X_****. (**S0 針對 object "X" 發送 type "a" 的請求。**)**
    2. **The request causes the system(the operating system or an access control interface module of some sort) to generate a message of the form (****_S_****0, a,** **_X_****) to the controller for** **_X_****. (**生成形式為 (S0, a, X) 的消息到 X 的控制器。**)**
    3. **The controller interrogates the access matrix** **_A_** **to determine if a is in** **_A_****\[****_S_****0,** **_X_****\]. If so, the access is allowed; if not, the access is denied and a protection violation occurs. The violation should trigger a warning and appropriate action. (**控制器查詢訪問矩陣 A 以確定 a 是否存在於 A\[S0, X\] 中。如果是這樣，則允許訪問；如果不是，則拒絕訪問並發生保護違規。違規應觸發警告和適當的動作。)
*   model also includes a set of rules that govern modifications to the access matrix
    *   access rights ‘owner’ and ‘control’
    *   concept of a copy flag
    *   Eight rules
        *   **R1:** A subject can transfer an access right, with or without a copy flag, to another subject.
            *   _S_1 may place ‘read’ or ‘read\*’ in any matrix entry in the _F_1 column.
        *   **R2:** A subject can grant an access right to an object for any other subject, if it is the owner of the object.
            *   if _S_0 is designated as the owner of object _X_, then _S_0 can grant an access right to that object for any other subject
            *   _S_0 can add any access right to _A_\[_S_, _X_\] for any _S_, if _S_0 has ‘owner’ access to _X_
        *   **R3:** A subject can delete an access right from any matrix entry in a row for which it controls the subject, or from any matrix entry in a column for which it owns the object.
        *   **R4:** A subject can read that portion of the matrix that it owns or controls.
        *   **R5:** A subject can create a new object, which it owns, and can then grant and delete access to the object.
        *   **R6:** The owner of an object can destroy the object, resulting in the deletion of the corresponding column of the access matrix.
        *   **R7:** Any subject can create a new subject; the creator owns the new subject and the new subject has control access to itself.
        *   **R8:** The owner of a subject can delete the row and column (if there are subject columns) of the access matrix designated by that subject.
        *   first three rules :
            *   transferring, granting, and deleting access rights
                1. If a subject S0 has access right a to subject X, it can transfer this right, with or without a copy flag, to another subject.
                2. If S0 is designated as the owner of object X, then S0 can grant an access right to that object for any other subject.
                3. If S0 has 'owner' access to X, it can add any access right to A\[S, X\] for any S.
                4. S0 can delete any access right from any matrix entry in a row for which it controls the subject, or from any matrix entry in a column for which it owns the object.
                5. A subject can read that portion of the matrix that it owns or controls.



![](https://t3764800.p.clickup-attachments.com/t3764800/509b1472-dc14-4715-b69f-f2f8afafc5a2/Screen%20Shot%202023-11-09%20at%205.11.24%20PM.png)

### Protection Domains (flexible approach)

*   A set of objects together with access rights to those objects
    *   e.g., In term of the access matrix
        *   A row defines a protection domain
        *   Each user has a protection domain→Any processes spawned(產生) by the user have access rights of the same domain (每個用戶都有一個 protection domain - 由用戶生成的所有 process 都具有相同的 protection domain 的訪問權限。)

Do the processes really need all the access rights? (process**真的需要所有訪問權限嗎？**)

*   Recall security design principles: Least privilege (請記住安全設計原則：最低權限)
    *   Every process and every user of the system should operate using the least set of privileges necessary to perform the task
*   More general concept: minimize the access rights that any user or process has at any one time
    *   e.g., A user: spawns processes with a subset of the access rights of the user
        *   Limit the capability of the processes (**用戶可以生成具有用戶訪問權限子集的進程，定義為新的保護域。這限制了 process的功能。這種方案可以用於 server process 來為不同 classes 的用戶生成 process 。此外，用戶可以為不完全信任的程序定義 protection domain，因此其訪問權限限於用戶訪問權限的** safe subset )
*   Association between a process and a domain can be static or dynamic
    *   e.g., A process: a sequence of procedures require different access rights (一系列程序需要不同的訪問權限) (**進程可能會執行一系列程序，並需要每個程序不同的訪問權限，例如讀取文件和寫入文件。通常，我們希望盡量減少任何用戶或進程在任何時候都擁有的訪問權限；保護域的使用提供了一種滿足此要求的簡單方法。**)
*   One form: distinction mode in many OSes (e.g., UNIX)
    *   User mode: certain areas of memory are protected and certain instructions may not be executed
    *   Kernel mode : privileged instructions may be executed and in which protected areas of memory may be accessed.



# **4.4  Example: Unix File Access Control**

UNIX files are administered using inodes (index nodes)

*   An inode: a control structure with key information needed by the OS for a particular file (**OS 為特定file所需的重要信息的控制結構**)
*   Several file names may be associated with a single inode (hard link); inode and file are 1-1 mapping
    *   Each file or directory has a unique inode number, and the inode number is used to identify the file or directory in the file system.
    *   Several file names may be associated with a single inode ➝ hard link
        *   inode that allows multiple file names to point to the same file.
        *   two or more file names can represent the same physical file on disk
    *   active inode is associated with exactly one file, and each file is controlled by exactly one inode （active inode 與一個文件關聯，並且由一個inode控制）
        *   active inode: an inode that is currently being used by a process.
            *   opens a file inode is activated
            *   track file's current state
                *   position in the file
                *   number of processes that have it open
*   File attributes, permissions and control information are sorted in the inode
*   On the disk there is an inode table, or inode list, that contains the inodes of all the files in the file system
*   When a file is opened its inode is brought into main memory and stored in a memory resident inode table
*   Directories are struct

Directories are structured in a hierarchical tree

• May contain files and/or other directories

• Simply a file: contains file names plus pointers to associated inodes

## Traditional UNIX File Access Control

*   UNIX user: a unique user identification number (user ID)
    *   A member of a primary group, and possibly other groups
    *   Each group is identified by a group ID
    *   It also belongs to a specific group, which initially is either its creator’s primary group, or the group of its parent directory if that directory has SetGID permission set. (**它還屬於一個特定的group，該組最初是其創建者的primary group，或者如果該目錄具有 SetGID 許可權，則該組是其 parent directory 的 group。**)
    *   Each file/directory: 12 protection bits
        *   First 9 bits: read, write, execute
        *   Last 3 bits: setUID, setGID, and sticky (**定義了文件或目錄的特殊附加行為**)![](https://t3764800.p.clickup-attachments.com/t3764800/6bcc2264-3806-488d-bcb8-34ad377edc48/Screen%20Shot%202023-11-09%20at%207.16.18%20PM.png)



*   SetUID/SetGID ([https://doc.clickup.com/d/h/3jwj0-4702/9a3306ea12c89a2](https://doc.clickup.com/d/h/3jwj0-4702/9a3306ea12c89a2)) bits
    *   **SetUID**：當設定在可執行檔案上時，在執行該檔案時，將會以該檔案的擁有者權限來執行。
    *   **SetGID**：當設定在可執行檔案上時，在執行該檔案時，將會以該檔案的群組權限來執行。
    *   Known as the “effective user ID” and “effective group ID”
    *   System temporarily grants a real user with the rights of the file owner/group in addition to the real user’s rights
    *   For executable files
        *   Only effective while the program is being executed
        *   Allows users to run programs with temporarily elevated privileges to perform a specific task
        *   e.g., the ping command: need access to networking privileges that a normal user cannot access
    *   For directories
        *   SetGID: newly created files will inherit the group of this directory, rather than the primary group ID of the user who created this file (**應用於目錄時，SetGID 許可權指定新創建的文件將繼承此目錄的組**)
        *   SetUID is ignored (**SetUID 許可權被忽略。**)
    *   Security risk?
    *   Examples: passwd and ping
        *   **%a:** The permissions of the file, in octal format. In this case, the permissions are `4755`, which translates to `rwxr-xr-x` in symbolic format. This means that the file is readable, writable, and executable by the owner, readable and executable by the group, and readable and executable by other users.
        *   **%U:** The username of the file's owner. In this case, the owner is the user `root`.
        *   **%G:** The name of the file's group. In this case, the group is the group `root`.
        *   **%n:** The name of the file. In this case, the name is `/usr/bin/passwd`.
        ![](https://t3764800.p.clickup-attachments.com/t3764800/d40509be-1ccc-4777-8a3a-6caf6d21817f/Screen%20Shot%202023-11-09%20at%207.54.14%20PM.png)
*   Sticky bit
    *   Files: the system should retain the file contents in memory following execution（**系統應在執行後將文件內容保留在內存中**） (_no longer used_)
    *   Directories: only the owner of any file in the directory can rename, move, or delete that file (**指定只有目錄中任何文件的 Owner 才能重命名、移動或刪除該文件**)
        *   Useful for managing files in shared temporary directories (**管理共享臨時目錄中的文件非常有用**)
        *   preventing other users from accidentally or maliciously deleting or moving files that they do not own
*   Superuser
    *   Exempts from the usual file access control constraints (**不受通常的文件訪問控制約束的限制**)
    *   Needs great care on the programs owned by and setuid set to “superuser” (**由“超級用戶”擁有並設置 SetUID 的****任何程序都可能會向執行該程序的任何用戶授予對系統的無限制訪問權限****。**)
*   What issues does this access scheme have?
    *   Consider one scenario
        *   Read access for file X to Users A and B
        *   Read access for file Y to Users B and C
    *   Need at least two user groups
    *   What if there are a large number of different groupings of users requiring a range of access rights to different files? (**如果需要不同訪問權限範圍的大量不同用戶組** **，則可能需要大量的group來提供此功能**)
*   No scalability: unwieldy(不便的) and difficult to manage

> Note:  
> A final point to note is that the traditional UNIX file access control scheme implements a simple protection domain structure. A domain is associated with the user, and switching the domain corresponds to changing the user ID temporarily. **最後需要注意的一點是，傳統的 UNIX 文件訪問控制方案實現了一個簡單的保護域結構。域與用戶相關聯，切換域等於臨時更改用戶 ID。**

## Access Control Lists in UNIX (Modern Unix)

*   Supported by many modern UNIX-based OSes
    *   e.g., FreeBSD, OpenBSD, Linux, and Solaris
    *   **Extended ACL** vs. [minimal ACL (traditional)](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4582?block=block-e107958a-dd19-4915-9324-fb6a2f37e70b)
*   FreeBSD
    *   administrator can assign a list of UNIX user IDs and groups to a file ➝ `setfacl, getfacl`command
    *   Any number of users and groups can be assigned to a file
        *   Each with three protection bits
    *   A file need not have an ACL; may be protected solely by traditional access control (文件不需要具有 ACL，但可以僅由傳統的訪問控制保護)
    *   An additional protection bit: whether the file has an extended ACL (**FreeBSD 文件包括一個附加的保護位，指示文件是否具有擴展 ACL**) `-rw-r--r--@` indicates that the file has extended attributes
*   Extended ACLs are used with the following strategies
    *   Owner and other classes remain the same
    *   Group class specifies the permissions for the owner group for this file
        *   Functions as a mask (maximum permission)
    *   Additional named users and named groups may be associated with the file
        *   Each with a 3-bit permission field
*   Two steps of a process requests access to a file system object
    1. selects the ACL entry that most closely matches the requesting process (最接近process request 的ACL規則)
        1. ACL entries are looked at in the following order: owner, named users, (owning or named) groups, others.
        2. Only a single entry determines access.
    2. checks if the matching entry contains sufficient permissions.
        1. A process can be a member in more than one group; so more than one group entry can match ( 一個process可以是多個 group 的 member ; 因此多個 group entry 可以匹配)
        *   **one that group entries contains the requested permissions is picked** (則會挑選一個包含所請求許可權的 **group entries**)

### **Traditional ACLs V.S. Modern ACLs**

**Traditional ACLs**

*   Define access permissions for the owner, group, and other classes
*   Use 12 protection bits to define permissions
*   Has a hierarchical structure, with the owner and group classes having priority over the other class
*   Less flexible

**Modern ACLs**

*   Define access permissions for individual users and groups, as well as the owner and group classes
*   Use 16 protection bits to define permissions
*   Have no hierarchical structure, so the permissions for individual users and groups can override the permissions for the owner and group classes
*   More flexible

Here is a table that summarizes the key differences:

| Feature | Traditional ACL | Modern ACL |
| ---| ---| --- |
| Access permissions | Owner, group, other | owner, named users, (owning or named) groups, others |
| Protection bits | 12 | 16 |
| Hierarchy | Yes | No |
| Flexibility | Less | More |

![](https://t3764800.p.clickup-attachments.com/t3764800/55676b52-28bd-4153-a266-5b611d2518e0/image.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/a6c1a92e-7c92-48f2-8648-3beb1ef634b6/image.png)

傳統 ACL 可以通過管理員為個別用戶和組以及所有者和組類別定義訪問許可權，但方式與擴展 ACL 不同。

傳統 ACL 使用 12 位保護位來定義訪問許可權。其中，9 位用於定義所有者、組和其他用戶的讀取、寫入和執行許可權。這 9 位保護位形成一個層次結構，以所有者、組和所有其他人的順序進行優先處理。

因此，在傳統 ACL 中，Owner和 group class的許可權總是優先於其他用戶的許可權。例如，如果所有者擁有讀取和寫入許可權，而組擁有讀取許可權，則所有用戶都將具有讀取許可權，但只有所有者和組中的用戶將具有寫入許可權。

擴展 ACL 則不同。它使用 16 位保護位來定義訪問許可權。其中，12 位用於定義個別用戶和組的讀取、寫入和執行許可權。這 12 位保護位是獨立的，沒有層次結構。

因此，在擴展 ACL 中，個別用戶和組的許可權可以覆蓋所有者和組類別的許可權。例如，如果所有者擁有讀取和寫入許可權，而組擁有讀取許可權，則管理員可以使用擴展 ACL 授予特定用戶對文件的執行許可權，即使該用戶不屬於所有者組。

總而言之，傳統 ACL 和擴展 ACL 都可以用於定義訪問許可權。傳統 ACL 更簡單，但靈活性較低。擴展 ACL 更複雜，但靈活性更高。

# **4.5  Role-Based Access Control**

*   Based on the roles that users assume, instead of their identities
*   Widespread commercial use and an area of active research
*   Many-to-many relationship
    *   users to roles
    *   roles to resources ![](https://t3764800.p.clickup-attachments.com/t3764800/6504c342-a7dd-44c5-bbe7-808bcc554076/Screen%20Shot%202023-11-10%20at%2011.23.00%20AM.png)



*   RBAC: obeys principle of “least privilege”
    *   Each role contains the minimum set of access rights needed for that role
    *   A user is assigned to a role that enables him or her to perform only what is required for that role
    *   role hierarchies

![](https://t3764800.p.clickup-attachments.com/t3764800/8ba0978d-103c-4e03-90bc-af3b98cc8290/Screen%20Shot%202023-11-10%20at%2011.26.45%20AM.png)![](https://t3764800.p.clickup-attachments.com/t3764800/b65f6625-425a-4de9-a60b-03def8f94173/Screen%20Shot%202023-11-10%20at%2011.27.21%20AM.png)



## RBAC Reference Models

*   A family of reference models have been defined as the basis for ongoing standardization efforts \[SAND96\]
*   Four models
    *   [RBAC0](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4582?block=block-fbf7d738-1e29-4f4e-ad46-e3fe312ad1f3): minimum functionality
    *   [RBAC1](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4582?block=block-0c3772b1-f309-449f-b8d6-3b8366abf613): RBAC0 + role hierarchies (one role to inherit permissions from another role )
    *   [RBAC2](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4582?block=block-b12e23ff-b2e0-4506-bad7-525be62804f1): RBAC0 + constrains (restrict the ways in which the components of an RBAC system may be configured)
    *   RBAC3: RBAC0 + RBAC1 + RBAC2
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/f2518e9a-bbcf-4f50-a62f-3f4043522b7c/Screen%20Shot%202023-11-10%20at%2011.31.47%20AM.png)
*   **Table 4.4 Scope RBAC Models**

| **Models** | **Hierarchies** | **Constraints** |
| ---| ---| --- |
| RBAC 0 | No | No |
| RBAC 1 | Yes | No |
| RBAC 2 | No | Yes |
| RBAC 3 | Yes | Yes |

### Base Model — **_RBAC0\\_**

*   four types of entities in an RBAC0 system:
    *   User: an individual that has access to this computer system
        *   Has an associated user ID
    *   Role: a named job function (authority level)
    *   Permission: an approval of a particular mode of access to one or more objects
    *   Session: a mapping between a user and set of roles to which a user is assigned (用戶和用戶分配的角色集之間的映射)
*   RBAC models
    *   **單箭頭表示一個，雙箭頭表示多個**
    *   RBAC0 systems use a many-to-many relationship between users and roles, and between roles and permissions.
    *   This provides greater flexibility and granularity of assignment than traditional DAC schemes.
    *   Without this flexibility and granularity, there is a greater risk that users will be granted more access to resources than is needed.
    *   The NIST RBAC document gives the following examples of the need for fine-grained access control:
        *   Users may need to list directories and modify existing files without creating new files.
        *   Users may need to append records to a file without modifying existing records.

![](https://t3764800.p.clickup-attachments.com/t3764800/f2f0598f-a9cf-4378-aa1a-196c596c1cc5/Screen%20Shot%202023-11-10%20at%2011.44.47%20AM.png)

### Role Hierarchies — **_RBAC_****1**

*   Roles with greater responsibility
    *   Greater authority to access resources
*   A subordinate job function may have a subset of the access rights of the superior job function
*   Role hierarchies reflect the hierarchical structure of roles in an organization.(角色層次結構反映了組織中角色的層次結構)
*   Subordinate roles may have a subset of the access rights of superior roles.(下屬角色可能具有上級角色的部分訪問權限)
*   Role hierarchies use inheritance to allow one role to implicitly include access rights associated with a subordinate role.(角色層次結構使用繼承來允許一個角色隱式包含與下屬角色相關聯的訪問權限)
*   A role can inherit access rights from multiple subordinate roles. (一個角色可以從多個下屬角色繼承訪問權限)
*   Multiple roles can inherit from the same subordinate role. (多個角色可以從同一個下屬角色繼承)
*   Roles can have overlapping access rights.(角色可以具有重疊的訪問權限)
    *   Production Engineer and Quality Engineer role have overlapping access share with the Engineer role
    *   Production Engineer role and the Quality Engineer role include all of the access rights of the Engineer role

![](https://t3764800.p.clickup-attachments.com/t3764800/b01a9ac3-27c4-46e6-9f26-e6091c0a8ad3/Screen%20Shot%202023-11-10%20at%2011.58.02%20AM.png)

### Constraints — **_RBAC_****2**

*   Adapting RBAC to the specifics of administrative and security policies in an organization
    *   Mutually exclusive roles (**互斥角色**)
        1. A user can be assigned to only one role in the set (either during a session or statically) (**互斥角色是指用戶只能被分配到集合中的一個角色的角色。**)
        2. Any permission (access right) can be granted to only one role in the set (任何許可權（訪問權限）只能授予集合中的其中一個角色)
        *   Non-overlapping permissions, if two users are assigned to different roles in the set (角色集具有不重疊的許可權)
        > The purpose of mutually exclusive roles is to increase the difficulty of collusion among individuals of different skills or divergent job functions to thwart security policies. (互斥角色的目的是增加具有不同技能或不同職能的個人之間勾結的難度，以挫敗安全策略。)
    *   Cardinality (**基數**)
        *   Setting a maximum number of users w.r.t. roles (**角色設置最大數量**)
        *   e.g., a project leader role or a department head role might be limited to a single user (**項目經理角色或部門主管角色可能僅限於單個用戶**)
    *   Prerequisite role (**前提角色**)
        *   A user can only be assigned to a particular role if it is already assigned to some other specified role (**該角色規定用戶只有在已經分配到其他指定角色的情況下才能被分配到特定角色**) (**前提條件可以用於構建最小特權概念的實施**)
        *   e.g., a user can be assigned to a senior (higher) role only if it is already assigned an immediately junior (lower) role (**可能要求只有在已經分配到直接下屬（較低）角色的情況下，才能將用戶分配到高級（較高）角色**)
        > **在圖 4.9 中，被分配到項目 Project Lead 的用戶也必須被分配到下屬的 Production Engineer 和 Quality Engineer 角色。然後，如果用戶在執行特定任務時不需要 Project Lead 角色的所有許可權，則用戶可以使用僅包含所需下屬角色的會話。請注意，使用與** hierarchy **概念相關聯的** prerequisites **需要 RBAC3 模型。**

###   

# **4.6  Attribute-Based Access Control**

*   Define authorizations that express conditions on properties of both the resource and the subject (**定義對resource和subject 屬性條件的授權authorization**)
    *   e.g., Alice (subject attr.) can access the HR database (resource attr.) during week days (environment attr.)
*   Strength: _flexibility_ and _expressive power_
*   Drawback: the _performance impact_ of evaluating predicates on both resource and user properties for each access (對每個 access 評估 resource 和 user properties 的性能影響)
    *   However, increased performance cost is less noticeable for Web services and cloud computing (對於 Web 服務和雲計算，增強的性能成本不太明顯)



## Attributes

*   Subject attributes
    *   A subject is an active entity that causes information to flow among objects or changes the system state （subject是指在 object 之間傳遞信息或更改系統狀態的 active entity）
    *   Attributes define the identity and characteristics of the subject
        *   e.g., name, organization, job title
*   Object attributes
    *   An object (or resource) is a passive system-related entity containing or receiving information (object（或資源）是指包含或接收信息的被動系統相關實體)
    *   Objects have attributes that can be leveraged to make access control decisions ( objects 具有可以利用來做出訪問控制決策的屬性)
        *   e.g., file name, file size, creator
*   Environment attributes
    *   The operational, technical, and even situational environment or context in which the information access occurs (信息訪問發生的操作、技術甚至情境環境或上下文)
        *   e.g., current date, time, network type, etc.
    *   _Environment attributes_ attributes have so far been largely ignored in most access control policies (這些屬性在迄今為止的大多數訪問控制策略中都很大程度上被忽略了。)

### ABAC Model: Distinguishable

*   Controls access to objects by evaluating rules against the attributes of entities (subject and object), operations, and the environment (**通過評估針對entity（subject & object）、operation 和environment 的屬性的規則來控制對object的訪問**)
    *   Attributes may be considered characteristics of anything that may be defined
*   Capable of enforcing DAC, RMAC, and MAC concepts
*   Fine-grained access control(**細粒度訪問控制**): allows an unlimited number of attributes to be combined to satisfy any access control rule (**允許將無限制數量的屬性組合起來以滿足任何訪問控制規則**)

## ABAC Logical Architecture

*   Four independent sources of information used for the access control decision
*   It is very powerful and flexible, but the cost is larger than that of other access control approaches

object proceeds according to the following steps:

1. A subject requests access to an object. This request is routed to an access control mechanism.
2. The access control mechanism is governed by a set of rules (2a) that are defined by a preconfigured access control policy. Based on these rules, the access control mechanism assesses the attributes of the subject (2b), object (2c), and current environmental conditions (2d) to determine authorization. （按照Attribute判斷是否授權）
3. The access control mechanism grants the subject access to the object if access is authorized, and denies access if it is not authorized. （提權或拒絕）



![](https://t3764800.p.clickup-attachments.com/t3764800/0ac86c63-f6e7-4d28-ab51-a65889a6c99d/Screen%20Shot%202023-11-10%20at%202.38.45%20PM.png)

*   Figure 4.11, one can observe that with ACLs the root of trust is with the object owner
    *   who ultimately enforces the object access rules by provisioning access to the object through addition of a user to an ACL.
*   In ABAC, the root of trust is derived from many sources of which the object owner has no control
    *   such as Subject Attribute Authorities, Policy Developers, and Credential Issuers.



## ABAC Policies

*   A policy is a set of rules and relationships that govern allowable behavior within an organization
    *   Based on
        *   (1) privileges of subjects;
        *   (2) how resources or objects are to be protected;
        *   (3) under which environment conditions
*   An ABAC policy model \[YUAN05\]

![](https://t3764800.p.clickup-attachments.com/t3764800/fedf368c-e83e-4b47-83c3-f0589533323c/Screen%20Shot%202023-11-10%20at%202.05.12%20PM.png)

*   e.g., an online movie website (user 𝑢, movie 𝑚, environment 𝑒) 𝑐𝑎𝑛\_𝑎𝑐𝑐𝑒𝑠𝑠 𝑢, 𝑚, 𝑒 ← 𝑀𝑒𝑚𝑏𝑒𝑟𝑠h𝑖𝑝𝑇𝑦𝑝𝑒 𝑢 = 𝑃𝑟𝑒𝑚𝑖𝑢𝑚 | (𝑀𝑒𝑚𝑏𝑒𝑟𝑠h𝑖𝑝𝑇𝑦𝑝𝑒 𝑢 = 𝑅𝑒𝑔𝑢𝑙𝑎𝑟 & 𝑀𝑜𝑣𝑖𝑒T𝑦𝑝𝑒 𝑚 = 𝑂𝑙𝑑𝑅𝑒𝑙𝑒𝑎𝑠𝑒 & 𝑇𝑖𝑚𝑒 𝑒 = 9𝑎𝑚 − 9𝑝𝑚)

### ACL Trust Chain

![](https://t3764800.p.clickup-attachments.com/t3764800/1e1d064d-0991-4c2f-83d7-73cb01ee4d32/Screen%20Shot%202023-11-10%20at%202.02.10%20PM.png)

### ABAC Trust Chain

### ![](https://t3764800.p.clickup-attachments.com/t3764800/f4900c14-f89c-4ae4-ac44-3422bcb8ba18/Screen%20Shot%202023-11-10%20at%202.02.19%20PM.png)

# **4.7  Identity, Credential, and Access Management**

> Teacher doesn't teach this section

## Identity Management

## Credential Management

## Access Management

## Identity Federation

# **4.8  Trust Frameworks**

> Teacher doesn't teach this section

## Traditional Identity Exchange Approach

## Open Identity Trust Framework



# **4.9  Case Study: RBAC System for a Bank**

*   Dresdner bank uses a variety of computer applications over servers and mainframe computers
*   In 1990, a simple DAC system was used
*   For each server and mainframe computer, administrators maintained a local access control file on each host
    *   Defining access rights for each employee on each application installed on the host
*   However, it was cumbersome, time-consuming, and error-prone
*   How to solve it?
*   Dresdner bank then introduced an RBAC scheme
*   The determination of access rights is compartmentalized into three different administrative units
    *   Roles: a combination of official position and job function
    *   Difference from NIST: a role is defined by a job function



**Role A**: Financial analyst/Clerk

**Role B**: Financial analyst/Group manager

![](https://t3764800.p.clickup-attachments.com/t3764800/574b3398-f0f1-4be0-ae00-a5189a928ed6/Screen%20Shot%202023-11-10%20at%202.08.24%20PM.png)

![](https://t3764800.p.clickup-attachments.com/t3764800/168da914-b4ae-4245-a000-02a3b870fe9b/Screen%20Shot%202023-11-10%20at%202.08.32%20PM.png)

### **Access Control Administration**

![](https://t3764800.p.clickup-attachments.com/t3764800/052cc147-3bf2-46f8-8c36-300831ad684c/Screen%20Shot%202023-11-10%20at%202.09.46%20PM.png)

###   

# **4.10  Key Terms, Review Questions, and Problems**

**4.1 What is the difference between authentication and authorization?**

Authentication is the process of verifying the identity of a user. Authorization is the process of determining whether an authenticated user has permission to access a particular resource.



**4.2 How does RBAC relate to DAC and MAC?**

RBAC, or Role-Based Access Control, is a type of access control that assigns permissions to users based on their roles within an organization. DAC, or Discretionary Access Control, is a type of access control that allows users to control who has access to their own resources. MAC, or Mandatory Access Control, is a type of access control that is imposed by the system and cannot be overridden by users.

RBAC is a more flexible and expressive type of access control than DAC or MAC. It allows organizations to define complex roles and permissions based on the needs of their business. RBAC can also be used to implement DAC and MAC policies.



**4.3 List and define the three classes of subject in an access control system.**

The three classes of subject in an access control system are:

*   **User:** A user is a human being or entity that requests access to a resource.
*   **Process:** A process is a running program that requests access to a resource.
*   **Agent:** An agent is a program or entity that acts on behalf of another subject.



**4.4 List and briefly explain the three basic elements of access control.**

The three basic elements of access control are:

*   **Subject:** The entity that requests access to a resource.
*   **Resource:** The object that access is requested for.
*   **Action:** The operation that the subject wants to perform on the resource.



**4.5 What is ABAC?**

ABAC, or Attribute-Based Access Control, is a type of access control that bases access decisions on the attributes of the subject, resource, and environment. ABAC is more flexible and expressive than RBAC, but it can also be more complex to implement and manage.



**4.6 What is the difference between an access control list and a capability ticket?**

An access control list (ACL) is a list of permissions associated with a resource. A capability ticket is a token that grants a subject permission to perform a specific operation on a specific resource.

ACLs are typically used to implement DAC policies, while capability tickets are typically used to implement MAC policies.



**4.7 List some of the main types of access control.**

The main types of access control are:

*   **Discretionary Access Control (DAC)**
*   **Mandatory Access Control (MAC)**
*   **Role-Based Access Control (RBAC)**
*   **Attribute-Based Access Control (ABAC)**



**4.8 Briefly define the four RBAC models of Figure 4.8a.**

The four RBAC models of Figure 4.8a are:

*   **RBAC0:** The simplest RBAC model, which only supports basic role assignment and permission assignment.
*   **RBAC1:** Expands on RBAC0 by supporting role hierarchies and separation of duty constraints.
*   **RBAC2:** Expands on RBAC1 by supporting constraints on role activation and permission delegation.
*   **RBAC3:** The most complex RBAC model, which supports all of the features of RBAC0, RBAC1, and RBAC2, as well as advanced features such as mutually exclusive roles and role hierarchies.



**4.9 What is meant by mutually exclusive roles in the RBAC3 model?**

Mutually exclusive roles in the RBAC3 model are roles that a user can only be assigned to one of at a time. This type of constraint can be used to prevent users from having conflicting permissions.



**4.10 Describe three types of role hierarchy constraints.**

The three types of role hierarchy constraints are:

*   **Static:** A static role hierarchy constraint is a constraint that is defined when the roles are created and cannot be changed.
*   **Dynamic:** A dynamic role hierarchy constraint is a constraint that can be changed at runtime.
*   **Hybrid:** A hybrid role hierarchy constraint is a combination of static and dynamic constraints.



**4.11 In the NIST RBAC model, what is the difference between SSD and DSD?**

SSD, or Static Separation of Duty, is a type of constraint that prevents users from being assigned to roles that have conflicting permissions. DSD, or Dynamic Separation of Duty, is a type of constraint that prevents users from activating roles that have conflicting permissions at runtime.
