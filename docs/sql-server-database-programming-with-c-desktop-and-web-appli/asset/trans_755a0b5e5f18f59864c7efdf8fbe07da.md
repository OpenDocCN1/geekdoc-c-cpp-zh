

# 使用 Visual C# 进行数据更新和删除

在恢复已删除的记录时，另一个重要点是执行这些恢复任务的顺序。你必须首先从父表 `Faculty` 表中恢复被删除的教员记录，然后才能恢复所有其他子表中的任何相关记录。这是因为 `Faculty` 是以 `faculty_id` 为主键的父表，如果不先恢复父表中的被删除记录，你将无法恢复任何其他记录。

为了避免恢复时出现问题，我们倾向于删除一些新插入的教员记录。记得在第 6 章第 6.2.8 节，我们插入了一位名为 Steve Wang 的新教员，其数据项如下：

| Faculty ID: | W56788 |
|---|---|
| Faculty Name: | Steve Wang |
| Title: | Professor |
| Office: | MTC-311 |
| Phone: | 750-378-2258 |
| College: | University of Miami |
| Email: | swang@college.edu |
| Faculty Image | Wang.jpg |

删除此记录的主要原因是其他任何表中都没有记录与此新插入的教员相关，这使得恢复工作变得更加简单直接。在执行此删除操作之前，运行我们当前的项目以向示例数据库中的 `Faculty` 表中插入记录。

现在进入 `Faculty Name` 组合框，可以找到新插入的教员 Steve Wang。选择该教员并点击 `Delete` 按钮以从 `Faculty` 表中删除此记录。然后点击消息框，所有显示在七个 `TextBox` 中的教员信息都会消失。我们的数据删除成功了吗？为了回答这个问题，在框中无法找到 `Faculty Name` 组合框和已删除的教员 Steve Wang，这意味着带有所有信息的教员已成功从 `Faculty` 表中删除。是的，我们的数据删除成功了。

确认此删除操作的另一种方法是从“服务器资源管理器（Server Explorer）”窗口打开 `Faculty` 表进行此类检查。

一个完整的项目 `SPUpdateDelete` 可以在 `Class DB Projects\Chapter 7\SPUpdateDelete Solution` 文件夹中找到，该文件夹位于 CRC-fps.com 站 `Students` 文件夹下（参见第 1 章图 1）。

# 7.6 使用 LINQ to SQL 查询对数据库进行更新和删除

正如我们在第 4 章讨论过的，LINQ to SQL 查询可以执行各种数据查询操作，包括数据选择、数据插入、数据更新和删除操作。标准的 LINQ to SQL 查询包括以下四种查询：

- Select（选择）
- Insert（插入）
- Update（更新）
- Delete（删除）

为了执行这些操作或查询操作，我们需要使用第 4 章第 4.6 节中讨论的实体类和 `DataContext` 来对我们的示例数据库执行 LINQ to SQL 操作。为了简单起见，在本节中，我们想使用第 5 章构建的现有 `LINQSelect` 项目将其作为一个新项目，使用 LINQ to SQL 查询对我们示例数据库 `CSE_DEPT` 中的 `Faculty` 执行数据更新和删除操作。我们将数据插入的代码留给读者作为作业。

现在让我们执行以下步骤来创建我们新的 `LINQSelect` 项目：

1) 如果你的本地机器上没有，请创建一个新文件夹 `C:\Chapter 7`。
2) 浏览到 `LINQSelect Solution` 解决方案，它是在第 5 章开发的，位于 CRC 站 `Students` 文件夹下的 `ClassDB Projects\Chapter 5` 文件夹（参见第 1 章图 1.2）。
3) 复制此项目文件夹并粘贴到你的新文件夹 `C:\Chapter 7` 中。

我们可以将其作为我们的新项目，对示例数据库中的 `Faculty` 表执行数据更新和删除功能。

我们选择这个新项目的原因是我们不需要创建任何新的数据实体类 `CSE_DEPTDataContext` 和数据库模型 `CSE_DEPT.dbml` 组件，而是使用现有的对象来节省时间和精力。

现在让我们考虑数据更新和删除操作的代码。打开 Visual Studio，打开我们新项目 `LINQSelect` 的 `Form` 窗口。为了执行这些操作或查询，我们需要使用第 4 章第 4.6 节讨论的实体类和 `DataContext` 对我们的示例数据库执行 LINQ to SQL 操作。为了简单起见，在本节中，我们想使用第 5 章构建的现有 `LINQSelect` 项目将其作为一个新项目，使用 LINQ to SQL 查询对我们示例数据库 `CSE_DEPT` 中的 `Faculty` 执行数据更新和删除操作。我们将数据插入的代码留给读者作为作业。

现在让我们执行以下步骤来创建我们新的 `LINQSelect` 项目：

1) 如果你的本地机器上没有，请创建一个新文件夹 `C:\Chapter 7`。
2) 浏览到 `LINQSelect Solution` 解决方案，它是在第 5 章开发的，位于 CRC 站 `Students` 文件夹下的 `ClassDB Projects\Chapter 5` 文件夹（参见第 1 章图 1.2）。
3) 复制此项目文件夹并粘贴到你的新文件夹 `C:\Chapter 7` 中。

我们可以将其作为我们的新项目，对示例数据库中的 `Faculty` 表执行数据更新和删除功能。

我们选择这个新项目的原因是我们不需要创建任何新的数据实体类 `CSE_DEPTDataContext` 和数据库模型 `CSE_DEPT.dbml` 组件，而是使用现有的对象来节省时间和精力。

现在让我们考虑数据更新和删除操作的代码。打开 Visual Studio，打开我们新项目 `LINQSelect` 的 `Form` 窗口。为了执行这些操作或查询，我们需要使用第 4 章第 4.6 节讨论的实体类和 `DataContext` 对我们的示例数据库执行 LINQ to SQL 操作。为了简单起见，在本节中，我们想使用第 5 章构建的现有 `LINQSelect` 项目将其作为一个新项目，使用 LINQ to SQL 查询对我们示例数据库 `CSE_DEPT` 中的 `Faculty` 执行数据更新和删除操作。我们将数据插入的代码留给读者作为作业。

现在让我们执行以下步骤来创建我们新的 `LINQSelect` 项目：

1) 如果你的本地机器上没有，请创建一个新文件夹 `C:\Chapter 7`。
2) 浏览到 `LINQSelect Solution` 解决方案，它是在第 5 章开发的，位于 CRC 站 `Students` 文件夹下的 `ClassDB Projects\Chapter 5` 文件夹（参见第 1 章图 1.2）。
3) 复制此项目文件夹并粘贴到你的新文件夹 `C:\Chapter 7` 中。

我们可以将其作为我们的新项目，对示例数据库中的 `Faculty` 表执行数据更新和删除功能。

我们选择这个新项目的原因是我们不需要创建任何新的数据实体类 `CSE_DEPTDataContext` 和数据库模型 `CSE_DEPT.dbml` 组件，而是使用现有的对象来节省时间和精力。

现在让我们考虑数据更新和删除操作的代码。打开 Visual Studio，打开我们新项目 `LINQSelect` 的 `Form` 窗口。

# 7.6.1 修改教员构造函数的代码（MODIFYING THE CODES FOR THE FACULTY CONSTRUCTOR）

为了执行这些操作或查询，我们需要使用第 4 章第 4.6 节讨论的实体类和 `DataContext` 对我们的示例数据库执行 LINQ to SQL 操作。为了简单起见，在本节中，我们想使用第 5 章构建的现有 `LINQSelect` 项目将其作为一个新项目，使用 LINQ to SQL 查询对我们示例数据库 `CSE_DEPT` 中的 `Faculty` 执行数据更新和删除操作。

为了让教员显示出来，修改教员构造函数的代码如下：

```csharp
private void CurrentFaculty()
{
LogInfof logForm = new LogInfof();
ComboName.Items.Clear();
var f_info = from f in logForm.Facies
select f;
foreach (var f in f_info)
ComboName.Items.Add(f.faculty_name);
ComboName.SelectedIndex = 0;
logForm.Close();
}
```

# 7.6.2 使用 SQO 方法构建定义的 CURRENTULTY 方法（BUILD THE USER-DEFINED METHOD CURRENTULTY WITH SQO METHOD）

我们在第 6 章第 6.2.4 和 6.5.2 节通过两种不同的方法 `DataAdapter` 和 `SqlDataReader` 执行过此方法，现在我们使用 LINQ 执行更新操作，然后我们需要使用 SQO 方法来构建它。在打开的 `Form` 窗口中，现在将图 7.37 所示的代码输入到方法中：

```csharp
private void UpdateFaculty()
{
byte[] img = getFacultyImage();
LogInfof logForm = new LogInfof();
// ... 后续代码
}
```

# 7.6.3 开发更新按钮点击的代码（DEVELOP THE CODES FOR THE UPDATE BUTTON CLICK METHOD）

双击 `Form` 窗口中的 `Update` 按钮打开其 `Click` 方法，并将图 7.38 所示的代码输入到此处。

