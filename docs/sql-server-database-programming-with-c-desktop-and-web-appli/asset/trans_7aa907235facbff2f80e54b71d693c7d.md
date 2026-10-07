

# ASP.NET 服务

| WebServiceInsertPoint | FillCourseDetail() |
|---|---|

```csharp
protected void FillCourseDetail(ref SQLInsertRecord sResult, SqlDataReader sReader)
{
    sReader.Read();
    sResult.FacultyID = System.Convert.ToString(sReader("facultyID"));
    sResult.Course = System.Convert.ToString(sReader("course"));
    sResult.Schedule = System.Convert.ToString(sReader("schedule"));
    sResult.Classroom = System.Convert.ToString(sReader("classroom"));
    sResult.Credit = System.Convert.ToInt32(sReader("credit"));
    sResult.Enrollment = System.Convert.ToInt32(sReader("enrollment"));
}
```

**图 9.6** FillCourseDetail() 方法的代码。

C. 查询的课程记录的每一列都被分配给我们子类中相关的成员数据。使用了两个系统方法：`Convert.ToString()` 和 `Convert.ToInt32()` 将所有数据转换为适用于赋值的适当类型。对于这一点，可以在页面顶部通过添加 `System;` 来使用 System 命名空间，从而直接使用 Convert 类而无需加 System 前缀。

现在让我们构建并运行我们的到该 Web 方法的项目。点击 IIS Express 按钮运行项目。从内置的 Web 界面中选择我们的 `GetCourse()` 方法，在 Value 框中输入 `CSE-665` 作为课程 ID，然后点击 Invoke 运行此 Web 方法。该方法的的结果显示在图 9.68 中。

六条课程信息以 XML 标签的形式显示。记住，在我们的子类中，`course_id` 是维度为 10 的数组 `Course[]`。该成员数据被用于我们的第二个 Web 方法 `GetFirst()`。由于我们没有在此方法中使用它，元素 `CourseID[]` 数组被设置为 `true` 并显示在生成的生成文件中。

![](img/d59a47501d0a20fc0460a49c469c6fb7_607_0.png)

**图 9.68** 我们的 Web 方法 GetInsertCourse() 的运行结果。

# 580 使用 C# 进行 SQL 数据库编程

点击此 Web 界面右上角的 Close 按钮以终止我们的服务。可以在 CRC Press 过滤器中 Students 文件夹下的 `ClassDB Projects\Chapter 9\WebServiceInsert` 文件夹中找到完整的 Web 服务项目 `WebServiceInsert`（请参见第 1 章中的图 1.2）。

至此，我们已经完成了 Web 项目中服务端的所有代码工作。接，，我们需要开发一些具有精美图形用户界面的专业级基于 Windows 和基于 Web 的应用程序项目，以使用或调用在该 Web 服务项目 `WebServiceInsertProject` 中开发的 Web 服务应用程序。这些基于 Windows 和基于 Web 的应用程序可以开发为 Web 服务客户端。

## 9.4.3 构建基于 Windows 的客户端以调用 Web 服务

要使用或调用 Web 服务，我们首先需要在基于 Windows 或基于 Web 的应用程序中创建一个 Web 服务代理类。然后，我们可以创建 Web 服务代理类的新实例，并在该服务类中执行所需的 Web 服务方法。创建 Web 服务代理类的过程等同于向我们的基于 Windows 或基于 Web 的应用程序中添加 Web 引用。

### 9.4.3.1 创建基于 Windows 的消费者和 Web 服务代理类

基本上，向我们的基于 Windows 或基于 Web 的应用程序添加 Web 引用就是执行一次搜索。在此过程中，Visual Studio.NET 2022 将找到我们应用程序可用的所有 Web 服务。

以管理员模式打开 Visual Studio.NET 2022，并创建一个新的 C# Windows Forms App (.NET Framework)，将其命名为 `WinClientInsertProject` 并保存到文件夹 `C:\Chapter 9.3.11`，以便为新项目添加 Web 引用。参考第 9.3.12 节开始此 Web 引用。执行以下操作完成完成：

- 打开我们的 Web 服务项目 WebInsert，并点击 IIS 按钮运行它。
- 从运行的 Web 服务项目的地址栏中复制 URL。
- 然后从解决方案管理器打开我们的基于 Windows 的客户端 `WinClientInsertProject`。
- 右键点击客户端，从弹出菜单选择 `Add | Service Reference` 打开添加服务引用。
- 点击此窗口左下角的 `Advanced` 按钮打开服务设置。
- 点击 `Add Reference` 按钮打开 Web 引用向导，如图 9.6 所示。
- 将从步骤 2 复制的 URL 粘贴到 Add Reference 向导的 URL 框中，并点击按钮让 Visual Studio.NET 开始搜索。
- 当找到 Web 服务时，右侧面板会显示我们的服务的名称，如图 9.6 所示。
- 或者，你可以在类中将此 Web 引用的名称从 `localhost` 更改为任何有意义的，例如 `WS_SQLInsert`。点击 `Add Reference` 按钮将 Web 服务作为新的客户端项目添加。
- 点击 Web 服务窗口上的 `Close` 按钮以终止我们的项目。

立即，你会发现 `References` 文件夹下的 Web 服务 `WS_SQLInsert` 已经添加到我们客户端项目的解决方案管理器中。该引用就是 Web 服务代理类。

![](img/d59a47501d0a20fc0460a49c469c6fb7_608_0.png)

# ASP.NET Web 服务

581

![](img/d59a47501d0a20fc0460a49c469c6fb7_609_0.png)

**图 9.6** 完成的 Web 引用向导。

接下来，让我们通过添加有用的控件来开发图形界面，以调用服务并显示课程信息。

### 9.4.3.2 为客户端开发图形界面

对新客户端执行以下修改：

- 将表单从默认名称 `Form1` 重命名为 `WinClient`。
- 将窗口从默认名称 `Form1` 重命名为 `CourseForm` 并修改 Name 属性。
- 将表单从默认名称 `Form1` 重命名为 `CourseForm`。
- 将表单窗口的 `StartPosition` 属性设置为 `CenterScreen`。

为了节省时间和空间，我们可以使用第 7 章中开发的 `RTODelete` 项目表单。你可以在 CRC Press 站点 Students 文件夹下的 `ClassDB Projects\Chapter7\RTODelete` 找到该项目（参见图 1.2）。执行以下操作将课程添加到新客户端：

- 打开 RTODelete 项目和 Course 表单窗口。
- 通过 `Edit | Select All` 和 `Edit | Copy` 选择该表单中的所有控件。
- 返回我们基于 Windows 的客户端 `WinClientInsertProject`，打开 `CourseForm` 表单窗口并将从步骤 2 复制的控件粘贴到此表单中。

# 502 使用 C# 进行 SQL 数据库编程

![](img/d59a47501d0a20fc0460a49c469c6fb7_610_0.png)

**图 9.7** 完成的图形界面。

