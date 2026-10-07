# Understanding Your Computer’s Memory

If you already know how a computer’s memory operates, you can skip this section. If you’re not sure, read on. Understanding your computer’s memory and how it works help you better understand certain aspects of C programming.

A computer uses random-access memory (RAM) to store information while it operates. RAM is volatile, which means that it is erased and replaced with new information as needed. Being volatile also means that RAM “remembers” only while the computer is turned on and loses its information when you turn the computer off.

Each computer has a certain amount of RAM installed. The amount of RAM in a system is usually specified in gigabytes (GB), such as 1GB, 2GB, 4GB, 8GB, or more. One gigabyte of memory is 1,024 megabytes. One megabyte of memory is 1,024 bytes. Kilobyte of memory consists of 1,024 bytes. Thus, a system with 4GB of memory actually has 4x1,024 megabytes or 4x1,024x1,024 kilobytes, or 4,194,304 kilobytes of RAM. This would be 4,194,304KBx1,024 bytes for a total of 4,294,967,296 bytes of RAM.

A byte is the fundamental unit of computer data storage. Lesson 21, “Working with Memory,” has more information about bytes. For now, Table 3.1 provides you with how many bytes it takes to store certain kinds of data.

# TABLE 3.1 Memory Space Required to Store Data

| Data | Bytes Required |
| --- | --- |
| The letter x | 1 |
| The number 500 | 2 |
| The number 241.105 | 4 |
| The phrase Sams Teach Yourself C | 21 |
| One typewritten page | Approximately 3,000 |

The RAM in your computer is organized sequentially, 1 byte following another. Each byte of memory has a unique address that can be used to identify it. This address can be used to distinguish the byte of memory from all other bytes. Addresses are assigned to memory locations in order, starting at zero and increasing to the system limit. For now, you don’t need to worry about addresses; it’s all handled by the C compiler.

Your computer’s RAM has several uses, but only data storage need concern you as a programmer. Data is the information with which your C program works. Whether your