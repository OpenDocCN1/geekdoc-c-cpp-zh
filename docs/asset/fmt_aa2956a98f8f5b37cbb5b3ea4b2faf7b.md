
> 定义 `Default DDL Files Export Directory` 设置，这样你就能始终知道 DDL 文件保存在哪里了。

![](img/431f8ac8f273fa89a28377c500ed60d7_194_0.png)

> 注意
> 第 10 章将涵盖影响导入的 DDL 首选项（导入时替换系统名称、导入时创建定义域）。

![](img/431f8ac8f273fa89a28377c500ed60d7_194_1.png)

图 7-2 显示了首选项对话框打开到 `Data Modeler | DDL | DDL/Storage` 选项卡。`DDL Storage Options For Import And Export` 下的选项允许你定义是否将存储选项包含在导入和导出操作的 DDL 中。你可以在 DDL 的存储句中包含或排除这些参数：`PCTFREE`、`PCTUSED`、`INITRANS` 和 `MAXTRANSANS`、`INITIAL`、`NEXT`、`MINEXTENTS`、`MAXEXTENTS`、`PCTINCREASE`、`BUFFER_POOL`、`FREELIST`、`FREELIST GROUPS`、`OPTIMAL` 以及 `Encryption`。默认行为是选中所有这些关键字，并将物理模型中定义的值包含在生成的 DDL 中。

# 第 7 章：生成用于创建数据库对象的 DDL 脚本 169

![](img/431f8ac8f273fa89a28377c500ed60d7_195_0.png)

图 7-2. 用于导入和导出的 DDL 存储选项

此外，还有两个设计属性会影响 DDL 的生成。在 `DDL Properties` 对话框中（通过选择 `Design Properties | Settings | DDL` 打开），你可以决定是否对主键、唯一和外键约束自动生成索引。如果你启用了自动生成索引，索引将自动生成，你不需要在物理模型中定义它。我建议禁用这些设计属性（该功能在工具中也是默认值），并在你的数据库中指定每个索引。有时会有两个相似的索引候选，你可能决定不创建外键，因为另一个候选包含了所有的外键列，并在索引末尾还有一些额外的列。手动查看所有索引并决定是否创建索引是非常重要的。另一个属性是 `Preserve DDL Generation Options`，用于控制在当前 DDL 生成操作后恢复原始的 DDL 生成选项。

> 提示
> 记住，在设计级属性中，你也可以为自动生成的索引定义一个命名标准的模板。

在 `DDL Migration Properties`（`Design Properties | Settings | DDL | Migration`）的 `Name Substitution` 选项卡中，你可以定义在生成 DDL 语句时将对象中的旧字符串替换为新字符串。只有当你同样勾选 `DDL Generation Options` 对话框中的 `Apply Name Substitution` 时，才会生效。这在很多情况下有用。例如，如果你的测试数据库有一个名为 `TEST` 的模式，而生产数据库有一个名为 `XYZ` 的模式，你不需要准备独立的物理模型；可以使用名称替换在为测试数据库生成 DDL 时替换名称 `XYZ`。如果你在 `Design Properties` 中指定了 `Name Substitution` 规则，你可以在 DDL 生成的 `Name Substitution` 选项卡中看到它们，并将其用于名称替换。

## 提示

测试这些首选项和属性最快的方法是使用 `DDL Preview`。在关系图中选择一个表，右键点击并选择 `DDL Preview`。现在预览器已打开，你可以选择图中的另一个对象，DDL 脚本将相应更新。你也可以更改首选项或设计属性，并查看更改将如何影响 DDL 的生成。

![](img/431f8ac8f273fa89a28377c500ed60d7_196_0.png)

## 导出 DDL 文件

你可以通过选择 `File | Export | DDL File` 或点击关系模型工具栏上的 `Generate DDL` 图标来开始 DDL 生成。首先，你选择用于 DDL 生成的 RDBMS 站点和关系模型，然后点击 `Generate`（如图 7-3 所示）。如果一个关系模型有多个物理模型，Data Modeler 默认会建议最近更改过的 RDBMS 站点；如果你需要，可以选择另一个。在 DDL 生成后也会显示此屏幕，这就是为什么有 `Clear`、`Save` 和 `Find` 按钮。`Clear` 清空屏幕，`Save` 将内容保存到文件。你可以使用 `Find` 在 SQL 中搜索某些文本。图 7-3 中的示例是生成后的。你可以看到生成的 SQL。

> 注意
> 如果你选择的 RDBMS 站点不存在或未打开，生成的 DDL 将仅包含关系模型的信息。

![](img/431f8ac8f273fa89a28377c500ed60d7_196_1)

# 第 7 章：生成用于创建数据库对象的 DDL 脚本 171

![](img/431f8ac8f273fa89a28377c500ed60d7_197_0)

图 7-3. DDL 文件

## 探索 DDL 选项

显示了首选项对话框打开到 `Data Modeler | DDL | DDL/Storage` 选项卡。`DDL Storage Options For Import And Export` 下的选项允许你定义是否将存储选项包含在导入和导出操作的 DDL 中。你可以在 DDL 的存储句中包含或排除这些参数：`PCTFREE`、`PCTUSED`、`INITRANS` 和 `MAXTRANSANS`、`INITIAL`、`NEXT`、`MINEXTENTS`、`MAXEXTENTS`、`PCTINCREASE`、`BUFFER_POOL`、`FREELIST`、`FREELIST GROUPS`、`OPTIMAL` 以及 `Encryption`。默认行为是选中所有这些关键字，并将物理模型中定义的值包含在生成的 DDL 中。

# 第 7 章：生成用于创建数据库对象的 DDL 脚本 172

![](img/431f8ac8f273fa89a28377c500ed60d7_198_0)

**图 7-4.** DDL 生成选项对话框

`DDL Generation Options` 控制包含在 DDL 中的内容。在树中你可以看到物理模型中的所有元素，选中的物理模型名称出现在生成的 DDL 顶部。在树的底部你可以看到这些选项：`Tables`、`UK Constraints`、`Foreign Keys`、`Views`、`Clusters`、`Dimensions`、`Materialized Views`、`Synonyms`、`Sequences`、`Bitmap Join Indexes`、`External Tables`、`Collection Types`、`Triggers`、`Packages`、`Package Bodies`、`Stored Procedures` 和 `Structured Types`。在这些选项卡上，你可以选择并排除某些对象类型。例如，在 `Tables` 选项卡上你可以选择某些表并排除其他。

这些选项卡下方有一个 `Design Rules` 按钮。此按钮允许你对当前设计中的定义规则进行检查。在生成 DDL 之前最好使用它并修复任何违规项。如果选中了 `Include Comments` 选项，DDL 将包含关系模型定义的注释。还有支持的 DDL 类型列表：`Regular DDL`、`Interactive DDL` 和 `Advanced DDL`。`Regular DDL` 生成常规 DDL，而 `Interactive DDL` 和 `Advanced DDL` 支持交互式脚本。在生成的 DDL 脚本开头（注释中），你可以看到什么样的交互式类型以及该功能需要哪些权限。常规 DDL 看起来就像我们在本章节早期创建名为 `Order` 表时看到的示例。

用于创建 `Order` 表的定义交互式 DDL 脚本看起来如下：

```sql
declare
  statement varchar2(32000);
  comments varchar2(200);
begin
  statement := 'PROMPT CREATING TABLE ''Order''
CREATE TABLE ''Order'' (
  ''OrderNo'' NUMBER NOT NULL,
  ''Information'' VARCHAR2 (100 CHAR) NULL
  ORGANIZATION HEAP NOCOMPRESS NOCACHE PARALLEL NOROWDEPENDENCIES
)
DISABLE ROW MOVEMENT';
comments := 'PROMPT CREATING TABLE ''Order''';
adv_scripting.EXEC_STATEMENT(10,statement,comments);
end;
/
end Step10
-- Step20
declare
  statement varchar2(32000);
  comments varchar2(200);
begin
  statement := 'COMMENT ON TABLE ''Order'' IS ''This is the table for Orders.'''
  comments = 'COMMENT ON TABLE ''Order'' ';
adv_scripting.EXEC_STATEMENT(20,statement,comments);
end;
/
end Step20
```

以下是选择 Advanced CL DDL 时相同示例的代码：

```sql
-- Step10
declare
    statement varchar2(32000);
    comments varchar2(200);
begin
    statement :=='PROMPT CREATING TABLE ''Order'';
    CREATE TABLE ''Order'' (
      ''OrderNo'' NUMBER,
      ''Information'' VARCHAR2 (100 CHAR) NULL
    ) ORGANIZATION HEAP
    NOCCOMPRESS
    NOCACHE
    NOPARALLEL
    NOWDEPENDENCIES
    DISABLE ROW MOVEMENT
    ;
    comments := ''PROMPT CREATING TABLE ''Order'';
    CREATE TABLE ''Order'' '';
    adv_scripting.EXEC_STATEMENT(10,statement,comments);
end;
-- Step20
declare
    statement varchar2(32000);
    comments varchar2(200);
begin
    statement :='COMMENT ON TABLE ''Order'' IS ''This is the table for
Orders.'''';
    comments := ''COMMENT ON TABLE ''Order'' '';
    adv_scripting.EXEC_STATEMENT(20,statement,comments);
end;
-- Step30
declare
    statement varchar2(32000);
    comments varchar2(200);
begin
    statement :=='PROMPT CREATING PRIMARY KEY ON ''Order'';
    ALTER TABLE ''Order''
    ADD CONSTRAINT ''Order_PK'' PRIMARY KEY ( ''OrderNo'' ) NOT DEFERRABLE
    ENABLE VALIDATE '';
    comments := ''PROMPT CREATING PRIMARY KEY ON ''Order'';
    ALTER TABLE ''Order''
    adv_scripting.EXEC_STATEMENT(30,statement,comments);
end;
/

- end Step30
spool off
exit;
```

如果你想为每个对象单独创建一个 DDL 文件，请选择“在单独文件中生成 DDL”（`Generate DDL In Separate Files`）。否则，所有 DDL 将生成在一个单独文件中。此选项从 4.0.2 版本起可用。将其添加到工具中是因为许多用户希望每个对象拥有一个 DDL 文件，而在之前，只能一次生成一个。现在，你可以通过选择“在单独文件中生成 DDL”来生成。文件将生成到你在生成期间指定的目录或你在“偏好”（`Preferences`）中定义的目录。Data Modeler 将创建一个以设计名称命名的目录，以及一个关系模型的子目录和一个物理模型的子目录。对于物理模型目录，如果你定义了创建策略，你可以在那里找到这些策略的 DDL 以及一个名为 `DataObjects` 的目录。在 `DataObjects` 下，你会找到所有对象类型的目录，在它们下面，你会找到每个对象类型的所有 DDL。在我看来，这是处理生产环境 DDL 的最佳方法，因为你通常逐个创建对象并对其进行仔细计划和测试。对于测试环境，你可能希望创建一个特定版本的整个数据库，在这种情况下，你会希望所有的 DDL 都在一个文件中。如果你选择了“常规 DDL”（`Regular DDL`）以外的任何其他 DDL 类型，则无法使用将 DDL 放在单独文件的选项。

在同一树形结构的顶部，你可以看到不同类型 DDL 操作的标签卡。在“创建”（`Create`）标签卡（如图 7-4 所示）上，你可以选择底部的标签卡以包含在 DDL 生成中，或者使用标签卡按对象类型进行选择和取消。在“删除”（`Drop`）选择标签卡（图 7-5）中，你可以指定哪些对象类型将带有位于 CREATE 子句之前的 DROP 子句 DDL。你还可以决定是否为所有选择对象生成 DROP 子句，或仅为生成的对象生成（仅删除已生成的对象），以及是否在 DROP 子句中添加 CASCADE 选项。CASCADE 表示子表将包含在 DROP 操作中。

在“名称替换”（`Name Substitution`）标签卡（图 7-6）上，你可以定义在生成 DDL 语句时将对象名称中的旧字符串替换为新字符串。只有当你同时在屏幕底部选择“名称替换”时，这才会生效。你也可以像本章前面解释的那样，在设计属性中定义名称替换。在设计属性中定义的名称替换将自动显示在此屏幕上。

# 176 Oracle Developer Data Modeler 数据库设计精通

![](img/431f8ac8f273fa89a28377c500ed60d7_202_0.png)

图 7-5. “删除”选择标签卡

在“对象类型”（Object Types）标签卡上，你可以指定名称替换的对象类型：索引（`Index`）、角色（`Role`）、表（`Table`）、表空间（`Tablespace`）和用户（`User`）。

如果你为表定义了这些脚本（第 5 章），你可以在“包含表脚本”（`Include Table Scripts`）标签卡上看到它们（图 7-7）。在此标签卡上，你可以定义这些脚本是否被包含在生成的 DDL 中。这不会影响为视图定义的脚本；它们只能通过关系模型中视图属性“脚本”（Scripts）标签卡上的“包含到 DDL 脚本”（`Include Into DDL Script`）来控制。如果你在“DDL 生成选项”中禁用表的脚本生成，则关系模型中表属性“脚本”标签卡上的表的“包含到 DDL 脚本”属性将自动禁用。

> 注意
> 你无法在 DDL 预览中看到表脚本。

# 第 7 章：创建数据库对象生成 DDL 脚本 177

![](img/431f8ac8f273fa89a28377c500ed60d7_203_0.png)

图 7-6. 名称替换标签卡

如果你选择了“高级 DDL”（`Advanced DDL`）或“高级 CL DDL”而不是“常规 DDL”（`Regular DDL`），在“Oracle 错误”（`Oracle Errors To Mask`）标签卡上，你可以指定脚本执行期间忽略的任何 Oracle 错误。在类型字段中指定错误编号和有效数字。例如，对于 ORA-0942，指定 -942。你还可以指定错误描述，但这仅供参考，不影响脚本执行。

你可以通过 DDL 生成对话框底部的“保存配置”（`Save Configuration`）按钮保存配置，配置将保存在 XML 文件中。以后可以通过“加载配置”（`Load Configuration`）按钮获取这些设置。此功能非常有用；例如，当你找到了适用于测试数据库的设置组合，只需保存配置即可。记得命名配置文件以便区分哪一个。

# 178 Oracle SQL Developer Data Modeler 数据库设计精通

![](img/431f8ac8f273fa89a28377c500ed60d7_204_0.png)

图 7-7. 包含表脚本标签卡

如果你想生成 DDL，请点击 OK。如果你想取消，点击取消。

当你点击 OK 后，你将返回 DDL 文件编辑器屏幕，但这次它不是空的。你将看到根据你定义的参数生成的所有对象的 DDL 子句。设计规则也会自动检查，因此你可能会收到一条提示错误的消息，你应该检查设计规则以获取详细信息。在 DDL 文件编辑器中，你可以向上向下滚动代码，可以保存 DDL 文件（记住偏好“默认 DDL 文件导出目录”定义了该目录的默认值），可以点击“查找”搜索文件字符串，或者点击“清除”清除屏幕代码。

> 提示
> 保存 DDL 文件时，记得为文件名添加扩展名，例如 `Customer.sql`。

从 4.1 版本开始，你可以使用转换脚本自定义 DDL 生成。通过转换脚本，你可以动态生成 DDL 为你的对象添加前缀/后缀，或完全替换它们。例如，可以在 DDL 中生成表后，立即创建日志表。
