

## 286 掌握 Oracle SQL Developer Data Modeler 数据库设计大师

更改将在目标元素上执行。你可以在树形视图中看到更改将在列上执行，在“详细信息（Details）”面板中，你可以选择仅执行建议的部分更改。例如，你可以指定仅更改名称而不更改数据类型，如图 12-3 所示。

在“存储（Storage）”选项卡中，你可以查看具有存储值的元素（如表）的源和目标存储值。如果存在差异，将用红色标记。存储详细信息例如表空间或存储子句中的任何参数。

![](img/431f8ac8f273fa89a28377c500ed60d7_312_0.png)

图 12-3 比较模型对话框，详细信息选项卡

## 第 12 章：比较设计与数据库

在“选项（Options）”选项卡中，你可以定义 DDL 选项、DDL 存储选项、比较选项、属性过滤器、存储属性过滤器以及日期/时间格式。让我们更仔细地查看它们：

- 在 DDL 选项中，你可以指定以下内容：

- 你可以指定将包含在 DDL 语句中的元素。在“首好（Data Modeler | DDL）”中，你已经指定了除“包含注释”（Include Comments，见第 7 章）之外的所有参数值。可以通过在“比较模型（Compare Models | Options）”中设置不同的值来让比较结果覆盖首好设置。下次启动 Data Modeler 时，首好设置将覆盖此参数设置。

- `Include Comments（包含注释）` 参数控制比较中是否包含注释。

- `Include Default Settings（包含默认设置）` 参数控制生成的 DDL 中是否包含设置。它将为生成的 DDL 中创建的对象的对象添加所有 DDL 关键字。如果你想查看对象 DDL 的语法，此选项非常有用。

- `Include Logging（包含日志）` 参数控制生成的 DDL 中是否包含日志信息。

- `Include Schema（包含模式）` 参数控制在生成的 DDL 语句中，对象名是否带有模式名前缀，例如使用 PROD.CUSTOMER 而不是 CUSTOM。

- `Include Storage（包含存储）` 参数控制生成的 DDL 中是否包含存储信息。如果未包含存储，在 Oracle 中将使用保存对象所在的表空间的存储设置。存储设置例如 PCTREE、PCTUSED、INITRANS 和 MAXTRANS、INITIAL、NEXT、MINEXTENTS 和 MAXEXTENTS。

- `Include Tablespace（包含表空间）` 参数控制生成的 DDL 中是否包含表空间信息。

- 你可以像第 7 章提到的那样选择 DDL 类型。可能的类型有常规 DDL（Regular DDL）、高级交互式 DDL（Advanced Interactive DDL）和高级命令行（Advanced CL）DDL。高级交互式 DDL 和高级 CL DDL 都会创建脚本。这两个脚本都是交互式的，且高级 CL DDL 脚本可以从命令行运行。两个脚本都包含输入参数，例如起始步骤、停止步骤、日志文件和日志级别（1、2 或 3）。如果你想在 SQL*Plus 中运行高级 CL DDL 脚本，语法如下：`SQL> sqlplus user/password@ name @script_name start_step stop_step log_file log_level`。

- 如果选择了 `Replacing Files（替换文件）` 参数，Data Modeler 将自动替换任何现有的 DDL 文件。

- 你还可以指定 `Upload Directory（上传目录）`。这是服务器端的一个目录，如果在执行操作时出现任何问题将使用它。例如，如果数据库运行在 Linux 目录，原本应重建表的表空间可能会耗尽空间。这仅适用于高级交互式 DDL 或高级 DDL，且备份策略设置为“卸（unload）”。常规 DDL 仅使用重命名进行备份。

- 在 `DDL Storage Options（DDL 存储选项）`中，你可以更改在“首好”中设置的 DDL 子句包含内容的值（第 7 章）。你可以在 DDL 的存储子句中包含或排除这些参数：PCTREE、PCTUSED、ITRANS、INITIAL、NEXT、MINEXTENTS、MAXEXTENTS、PCTINCREASE、BUFFER_POOL、FREELIST、FREELIST GROUPS 和 OPTIMAL。

- 在 `Compare Options（比较选项）`中，你可以指定本节之前介绍的相同首好参数：`Use Data Type Kind Property（使用数据类型属性）`、`Use Schema Property（使用模式属性）`、`Use Column Order Property（使用列顺序属性）`、`Case Sensitive Names（大小写敏感名称）`和 `Include System Names（包含系统名称）`。值将来自首好设置，但你可以为比较更改它们。更改这些参数后，点击“刷新树（Refresh Tree）”以更新屏幕上部分，这些参数将对当前比较生效。

- 在 `Properties Filter（属性过滤器）`中，你可以选择在比较时包含或排除的属性。针对弧（arcs）、列、外键、主键和唯一键约束、结构化类型、表和视图等元素都有设置。对于你想要包含的元素，为它的所有属性选择“包含（Included）”。例如，当你将一个带有注释的模型与另一个从数据库创建且没有注释的模型进行比较时，可以排除表的注释和备注，从而确保该元素不会被覆盖。

- `Storage Properties Filter（存储属性过滤器）`如果元素属于具有存储属性的类型，则该过滤器会有内容。你可以从比较中排除某些存储属性。如果你知道源和目标表的表空间不同是故意为之，你可能希望从比较中排除表空间。

- 在 `Date/Time Format（日期/时间格式）`中，你可以设置日期格式、时间戳格式和时间时区格式。

在 `Tables That Will Be Recreated（将重建的表）`中，你可以为每个将要重建的表定义备份策略（重命名/无）、数据恢复（恢复/无）、脚本执行（继续）和卸载目录。表可能需要重建，例如如果列正在发生变化。如果数据类型发生变化，并且根据表是否为空，你可能需要选择一种不同的备份策略。

在 `Data Type Conversion（数据类型转换）`选项卡中，你可以看到哪些列将转换以及新旧数据类型。你可以定义是否重建表。如果表被删除并创建，但它是空的，则必须重建。你还可以定义转换表达式。

如果你选择了高级 DL 或高级 CDL，你可以在 Oracle Errors（Oracle 错误）中指定脚本执行期间忽略某些 Oracle 错误。例如，你可以为 ORA-00942 指定 -942。

![](img/431f8ac8f273fa89a28377c500ed60d7_315_0.png)

提示：你可以点击标题更改 `Tables Be Recreated` 和 `Data Conversion` 选项卡的列顺序。这种更改可能会让屏幕更易读。

经常有人问哪种视图更好，树形视图还是表格视图。我的回答是它们互为补充，这取决于你正在做什么。在表格视图中，你可以一键选择/取消选择所有内容，并可以只选择你想看到的模型元素：全部、数据类型模型和关系模型。在两个视图中，你都可以按状态（新建、删除或修改）进行选择，但在表格视图中你还可以选择未更改。在表格视图中，你可以按类型选择：全部、列、FK 弧、外键、结构化类型或表。对我来说，树形视图更易读，但在表格视图中你可以看到索引等其他内容，这些是可以用的。我建议你学会使用两个视图，因为它们都非常好，根据你的需求，在特定情况下一个可能比另一个更好。我建议在最终合并逻辑时使用树形视图，因为表格视图中的合并可能并不那么明显。在任何视图中，你都可以生成差异报告（HTML、PDF、RTF）。通过选择“按状态分离对象（Separate Objects By Status）”，你可以根据状态列出报告中的差异。

 比较设计与数据库

设计和数据库可以使用“同步模型与数据字典（Synchronize Model With Data Dictionary）”或“同步数据字典与模型（Synchronize Data Dictionary With Model）”进行比较。在所有比较中，你始终有一个目标和一个源，且可能的更改始终在目标上执行。在“同步模型与数据字典”中，目标是

