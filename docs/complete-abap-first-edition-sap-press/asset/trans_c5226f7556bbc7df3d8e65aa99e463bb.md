
```abap
FLDATE TYPE S_DATE,
END OF ty_sflight.
DATA : it_sflight TYPE TABLE OF ty_sflight,
       wa_sflight TYPE ty_sflight.
```

**清单 5.7** 定义内表工作区

**图 5.11** 展示了工作区的用法。由于工作区只能存储一条记录，因此你可以从内表中读取单行，或逐行遍历表的所有行。

要从内表读取单条记录，请使用 READ 语句；要处理多条记录，请使用 LOOP 语句。READ 和 LOOP 语句会将数据从内表复制到工作区。

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_164_0.png)

**图 5.11** 内表与工作区

通过 READ 语句访问内表中的单条记录有几种方式。你可以使用索引（索引访问），也可以通过比较行中一个字段（或一组字段）的值来读取表（键访问）。请注意，并非所有内表都支持索引访问，我们将在下一节讨论这一点。

**清单 5.8** 展示了使用索引访问读取内表的示例代码。

```abap
TYPES : BEGIN OF ty_sflight.
         CARRID TYPE S_CARRID,
         CONNID TYPE S_CONN_ID,
         FLDATE TYPE S_DATE,
       END OF ty_sflight.
DATA : it_sflight TYPE TABLE OF ty_sflight,
       wa_sflight TYPE ty_sflight.

SELECT carrid connid fldate FROM sflight INTO TABLE it_sflight.

*Reading a single record from the internal table into work area
*using index access
READ TABLE it_sflight INTO wa_sflight INDEX 2.
```

**清单 5.8** 使用索引访问

清单 5.8 使用 DATA 关键字的 TABLE OF 附加项定义结构类型 TY_SFLIGHT 和内表 IT_SFLIGHT。内表 IT_SFLIGHT 的行类型被定义为结构类型 TY_SFLIGHT。我们使用 SELECT 语句将数据库表 SFLIGHT 中的数据提取到内表 IT_SFLIGHT 中。

由于内表可以存储多条记录，系统会将数据库表 SFLIGHT 中的所有记录传输到内表 IT_SFLIGHT 中。SELECT 语句通常应始终使用 WHERE 子句加以限制，但为简单起见，本示例中我们忽略了该规则。你将在第 5.3 节中了解更多关于 Open SQL 语句的内容。

在清单 5.8 中，我们使用 READ 语句从内表读取单条记录，并使用 INDEX 附加项指定索引。在本示例中，内表的第二条记录将被复制到工作区。

要使用键访问读取内表记录，请使用 WITH KEY 附加项，并列出要与值匹配的表组件，使用 = 运算符，如下文示例所示。你可以列出多个组件，以空格分隔：

```abap
READ TABLE it_sflight INTO wa_sflight WITH KEY connid = 'AA'.
```

要逐行处理内表的所有记录，请使用 LOOP 语句：

```abap
LOOP AT it_sflight INTO wa_sflight.

ENDLOOP.
```

我们可以使用索引限制循环仅处理特定记录：

```abap
LOOP AT it_sflight INTO wa_sflight FROM 1 to 5.

ENDLOOP.
```

我们也可以使用键限制循环：

```abap
LOOP AT it_sflight INTO wa_sflight WHERE carrid EQ 'AA'.

ENDLOOP.
```

## 5.2.2 内表的类型

内表由其行类型、表类别和表键定义。我们将在以下小节中逐一介绍这些元素。

### 行类型

行类型定义内表的行（即构成表行的字段）。任何类型都可以用作行类型，例如基本类型、结构化类型、表类型或引用类型。例如，内表可以由字段（称为基本类型）、结构、表类型，甚至引用对象（如 ABAP 类）组成。

### 表类别

在 ABAP 程序中可以定义三种类型的内表：标准表、排序表和哈希表。表类别根据单行的访问方式定义内表的类型。

在以下小节中，我们将仔细了解可以定义的不同表类别类型。

### 标准表

*标准表*使用行索引进行管理。对于添加到内表的每条记录，系统都会创建一个线性索引。新行可以使用 `APPEND` 关键字追加到表的末尾（例如 `APPEND wa_sflight TO it_sflight`），或使用 `INSERT` 关键字插入到特定位置（例如 `INSERT wa_sflight INTO it_sflight INDEX 3`）。单行通过表键或行索引访问；标准表同时支持键访问和索引访问。

在声明表时，你不必显式指定主表键。标准表的主键可以为空。标准表仅支持非唯一主键，这意味着同一表中的多行可以具有相同的键值。

当在 `READ` 语句中使用 `TABLE KEY` 附加项时，系统会执行线性搜索以识别匹配行。

声明标准表的语法如下：

```abap
DATA internaltable_name TYPE TABLE OF [or STANDARD TABLE OF] structure_reference
```

TYPE TABLE OF 和 TYPE STANDARD TABLE OF 附加项都定义标准表。`internaltable_name` 是内表的名称，`structure_reference` 是对结构类型的引用。

在以下语句中

```abap
DATA it_sflight TYPE TABLE OF ty_sflight.
```

内表 IT_SFLIGHT 被定义为行类型为 TY_SFLIGHT 的标准表。这里，TY_SFLIGHT 是结构类型。TABLE OF 附加项是定义标准表的简写形式。我们也可以使用长形式 STANDARD TABLE OF 来定义标准表，如下所示：

```abap
DATA it_sflight TYPE STANDARD TABLE OF ty_sflight.
```

### 排序表

*排序表*与标准表类似，不同之处在于记录始终按键升序排序。新记录只有在保持排序顺序时才能插入或追加。与标准表一样，排序表也通过行索引进行管理，因此你可以按索引或键读取单行。

排序表同时支持唯一主键和非唯一主键，并且在声明内表时必须定义主键。如果表具有唯一键，则该键不能重复。具有非唯一键的表可以包含多个具有该键的记录。换言之，对于唯一键，不能存在多条键字段值相同的记录。

例如，如果表的键定义为 CARRID 和 CONNID，并且表中包含一条 CARRID 值为 'AA'、CONNID 值为 '0017' 的记录，那么表中不能有第二条 CARRID 和 CONNID 值相同的记录。构成键的各个字段可以重复，但键字段的组合应唯一。因此，我们可以有另一条 CARRID 为 'AA' 的记录，也可以有另一条 CONNID 为 '0017' 的记录，但不能有另一条同时包含 CARRID 为 'AA' 和 CONNID 为 '0017' 的记录。

当你定义具有非唯一键的表时，可以存在多条键值相同的记录，且不受限制。你应根据所处理的数据谨慎选择键，以避免数据不一致。

当在 READ 语句中使用 TABLE KEY 附加项时，系统会执行二分查找以识别匹配行。

声明排序表的语法如下：

```abap
DATA internaltable_name TYPE SORTED TABLE OF structure_reference WITH UNIQUE [or NON-UNIQUE] KEY key_fields.
```

要定义排序表，请使用 SORTED TABLE OF 附加项。在声明期间必须定义表的键。使用 WITH UNIQUE KEY 或 WITH NON-UNIQUE KEY 附加项分别定义唯一键或非唯一键。排序表的键可以由单个字段或多个字段组成。如果键包含多个字段，则每个字段列在 WITH UNIQUE（或 NON-UNIQUE）KEY 附加项之后，以空格分隔。

例如，以下语句定义了一个排序表 IT_SFLIGHT，其行类型为 TY_SFLIGHT，由唯一键 CARRID 和 CONNID 组成（假设 CARRID 和 CONNID 是结构类型 TY_SFLIGHT 的组件）：

```abap
DATA it_sflight TYPE SORTED TABLE OF ty_sflight WITH UNIQUE KEY carrid connid.
```

此外，以下语句定义了一个具有非唯一键 CARRID 和 CONNID 的排序表 IT_SFLIGHT：

```abap
DATA it_sflight TYPE SORTED TABLE OF ty_sflight WITH NON-UNIQUE KEY carrid connid.
```

### 哈希表

与标准表和排序表不同，哈希表没有行索引。它们使用哈希算法进行管理。由于没有行索引，因此不能执行任何索引操作，只能按键读取单行。哈希表仅支持唯一键，并且在声明内表时必须定义键。

当在 READ 语句中使用 TABLE KEY 附加项时，系统不会手动比较键字段的内容来识别匹配行。相反，系统使用哈希函数来识别匹配行。
