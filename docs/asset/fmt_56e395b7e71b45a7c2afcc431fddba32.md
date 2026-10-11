
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

| private void ClearFactory() { int index; TextBox[] fbox = {txtFacultyID, txtName, txtOffice, txtPhone, txtCollege, txtEmail}; for (index = 0; index < fbox.Length; index++) fbox[index].Text = ""; } |

图 6.13 `ClearFactory()` 方法的代码。

接下来是 `ClearImage` 方法的代码。该方法的目的是在记录成功插入后清理 TextBoxes 中所有已插入的信息，并允许用户测试数据插入。

在打开的 Form 窗口代码窗口，输入图 6.13 所示的代码以生成该方法。

代码 `fbox` 的功能非常直观。首先，一个局部整数变量 `index` 和一个 TextBox 数组 `fbox` 意味着使用 `for` 循环将每个 TextBox 的 `Text` 属性设置为空字符串以进行清理。

## 6.2.8 使用 TableAdapter.Update 方法插入数据

当数据驱动型应用程序使用 DataSet 存储数据时（如我们在本应用程序中使用 `CSE_DEPTDataSet` 所示），人们可以使用 `TableAdapter.Update()` 方法向数据库插入（或添加）新记录。

在此方法中，要向数据库表插入新记录需要两个步骤：

- 1) 向 DataSet 中的目标数据表添加新项。例如，在本应用程序中，即指向 `CSE_DEPTDataSet` 中的 `faculty` 表。
- 2) 调用 `TableAdapter.Update()` 方法将更新的记录添加到数据库数据表中。要更新的数据量可以通过向 `Update()` 方法传递不同的参数来控制，可以是整个 DataSet、一个 DataTable、一个 `DataRow` 数组或单个 `DataRow`。

接下来我们根据上述步骤开发代码，以使用此方法插入数据。

# 使用 C# 进行 SQL Server 编程

| SelectWizardProject | cmdInsert_Click(object sender, EventArgs e) |

|---|---|

```csharp
private void cmdInsert_Click(object sender, EventArgs e)
{
    byte[] image;
    int check = btInsert = 0;
    CSE_DEPTDataSet.AddRow newFacultyRow();
    CreateFacultyCollection();
    check = CreateFacultyCollection();
    if (check != 0)
    {
        MessageBox.Show("Please fill all textboxes...");
    }
    else
    {
        if (ComboMethod.Text == "TableAdapter Insert")
        {
            image = getFacultyImage();
            int intinsert = tableAdapter.Insert(txtFacultyID.Text, txtFacultyName.Text, txtTitle.Text, null, txtPhone.Text, txtCollege.Text, txtEmail.Text, image);
        }
        else
        {
            newFacultyRow = this_CSEDEPTDataSet.NewFacultyRow();
            InsertFacultyRow = newFacultyRow;
            CSE_DEPTDataSet.Faculty.Rows.Add(newFacultyRow);
            int intinsert = tableAdapter.Update(CSE_DEPTDataSet);
        }
        if (intinsert != 0)
        {
            // data insertion is successful
            UpdateFaculty();
            ClearFaculty();
            PhotoBox.Image = null;
            cmdInsert.Enabled = false;
        }
        else
        {
            MessageBox.Show("The data insertion is failed.");
            cmdInsert.Enabled = true; // enable the Insert button to allow the insertion
        }
    }
    RemoveFacultyCollection();
}
```

**图 6.14** 第二种数据插入方法的代码。

重新打开教师窗口（Faculty Window）的图形用户界面，双击**插入**（Insert）按钮打开其 Click 方法。我们在上一节中已经开发了该方法的大部分代码，现在我们需要将代码添加到第二种数据插入方法中。浏览到 **else** 块（图 6.10 中的 **E**），并将图 6.14 所示的代码输入此块中。

为了区分新代码和之前添加的代码，旧代码用灰色背景颜色表示。请查看此代码以了解其工作原理。

- **A.** 我们首先需要声明一个 **DataRow** 类的对象，**newFacultyRow**。每个 DataRow 对象都可以映射到数据表中的一行。我们正在使用 DataSet 来管理此表中的所有数据页，在 **DataRow** 对象之前必须带有 DataSet 前缀。此外，我们需要在 **faculty** 数据表中创建的一行，因为 **FacultyRow** 被选为 DataRow 类。
- **B.** 接下来我们需要创建一个 **newFacultyRow** 类的对象。
- **C.** 调用用户自定义方法 **InsertFaculty()**，以将关于新插入教师的所有教职信息（这些信息存储在七个 TextBox 和一个 PhotoBox 中）添加到此新创建的 DataRow 中。该用户自定义方法的代码和功能将在稍后解释。该方法返回一个包含新记录所有部分信息的完整 DataRow。需要注意的是，传递到方法的是一个引用参数 `ref newlyRow`，这意味着传递到方法的是对象 `newlyRow` 的地址（而不是值），对它的任何修改都是永久的。我们需要这个永久属性来保持返回的 `newlyRow` 是更新的。
- **D.** 将完成的 DataRow 添加到 DataSet 中的 Faculty 中。需要注意的是，向 DataSet 中的数据表添加新记录与向数据库中的数据表添加新记录无关。数据表只是数据库中实际数据表的映射。要添加这一点，我们需要执行下一步。
- **E.** 执行 TableAdapter 的方法 `Update()`，以将此记录添加到实际数据库中。如前所述，您可以通过通过传递不同的参数来控制添加到数据库的数据量。在这里，我们想向 Faculty 中添加一条新记录，因此将数据表作为参数。此 `Update()` 返回一个整数值，用指示更新是否成功。返回的整数值是成功添加到数据库的行数。返回值为 0 则表示更新失败，因为没有向数据库中添加新行。

## 使用 Visual C#.NET 进行数据插入

# 328 使用 C# 进行 SQL Server 数据库编程

使用上述列出的七条新教职工信息以及所需的教师图像 Wang.jpg 重新执行此插入。

第二种方法如下所示插入新教职工记录：

| 教师 ID | D56789 |

| :--- | :--- |

| 教师姓名 | James David |

| 职称 | 副教授 |

| 办公室 | MTC-222 |

| 电话 | 750-330-1662 |

| 学院 | 州立大学 |

| 邮箱 | jdavid@college.edu |

运行项目并从 Query Method（查询方法）组合框中完成 TableAdapter Update，并选择 Form 窗口。选择第二种方法，在 TextBox 中输入上述新教职工信息。然后点击 Insert（插入）按钮以选择选定的教师图像 David.jpg，然后点击 Exit（退出）按钮。

为了检查数据插入情况，展开 ComboName 组合框，你会发现新插入的教师 James David 已添加到此教职工列表中。为了验证这一点，选择该教师并点击 Select（选择）按钮以检索回插入的信息。立即，新插入的教职工信息将从数据中检索并显示在 TextBoxes 中，如图 6.19 所示。

点击 Form 和 Selection Forms 中的 Back（返回）和 Exit（退出）按钮以终止项目。

完成的具有数据插入功能的项目 SelectWizard 项目可以在 CRC ftp 站的 Students 文件夹下的 Class DB Project，Chapter 6 & SelectWizard Solution 文件夹中找到（请参阅第 1 节中的图 1.2）。

![](img/d59a47501d0a20fc0460a49c469c6fb7_356_0.png)

图 6.19 使用 TableAdapter.Update() 测试数据插入的状态。

# 6.3 使用三种方法向课程表中插入数据

在本节中，我们想要讨论如何使用三种不同的方法向数据库插入新记录：TableAdapter Insert、TableAdapter Update 和存储过程（Stored Procedure）方法。为了简单起见，我们将使用上一节中构建的 SelectWizard 项目中的 Course Form，通过这些方法向示例数据库中的 Course 表插入新的课程记录。

要使用不同的方法向数据库插入新记录，我们需要执行以下任务来构建我们的项目：

- 1. 首先，我们需要添加一些类级变量，并通过添加查询方法修改 Course 窗口 Form_Load() 方法中的代码，允许用户选择其中一种来执行相关的数据插入。
- 2. 要使用 TableAdapter.Insert() 方法，我们需要通过 TableAdapter 配置向导构建查询 InsertCourse()。
- 3. 要使用存储过程，我们需要使用 Table 查询向导在 Course 表上创建一个名为 InsertSP() 的存储过程。
- 4. 构建 Insert 按钮的 Click 方法代码，以调用其中一种方法向示例数据库中的 Course 表插入新的课程记录。

让我们从上述列表的第 1 步开始工作。

## 6.3.1 添加类变量并修改 FORM_LOAD() 方法中的代码

打开 Course 窗口及其 Form_Load() 方法，将图 6.20 所示的代码输入到代码中，替换所有原始代码，允许用户选择其中一种来执行相关的数据插入。

| SelectWizard 项目 | Course_Form_Load(object sender, EventArgs e) |

| :--- | :--- |

| public class CourseForm : Form {

 string strFacultyID;

 string[] CourseInfo = new string[6];

public CourseForm() {

 InitializeComponent();

 }

 void CourseForm_Load(object sender, EventArgs e) {

 ComboName.Items.Add("Vic Bai");

 ComboName.Items.Add("David Bhalla");

 ComboName.Items.Add("Black Anderson");

 ComboName.Items.Add("Steve Johnson");

 ComboName.Items.Add("Jenney King");

 ComboName.Items.Add("Alice Brown");

 ComboName.Items.Add("Debbie Augie");

 ComboName.Items.Add("Jeff Henry");

 ComboName.SelectedIndex = 0;

 ComboMethod.Items.Add("TableAdapter Insert");

 ComboMethod.Items.Add("LINQ & Data Set Method");

 ComboMethod.Items.Add("TableAdapter Insert");

 ComboMethod.Items.Add("TableAdapter Update");

 ComboMethod.Items.Add("Stored Procedure");

 ComboMethod.SelectedIndex = 0;

 } | |

图 6.20 在 Form_Load() 方法中新添加的代码。

参考图 6.20，生成了两个类变量 strfacultyID 和一个数组 CourseInfo[]，这些变量稍后将使用。在 Method 组合框 ComboMethod 中总共列出了五个方法。前两个方法用于 Select 查询，后三个方法用于数据插入。

接下来，让我们通过 TableAdapter 查询配置向导构建一个新的查询 InsertCourse()，它将由 Table.Insert() 方法调用。

## 6.3.2 构建查询方法 InsertCourse()

执行以下操作来构建此新查询方法：

- 1. 在打开的 Data Sources（数据源）窗口中，右键点击数据源窗口内的任意位置，从弹出菜单选择 Edit DataSet with Designer（使用设计器编辑数据集）打开此向导。
- 2. 右键点击 Course 表的最后一项，从弹出菜单中选择 Add Query（添加查询）打开 TableAdapter 查询配置向导。使用 SQL 语句并点击 Next（下一步）。
- 3. 保持默认选择。
- 4. 勾选 INSERT 按钮并点击 Next。
- 5. 在打开的向导中点击 Query（查询器）按钮，因为我们需要构建一个新的查询。如图 6.21 所示。
- 6. 点击 OK 确认功能。
- 7. 默认查询使用 SELECT ... FROM 语句，用于从 Course 表选择所需的列并将其插入另一个目标表。这里我们只需要向 Course 表插入记录，不需要其他目标表，因此只需高亮 SELECT 语句并按 Delete 键将其删除。

![](img/d59a47501d0a20fc0460a49c469c6fb7_358_0.png)

图 6.21 打开的查询器。

- 8. 点击 Next 进入下一个向导。
- 9. 在下一个向导中，在名称框中输入 Insert 作为该查询的名称。
- 10. 点击 Next 和 Finish 完成后续向导并关闭此过程。

# 使用 C# 插入数据

## 6.3.3 使用 TableAdapter 配置向导创建存储

点击 View Data Sources（查看数据源）菜单项打开数据源，然后右键点击数据源窗口内的任意位置，从弹出菜单选择 Edit DataSet with Designer（使用设计器编辑数据集）打开此向导。右键点击 Course 表的项，从弹出菜单中选择 Add Query（添加查询）打开 TableAdapter 配置向导。执行以下操作来构建此查询：

- 1. 勾选 New stored procedure（新建存储过程），因为我们要创建一个过程来执行数据插入，并点击 Next 按钮。
- 2. 勾选 INSERT 按钮并点击 Next 继续。
- 3. 在打开的向导中点击 Query Builder 按钮，因为我们需要构建一个新的查询。如图 6.22 所示。
- 4. 点击 OK 确认功能。
- 5. 默认查询使用 SELECT ... FROM 语句，用于从 Course 表选择所需的列并插入另一个目标表。这里我们只需要向 Course 表插入记录，不需要其他目标表，因此只需高亮第二个 SELECT 语句并按 Delete 键将其删除。
- 6. 点击 Next 进入下一个向导。
- 7. 在下一个向导中，在名称框中输入 InsertSP 作为该存储过程的名称。
- 8. 点击 Next 和 Finish 完成后续向导并关闭此过程。

![](img/d59a47501d0a20fc0460a49c469c6fb7_359_0.png)

图 6.22 插入确认向导。

接下来，让我们通过 TableAdapter 配置向导在 Course 表上创建一个 InsertSP() 存储过程。

# 使用 C# 插入数据

![](img/d59a47501d0a20fc0460a49c469c6fb7_360_0.png)

图 6.23 插入确认向导。

## 6.3.4 构建 INSERT 按钮的 Click 方法代码

# 使用 C#.NET 进行数据插入
