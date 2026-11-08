

#### 1.5.2 传递效率

使用 PROC SQL 创建数据库特定代码并将其传递到 SAS 以外的数据库（如 Oracle 或 DB2）时，务必注意如何处理特定问题的编程方式。根据编码方式的不同，SQL 可能非常高效，也可能非常低效，而当您使用传递技术创建数据子集时，这一点可能更加重要。

从服务器传回信息通常比在服务器上处理更慢。设计传递时应尽量减少返回的信息量。通常，主数据库会存储在具有最大处理能力的位置。请充分利用这种能力。至少，减少需要传回给您的信息量将有助于节省带宽。

在 SQL 中，数据集在内存中处理。这意味着大型数据集连接应在可用内存最大的地方执行。当连接受内存限制时，在连接之前对数据进行子集化会有所帮助。请了解并理解您的数据库和操作系统；有些 WHERE 语句形成的子句是应用于连接结果，而非传入数据集。

即使您不打算写入通过 SQL 传递访问的主数据库，也可能会对该数据表进行额外的过程检查。这些检查可能代价高昂，但可以通过将传入数据表指定为只读来消除。这可以通过多种方式实现。在 DB2 中，在传递给数据库的代码中使用 *for fetch only* 子句可消除对传入表的写入检查。在 1.5.1 节的 DB2 传递示例中，我们只想提取或获取数据。我们通过让数据库知道我们不会写入任何数据（仅获取数据）来加快处理速度。

**更多信息**

使用传递代码的 SQL 步骤可在第 5.4.2 节中找到。

### 1.6 读写 XML

可扩展标记语言（XML）具有层次结构，而 SAS 数据集基于记录或观测。由于 XML 正迅速成为通用的数据交换格式，SAS 程序员有责任掌握如何在 SAS 与 XML 之间移动信息的工作知识。

XML 引擎（第 1.6.2 节）首次在 SAS 8 版本中引入。后来增加了 ODS XML 目标；但目前已将 XML 目标的功能内置到 ODS MARKUP 目标中（参见第 1.6.1 节）。

由于 XML 基于文本，每一行都包含自己的元数据，因此文件本身可能相当大。

**另请参阅**

可在（Pratter, 2008）中找到关于 XML 及其与 SAS 关系的非常好的概述。其他关于 XML 与 SAS 关系的入门讨论包括：Chapal (2003)、Palmer (2003 和 2004)，以及 SAS 文档中关于“XML Engine with DATA Step or PROC COPY”的部分。

#### 1.6.1 使用 ODS

您可以使用 ODS MARKUP 目标创建 XML 文件。该文件可以包含 XML 格式的过程输出，然后可以将此 XML 文件传递给另一个使用/读取 XML 的应用程序。默认情况下，MARKUP 目标会创建一个 XML 文件。

```sas
title1 '1.6.1 Using ODS MARKUP';
ods markup file="&path\\data\\E1_6_1Names.xml"; ❶

* create a xml file of the report; ❷
proc print data=advrpt.demog;
    var lname fname sex dob;
    run;
ods markup close; ❸
```

- ❶ FILE= 选项用于指定要创建的文件的名称。注意使用了 XML 扩展名。

- ❷ 该过程必须位于 ODS“三明治”内部。

- ❸ 必须关闭该目标后，文件 ❶ 才能在 SAS 外部使用。

**更多信息**

如果您计划与 XML 文件一起使用的应用程序是 Excel，则 EXCELXP 标签集是更优选择（参见第 11.2 节）。

**另请参阅**

LinkedIn 线程 [http://www.linkedin.com/groupItem?view=&srchtype=discussedNews&gid=70702&item=74453221&type=member&trk=eml-anet_dig-b_pdt-ttl-cn&ut=34c4-PQjofGK1](http://www.linkedin.com/groupItem?view=&srchtype=discussedNews&gid=70702&item=74453221&type=member&trk=eml-anet_dig-b_pdt-ttl-cn&ut=34c4-PQjofGK1) 中讨论了使用 ODS 生成 XML 的内容。

#### 1.6.2 使用 XML 引擎

使用 XML 引擎的过程与第 1.6.1 节中所示的过程类似，可用于写入 XML 格式。XML 是一种标记语言，XML 代码存储在文本文件中，SAS 既可以读取也可以写入该文本文件。如上面的示例所示，在 LIBNAME 语句上使用引擎来与执行转换的 SAS 建立链接。建立 fileref 并在 LIBNAME 语句中使用它。

```sas
filename xmlmst "&path\\data\\E1_6_2list.xml";
libname toxml xml xmlfileref=xmlmst; ❶

* create a xml file (E1_6_2list.xml);
data toxml.patlist; ❷
    set advrpt.demog(keep=lname fname sex dob);
    run;

* convert xml to sas;
data fromxml;
    set toxml.patlist; ❸
    run;
```

- ❶ 在包含 XML 引擎的 LIBNAME 语句上，XMLFILEREF= 选项用于指向包含 XML 文件的 fileref，或者如本例所示，指向要写入的文件。

```xml
<?xml version="1.0" encoding="windows-1252" ?>
<TABLE>
  <PATLIST> ③
    <lname>Adams</lname>
    <fname>Mary</fname>
    <sex>F</sex>
    <dob>1951-08-12</dob>
  </PATLIST>
  <PATLIST>
    <lname>Adamson</lname>
    <fname>Joan</fname>
    <sex>F</sex>
    <dob missing="." />
  </PATLIST>
    . . . the remaining observations are not shown . . . .
```

- ② **libref** TOXML 可用于读取和写入 XML 文件。数据集的名称（PATLIST）作为 XML 文件的一部分被记录 ③。这意味着可以将多个 SAS 数据集写入同一个 XML 文件。

所选变量会写入 XML 文件。请注意，每个变量都在各自行上命名，日期已重新编码为 YYYY-MM-DD 格式，并且“Joan Adamson”缺失的 DOB 已使用 `missing=` 表示法写入。

**另请参阅**

Hemendinger 和 Slaughter (2011) 简要描述了 XML 和 XML Mapper 的使用。

![](img/4b16455363806a3241267bf9f49ba5d1_65_0.png)

## 第 2 章：处理您的数据

- **2.1 数据集选项** 38
    - 2.1.1 REPLACE 和 REEMPT 40
    - 2.1.2 密码保护 41
    - 2.1.3 KEEP、DROP 和 RENAME 选项 42
    - 2.1.4 使用 FIRSTOBS 和 OBS 数据集选项进行观测控制 43
- **2.2 计算表达式** 45
    - 2.2.1 运算符层次结构 45
    - 2.2.2 使用冒号作为比较修饰符 46
    - 2.2.3 赋值语句中的逻辑和比较运算符 47
    - 2.2.4 复合不等式 49
    - 2.2.5 MIN 和 MAX 运算符 50
    - 2.2.6 数值表达式和布尔变换 51
- **2.3 数据验证和异常报告** 52
    - 2.3.1 数据验证 52
    - 2.3.2 写入错误数据集 55
    - 2.3.3 使用宏控制异常报告 58
- **2.4 规范化——转置数据** 60
    - 2.4.1 使用 PROC TRANSPOSE 61
    - 2.4.2 在 DATA 步骤中转置 63
- **2.5 填充稀疏数据** 65
    - 2.5.1 已知行模板 65
    - 2.5.2 双重转置 67
    - 2.5.3 将 COMPLETETYPES 与 PROC MEANS 或 PROC SUMMARY 一起使用 70
    - 2.5.4 使用 CLASSDATA 70
    - 2.5.5 使用预加载格式 72
    - 2.5.6 将 SPARSE 选项与 PROC FREQ 一起使用 73
- **2.6 一些一般概念** 73
    - 2.6.1 变量名称简写 73
    - 2.6.2 理解 ORDER= 选项 77
    - 2.6.3 引号中的引号中的引号 79
    - 2.6.4 设置数值变量的长度 81
- **2.7 WHERE 详情** 82
    - 2.7.1 仅用于 WHERE 的运算符 83
    - 2.7.2 与 BY 语句的交互 86
- **2.8 追加数据集** 88
    - 2.8.1 使用 DATA 步骤和 SQL UNION 追加数据集 88
    - 2.8.2 使用 DATASETS 过程的 APPEND 语句 90
- **2.9 查找和消除重复项** 90
    - 2.9.1 使用 PROC SORT 91
    - 2.9.2 使用 FIRST. 和 LAST. 进行 BY 组处理 92
    - 2.9.3 使用 PROC SQL 93
    - 2.9.4 使用 PROC FREQ 93
    - 2.9.5 使用数据组件哈希对象 94
- **2.10 处理缺失值** 97
    - 2.10.1 特殊缺失值 97
    - 2.10.2 MISSING 系统选项 98
    - 2.10.3 使用 CMISS、NMISS 和 MISSING 函数 99
    - 2.10.4 使用 CALL MISSING 例程 100
    - 2.10.5 当分类变量缺失时 100
    - 2.10.6 缺失值和更多变量 101
    - 2.10.7 填补缺失值 101

在 SAS 中，数据集是大多数分析和报告的核心。这意味着我们能够了解有关数据的各种信息是至关重要的。我们需要的这种能力来自众多的 SAS 工具和技术。本章是这些工具和技术的集合，虽然内容较为多样，但可以帮助我们实现处理数据集的目标。

### 2.1 数据集选项

数据集选项可用于修改数据集的读取或写入方式。这些选项有三十多种，虽然您通常只会用到其中少数几个，但您应该对它们的范围有很好的了解。

