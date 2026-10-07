

# 使用 C# 进行 SQL Server 数据库编程

| s_course_id | student_id | course_id | credit | major |
|---|---|---|---|--|
| 1002 | T77896 | CSC-335 | | 3 CS/IS |
| 1005 | T77896 | CSC-234A | | 3 CS/IS |
| 1010 | T77896 | CSC-439 | | 3 CS/IS |
| 1015 | T77896 | CSC-432 | | 3 CS/IS |
| 1020 | T77896 | CSC-429 | | 3 CS/IS |
| 1024 | T77896 | CSC-333A | | 3 CS/IS |

**9.109** 已在 StudentCourse 表中删除。

| student_name | gpa | credits | major | schoolYear | email | simage |
|---|---|---|---|---|---|--|
| Tom Erica | T77896 | 3.95 | 127 | Computer Science | Senior | terica@college.edu | NULL |

**9.110** 已在 student 表中删除。

我们已经完成了 Web 服务项目的开发，接下来让我们构建一些客户端项目来调用我们的 Web 服务项目，以便从示例数据库中更新和删除学生记录。

## 9.6 构建基于 Windows 的客户端项目以消费 Web 服务

为了节省时间和所在空间，我们不需要创建任何新的 Windows 项目并进行完整的开发。相反，我们可以复制并修改我们在第 7 章第 7.5 节开发的现有 Windows 项目 **SPUpdateDelete Project**。从 CRC Press ftp 站点中 **Students** 文件夹下的 ClassDB\Project 7 文件夹中复制该项目（参见第 1 章的图 1.2），并将其粘贴到我们的新项目路径 C:\Chapter 9 中。

让我们对该项目进行必要的修改，使其成为我们的新项目。修改可以分为两个部分：

- 1. 为我们的新客户端项目添加 Web 引用（Web reference）。
- 2. 在代码窗口中为两个按钮的点击事件方法编写代码。

首先，让我们执行第一部分的修改。

### 9.6.1 为我们的客户端项目添加新的 Web 引用

为了使用我们在上一节开发的 Web 服务 **WebServiceUpdt Project**，我们首先需要添加一个 Web 引用以连接到该服务项目。执行以下操作来添加此 Web 引用：

- 1. 打开 Web 项目 **WebServiceUpdt Project**，点击 IIS Express 按钮运行它。
- 2. 从正在运行的 Web 服务项目的 **Address** 栏中复制 URL。
- 3. 然后打开我们的 Windows 客户端项目 **SPUpdateDelete Project**。
- 4. 在解决方案窗口中右键点击客户端项目 **SPUpate Project**，从弹出菜单中选择 **Add | Service Reference**（添加 | 服务引用），打开添加服务引用向导。
- 5. 点击左下角的 **Advanced**（高级）按钮，打开服务引用设置向导。

## ASP.NET Web Services

![](img/d59a47501d0a20fc0460a49c469c6fb7_647_0.png)

图 9.111 打开的添加引用向导。

- 6) 点击 **Add Reference**（添加引用）按钮进入添加 Web 引用向导，如图 9.111 所示。
- 7) 将我们在步骤 2 中复制的 URL 粘贴到 URL 框中，并点击**箭头**按钮让 Visual Studio.NET 开始搜索。
- 8) 当找到服务时，右侧面板将显示服务的名称，如图 9.111 所示。
- 9) 理想情况下，你可以将此 Web 引用的名称从 **localhost** 更改为有意义的名字，在我们案例中可以是 **WS_SQLUpdt**。点击 **Add Reference**（添加引用）按钮将此服务作为引用添加到我们的新客户端项目中。
- 10) 点击服务内置 Web 窗口上的 **Close**（关闭）按钮结束我们的服务项目。

接下来，让我们构建并修改相关事件方法和用户定义方法代码，调用我们的服务以执行所需的数据操作。

### 9.6.2 为更新按钮点击方法编写代码

打开此事件代码，并将图 9.12 中的代码添加到此方法中。让我们仔细查看这段代码，看看它是如何工作的。

- A. 声明了两个本地引用对象：**wsSQLUpdt** 和 **wsResult**，并通过这些引用访问我们的 Web 服务项目。
- B. 声明了一个图像对象 **blmage**，并通过一个字节数组来存储更新后的学生图像。调用用户定义方法 **getStudentImage()** 来获取要在示例数据库中更新的目标学生图像。
- C. 通过 Web 引用对象 **wsSQLUpdt** 执行我们的方法 **SQLupdateSP()**，传入七条更新后的学生信息。

# 使用 C# 进行 SQL Server 数据库编程

| cmdUpdate_Click(object sender, EventArgs e) |
|---|
| private void cmdUpdate_Click(object sender, EventArgs e) { 
| A WS_WSQLUpDt |
| B WS_WSQLUpDt |
| C WS_WSQLUpDt |
| D WS_WSQLUpDt |
| E WS_WSQLUpDt |
| F WS_WSQLUpDt |
| G WS_WSQLUpDt |
| H WS_WSQLUpDt |

