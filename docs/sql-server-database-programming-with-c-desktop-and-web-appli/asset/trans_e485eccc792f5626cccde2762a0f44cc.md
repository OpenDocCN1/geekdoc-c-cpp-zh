

## 使用 Visual#.NET 进行数据更新和删除

文件夹 `DB Projects\Chapter 6\SelectWizard` 位于 CRC Press 网站的 Students 文件夹下。将整个 `SelectWizard` 解决方案复制并粘贴到新文件夹 `C:\Chapter 7` 中。

在开发新项目的代码之前，我们需要首先通过数据源（Data Source）构建两个查询：`UpdateFaculty()` 和 `DeleteFaculty()`。

## 7.2.1 配置 TableAdapter 并构建数据更新和删除查询

执行以下操作步骤来构建数据更新查询：

- 1. 在数据源窗口内任意位置点击右键，打开“数据源”窗口和“TableAdapter 查询配置向导”。从弹出菜单中选择 `DataSet with Designer` 项。
- 2. 在打开的向导中，进入 `Faculty` 表，右键点击 `Faculty` 表中的最后一项，从弹出菜单中选择“Add Item”（添加项）。
- 3. 保持默认选择“使用 SQL 语句”，并点击“Next”（下一步）进入下一个向导。
- 4. 从此向导中选择并点击 `UPDATE` 项，因为我们需要执行数据查询，然后再次点击“Next”继续。
- 5. 点击“Query Builder”（查询生成器）按钮打开查询生成器以构建我们的更新查询。打开的查询生成器如图 7.3 所示。
- 6. 从 `Filter` 和 `Or` 列下的 `faculty_id` 和 `faculty_name` 行移除列。
- 7. 取消勾选 `Set` 列下 `faculty_id` 行的复选框，并在 `Filter` 列下的 `faculty_id` 输入问号 (`?`)，按键盘回车键。
- 8. 将 `faculty_id` 行中 `Filter` 列的参数名称 `@Param1` 修改为 `@fid`。

![](img/d59a47501d0a20fc0460a49c469c6fb7_395_0.png)

图 7.3 查询生成器。

- 9. 删除最后一行之后所有行的内容，你的查询生成器向导应与图 7.3 所示一致。
- 10. 点击 OK 按钮进入下一个向导。删除 `WHERE` 子句下的 `SELECT` 语句，因为我们不需要此功能。点击“Next”按钮确认此查询并继续下一步。
- 11. 将查询函数名从默认值修改为 `UpdateFaculty`，并点击“Next”按钮进入最后一个向导。
- 12. 点击“Finish”（完成）按钮完成此查询构建并关闭向导。

执行以下操作来构建数据查询：

- 1. 在数据源窗口内任意位置点击右键，打开“数据源”窗口和“TableAdapter 查询配置向导”，从弹出菜单中选择 `Edit DataSet with Designer`。
- 2. 在打开的向导中，进入 `Faculty` 表，右键点击 `Faculty` 表中的最后一项，从弹出菜单中选择“Add Query item”（添加查询项）。
- 3. 保持默认选择“Use SQL statements”不变，点击“Next”按钮进入下一个向导。
- 4. 从此向导中选择并点击 `DELETE` 项，因为我们需要执行删除查询。点击“Next”按钮继续进入下一个向导。
- 5. 点击“Query Builder”按钮以构建我们的删除查询。打开的查询生成器向导如图 7.4 所示。
- 6. 删除整行 `faculty_id` 和行 `@IsNull_faculty_name`。移除 `faculty_name` 行中 `Filter` 和 `Or` 列的内容。
- 7. 在 `faculty_name` 行对应的 `Filter` 列中输入问号 (`?`) 并按键盘回车键。

![](img/d59a47501d0a20fc0460a49c469c6fb7_396_0.png)

图 7.4 删除查询生成器。

- 8. 将动态参数 `@Param1` 的名称更改为 `@fname`，按键盘回车键。
- 9. 你完成的查询生成器应与图 7.4 所示。点击 OK 按钮进入下一个向导。
- 10. 点击“Next”按钮确认此查询并继续下一步。
- 11. 将查询函数名修改为 `DeleteFaculty` 并点击“Next”按钮进入最后一个向导。
- 12. 点击“Finish”完成查询构建并关闭向导。立即，你会发现新的查询函数 `DeleteFaculty` 已作为最后一项添加到 `Faculty` TableAdapter 中。

接下来，让我们编写代码来调用这些查询方法，以执行相关的数据更新和删除操作。首先，让我们构建数据更新操作的代码。

## 7.2.2 使用 TableAdapter 直接方法开发更新代码

要使用查询方法执行数据更新，需要对 `Faculty` 表单中的原始代码进行一些修改。我们将这些修改分为两个部分：代码修改和代码创建。

首先，让我们对 `Faculty Form` 类中的代码进行一些修改。

### 7.2.2.1 代码修改

第一个修改是修改 `Faculty Form` 类中 `Form_Load()` 方法内部的代码。涉及两处修改：

- 1. 将第 6 章 6.5.2 中构建的自定义方法 `CurrentFaculty()` 添加到此处，用以更新 `Faculty Name` 组合框中的所有教职员，以便用户能够验证数据更新操作。
- 2. 在 `Query Method` 组合框中添加两个新的更新方法：
    - a) TableAdapterDirect Method
    - b) TableAdapter Update Method

打开 `Faculty Form` 窗口，使用 `Add` 方法向 `Form_Load()` 方法添加项。该方法的修改后的代码如图 7.5 中的步骤 A 和 B 所示。新添加的代码已**加粗**显示。

| SelectWizardProject | FacultyForm_Load(object sender, EventArgs e) |
|---|---|
| private void FacultyForm_Load(object sender, EventArgs e) | |
| A | CurrentFaculty(); ComboMethod.Items.Add("TableAdapter Method"); ComboMethod.Items.Add("LINQ & DataSet Method"); ComboMethod.Items.Add("TableAdapter Insert"); ComboMethod.Items.Add("TableAdapter Update"); ComboMethod.Items.Add("TableAdapter DBDDirect Method"); ComboMethod.Items.Add("TableAdapter Update Method"); this.ComboMethod.SelectedIndex = 0; ) |
| B | |

图 7.5 Form_Load 方法的修改后的代码。

### 7.2.2.2 代码创建

执行此数据更新的主要编码过程开发在 `Faculty Form` 窗口的 Update 按钮的 `Click` 方法中。打开此方法并将图 7.6 所示的代码输入其中。

让我们仔细观察这段新添加的代码，看看它是如何工作的。

- A. 首先声明了一些局部变量和对象，包括一个 `FacultyRow` 对象 `FacultyRow`，它用于存储在 `faculty` 表中要更新的新教职员；一个字符串 `facultyID`，用于保存根据所选教职员保存检索到的教职员 ID。这两个变量都用于 `TableAdapter Update` 数据更新方法。整数变量 `intUpdate` 也用于保存 `UpdateFaculty()` 查询方法的执行状态，以执行教职员记录的更新操作。`byte[]` 数组 `bmage` 用于存储要更新的选教职员图像。
- B. 如果选择了 `TableAdapter DBDirect Method`，则执行在第 6 章 6.5.3 节构建的自定义方法 `getFacultyImage()` 来获取更新的教职员图像，然后赋值给 `byte[]` 数组 `bmage`。
- C. 然后，使用第 7.2.1 节构建的查询 `UpdateFaculty()` 根据存储在 `Faculty Form` 窗口框中的八个教职员信息和选定的教职员图像来执行此教职员记录更新操作。查询的执行状态将返回并赋值给局部变量 `intUpdate`。
- D. 如果选择了 `TableAdapter Update Method`，我们需要在下一节中构建代码以执行此类数据更新操作。
- E. 通过检查变量 `intUpdate` 中的返回运行状态，我们可以判断数据更新是否成功。如果返回零值，意味着遇到了错误且数据更新失败，将显示一个带有警告消息的 `MessageBox` 来指示这种情况。

| WizardProject | cmdUpdate_Click(object sender, EventArgs e) |
| private void cmdUpdate_Click(object sender, EventArgs e) { CSE_DataSet.FacultyRow FacultyRow; string facultyID = null; int intUpdate = 0; byte[] bmage; if (SqlCommand.Method.Text == "TableAdaptDBDirectMethod") { bmage = getFacultyImage(); intUpdate = facultyTableAdapter.Update(facultyName.Text, txtTitle.Text, txtOffice.Text, txtPhone.Text, txtCollege.Text, txtEmail.Text, bmage, facultyID.Text); } else { //TableAdapter Update method selected } } if (intUpdate == 0) { MessageBox.Show("Faculty Updating is failed!"); } else { CurrentFaculty(); } |

图 7.6 更新命令按钮点击方法的代码。

