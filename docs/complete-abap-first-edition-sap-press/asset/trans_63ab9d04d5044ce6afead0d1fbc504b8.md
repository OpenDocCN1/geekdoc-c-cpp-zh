

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_808_0.png)

**图 19.4** 事务 MM01 的第三屏

要创建另一种物料，请使用不同的数据集重复相同的步骤。如果只想创建少量物料，通过此事务手动创建物料很容易。但如果要创建数百或数千种物料呢？我们可以通过创建批输入程序来自动化此过程。我们将在下一小节中逐步介绍执行此操作的步骤。

## 创建批输入程序

批输入程序要求您将屏幕和字段信息捕获到一个具有特殊结构的内表中，该结构称为 BDCDATA（这里的 BDC 表示*批量数据通信*）。

BDCDATA 结构如图 19.5 所示。

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_808_1.png)

**图 19.5** BDCDATA 结构

BDCDATA 结构由五个组件组成，详见表 19.2。

| 字段名 | 含义 |
| --- | --- |
| PROGRAM | 数据要传输到的屏幕的程序名 |
| DYNPRO | 程序（在上述 PROGRAM 字段中指定）的屏幕编号 |
| DYNBEGIN | 指示新屏幕的标志 |
| FNAM | 屏幕的字段名 |
| FVAL | 要传输到字段的值 |

表 19.2 BDCDATA 结构组件

开发批输入程序的基本概念是：捕获事务的程序名和屏幕字段名，并使用表 BDCDATA 映射应传递给屏幕字段的值。例如，如果查看事务 MM01 的初始屏幕，并在 MATERIAL 字段上使用 [F1] 帮助查看技术信息，可以找到该字段的技术详细信息，如图 19.6 所示。

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_809_0.png)

图 19.6 屏幕字段的技术信息

请注意，程序名为 SAPLMGMM，屏幕编号为 0060，屏幕字段名为 RMG1-MATNR。使用这些信息，我们可以映射 BDCDATA 结构，如清单 19.1 所示。

```abap
PROGRAM ZDEMO_BATCH_INPUT.
Data: it_bdcdata TYPE STANDARD TABLE OF bdcdata,
      wa_bdcdata TYPE bdcdata.
START-OF-SELECTION.
  perform bdc_dynpro      USING 'SAPLMGMM' '0060'.
  perform bdc_field       USING 'RMG1-MATNR' '567A5HG'.
  PERFORM bdc_field       USING 'RMG1-MBRSH' 'P'.
  PERFORM bdc_field       USING 'RMG1-MTART' 'ROH'.
  PERFORM bdc_dynpro      USING 'SAPLMGMM' '0070'.
  ........
FORM bdc_dynpro USING program dynpro.
  CLEAR wa_bdcdata.
  wa_bdcdata-program = program.
  wa_bdcdata-dynpro = dynpro.
  wa_bdcdata-dynbegin = 'X'.
  APPEND wa_bdcdata TO it_bdcdata.
ENDFORM.
FORM bdc_field USING fnam fval.
  CLEAR wa_bdcdata.
  wa_bdcdata-fnam = fnam.
  wa_bdcdata-fval = fval.
  APPEND wa_bdcdata TO it_bdcdata.
ENDFORM.
```

**清单 19.1** 填充 BDCDATA 结构

在清单 19.1 中，我们定义了一个内表 it_bdcdata，其行类型为 BDCDATA。我们定义了两个子例程 BDC_DYNPRO 和 BDC_FIELD。在 BDC_DYNPRO 子例程中，我们填充程序名和屏幕编号。在 BDC_FIELD 子例程中，我们填充字段名和字段值。这两个子例程的 PERFORM 语句都传递两个实际参数。

例如，PERFORM BDC_DYNPRO 语句将程序名和屏幕编号作为字面量传递，PERFORM BDC_FIELD 语句传递字段名和字段值。在我们的示例中，我们为字段值传递字面量，但该字面量将被从顺序文件上传的字段值替换。我们在 BDC_DYNPRO 子例程中将 dynbegin 标记为 X，因为仅当需要传递新屏幕信息时才调用此子例程。

一旦内表填充了所有所需的屏幕和字段信息，我们就可以使用 CALL TRANSACTION 方法或 SESSION 方法传递数据。我们将在接下来的两个小节中介绍这些方法。

### CALL TRANSACTION

在 CALL TRANSACTION 方法中，使用 CALL TRANSACTION USING 语句将 BDCDATA 传递给事务。包含 BDCDATA 的内表随该语句一起传递。事务可以以前台模式、后台模式或出错时前台模式执行。

当事务以*前台模式*执行时，事务在前台运行，显示所有屏幕。以*前台模式*运行事务在进行测试运行时很有用，因为它有助于验证字段是否使用正确的数据进行了正确映射。

当事务以*后台模式*执行时，事务完全在后台运行，不显示任何屏幕。事务在执行期间引发的任何消息将在最后传输到批输入程序。

以*后台模式*运行事务是生产运行的首选方法。如果使用*出错时前台*模式，则事务在后台运行，除非事务引发任何错误消息。如果引发错误消息，则向用户显示导致错误的事务屏幕。

数据可以同步或异步更新。对于同步更新，系统会等待前一个事务提交；而对于异步更新，系统会启动处理下一个事务，而不等待前一个事务提交。

例如，如果要更新销售订单抬头和行项目数据，同步更新可以确保只有在抬头数据提交到数据库后，才更新销售订单行项目数据。如果使用异步更新，销售订单行项目数据可能会在抬头数据提交之前就提交到数据库。因此，异步更新比同步更新更快。

CALL TRANSACTION 方法不支持自动错误日志或出错后恢复。错误处理应在程序中执行。一次只能调用一个事务，并且数据同步处理。

### SESSION

在 SESSION 方法中，我们使用所有数据生成一个会话。然后单独处理该会话。可以通过手动方式处理会话，也可以通过将程序 RSDCSUB 调度为后台作业来按固定间隔处理会话。此方法在出现任何错误时自动创建错误日志。

更正错误后，可以通过恢复会话来处理出错的事务。BDC 程序打开会话（使用函数模块 BDC_OPEN_GROUP），将数据写入会话（使用函数模块 BDC_INSERT），并关闭会话（使用函数模块 BDC_CLOSE_GROUP）。在打开新会话之前，应关闭前一个会话。

SESSION 方法可用于将数据传输到多个事务并执行同步数据库更新。例如，可以使用 SESSION 方法过账单据的抬头和行项目数据，并让系统在更新抬头数据后更新行项目数据。

事务应始终在后台模式下更新；前台模式应仅用于测试屏幕顺序。

CALL TRANSACTION 方法和 SESSION 方法都要求使用表 BDCDATA 传递事务的屏幕和字段信息。然而，手动捕获所有屏幕和字段信息是一项繁琐的工作。为了简化此操作并生成批输入程序，SAP 提供了一个名为事务记录器（事务 SHDB）的工具。

在下一小节中，我们将讨论使用事务 SHDB 生成批输入程序的步骤。

### 使用事务记录器创建批输入程序

使用事务记录器，我们可以模拟事务执行的步骤序列，以捕获表 BDCDATA 所需的所有信息。事务记录器还支持使用这些信息生成批输入程序。

以下步骤演示如何通过事务记录器生成批输入程序：

1. 在事务 SHDB 的初始屏幕（事务记录器：记录概览）上，如图 19.7 所示，单击“新建记录”按钮。

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_813_0.png)

**图 19.7** 事务记录器初始屏幕

2. 在“创建记录”对话框中，如图 19.8 所示，为记录提供名称，并输入应执行记录的事务代码。还可以设置“更新模式”来更新数据。共有三种更新模式可用，如表 19.3 所列。

| 更新模式 | 含义 |
| --- | --- |
| 本地 | 更新任务由处理该事务的对话工作进程执行。 |
| 异步 | 更新由更新工作进程异步执行。 |
| 同步 | 更新由更新工作进程同步执行。 |

**表 19.3** 更新模式选项

还要在“创建记录”框中提供以下设置（图 19.8）：

- 选择“默认大小”复选框，以避免屏幕分辨率问题，并为记录使用默认大小。
- “提交后继续”复选框设置一个标志，以便在使用 CALL TRANSACTION 方法执行提交工作时继续处理。

