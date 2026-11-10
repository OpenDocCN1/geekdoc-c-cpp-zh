
在**第 5.1 节**中，我们将了解定义和使用结构的各种方式。结构数据对象仅由一行组成，这意味着它只能存储一行数据。当你在结构中存储新记录时，它会替换现有记录。要处理多行数据，我们需要使用内表。我们将在**第 5.2 节**中讨论内表。

结构和内表主要用于处理来自数据库表的数据；此类数据通过 Open SQL 语句访问。你将在**第 5.3 节**中进一步了解关系数据库，并了解不同的 Open SQL 语句。然后我们将在**第 5.4 节**中了解如何使用结构和内表处理来自数据库表的数据。

程序出现难以在语法检查期间静态检测到的逻辑问题是很常见的，尤其对初学者而言。我们将在**第 5.5 节**中讨论*调试*，帮助你熟悉调试工具，以便修复程序中的任何逻辑问题。调试还有助于你更好地理解程序执行，我们鼓励你调试在本书学习过程中创建的所有程序。

我们将在**第 5.6 节**中以一个练习结束本章，该练习将巩固本章讨论的概念。

## 5.1 定义结构

结构可以是局部的或全局的。局部和全局都有多种定义，我们将在后面介绍。根据上下文，术语*局部*可能表示几种含义；如果我们讨论的是程序，局部可能指属于程序中特定过程的对象（数据对象或数据类型）。这些对象将在定义它们的过程内可见。在此上下文中，*全局*对象是在整个程序中可见的对象；它可以从程序中的任何过程或处理块访问。可见性表示数据对象或数据类型是否可以从程序代码中的特定位置访问。

例如，如**代码清单 5.1**所示，你可以访问数据类型 `ty_sflight` 和数据对象 `ls_sflight`，但只能在子例程 `data` 内访问。尝试从同一程序的另一个过程（示例中的子例程 `output`）访问它们将导致语法错误，因为这些对象不可见。

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_153_0.png)

**图 5.2** 不同的结构类型

### 5.1.1 何时定义结构

我们使用结构来处理顺序数据，例如存储在数据库表或顺序文件的行和列中的数据。数据对象允许你将来自外部源（例如数据库表或顺序文件）的数据导入 ABAP 程序，这必须发生在 ABAP 语句可以访问同一数据之前（见图 5.3）。

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_153_1.png)

**图 5.3** ABAP 程序中的数据处理

因此，你需要单个变量还是包含多个字段的结构，取决于你在 ABAP 程序中导入或处理的数据。如果你要处理一行中的多个字段或完整的一行数据，请在程序中定义结构。如果你要处理单个字段或一行中的仅一个字段，请在程序中定义单个字段。

### 5.1.2 局部结构

让我们以表 `SFLIGHT` 为例，了解在 ABAP 程序中定义结构的各种方式。一旦你理解了如何定义结构，就应该能够运用它们来处理来自数据库表的数据。

[图 5.4](#figure-5-4) 显示了表 `SFLIGHT` 的字段。

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_154_0.png)

**图 5.4** 表 SFLIGHT 的字段

图 5.5 显示了数据浏览器工具中的表数据。要打开该表，请进入事务码 SE11，选择 DATABASE TABLE 单选按钮，输入表名，然后单击 DISPLAY。

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_155_0.png)

图 5.5 在数据浏览器视图中以列表示的表字段

代码清单 5.2 使用 TYPES 关键字定义了一个结构数据类型。该结构包含来自表 SFLIGHT 的三个字段。当你想要处理表中某些字段的数据时，使用数据库表中的特定字段定义结构很有用。结构的所有字段都应具有与数据库表对应字段相同的技术属性。

为确保这一点，请将程序中结构的组件指向与数据库表中对应字段相同的数据元素——例如，CARRID TYPE S_CARR_ID。

这里，S_CARR_ID 是表 SFLIGHT 的 CARRID 字段所引用的数据元素。你也可以通过使用表引用将结构的组件指向表字段——例如，CARRID TYPE SFLIGHT-CARRID。将字段引用到数据元素或表字段还可确保对数据元素或表字段定义的任何更改都会自动反映到程序中。

在代码清单 5.2 中，我们使用 `TYPES` 关键字定义了结构类型 `TY_SFLIGHT`，并将 `CARRID`、`CONNID` 和 `FLDATE` 作为组件。我们将结构类型的组件引用到各自的数据元素。我们还使用 `DATA` 关键字定义了结构 `ST_FLIGHT`，并引用结构类型 `TY_SFLIGHT`。展示结构类型 `TY_SFLIGHT1` 声明的示例使用基本类型来为结构类型的组件指定类型。

```text
*Notice the chain operator colon(:) after the TYPES keyword.
*without which you will have to use the keyword at the beginning
*of each line and end each line with a period.
```

```abap
TYPES : BEGIN OF ty_sflight,
        CARRID TYPE S_CARR_ID,
        CONNID TYPE S_CONN_ID,
        FLDATE TYPE S_DATE,
        END OF ty_sflight.
```

```text
*Since the TYPES keyword created a data type, you can define a
*data object referring to this structure as below.
```

```abap
DATA st_sflight TYPE ty_sflight.
```

```text
*The same structure type can also be declared while referring the
*fields to elementary types. Note that the type and length of
*each field matches the fields in the table. Matching the type
*and length is very important when using elementary types.
```

```abap
TYPES : BEGIN OF ty_sflight1,
        CARRID TYPE C LENGTH 3,
        CONNID TYPE N LENGTH 4,
        FLDATE TYPE D,
        END OF ty_sflight1.
```

**代码清单 5.2** 使用字段集定义结构类型

下面展示了如何定义与 ABAP 数据字典表匹配的结构类型：

```abap
TYPES : ty_sflight TYPE sflight.
```

要定义包含表中所有字段的结构类型，你只需将结构类型引用到该表。在此示例中，`ty_sflight` 将包含 ABAP 数据字典表 `SFLIGHT` 的全部 14 个字段。

[代码清单 5.3](#) 展示了定义嵌套结构的示例。

```abap
* Defining nested structure type
TYPES : ty_sflight TYPE sflight.
TYPES : BEGIN OF ty_trip,
        name TYPE name1,
        flight TYPE ty_sflight,
      END OF ty_trip.
```

**代码清单 5.3** 嵌套结构类型

在代码清单 5.3 中，我们定义了引用透明表 `SFLIGHT` 的结构类型 `TY_SFLIGHT`。我们还定义了一个嵌套结构类型 `TY_TRIP`，它由组件 `NAME` 和结构类型 `FLIGHT` 组成。

代码清单 5.4 展示了使用 `DATA` 关键字将结构定义为数据对象的示例。其语法与 `TYPES` 关键字类似。

```abap
*To define a structure as a data object, simply use the
*DATA keyword instead of the TYPES keyword.
DATA : BEGIN OF st_sflight,
             CARRID TYPE S_CARR_ID,
             CONNID TYPE S_CONN_ID,
             FLDATE TYPE S_DATE,
         END OF st_sflight.
*You can also create a structure by referring to the
*database table to match the table row type.
DATA st_sflight1 TYPE sflight.
```

**代码清单 5.4** 将数据对象定义为结构

在代码清单 5.4 中，结构 `ST_SFLIGHT` 由三个组件 `CARRID`、`CONNID` 和 `FLDATE` 组成，而结构 `ST_SFLIGHT1` 包含 ABAP 数据字典表 `SFLIGHT` 的所有字段。

### 5.1.3 全局结构

结构类型可以全局定义，以使其跨程序可见。全局结构类型也用于定义功能模块或方法的参数接口，还可用于定义常规屏幕的屏幕元素。你将在第 7 章进一步了解功能模块和方法，并在第 12 章进一步了解屏幕编程。

全局结构类型在 ABAP 数据字典（事务码 SE11）中创建。按照以下步骤创建全局结构：

- 1. 进入事务码 SE11。
- 2. 在 ABAP 数据字典初始屏幕上选择 DATA TYPE 单选按钮。输入结构名称。名称应位于客户命名空间中，并以 Y 或 Z 开头。单击 CREATE 按钮（图 5.6）。

