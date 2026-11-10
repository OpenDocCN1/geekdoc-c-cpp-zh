
```
ASSIGN comp OF STRUCTURE struc TO <fs>.
```

通过此语句，`struc` 结构的 `comp` 组件被分配给 `<fs>` 字段符号。如果 `comp` 数据对象被设置为 `TYPE c` 或 `TYPE string`，则 `comp` 字段的内容会被解释为组件名称。例如，在代码清单 16.11 中，`st_mara` 结构的 `matnr` 字段将被分配给该字段符号。

```abap
DATA: st_mara TYPE mara,
      l_field TYPE string VALUE 'MATNR'.
FIELD-SYMBOLS: <fs_any> TYPE any.
ASSIGN l_field OF STRUCTURE st_mara TO <fs_any>.
```

**代码清单 16.11** 为结构字段赋值

但是，如果 `comp` 数据对象属于不同类型并且包含数字，则系统会将其解释为字段位置，并将该字段分配给字段符号。

例如，在代码清单 16.12 中，`st_mara` 结构的第三个字段 `mtart` 将被分配给该字段符号，因为 `l_field` 数据对象包含值 3。

```abap
TYPES: BEGIN OF ty_mara,
         matnr TYPE matnr,
         ersda TYPE ersda,
         mtart TYPE mtart,
       END OF ty_mara.
DATA: st_mara TYPE ty_mara,
      l_field TYPE n VALUE 3.
FIELD-SYMBOLS: <fs_any> TYPE any.
ASSIGN l_field OF STRUCTURE st_mara TO <fs_any>.
```

**代码清单 16.12** 基于字段位置的动态分配

处理内表时，可以将字段符号用作工作区。使用 `LOOP` 或 `READ` 语句的 `ASSIGNING` 附加项，将内表记录分配给字段符号，如代码清单 16.13 所示。

```abap
READ TABLE itab ASSIGNING <fs>...
LOOP AT itab ASSIGNING <fs>.
ENDLOOP.
```

**代码清单 16.13** 使用 ASSIGNING 附加项

当使用 `LOOP` 或 `READ` 语句将内表记录分配给字段符号时，字段符号将直接指向表中被分配的行。

例如，在代码清单 16.14 中，我们将内表 `IT_MARA` 的第一行分配给 `<FS_MARA>` 字段符号。

在此分配之后，字段符号将指向内表的第一行，你可以直接使用字段符号更改该行中的任何字段。

在此示例中，`<FS_MARA>-MTART = 'ROH'` 语句将更改内表第一行中 `MTART` 字段的值。与工作区不同，使用字段符号时，不需要使用 `MODIFY` 语句将工作区的内容复制回内表。

```abap
TYPES: BEGIN OF ty_mara,
         matnr TYPE matnr,
         ersda TYPE ersda,
         mtart TYPE mtart,
       END OF ty_mara.
DATA: it_mara TYPE TABLE OF ty_mara.
FIELD-SYMBOLS: <fs_mara> LIKE LINE OF it_mara.
PARAMETERS p_matnr TYPE matnr.
SELECT matnr ersda mtart FROM mara INTO TABLE it_mara
       WHERE matnr EQ p_matnr.
READ TABLE it_mara ASSIGNING <fs_mara> INDEX 1.
IF <fs_mara> IS ASSIGNED.
  <fs_mara>-mtart = 'ROH'.
ENDIF.
```

**代码清单 16.14** 将内表记录分配给字段符号

### 16.1.4 检查字段符号是否已分配

当数据对象被分配给字段符号时，`SY-SUBRC` 系统字段被设置为 0。如果要在分配后立即检查，可以检查 `SY-SUBRC` 字段，如代码清单 16.15 所示。

```abap
ASSIGN dobj TO <fs>.
IF sy-subrc IS INITIAL.
  <fs> = 123.
ENDIF.
```

**代码清单 16.15** 检查 SY-SUBRC 字段

但是，在大多数情况下，你不需要在分配后立即访问字段符号，而可能需要在代码后面访问它。在这种情况下，检查 `SY-SUBRC` 系统字段没有用，因为 `SY-SUBRC` 会被许多语句更新，并且它始终包含最后一次更新它的语句的结果。

为了确保在访问字段符号之前它已分配，请使用以下语法的 `IS ASSIGNED` 语句：

```abap
IF <fs> IS ASSIGNED.
ENDIF.
```

我们建议你始终在访问字段符号之前检查它是否已分配。尝试访问未分配的字段符号将导致不可处理的异常。

### 16.1.5 取消分配字段符号

如果要移除字段符号的分配以确保没有数据对象分配给它，请按如下方式使用 `UNASSIGN` 语句：

```abap
UNASSIGN <fs>.
```

字段符号取消分配后将被初始化，因此不会指向任何数据对象。除非另一个数据对象分配给该字段符号，否则不应在取消分配后访问该字段符号。

使用 `CLEAR` 语句不会初始化字段符号；它只会清除分配给字段符号的数据对象的内容。

### 16.1.6 强制转换

当数据对象被分配给字段符号时，字段符号的类型应与数据对象兼容。但是，当数据对象被分配给字段符号时，你可以对任何数据类型执行强制转换。

强制转换允许你将特定数据类型视为另一种数据类型。这意味着任何内存区域都可以被视为已采用给定类型。例如，当通过执行强制转换将数据对象分配给字段符号时，你可以将字符字段的值解释为日期。

`CASTING` 用于执行强制转换，如下所示：

```abap
ASSIGN dobj TO <fs> CASTING.
```

使用 `CASTING` 时，可以将不同类型的数据对象分配给字段符号。强制转换允许你将与字段符号不兼容的数据对象分配给字段符号。

代码清单 16.16 显示了示例代码，其中类型为 `C` 的字段被分配给类型为 `D` 的字段符号。数据对象分配后，其内容将被解释为类型 `D`。

```abap
DATA text(8) TYPE c VALUE '20111201'.
FIELD-SYMBOLS <fs> TYPE sy-datum.
ASSIGN text TO <fs> CASTING.
WRITE <fs>.
```

**代码清单 16.16** 强制转换

强制转换可以隐式或显式执行。如果字段符号是完全类型化的，或使用内置 ABAP 类型（c、n、p 或 x）之一进行泛型类型化，则 `CASTING` 可与 `ASSIGN` 语句一起使用，该语句执行隐式强制转换，将分配的内存转换为字段符号的类型。

如果字段符号是泛型类型化的，则可以通过在 `ASSIGN` 语句中指定数据类型来执行显式强制转换，如下所示：

```abap
ASSIGN dobj TO <fs> CASTING [TYPE data_type|LIKE dobj].
```

在 `CASTING` 附加项之后，可以指定数据类型或数据对象。强制转换将按指定类型执行。你指定的类型应与字段符号的泛型类型兼容，并且不应对完全类型化的字段符号执行显式类型化。强制转换允许你按类型转换以不同方式解释数据。

本节讨论了字段符号在动态编程中的使用。下一节，我们将了解如何使用数据引用指向内存中的数据对象。

## 16.2 数据引用

与对象引用类似，*数据引用*指向内存中的数据对象。数据引用可以像字段符号一样，用作对现有数据对象的替代访问引用。但是，使用数据引用可以定义匿名数据对象。数据引用存储在数据引用变量中，该变量使用 `DATA` 语句的 `TYPE REF TO` 附加项定义。

现在，我们将解释如何定义和使用数据引用。我们还将讨论如何使用数据引用以及数据引用之间的赋值来动态定义数据对象。

### 16.2.1 定义引用变量

定义数据引用变量的语法如代码清单 16.17 所示。

```abap
DATA dref TYPE REF TO dtype.
DATA dref LIKE REF TO dobj.
DATA dref TYPE REF TO DATA.
```

**代码清单 16.17** 定义数据引用变量

在代码清单 16.17 中，第一条语句使用数据类型引用，第二条语句使用数据对象引用。这些数据引用变量是完全类型化的，可以指向此类型的数据对象。第三条语句定义为泛型类型 `DATA`，可以指向任何数据对象。

与对象引用类似，数据引用可以是静态类型或动态类型。数据引用的静态类型应为完全类型化或完全泛型类型，如代码清单 16.17 所示。动态类型应等于静态类型，或比其静态类型更特殊（不是泛型）。

定义数据引用变量时，它是初始的；换句话说，数据引用变量不指向任何数据对象。应向数据引用变量提供一个数据对象引用。

一旦提供了数据引用，它保存所引用数据对象的内存位置，而不是其内容。要访问所引用数据对象的内容，应使用 `->*` 解引用选择器对引用变量进行解引用。

图 16.3 在调试模式下显示了数据引用变量，以便更好地可视化。如图所示，当访问数据引用变量 `DREF` 时，它持有对 `V_MATNR` 数据对象的引用。要访问 `V_MATNR` 的内容，我们使用 `->*` 选择器对引用变量进行解引用。
