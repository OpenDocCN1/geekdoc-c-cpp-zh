
# 4.4 The switch Statement 167

# 4.5 Common Programming Errors 173

# 4.6 Chapter Summary 174

# 4.7 Chapter Supplement: A Closer Look at Testing 176

# Chapter 5

# Repetition 179

# 5.1 The while Statement 180

# 5.2 Interactive while Loops 188

- Sentinels 194
- break and continue Statements 197
- The Null Statement 198

# 5.3 The for Statement 201

- Interactive for Loops 208
- Nested Loops 209

# 5.4 The do-while Statement 217

- Validity Checks 219

# 5.5 Common Programming Errors 220

# 5.6 Chapter Summary 222

# Chapter 6

# Modularity Using Functions 225

# 6.1 Function and Parameter Declarations 226

- Function Prototypes 227
- Calling a Function 228
- Defining a Function 229
- Placement of Statements 234
- Function Stubs 234
- Functions with Empty Parameter Lists 235
- Default Arguments 236
- Reusing Function Names (Overloading) 237
- Function Templates 238

# 6.2 Returning a Single Value 244

- Inline Functions 250
- Templates with a Return Value 251

# 6.3 Returning Multiple Values 257

- Passing and Using Reference Parameters 258

# 6.4 Variable Scope 267

- Scope Resolution Operator 271
- Misuse of Globals 272

## 1. 引言

本文档旨在介绍一种新型的文档解析方法，该方法能够高效地从复杂布局的图片中提取结构化信息。

- 支持多种元素类型
- 输出标准 Markdown 格式
- 提供精确的边界框坐标

| 元素类型 | 说明 |
|----------|------|
| 标题     | 文档中的各级标题 |
| 段落     | 普通文本段落 |
| 列表     | 有序或无序列表 |

> > 注意：所有坐标均为相对坐标，范围在 0 到 1 之间。

![](img/e9bf940282dfb289356f077151cc69dd_10_0.png)

```
```python
print("Hello, World!")
```
```

# Contents

10.5 Class Scope and Duration Categories 473

Static Class Members 474

Friend Functions 478

10.6 Common Programming Errors 482

10.7 Chapter Summary 482

10.8 Chapter Supplement: Thinking in Terms of Objects 484

Representing Problems with Models 485

Modeling Classes 486

# Chapter 11

Adding Functionality to Your Classes 491

11.1 Creating Class Operators 491

Assignment Operator 499

Copy Constructors 500

Base/Member Initialization 503

Operator Functions as Friends 504

11.2 How Methods Are Shared 508

The this Pointer 509

The Assignment Operator Revisited 511

Objects as Arguments 514

Notation 515

11.3 Data Type Conversions 519

Built-in to Built-in Conversion 520

Class to Built-in Conversion 520

Built-in to Class Conversion 522

Class to Class Conversion 525

11.4 Two Useful Alternatives: operator() and operator[] 529

11.5 Common Programming Errors 533

11.6 Chapter Summary 533

11.7 Chapter Supplement: Insides and Outsides 535

Abstraction and Encapsulation 537

Code Extensibility 537

# Chapter 12

Extending Your Classes 539

12.1 Class Inheritance 540

Access Specifications 541

12.2 Polymorphism 547

12.3 Dynamic Object Creation and Deletion 552

12.4 Pointers as Class Members 562

Assignment Operators and Copy Constructors Reconsidered 565

# 12.5 Common Programming Errors 568

# 12.6 Chapter Summary 568

# 12.7 Chapter Supplement: UML Class and Object Diagrams 569

Class and Object Diagrams 570

# Chapter 13

# The Standard Template Library 573

# 13.1 The Standard Template Library 574

# 13.2 Linked Lists 579

Using the STL list Class 581

Using User-Defined Objects 586

# 13.3 Stacks 590

Stack Implementation with the deque Class 592

# 13.4 Queues 598

Queue Implementation with the deque Class 599

# 13.5 Common Programming Errors 602

# 13.6 Chapter Summary 602

# Part Three

# Additional Topics 603

# Chapter 14

# The string Class and Exception Handling 605

# 14.1 The string Class 606

string Class Functions 607

String Input and Output 609

String Processing 613

# 14.2 Character Manipulation Methods 622

Character I/O 627

A Second Look at User-Input Validation 632

# 14.3 Exception Handling 634

# 14.4 Exceptions and File Checking 640

Opening Multiple Files 644

# 14.5 Input Data Validation 649

# 14.6 Common Programming Errors 656

# 14.7 Chapter Summary 656

# 14.8 Chapter Supplement: Namespaces and Creating a personal Library 657

# Contents

# Chapter 15

Strings as Character Arrays ................................ 665

**15.1 C-String Fundamentals** ................................ 666

C-String Input and Output ................................ 666

C-String Processing ................................ 670

**15.2 Pointers and C-String Library Functions** ................................ 675

Library Functions ................................ 681

Character-Handling Functions ................................ 684

Conversion Functions ................................ 688

**15.3 C-String Definitions and Pointer Arrays** ................................ 691

Pointer Arrays ................................ 693

**15.4 Common Programming Errors** ................................ 698

**15.5 Chapter Summary** ................................ 698

# Chapter 16

Data Structures ................................ 701

**16.1 Single Structures** ................................ 702

**16.2 Arrays of Structures** ................................ 708

**16.3 Structures as Function Arguments** ................................ 712

Passing a Pointer ................................ 716

Returning Structures ................................ 718

**16.4 Dynamic Structure Allocation** ................................ 721

**16.5 Unions** ................................ 724

**16.6 Common Programming Errors** ................................ 727

**16.7 Chapter Summary** ................................ 728

# Appendixes

**Appendix A**

Operator Precedence Table ................................ 729

**Appendix B**

ASCII Character Codes ................................ 731

**Appendix C**

Bit Operations ................................ *Online Only*

**Appendix D**

Floating-Point Number Storage ................................ *Online Only*

**Appendix E**

Solutions to Selected Exercises ................................ 733

Index ................................ 753

The main goal of this fourth edition of A First Book of C++ remains the same as in previous editions: to introduce, develop, and reinforce well-organized programming skills using C++. All topics are presented in a clear, unambiguous, and accessible manner to beginning students. Students should be familiar with fundamental algebra, but no other prerequisites are assumed.

Therefore, like the first three editions, this new edition begins by providing a strong foundation in structured programming. This foundation is then expanded to an object-oriented design and programming approach in a pedagogically sound, achievable progression. In addition to a number of minor changes throughout the book, the major changes in this edition are the following:

- Part I has been restructured to include arrays, files, and pointers, so it can be used as the basis for a complete introductory semester course in C++.
- The four chapters covering object-oriented programming have been revised and moved to Part II so that they form a logical continuation from structured programming to object-oriented programming.
- More than 50 new exercises have been added, and all exercises are labeled to indicate their function (Review, Practice, Program, Modify, Debug, Desk check, or For thought).
- Three new Chapter Supplements have been added to introduce the fundamentals of object-oriented design and the Unified Modeling Language (UML).
- A complete set of case studies has been added and is available on the Cengage Web site, login.cengage.com, for instructors to distribute.

The following features from the third edition have been retained:

- Fundamentals of software engineering are discussed from both procedural and object-oriented viewpoints.
- Each chapter contains a Common Programming Errors section that describes problems beginning C++ programmers typically encounter.
- The ANSI/ISO C++ iostream library and namespace mechanism are used in all programs.
- Exception handling is discussed in a separate section, with practical applications of exception handling included throughout the book.
- The C++ string class is covered.
- A thorough discussion is included of input data validation and functions to check the numerical data type of input items and allow reentering invalid numerical types.

In practical terms, this book has been written to support both a one- and two-semester technical C++ programming course; the only prerequisite is that students should be familiar with fundamental algebra. This book is constructed to be flexible enough so that instructors can mold the book to their preferences for topic sequence. This flexibility is achieved in the following ways.

Part I includes the basic structured syntax, flow control, and modularity topics needed for a thorough understanding of C++'s structural features. With the topics of arrays (Chapter 7) and files (Chapter 9) moved to Part I, this part now provides a comprehensive one-semester
