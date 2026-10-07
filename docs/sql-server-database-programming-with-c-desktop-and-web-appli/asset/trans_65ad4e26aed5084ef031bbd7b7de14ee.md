

# 使用 C# 进行 SQL Server 数据库编程

| | | |
|---|---|---|
| CmdPW_Click(object sender, EventArgs e) | | |
| A private void cmdPW_Click(object sender, EventArgs e) | | |
| B { string passWord;
| C logTableAdapter.ClearBeforeFill = true; | |
| | passWord = logTableAdapter.PasswordQuery(txtUserName.Text);
| D if (passWord != String.Empty)
| | MessageBox.Show("The password is: " + passWord);
| | else
| | | MessageBox.Show("No matched password found!");
| | } | | |

图 5.46 cmdPW 点击按钮的代码。

SQL 语句：

```sql
SELECT pass_word From Login Where (user_name = @Param)
```

表示我们想要根据动态参数用户名 `user_name` 从 `Login` 表中查询密码，该参数将在程序启动时由用户输入。点击 OK 按钮进入下一个向导。

下一个窗口用于确认您的 SQL 语句。点击 Next 按钮继续。

下一个向导允许您为此查询选择一个名称。点击默认名称 `PasswordQuery`，然后点击 Next 按钮。如果没有问题，将显示成功的 Result。点击 Finish 按钮完成此配置。

现在让我们编写登录表（Login form）的代码。为了测试，我们需要在登录表上添加一个名为 `cmdPW` 的临时按钮，并将文本设为 `Password`。然后，从解决方案资源管理器（Solution Explorer）窗口中选择并打开登录表，双击 Password 按钮打开其方法，并将图 5.46 中的代码输入到该方法中。让我们仔细查看这段代码。

- A. 创建了一个局部变量 `password`，它用于存储检索到的单个 `pass_word` 数值。
- B. 我们在这一节中构建的查询方法 `PasswordQuery()`，它包含一个由用户输入的参数 `username`，用于检索匹配的 `pass_word`。
- C. 如果此查询根据用户输入的用户名从 `Login` 表中找到有效密码，将返回密码并在 MessageBox 消息框中显示。
- D. 如果此查询找不到任何匹配的 `pass_word`，将返回一个空字符串并赋值给变量 `passWord`。如果发生这种情况，将显示一个带有警告消息的 MessageBox。

现在让我们运行项目来测试此。点击 Start 按钮运行项目，您的运行项目界面如图 5.47 所示。

在 User Name 框中输入用户名 `ybai` 并点击 Password 按钮。返回的密码将显示在消息框中，如图 5.48 所示。

现在，如果您愿意，可以从此登录表中删除临时的 Password 按钮及其方法，因为我们在这个项目中不再需要它了。

# 使用 Visual C#.NET 进行数据选择查询

# 215

![](img/d59a47501d0a20fc0460a49c469c6fb7_243_0.png)

图 5.47 登录表的运行状态。

![](img/d59a47501d0a20fc0460a49c469c6fb7_243_1.png)

图 5.48 返回的密码。

在接下来的章节中，我们将向读者展示如何通过更多的控件和方法开发一个更专业的数据驱动项目。我们仍然使用 SelectWizard 项目示例，并继续处理 SelectionForm（选择表）。

# 5.9 选择表的编码

正如我们在第 5.6 节中讨论的，如果登录过程成功，则应该显示 SelectionForm 窗口以允许用户继续下一步。图 5.49 显示了一个打开的 SelectionForm 窗口。

![](img/d59a47501d0a20fc0460a49c469c6fb7_243_2.png)

图 5.49 打开的选择表。

# 使用 C# 进行 SQL Server 数据库编程

ComboBox 控件中的每条信息都与一个表窗口相关，此外它还与存储在数据库数据表中的一组数据相关。
该表的操作步骤总结如下：

- 1) 当此表打开时，ComboBox 控件中将显示三条信息，允许用户进行选择以浏览与该选择相关的信息。
- 2) 当用户点击 OK 按钮时，应显示选中的表以允许用户浏览相关信息。

根据操作步骤 1，显示三条信息的代码应位于 `SelectionForm` 的构造函数中，因为当创建 `SelectionForm` 实例时，该构造函数应该被首先调用。
打开 SelectionForm 窗口并点击 View Code 按钮打开其窗口。将图 5.50 所示的代码输入到 `SelectionForm` 的构造函数。
让我们仔细查看这段代码。

- A. 创建了三个实例，每个实例都与一个表相关。
- B. ComboBox 类的 `Add()` 方法用于将三条信息添加到 ComboBox 中。
- C. `SelectedIndex` 属性被设置为默认选择第一条信息。

根据操作步骤 2，当点击 OK 按钮时，应显示选中的表以允许用户浏览相关信息。SelectionForm 的 GUI 双击 OK 按钮打开其 `cmdOK_Click` 方法，并输入图 5.51 所示的代码。让我们仔细查看这段代码它是如何工作的。

| SelectWizardProject | SelectionForm |
|---|---|
| namespace SelectWizard_Project | |
| public class SelectionForm : Form | |
| { | |
| FacultyForm facultyForm = new FacultyForm(); | |
| CourseForm courseForm = new CourseForm(); | |
| StudentForm studentForm = new StudentForm(); | |
| public SelectionForm() | |
| { | |
| InitializeComponent(); | |
| this.ComboBox.Add("Faculty Information"); | |
| this.ComboBox.Add("Course Information"); | |
| this.ComboBox.Add("Student Information"); | |
| this.SelectedIndex = 0; | |
| } | |
| } | |

图 5.50 选择表的详细代码。

# 使用 Visual C#.NET 进行数据选择查询

| SelectWizardProject | CmdOK_Click(object sender, EventArgs e) |
|---|---|
| A private void CmdOK_Click(object sender, EventArgs e) | |
| B { | |
| C if (this.ComboSelection.Text == "Faculty Information") | |
| | facultyForm.Show(); | |
| D else if (this.ComboSelection.Text == "Course Information") | |
| | courseForm.Show(); | |
| E else if (this.ComboSelection.Text == "Student Information") | |
| | studentForm.Show(); | |
| F else | |
| | MessageBox.Show("Invalid Selection"); | |
| G } | |

图 5.51 OK 按钮的代码。

| SelectWizardProject | cmdExit_Click(object sender, EventArgs e) |
|---|---|
| A private void CmdExit_Click(object sender, EventArgs e) | |
| B { | |
| C courseForm.Close(); | |
| D facultyForm.Close(); | |
| E studentForm.Close(); | |
| F Application.Exit(); | |
| G } | |

图 5.52 退出按钮的完成代码。

这段编码的功能直观且易于理解，概述如下：

- A. 如果用户选择了 Faculty Information，则打开 FacultyForm 窗口。
- B. 如果用户选择了 Student Information，则打开 StudentForm 窗口。
- C. 如果用户选择了 Course Information，则打开 CourseForm 窗口。
- D. 如果没有选择信息，则显示错误消息。

此表最后的编码过程是退出按钮。SelectionForm 的 GUI 双击退出按钮打开其 `cmdExit_Click()` 方法。将以下代码输入到该方法，如图 5.52 所示。
这段代码看起来有点复杂。让我们看看这段代码是如何工作的。

假设用户选择了第一条信息——Faculty Information。将显示一个 faculty窗口，它应该连接到 DataSet 中的 faculty 数据表。如果用户从 ComboBox 控件中选择一个系名称并点击该表上的 Select 按钮，与该系相关的所有信息都应该显示在该表上，正好显示在七个 TextBox 和一张图片中。

