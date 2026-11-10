
例如，假设你正在调试一个程序，并遇到一个函数模块调用，如*图 17.16*所示。

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_711_0.png)

**图 17.16** 调试系统程序

*图 17.16*中所示的 SUSR_SHOW_USER_DETAILS 函数模块属于一个函数组，该函数组的 PROGRAM STATUS 被设置为系统程序（类型 S），如*图 17.17*所示。如果你在此函数模块调用处按 F5，调试器不会进入该函数模块。要进入该函数模块，你首先需要激活系统调试。为此，请按照菜单路径 SETTINGS • SYSTEM DEBUGGING 操作。该选项默认关闭，以便让你跳过调试系统程序，这些程序通常不会引发任何问题。

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_711_1.png)

**图 17.17** 程序状态

除了在程序源代码中保留断点外，你还可以在屏幕的命令栏中输入 /H 来激活调试器。如果你想从应用程序某个屏幕的 PAI 开始调试，此选项很有用。例如，假设你想分析在屏幕上选择特定按钮时所调用的代码。逐行查看源代码以确定按钮操作所调用的代码非常繁琐。通过为该屏幕激活调试并执行你想检查程序执行情况的操作，就可以轻松避免手动浏览源代码。

有时，你可能想为模态对话框窗口激活调试。由于这些窗口没有命令栏，因此无法使用 /H 为这类窗口激活调试器。要为没有命令栏的对话框窗口激活调试器，你可以为 /H 命令创建快捷方式，然后将该快捷方式拖放到对话框窗口上。要创建快捷方式，请单击任意屏幕标准工具栏中的 Generate Shortcut 图标。这将打开一个对话框窗口，如图 17.18 所示。

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_712_0.png)

**图 17.18** 创建快捷方式

在 Type 下，选择 SYSTEM COMMAND，并在 Command 字段中输入 "/H"。对于 Location，选择 DESKTOP，然后单击 FINISH。这将在你的桌面上创建快捷方式。你可以将该快捷方式拖放到任意模态对话框上，以开启该窗口的调试。

## 17.2 新调试器

经典调试器与程序在同一会话中加载。这给调试 ABAP 程序带来了一些技术挑战。这也限制了为调试器开发新的 UI 设计。为了克服这些挑战，SAP 引入了新调试器。

在以下各节中，我们将介绍新调试器提供的、与经典调试器不同的 UI 和工具。我们还将介绍整体布局以及会话的使用。

### 17.2.1 UI 与工具

新调试器提供功能丰富的 UI，可自定义为在一个桌面中最多显示四个工具。图 17.19 展示了将 UI 自定义为显示不同工具的新调试器。一个工具显示源代码，另一个工具显示内表，第三个工具显示对象，第四个工具显示变量。

在新调试器中，每个选项卡称为一个桌面，总共有十二个桌面，每个桌面能够显示四个工具。每个工具都有自己的选项，如图 17.20 所示。使用工具的可用选项，你可以在桌面中加载新工具、替换工具、交换工具、最大化工具等。工具还有特定的服务，可使用 SERVICES OF THE TOOL 图标访问。

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_714_0.png)

ABAP Debugger(1) (Exclusive)(CR2EH6_EH7_00)

Step Size  Watchpoint  Layout  Configure Debugger Layer

MODULE (PBO) / STATUS 1001    Deskt...  Desktop 2  Desktop 3  Stand...  Structures  Tables  Objects  Details  Display Data Explorer  Break/Watchpoints  Diff  Script

```abap
100 column
101 container = container_1.
102 CALL METHOD cl_gui_cfw=>...
103   EXPORTING
104     container = container_1
105   IMPORTING
106     ...
107     list_display = if_salv_bs...
108   TABLES
109     ...
110 CALL METHOD cl_salv_table=>factory
111   EXPORTING
112     ...
113   IMPORTING
114     ...
115   EXCEPTIONS
116     ...
117 * error/warning handler here
118   IF sy-subrc <> 0.
119     MESSAGE ...
120   ENDIF.
121 * set handler on double click
122   SET HANDLER ...
123 ENDTRY.
```

| 行 | MATNR (C18) | ERSDA (D8) | ERNAM (C12) |
| --- | --- | --- | --- |
| 1 | 100-101 | 19960305 | KOSTTE |
| 2 | 100-102 | 19960305 | KOSTTE |
| 3 | 100-103 | 19960417 | BALLER |
| 4 | 100-110 | 20100310 | ERCHA |
| 5 | 100-113 | 20100310 | ERCHA |

| 引用 | 对象 | 视图 | 属性 |
| --- | --- | --- | --- |
| CONTAINER | (0:60)*CL_GUI_CONTAINER | ... | ... |

- CONTAINER
  - CL_GUI_CONTAINER
    - 0:60*CL_GUI_CONTAINER
    - 0:60*CL_GUI_CONTAINER
- CONTROLLER
  - CL_GUI_CONTROLLER
    - M_CLSID
    - ACTIVEX

| S... | 变量 | 值... |
| --- | --- | --- |
| MO_ALV | CONTAINER_1 | (0:60)*CL_GUI_CONTAINER |
| CONTAINER_1 | ... | (0:60)*CL_GUI_CONTAINER |

**图 17.19** 新 ABAP 调试器

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_714_1.png)

各种桌面

```abap
115 CALL METHOD splitter->get_container
116   EXPORTING
117     column = 1
118   RECEIVING
119     container = container_1.
120 * get alv object reference
121   TRY.
122     CALL METHOD cl_salv_table=>factory
123       EXPORTING
124         list_display = if_salv_bs...
125         container = container_1
126       IMPORTING
...
```

- 关闭工具
- 新建工具
- 替换工具
- 全屏
- 交换工具
- 水平最大化
- 工具服务

**图 17.20** 工具区域

选择 NEW TOOL 选项会打开一个窗口，如图 17.21 所示。如你所见，新调试器提供的工具支持比经典调试器更广泛。它还提供一些特殊工具——例如，用于调试 Web Dynpro 应用程序的工具。从 New Tool 窗口中选择任意工具，即可将其添加到桌面。

逐行运行代码并分析数据对象的过程与经典调试器类似（使用 F5 到 F8 功能键，如第 17.1.1 节所述）。与经典调试器相比，CREATE WATCHPOINT 窗口除了变量之外，还允许你设置监视点来监控对象属性的更改。

按照菜单路径 MISCELLANEOUS • DEBUGGER TIPS 操作，你将看到使用新调试器的各种提示。我们建议你浏览所有提示，以便能够自如地使用新调试器。

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_715_0.png)

### 17.2.2 布局与会话

你可以通过菜单路径 DEBUGGER ▸ DEBUGGER SESSION ▸ SAVE LAYOUT 保存新调试器的布局（见图 17.22）。如果你使用不同工具自定义了桌面布局，并希望将结果用作默认布局，此选项很有用。

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_716_0.png)

**图 17.22** 保存布局

你可以通过菜单路径 DEBUGGER ▸ DEBUGGER SESSION ▸ SAVE 保存当前调试会话。这将打开 SAVE CURRENT DEBUGGING SESSION 窗口，如图 17.23 所示。你可以通过选择相应的单选按钮并为会话提供名称，将当前调试会话保存到文件或数据库。还可以选择添加注释，以便轻松识别已保存的会话。

会话的不同组件（如布局、断点、监视点、设置、选项和变量）都可以保存（见图 17.23）。你可以通过菜单路径 DEBUGGER ▸ DEBUGGER SESSION ▸ LOAD 加载已保存的会话，通过菜单路径 DEBUGGER ▸ DEBUGGER SESSION ▸ OVERVIEW/DELETE 查看并删除已保存的会话，以及通过菜单路径 DEBUGGER ▸ DEBUGGER SESSION ▸ DESIGNATION OF THE USER DESKTOP 更改桌面选项卡的名称。

由于新调试器会在新会话中打开，因此当被调试的应用程序进入可输入状态时，外部调试器会话会保持打开，并且应用程序屏幕会呈现给用户以供输入。如果到达任何后续断点，调试器会自动加载。这可确保调试器不会丢失之前设置的任何布局更改或工具排列。

