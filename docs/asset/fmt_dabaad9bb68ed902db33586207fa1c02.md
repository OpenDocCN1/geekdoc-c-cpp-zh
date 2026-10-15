
EDM 生成器工具提供五种模式来执行特定功能，如表 22.8 所列：

**表 22.8**：EDM 生成器工具的模式

| Mode | Description |
|---|---|
| `/mode:ValidateArtifacts` | 至少需要一个 `/inssdl` 或 `/incsdl` 参数。如果指定了 `/inmsl`，则也需要 `/inssdl` 和 `/incsdl` 参数。您可以指定此模式以验证 `.csdl`、`.ssdl` 和 `.msl` 文件中的错误或警告并显示它们。 |
| `/mode:FullGeneration` | 需要 `/connectionstring` 参数以及 `/project` 参数或 `/outcsdl`、`/outssdl`、`/outmsl`、`/outobjectlayer`、`/outviews`、`/namespace` 和 `/entitycontainer` 参数。此模式使用 `/connectionstring` 选项中指定的数据库信息生成 `.csdl`、`.ssdl`、`.msl`、对象层和视图文件。 |
| `/mode:FromSSDLGeneration` | 需要 `/inssdl` 参数以及 `/project` 参数或 `/outcsdl`、`/outmsl`、`/outobjectlayer`、`/outviews`、`/namespace` 和 `/entitycontainer` 参数。此模式从指定的 `.ssdl` 文件生成 `.csdl` 和 `.msl` 文件、源代码和视图。 |
| `/mode:EntityClassGeneration` | 需要 `/incsdl` 参数以及 `/project` 参数或 `/outobjectlayer` 参数。`/language` 参数是可选的。此模式创建包含从 `.csdl` 文件生成的类的源代码文件。 |
| `/mode:ViewGeneration` | 需要 `/inssdl`、`/incsdl`、`/inmsl` 以及 `/project` 或 `/outviews` 参数。`/language` 参数是可选的。此模式创建包含从 `.ssdl`、`.csdl` 和 `.msl` 文件生成的视图的源代码文件。 |

表 22.9 列出了 `EdmGen.exe` 工具的重要选项：

**表 22.9**：`EdmGen.exe` 工具的选项

| Option | Description |
|---|---|
| `/p[roject]:<string>` | 指定与 `EdmGen.exe` 工具一起使用的项目名称。默认情况下，项目名称用作命名空间。项目名称还用于 EDM 文件的名称和视图生成源文件的名称。 |
| `/c[onnectionstring]:<connection string>` | 指定用于连接到数据源的连接字符串。 |
| `/incsdl:<file>` | 指定 `.csdl` 文件或包含 `.csdl` 文件的目录。如果要指定多个目录或 `.csdl` 文件，可以多次使用此参数。它主要在实体类或视图生成期间使用。 |
| `/refcsdl:<file>` | 在从源 `.csdl` 文件引用另一个 `.csdl` 文件时需要。此参数可以多次指定。 |
| `/inmsl:<file>` | 指定 `.msl` 文件或 `.msl` 文件的位置。如果要指定多个目录或 `.msl` 文件，可以多次使用此参数。它主要在实体类或视图生成期间使用。当概念模型被拆分等情况时需要此参数。 |
| `/inssdl:<file>` | 指定 `.ssdl` 文件或 `.ssdl` 文件所在的目录。 |
| `/outcsdl:<file>` | 指定 `EdmGen.exe` 工具将创建的 `.csdl` 文件的名称。 |
| `/outmsl:<file>` | 指定 `EdmGen.exe` 工具将创建的 `.msl` 文件的名称。 |
| `/outssdl:<file>` | 指定 `EdmGen.exe` 工具将创建的 `.ssdl` 文件的名称。 |
| `/outobjectlayer:<file>` | 指定包含从 `.csdl` 文件生成的对象的源代码文件的名称。 |
| `/outviews:<file>` | 指定包含已生成视图的源代码文件的名称。 |
| `/language:[VB\|CSharp]` | 指定生成的源代码文件的语言。默认语言为 C#。 |
| `/namespace:<string>` | 指定要使用的命名空间。运行 `/mode:FullGeneration` 或 `/mode:FromSSDLGeneration` 模式时，命名空间会设置在 `.csdl` 文件中。运行 `/mode:EntityClassGeneration` 模式时不使用命名空间。 |
| `/entitycontainer:<string>` | 指定应用于生成的 EDM 文件中 `<EntityContainer>` 元素的名称。 |

在下一节中，我们学习如何使用实体框架提供的各种工具、模板和向导。

## 立即可用的解决方案

熟悉实体框架及其组件后，让我们进一步学习如何在应用程序中使用此框架。

让我们执行以下步骤来学习在 ASP.NET 4.0 应用程序中使用实体框架：

1. 打开 Microsoft Visual Studio 2010。
2. 创建一个 ASP.NET 网站并将其保存为 `EDMgenerationCS`（也可在光盘上获得）。
3. 在解决方案资源管理器中右键单击 `EDMgeneration` 网站并选择 Add New Item 选项。Add New Item 对话框出现，如图 22.5 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1126_0.png)

**图 22.5**：显示 Add New Item 对话框

> **注意**
>
> 本章中的应用程序使用 New Web Site 对话框中的 ASP.NET Empty Web Site 模板创建。创建应用程序后，您需要向应用程序添加 `Default.aspx` 页面。

因此，如图 22.5 所示，您可以以类似的方式从 Add New Item 对话框中添加 ADO.NET 实体数据模型模板。在“深入”部分中，我们讨论了实体框架提供的工具，例如实体数据模型模板和向导。现在，让我们讨论如何在应用程序中实现这些工具。

### 创建实体数据模型

可以使用 ADO.NET 实体数据模型模板创建 EDM。我们可以使用此模板创建 C# 项目。此模板可以添加到控制台应用程序、Windows 应用程序、类库、ASP.NET Web 服务应用程序、ASP.NET Web 应用程序或 ASP.NET 网站项目中。单个项目可以包含多个实体数据项，这些项可能从不同的数据库或数据库中的不同表生成。现在，执行以下步骤将实体数据模型项模板添加到网站：

1. 在解决方案资源管理器中右键单击网站名称，即 `EDMgenerationCS`，如图 22.6 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1127_0.png)

**图 22.6**：在 `EDMgenerationCS` 网站中添加新项

2. 单击 Add New Item 选项。Add New Item 对话框出现（图 22.7）。

3. 选择 ADO.NET 实体数据模型模板并单击 Add 按钮以将模板包含到 `EDMgenerationCS` 网站中，如图 22.7 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1127_1.png)

**图 22.7**：在 `EDMgenerationCS` 网站中添加实体数据模型项模板

会出现一个消息框，提示您将 ADO.NET 实体数据模型项放置到 `App_Code` 文件夹中（图 22.8）。

4. 单击 Yes 按钮，如图 22.8 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1127_2.png)

**图 22.8**：将文件定位到 `App_Code` 文件夹

在应用程序中创建了 `App_Code` 文件夹。实体数据模型向导开始显示创建模型的两个选项，即 Generate from database 和 Empty model（图 22.9）。

5. 从 Choose Model Contents 页面选择 Generate from database 选项并单击 Next 按钮以从现有数据库生成模型，如图 22.9 所示：

> **注意**
>
> 当我们在 ASP.NET 网站中使用 EDM 工具时，实体连接字符串保存在 `web.config` 文件中；然而，在 Windows 应用程序中，实体连接字符串保存在 `App.config` 文件中。元数据文件的位置指定为 `metadata=res://*/`。因此，请确保选中 Save entity connection settings in web.config as 复选框并指定值（图 22.10）；否则，连接设置将不会被保存。

8. 选择您需要从数据库创建 EDM 的 Tables、Views 和 Stored Procedures 复选框，然后单击 Finish 按钮，如图 22.11 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1129_0.png)

**图 22.11**：选择数据库对象

从 `Northwind` 数据库创建的 EDM 已加载到网站中，如图 22.12 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1129_1.png)

**图 22.12**：显示 EDM 的输出

> **注意**
>
> 在图 22.11 中，Model Namespace 文本框包含 `NORTHWINDModel` 值。这会导致 ADO.NET 运行时从由 ASP.NET 动态编译的程序集中加载 EDM 元数据工件文件，例如 `.csdl` 文件的资源。

EDM 包含我们在选择数据库对象时所选的表、视图和存储过程。向导创建的 `Model.edmx` 文件必须添加到 ASP.NET 网站项目的 `App_Code` 文件夹中。如果我们选择将 `.edmx` 文件重新定位到另一个目录，则模型将不被 ASP.NET 的 EDM 构建提供程序支持。现在，让我们了解如何使用 ADO.NET 实体数据模型设计器。

## 使用实体数据模型设计器

ADO.NET 实体数据模型设计器使用 `.edmx` 文件工作，该文件是对 CSDL、SSDL 和 MSL 文件的封装。此 `.edmx` 文件在创建 EDM 后创建并添加到我们的项目中。我们可以通过使用 ADO.NET 实体数据模型设计器通过 `.edmx` 文件对 EDM 进行更改。要打开 EDM 设计器，请在解决方案资源管理器中双击 `Model.edmx` 文件，如图 22.13 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1130_0.png)

**图 22.13**：在 `App_Code` 文件夹中显示 `Model.edmx` 文件

EDM 设计器窗口出现（图 22.14）。它为编辑概念模型提供了一个设计表面，该模型提供用于处理实体的功能。现在让我们了解以下窗口：

- Model Browser
- Mapping Details

## 使用实体模型浏览器窗口

模型浏览器窗口以两个节点显示信息。第一个节点显示概念模型的详细信息。我们可以展开其下方的节点以查看模型中包含的所有实体类型和关联。第二个节点显示目标数据库模型的详细信息。图 22.14 显示了模型中使用的数据库表、视图和存储过程的部分内容：

![](img/e073a4882197be4ab61103cbe0bcb394_1130_1.png)

**图 22.14**：使用模型浏览器窗口查看 `Model.edmx` 文件

> **注意**
>
> 您可以通过从菜单栏中单击 View → Other Windows → Entity Data Model Browser 选项来查看模型浏览器窗口。

模型浏览器窗口还提供了创建 CSDL 函数导入条目的功能，该条目用于调用存储过程，并指定函数导入的返回类型。现在，让我们通过执行以下步骤了解如何通过模型浏览器窗口创建函数导入：

1. 在模型浏览器窗口中展开 Stored Procedures 节点（图 22.15）。
   出现可用存储过程的列表。
2. 右键单击列表中的任意存储过程，然后从上下文菜单中选择 Add Function Import 选项，如图 22.15 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1131_0.png)

**图 22.15**：为存储过程创建函数导入

Add Function Import 对话框出现，如图 22.16 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1131_1.png)

**图 22.16**：指定字段

Add Function Import 对话框显示三个字段—— Function Import Name、Stored Procedure Name 和 Returns a Collection Of。Stored Procedure Name 字段指定我们为其创建函数导入的数据库的名称。Function Import Name 字段指定函数导入的名称。Returns a Collection of 字段指定函数导入的返回类型。

通过为这些字段中的每一个指定值，我们可以在存储过程中创建一个 CSDL 函数导入条目。现在，让我们了解如何使用映射详细信息窗口修改数据库对象的映射。

## 使用映射详细信息窗口

映射详细信息窗口使我们能够查看和编辑 EDM 中的映射。我们可以通过在模型浏览器窗口中选择 Entity Types 选项来访问此窗口。映射详细信息窗口显示在模型浏览器窗口中选择的实体对象的映射，如图 22.17 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1132_0.png)

**图 22.17**：显示实体映射详细信息窗口

可以通过映射详细信息窗口执行以下功能：

- 修改实体的映射
- 添加表或视图
- 添加条件

### 修改实体的映射

要在应用程序中修改实体的映射，请执行以下步骤：

1. 从 Column Mappings 文件夹中选择要更改映射的类别名称。
2. 从相邻的下拉列表中选择 `Categories` 表的所需列，如图 22.18 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1132_1.png)

**图 22.18**：修改实体的映射

在图 22.18 中，我们更改了 `CategoryName` 列的映射。

### 添加表或视图

要在应用程序中添加表或视图，请执行以下步骤：

1. 在映射详细信息窗口中选择 `<Add a Table or View>` 选项。会出现一个下拉列表，显示表和视图的列表（图 22.19）。
2. 选择所需的表或视图，如图 22.19 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1133_0.png)

**图 22.19**：添加表或视图

在图 22.19 中，我们选择了 `Customers` 表。Maps to Customers 选项已添加到映射详细信息窗口。在 Map to Customers 选项卡下有两个选项，一个是 `<Add a Condition>`，另一个是 Column Mappings，其中包含表的全部列，如图 22.20 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1133_1.png)

**图 22.20**：显示映射详细信息窗口

### 为字段添加条件

要为列的字段添加条件，我们首先需要启用 `<Add a Condition>` 选项，这可以通过执行以下步骤完成：

1. 在模型浏览器窗口中 Entity Types 文件夹下选择 `Customers` 表，如图 22.21 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1134_0.png)

**图 22.21**：在模型浏览器窗口中选择实体

2. 现在，选择一个列，例如 `City`，我们想在其中放置条件，通过选择 `<Add a Condition>` 选项，如图 22.22 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1134_1.png)

**图 22.22**：添加条件

现在，屏幕显示与 `City` 列关联的条件（图 22.23）。

3. 从下拉列表中选择 When City 子句旁边的 Not Null 选项，如图 22.23 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1134_2.png)

**图 22.23**：选择 Not Null 选项

![](img/e073a4882197be4ab61103cbe0bcb394_1136_0.png)

**图 22.25**：指定实体的属性

在派生实体的情况下，Entity Set Name 字段被禁用。

> **注意**
>
> 我们还可以通过设计器表面（不使用工具箱中的 Entity 控件）创建实体，执行以下步骤：
>
> 1. 在设计器窗口的任意位置右键单击。上下文菜单打开。
> 2. 从上下文菜单中单击 Add → Entity 选项。New Entity Dialog Box 出现（图 22.26）。
> 3. 通过 New Entity 对话框指定实体的属性，如图 22.26 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1136_1.png)

**图 22.26**：显示添加实体对话框

只有在基类型选择为 `None` 时才能创建键属性，而在派生实体的情况下，此选项被禁用。

要删除实体，请右键单击它并从上下文菜单中选择 Delete 选项。现在，让我们了解如何形成实体之间的关联并将其添加到模型中。

## 使用关联控件创建关联

关联定义实体类型之间的关系。关联是双向的，关联中每个参与实体被称为 End。让我们执行以下步骤在 `Customers` 和 `Contact` 实体之间形成关联：

1. 在 `WorkingEntitiesCS` 应用程序中创建另一个实体并将其命名为 `Contact`。
2. 现在，要在 `Customers` 和 `Contact` 实体之间形成关联，请在设计器窗口的任意位置右键单击并从上下文菜单中选择 Add → Association 选项。New Association 对话框出现（图 22.27）。
3. 在 Association Name 字段中输入关联的名称（图 22.27）。在此例中，我们将关联命名为 `CustomersContact`。
4. 从 Multiplicity 下拉列表中为两个实体选择值（图 22.27）。在此应用程序中，我们在 `Customers` 和 `Contact` 实体之间创建一对多多重性。
5. 为两个实体在 Navigation Property 字段中输入值（图 22.27）。
6. 单击 OK 按钮，如图 22.27 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1137_0.png)

**图 22.27**：创建关联

在 `Customers` 和 `Contact` 实体之间形成了关联。您可以看到关联作为一条线，即 `CustomersContact`，连接两个实体，如图 22.28 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1137_1.png)

**图 22.28**：显示两个实体的关联

Entity Framework 允许我们在同一对实体之间形成多于一个的关联。图 22.28 中的第二行显示，`Customers` 和 `Contact` 实体之间除了 One to Many 关联外，还形成了 Many to Many 关联。要删除一个关联，右键单击它并从上下文菜单中选择 Delete 选项。现在，让我们了解 Inheritance 工具。

## Creating an Inheritance by Using the Inheritance Control

继承工具允许一种类型从另一种类型派生，但源端和目标端必须不同。假设我们还有另一个名为 `Vendor` 的实体，我们希望 `Vendor` 和 `Customers` 实体都从 `Contact` 实体继承。在这种情况下，`Contact` 实体是基类型，而 `Vendor` 和 `Customers` 实体称为派生类型。为此，在各自的 Properties 窗口中，从 Base Type 字段将 `Contact` 实体设为 `Vendors` 和 `Customers` 实体的基类型。

三个实体之间的继承关系如图 22.29 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1138_0.png)

在这里，我们学习了如何使用 Toolbox 中的各种控件创建实体，将其与其它实体关联，以及在不同实体之间定义继承。现在，让我们继续基于 EDM 创建 Web 应用程序。

## Creating an EDM-Based Application

在熟悉了 Entity Framework 的所有工具和控件的工作原理后，让我们执行以下步骤来创建一个基于 EDM 的 Web 应用程序：

1. Create an ASP.NET Web site and save it as `Publisher_EntityCS` (also available on the CD).

在此应用程序中，我们使用了一个名为 `NewPublisher` 的数据库。清单 22.1 显示了 `NewPublisher` 数据库的代码：

**Listing 22.1: Showing the Code for the `NewPublisher` Database**

```sql
```
