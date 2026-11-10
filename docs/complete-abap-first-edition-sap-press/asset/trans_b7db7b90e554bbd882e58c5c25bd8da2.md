

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_264_0.png)

**图 7-5** START-OF-SELECTION 作为默认事件

通常，你会将 ABAP 程序的所有数据选择逻辑放在 START-OF-SELECTION 事件中。在这里，程序开始从表中选取值。在典型的报表程序中，你在 INITIALIZATION 事件下初始化程序数据，在选择屏幕事件下校验选择屏幕输入，如果一切正常，则在 START-OF-SELECTION 事件下继续（基于选择条件）进行数据选择。

## GET table

GET table 事件用于可执行程序使用逻辑数据库进行数据选择时。逻辑数据库是一种特殊的 ABAP 程序，它从数据库检索数据并将其提供给应用程序。换句话说，当你在程序中使用逻辑数据库时，无需编写 SQL 语句来从数据库检索数据。

逻辑数据库本身包含 Open SQL 语句，这些语句从数据库检索数据，并逐行将数据传递到应用程序的接口工作区。

逻辑数据库由一个带有选择屏幕和权限检查的程序组成。当报表程序使用逻辑数据库时，该程序可以自动继承选择屏幕和权限检查。

接口工作区使用 `TABLES` 或 `NODES` 关键字定义，它们与使用 `DATA` 关键字定义的工作区工作方式相似，只有一个基本区别。这些接口工作区创建在程序之间的共享数据区中。换句话说，当你使用 `DATA` 关键字定义工作区时，它定义在程序的内存空间中。接口工作区定义在会话的共享内存空间中，同一会话中运行的所有程序都可以访问该空间。因此，不建议使用 `TABLES`，因为它可能产生副作用。

在旧版本的 SAP ERP 系统中，使用逻辑数据库的唯一方式是将其链接到可执行程序，并使用 `GET` 事件检索数据。然而，从 SAP R/3 4.5A 版本开始，可以使用 `LDB_PROCESS` 函数模块在任何程序中调用逻辑数据库。该模块允许你在程序中以任意顺序嵌套调用多个逻辑数据库。在这方面，接口工作区的使用实际上已经过时，仅为了与早期版本向后兼容而保留。

当逻辑数据库从事件关键字中提到的表读取一行，并使其在程序中使用 `TABLES` `<table>` 或 `NODES` `<table>` 语句声明的工作区中可用时，会触发 `GET` 事件（如清单 7.12 所示）。

```abap
    NODES: SPFLI.
    GET SPFLI.
      SKIP.
      WRITE: / 'From:', SPFLI-CITYFROM,
             'To  :', SPFLI-CITYTO.
```

**清单 7.12** 展示 GET 事件的代码

### GET `<table>` LATE

一旦读取完逻辑数据库某个节点的所有数据记录，ABAP 运行时环境就会触发 `GET <table> LATE` 事件。通过在程序中维护此事件，你可以处理应在块末尾执行的步骤。例如，如果你想打印销售订单的逐项汇总，可以在此事件块中完成。

清单 7.13 展示了此事件块的实现。

```abap
NODES: SPFLI, SFLIGHT, SBOOK.
DATA WEIGHT TYPE I VALUE 0.
GET SPFLI.
SKIP.
WRITE: / 'Carrid:', SPFLI-CARRID,
       'Connid:', SPFLI-CONNID,
       / 'From:', SPFLI-CITYFROM,
       'To:', SPFLI-CITYTO.
ULINE.
GET SFLIGHT.
SKIP.
WRITE: / 'Date:', SFLIGHT-FLDATE.
GET SBOOK.
WEIGHT = WEIGHT + SBOOK-LUGGWEIGHT.
GET SFLIGHT LATE.
WRITE: / 'Total luggage weight =', WEIGHT.
ULINE.
CLEAR WEIGHT.
```

**清单 7.13** 展示 GET `<table>` LATE 事件的代码

在清单 7.13 中，我们按日期打印每个航空公司代码（CARRID）和航班连接号（CONNID）的总行李重量汇总。我们使用 GET SPFLI 事件检索航班详细信息。GET SFLIGHT 事件循环处理给定日期的所有航班（用户可以在逻辑数据库选择屏幕上限制范围）。

GET SBOOK 事件从表 SBOOK 中检索相应航班每次预订的行李重量。在此事件中，我们汇总给定日期的总重量。

最后，一旦处理完给定日期航班的所有记录，就会在末尾调用 GET SFLIGHT LATE 事件。在此事件中，我们打印相应 CARRID 和 CONNID 在给定日期的总行李重量。在此示例中，我们使用逻辑数据库选择 F1S，你可以使用事务 SLDB 进行检查。

## END-OF-SELECTION

END-OF-SELECTION 事件用于标记选择的结束。如果你的报表未使用逻辑数据库，则该事件在 START-OF-SELECTION 事件之后使用，以标记选择结束，并继续对所选数据进行进一步处理，例如在输出中打印所选数据。但是，如果你的报表链接到逻辑数据库，则该事件在逻辑数据库将所有记录完全传输到应用程序之后调用。

例如，在清单 7.13 中，如果逻辑数据库选择的所有数据都更新到一个内部表中，而你随后想进一步处理该表，则可以使用 END-OF-SELECTION 事件标记数据选择的结束，并实现进一步处理所选数据的逻辑。END-OF-SELECTION 事件由运行时环境在处理完所有 GET 事件后调用。

当使用逻辑数据库时，使用此事件来将选择逻辑与输出逻辑分离变得必不可少。否则，它的目的纯粹是为了文档化和使代码更易读。我们建议即使程序中没有使用逻辑数据库，也使用此事件来标记从选择逻辑到输出逻辑的分离。

清单 7.14 展示了一个使用 END-OF-SELECTION 事件的示例。

```abap
NODES: SPFLI, SFLIGHT, SBOOK.
DATA: gr_table TYPE REF TO cl_salv_hierseq_table.
DATA: it_spfli TYPE TABLE OF spfli.
DATA: it_sflight TYPE TABLE OF sflight.
DATA: it_binding TYPE salv_t_hierseq_binding.
DATA: wa_binding LIKE LINE OF it_binding.

GET SPFLI.
APPEND spfli TO it_spfli.
GET SFLIGHT.
APPEND sflight TO it_sflight.

END-OF-SELECTION.
wa_binding-master = 'CARRID'.
wa_binding-slave = 'CARRID'.
APPEND wa_binding TO it_binding.

wa_binding-master = 'CONNID'.
wa_binding-slave = 'CONNID'.
APPEND wa_binding TO it_binding.

cl_salv_hierseq_table=>factory(
  EXPORTING
    t_binding_level1_level2 = it_binding
  IMPORTING
    r_hierseq = gr_table
  CHANGING
    t_table_level1 = it_spfli
    t_table_level2 = it_sflight ).
gr_table->display( ).
```

**清单 7.14** END-OF-SELECTION 事件

在 **清单 7.14** 中，我们分别在 `GET SPFLI` 和 `GET SFLIGHT` 事件中填充内部表 `IT_SPFLI` 和 `IT_SFLIGHT`。然后，我们在 `END-OF-SELECTION` 事件中使用 ALV 对象模型将此数据显示为层次顺序显示。

ALV 对象模型使生成 ALV 输出变得容易。我们将在 **第 15 章** 中进一步讨论 ALV 对象模型。

### 7.3.3 选择屏幕事件

*选择屏幕*是允许用户输入程序选择条件的特殊屏幕。它们通常用于报表程序（可执行程序），但也可用于模块池程序或函数组。

选择屏幕事件通常有助于准备选择屏幕并评估用户在屏幕上的操作。例如，我们可以使用选择屏幕事件在运行时为输入字段分配默认值、动态禁用或启用某些字段，或者校验用户输入并向用户显示适当消息。

当为程序定义选择屏幕并由 ABAP 运行时环境处理时，会触发选择屏幕事件。如果程序未定义选择屏幕，则不会触发任何选择屏幕事件。

选择屏幕被归类为特殊屏幕，可以使用 ABAP 语句（`PARAMETERS` 或 `SELECT-OPTIONS`）定义，并由 ABAP 编译器自动生成，而不是像一般屏幕那样使用屏幕绘制器（Screen Painter）手动定义。

由于选择屏幕是自动生成的，程序员无法访问屏幕流逻辑，而原本可以在其中定义对话模块来修改屏幕或响应用户操作。ABAP 运行时环境完全控制屏幕处理，并生成若干选择屏幕事件，程序员可以通过这些事件在程序中维护事件块以响应这些事件。

