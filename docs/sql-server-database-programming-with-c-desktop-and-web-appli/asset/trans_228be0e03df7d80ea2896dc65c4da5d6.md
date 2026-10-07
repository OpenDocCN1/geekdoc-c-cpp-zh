

# 使用 C#.NET 插入数据

| SelectWizard 项目 | CurrentFaculty() |

```csharp
private int CurrentFaculty()
{
    int result = 0; index;
    facultyTableAdapter.ClearBeforeFill(true);
    facultyTableAdapter.Fill(cSE_DEPTDataSet.Faculty);
    if (cSE_DEPTDataSet.Faculty.Count != 0)
    {
        ComboName.Items.Clear();
        for (index = 0; index < cSE_DEPTDataSet.Faculty.Count; index++)
            ComboName.Items.Add(cSE_DEPTDataSet.Faculty.Rows[index].ItemArray[1].ToString());
        ComboName.SelectedIndex = 0;
        return result;
    }
    else
        return result++;
}
```

**图 6.7** CurrentFaculty() 方法的代码。

在 **for** 循环中，字母作为循环，用于从我们示例数据库的 **Faculty** 表中获取所有选定的教职人员名称。

- B. 在执行 **Fill() 方法** 之前，会清空 TableAdapter。

- C. 执行 **Fill() 方法**，通过从示例数据库中检索教职人员记录来填充 DataSet 中的 **Faculty** 表。

- D. 通过检查已填充的 **Faculty** 表中的 **Count** 属性，我们可以确认填充操作是否成功。如果 **Count** 属性非零，意味着至少检索到了一行数据且填充操作正常，我们需要选取所有查询的数据列，并将它们显示在教职人员名称组合框 **ComboName** 中。在执行此操作之前，我们首先需要使用 **Clear() 方法**确保组合框是空的。

- E. 使用 **for** 循环以 **Count** 属性为上限来获取所有查询的教职人员名称。所有检索到的教职人员名称都将使用 **Add() 方法** 添加到组合框 **ComboName** 中。一个关键问题是使用 **Fill() 方法** 从所有查询的教职人员记录中找到并定位所需的教职人员列。这里我们使用了 **Rows[index]**，并且 **ItemArray[1]** 用于查找此位置。**Rows[index]** 可以视为 **Column[1]**，即 **Faculty** 表中的第二列或 **faculty_name**，而 **Column[0]** 是 **Faculty** 表中的第一列 **faculty_id**。**index** 起循环的作用，用于计数并选取 **Faculty** 表中的所有数据行。

- F. 在所有教职人员名称都添加到组合框后，选择第一个教职人员名称作为默认项。

- G. 返回值为 0 的结果给调用方法，表示该方法执行失败。

- H. 否则，返回值为 1 表示该方法失败。

我们使用默认查询方法 **Fill()** 的原因是，该方法根据主架构查询所有列，不会遗漏 **Faculty** 表中的任何列，且我们不需要创建任何新的查询方法。另一个原因是我们无法仅查询或选择所需的列，例如在我们的案例中，如果只需要查询 **faculty_name** 列。但我们无法这样做，必须从此 Faculty 表中选择所有列，因为 DataSet 和 Adapter 的主架构是要求全选择的。否则，可能会遇到某些不匹配的查询。

# 318 使用 C# 进行 SQL Server 数据库编程

## 6.2.5 数据插入的初始化编码

在本节中，我们需要为以下内容构建代码：

- Form_Load 方法的代码，通过添加和显示两种插入方法 TableAdapter.Insert() 和 TableAdapter.Update() 来初始化组合框 ComboMethod，因为我们希望使用两个方法来执行此数据插入操作。

当项目运行并显示 Faculty 表单时，此框中应显示两个方法，允许用户执行数据插入，即执行任一方法。在此执行此之前，我们首先需要确保组合框是空的，使用 **Clear() 方法**。

当项目运行并显示 Faculty 表单时，此框中应显示两个方法，允许用户执行数据插入，即执行任一方法。在此操作之前之前，首先首先需要组合组合框使用 **使用****。。。。。显示显示显示，，，，，，，，，，，，，，，，，。，.，，，。，.，。。。。。。。。。，。。..，.。.。。。。。。。。。。 ...   .. 所示。

**图 6.8** Form_Load 的添加代码。

# 使用 C#.NET 插入数据

## 6.2.6 使用 TableAdapter.Insert() 构建插入查询

为了使用 TableAdapter.Insert() 访问数据库，我们需要首先配置 TableAdapter 并构建查询：

1) 打开 Data Sources 窗口。
2) 在打开的窗口中，点击 Designer 按钮打开设计器。然后右键点击 Faculty 表并选择 Add Query 项。
3) 保持默认选择，使用 SQL 语句，并点击 Next 按钮进入下一步。
4) 选择并检查插入项，然后点击 Next。
5) 点击 Query Builder 构建我们的查询。打开的 Query Builder 如图 6.9 所示。
6) 我们要插入包含 faculty_name、office、email 和 fimage 信息的新记录。点击 OK 按钮进入下一步。
7) 点击 Next 确认查询并继续。
8) 将查询名称修改为 InsertFaculty 并点击 Next 按钮进入最后一步。
9) 点击 Finish 完成查询并关闭向导。

你会发现一个新的查询函数已作为最后一项添加到 FacultyTableAdapter。

**图 6.9** 打开的查询生成器。

# 使用 C# 进行数据库编程

现在我们已经完成了 TableAdapter 的配置和插入查询的构建，是时候编写代码来运行 TableAdapter 以完成此数据插入查询了。

现在让我们开始编写 DBDirect 方法，**首先我们需要为第一个方法开发代码，使用 TableAdapter.Insert()**

## 6.2.7 使用 TableAdapter.Insert 开发插入数据的代码

打开表单的 GUI，然后双击 **Insert** 按钮打开其 Click 方法，代码如图 6.10 所示。

回顾一下我们在 6.2.3.2 节中为该方法创建了一些代码以执行数据验证，因此这些代码以灰色背景显示。

让我们看看这段新代码是如何工作的。

- A. 在这里声明了一个本地[] bimage 数组和一个整数 int，前者用于存储插入到我们 faculty 表中的选定教职人员图像，后者用于存储执行 **TableAdapter.Insert()** 方法的返回值。此返回值表示在数据库中成功插入或影响的记录数，可用于判断此数据插入是否成功影响了数据库；否则，插入失败。

**图 6.10** 修改后的插入点击方法代码。

