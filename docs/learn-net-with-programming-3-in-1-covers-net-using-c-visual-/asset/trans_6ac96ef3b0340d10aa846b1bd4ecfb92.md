

| TutorialID | TutorialName |
| 1 | C# |
| 2 | ASP.Net |
| 3 | VB.Net |

让我们更改表单中的代码，以便我们可以更新以下行。旧行的值为 tutorialid 为“3”，Tutorial Name 为“VB.Net”。我们将把它更新为“VB.Net complete”，而 Tutorial ID 的行值保持不变。

## Old Row

| TutorialID | TutorialName |
| 3 | VB.Net |

## New row

| TutorialID | TutorialName |
| 3 | VB.Net Complete |

因此让我们将以下代码添加到我们的程序中。下面的代码片段将用于更新数据库中现有记录。

![](img/e7ca4af023a4148a909dd82c11f81893_232_0.png)

## C# sqlcommand Example: With Code Explanation:-

- 第一步是创建以下变量
- 1. Sqlcommand – 此数据类型用于定义用于对数据库执行 SQL 操作的对象。此对象将保存将针对我们的 SQL Server 数据库运行的 SQL 命令。
- 2. dataadapter 对象用于执行特定的 SQL 操作，例如插入、删除和更新命令。
- 3. 我们然后定义一个字符串变量，即 SQL，用于保存我们的 SQL 命令字符串。

- 下一步是定义将用于针对数据库的 SQL 语句。在我们的例子中，我们发出的是更新语句，这将把 Tutorial name 更新为“VB.Net Complete”，而 tutorialid 保持不变为 3。
- 接下来，我们将创建命令对象，用于针对数据库执行 SQL 语句。在 SQL 命令中，您已传递连接对象和 SQL 字符串。
- 在我们的 data adapter 命令中，我们现在将插入 SQL 命令与适配器关联。我们还发出 executenonquery 方法，该方法用于针对数据库执行 Update 语句。
- 我们最后关闭与数据库操作相关的所有对象。请记住，这始终是一个良好的做法。

当设置上述代码并使用 Visual Studio 执行项目时，您将获得以下输出。表单显示后，单击 Connect 按钮。

Output:-

![](img/e7ca4af023a4148a909dd82c11f81893_234_0.png)

如果您实际进入 SQL Server Express 并查看 demotb 表中的行，您将看到该行已成功更新，如下所示。

![](img/e7ca4af023a4148a909dd82c11f81893_234_1.png)

## Deleting Records

就像访问数据一样，C# 也有能力从数据库中删除现有记录。为了展示如何将记录删除到我们的数据库中，让我们采用上面使用过的相同表结构。

| TutorialID | TutorialName |
|------------|---------------|
| 1 | C# |
| 2 | ASP.Net |
| 3 | VB.Net Complete |

让我们更改表单中的代码，以便我们可以删除以下行

| TutorialID | TutorialName |
|------------|---------------|
| 3 | VB.Net Complete |

因此让我们将以下代码添加到我们的程序中。下面的代码片段将用于从数据库中删除现有记录。

![](img/e7ca4af023a4148a909dd82c11f81893_236_0.png)

## Code Explanation:-

- 此代码的关键区别在于我们现在发出的是 delete SQL 语句。delete 语句用于删除 demotb 表中 tutorialid 值为 3 的行。
- 在我们的 data adapter 命令中，我们现在将插入 SQL 命令与适配器关联。我们还发出 executenonquery 方法，该方法用于针对数据库执行 Delete 语句。

当设置上述代码并使用 Visual Studio 执行项目时，您将获得以下输出。表单显示后，单击 Connect 按钮。

## Output:-

如果您实际进入 SQL Server Express 并查看 demotb 表中的行，您将看到该行已成功删除，如下所示。

## Connecting Controls to Data

![](img/e7ca4af023a4148a909dd82c11f81893_237_0.png)

![](img/e7ca4af023a4148a909dd82c11f81893_237_1.png)

在前面的部分中，我们已经看到如何使用 C# 命令例如 sqlcommand 和 sqlreader 从数据库中获取数据。我们还看到了如何读取表的每一行并使用 messagebox 将表的内容显示给用户。

但显然，用户不想通过消息框查看数据，而是希望有更好的控件来显示数据。让我们采用下面表格中的数据结构

| TutorialID | TutorialName |
|---|---|
| 1 | C# |
| 2 | ASP.Net |
| 3 | VB.Net Complete |

从上述数据结构来看，用户理想情况下希望在文本框中看到 tutorialid 和 Tutorial Name。其次，他们可能希望拥有某种按钮控件，可以让他们转到表中的下一条记录或上一条记录。这需要开发人员进行一些额外的编码。

好消息是 C# 可以通过允许控件与数据绑定来减少额外的编码工作。

这意味着 C# 可以根据表的特定字段自动填充文本框的值。

因此，您可以在 windows 窗体中拥有 2 个文本框。然后您可以将一个文本框链接到 tutorialid 字段，另一个文本框链接到 tutorialname 字段。这种链接是在 Visual Studio 设计器中完成的，您不需要为此编写额外代码。

Visual Studio 将确保为您编写代码以确保链接正常工作。然后当您运行应用程序时，文本框控件将自动连接到数据库，获取数据并在文本框控件中显示。开发人员无需进行任何编码即可实现这一点。

让我们看一个代码示例：如何实现控件绑定。

在我们的示例中，我们将在 windows 窗体上创建 2 个文本框。它们将分别代表 Tutorial ID 和 Tutorial Name。它们将分别绑定到数据库的 Tutorial ID 和 tutorialname 字段。

让我们按照下面提到的步骤来实现这一点。

Step 1) 构建基本窗体。在窗体上拖放 2 个组件-标签和文本框。然后执行以下子步骤

- 将第一个标签的文本值设为 tutorialid
- 将第二个标签的文本值设为 tutorialname
- 将第一个文本框的名称属性设为 txtid
- 将第二个文本框的名称属性设为 txtname

下面是执行上述步骤后窗体的外观。

![](img/e7ca4af023a4148a909dd82c11f81893_240_0.png)

Step 2) 下一步是向窗体添加 binding Navigator。binding Navigator 控件可以自动浏览表的每一行。要添加 binding navigator，只需转到工具箱并将其拖到窗体上。

![](img/e7ca4af023a4148a909dd82c11f81893_240_1.png)

## Step 3

下一步是向我们的数据库添加绑定。这可以通过转到任何文本框控件并单击 datagridbindings->Text 属性来完成。Binding Navigator 用于在应用程序和数据库之间建立链接。

当您执行此步骤时，Visual Studio 将自动向应用程序添加所需代码，以确保应用程序与数据库链接。通常 Visual Studio 中的数据库被称为项目数据源。因此，为了确保应用程序和数据库之间建立连接，第一步是创建项目数据源。

以下屏幕将显示。单击链接-“Add Project Data Source”。当您单击项目数据源时，您将看到一个向导；这将允许您定义数据库连接。

![](img/e7ca4af023a4148a909dd82c11f81893_241_0.png)

> Click on Add Project Data

Step 4) 一旦您单击 Add Project Data Source 链接，您将被提供一个向导，该向导将用于创建到 demoth 数据库的连接。以下步骤详细说明了在向导的每个步骤中需要配置的内容。

- • 在弹出的屏幕中，选择数据源类型为 Database，然后单击下一步按钮。

![](img/e7ca4af023a4148a909dd82c11f81893_242_0.png)

- • 在下一个屏幕中，您需要开始创建到数据库的连接字符串。连接字符串对于应用程序建立到数据库的连接是必需的。它包含

