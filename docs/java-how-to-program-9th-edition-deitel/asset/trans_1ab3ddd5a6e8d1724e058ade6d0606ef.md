

## GUI 和图形

- 可扩展的 GUI 和图形呈现。教授入门课程的教师可以选择涵盖 GUI 和图形的程度——从无，到在早期章节中穿插的可选 10 个简短章节的入门序列，再到第 14、15 和 25 章以及附录 I 中的深入讲解。
- GroupLayout 布局管理器。我们在 NetBeans IDE 中的 GUI 设计工具的上下文中讨论 GroupLayout 布局管理器。
- JTable 排序和过滤功能。第 28 章使用这些功能对 JTable 中的数据进行重新排序并通过正则表达式进行过滤。

## 其他功能

- Android。由于对基于 Android 的智能手机和平板电脑的巨大兴趣，我们在 Companion Website 上包含了三章关于 Android 应用开发的介绍。这些章节来自我们新推出的 Deitel Developer Series 书籍《Android for Programmers: An App-Driven Approach》。在学习 Java 之后，你会发现使用可从 developer.android.com 下载的免费 Android 模拟器开发和运行 Android 应用是相当直接的。
- 软件工程社区概念。我们讨论敏捷软件开发、重构、设计模式、LAMP、SaaS（软件即服务）、PaaS（平台即服务）、云计算、开源软件等。

## 依赖关系图

下一页的图表显示了各章节之间的依赖关系，以帮助教师规划教学大纲。《Java How to Program, 9/e》适用于各种水平的多种编程课程，尤其最适用于 CS 1 和 CS 2 课程以及相关学科的入门课程序列。该书具有清晰的模块化组织。第 1–11 章和第 14–17 章构成了具有扎实面向对象编程介绍的可访问的初级编程序列。可选的第 12–13 章构成了使用 UML 进行面向对象设计的入门。GUI 和图形轨道以及第 14、15、24 和 25 章构成了实质性的 GUI、图形和多媒体序列。第 18–22 章构成了不错的数据结构序列。第 26–27 章构成了多线程和 Internet 网络的坚实介绍。第 28–31 章构成了丰富的数据库驱动的 Web 应用开发序列。

### 模块和章节依赖关系图

[Note: Arrows pointing into a chapter indicate that chapter's dependencies. Some chapters have multiple dependencies.]

**介绍**
- 1 Introduction to Computers and Java

**编程入门、类和对象**
- 2 Intro to Java Applications
- 3 Intro to Classes and Objects

**控制语句、方法和数组**
- 4 Control Statements: Part 1
- 5 Control Statements: Part 2
- 6 Methods: A Deeper Look
- 7 Arrays and ArrayLists

**(Optional) GUI & Graphics Track**
- 3.9 Using Dialog Boxes
- 4.14 Creating Simple Drawings
- 5.10 Drawing Rectangles and Ovals
- 6.13 Colors and Filled Shapes
- 7.15 Drawing Arcs
- 8.16 Using Objects with Graphics
- 9.8 Displaying Text and Images Using Labels
- 10.8 Drawing with Polymorphism

**面向对象编程**
- 8 Classes and Objects: A Deeper Look
- 9 Object-Oriented Programming: Inheritance
- 10 Object-Oriented Programming: Polymorphism
- 11 Exception Handling

**使用 UML 进行面向对象设计**
- 12 (Optional) Object-Oriented Design with the UML
- 13 (Optional) Implementing an Object-Oriented Design

**数据结构**
- 18 Recursion¹
- 19 Searching, Sorting and Big O
- 20 Generic Collections
- 21 Generic Classes and Methods
- 22 Custom Generic Data Structures

**字符串和文件**
- 16 Strings, Characters and Regular Expressions
- 17 Files, Streams and Object Serialization

**多线程和网络**
- 26 Multithreading²
- 27 Networking³

**数据库驱动的桌面和 Web 开发**
- 28 JDBC⁴
- 29 JSF Web Apps: Part 1
- 30 JSF Web Apps: Part 2
- 31 Web Services

**GUI、图形、Applet 和多媒体**
- 14 GUI Components: Part 1
- 15 Graphics and Java2D
- 23 Applets and Java Web Start⁵
- 24 Multimedia: Applets and Applications
- 25 GUI Components: Part 2

1. Chapter 18 is dependent on Chapters 14 and 15 for GUI and graphics used in one example.

2. Chapter 26 is dependent on Chapter 14 for GUI used in one example and on Chapters 20–21 for one example.
3. Chapter 27 is dependent on Chapter 23 for one example that uses an applet. The large case study (on the web) depends on Chapter 25 for GUI and Chapter 26 for multithreading.
4. Chapter 28 is dependent on Chapter 14 for GUI used in one example.
5. More applets are covered in Chapters 24 and 27.

## 教学方法

《Java How to Program, 9/e》包含数百个完整的可用示例。我们强调程序的清晰度并专注于构建工程良好的软件。

语法着色。为提高可读性，我们对所有 Java 代码进行语法着色，类似于大多数 Java 集成开发环境和代码编辑器对代码进行语法着色的方式。我们的语法着色约定如下：

- comments appear in green
- keywords appear in dark blue
- errors appear in red
- constants and literal values appear in light blue
- all other code appears in black

*Code Highlighting.* We place yellow rectangles around key code segments.

*Using Fonts for Emphasis.* We place the key terms and the index’s page reference for each defining occurrence in **bold maroon** text for easier reference. We emphasize on-screen components in the **bold Helvetica** font (e.g., the File menu) and emphasize Java program text in the Lucida font (for example, int x = 5;).

*Web Access.* All of the source-code examples can be downloaded from:

```
www.deitel.com/books/jhtp9
www.pearsonhighered.com/deitel
```

*Objectives.* The opening quotes are followed by a list of chapter objectives.

*Illustrations/Figures.* Abundant tables, line drawings, UML diagrams, programs and program outputs are included.

*Programming Tips.* We include programming tips to help you focus on important aspects of program development. These tips and practices represent the best we’ve gleaned from a combined seven decades of programming and teaching experience.

**Good Programming Practices**
*The Good Programming Practices call attention to techniques that will help you produce programs that are clearer, more understandable and more maintainable.*

**Common Programming Errors**
*Pointing out these Common Programming Errors reduces the likelihood that you’ll make them.*

**Error-Prevention Tips**
*These tips contain suggestions for exposing bugs and removing them from your programs; many describe aspects of Java that prevent bugs from getting into programs in the first place.*

**Performance Tips**
*These tips highlight opportunities for making your programs run faster or minimizing the amount of memory that they occupy.*

**Portability Tips**
*The Portability Tips help you write code that will run on a variety of platforms.*

**Software Engineering Observations**
*The Software Engineering Observations highlight architectural and design issues that affect the construction of software systems, especially large-scale systems.*

**Look-and-Feel Observations**
*The Look-and-Feel Observations highlight graphical-user-interface conventions. These observations help you design attractive, user-friendly graphical user interfaces that conform to industry norms.*

Summary Bullets. We present a section-by-section bullet-list summary of the chapter. For ease of reference, we include the page number of each key term’s defining occurrence in the text.

Self-Review Exercises and Answers. Extensive self-review exercises and answers are included for self study. All of the exercises in the optional ATM case study are fully solved.

Exercises. The chapter exercises include:

- simple recall of important terminology and concepts
- What’s wrong with this code?
- What does this code do?
- writing individual statements and small portions of methods and classes
- writing complete methods, classes and programs
- major projects
- in many chapters, Making a Difference exercises.

Index. We’ve included an extensive index. Defining occurrences of key terms are highlighted with a bold maroon page number.

## 《Java How to Program, 9/e》 中使用的软件

本书所需的所有软件均可免费从网络下载。请参阅本前言之后紧跟的 Before You Begin 部分，其中包含每个下载的链接。

我们使用免费的 Java Standard Edition Development Kit (JDK) 6 编写了《Java How to Program, 9/e》中的大多数示例。对于可选的 Java SE 7 模块，我们使用了 OpenJDK 的 JDK 7 早期访问版本。在第 29–31 章中，我们还使用了 NetBeans IDE，在第 28 章中，我们使用了 MySQL 和 MySQL Connector/J。你可以在我们的 Java Resource Centers 找到更多资源和软件下载：

```
www.deitel.com/ResourceCenters.html
```

## Java IDE 资源工具包

你的讲师可能已通过你的大学书店订购了《Java How to Program, 9/e》的 Value Pack 版本，该版本捆绑了 Java IDE Resource Kit。该工具包包含 CD 或 DVD 版本的 Java™ SE Development Kit 6 for Windows®、Eclipse™ IDE for Windows®、NetBeans™ IDE、jGRASP™ IDE、DrJava IDE、BlueJ IDE 和 TextPad® Text Editor for Windows®。这些 IDE 的免费版本也可以从网络下载。Java IDE Resource Kit 还包括访问 Companion Website 的权限，其中包含逐步的 VideoNotes 和书面说明，帮助你开始使用每个开发环境。如果你的书籍未附带 Java IDE Resource Kit，你可以从 www.pearsonhighered.com/javaidekit/ 购买访问 Resource Kit Companion Website 的权限。你仍需单独下载免费软件。

## Deitel Developer Series 书籍折扣

如果你想接收有关专业 Deitel Developer Series 书籍的信息，包括《Android for Programmers: An App-Driven Approach》，请注册你的《Java How to Program》副本

