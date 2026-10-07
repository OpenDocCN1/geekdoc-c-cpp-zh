

H. 此步骤显示了用户定义方法 `UpdateParameters()` 的详细代码。带有原始 `course_id` 的五条课程信息被分配到 `Course` 表的相关列中。

至此，我们已经使用运行时方法完成了 `Course` 表数据更新过程的代码开发。接下来，让我们处理数据更新后的验证，以确认我们的数据更新是否成功。

### 7.4.3.2 验证课程数据更新

我们不需要添加任何表单窗体或按钮来执行此数据更新验证；相反，我们可以使用 `Course` 窗口并选择 `Select` 按钮的 `Click` 方法来执行此验证工作。通过在 `Faculty Name` 组合框中选择指定的教师并点击 `Course` 表单上的 `Select`，我们可以执行查询以从数据库检索更新后的课程记录，并将其显示在 `Course` 表单上进行确认。

现在让我们运行项目来测试数据更新功能。点击 `Start` 运行项目，在 `Login Form` 中输入相应的用户名和密码，并在 `Selection Form` 中选择 `Course Information` 项打开 `Course` 表单。

首先，让我们选择一名教师并点击 `Select`，从我们的数据库中检索与该教师（如 Yi Bai）相关的所有课程信息，并将这些信息显示在此表单中。然后，我们可以通过从 `CourseList` 框中选择某个课程（如 CSE-438），并修改存储在相关 `TextBox` 中的某些信息来更新该课程。在相关的文本框中输入更新后的信息：

| Field | Value |
| :--- | :--- |
| Course Name | Artificial Controls |
| Schedule | T-H: 1:30 – 2:45 PM |
| Classroom | MTC-212 |
| Credit | 4 |
| Enrollment | 26 |

现在点击 `Update` 按钮开始此课程更新操作。为了验证此更新操作，首先从 `Faculty Name` 组合框中选择另一个教师（如 Davis Bhalla），并点击 `Select` 显示该教师教授的所有课程。然后重新从 `Faculty Name` 组合框中选择 Yi Bai，并点击 `Select` 显示所有课程。现在点击 `CourseList` 框中的 `course_id` —— `CSE-438`，你会发现课程已经更新，如图 7.26 所示。

为了保持数据库的整洁和一致，强烈建议将该课程记录恢复到原始状态。在此 `Course` 表单的相关 `TextBox` 中输入以下数据，并执行另一次数据更新操作以确认此课程数据的恢复：

| Field | Value |
| :--- | :--- |
| Course Name | Adv Logic & Microprocessor |
| Schedule | M-W-F: 11:00-11:55 AM |
| Classroom | MTC-213 |
| Credit | 3 |
| Enrollment | 35 |

点击 `Back` 和 `Exit` 按钮终止此项目。我们的课程数据更新成功。接下来，让我们讨论如何从示例数据库的 `Course` 表中删除课程记录。

## 使用 Visual C#.NET 进行数据更新和删除

![](img/d59a47501d0a20fc0460a49c469c6fb7_417_0.png)

图 7.26 课程数据更新操作的确认结果。

## 7.4.4 删除 SQL Server 数据库中 Course 表的数据

在本节中，我们将讨论如何通过上一节构建的 `RTUpdateDelete` 项目中的 `Course` 窗口，对示例数据库中的 `Course` 表执行数据删除。

让我们集中讨论从 SQL Server 数据库中删除 `Course` 表的方法。为了删除数据，我们不需要添加任何新的窗体表单，可以使用 `Course` 表单作为界面，并在 `Delete` 按钮（具体为 `Delete` 的 `Click` 方法）执行此删除操作。我们需要执行以下步骤来完成此数据更新操作：

- 1) 开发删除课程记录的代码。
- 2) 验证数据删除结果。

现在让我们编写执行数据删除操作的代码。

### 7.4.4.1 开发删除课程记录的代码

与从 `Faculty` 表中删除记录类似，删除课程记录的主要编码工作是在 `Delete` 的 `Click` 方法内部开发的。现在让我们开始从示例数据库中删除课程记录的代码编写。

打开 `RTUpdateDelete` 项目和 `Course Form` 窗口，双击 `Delete` 按钮打开其 `Click` 方法。将如图 7.27 所示的代码输入此方法中。让我们仔细观察这段代码，看看它是如何工作的。

- A. 删除查询字符串首先在方法的开头声明。唯一的输入参数是 `course_id`，它是示例数据库中 `Course` 表的主键。
- B. 创建了一个 `MessageBox` 按钮对象，该对象用于在项目运行时在 `MessageBox` 中显示 `Yes` 和 `No` 两个按钮。

