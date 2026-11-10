
如果通过字段符号更改字段，第三行的字段会立即更改，因为字段符号直接指向第三行。

我们不必像清单 16.2 中那样使用 `MODIFY` 语句手动复制内容，因为清单 16.3 中的 `<wa>` 字段符号不占用单独的内存空间，而是指向现有内存，这与清单 16.2 中的工作区 `wa` 不同。

一旦将数据对象分配给字段符号，我们就可以像使用所分配的数据对象一样使用该字段符号，并执行通常可以在所分配的数据对象上执行的操作。几乎任何数据对象都可以分配给字段符号。

正如你在清单 16.3 中看到的，可以定义字段符号、将数据对象分配给字段符号、在访问字段符号之前检查字段符号是否已分配，等等。不过，在讨论这些方面之前，我们先看看字段符号如何帮助使程序动态化。

### 16.1.1 使用字段符号使程序动态化

对于我们的示例，我们将使用一个报表来显示物料的某些基本信息。在这个报表中，我们将使用 ALV 对象模型来显示输出。我们将提供一项功能，让用户可以双击任意单元格，以便根据该单元格的值过滤记录，并在所显示输出下方的新容器中显示结果。

该报表的大多数组件都是静态的：我们已经知道要在输出中显示的数据以及该报表的用户输入。然而，根据用户操作过滤记录是动态的。我们来看看如何以静态方式实现这一点，然后再看看如何使其动态化。

清单 16.4 展示了使用 ALV 对象模型的报表代码。代码很长，但非常直接。花些时间通读代码，并在你的系统中试用一下。

```abap
REPORT zdemo_salv_static.
CLASS lcl_event_handler DEFINITION DEFERRED.
DATA: custom_container TYPE REF TO cl_gui_custom_container,
      splitter         TYPE REF TO cl_gui_splitter_container,
      container_1      TYPE REF TO cl_gui_container,
      so_alv           TYPE REF TO cl_salv_table,
      mo_alv           TYPE REF TO cl_salv_table,
      gr_event_handler TYPE REF TO lcl_event_handler,
      gr_event         TYPE REF TO cl_salv_events_table.
TYPES: BEGIN OF ty_mara,
         matnr TYPE mara-matnr,
         ersda TYPE ersda,
         ernam TYPE ernam,
         laeda TYPE laeda,
         mtart TYPE mtart,
       END OF ty_mara.
DATA: it_mara TYPE STANDARD TABLE OF ty_mara,
      gv_matnr TYPE matnr.
SELECT-OPTIONS: s_matnr FOR gv_matnr.

*&--------------------------------------------------------------*
*&    Class LCL_EVENT_HANDLER
*&--------------------------------------------------------------*
CLASS lcl_event_handler DEFINITION.
  PUBLIC SECTION.
    METHODS: on_double_click FOR EVENT double_click OF cl_salv_events_table IMPORTING row column.
ENDCLASS. "LCL_EVENT_HANDLER

*--------------------------------------------------------------*
*    CLASS lcl_event_handler IMPLEMENTATION
*--------------------------------------------------------------*
CLASS lcl_event_handler IMPLEMENTATION.
  METHOD on_double_click.
    DATA: lo_sel       TYPE REF TO cl_salv_selections,
          ls_cell      TYPE salv_s_cell,
          container_2  TYPE REF TO cl_gui_container,
          lt_mara      TYPE STANDARD TABLE OF ty_mara,
          lw_mara      TYPE ty_mara.
*Get reference to the user selection.
    lo_sel = mo_alv->get_selections( ).
*Get the value of the cell
    ls_cell = lo_sel->get_current_cell( ).
*Logic to filter records
    IF ls_cell-columnname EQ 'MATNR'.
      LOOP AT it_mara INTO lw_mara WHERE matnr EQ ls_cell-value.
        APPEND lw_mara TO lt_mara.
      ENDLOOP.
    ELSEIF ls_cell-columnname EQ 'ERSDA'.
      LOOP AT it_mara INTO lw_mara WHERE ersda EQ ls_cell-value.
        APPEND lw_mara TO lt_mara.
      ENDLOOP.
    ELSEIF ls_cell-columnname EQ 'ERNAM'.
      LOOP AT it_mara INTO lw_mara WHERE ernam EQ ls_cell-value.
        APPEND lw_mara TO lt_mara.
      ENDLOOP.
    ELSEIF ls_cell-columnname EQ 'LAEDA'.
      LOOP AT it_mara INTO lw_mara WHERE laeda EQ ls_cell-value.
        APPEND lw_mara TO lt_mara.
      ENDLOOP.
    ELSEIF ls_cell-columnname EQ 'MTART'.
      LOOP AT it_mara INTO lw_mara WHERE mtart EQ ls_cell-value.
        APPEND lw_mara TO lt_mara.
      ENDLOOP.
    ENDIF.
    CALL METHOD splitter->get_container
      EXPORTING
        row    = 2
        column = 1
      RECEIVING
        container = container_2.

    TRY.
        IF so_alv IS BOUND.
          so_alv->set_data( CHANGING t_table = lt_mara ).
        ELSE.
          CALL METHOD cl_salv_table=>factory
            EXPORTING
              list_display = if_salv_c_bool_sap=>false
              r_container = container_2
            IMPORTING
              r_salv_table = so_alv
            CHANGING
              t_table      = lt_mara.
        ENDIF.
      CATCH cx_salv_no_new_data_allowed.
      CATCH cx_salv_msg.
    ENDTRY.

    so_alv->display( ).
  ENDMETHOD.                    "on_double_click
ENDCLASS.                     "lcl_event_handler

START-OF-SELECTION.
  PERFORM fill_table.
  CALL SCREEN 100.

*&---------------------------------------------------------------------*
*&      Module STATUS_100 OUTPUT
*&---------------------------------------------------------------------*
MODULE status_100 OUTPUT.
* Create Container Object
  CREATE OBJECT custom_container
    EXPORTING
      container_name = 'CONTAINER'.
*Create splitter Object
  CREATE OBJECT splitter
    EXPORTING
      parent  = custom_container
      rows    = 2
      columns = 1.
*Split the container
  CALL METHOD splitter->get_container
    EXPORTING
      row    = 1
      column = 1
    RECEIVING
      container = container_1.
*Get ALV Object reference
  TRY.
      CALL METHOD cl_salv_table=>factory
        EXPORTING
          list_display = if_salv_c_bool_sap=>false
          r_container  = container_1
        IMPORTING
          r_salv_table = mo_alv
        CHANGING
          t_table      = it_mara.
    CATCH cx_salv_msg.
  ENDTRY.
* Set the event handler here
  gr_event = mo_alv->get_event( ).
  CREATE OBJECT gr_event_handler.
  SET HANDLER gr_event_handler->on_double_click FOR gr_event.
*Display Output
  mo_alv->display( ).
ENDMODULE.                 " STATUS_100  OUTPUT
*&--------------------------------------------------------------*
*&      Form  FILL_TABLE
*&--------------------------------------------------------------*
*&--------------------------------------------------------------*
FORM fill_table.
  SELECT matnr ersda ernam laeda mtart FROM mara INTO TABLE it_mara WHERE matnr IN s_matnr.
ENDFORM.                    " FILL_TABLE
```

**清单 16.4** 显示物料和过滤功能的报表

在清单 16.4 中，我们从表 MARA 中选择某些字段数据并显示输出。我们使用 ALV 对象模型生成 ALV 输出。

我们为程序定义了屏幕 100，并在其中创建了一个自定义控件。因为我们要在同一屏幕上显示过滤后的记录，所以我们使用 CL_GUI_SPLITTER_CONTAINER 类将容器拆分为两行。

在第一行中，我们显示完整的选择数据；在第二行中，我们显示过滤后的数据。图 16.1 展示了该报表的初始显示。

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_669_0.png)

**图 16.1** 初始 ALV 显示

用户可以双击任意单元格，以在主显示下方的新容器中显示过滤后的记录。例如，如果用户在图 16.1 中双击物料类型 HALB，输出将如图 16.2 所示。

要按照用户的选择在新容器中显示过滤后的数据，我们需要做几件事：

- 1. 识别用户操作（双击）
- 2. 识别要用于过滤记录的单元格的列和值

当用户双击单元格时，ALV 对象模型会触发 `ON_DOUBLE_CLICK` 事件。在程序中，我们设置事件处理器，并且还在 `LCL_EVENT_HANDLER` 局部类中定义了 `ON_DOUBLE_CLICK` 事件处理器方法。在该方法中，我们根据值过滤记录并显示过滤后的记录，如图 16.2 所示。

当用户双击时，会调用 `LCL_EVENT_HANDLER` 局部类的 `ON_DOUBLE_CLICK` 方法。我们感兴趣的正是该方法中的代码。如果查看该方法中的代码，你会注意到我们使用了 `IF... ELSEIF... ENDIF` 块来手动检查字段名，并相应地过滤内表数据。
