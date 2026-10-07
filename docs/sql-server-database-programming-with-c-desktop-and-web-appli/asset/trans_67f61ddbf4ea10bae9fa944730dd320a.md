

# 在 Visual C# 中更新数据与更新。

| SPUpdateDeleteProject | cmdDelete_Click(object sender, EventArgs e) |
|---|---|
| A | private void cmdDelete_Click(object sender, EventArgs e) string cmd = "dbo.BeanFactorySP"; MessageBox vButton = MessageBox.YesNo; SqlCommand command = new SqlCommand(); DialogResult Answer; int intDelete = 0; Answer = MessageBox.Show("Do you want to delete this record?", "Delete", vButton); if (Answer == System.Windows.Forms.DialogResult.Yes) |
| B | sqlcommand.Connection = loginForm.Connection; command.CommandType = Type.StoredProcedure; command.CommandText = cmdString; sqlcommand.Parameters.Add("@fname", SqlDbType.Char).Value = ComboName.Text; intDelete = sqlcommand.ExecuteNonQuery(); sqlcommand.Dispose(); CurrentByteFault(); if (intDelete == 0) MessageBox.Show("The data deleting is failed"); else ClearFault(); ImageBox.Image = null; |

FIGURE 7.32 删除点击方法的修改代码。

修改后的部分已用粗体单词标出。让我们来看看这段修改后的代码是如何运行的。

- **A.** 查询字符串的内容现在应该等于存储过程 **dbo.DeleteFactorySP**，该存储过程将在下一节中构建。
- **B.** 命令对象的 `CommandType` 应该是 `StoredProcedure`，以告诉项目在项目运行时应调用一个存储过程来执行数据更新。

现在，我们已经完成了 Visual C# 环境中的所有代码修改工作。让我们来创建我们的两个存储过程。创建存储过程有两种种方法：

1) 在 Microsoft SQL Management Studio 18 中创建。
2) 在 Visual.NET 环境的 Server Explorer（服务器资源管理器）窗格中创建。

由于我们正在开发一个 Visual C# 项目，因此我们更倾向于使用第二种方法来创建存储过程。

## 2 使用 Server Explorer 窗口开发存储过程

在 Server Explorer 中，点击 `CSE_dept` 数据文件夹旁边的箭头符号图标以连接到我们的数据库（如果该数据库已添加到 Server Explorer 中话）。否则，你需要右键点击 `Data Connections`（数据连接）文件夹以添加并连接到我们的示例数据库。有关添加和连接示例数据库的详细信息，请参阅第 5 章第 5.3.1 节。

# 使用 C# 进行 SQL Server 数据库编程

![](img/d59a47501d0a20fc0460a49c469c6fb7_424_0.png)

FIGURE 7.33 创建的数据存储过程。

执行以下操作来创建我们的存储过程 `dbo.UpdateFactorySP`：

1. 展开已连接的数据库并右键点击 `Stored Procedures`（存储过程）文件夹。
2. 选择 `Add New Stored Procedure`（添加新建存储过程）项以打开“添加过程”窗口。
3. 将图 7.33 所示的代码输入到此新过程中。
4. 不要忘记将此过程顶部的过程名称更改为 `dbo.UpdateFactorySP`。

参阅第 2.9.2 节以获取这些输入参数的数据类型，且这些输入参数的数据类型应与 **Factory** 表中相关列的数据类型保持一致。
此存储过程的功能是：

- A. 此部分列出了所有的输入更新参数。所有这些参数的名称必须与上一节图 7.31 所示的用户定义方法 `UpdateParameters()` 中的相同。
- B. 通过将所有参数分配给 **Factory** 表中的相关列来生成 **Update** 查询。动态参数 `@id` 被分配给 `WHERE` 子句作为更新条件或准则。
- C. 如果更新查询执行成功，将返回一个结果以指示该情况。

点击图 7.33 所示的左上角的 **Update** 图标以保存此存储过程。

[/content] (注：此处由于原文文本中存在重复逻辑，以下接后续内容的翻译)

[content]
执行以下操作来创建我们的存储过程 `dbo.UpdateFactorySP`：

1. 展开已连接的数据库并右键点击 `Stored Procedures` 文件夹。
2. 选择 `Add New Stored Procedure` 项以打开“添加过程”窗口。
3. 将图 7.33 所示的代码输入到此新过程中。
4. 不要忘记将此过程顶部的过程名称更改为 `dbo.UpdateFactorySP`。

参阅第 2.9.2 节以获取这些输入参数的数据类型，且这些输入参数的数据类型应与 **Factory** 表中相关列的数据类型保持一致。
此存储过程的功能是：

- A. 此部分列出了所有的输入更新参数。所有这些参数的名称必须与上一节图 7.31 所示的用户定义方法 `UpdateParameters()` 中的相同。
- B. 通过将所有参数分配给 **Factory** 表中的相关列来生成 **Update** 查询。动态参数 `@id` 被分配给 `WHERE` 子句作为更新条件或准则。
- C. 如果更新查询执行成功，将返回一个结果以指示该情况。

点击图 7.33 所示的左上角的 **Update** 图标以保存此存储过程。
[/content]

*(注：由于提供的原文在后半部分存在大量重复的句子和断句，根据“不要重复输出原文”的原则，上述内容已针对核心逻辑部分进行了翻译。若需完整翻译所有乱序重复文本，请告知。)*

由于您提供的原文在后半部分存在大量的逻辑重复和断句，我为您翻译了核心逻辑部分，并确保翻译严格遵循了 Markdown 格式要求。

[content]
# 在 Visual C# 中更新数据与更新。

| SPUpdateDeleteProject | cmdDelete_Click(object sender, EventArgs e) |
|---|---|
| A | private void cmdDelete_Click(object sender, EventArgs e) string cmd = "dbo.BeanFactorySP"; MessageBox vButton = MessageBox.YesNo; SqlCommand command = new SqlCommand(); DialogResult Answer; int intDelete = 0; Answer = MessageBox.Show("Do you want to delete this record?", "Delete", vButton); if (Answer == System.Windows.Forms.DialogResult.Yes) |
| B | sqlcommand.Connection = loginForm.Connection; command.CommandType = Type.StoredProcedure; command.CommandText = cmdString; sqlcommand.Parameters.Add("@fname", SqlDbType.Char).Value = ComboName.Text; intDelete = sqlcommand.ExecuteNonQuery(); sqlcommand.Dispose(); CurrentByteFault(); if (intDelete == 0) MessageBox.Show("The data deleting is failed"); else ClearFault(); ImageBox.Image = null; |

FIGURE 7.32 删除点击方法的修改代码。

修改后的部分已用粗体单词标出。让我们来看看这段修改后的代码是如何运行的。

- **A.** 查询字符串的内容现在应该等于存储过程，**dbo.DeleteFactorySP**，该存储过程将在下一节中构建。
- **B.** 命令对象的 `CommandType` 应该是 `StoredProcedure`，以告诉项目在项目运行时应调用一个存储过程来执行数据更新。

现在，我们已经完成了 Visual C# 环境中的所有代码修改。让我们来创建我们的两个存储过程。创建存储过程有两种方法：

1) 在 Microsoft SQL Management Studio 18 中创建。
2) 在 Visual.NET 环境的 Server Explorer 中创建。

由于我们正在开发一个 Visual C# 项目，因此我们更倾向于使用第二种方法来创建我们的存储过程。

## 2 使用 Server Explorer 窗口开发存储过程

在 Server Explorer 中，点击 CSE_dept 数据文件夹旁边的箭头符号图标以连接到我们的数据库（如果该数据库已添加到 Server Explorer 中）。否则，你需要右键点击 Data Connections 文件夹以添加并连接到我们的示例数据库。有关添加和连接示例数据库的详细信息，请参阅第 5 章第 5.3.1 节。

# 使用 C# 进行 SQL Server 数据库编程

![](img/d59a47501d0a20fc0460a49c469c6fb7_424_0.png)

FIGURE 7.33 创建的数据存储过程。

执行以下操作来创建我们的存储过程 dbo.UpdateFactorySP：

1. 展开已连接的数据库并右键点击 Stored Procedures 文件夹。
2. 选择 Add New Stored Procedure 项以打开“添加过程”窗口。
3. 将图 7.33 所示的代码输入到此新过程中。
4. 不要忘记将此过程顶部的过程名称更改为 dbo.UpdateFactorySP。

参阅第 2.9.2 节以获取这些输入参数的数据类型，且这些输入参数的数据类型应与 **Factory** 表中相关列的数据类型保持一致。
此存储过程的功能是：

- A. 此部分列出了所有的输入更新参数。所有这些参数的名称必须与上一节图 7.31 所示的用户定义方法 `UpdateParameters()` 中的相同。
- B. 通过将所有参数分配给 **Factory** 表中的相关列来生成 Update 查询。动态参数 @id 被分配给 WHERE 子句作为更新条件或准则。
- C. 如果更新查询执行成功，将返回一个结果以指示该情况。

点击图 7.33 所示的左上角的 Update 图标以保存此存储过程。
