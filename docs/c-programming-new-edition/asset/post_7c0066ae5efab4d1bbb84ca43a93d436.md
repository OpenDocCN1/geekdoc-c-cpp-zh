
## LIST OF FIGURES

- Figure 2.1. Data types in C programming.
- Figure 2.2. Basic function in C programming.
- Figure 2.3. Arithmetic operators.
- Figure 2.4. Relational and logical operators.
- Figure 3.1. Flow diagram control statements.
- Figure 4.1. Array inside the memory.
- Figure 4.2. Multi-dimensional array.
- Figure 8.1. Declaring and accessing a structure.
- Figure 8.2. Pointer and structure.
- Figure 9.1. Singly linked lists.
- Figure 9.2. Doubly linked lists.
- Figure 9.3. Circular doubly linked list.
- Figure 9.4. Stack in C programming.
- Figure 9.5. Queue in C.
- Figure 9.6. Binary tree.
- Figure 9.7. Sorting techniques.

## PREFACE

Welcome to the world of C programming! In the vast landscape of programming languages, C stands as a timeless and essential tool. Whether you are a novice programmer eager to take your first steps or an experienced developer seeking to strengthen your skills, this book is your passport to mastering the art of C programming. C has endured for decades because of its simplicity, versatility, and efficiency. It has been the foundation for building operating systems, creating applications, and even crafting embedded systems. By learning C, you are not merely acquiring a programming language; you are delving into the very heart of computing.

This book takes a practical and hands-on approach to learning C. We believe that programming is best understood through practice, so you will find numerous examples, exercises, and projects designed to reinforce your understanding and encourage your creativity. Whether your interests lie in system programming, game development, web applications, or beyond, a solid grounding in C is your gateway to success.

- **Beginners:** If you are new to programming, fret not. We begin with the basics and guide you step by step, ensuring you grasp each concept before moving on.
- **Experienced Coders:** If you are already proficient in other languages but wish to master C, you will discover advanced topics and challenges to elevate your skills.

## Introduction

Major aspect of the data processing function is the logical control of programming elements necessary to ensure that data is read and processed properly and used to produce the required output. In fact, the logical control of elements within a program is the single most important aspect of programming. Various descriptive charts are used by computer professionals to indicate the logic that a program is to incorporate. We consider the following three techniques, which are the most commonly used in the EDP field to indicate program logic.

Tools used for specifying program logic:

- Program flowcharts;
- Pseudocode;
- HIPO charts.

### 1. Program Flow Chart

It is a diagram, or pictorial representation, of the logical flow of data in a particular program. The flowchart is drawn before the program is written to ensure that the instructions will be logically integrated. The concept is not unlike that used by architects, who prepare pictorial representations, called blueprints, prior to the actual design of a building. Blueprints verify and integrate elements of a building before construction. Similarly, flowcharts verify and integrate elements of a program prior to coding.

The flowchart is drawn by programmers to ensure the accuracy of their interpretation of the logic required in the program.

Notice that the coding of instructions is only part of a program; the sequence in which these instructions are written and executed represents the logic of the program. Coding errors similar to typographical errors are easily detected by the computer during program translation; errors in logic, however, are harder to find and more difficult to fix. These logic errors can often be avoided when logical tools such as program flowcharts are drawn beforehand.

The user and the programmer often work closely in refining the flowchart. Any discrepancies, misconceptions, or lack of detail will become apparent when the logic is represented in flowchart form. The flowchart, thus, provides a common foundation with which computer specialists and users can bridge communications gaps. In the end, the flowchart should be approved by users and programmers before detailed coding is undertaken.

A special plastic or metal tool called a template is used to draw the symbols in a flowchart.

Most flowcharts can be effectively drawn using the template's five basic symbols. Note that these symbols conform to a data processing standard and are universally used throughout the computer industry. Thus, data processing personnel in diversified areas can understand the symbols and the logic used in any flowchart if they are familiar with these basic symbols. Each symbol is used to indicate the specified functions to be included in a particular logic diagram.

Let us consider the following problem to see what a program flowchart looks like.

Assume that we have a file, each with the format shown below:

| Field Name | Data Type |
|---|---|
| LASTNAME | char(15) |
| FIRSTNAME | char(12) |
| CODE | char(1) |
| TELNO | char(8) |
| ' ' | ' ' |
| ' ' | ' ' |
| ' ' | ' ' |

- ii. Flowcharts are no longer completely standardized tools. The newer structured programming techniques have necessitated changes in the traditional format of a flowchart.
- iii. It is sometimes difficult for a businessperson or user to understand the logic depicted in a flowchart.

To compensate for some of the shortcomings of program flowcharting, a new tool has been introduced that is specifically designed to depict the logic flow of a structured program. This tool is called pseudocode.

As indicated, pseudocode has been designed specifically as a method for facilitating the representation of logic in a structured program. No symbols are used, just words. As with flowcharts, the pseudocode need not indicate all the processing details; abbreviations are permissible.

Using a flowchart, it is possible, although somewhat cumbersome, to indicate a logical control sequence that is executed until a given condition exists. The following symbol is used to perform a routine until a condition is met.

![](img/c948b22e3869eae71cd653f0917e0009_20_0.png)

However, such a sequence is more easily specified using pseudocode.

The term "pseudocode" indicates that the technique is a code, similar to that used in a program. The term "pseudo" implies that, although this is a code similar to that used in a program, it is merely a representation of a code and not a language itself.

### 4. Program Development Process

There are numerous ways to complete the tasks in any process. Some methods are more efficient and effective than others. For example, if you want to dig a swimming pool in your backyard, you could get out your spade and start digging, or you could use heavy, mechanical equipment designed for the task. Both methods would get the job done, but the second method is more efficient and effective. The same principle applies to programming.

The program development process is a recommended series of steps to follow when developing a program. It consists of the following six steps:

- Define the problem;
- Design the algorithm;
- Code the program;
- Test and debug the program;
- Implement the program and train users; and
- Maintain and upgrade the program.

This list does not include documentation as a separate step; however, documentation is an important requirement throughout all the steps, each of which will be examined below. Although each step is presented as a separate and distinct process, they are all related; in actual practice, there may not be a clear separation between the steps. Let's address the topic common to all the steps of the program development process — documentation.

### 5. The Importance of Documentation

**i. Documentation** is the text or graphics that provides specific instructions about, or records the purpose or function of, a particular step or instruction in a program. Each step throughout the programming process should be documented. Documentation is sometimes done as an afterthought rather than as an ongoing integral part of the project. Approached in this manner, it can become an overwhelming burden of paperwork. If documentation guidelines are established and followed from the beginning of a project, the process will take less time and effort in the long run.

There are two good reasons to document the program development process. First, documentation leaves a clear record for someone else to understand what was done. This record is extremely important in a business environment because it is likely that the person who later corrects an error or modifies the program will not be the same person who originally designed or coded it.

Second, documenting the steps as they are developed forces a reexamination of the actions taken. Problems might be discovered early enough to avoid costly alterations later. Documentation is important even if you are programming just for your own use.

For documentation to be of value, it must be clear and concise, and it must be available to those who need it. Many organizations maintain a library where copies of all documentation are accessible to authorized personnel.
