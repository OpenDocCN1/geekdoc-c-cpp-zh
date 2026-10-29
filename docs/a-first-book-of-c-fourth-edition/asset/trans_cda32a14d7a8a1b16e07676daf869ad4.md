
# 信息点

## 均质与异质数据结构

列表和对象都是数据结构。**数据结构**是一种以便于插入、检索和删除数据的方式组织数据的容器。这两种数据结构之间的区别在于它们包含的对象类型。列表是**均质**数据结构，这意味着它的所有组成部分必须是相同的数据类型。对象是**异质**数据结构，这意味着它的组成部分可以是不同的数据类型。

例如，一个对象可以包含一个以字符串数据类型存储的名称、以双精度数据类型存储的薪酬率，以及以整数数据类型存储的 ID 号。因为对象可以由不同的数据类型组成，所以它是一个异质数据结构。然而，保存所有对象的列表是一个均质数据结构，其中每个对象具有相同的异质结构。

类型，它们仍然保留与更高级的 STL 列表类型相同的一般特征。例如，像数组一样，STL 列表可以为空，意味着它当前不包含任何项目。就数组和 STL 列表而言，列表被视为可以容纳零个或多个相同类型项目的容器。因此，STL 列表和数组被称为**容器**和**集合**，这两个术语可以互换使用。列表还必须提供访问每个对象的方式。当列表提供这种数据位置能力时，列表就成为数据结构。在数组中，这种位置能力由数组中每个对象的位置提供；位置是通过使用整数索引值来指定的。

尽管 STL 列表也可以存储内置数据类型，但它们更常用于存储和维护对象。在商业应用中，这些对象通常被称为“记录”。为了使记录的概念更具体，请看一下准备邮件标签时通常使用的数据项：

- Name:
- Street Address:
- City:
- State:
- Zip:

此列表中的每个数据项都是一个单独的实体，称为**数据字段**。合在一起，这些数据字段形成一个称为**记录**的单一单元。虽然邮件列表中可能有成千上万个姓名和地址，但所有邮件标签在形式上都是相同的。记录的一般形式被描述为类的成员数据，而每个记录则表示为要存储在列表中的对象。

在定义了对象的结构之后，需要某种方式将所有对象收集到一个列表中。此外，还需要一种方式来定位、显示、打印和更新列表中的对象。STL 提供了这些功能。

在详细描述特定类型的应用之前，值得强调的是，只有对象——而不是类的成员方法——才存储在列表中。方法适用于整个类，只是提供在对象放入列表之前初始化每个对象，以及在对象插入列表之前或从列表中提取之后报告和修改对象的方式。图 13.1 显示了创建和使用对象和列表的过程。

![](img/202cface8244f523c2641baa2e00d7dd_595_0.png)

### Figure 13.1 The list creation process

每个 STL 类都提供自己的一组用于列表维护的方法。此外，STL 还提供了一组通用方法（称为算法），可以应用于存储在任何 STL 创建的列表中的任何对象范围。表 13.2 列出了这些算法。

### Table 13.2 Commonly Used STL Algorithms

| Algorithm Name | Description |
|---|---|
| `accumulate` | Returns the sum of the numbers in a specified range. |
| `binary_search` | Returns a Boolean value of true if the specified value exists within the specified range; otherwise, returns false. Can be used only on a sorted set of values. |
| `copy` | Copies objects from a source range to a destination range. |
| `copy_backward` | Copies objects from a source range to a destination range in a reverse direction. |
| `count` | Returns the number of objects in a specified range that match a specified value. |
| `equal` | Compares the objects in one range of objects, object by object, to the objects in a second range. |
| `fill` | Assigns every object in a specified range to a specified value. |

### Table 13.2 Commonly Used STL Algorithms (continued)

| Algorithm Name | Description |
|---|---|
| find | Returns the position of an object's first occurrence in a specified range having a specified value if the value exists. Performs a linear search, starting with the first object in a specified range, and proceeds one object at a time until the complete range has been searched or the specified object has been found. |
| max_object | Returns the maximum value of objects in the specified range. |
| min_object | Returns the minimum value of objects in the specified range. |
| random_shuffle | Randomly shuffles object values in a specified range. |
| remove | Removes a specified value in a specified range without changing the order of the remaining objects. |
| replace | Replaces each object in a specified range having a specified value with a newly specified value. |
| reverse | Reverses objects in a specified range. |
| search | Finds the first occurrence of a specified value or sequence of values within a specified range. |
| sort | Sorts objects in a specified range into ascending order. |
| swap | Exchanges object values between two objects. |
| unique | Removes duplicate adjacent objects in a specified range. |

最后，STL 提供了额外的组件，称为迭代器，用于指定访问列表对象的方式，与索引为数组提供的方式类似。

要创建和使用 STL 列表，你必须执行以下操作：

- 1. Select a suitable STL class to construct the container type.
- 2. Store objects in the list.
- 3. Apply the STL class's methods or the more general STL algorithms to the stored objects.

你在以下各节中将把这些步骤付诸实践，在其中构建三种常用的列表：链表、栈和队列。

![](img/202cface8244f523c2641baa2e00d7dd_596_0.png)

## EXERCISES 13.1

- 1. (Review) Define the following terms:
  - a. Container
  - b. Collection
  - c. Data structure
  - d. Iterator
  - e. List
  - f. Standard Template Library

2. (Review) What sequential container types are supported in the STL?

3. (Review) What associative container types are supported in the STL?

4. (Practice) For each of the following, define a class containing only a class declaration section that can be used to create the following objects:

- a. An object (known as a student record) containing a student ID number, the number of credits completed, and a cumulative grade point average
- b. An object (known as a student record) capable of holding a student's name, date of birth, number of credits completed, and cumulative grade point average
- c. A mailing list containing a title field, last name field, first name field, two street address fields, a city field, a state field, and a zip code field
- d. A stock object containing the stock's name, the purchase price, and the date of purchase
- e. An inventory object containing an integer part number, a string part description, an integer number of parts in inventory, and an integer reorder value

5. (Practice) For each class declared in Exercise 4, add a suitable constructor and accessor method. Test each method to initialize and display the following data:

- a. ID Number: 4672
  - Number of Credits Completed: 68
  - Grade Point Average: 3.01
- b. Name: Rhona Karp
  - Date of Birth: 8/4/60
  - Number of Credits Completed: 96
  - Grade Point Average: 3.89
- c. Title: Dr.
  - Last Name: Kingsley
  - First Name: Kay
  - Address 1: Apt. 2B
  - Address 2: 614 Freeman Street
  - City: Indianapolis
  - State: IN
  - Zip Code: 07030
- d. Stock: IBM
  - Purchase Price: 134.5
  - Date Purchased: 10/1/2010
- e. Part Number: 16879
  - Description: Battery
  - Number in Stock: 10
  - Reorder Number: 3

6. (Program) a. Write a C++ program that prompts a user to input the current month, day, and year. Store the data entered in a suitably defined object and display the date in an appropriate manner.

b. Modify the program written in Exercise 6a to use an object that accepts the current time in hours, minutes, and seconds.

