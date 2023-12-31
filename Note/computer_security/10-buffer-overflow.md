---
title: "Computer Security Principles and Practice"
permalink: /Computer-Security-Principles-and-Practice/10-buffer-overflow/
layout: default
---
# 10-buffer-overflow

[https://youtu.be/NEtHcWE3Ki0?si=dFJ6BSPrhXRJ8fCU&t=6450](https://youtu.be/NEtHcWE3Ki0?si=dFJ6BSPrhXRJ8fCU&t=6450)

| 1995 | A buffer overflow in NCSA httpd 1.3 was discovered and published on the Bugtraq mailing list by Thomas Lopatic. |
| ---| --- |
| 1996 | Aleph One published “Smashing the Stack for Fun and Profit” in Phrack magazine, giving a step by step introduction to exploiting stack-based buffer overflow vulnerabilities. |
| 2001 | The Code Red worm exploits a buffer overflow in Microsoft IIS 5.0 |
| 2003 | The Slammer worm exploits a buffer overflow in Microsoft SQL Server 2000. |
| 2004 | The Sasser worm exploits a buffer overflow in Microsoft Windows 2000/XP Local Security Authority Subsystem Service (LSASS). |
| 1998 | The Morris Internet Worm uses a buffer overflow exploit in “fingerd” as one of its attack mechanisms. |

| **1988** | The Morris Internet Worm uses a buffer overflow exploit in “fingerd” as one of its attack mechanisms. |
| ---| --- |
| **1995** | A buffer overflow in NCSA httpd 1.3 was discovered and published on the Bugtraq mailing list by Thomas Lopatic. |
| **1996** | Aleph One published “Smashing the Stack for Fun and Profit” in _Phrack_ magazine, giving a step by step introduction to exploiting stack-based buffer overflow vulnerabilities. |
| **2001** | The Code Red worm exploits a buffer overflow in Microsoft IIS 5.0. |
| **2003** | The Slammer worm exploits a buffer overflow in Microsoft SQL Server 2000. |
| **2004** | The Sasser worm exploits a buffer overflow in Microsoft Windows 2000/XP Local Security Authority Subsystem Service (LSASS). |

# **10.1  Stack Overflows**

## Buffer Overflow Basics

*   A buffer overflow: known as a **_buffer overrun_** or **_buffer overwrite_**
*   NISTIR 7298 (Glossary of Key Information Security Terms, May 2013)

> A condition at an interface under which **_more input can be placed into a buffer or data holding area than the capacity allocated, overwriting other information_**. Attackers exploit such a condition to crash a system or to insert specially crafted code that allows them to gain control of the system.

*   Programming error: a process attempts to store data beyond the limits of a fixed sized buffer
    *   Overwrites adjacent memory locations(覆寫比鄰的記憶體位置)
    *   Locations could hold other program variables and parameters
*   Buffer could be located on the stack, in the heap, or in the data section of the process

**Consequences**

*   **Corruption of program data**
*   **Unexpected transfer of control**
*   **Memory access violations**
*   **Execution of code chosen by attacker**

### Basic Buffer Overflow Example

```cpp
int main(int argc, char *argv[]) { int valid = FALSE;
  char str1[8];
  char str2[8];
  next_tag(str1);
  gets(str2);
  if (strncmp(str1, str2, 8) == 0)
    valid = TRUE;
  printf("buffer1: str1(%s), str2(%s), valid(%d)\n", str1, str2, valid);
}
```



```powershell
$ cc -g -o buffer1 buffer1.c
$ ./buffer1
START
buffer1: str1(START), str2(START), valid(1)
$ ./buffer1
EVILINPUTVALUE
buffer1: str1(TVALUE), str2(EVILINPUTVALUE), valid(0)
$ ./buffer1
BADINPUTBADINPUT
buffer1: str1(BADINPUT), str2(BADINPUTBADINPUT), valid(1)
```



![](https://t3764800.p.clickup-attachments.com/t3764800/d9e0b0d8-b446-4eb7-acc1-c302597076ce/image.png)

Result: corruption of the variable str1

What if str1 is a password?



Needs for the Attacker: Exploiting a Buffer Overflow

*   To identify a buffer overflow vulnerability in some program (識別程式buffer overflow弱點)
    *   That can be triggered using externally sourced data under the attackers control
*   To understand how that buffer will be stored in the process memory (知道buffer是如何存在ｐprocess memory)
    *   The potential for corrupting adjacent memory locations
    *   Potentially altering the flow of execution of the program

### How to Identify Vulnerable Programs?

*   Inspecting the program source
*   Tracing the execution of programs as they process oversized input
*   Using tools to automatically identify potentially vulnerable programs
    *   Such as fuzzing: a software testing technique
        *   Using randomly generated data as inputs to a program
        *   The range of inputs can be very large
        *   To test whether the program correctly handles all such abnormal inputs

### Why Programs are not Necessarily Protected?

*   Basic machine level
    *   All the data manipulated by machine instructions: stored in either the processor’s registers or in memory
    *   Data’s interpretation: entirely determined by the function of the instructions
        *   Can be treated as integer values, addresses of data, arrays of characters, etc.
    *   Responsibility on the assembly language programmer: ensuring that the correct interpretation is placed on any saved data value
*   Assembly language programs
    *   The greatest access to the resources
    *   But, at the highest cost and responsibility in coding effort
*   Modern high-level programming languages (e.g., Java, Python)
    *   Have a strong notion of type and valid operations
    *   Not vulnerable to buffer overflows: flexibility and safety
        *   More data to be saved are not allowed
    *   Costs in resource use
        *   Imposing checks at both compile and run times
    *   Limiting the usefulness in writing code
*   Between these two extremes: C and related languages
    *   Have many modern high-level control structures and data type abstractions
    *   But, allow direct access to low-level resources
        *   Vulnerable to the buffer overflow
        *   A large legacy of widely used, unsafe, and hence vulnerable codes

## Stack Buffer Overflows

*   Occurring when the targeted buffer is located on the stack
    *   Stack: storing local variables in a function’s stack frame
*   Also referred to as stack smashing
*   First being seen in the Morris Internet Worm in 1988
    *   An unchecked buffer overflow from the C gets()in the fingerd daemon

### Function call Mechanims

*   Stack frame: saving the following data
    *   Return address to the calling function
    *   Parameters passed to the called function
    *   Values of local variables
    > 一個函數調用另一個函數時，至少需要一個地方保存返回地址，以便被調用的函數完成後可以返回控制權。所有這些數據通常都保存在stack上，結構稱為stack frame
*   Right stack frame: function P calls another function Q



![](https://t3764800.p.clickup-attachments.com/t3764800/470ac872-6daa-4766-acba-009b0dc7755f/image.png)

function P calling another function Q can be summarized as follows. The calling function P:

1. **Pushes the parameters for the called function onto the stack (typically in reverse order of declaration). (**將要傳遞給被調用函數的参数壓入Stack (通常按照聲明順序的逆序排列**)**
2. **Executes the call instruction to call the target function, which pushes the return address onto the stack. (**執行 `call` 指令，調用目標函數，並將返回地址壓入堆棧**)**

The called function Q:

1. **Pushes the current frame pointer value (which points to the calling routine’s stack frame) onto the stack. (**將當前的幀指標值 (指向調用例程的堆棧幀esp) 壓入堆棧**)**
2. **Sets the frame pointer to be the current stack pointer value (i.e., the address of the old frame pointer), which** **now identifies the new stack frame location for the called function****. (**將frame pointer設置為當前的stack pointer的值 (即舊幀指標的地址old ebp)，現在它標示了被調用函數的新堆棧幀stack frame location(ebp)**)**
3. **Allocates space for local variables by moving the stack pointer down to leave sufficient room for them. (**通過將stack pointer向下移動以留出足夠空間(esp)，為局部變量（esi,edi,ebx)分配空间。**)**
4. **Runs the body of the called function. (**運行被調用函數的程式主體**)**
5. **As it exits, it first sets the stack pointer back to the value of the frame pointer (effectively discarding the space used by local variables). (**在退出時，首先將stack pointer(esp)設置frame pointer(ebp)的值 (實際上是丟棄了局部變量使用的空間**)**
6. **Pops the old frame pointer(ebp) value (restoring the link to the calling routine’s stack frame). (**彈出舊幀指標值 (恢復到調用例程的stack frame的鏈接)**)**
7. **Executes the return instruction which pops the saved address off the stack and returns control to the calling function. (**執行 `return` 指令，將保存的地址從堆棧中彈出，並將控制權返回给調用函數**)**

Lastly, the calling function:

10\. Pops the parameters for the called function off the stack. (將被調用函數的参数從stack中彈出)

11\. Continues execution with the instruction following the function call. (繼續執行函數調用後面的指令)

[https://youtu.be/5iQkR69H\_1M?feature=shared](https://youtu.be/5iQkR69H_1M?feature=shared)[https://youtu.be/7ukTs4Bi7hI?feature=shared](https://youtu.be/7ukTs4Bi7hI?feature=shared)[https://youtu.be/seo5Es4pycs?feature=shared](https://youtu.be/seo5Es4pycs?feature=shared)

### Stack Overflow Example

### ![](https://t3764800.p.clickup-attachments.com/t3764800/8687c234-df80-4ae2-8ccb-4d61b38673b9/image.png)

1. **Local buffer overflow vulnerability:** An exploit can overwrite the saved frame pointer and return address, leading to a stack overflow attack.
2. **Layout of local variables:** Local variables are allocated in the stack frame in order of declaration, growing downward in memory.
3. **Process address space:** A program has its own virtual address space with specific sections for code, data, heap, and stack.
4. **Stack growth:** The stack grows downward in memory, with stack frames placed one below another.



### Stack Overflow Example

![](https://t3764800.p.clickup-attachments.com/t3764800/2532b21c-c13e-4d23-8b8c-6ba105b01b40/image.png)

### Stack Overflow Stack Values

Return address: 0x080483f0

Frame pointer value: 0xbffffbe8

## ![](https://t3764800.p.clickup-attachments.com/t3764800/0b1e3655-a00a-410c-acfb-f8f2b101b74d/image.png)

### More Stack Overflow Vulnerabilities

*   Potential for a buffer overflow: anywhere that data is copied or merged into a buffer
*   Occurring when the program does not check to ensure the buffer is large enough, or the data copied are correctly terminated
    *   Some of the data are read from outside the program
    *   Unsafe copy between functions in the same program

### Example for the Unsafe Copy between Functions

### ![](https://t3764800.p.clickup-attachments.com/t3764800/1b7297d3-efe0-4382-83f5-2ef311e77fd3/image.png)

### Some Common Unsafe C Standard Library Routines

*   These routines are all suspect and should not be used without checking the total size of data being transferred

![](https://t3764800.p.clickup-attachments.com/t3764800/a9959309-626e-4d28-9781-86e0a4e5a69b/image.png)

## Shellcode

*   Code supplied by the attacker
    *   Often save in buffer being overflowed
    *   Traditionally transferred control to a user command-line interpreter (shell)
*   Simply machine code
    *   Specific to processor and operating system
    *   Traditionally needed good assembly language skills to create
*   Many sites and tools have been developed that automate this process
    *   e.g., Metasploit project [https://www.metasploit.com/](https://www.metasploit.com/)
        *   Providing useful information to people who perform penetration, IDS signature development, and exploit research
        *   Including an advanced open-source platform for developing, testing, and using exploit code

### Example: Launching Shell on an Intel Linux System

*   Several requirements
    *   The high-level language spec must be compiled into equivalent machine language
    *   The instructions should be included inline, rather than relying on the library function
    *   Position independent: cannot contain any absolute address
        *   Only relative address references, offsets to the current instruction address
    *   Cannot contain any NULL values
        *   In C, a string is always terminated with a NULL character

![](https://t3764800.p.clickup-attachments.com/t3764800/3a918d20-304a-4806-b92a-02ba2c9db0ff/image.png)

# ![](https://t3764800.p.clickup-attachments.com/t3764800/d37d80ca-18b9-4c4e-aede-dcff3370675e/image.png)

# ![](https://t3764800.p.clickup-attachments.com/t3764800/5b614dce-11e4-4fa0-989f-1efe48149f47/image.png)

### Example of a Stack Overflow Attack

*   Scenario: an intruder has gained access to some system as a normal user, and wishes to exploit a buffer overflow in a trusted utility to gain greater privileges
*   How?
    *   Identified a suitable, vulnerable, trusted utility program: **_buffer4_**
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/cf5c190f-aff4-4b2d-b9c8-b193680161c3/image.png)
    *   Analyze it to determine➔running the program using a debugger
        *   The likely location of the targeted buffer on the stack
        *   How much data are needed to reach up to and overflow the old frame pointer and return address in its stack frame
    *   Assume that the following information has been obtained
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/cd6c14e6-2b30-43f6-82ca-5beb44d5b0e0/image.png)
    *   How many bytes are needed to fill the buffer and reach the saved frame pointer?
*   Given the number of bytes needed to fill the buffer, what are next steps?
    *   Allowing a few more spaces at the end to provide room for the args array
    *   The NOP sled at the start is extended until the buffer is full
    *   Replace the return address
*   How many bytes are needed to be packed into inp?
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/6c310da7-6b80-4f63-ad9f-7fd331eb5df8/image.png)
    *   ![](https://t3764800.p.clickup-attachments.com/t3764800/d8a43735-2125-4050-ada7-0965686b37f8/image.png)
*   Attacker must also specify the commands to be run by the shell once the attack succeeds
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/c44e3ddd-b7c5-4fcd-b29e-b828a111885a/image.png)

### Much More than this Attack Example

*   Exploit of a local vulnerability: enabling attacker to escalate his privileges
*   Some practical variances
    *   The buffer is likely to be larger (1024 is a common size)
    *   A targeted utility will likely use buffered rather than unbuffered input
        *   The input library reads ahead by some amount beyond what the program was requested
        *   When the execve (“/bin/sh”) function is called, this buffered input is discarded
*   Another possible target: a network daemon
    *   Listening for connection requests from clients
    *   Spawning a child process to handle that request
    *   Typically with the network connection mapped to its standard input/output
    *   May use the same type of unsafe input or buffer copy code
*   Attacker might want to create shellcode to perform somewhat more complex operations
*   Both the Metasploit project and the Packet Storm websites include many packaged shellcodes
    *   Set up a listening service to launch a remote shell
    *   Create a reverse shell that connects back to the hacker
    *   Use local exploits that establish a shell or execve a process
    *   Flush firewall rules that currently block other attacks
    *   Break out of a restricted execution environment, giving full access to the system

# **10.2  Defending Against Buffer Overflows**

*   Two broad defense approaches
    *   [Compile-time defense](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4882?block=block-8c7e0941-866c-426c-8448-1daebf881185)
        *   Aim to harden programs to resist attacks in new programs (旨在強化程序以抵禦新程序中的攻擊)
    *   [Run-time defense](https://app.clickup.com/3764800/v/dc/3jwj0-1320/3jwj0-4882?block=block-04fa589f-220b-4db7-bea6-bebdb40c52e5)
        *   Aim to detect and abort attacks in existing programs(偵測並中止現有程式中的攻擊)

## Compile-Time Defenses

### Choice of programming languages

*   Using a modern high-level language
*   Pros: not vulnerable to buffer overflow
    *   Having a strong notion of variable type and permissible operations
    *   Compilers include additional code to enforce range checks and permissible operations
*   Cons:
    *   Additional code must be executed at run time to impose checks
    *   Flexibility and safety come at a cost in resource use
        *   Mush less significant due to the rapid increase in processor performance
*   Access to some low-level instructions and hardware resources is lost

### Safe coding techniques

*   C designers placed much more emphasis on space efficiency and performance considerations than on type safety
    *   Assumed programmers would exercise due care in writing code
*   Programmers need to inspect the code and rewrite any unsafe coding
    *   An example of this is the OpenBSD project
        *   Programmers have audited the existing code base, including the operating system, standard libraries, and common utilities
        *   This has resulted in what is widely regarded as one of the safest operating systems in widespread use
*   Codes not only for normal successful execution
    *   But, constantly aware of how things might go wrong
    *   Coding for graceful failure: always doing something sensible when the unexpected occurs
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/3eb53128-d183-4f1a-a307-b292284f0c42/image.png)

> Figure 10.10a shows an example of an unsafe byte copy function. This code copies len bytes out of the from array into the to array starting at position `pos` and returning the end position. Unfortunately, this function is given no information about the actual size of the destination buffer `to` and hence is unable to ensure an overflow does not occur
>
> `to`可能 pos 過大導致 buffer overflow，呼叫程式碼應確保size+len的值不大於to數組的大小

*   ![](https://t3764800.p.clickup-attachments.com/t3764800/7d11a6f6-1435-493e-a3b6-f52fd4d961e2/image.png)

> Figure 10.10b shows an example of an unsafe byte input function. It reads the length of binary data expected and then reads that number of bytes into the destination buffer. Again the problem is that this code is not given any information about the size of the buffer, and hence is unable to check for possible overflow.
>
> 它讀取預期的二進位資料長度，然後將該位元組數讀入目標緩衝區。同樣的問題是，這段程式碼沒有給出任何有關緩衝區大小的信息，因此無法檢查可能的溢出

### Language extensions and use of safe libraries

*   Handling dynamically allocated memory: more problematic
    *   The size information is not available at compile time
*   Requiring an extension and the use of library routines
    *   Cons
        *   Generally, there is a performance penalty
        *   Programs and libraries need to be recompiled with the modified compiler
        *   Feasible for new OSes, but likely to have problems with third-party apps
*   Common Concern with C: the use of unsafe standard library routines
    *   Replacing these with safer variants
    *   A well-known example: Libsafe
        *   Including additional checks to ensure that the copy operations do not extend beyond the local variable space
        *   Dynamic library: does not require existing programs to be recompiled

#### Safe Coding Style

*   google C++ Style Guide
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/782a318b-0606-48ad-af81-c057d44536f8/image.png)
*   ![](https://t3764800.p.clickup-attachments.com/t3764800/c770e8b8-4ed8-4449-b26d-f2e8aa1ebea1/image.png)

### Stack protection mechanisms

*   Add function entry and exit code to check stack for signs of corruption
    *   Stackguard: best known protection mechanism➔a GCC compiler extension
    *   Function entry code: writing a _canary value_ below the old frame pointer address
    *   Function exit code: checking that the _canary value_ has not changed
    *   The _canary value_: unpredictable and different on different systems Why?
    > Named after the miner’s canary used to detect poisonous air in a mine and thus warn the miners in time for them to escape.
    *   Cons
        *   All programs needing protection need to be recompiled
        *   The structure of the stack frame has changed: causing problems with programs, e.g., debuggers
    *   Has been used to recompile an entire Linux distribution
*   Another variants: Stackshield and Return Address Defender (RAD)
    *   Also GCC extensions: including additional function entry and exit code
    *   Do not alter the structure of the stack frame
    *   Function entry code: writing a copy of the return address to a safe region of memory
    *   Function exit code: checking the return address in the stack frame against the save copy
    *   Compatible with unmodified debuggers Why?
    *   Programs must be recompiled

## Run-Time Defenses

*   Can be deployed as OS updates to provide protection
    *   Compile-time approaches: usually require recompilation of existing programs
    *   Involving changes to the memory management
*   Several approaches
    *   Executable Address Space Protection
        *   Block the execution of code on the stack
            *   Against the attacks: copying machine code into the targeted buffer and then transferring execution to it
        *   Tag pages of virtual memory as being non-executable
            *   Requires support from memory management unit (MMU)
            *   Long existed on SPARC used by Solaris
            *   Recent addition of the no-execute bit in the x86 family
            *   A standard feature in recent OSes
        *   Cons
            *   Unable to support executable stack code
                *   e.g., Java Runtime system, nested functions in C, Linux signal handlers
    *   Address space randomization
        *   Manipulate location of key data structures
            *   Stack, heap, global data
            *   Using random shift for each process
            *   Large address range on modern systems: wasting some has negligible impact
        *   Randomize location of heap buffers
        *   Random location of standard library functions
        *   **Example implementation:**
            *   OpenBSD includes all of these extensions in its security features.
    *   **Guard pages**
        *   Place guard pages between critical regions of memory
            *   Flagged in MMU as illegal addresses
            *   Any attempted access aborts process
        *   Further extension places guard pages between stack frames and heap buffers
            *   Cost in execution time to support the large number of page mappings necessary

# **10.3  Other Forms of Overflow Attacks**

## Replacement Stack Frame

## Return to System Call

## Heap Overflows

*   Attack buffer located in heap
    *   Typically located above program code
    *   Memory is requested by programs to use in dynamic data structures (such as linked lists of records)
*   No return address
    *   Hence no easy transfer of control
    *   May have function pointers to be exploited
    *   Or manipulate management data structures

> Defense:  
> • Making the heap non-executable  
> • Randomizing the allocation of memory on the heap

![](https://t3764800.p.clickup-attachments.com/t3764800/4c4a9660-5780-4b87-96e5-8daca52f75e2/image.png)

## Global Data Area Overflows

*   Attack buffer located in global data
    *   May be located above program code
    *   If has function pointer and vulnerable buffer
    *   Or adjacent process management tables
    *   Aim to overwrite function pointer later called

> Defense  
> Non executable or random global data region  
> Move function pointers or use guard pages

![](https://t3764800.p.clickup-attachments.com/t3764800/134d05a7-ee8e-4fa4-a1cc-b884252aac7e/image.png)

## Other Types of Overflows

# **10.4  Key Terms, Review Questions, and Problems**

#
