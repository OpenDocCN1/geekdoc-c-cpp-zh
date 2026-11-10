
将保存输出数据的内部表的名称赋给 `TABNAME` 组件，将字段名称赋给 `FIELDNAME` 组件，将列位置赋给 `COL_POS` 组件，并将列名称赋给相应的 `SELTEXT` 组件。

在清单 15.3 中，字段目录在 `FIELD_CATALOG` 子例程中填充。函数模块文档应该可以帮助你探索字段目录中可用于格式化输出的其他组件。

我们也可以使用 `REUSE_ALV_FIELDCATALOG_MERGE` 函数模块来填充字段目录内部表。

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_634_0.png)

**图 15.4** 打印 SFLIGHT 表中所选字段

布局可以通过向 `IS_LAYOUT` 形式参数传递类型为 `SLIS_LAYOUT_ALV` 的结构来处理。使用 `IS_LAYOUT` 参数，我们可以控制输出布局，例如使字段可编辑、为单元格使用斑马纹样式、移除水平线或垂直线等。函数模块文档解释了 `SLIS_LAYOUT_ALV` 结构中每个组件的含义。

清单 15.4 展示了如何使用 `IS_LAYOUT` 参数使单元格可编辑，如图 15.5 所示。

> **注意**
> 
> 只有在网格显示中才能使单元格可编辑；此功能在列表显示中不受支持。

```abap
FORM show_output.
DATA layout TYPE SLIS_LAYOUT_ALV.
layout-edit = 'X'.
  CALL FUNCTION 'REUSE_ALV_GRID_DISPLAY'
    EXPORTING
      I_GRID_TITLE = 'ALV Grid Display'
      IS_LAYOUT    = layout
      IT_FIELDCAT  = it_fieldcat
    TABLES
      t_outtab     = it_sflight
    EXCEPTIONS
      PROGRAM_ERROR = 1
      OTHERS        = 2
      .
```

**清单 15.4** 传递 ALV 布局

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_635_0.png)

**图 15.5** 使单元格可编辑

### 15.1.2 块显示

使用块显示，我们可以在输出中打印多个内部表的数据，每个内部表的数据以块的形式打印。对于块显示，我们使用三个函数模块：

- `REUSE_ALV_BLOCK_LIST_INIT`：此函数模块用于初始化块列表并设置 SAP GUI 状态。
- `REUSE_ALV_BLOCK_LIST_APPEND`：此函数模块用于在块模式下附加简单列表；每次需要将内部表中的数据附加到输出时会调用它。
- `REUSE_ALV_BLOCK_LIST_DISPLAY`：此函数模块用于显示块列表。此函数模块的所有参数都是可选的。

清单 15.5 显示了用于块显示的示例代码。

```abap
REPORT ZDEMO_BLOCK_REPORT.
DATA : it_sflight TYPE STANDARD TABLE OF sflight,
       it_spfli TYPE STANDARD TABLE OF spfli,
       it_fcat_sflight TYPE SLIS_T_FIELDCAT_ALV,
       it_fcat_spfli TYPE slis_t_fieldcat_alv,
       it_events TYPE SLIS_T_EVENT.

PARAMETERS p_carrid TYPE s_carr_id.
START-OF-SELECTION.
PERFORM get_data.
END-OF-SELECTION.
PERFORM field_catalog.
PERFORM show_output.

*&---------------------------------------------------------------------*
*&      Form  GET_DATA
*&---------------------------------------------------------------------*
FORM get_data .
SELECT * FROM sflight INTO TABLE it_sflight WHERE carrid EQ p_carrid.
SELECT * FROM spfli INTO TABLE it_spfli WHERE carrid EQ p_carrid.
ENDFORM.
*&---------------------------------------------------------------------*
*&      Form  FIELD_CATALOG
*&---------------------------------------------------------------------*
FORM field_catalog .
CALL FUNCTION 'REUSE_ALV_FIELDCATALOG_MERGE'
  EXPORTING
    i_structure_name       = 'SPFLI'
  CHANGING
    ct_fieldcat            = it_fcat_spfli
  EXCEPTIONS
    inconsistent_interface = 1
    program_error          = 2
    others                 = 3
    .
IF sy-subrc <> 0.
* Implement suitable error handling here
ENDIF.
CALL FUNCTION 'REUSE_ALV_FIELDCATALOG_MERGE'
  EXPORTING
    I_STRUCTURE_NAME = 'SFLIGHT'
  CHANGING
    ct_fieldcat      = it_fcat_sflight
  EXCEPTIONS
    INCONSISTENT_INTERFACE = 1
    PROGRAM_ERROR          = 2
    OTHERS                 = 3
    .
  IF sy-subrc <> 0.
* Implement suitable error handling here
  ENDIF.
ENDFORM.
*&---------------------------------------------------------------------*
*&      Form  SHOW_OUTPUT
*&---------------------------------------------------------------------*
FORM show_output .
  DATA layout TYPE SLIS_LAYOUT_ALV.
  layout-zebra = 'X'.
  CALL FUNCTION 'REUSE_ALV_BLOCK_LIST_INIT'
    EXPORTING
      i_calling_program = 'ZDEMO_BLOCK_REPORT'
    .

  CALL FUNCTION 'REUSE_ALV_BLOCK_LIST_APPEND'
    EXPORTING
      is_layout   = layout
      it_fieldcat = it_fcat_sflight
      i_tabname   = 'IT_SFLIGHT'
      it_events   = it_events
    TABLES
      t_outtab    = it_sflight
    EXCEPTIONS
      PROGRAM_ERROR          = 1
      MAXIMUM_OF_APPENDS_REACHED = 2
      OTHERS                 = 3
    .
  IF sy-subrc <> 0.
* Implement suitable error handling here
  ENDIF.

  CALL FUNCTION 'REUSE_ALV_BLOCK_LIST_APPEND'
    EXPORTING
      is_layout   = layout
      it_fieldcat = it_fcat_sflight
      i_tabname   = 'IT_SFLIGHT'
      it_events   = it_events
    TABLES
      t_outtab    = it_sflight
    EXCEPTIONS
      PROGRAM_ERROR              = 1
      MAXIMUM_OF_APPENDS_REACHED = 2
      OTHERS                     = 3
    .
  IF sy-subrc <> 0.
* Implement suitable error handling here
  ENDIF.

  CALL FUNCTION 'REUSE_ALV_BLOCK_LIST_DISPLAY'
    EXCEPTIONS
      PROGRAM_ERROR = 1
      OTHERS        = 2
    .
  IF sy-subrc <> 0.
* Implement suitable error handling here
  ENDIF.
ENDFORM.
```

**清单 15.5** 块显示

在清单 15.5 中，我们从表 SFLIGHT 和 SPFLI 中选择数据，并将这些数据以块的形式显示在输出中，如图 15.6 所示。

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_638_0.png)

**图 15.6** 显示表 SPFLI 和 SFLIGHT 数据的块显示

### 15.1.3 层次顺序显示

层次顺序显示用于显示相关数据，例如文档的抬头和项目数据。我们使用 REUSE_ALV_HIERSEQ_LIST_DISPLAY 函数模块生成层次顺序显示。此函数模块要求您传递抬头表和项目表以及这些表的关键信息。

关键信息用于标识抬头表和项目表中的相关记录。准备一个字段目录，其中包含抬头表和项目表的所有字段，并将其传递给函数模块。

清单 15.6 显示了开票凭证的顺序报表，输出中打印了有关开票凭证抬头和项目明细的特定数据（参见图 15.7）。

```abap
REPORT ZDEMO_HIERARCHICAL_REPORT.
TYPES : BEGIN OF ty_vbrk,
            vbeln TYPE vbeln_vf,          "Document Number
            kunnr TYPE kunrg,             "Payer
            fkdat TYPE fkdat,             "Billing date
            netwr TYPE netwr.             "Net Value
        END OF ty_vbrk.

TYPES : BEGIN OF ty_vbrp,
            vbeln TYPE vbeln_vf,          "Document Number
            posnr TYPE posnr_vf,          "Billing item
            arktx TYPE arktx,             "Description of item
            fkimg TYPE fkimg,             "Billed quantity
            vrkme TYPE vrkme,             "Sales Unit
            netwr TYPE netwr_fp,          "Net Value
            matnr TYPE matnr.             "Material Number
        END OF ty_vbrp.

DATA : it_vbrk TYPE STANDARD TABLE OF ty_vbrk,
       it_vbrp TYPE STANDARD TABLE OF ty_vbrp,
       it_fieldcat TYPE SLIS_T_FIELDCAT_ALV,
       wa_fieldcat TYPE SLIS_FIELDCAT_ALV,
       v_vbeln TYPE vbeln_vf.
SELECT-OPTIONS s_vbeln FOR v_vbeln.
START-OF-SELECTION.
PERFORM get_data.
END-OF-SELECTION.
PERFORM field_catalog.
PERFORM show_output.
*&---------------------------------------------------------------------*
*&      Form  GET_DATA
*&---------------------------------------------------------------------*
FORM get_data .
  SELECT vbeln kunnr fkdat netwr FROM vbrk INTO TABLE it_
```

