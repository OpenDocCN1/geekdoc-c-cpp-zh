

# ASP.NET Web Services

| WinClickInsertPoint | cmdSelect_Click(object sender, EventArgs e) |
|---|---|
| private void cmdSelect_Click(object sender, EventArgs e) |
| { |
| WS_SQLInsert.SQLInsertResult = new WS_SQLInsert.SQLInsertRecord(); |
| WS_SQLInsert.WebServiceInsert = new WS_SQLInsert.WebServiceInsert(); |
| if (ComboBox.Text == "Stored Procedure") |
| try { wsSQLResult = wsSQLInsert.GetClassName(ComboBox.Text); } |
| catch (Exception err) { MessageBox.Show("Web service is wrong: " + err.Message); } |
| if (wsSQLResult == SQLInsertOK) |
| MessageBox.Show(wsSQLResult,"SQLInsertError"); |
| ProcessObject(wsSQLResult); |
| } else |
| if (dsFlag == false) |
| MessageBox.Show("No DataSet Insert, do data insertion first"); |
| FullCourseDataSet(ref wsSQLResult); |
| dsFlag = false; |
| } |

**图 9.76** 用于选择按钮点击方法的代码。

该 Web 服务包含了从数据库中检索的所有 course_id，并将其分配给我们的本地实例以便稍后处理。如果在执行该 Web 方法期间遇到任何错误，将显示错误消息。

C. 此外，系统通过检查数据 状态 `SQLInsertOK` 来执行我们的错误检查过程。如果发生任何错误，将显示错误源。

D. 如果该 Web 方法正常工作，将调用用户定义的 `ProcessObject()`（详细代码见图 9.77），以从返回的实例 `wsSQLResult` 中提取所有列。

E. 如果用户选择 DataSet 方法，首先我们需要检查 Web 方法 `InsertDataSet()` 是否已经执行，或者通过检查类层级变量 `dsFlag` 的状态来检查。因为应该已经通过 Insert 按钮方法中的 `InsertDataSet()` 方法在数据库中插入了一条新的课程记录。事实上，该方法同时执行了数据插入和数据检索。如果你在没有通过 Insert 按钮点击方法执行数据插入的情况下使用此方法从 Select 点击方法检索信息，可能会遇到错误，因为没有插入任何内容。因此，从返回的 DataSet 中无法获取任何内容。如果此 `dsFlag` 为 `False`，意味着没有插入任何内容，将显示信息消息要求你先执行数据插入。

F. 如果 Web 方法 `InsertDataSet()` 已执行，将调用用户定义的方法 `FullCourseDataSet()`（详细代码见图 9.78），在列表框中填充所有检索到的 course_id。

G. 最后，`dsFlag` 重置为 `False`，表示方法 `InsertDataSet()` 未被执行。

`ProcessObject()` 和 `FullCourseListBox()` 方法的详细代码见图 9.77。让我们来看看这两个子程序中的代码，看看它们是如何工作的。

# 590

# C# SQL Server 数据库编程

```
WinClientInsert Project
ProcessObject()
private void ProcessObject(ref WS_SQLInsert.SQLInsertRecord wsResult)
{
    if (wsResult.SQLInsertOK == true)
        FullListBox(ref wsResult);
    else
        MessageBox.Show("Course information cannot be retrieved: " + wsResult.SQLInsertError());
}
private void FullListBox(ref WS_SQLInsert.SQLInsertRecord sqlResult)
{
    int index = 0;
    //clean up the course listBox
    CourseList.Items.Clear();
    for (index = 0; index <= sqlResult.CourseID.Length - 1; index++)
{
        if (sqlResult.CourseID[index] != null)
            CourseList.Items.Add(sqlResult.CourseID[index]);
    }
}
```

图 9.77 `ProcessObject()` 和 `FullListBox()` 方法。

图 9.78 `FullCourseDataSet()` 方法的代码。

- A. 首先，我们需要检查成员数据 `SQLInsertOK` 以确保方法是否执行成功。如果是，则调用 `FullListBox()` 方法从返回的实例中将所有 course_id 填充到我们客户端表单中的列表框控件中。
- B. 如果在执行该 Web 方法期间遇到任何错误，将显示警告消息。
- C. 在用户定义的方法 `FullListBox()` 中，创建了一个本地整数变量 `index` 作为循环计数器，从返回的实例中不断提取 course_id 并将其添加到列表框控件中。
- D. 在向列表框添加任何 course_id 之前会清空列表框控件。这个过程在显示任何 course_id 时非常重要，否则任何新的 course_id 将附加在该控件中原始 course_id 的末尾，导致显示结果混乱。
- E. 使用 `for()` 循环从我们返回的类 `SQLResult` 中定义的 `CourseID()` 数组中不断提取每个 course_id。需要注意的是此数组的上限或长度。数组的长度或大小为 11。但此数组的上限是 10，因为数组索引从 0 开始，因此数组的上限等于数组长度减 1。只要 `CourseID(index)` 的内容不为空，就会使用 `Add()` 方法将剩余的 course_id 添加列表框控件中。

# ASP.NET Web Services

子程序 `FillCourseDataSet()` 的代码见图 9.78。让我们来看看这个子程序的代码，看看它们如何提供帮助。

- A. 在此方法的开头声明了一个 `DataTable`，我们需要使用它从返回的实例中执行数据提取并将数据添加到列表框控件中。
- B. 清空列表框控件，以避免多个 course_id 显示混乱。
- C. 通过添加新的数据表 "Course" 来初始化 `Course` 对象，并将其分配给 `DataSet` 对象。
- D. 使用 `foreach` 循环从第一列（即 course_id）中不断提取每一行并将每项添加到列表框控件中。需要注意的是，第一列的索引为 0, 1，索引从 0 开始。

此时，我们完成了 Select 按钮点击的所有编码工作。换句话说，所有与数据验证相关的代码都已完成。

现在让我们运行我们的客户端项目，在数据插入过程后执行数据验证。在启动项目之前，确保满足以下两个条件：

- 1) 我们的服务处于运行状态，可以通过定位屏幕底部状态栏上的一个小白色图标来检查。如果你找不到它，请打开我们的服务 `WebServiceInsert` 并点击运行。服务启动后，你可以最小化 IIS 页面
- 2) 在 9.4.3.3.2 中通过 Insert 点击方法插入的新课程记录 CSE-668 和 CSE-526 已经从我们示例数据库的 Course 表中删除，我们要插入相同的课程记录。

现在点击启动按钮运行我们的客户端项目。按照图 9.74（见 9.4.3.3.2）所示输入参数，然后按照图 9.75（见存储过程方法）所示输入参数。接下来点击按钮使用 DataSet 方法完成此数据插入。

要检查或验证这些数据集，请确保查询方法组合中选择的方法是 DataSet 方法，且教师名称为 "Yin Bai"。点击 Select 按钮从数据库中检索所有 course_id。可以发现所选教师的所有课程都在列表框控件中，course_id 作为每个课程的标识符。

要测试存储过程方法，请确保在查询方法组合中选择了 Stored Procedure。现在我们可以在教师名称组合框中选择另一个教师，并点击 Select 获取所选教师的所有 course_id。默认教师为 Yin Bai，然后点击 Select 按钮检索所选教师的所有 course_id。你可以发现使用 DataSet 方法获得的结果显示在列表框控件中。

运行结果和数据验证见图 9.79。我们可以发现新插入的课程 CSE-668 和 CSE-526 已添加并显示在列表框控件中，我们的数据插入成功。点击返回按钮结束项目。

现在让我们考虑为列表框控件中选中的 course_id 显示详细课程信息的编码开发。

## 9.4.3.4.4 开发课程以获取特定课程的详细信息
此代码的功能是将详细课程信息（如名称、安排、教室、学分和人数）显示在相关的文本框控件中，作为

