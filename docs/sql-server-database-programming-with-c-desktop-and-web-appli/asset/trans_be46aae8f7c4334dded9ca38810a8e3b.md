

# 346 使用 C# 进行 SQL Server 数据库编程

| RTOInsert 项目 | ClearFaculty() |
| :--- | :--- |

```csharp
private void ClearFaculty() {
    int index;
    Text[] fbox = {txtFacultyID, txtFacultyName, txtTitle, txtOffice, txtPhone, txtCollege, txtEmail};
    for (index = 0; index < fbox.Length; index++)
        fbox[index].Text = "";
}
```

图 6.34 ClearFaculty() 方法详细代码。

| RTOInsert 项目 | getFaceImage() |
| :--- | :--- |

```csharp
private byte[] getFaceImage() {
    MemoryStream ms = new MemoryStream();
    OpenFileDialog dig = new OpenFileDialog();
    byte[] bimage = null;
    dig.Filter = "JPG Files (*.jpg)|*.jpg|All Files (*.*)|**";
    dig.Title = "Select the Faculty Image";
    if (dig.ShowDialog() == DialogResult.OK) {
        PhotoBox.Image = Image.FromFile(dig.FileName);
        PhotoBox.Image.Save(ms, PhotoBox.Image.Format);
        bimage = ms.ToArray();
    }
    return bimage;
}
```

图 6.35 getFaceImage() 方法代码。

让我们仔细查看这段代码，看看它是如何工作的。

- A. 首先声明了一些本地对象，包括一个 MemoryStream 类对象和一个 OpenFileDialog 类对象，即 ms 和 dig。前者被用作中间转换图像数组，后者提供一个文件对话框，允许用户选择要插入我们数据库的教师图像。还会生成并返回一个 `byte[]` 数组 `bimage`，因为 SQL Server 中存储图像的唯一数据类型是 byte。
- B. 初始化 OpenFileDialog 类对象 dig 并设置 Filter 和 Title 属性。前者用于定义要选择的图像类型，后者为对话框提供标题。
- C. 如果系统 `ShowDialog()` 执行成功，它将返回一个常量，`DialogResult.OK` 表示 `OpenFileDialog` 已打开且用户已选择有效的教师图像。首先，使用 `FromFile()` 方法读取所选图像，并将其赋值给 Faculty Form 窗口中教师图像控件 PhotoBox 的 `Image` 属性，然后将该图像转换为 MemoryStream 格式，并通过系统方法 `Save()` 保存到 MemoryStream 对象 `ms` 中。
- D. 最后，转换后的图像通过 `ToArray()` 方法进一步转换为字节数组。
- E. 将转换后的图像数组返回给调用方法。

# 使用 Visual C#.NET 插入数据

| RTOInsert 项目 | txtFacultyID_TextChanged() |
| :--- | :--- |
| private void txtFacultyID_TextChanged(object sender, EventArgs e) { cmdInsert.Enabled = true; } |

**图 6.36** 教师 ID TextBoxChanged 方法的代码。

最后的一项编码工作是针对教师 ID  TextBox，专门用于教师文本框的 **TextChanged** 事件及其方法。正如我们提到的，为了避免重复插入相同数据，在完成一次数据插入后，应该禁用 **Insert**（插入）按钮。当教师 ID 文本框的内容发生变化时，应该重新启用该 **Insert** 按钮，这意味着要向数据库插入不同的记录。

从表单（Form）窗口双击教师 ID TextBox 以打开此方法，并将图 6.36 中的代码输入到该方法中。

现在我们准备好运行项目，测试我们开发的代码，以向示例数据库中的 **Faculty** 数据表插入一条新记录。点击 **Start**（启动）按钮运行项目，完成登录过程并打开表单窗口。在 TextBox 中输入以下数据作为新记录：

| 教师 ID | W56788 |
| :--- | :--- |
| 教师姓名 | Steve Wang |
| 职称 | Professor |
| 办公室 | MTC-311 |
| 电话 | 750-378-2258 |
| 学院 | University of Miami |
| 邮箱 | swang@college.edu |

点击 **Insert** 按钮将此新记录插入数据库中的 **Faculty** 表。在打开的文件对话框窗口中，浏览到存储所有教师图像的文件夹。实际上，所有教师图像都存储在 **Students** 文件夹下的 **Images\Faculty** 文件夹中（位于 CRC 文件路径，参见第 1 章的图 1-2）。你可以从该文件夹复制所有教师图像并将其保存到用户机器的本地文件夹中。现在浏览到该本地文件夹并选择教师图像 **Wang.jpg**，然后点击 **Open**（打开）按钮。

数据插入成功后立即！**Insert** 按钮将被禁用。要检查并验证此新插入的记录，可以使用两种方法：1) 使用 **Select**（选择）按钮的 Click 方法尝试从我们的数据库中检索这条新插入的记录；2) 打开我们的示例数据库并验证 **Faculty** 表以确认此数据插入。

首先，使用 **Faculty Name**（教师姓名）组合框并点击其下拉，可以发现新插入的教师 **Steve Wang** 已添加到此框中。选择它并点击 **Select** 按钮尝试取回该记录。立即，所有新插入的信息片段（包括所选的教师图像）都会显示在 Faculty Form 窗口中，如图 6.37 所示。

![](img/d59a47501d0a20fc0460a9c469c6fb77_376_0.png)

图 6.37 新插入的教师卡片。

从 Faculty Form 和选择窗口点击 **Back**（返回）和 **Exit**（退出）按钮关闭我们的项目。

要使用第二种方法确认此数据，可以使用 Server Explorer（服务器资源管理器）进行插入并执行以下操作以打开我们的 **Faculty** 表：

- 1. 点击 Server Explorer 中数据库左侧的箭头连接到我们的示例数据库。
- 2. 展开数据库文件夹和 **Tables** 表找到 **Faculty** 表。
- 3. 右键点击我们的 **Faculty** 表并选择 **Show Data**（显示数据）项打开 Faculty 表。
- 4. 浏览到此表的底部，可以发现新插入的教师卡片，如图 6.38 所示。

| faculty_id | faculty_name | title | office | phone | college |
| :--- | :--- | :--- | :--- | :--- | :--- |
| A52990 | Black Anderson | Professor | MTC-218 | 750-378-9987 | Virginia Tech |
| A73857 | Debye Angus | Associate Prof. | MTC-320 | 750-330-2276 | University of FL |
| B66750 | Brown Alice | Associate Prof. | MTC-250 | 750-370-4669 | Alabama of |
| B78680 | Yang Henri | Associate Prof. | MTC-118 | 750-378-1148 | Florida Atlantic |
| B88590 | Dalla Bahia | Professor | MTC-214 | 750-378-1001 | University of N |
| M18318 | Jerry King | Professor | MTC-250 | 750-370-4669 | Texas State |
| J3486 | Steve Johnson | Distinguished P | MTC-118 | 750-330-1116 | Harvard Univ |
| K9890 | Jenny King | Professor | MTC-324 | 750-330-1116 | East Florida |
| W56788 | Steve Wang | Professor | MTC-311 | 750-378-2258 | University of M |
| NULL | NULL | | | | |

图 6.38 打开的 Faculty 表。

# 使用 Visual C#.NET 插入数据

# 使用存储过程插入 SQL 数据库

在本节中，我们将讨论如何使用存储过程进行数据插入。为了节省时间和空间，我们将对上一节构建的 RTOInsert 项目尝试使用存储过程进行数据插入。执行以下操作以修改我们的项目：

