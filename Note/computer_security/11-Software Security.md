---
title: "Computer Security Principles and Practice"
permalink: /Computer-Security-Principles-and-Practice/11-Software-Security/
layout: default
---
# 11-Software Security

# **11.1  Software Security Issues**

## Introducing Software Security and Defensive Programming

*   Many vulnerabilities result from poor programming practices
*   Consequences from insufficient checking/validation of data and error codes in programs
    *   Unvalidated input
    *   Cross-site scripting
    *   Buffer overflow
    *   Injection flaws
    *   Improper error handling
    *   ...

### Software Error Categories

*   Insecure interaction between components
    *   e.g., SQL injection, cross-site scripting, open redirect
*   Risky resource management
    *   e.g., classical buffer overflow, path traversal, download of code without integrity check
*   Porous defenses
    *   e.g., missing authentication for critical function, authorization, or encryption of sensitive data

![](https://t3764800.p.clickup-attachments.com/t3764800/ac51e22f-9bb9-4cf8-a138-1b81a18cbed0/image.png)

### Software Security: Software Quality/Reliability?

*   **Software Quality and Reliability**
    *   Concern: accidental failure of a program
        *   Unanticipated input
        *   System interaction
        *   Use of incorrect code
    *   Not the total number of bugs, but how often they are triggered
    *   Improvement: structured design and testing to identify and eliminate bugs
*   **Software Security**
    *   Attacker targets specific bugs that result in a failure that can be exploited
    *   Triggered by inputs that differ dramatically from what is usually expected
    *   Unlikely to be identified by common testing approaches

### Defensive or Secure Programming

*   The process of designing and implementing software: continue to function even when under attack
*   Software written using this process
    *   Detect erroneous conditions resulting from some attack
    *   Either continue executing safely, or fail gracefully
*   Key rule: never assume anything
    *   Check all assumptions and handle any possible error states
*   Typical programmers
    *   Attention on the steps needed for success
        *   Follow the normal flow of execution of the program
        *   But not consider every potential point of failure
    *   Often make assumptions: type of inputs and environment
*   Defensive Programming
    *   The assumptions need to be validated by the program
    *   All potential failures handled gracefully and safely
    *   But, increase codes and time spent ➔ Conflicts with business pressures
*   Typical programmers: when changes are required
    *   Focus on the changes required and what needs to be achieved
*   Defensive programming
    *   Must carefully check any assumptions made
    *   Check and handle all possible errors
    *   Carefully check any interactions with existing code
*   Requiring a changed mindset to traditional programming practices



### Security by Design

*   Security and reliability are common design goals in most engineering disciplines
*   Software development has _not_ reached high level of maturity
*   Recent years have seen increasing efforts to improve secure software development processes
    *   Software Assurance Forum for Excellence in Code (SAFECode)
        *   Outlining industry best practices for software assurance
        *   Providing practical advice for secure software development

# **11.2  Handling Program Input**

*   Incorrect handling is one of the most common failings
*   Input is any source of data from outside and whose value is not explicitly known by the programmer
*   All sources of input data must be identified
*   Explicitly validate assumptions on size and type of values before use
*   Two key areas of concern: size and interpretation

## Input Size and Buffer Overflow

*   Programmers often make assumptions: maximum expected size of input
    *   Allocated buffer size is not confirmed
    *   May result in buffer overflows
*   Testing may not identify the vulnerability (未測試發現的弱點)
    *   Test inputs are unlikely to include large enough inputs to trigger the overflow
*   Safe programming practices (in Chapter 10)
    *   Use of safe string and buffer copying routines, etc.
    *   驗證長度跟input
*   Safe coding regards any input as dangerous
    *   Processes it in a manner that does not expose the program to danger

## Interpretation of Program Input

*   Program input may be binary(0100101) or textual
    *   Binary data: depends on encoding and is usually app-specific (H.264)
    *   e.g., Ethernet frames, IP packets, and TCP segments
    *   e.g., DNS, SNMP, etc.: using binary encoding of the requests and responses
*   Failure to validate may result in an exploitable vulnerability
    *   e.g., 2014 [Heartbleed](https://zh.wikipedia.org/zh-tw/%E5%BF%83%E8%84%8F%E5%87%BA%E8%A1%80%E6%BC%8F%E6%B4%9E) OpenSSL bug
        *   Failure to check the validity of a binary input value ➔ return too much data
*   An increasing variety of character sets being used (e.g., ASCII)
    *   Care is needed to identify just which set is being used, and just what characters are being read

### Injection Attacks

*   When program input data can accidentally or deliberately influence the flow of execution of the program
    *   Most common: input data are passed as a parameter to another helper program
        *   Often occurs when using scripting languages (e.g., perl, PHP, python)
        *   Such languages encourage the reuse of other existing programs
        *   Now, often used as Web CGI scripts to process data supplied from HTML forms
*   Example
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/bdebcb87-79fe-42b5-be62-c3a1dfb65c75/image.png)
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/7cd4a487-cbc0-484d-b12a-1620bb51b941/image.png)
*   Command injection attack
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/8b6c4e65-835e-4147-8c30-e59383e85f8f/image.png)
*   Safety extension
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/16200820-986c-49e9-b6e5-03db96498c9a/image.png)



### SQL Injection Example

Vulnerable PHP code

*   ![](https://t3764800.p.clickup-attachments.com/t3764800/322bf262-de8e-4211-8e2c-364a9ae2ec0e/image.png)
*   Safer PHP code
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/5f13ff1c-fdef-45f8-8bbe-02bba5f0fec0/image.png)

Vulnerable PHP code

*   ![](https://t3764800.p.clickup-attachments.com/t3764800/94a3543d-79b4-4d08-aced-93c7bd617cba/image.png)
*   HTTP exploit request
*   Attacker利用path將hack.txt的函數使用到day.php
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/94008012-4499-470c-83dc-05cce4ad10a4/image.png)

### Cross-site Scripting (XSS) Attacks

*   Input provided to a program by one user that is subsequently output to another user
    *   Script code may need to access data associated with other pages
    *   Assumption: all content from one site is equally trusted and hence is permitted to interact with other content from that site
    *   Attacks exploit this assumption and attempt to bypass the browser’s security checks
*   Most commonly seen in scripted Web apps
    *   Involving the inclusion of script code in the HTML content of a Web page displayed by a user’s browser
    *   e.g., JavaScript, ActiveX, VBScript, Flash
*   Most common variant: XSS reflection

#### XSS Reflection

*   Consider the widespread use of guestbook programs
    *   e.g., wikis and blogs
    *   Allow users accessing the site to leave comments, which are subsequently viewed by other users
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/b8edee76-7bf9-43bf-86e7-5df3d8bdc66f/image.png)
*   Prevention: any user-supplied input should be examined
*   The browser interprets the following identically to the above code
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/b55e811c-a473-42fc-a26c-75f5c436ac91/image.png)

## Validating Input Syntax

*   Ensure that data conform with any assumptions made about the data before subsequence use
    *   e.g. textual data→contain only printable characters
*   Input data should be compared against what is wanted
    *   i.e., accepting only valid input→whitelisting
*   Alternative is to compare the input data with known dangerous values
    *   i.e., blacklisting
*   By only accepting known safe data, the program is more likely to remain secure
    *   using regular expressions



### Validating Numeric Input

*   Internally stored in fixed sized value
    *   8, 16, 32, 64-bit integers
    *   Floating point numbers depend on the processor used
        *   E.g., 32, 64, 96 bits
    *   Values may be signed or unsigned
*   Must correctly interpret text form
    *   Have issues comparing signed to unsigned (signed有正負，unsigned沒有正負，永遠都是正的)
        *   Input as unsigned may be treated as a signed value
        *   Vulnerability: negative values have the top bit set
        > e.g., input size (unsigned): s=1xxxxxxx (signed) s < max buffer size→s is negative
    *   Could be used to thwart buffer overflow check
    > 英文句子「negative values have the top bit set」的意思是「負值的最高位元會被設定為 1」。
    >
    > 在電腦科學中，一個位元（bit）是電腦中的基本儲存單位，可以用來表示 0 或 1。在二進制數字系統中，負值會用補碼（two's complement）來表示。在補碼中，負值的最高位元會被設定為 1，而其他位元則是原數字的反碼（complement）。
    >
    > 例如，在 8 位元補碼中，負值 -1 的表示如下：
    >
    > `原數字：10000001`
    >
    > `反碼：01111110`
    >
    > `補碼：11111111`
    >
    > 因此，負值的最高位元會被設定為 1。
    >
    > 在程式設計中，如果將負值當作無符號數來處理，就可能會發生錯誤。例如，如果將負值 -1 當作無符號數來處理，它會被當作 255。
    >
    > 以下是一段程式碼示例：
    >
    > C
    ```cpp
    #include <stdio.h>
    int main() {
      int x = -1;
      unsigned int y = x;
      printf("x: %d\n", x);
      printf("y: %u\n", y);
      return 0;
    }
    ```
    > 這段程式碼會輸出以下結果：
    >
    > `x: -1`
    >
    > `y: 255`
    >
    > 因此，在比較 signed 和 unsigned 值時，需要注意負值的最高位元會被設定為 1。

## Input Fuzzing

*   Major issue of input testing: very large range of inputs
    *   Textual or graphic input
    *   Random network requests
    *   Random parameters from system or libraries
    *   etc.
*   Fuzzing: a software testing technique -- using randomly generated data as inputs to a program
    *   Developed by Professor Barton Miller at University of Wisconsin Madison in 1989
    *   Simplicity and freedom from assumptions
    *   Very low cost of generating large numbers of tests
    *   Identifying reliability and security deficiencies in programs
*   Input can be completely randomly generated, or randomly generated according to some template
    *   Templates: likely scenarios for bugs
        *   e.g., excessively long inputs or textual inputs without spaces
        *   e.g., targeting critical aspects of the protocol
        *   Pros: increasing the likelihood of locating bugs
        *   Cons: assumptions about the input; misses may happen
        > 需要 random generating + template 測試
    *   A combination of both is needed for comprehensiveness
*   Conceptually very simple, but identifying only simple types of faults
    *   Unlikely to locate some bugs, e.g., only triggered by a small number of very specific input values
*   

# **11.3  Writing Safe Program Code**

*   Key issues
    *   Correct algorithm implementation: correctly solving the specified problem
    *   Correct machine instructions for algorithm
    *   Valid manipulation of data

## Correct Algorithm Implementation

*   Not correctly implement all cases or variants of the problem
    *   e.g., inappropriate interpretation or handling of program input
*   Example I: a bug in some early releases of the Netscape Web browser
    *   Implementation of the random number generator: generating session keys
    *   Assumption: the numbers should be unguessable
    *   Bug: numbers were relatively easy to predict
        *   Due to a poor choice of the information used to seed the algorithm
    *   Fix: reimplementing the random number generator
*   Example II: TCP session spoof or hijack attack
    *   Fooling the server into accepting packets using a spoofed source address
    *   Bug: initial sequence numbers are far too predictable
        *   Sequence number: an identifier and authenticator of packets
        > TCP 會話使用序列號來識別和驗證數據包。
        >
        > 初始序列號通常由隨機產生，但一些軟件存在漏洞，使其變得可預測。
        >
        > 攻擊者可以猜到序列號，並偽造源地址和序列號的數據包發送給伺服器，欺騙伺服器使其接受。
    *   Hijack attack
        *   Sequence number: the response from the server will not be seen by the attacker
        *   Correctly guessing this number: a suitable ACK packet can be constructed and sent to the server
        > 攻擊者可以猜到下一個序列號，並構造包含正確序列號的 ACK 數據包發送給伺服器，劫持原有合法的 TCP 連接。
    *   Hijack variant
        *   Waiting until some authorized external user connects and logs into the server
        *   Guessing the sequence number used and injecting packets with spoofed details
        > 攻擊者等待一個合法用戶連接并登入伺服器，然後猜測其使用的序列號，再注入包含偽裝信息和正確序列號的數據包。
    *   DoS attack
        *   Triggering RST packet from the server to terminate the connection
        > 攻擊者可以故意發送錯誤的或不完整的數據包，誘使伺服器發送 RST (重置) 數據包，終止與合法用戶的連接。
    *   Fix: truly randomized initial sequence numbers
    > **TCP 會話欺騙和劫持攻擊利用了初始序列號可預測的漏洞，通過偽造數據包和正確猜測序列號，可以竊取信息、劫持連接甚至發動 DoS 攻擊。使用真正隨機的初始序列號是重要的防禦措施之一。**
*   Example III: Programmers deliberately include additional code in a program to help test and debug it
    *   Inappropriately release information to a user of the program
    *   Permit a user to bypass security checks
    *   Was seen in the sendmail mail delivery program in the late 1980s
        *   Famously exploited by Morris Internet Worm
        *   Left in support for a DEBUG command that allowed the user to remotely query and control the running program
        *   The sendmail program ran using superuser privileges
*   Example IV: Interpreter for a high or intermediate-level languages
    *   Failure to adequately reflect the language semantics: bugs
    *   Some early implementations of the JVM: security checks for remotely codes
    > JVM把遠端code當local code執行
    *   Permit an attacker to introduce code remotely (e.g., on Web pages) and trick the JVM interpreter into treating them as locally sourced

## Ensuring that Machine Language Corresponds to Algorithm

*   Largely ignored by most programmers
    *   Assumption: the compiler or interpreter generates or executes code that validly implements the language statements
*   Malicious compiler programmer
    *   Including instructions in the compiler to emit additional code
*   Countermeasure: careful comparison of the machine code with the source
    *   Slow and difficult

## Correct Interpretation of Data Values

*   All data on a computer are stored as groups of binary bits
    *   Interpreted as a character, an integer, a floating-point number?
*   Different languages provide varying capabilities for restricting and validating interpretation of data in variables
    *   Strong typing: more limited and safer
    *   Much more liberal interpretation of data: permit program code to explicitly change their interpretation
        *   e.g., language C
        *   Easy interpretation conversion between integers and memory addresses
        *   Significant benefits for system level programming
        *   However, many errors can be caused

## Correct Use of Memory

*   Correct use of memory
    *   Issue: allocation and management of dynamic memory storage (heap)
        *   Used to manipulate unknown amounts of data
        *   Must be allocated when needed and released when done
    *   Memory leak
        *   Steady reduction in memory available on the heap: completely exhausted
        *   DoS attack: cause the program to crash
    *   Many older languages, including C: no explicit support for dynamically allocated memory
        *   By explicitly calling standard library routines
        *   Determine exactly when the memory is no longer required can be difficult ◼ Easily occur, and difficult to identify and correct
    *   Modern languages (e.g., Java and C++) handle it automatically



## 正確解釋數據值的意義

這段講述了電腦中數據存儲和解釋的方式，以及一些潛在的錯誤風險。

**重點:**

*   所有電腦數據都以二進制位元組的形式存儲。
*   同一段位元組可以被解釋為不同的東西，例如字符、整數、浮點數等等。
*   不同的程式語言對數據解釋的限制和驗證能力也不同。
*   強類型語言 (如 Java) 對數據類型有更嚴格的限制，更安全但功能也更有限。
*   弱類型語言 (如 C) 對數據類型解釋更靈活，允許程式碼改變數據的解釋方式。

**解釋轉換的風險:**

*   在弱類型語言中，整數和記憶體地址之間很容易相互轉換。
*   這種靈活性雖然對系統級程式設計帶來很多便利，但也有很大風險。
*   其中一個主要風險是錯誤使用記憶體。

**記憶體管理的錯誤:**

*   弱類型語言通常需要程式員手動管理堆記憶體 (動態分配的記憶體)。
*   堆記憶體用於處理未知大小的數據，需要在需要時分配，用完後釋放。
*   若記憶體沒有被正确釋放，就會造成記憶體洩漏。
*   記憶體洩漏會逐渐消耗可用堆記憶體，最終導致程序崩溃或 DoS 攻击。

**C 語言和記憶體管理:**

*   傳統的 C 語言没有直接支持動態分配記憶體，而是通过调用标准库函数来实现。
*   使用標準函数庫需要手動確定釋放記憶體的時機，容易出錯。
*   記憶體洩漏在 C 程序中很常見，並且難以發現和修復。

**現代語言的記憶體管理:**

*   現代語言 (如 Java 和 C++) 通常會自動管理動態分配的記憶體，避免記憶體洩漏的发生。

## Preventing Race Conditions with Shared Memory

*   Race condition
    *   Multiple processes and threats compete to gain uncontrolled access to some resource
    *   Solution: correct selection and use of appropriate synchronization primitives
    > 使用適當的同步機制，例如互斥鎖、訊號等，確保一次只能有一個進程或線程存取共享資源。
    *   But, deadlock can be still an issue
    *   Attackers may trigger the deadlock to launch DoS

# **11.4  Interacting with the Operating System and Other Programs**

## Environment Variables

## Using Appropriate, Least Privileges

*   In general, programs do not run in isolation on most computer systems
    *   multiple users, multiple programs
    *   various shared files and devices
    *   OS mediates access to system resources
    *   OS shares their use between all the executing programs
*   Several issues
    *   Environment variables
    *   Using appropriate, least privileges
    *   Systems calls and standard library functions
    *   Preventing race conditions with shared system resources
    *   Safe temporary file use
    *   Interacting with other programs

## Systems Calls and Standard Library Functions

*   Programs use system calls and standard library functions for common operations
*   The programs may not perform as expected
    *   Incorrect assumptions made for the operations of the system calls and standard library functions
    *   May be a result of system optimizing access to shared resources
    *   Result in requests for services being buffered, resequenced, or otherwise modified to optimize system use
    *   Optimizations can conflict with program goals
    > 作業系統為了優化對共享資源的訪問，可能會對程式的請求進行緩衝、重新排序或其他形式的修改。
    >
    > 這些優化雖然能提升系統整體效率，但卻可能與程式的特定需求相衝突。
    >
    > 程式可能假設系統呼叫會立即執行，但實際上作業系統可能會將其放入佇列中等待執行。
    >
    >   
    >
    > 程式可能依賴特定順序的系統呼叫回傳結果，但作業系統為了優化效能可能會改變此順序。
    >
    > 程式可能假設標準函數的行為與文件描述完全一致，但實際上一些實作可能會略有不同。



### Example: How to Securely Delete a File?

*   Standard file delete utility: simply removes the linkage between the file’s name and its contents
*   Initial secure file shredding program algorithm

![](https://t3764800.p.clickup-attachments.com/t3764800/00e67c9c-3d01-4fdc-b5ce-acfbcfd6fadd/Screen%20Shot%202023-12-15%20at%2012.26.56%20PM.png)

*   Incorrect assumptions
    *   System will write the new data to same disk blocks
    *   Data are written immediately to disk
    > OS為了最佳化硬碟的速度，所以會放在buffer，等buffer存到一定的程度才執行
    *   When the I/O buffers are flushed and the file is closed, the data are then written to disk
*   Better secure file shredding program algorithm

![](https://t3764800.p.clickup-attachments.com/t3764800/0a45935d-3a87-4311-bb21-6fa2e1993a1f/Screen%20Shot%202023-12-15%20at%2012.28.55%20PM.png)

*   Open the file for update: the existing data are still required
*   Flush buffer after each pattern is written
*   Synchronize the file system’s data with the values on the device

## Preventing Race Conditions with Shared System Resources

## Safe Temporary File Use

## Interacting with Other Programs

# **11.5  Handling Program Output**

*   Program output
    *   May be stored for future use, sent over net, displayed
    *   May be binary or text
*   Important: output conforms to the expected form and interpretation
*   Programs must identify what is permissible output content
    *   Filter any possibly untrusted data to ensure that only valid output is displayed
*   Character set should be specified

# **11.6  Key Terms, Review Questions, and Problems**

#
