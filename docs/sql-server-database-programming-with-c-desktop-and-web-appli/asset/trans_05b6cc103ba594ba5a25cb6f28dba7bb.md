

# 使用 C# 进行 SQL Server 数据库编程

# SelectWizard 项目

```csharp
private void cmdDelete_Click(object sender, EventArgs e)
{
    MessageButtons vbButton = MessageButtons.YesNo;
    CSE_DEPTData.FacultyRow FacultyRow;
    DialogResult Answer;
    string strFrameID = null;
    int i = 0;

    Answer = MessageBox.Show("Are you sure to delete this record?","Delete",vbButton);
    if (Answer == System.Windows.Forms.DialogResult.Yes)
    {
        if (Combo.Text == TableAdapter.Delete Method)
        {
            iDelete = TableAdapter.Delete(Combo.Text);
        }
        else
        {
            TableAdapter.Update(Combo.Text);
        }
    }

    strFacultyID = TableAdapter.FindByID(Combo.Text);
    FacultyRow = CSE_DEPTData.FindByFaculty_id(strFacultyID);
    FacultyRow.Delete(); // delete the data from the Table DataSet
    iDelete = TableAdapter.Update(CSE_DEPTData.FacultyRow);

    CurrentFaculty();
    if (iDelete == 0)
    {
        MessageBox.Show("Faculty Table Deleting failed!");
    }
}
```

**图 7.10** 第二种数据删除方法的代码。

## 7.2.5 使用 TABLE UPDATE 开发删除数据的代码

在打开的代码窗口中，准确位于 Faculty Form 窗口打开的 Delete 按钮的 Click 事件中，在方法的 `else` 块中添加图 7.10 所示的代码。我们在上一节中开发的代码已用灰色背景高亮显示。让我们仔细观察这段新代码，看看它是如何工作的。

- A. 为了从 DataTable 中找到要删除的 DataRow，将利用默认系统方法 `FindByFaculty_id`。然而，这需要使用 `faculty_id` 作为筛选准则。因此，我们需要根据用户选择的 Faculty 名称，基于 `FindByClassName()` 方法从 Faculty 表检索 `faculty_id`。
- B. 搜索后，执行默认系统方法 `FindByFaculty_id` 以定位 Faculty 表中所需的 DataRow，并将所需的 DataRow 返回并赋值给本地变量 `FacultyRow`。
- C. 执行 Faculty 的 `Delete()` 方法以从数据集中的 Faculty DataTable 中删除选定的 DataRow。
- D. 执行 `TableAdapter.Update()` 以将数据集中的该 DataRow 更新到数据库中的行。

至此，我们已经完成了该项目所有的代码开发。让我们运行项目以测试并确认数据的更新和删除。

## 7.2.6 运行项目验证数据更新和删除后的数据

点击 Run 按钮运行我们的项目。完成登录过程并从选择表（Selection Form）中选择教师信息以打开 Faculty Form 窗口。选择所需的教师，例如在 Faculty Name 下拉框中选择“Ying Bai”，然后点击 Select 按钮检索此教师记录。

输入以下信息以更新此教师记录：

| 教师姓名 | Susan Bai |
| :--- | :--- |
| 职称 | 教授 |
| 办公室 | MTC-218 |
| 电话 | 750-378-2800 |
| 学院 | 克大学 |
| 邮箱 | sbai@college.edu |

在 Query Method 下拉框中选择 TableAdapter DBDirect 方法，并点击 Update 按钮更新此记录。浏览到本地图像文件夹，并在打开的文件对话框中选择所需的教师图像 White.jpg，点击 Open 按钮加载并更新此教师图像。所有教师图像都可以在 CRC Press ftp 站点 Students 文件夹下的 Images 文件夹中找到（参见第 1 章的图 1.2）。你可以复制所有教师图像并将它们存储在本地文件夹中，以便测试此项目。

要确认或验证此数据更新，转到 Faculty Name 下拉框并选择更新的教师 Susan Bai，然后点击 Select 按钮尝试检索更新后的记录。立即，所有更新的教师信息都会显示在 Faculty Form 窗口中，如图 7.11 所示。![](img/d59a47501d0a20fc0460a49c_403.png) 图 7.11 使用 TableAdapter DBDirect 方法更新的教师记录。

# 使用 C# 进行 SQL Server 数据库编程

可以尝试使用第二种方法 `TableAdapter.Update()` 对教师 Ying Bai 进行另一种更新，具有以下数据项：

| 教师姓名 | Ying Bai |
| :--- | :--- |
| 职称 | 助理教授 |
| 办公室 | MTC-211 |
| 电话 | 750-378-1148 |
| 学院 | 大西洋大学 |
| 邮箱 | ybai@college.edu |
| 教师图像 | Bai.jpg |

测试删除教师记录的最佳方法是删除新插入的教师 Steve Wang，他在第 6 节 2.8 被插入到我们的数据库中。为了测试删除操作，只需在 Faculty Name 下拉框中并点击 Delete 按钮，Steve Wang 从框中消失了。另一种执行此任务的方法是打开 Faculty 表进行确认。

为了恢复已删除的记录，由于父表和子表之间的关系，例如，如果原始教师 Ying Bai 从 Faculty 表中删除，该教师将从所有 10 个相关的子表中被删除。图 7.12 显示了 CSE_DEPT 数据库中 Faculty 表与其他表之间的关系。

恢复已删除的教师是一项复杂的工作！根据图 7.12 所示的关系，应按顺序执行恢复工作：

- 首先根据图 7.13 和 7.14 中的原始记录恢复父表（Faculty 和 Course 表）。
- 然后根据图 7.15 和 7.16 中的原始记录恢复子表（LogIn 和 StudentCourse 表）。![](img/d59a47501d0a20fc0460a49c6fb7_404.png)

# 使用 Visual # 进行数据更新和删除

| 教师 ID | 教师姓名 | 职称 | 办公室 | 学院 | 邮箱 | 教师图像 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| B78880 | Ying Bai | 助理教授 | MTC-211 | 750-378 | 大西洋大学 | ybai@college.net | NULL |

**图 7.13** Faculty 表中待恢复的数据。

| 课程 ID | 课程 | 学分 | 教室 | 选人数 | 教师 ID |
| :--- | :--- | :--- | :--- | :--- | :--- |
| CSC-132B | 编程入门 | 3 | MTC-302 | 周二/周四 1:00-2:25 | 21 | B78880 |
| CSC-234A | 数据结构与算法 | 5 | MTC-302 | 周一/周三 9:00-9:55 | 25 | B78880 |
| CSE-434 | 高进电子学 | 3 | MTC-213 | 周一/周三 9:00-1:55 | 26 | B78880 |
| CSE-438 | 高级逻辑与微处理器 | 3 | MTC-213 | 周一/周三 11:00-11:55 | 35 | B78880 |

**图 7.14** 课程表中待恢复的数据。

| 用户名 | 密码 | 教师 ID | 学生 ID |
| :--- | :--- | :--- | :--- |
| ybai | come | B78880 | NULL |

**图 7.15** login 表中待恢复的数据。

| 课程 ID | 学生 ID ID | 课程 ID | 学分 | 专业 |
| :--- | :--- | :--- | :--- | :--- |
| 1005 | A778896 | CSC-234A | 5 | IS |
| 1009 | A78835 | CSE-434 | 3 | CE |
| 1014 | A78835 | CSE-438 | 3 | CE |
| 1016 | A97850 | CSC-132B | 3 | ISE |
| 1017 | A97850 | CSC-234A | 5 | ISE |

**图 7.16** 在图 7.12 中恢复的表顺序，并参考 7.13–7.16 以完成这些记录的恢复。

