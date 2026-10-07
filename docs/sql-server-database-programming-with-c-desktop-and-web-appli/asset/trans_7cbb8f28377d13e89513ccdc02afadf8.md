

# 392
使用 C# 进行 SQL Server 数据库编程

表，然后你就可以恢复所有子表中的相关记录。这是因为 Course 是一张主表，以 `course_id` 为主键，如果不先从主表中恢复被删除的记录，你就无法恢复任何其他记录。

完成这些恢复操作后，点击“文件 | 保存所有”（File | Save All）菜单项以保存这些恢复的记录。

你可以在 CRC Press 网站的 Students 文件夹下的 `DB Projects\Chapter 7\RTOUpdateDeleteSolution` 文件夹中找到一个完整的 RTOUpdateDelete 项目，该项目包含了 Course 表的更新和删除功能（参见第 1 章中的图 1.2）。

## 7.5 使用存储过程从数据库中更新和删除数据

如前面的节所述，在相关表之间执行数据更新是一项非常有挑战性的工作。好消息是，如果我们想将 Faculty 表中的任何其他信息更新到数据库，大多数不需要更新主键或 Faculty 表中的 `faculty_id`。基本上，在 Faculty 表中插入一条带有新 `faculty_id` 的新记录，比更新现有记录（包括主键 `faculty_id`）更好，因为主键 `faculty_id` 在实际应用中对于数据库的寿命是有利的。根据上述分析，在本节中我们将对 Faculty 表中除 `faculty_id` 外的所有列执行数据更新。

要删除相关表中的记录，我们需要执行两个步骤：首先，我们需要删除子表中的记录，然后就可以从主表中删除记录。例如，如果我们想删除 Faculty 表中的一条记录，首先需要通过 `Login` 和 `Course` 表（子表）删除与 Faculty 表中该记录相关的记录，然后就可以从 Faculty 表（主表）中删除该记录。

为了节省空间，我们可以修改现有项目使其成为我们的新项目。

### 7.5.1 使用存储过程对 SQL Server 数据库进行更新和删除

使用在 SQL Server 数据库中开发的存储过程进行更新和删除数据与我们在上一节中执行的数据更新和删除非常相似。通过对现有的 RTOUpdateDelete 项目进行细微修改，我们可以轻松地创建新项目 `SPupdatedeleteProject`，通过调用 SQL Server 数据库中的存储过程来执行数据更新和删除。

为了在此开发新项目，我们将其分为三个部分：

- 1) 修改现有的 RTOUpdateDelete 项目以创建我们的新项目 `SPupdatedelete Project`。
- 2) 在 SQL Server 数据库中开发数据更新和删除的存储过程。
- 3) 使用 Faculty 表窗口调用存储过程，执行教师信息的数据更新和删除功能。

现在让我们从第一步开始。

### 7.5.1.1 修改现有项目创建我们的新项目

打开 Windows 资源管理器，如果在本地机器上还没有 `C:\Chapter 7`，请创建一个，然后浏览到 CRC Press ftp 站点上的 `Students\Class DB Projects\Chapter 7` 文件夹（参见第 1 章中的图 1.2）。复制整个 `RTOupdateDelete Data Updating and Deleting with Visual C#. Solution` 解决方案文件夹并粘贴到我们的新文件夹 `C\Chapter 7` 中。执行以下操作使其成为项目：

- 1) 将解决方案和项目名称从 `RTOUpdateDeleteSolution` 更改为 `SPUpdateDeleteSolution`，从 `RTOUpdateDeleteProject.csproj` 更改为 `SPUpdateDeleteProject.csproj`。
- 2) 同样将 `RTOUpdateDeleteProject.csproj` 更改为 `SPUpdateDeleteProject.csproj`。然后双击项目 `Project |SPUpdateDeleteProject.csproj` 打开它。
- 3) 转到菜单项 `SPUpdateDeleteProject Properties` 更改项目窗口。将程序集名称（Assembly name）和默认名称（Default name）分别更改为 `SPUpdateDeleteProject` 和 `SPUpdateDeleteProject`。
- 4) 点击程序信息（Assembly Information）按钮更新程序信息向导，将标题（Title）和产品（Product）更改为 `SPUpdateDeleteProject`。点击 OK 按钮关闭它。
- 5) 使用重命名对话框将所有表单窗口（包括 `Login.cs`、`Faculty`、`Course.cs`、`Selection.cs` 和 `Student.cs`）以及相关的类 `Designer.cs` 项目从 `RTO UpdateDelete_Project` 更改为 `SPUpdateDelete_Project`。
- 6) 从解决方案管理器中双击 `CProgram.cs` 打开它，并将命名空间更改为 `SPUpdateDelete_Project`。

进入“文件 | 保存所有”以保存这些修改。再次点击“保存”、“覆盖”和“保存”按钮以保存此项目。现在我们准备好修改新项目中的代码，通过调用存储过程执行数据更新和删除操作。代码修改包括以下部分：

- 1) 将 Faculty 表中 Update 按钮的 `Click` 方法中的查询字符串替换为下一节将开发的数据更新存储过程的名称，以便该方法调用相关的存储过程来执行数据更新操作。
- 2) 将 Faculty 表中 Delete 按钮的 `Click` 方法中的查询字符串替换为下一节将开发的数据删除存储过程的名称，以便该方法调用相关的存储过程来执行数据删除操作。

通常情况下，在 SQL 数据库中创建存储过程后，应该执行这两项修改，因为我们从创建的存储过程中知道了某些信息，例如存储过程的名称和输入参数的名称，以便对存储过程执行这些修改。由于此项目与上一个项目的相似性，我们假设已经已知这些信息，并提前将这些信息放入这些方法中。假设的信息包括：

- 1) 数据更新存储过程的名称为 `dbo.UpdateFacultySP`。
- 2) 输入参数名称与用户方法 `UpdateParameters()` 中的名称相同。
- 3) 输入动态参数的名称为 `@FacultyID`。
- 4) 数据删除存储过程的名称为 `dbo.DeleteFacultySP`。
- 5) 输入动态参数的名称为 `@fname`。

基于这些假设，我们需要修改 Update 按钮的 `Click` 方法中的代码。关键点是记住这些输入参数的名称和存储过程的名称，并在下一节开发它们时将它们放入我们的存储过程中。

# SPUdateDelete 项目

# 使用 C# 进行 SQL Server 数据库编程

| | cmddUpdate_Click(object sender, EventArgs e) |
|---|---|

```csharp
private void cmddUpdate_Click(object sender, EventArgs e)
{
    string cmdString = "dbo.UpdateFactory";
    SqlCommand sqlCommand = new SqlCommand();
    int inUpdate = 0;
    sqlCommand.Connection = loginForm.sqlConnection;
    sqlCommand.CommandType = CommandType.StoredProcedure;
    sqlCommand.CommandText = cmdString;
    sqlCommand.Parameters.Add(sqlCommand);
    inUpdate = sqlCommand.ExecuteNonQuery();
    sqlCommand.Dispose();
    if(inUpdate == 0)
        MessageBox.Show("The data update is failed!");
}
```

**图 7.30** 修改后的按钮点击方法代码。

打开 Update 的 `Click` 方法并修改其代码。你对该方法完成的修改如图 7.30 所示。修改部分已用粗体字标出。让我们看看这段修改后的代码是如何工作的。

- **A.** 查询字符串的内容应该等于存储过程的名称 `dbo.UpdateFactory`。
- **B.** Command 对象的 `CommandType` 应该是 `StoredProcedure`，以告诉项目在项目运行时应该调用存储过程来执行数据更新。

用户定义方法 `UpdateParameters()` 没有修改。但为了明确在下一节中构建存储过程时所需的这些输入参数的正确性，该方法的代码显示在下面的图 7.31 中。
尝试记住这些参数，因为我们将在构建存储过程 `dbo.UpdateFactory()` 时需要使用它们。
接下来，让我们修改 Delete 按钮点击方法中的代码。打开此方法对该方法执行了两个项修改。你完成的方法应如图 7.32 所示。

# SPUdateDelete 项目

# UpdateParameters(ref SqlCommand cmd)

```csharp
private void UpdateParameters(ref SqlCommand cmd)
{
    byte[] image;
    image = getFaceImage();
    cmd.Parameters.Add("@name", SqlDbType.Char).Value = txtName.Text;
    cmd.Parameters.Add("@title", SqlDbType.Char).Value = txtTitle.Text;
    cmd.Parameters.Add("@office", SqlDbType.Char).Value = txtOffice.Text;
    cmd.Parameters.Add("@phone", SqlDbType.Char).Value = txtPhone.Text;
    cmd.Parameters.Add("@college", SqlDbType.Char).Value = txtCollege.Text;
    cmd.Parameters.Add("@email", SqlDbType.Char).Value = txtEmail.Text;
    cmd.Parameters.Add("@image", SqlDbType.Binary).Value = image;
    cmd.Parameters.Add("@fid", SqlDbType.Char).Value = txtIDField.Text;
}
```
```

**图 7.31** 用户定义方法 UpdateParameters() 的代码。

