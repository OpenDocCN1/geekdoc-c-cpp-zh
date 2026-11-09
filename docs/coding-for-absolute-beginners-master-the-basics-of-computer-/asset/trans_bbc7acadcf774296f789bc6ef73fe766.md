
## UNION 运算符

要合并两个或多个 SELECT 语句的结果，可使用 UNION 运算符；此时每一列都必须具有相似的数据类型。此外，两个表中 SELECT 语句里的列顺序应保持一致。在 SQL 中实现 UNION 运算符的语法定义如下：

```sql
SELECT column_name FROM table1
UNION
SELECT column_name FROM table2;
```

## GROUP BY

SQL 的 GROUP BY 语句可用于从数据库表中执行列出或编号操作。在 SQL 中使用 GROUP BY 语句的语法定义如下：

```sql
SELECT column_name
FROM table_name
WHERE condition
GROUP BY column_name
ORDER BY column_name;
```

## ORDER BY

SQL 中的 ORDER BY 语句用于按升序或降序对数据排序。实现 ORDER BY 子句的语法定义如下：

```sql
SELECT column_list
FROM table_name
WHERE condition
[ORDER BY column1, column2] [ASC | DESC];
```

## 高级 SQL

还有一些其他重要操作和子句可用于在数据库内执行复杂操作。以下详细说明高级 SQL 的一些关键特性：

### 索引

SQL 索引被数据库搜索引擎用于优化数据处理过程。由于索引被视为特殊的查找表，因此索引有助于加速 WHERE 子句和 SELECT 查询。要创建索引，我们可以使用 CREATE INDEX 语句以及 UNIQUE 约束来防止重复条目。

使用 CREATE INDEX 的语法：

```sql
CREATE INDEX index_name ON table_name;
```

使用 DROP INDEX 的语法：

```sql
DROP INDEX index_name;
```

### 截断表

SQL 中的 TRUNCATE TABLE 命令用于从现有表中删除全部数据。

基本语法：

```sql
TRUNCATE TABLE table_name;
```

### SQL 主键与外键

#### 主键

SQL 中的 PRIMARY KEY 约束用于唯一标识表中的每条记录。主键应始终包含唯一值，且不得有任何 NULL 值。此外，一个表只能有一个唯一的主键，该主键可以由单列或多列组成。

例如，在创建“Students”表时要在 ID 列上定义 PRIMARY KEY，我们可以使用以下 SQL 语句：

```sql
CREATE TABLE Students (
    ID int NOT NULL,
    FirstName varchar(255),
    LastName varchar(255) NOT NULL,
    Marks int,
    PRIMARY KEY (ID)
);
```

#### 外键

SQL 中的 FOREIGN KEY 约束用于将两个表链接在一起，其中一个表中的 FOREIGN KEY 引用另一个表中的 PRIMARY KEY。

在“StudentID”列上实现 FOREIGN KEY 约束以创建“Student”表的语法：

```sql
CREATE TABLE Student (
    StudentID int NOT NULL,
    StudentMarks int NOT NULL,
    ClassID int,
    PRIMARY KEY (StudentID),
    FOREIGN KEY (ClassID) REFERENCES Students(StudentID)
);
```

### 约束与有用资源

约束是应用于表数据列的特定规则。通常，约束用于限制可以插入表中的数据类型。最常见的是，这包括 NOT NULL 约束、DEFAULT 约束、UNIQUE 约束、PRIMARY KEY、FOREIGN KEY、CHECK 约束和 INDEX。

此外，完整性约束还可用于提高关系数据库中数据的一致性和准确性。通常，PRIMARY KEY、FOREIGN KEY 和 UNIQUE 约束是参照完整性（RI）的一部分。

为了提高 SQL 数据库的性能，有几个重要因素可以轻松实施。在编写列名时，建议使用 SELECT 语句，而不是 * 分隔符。

例如：

```sql
SELECT * FROM Students
```

此外，设置 NOCOUNT ON 语句将减少 SQL Server 为 INSERT、DELETE 或 UPDATE 操作更新行所需的时间。

![](img/9d932bec53e523b8d8b7b8134cf77ca7_49_0.png)

## 第四章

### C

C 编程语言于 1972 年在美国 AT&T 的贝尔实验室开发。通常，编程语言分为两大类，称为高级语言和低级语言，但 C 被归类为中级语言。该语言的目的是提供对内存的低级访问，并且还为其他主要编程语言（如 PHP 和 Java）提供了语法基础。

### 简介与简单程序

作为一种结构化语言，程序员可以创建分区的代码块，并通过实施不同的方法和编程技术来创建业务应用程序。此外，在 C 库中，我们还可以编写新函数，并在整个应用程序中重复使用它们。

### 开始 C 编程

编写 C 程序对初学者来说简单易行。从基本的程序语法开始，我们可以如下开发 C 应用程序和程序：

```c
#include <stdio.h>
int main()
{
    int a = 2;
    printf("%d", a);
    return 0;
}
```

### 头文件

编写 C 程序的第一部分是选择头文件。通常，头文件以 .h 为扩展名编写，并且包含函数声明。要包含头文件，我们可以遵循如下语法：

```c
#include <string.h>
```

C 头文件示例：

| 头文件 | 定义 |
|---|---|
| stdio.h | 用于定义输入和输出函数 |
| string.h | 用于字符串处理 |
| stddef.h | 定义有用的类型和宏 |
| stdlib.h | 定义内存分配 |
| stdint.h | 用于定义整数类型 |
| math.h | 用于执行数学函数 |

### 方法与变量声明

编写 C 程序的下一部分是定义方法并声明变量。声明 main 方法的语法是：

```c
int main()
{
```

变量声明的语法是：

```c
int main()
{
    int z;
}
```

### 程序主体

```c
int main()
{
    int z;
    printf("%d", z);
    return 0;
}
```

要终止程序，我们可以使用 return 语句：return 0。

### 关键字

关键字是任何编程语言的主要驱动力，也称为保留字。尽管高级编程语言有许多关键字，但 C 中只允许使用 32 个关键字，如下所示：

| double | long | int | switch |
| case | register | enum | typedef |
| union | extern | const | for |
| do | while | static | default |
| auto | break | else | struct |
| float | short | char | return |
| void | continue | for | if |
| signed | goto | sizeof | volatile |

### 数据类型与变量

在 C 编程语言中，数据类型用于定义变量，以便在程序中使用变量之前为其分配存储空间。C 编程语言的内置数据类型包括 float、int、char 和 double。这些数据类型具有称为 short、long、signed 和 unsigned 的修饰符。

以下是 C 编程语言中允许的有效数字、字母和符号：

- **字母：** A-Z, a-z.
- **符号：** ~ \` ! @ # % ^ & * ( ) _ - + = | \\ { } [ ] : ; ' " < > , . ? /
- **数字：** 0, 1, 2, 3, 4, 5, ...

### 变量

要在 C 中声明变量，我们可以遵循如下程序语法：

```c
#include <stdio.h>
// Variable declaration:
extern int a, b;
extern int c;

int main() {

    /* variable definition: */
    int a, b;
    int c;
    float f;

    /* initialization */
    a = 30;
    b = 20;
    c = a + b;
    printf("value of c : %d \n", c);

    return 0;
}
```

该程序的输出为：50。

### 变量的作用域

任何编程语言中变量的作用域都用于授予变量某些权限。通常，变量分为局部变量、全局变量和形式参数。

局部变量在块内声明，并且只能由编写在程序特定区域中的语句使用。由于程序中的其他函数不知道它们，因此我们无法在函数外部访问局部变量。

全局变量通常定义在函数外部，并保留其值
