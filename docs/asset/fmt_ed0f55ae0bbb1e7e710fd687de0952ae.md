
```csharp
private void readAll(string sql)
{
    int nameIndex;
    int cardIndex;
    int count = 0;
    string result;
    string lastName;
    string whichCard;
    try
    {
        using (SqlConnection conn = new SqlConnection(connectStr))
        {
            conn.Open();
            SqlDataReader myReader = null;
            SqlCommand myCommand = new SqlCommand(sql, conn);
            myReader = myCommand.ExecuteReader();
            while (myReader.Read()) {
                nameIndex = (int)myReader[0];
                // 需要减一，因为它从零开始计数
                lastName = myFriends[nameIndex - 1].ToString();
                cardIndex = (int)myReader[1];
                whichCard = myCardList[cardIndex].ToString();
                result = string.Format("{0,-20} {1,-25} {2,-25} {3,-15}", lastName,
                    whichCard, myReader[2], myReader[3]);
                lstResult.Items.Add(result);
            }
            myReader.Close();
            conn.Close();
        }
    }
    catch (Exception ex) {
        MessageBox.Show("Error: " + ex.Message);
        if (count == 0) {
            MessageBox.Show("No data found");
        }
    }
}
```

`using` 语句建立了与数据库的连接并打开了该连接。通过命令对象 `SqlCommand` 的定义定义了一个数据读取器对象 `myReader`。在定义两个对象后，代码执行查询并通过调用 `Read()` 填充数据读取器。`Read()` 被放置在一个 `while` 循环中，以遍历查询返回的记录。读取器对象通过索引进行访问，如 `myReader[0]`。该索引指向返回记录的列位置。由于你正在读取 `ExChanged` 表，`myReader[0]` 返回发送（或接收）卡片的朋友的 ID。由于你将朋友的姓氏存储在 `myFriends` 数组中，你可以使用查询返回的索引来检索该朋友的姓氏。

`ExChanged` 表中的 `myReader[1]` 位于 `CardTypes` 表。由于 `myCardList` 持有卡片类型，你可以使用该索引来显示发送（或接收）的卡片类型的字符串。该语句

```csharp
result = string.Format("{0,-20} {1,-25} {2,-25} {3,-15}", lastName,
    whichCard, myReader[2], myReader[3]);
```

该语句简单地使用字符串 `Format()` 方法在将数据放入列表之前对其进行格式化。由于你希望列能够正确对齐，你可以更改 `lstResult` 的字体，使用固定字体（Courier New）而不是真字体（True Type font）。

## 编辑记录 (UPDATE)

在某个时间，你可能想要更改数据库中的某条目。人们会搬家、更改地址并改名。当此类事件发生时，你可能需要更改上述表之一中的数据。当你想要编辑已存储在数据库的信息时，使用 `UPDATE` 命令。图 14-17 显示了用于编辑 `Friends` 表中朋友的表单。

图 14-17：编辑数据库记录

当表单首次显示时，所有字段都是空的。如果你知道要编辑的朋友的记录编号，你可以在顶部的文本框中输入该记录编号（你可以使用搜索选项找到合适的记录）。如果你不知道记录编号，代码也接受人的姓名作为搜索条件。如果没有数据存在且你在 `Name` 文本框中输入了内容并点击 `Find`（查找）按钮，其余数据将显示（参见图 17）。虽然这可能并不明显，但 `Status` 字段是被禁用的，这意味着你不能编辑该字段，因为数据是由卡片的交换决定的。列表 14-6 显示了与 `Save`（保存）按钮相关的代码。

### 列表 14-6：编辑数据库记录 (frmEditFriend.cs)

```csharp
******
* Purpose: 在 Friends 表中保存信息
*
* 参数列表: 触发事件的发送者
* EventArgs e 关于发送者的详细信息
*
* 返回值:
* void;
*/
private void Save_Click(object sender, EventArgs e)
{
    int status;
    int flag;
    string sqlCommand;
    if (chkStatus.Checked == true)
        status = 1;
    else
        status = 0;
    myData = new clsFriend(connectStr);
    // 构建命令
    sqlCommand = "UPDATE Friends SET +
    "FirstName = '" + txtFirstName.Text +
    "LastName = '" + txtLastName.Text +
    "Addr1 = '" + txtAddr1.Text +
    "Addr2 = '" + txtAddr2.Text +
    "City = '" + txtCity.Text +
    "State = '" + txtState.Text +
    "Zip = '" + txtZip.Text +
    "LastContact = '" + txtLastContact.Text +
    "Status = '" + status.ToString() +
    "WHERE ID = '" + txtRecordNumber.Text + "";
    try {
        flag = myData.ProcessCommand(sqlCommand);
        if (flag > 0) {
            MessageBox.Show("记录更新成功。");
        } else {
            MessageBox.Show("更新数据失败。", "处理错误");
        }
    } catch (Exception ex) {
        MessageBox.Show("Error: " + ex.Message);
    }
}
```

变量 `myData` 连接到数据库，`sqlCommand` 构建了 `SET` 关键字，以及字段名和相关数据。命令构建完成后，它被传递给 `clsFriend` 类的 `ProcessCommand()` 方法。列表 14-7 显示了 `ProcessCommand()` 方法的代码。

### 列表 14-7：处理 SQL 查询 (clsFriend.cs)

```csharp
******
* Purpose: 处理数据库上的 SQL 命令
列表 14-7 (续)
* 参数列表: 包含 CREATE TABLE 指令的命令字符串
* stringCommand
* 返回值: 成功则为 1，否则为 0
* int
* 注意：该方法假设连接字符串已设置
public int ProcessCommand(string sqlCommand)
{
    int flag = 1;
    try
    {
        using (SqlConnection conn = new SqlConnection(connectString))
        {
            conn.Open();
            SqlCommand command = new SqlCommand(sqlCommand, conn);
            flag = command.ExecuteNonQuery(); // 添加新记录
            conn.Close();
        }
    }
    catch
    {
        flag = 0;
    }
    return flag;
}
```

处理命令的代码现在看起来应该很熟悉了。命令字符串 `sqlCommand` 打开连接并调用 `ExecuteNonQuery` 来处理 `UPDATE`。由于查询字符串被传递给 `ProcessCommand()`，该方法可以处理任何表上的任何 SQL 命令。因此，虽然这里讨论的程序没有提供编辑卡片类型或卡片交换的功能，但实现这些功能相当简单，这留给你作为练习。

### 总结

你在这一章中涵盖了大量内容。你现在对什么是数据库、如何创建和扩展数据库，以及其他如何操作数据库中的数据应该有了良好的理解。现在你已经讨论了卡片数据库的主要元素，你应该花一些时间调试代码。此外，尝试 `dataGridView` 控件并更改其某些属性，以观察其对行为的影响。这种努力是值得的。

# 练习题

你可以在附录 A 中找到以下练习答案。

- 1. 假设你使用第 13 章建议的数据结构定义了一个 Friends 表。请给出两个 SQL 命令，用于返回 Friends 表中活跃成员的数量。
- 2. 再次使用第 13 章的 Friends 数据结构，构造一个 SQL 语句，返回所有居住在印第纳州（或你可能使用的任何州）且第二个地址不为空的活跃成员。
- 3. `frmAddFriend` 中的代码有点像权宜之计，因为它与用户界面紧密耦合：

```csharp
// Build INSERT command
sqlCommand = "INSERT INTO Friends " + 
"(ID,FirstName,LastName,Addr1,Addr2,City,State, " + 
"Zip,LastContact,Status) VALUES ();";
// Now add the values
sqlCommand += records.Text + "," " " + 
txtFirstName.Text + "," " " + 
txtLastName.Text + "," " " + 
txtAddr1.Text + "," " " + 
txtAddr2.Text + "," " " + 
txtCity.Text + "," " " + 
txtState.Text.ToUpper() + "," " " + 
txtZip.Text + "," " " + 
txtLastContact.Text + "," " " + 
status + ");
```

之所以紧密耦合是因为输入与用于从用户处收集信息的 textbox 对象绑定了。因为你不希望在非 UI 类中使用 textbox，因此应该将类代码移动到 `clsDB` 类中。然而，如果能将 `frmAddFriend` 中用户界面代码的数据库 INSERT 命令移出并放入 `clsDB` 类就太好了。你会如何这样做呢？
- 4. 我不喜欢嵌套的 if 语句。在 `frmCardReport` 搜索按钮的点击事件代码中，你会看到六层嵌套的 if 语句。对我来说，这是 SDC 代码（某种垃圾堆代码）。原因是因为在某些情况下，你必须通过五个 if 测试才能进入正确的代码块。如果你使用 switch 语句代替，switch 变量测试结果将产生一个跳转指令，直接将控制发送到正确的代码块，从而避免不必要的 if 测试。重写代码以使用 switch 语句。

# 本章你学了什么

| 主题 | 关键点 |
|---|---|
| 数据库 | 一个以行列方式组织数据的文件。如果文件包含两个或多个相互相关的表，它就是关系数据库。 |
| 数据库的元素 | 数据库包含字段和记录的表。 |
| 数据库键 | 主键和外键用于关联表之间的信息。 |
| 规范化 | 如何从数据库中删除冗余数据。 |
| SQL | 用于从数据库中提取有用信息的结构化查询语言。 |
| 数据库 MDI | 如何将 MDI 系统与数据库结合使用。 |

# 15

# 使用 LINQ

在本章学习：

- 什么是 LINQ
- 如何使用 LINQ 查询数据对象
- `var` 关键字的含义
- 所需的 LINQ 命名空间
- 使用 LINQ 查询数据对象的优势

本章的 WROX.COM 代码下载
你可以在 `www.wrox.com/remtitle.cgi?isbn=9781118336922` 的 Download Code 标签页找到本章的 wrox.com 代码下载。Chapter15 文件夹中的代码根据整个章节中的名称分别命名。

SQL 简单易用；如果能将其简单性应用于数据库以外的数据结构，那不是很好吗？这正是微软 LINQ 设计初衷。LINQ 代表集成查询语言（Language Integrated Query），是 Visual Studio 2008 发布时的一个特性。

# 使用 LINQ

尽管你可以对关系数据库对象使用 SQL，但 LINQ 也可以查询数据库以外的对象类型，包括数组、XML 等。Visual Studio 直接整合了 LINQ 查询引擎，并定义了扩展方法以连接第三方数据源。

# 460 | 第15 章 使用 LINQ

正如 SQL 查询存储在内存中的数据集一样，LINQ 返回一个基于内存的对象集合。

# 查询关键字

SQL 语句使用了特定的关键字，而 LINQ 提供了类似的关键字。理解 LINQ 最简单的方法是尝试下面的简单示例。

# 尝试 LINQ 程序 (Chapter15ProgramLINQTest.zip)

在本示例中，程序生成最多（例如100 个）随机数并将它们显示在 listbox 对象中。

1. 在书中创建一个项目。
2. 从 wrox.com 下载 `Chapter15ProgramLINQTest.zip` 文件。
3. 创建具有两个 listboxes、五个 labels、两个 textboxes 和两个 button 对象的用户界面，如图 15-1 所示。用户在左侧的 textbox 中指定上限和下限（不包含）。查询结果显示在右侧的 listbox 中。图 15-1：示例运行。

# 它如何工作

# 代码 15-1：使用 LINQ (Main.cs)

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Windows.Forms;
public class frmMain : Form
{
    const int MAXNUM = 100; // 随机数
    List<int> numbers = new List<int>(); // 
    private Button btnCalc;
    private ListBox lstOutput;
    private ListBox lstFull;
    private TextBox txtLow;
    private TextBox txtHi;
    private Label label1;
    private Label label2;
    private Label label3;
    private Label label4;
    private Label label5;
    #region 构造函数
    public frmMain()
    {
        InitializeComponent();
    }
    #endregion
    #region 程序开始
    public static void Main()
    {
        frmMain main = new frmMain();
        Application.Run(main);
    }
    #endregion
    #region 辅助方法
    private void btnCalc_Click(object sender, EventArgs e)
    {
        lstOutput.Clear();
        SetLimits(out lo, out hi);
        DoQQuery(lo, hi);
    }
    private void GenerateRandomValues()
    {
        int temp;
        DateTime current = DateTime.Now;
        Random rnd = new Random((int)current.Ticks);
        for (int i = 0; i < MAXNUM; i++)
        {
            temp = rnd.Next(MAXNUM);
            numbers.Add(temp);
            lstFull.Add(temp.ToString());
        }
    }
    private void SetLimits(out int lo, out int hi)
    {
```
