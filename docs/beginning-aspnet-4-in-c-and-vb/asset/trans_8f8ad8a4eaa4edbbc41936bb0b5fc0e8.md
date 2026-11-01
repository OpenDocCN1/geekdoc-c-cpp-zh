
```
<td align="center" colspan="3">
<asp:ValidationSummary ID="validationSummary" runat="server"
HeaderText="Before submitting your request:" />
</td>
</tr>
</table>
</div>
<div>
<p>
Results:
<asp:Label runat="server" ID="resultLabel" Text="None." />
</p>
</div>
</form>
</body>
</html>
```

在设计视图中，你创建的表单如图 40-7 所示。这是一个功能完整的 UI，它会在服务器请求之间保持自身状态，并验证用户输入。考虑到前面的代码如此简短，这已经相当不错了。事实上，它给你留下的工作很少，至少就这个示例而言；你只需要为提交按钮指定按钮单击事件。

![](img/d7d2ffa0a76feaab821930e95daace93_1228_0.png)

图 40-7

其实这样说并不完全准确。到目前为止，你还没有为日历控件设置验证。你只需要为它提供一个初始值。你可以在代码隐藏文件的 `Page_Load()` 事件处理程序中完成：

```
protected void Page_Load(object sender, EventArgs e)
{
    if (!this.IsPostBack)
    {
        calendar.SelectedDate = DateTime.Now;
    }
}
```
代码片段 PCSWebsite2/Default.aspx.cs

这里你只是把今天的日期选择为起点。请注意，你首先通过检查页面的 `IsPostBack` 属性，判断 `Page_Load()` 是否是由回发操作调用的。如果正在进行回发，该属性将为 true，此时你不会改动所选日期（毕竟你不想丢失用户的选择）。

要添加按钮单击处理程序，只需双击按钮并添加以下代码：

```
protected void submitButton_Click(object sender, EventArgs e)
{
    if (this.IsValid)
    {
        resultLabel.Text = roomList.SelectedItem.Text + " has been booked on " + calendar.SelectedDate.ToLongDateString() + " by " + nameBox.Text + " for " + eventBox.Text + " event.";
        foreach (ListItem attendee in attendeeList.Items)
        {
            if (attendee.Selected)
            {
                resultLabel.Text += attendee.Text + ", ";
            }
        }
        resultLabel.Text += " and " + nameBox.Text + " will be attending.";
    }
}
```

这里你只是将 `resultLabel` 控件的 `Text` 属性设置为一个结果字符串，它随后会显示在主表下方。在 IE 中，这种提交的结果看起来可能如图 40-8 所示，除非存在错误；如果有错误，`ValidationSummary` 会取而代之被激活，如图 40-9 所示。

![](img/d7d2ffa0a76feaab821930e95daace93_1229_0.png)

图 40-8

![](img/d7d2ffa0a76feaab821930e95daace93_1230_0.png)

图 40-9

## ADO.NET 与数据绑定

你在上一节创建的网站功能上是完整的，但它只包含静态数据。此外，事件预订流程也没有包含事件数据的持久化。要同时解决这两个问题，你可以使用 ADO.NET 访问存储在数据库中的数据，从而连同房间和与会者列表一起存储和检索事件数据。

数据绑定让检索数据的过程变得更加容易。列表框等控件（以及稍后你会看到的某些更专门的控件）天生支持这项技术。它们可以绑定到任何公开 `IEnumerable`、`ICollection` 或 `IListSource` 接口的对象，也可以绑定到任何数据源 Web 服务器控件。

在本节中，你先把事件预订应用程序更新为支持数据，然后再借助其他数据感知 Web 控件，看看数据绑定还能实现哪些其他结果。

### 更新事件预订应用程序

为了与上一个示例保持独立，请在 `C:\ProCSharp\Chapter40\` 目录中新建一个名为 `PCSWebSite3` 的空网站，并将之前创建的 `PCSWebSite2` 应用程序中的代码复制到这个新应用程序中。在开始编写新代码之前，先看一下你将访问的数据库。

### 数据库

出于本示例的考虑，你将使用一个名为 `MeetingRoomBooker.mdf` 的 Microsoft SQL Server Express 数据库，它是本书可下载代码的一部分。对于企业级应用，使用完整版 SQL Server 数据库更有意义，但这里所涉及的技术几乎完全相同，而且 SQL Server Express 会让测试稍微容易一些。代码也会完全相同。

> 如果你要添加自己的数据库版本，则需要将新数据库添加到网站中名为 App_Data 的文件夹中。这是 ASP.NET 网站中可以存在的几个“特殊”文件夹之一；你可以通过选择“网站 ▸ 添加 ASP.NET 文件夹 ▸ App_Data”来添加它。要将新数据库添加到此文件夹，请右键单击新的 App_Data 文件夹，选择“添加新项”，然后选择“SQL Server 数据库”选项。将新数据库命名为 `MeetingRoomBooker`，再单击“添加”。这还会在“服务器资源管理器”窗口中配置好一条可以直接使用的数据连接。接下来，你可以按后续各节所示添加所需表，并提供自己的数据。或者，要在自己的代码中使用可下载的数据库，只需将其复制到网站的 App_Data 目录即可。

随附的数据库包含三张表：

- Attendees，包含可能的与会者列表
- Rooms，包含可用于举办事件的房间列表
- Events，包含已预订的事件列表

### Attendees

Attendees 表包含下表中所示的列。

| 列 | 类型 | 说明 |
|---|---|---|
| ID | 标识，主键 | 与会者标识号 |
| Name | varchar，必填，50 字符 | 与会者姓名 |
| Email | varchar，可选，50 字符 | 与会者电子邮件地址 |

随附的数据库包含 20 名与会者的记录，每人都配有各自（虚构的）电子邮件地址。可以设想，在更成熟的应用程序中，可以在完成预订时自动向与会者发送电子邮件，但这留给你作为可选练习，可使用本书其他地方介绍的技术来实现。

### Rooms

Rooms 表包含下表中所示的列。

| 列 | 类型 | 说明 |
|---|---|---|
| ID | 标识，主键 | 房间标识号 |
| Room | varchar，必填，50 字符 | 房间名称 |

数据库中提供了 20 条记录。

### Events

Events 表包含下表中所示的列。

| 列 | 类型 | 说明 |
|---|---|---|
| ID | 标识，主键 | 事件标识号 |
| Name | varchar，必填，255 字符 | 事件名称 |
| Room | int，必填 | 事件所在房间的 ID |
| AttendeeList | text，必填 | 与会者姓名列表 |
| EventDate | datetime，必填 | 事件日期 |

可下载数据库提供了一些事件记录。

### 绑定到数据库

你要绑定到数据的两个控件是 `attendeeList` 和 `roomList`。在此之前，你需要添加对应到 `MeetingRoomBooker.mdf` 数据库中要访问的表的 `SqlDataSource` Web 服务器控件。最快的方法是把它们从工具箱拖到 `Default.aspx` Web 窗体上，然后通过配置向导进行配置。图 40-10 展示了如何为 `SqlDataSource` 控件打开此向导。

![](img/d7d2ffa0a76feaab821930e95daace93_1232_0.png)

图 40-10

在“数据源配置向导”的第一页中，你需要选择之前创建的数据库连接。接下来，选择将连接字符串保存为 `MRBConnectionString`；然后选择从数据库的 `Attendees` 表中选择 `*`（所有字段）。

完成向导后，将 `SqlDataSource` 控件的 ID 改为 `MRBAttendeeData`。你还需要再添加两个 `SqlDataSource` 控件，分别从 `Rooms` 表和 `Events` 表获取数据，ID 值分别为 `MRBRoomData` 和 `MRBEventData`。对于这些后续控件，你可以使用已保存的 `MRBConnectionString` 作为连接。

添加这些数据源后，你会看到表单代码中的语法非常简单：

```
<asp:SqlDataSource ID="MRBAttendeeData" runat="server"
ConnectionString="<%$ ConnectionStrings:MRBConnectionString %>"
SelectCommand="SELECT * FROM [Attendees]"></asp:SqlDataSource>
<asp:SqlDataSource ID="MRBRoomData" runat="server"
ConnectionString="<%$ ConnectionStrings:MRBConnectionString %>"
SelectCommand="SELECT * FROM [Rooms]"></asp:SqlDataSource>
<asp:SqlDataSource ID="MRBEventData" runat="server"
ConnectionString="<%$ ConnectionStrings:MRBConnectionString %>"
SelectCommand="SELECT * FROM [Events]"></asp:SqlDataSource>
```
代码片段 PCSWebSite3/Default.aspx

所用连接字符串的定义位于 `web.config` 文件中，本章稍后会更详细地介绍它。

接下来，你需要设置 `roomList` 和 `attendeeList` 控件的数据绑定属性。`roomList` 所需的设置如下：

- DataSourceID — `MRBRoomData`
- DataTextField — `Room`
- DataValueField — `ID`

同样，对于 `attendeeList`：

- DataSourceID — `MRBAttendeeData`
- DataTextField — `Name`
- DataValueField — `ID`

你还可以从这些控件的代码中删除现有的硬编码列表项。

现在运行应用程序，数据绑定控件就会提供完整的与会者和房间数据。稍后你将使用 `MRBEventData` 控件。
