
运行时的数据类型。这些类型类的实例被称为*类型对象*。

对于每个ABAP类型，例如基本类型、引用类型、复杂类型（结构和内表）等，都有一个类型类。

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_685_0.png)

**图 16.4** 类型类层次结构

对于每个ABAP类型，程序中恰好存在一个类型对象，并且我们为新的类型创建新的类型对象。类型对象包含描述该类型的属性。类文档提供了每个类型类的信息。

在接下来的小节中，我们将更详细地讨论RTTI和RTTC。

### 16.3.1 运行时类型信息

通常，您需要动态确定对象的类型信息。例如，在算术运算中使用过程的泛型类型参数或泛型匿名数据对象之前，您可能希望检查其类型、长度和小数位数。在这种情况下，您可以使用类型对象来标识数据对象的类型信息。

类型对象是使用类型类的方法创建的。类型对象的属性包含类型信息。**清单 16.25** 展示了识别类型信息的示例代码。

```abap
REPORT ZDEMO_EXAMPLES.
TYPES: ty_type TYPE p DECIMALS 2.
DATA: v_data TYPE ty_type.
      r_typedescr TYPE REF TO cl_abap_typedescr.
START-OF-SELECTION.
r_typedescr = cl_abap_typedescr=>describe_by_data( v_data ).

WRITE: / 'Kind:',    r_typedescr->type_kind.
WRITE: / 'Length:',  r_typedescr->length.
WRITE: / 'Decimals:', r_typedescr->decimals.
```

### 清单 16.25 查询类型信息

在清单 16.25 中，我们将 R_TYPEDESCR 类型对象定义为类型类 CL_ABAP_TYPEDESCR 的一个实例。当调用该类型类的 DESCRIBE_BY_DATA 静态方法时，类型对象被实例化。我们向此静态方法传递需要获取类型信息的数据对象。

一旦类型对象被实例化并带有类型信息，我们就可以访问其属性来确定数据对象的类型信息。类型对象还包含常量，可以在 IF 或 CASE 结构中使用这些常量来比较 TYPE_KIND 属性。

### 16.3.2 运行时类型创建

如上一节所讨论的，类型对象通过 RTTS 的 RTTI 方法创建；这些类型对象可用于通过 RTTS 的 RTTC 方法创建新类型。RTTC 方法允许您动态创建数据类型，这些数据类型可用于动态定义数据对象。

例如，假设您想动态创建一个结构并立即在 SELECT 语句中使用它。您只有在运行时才知道该结构的字段。在这种情况下，您可以使用 RTTC 方法来定义数据类型，并使用它动态创建数据对象。CL_ABAP_STRUCTDESCR、CL_ABAP_TABLEDESCR 和 CL_ABAP_REFDESCR 类的 GET 工厂方法允许您创建类型对象。

创建类型对象所需的信息将传递给这些类的工厂方法。例如，组件详细信息传递给 CL_ABAP_STRUCTDESCR 类的工厂方法，以创建结构的类型对象。类似地，结构类型对象传递给 CL_ABAP_TABLEDESCR 类的工厂方法，以创建表类型对象。清单 16.26 展示了如何使用 RTTC 方法动态定义数据类型，并使用这些类型创建数据对象。

在清单 16.26 中，我们定义了两个选择屏幕字段，用于接收表名和 `WHERE` 子句作为输入。程序逻辑被构建为显示给定输入的任何表中的数据。

为实现这一点，在 `GET_TABLE` 子例程中，我们动态识别给定结构的类型信息以获取其组件。我们使用这些组件即时构建一个内表，并编写动态 `SELECT` 语句从所请求的表中获取数据。最后，在 `DISPLAY_TABLE` 子例程中使用 ALV 显示输出。

```abap
PARAMETERS: p_table TYPE string.
            p_where TYPE string.

DATA:       r_typedescr TYPE REF TO cl_abap_typedescr,
            r_structdescr TYPE REF TO cl_abap_structdescr,
            r_tabledescr TYPE REF TO cl_abap_tabledescr,
            r_table      TYPE REF TO data,
            components   TYPE cl_abap_structdescr=>component_table,
            component    LIKE LINE OF components,
            ro_alv       TYPE REF TO cl_salv_table.

FIELD-SYMBOLS: <table> TYPE ANY TABLE.
START-OF-SELECTION.
  PERFORM get_table.
  PERFORM display_table.
*&---------------------------------------------------------------------*
*&      Form  GET_TABLE
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
FORM get_table.
  r_typedescr = cl_abap_typedescr=>describe_by_name( p_table ).
  TRY.
      r_structdescr ?= r_typedescr.
    CATCH cx_sy_move_cast_error.
  ENDTRY.
  components = r_structdescr->get_components( ).
  TRY.
      r_structdescr = cl_abap_structdescr=>get( components ).
      r_tabledescr = cl_abap_tabledescr=>get( r_structdescr ).
    CATCH cx_sy_struct_creation.
    CATCH cx_sy_table_creation.
  ENDTRY.
  TRY.
      CREATE DATA r_table TYPE HANDLE r_tabledescr.
      ASSIGN r_table->* TO <table>.
    CATCH cx_sy_create_data_error.
  ENDTRY.
  TRY.
      SELECT *
        FROM (p_table)
        INTO CORRESPONDING FIELDS OF TABLE <table> WHERE (p_where).
    CATCH cx_sy_sql_error.
  ENDTRY.
ENDFORM.
*&---------------------------------------------------------------------*
*&      Form  DISPLAY_TABLE
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
FORM display_table.
  TRY.
      CALL METHOD cl_salv_table=>factory
        IMPORTING
          r_salv_table = ro_alv
        CHANGING
          t_table      = <table>.
    CATCH cx_salv_msg.
  ENDTRY.
  ro_alv->display( ).
ENDFORM.
```

### 清单 16.26 动态类型创建

在清单 16.26 的 `GET_TABLE` 子例程中，我们首先根据在选择屏幕上输入的表名创建 `R_TYPEDESCR` 类型对象。我们将 `R_TYPEDESCR` 类型对象向下转换为 `R_STRUCTDESCR`。`R_STRUCTDESCR` 类型对象是 `CL_ABAP_STRUCTDESCR` 类的一个实例，该类包含用于创建新类型对象的 RTTC 方法。

我们调用 `GET_COMPONENTS` 方法来获取结构的组件。利用这些信息，我们调用 `CL_ABAP_STRUCTDESCR` 类的 `GET` 工厂方法来创建结构类型对象。我们将此结构类型对象传递给 `CL_ABAP_TABLEDESCR` 类的 `GET` 工厂方法，以创建表类型对象。

一旦我们有了表类型对象，我们就在 `CREATE` 语句中使用 `TYPE HANDLE` 附加项来使用该类型对象实例化数据引用。这将创建 `R_TABLE` 数据引用，其类型定义在 `R_TABLEDESCR` 类型对象中定义。

尽管 TYPE 或 LIKE 附加项分别允许您指定数据类型或数据对象，但 CREATE DATA 语句的 TYPE HANDLE 附加项允许您指定类型对象。

在动态定义内表之后，我们在 SELECT 语句中使用它来查询给定的数据库表，随后显示输出。如您所见，我们在每一步都处理错误；错误处理对于动态编程至关重要。

如果用户按图 16.5 所示填写字段，清单 16.26 中的代码将生成如图 16.6 所示的输出。我们可以进一步增强代码，只选择表中的特定字段，并仅使用特定字段创建结构。

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_689_0.png)

**图 16.5** 数据浏览器的选择屏幕

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_689_1.png)

**图 16.6** 数据浏览器的输出

在本节中，我们了解了 RTTI 和 RTTC。在下一节中，我们将讨论动态标记的使用。
