
现在，当你使用 `BindingNavigator` 更改选定的 Author 时，相应的标题将显示在 `DataGridview` 中。

```c
// Fig. 22.37: Details.cs
// 使用 DataGridView 根据选择显示详情。
using System;
using System.Data.Entity;
using System.Linq;
using System.Windows.Forms;

namespace MasterDetail {
    public partial class Details : Form {
        InitializeComponent();
    }

    // Entity Framework DbContext
    BooksExamples.BooksEntities dbcontext = new BooksExamples.BooksEntities();
    
    // 当 Form 加载时初始化数据源
    private void Details_Load(object sender, EventArgs e) {
        // 按 LastName 后 FirstName 排序 Authors 表
        dbContext.Authors
            .OrderBy(author => author.LastName)
            .ThenBy(author => author.FirstName)
            .Load();
    }
    // 为 authorBindingSource 指定 DataSource
    authorBindingSource.DataSource = dbcontext.Authors.Local;
}
```

图. 22.37 | 使用 DataGridView 根据选择显示详情。

## 22.9 地址簿案例研究

我们的最后一个示例实现了一个简单的 AddressBook 应用（带有图 22.38–40 中的示例输出），该应用允许用户对数据库 AddressBook.mdf（包含包含在本章示例的目录中）执行以下任务：

- 插入新联系人。
- 查找姓以指定字母开头的联系人。
- 更新现有联系人。
- 删除联系人。

我们在数据库中填充了六个虚构联系人。

## 22.9 地址簿案例研究

![](img/57baed2319be0bb1b5f98674846f2711_969_0.png)

图. 22.38 | 使用 BindingNavigator 的控件在联系人之间导航。

![](img/57baed2319be0bb1b5f98674846f2711_969_1.png)

图. 22.39 | 在 Last Name TextBox 中输入搜索字符串，然后按 Find 查找姓以该字符串开头的联系人。只有两个名字以 Br 开头，因此 BindingNavigator 显示两个匹配记录中的第一个。

![](img/57baed2319be0bb1b5f98674846f2711_969_2.png)

图. 22.40 | 点击 Browse All Entries 清除搜索并返回浏览所有联系人。

## 第 22 章 数据库与 LINQ

该应用并不是在 DataGridView 中显示数据库表，而是通过多个 TextBox 一次显示一个联系人的详情。窗口顶部的 BindingNavigator 允许你控制在任何时刻显示表格中的某行。BindingNavigator 还允许你添加和删除联系人——但只有在浏览完整联系人列表时才可以。按姓过滤联系人时，应用程序将禁用 Add new

![](img/57baed2319be0bb1b5f98674846f2711_970_0.png)

Delete

![](img/57baed2319be0bb1b5f98674846f2711_970_1.png)

按钮（我们稍后会解释）。点击 Browse All Entries 将启用这些按钮。添加一行将清除 TextBoxes并将 Address ID 右侧的 TextBox 设置为 0，以表示 TextBoxes 现在代表一条新记录。当你保存条目时，Address 字段会自动由数据库从 0 更改为唯一的 ID 号。除非你点击 Save Data：否则不会对底层数据库进行任何更改。

### 22.9.1 创建地址簿应用程序的 GUI

我们稍后会讨论应用程序的代码。首先，你将设置一个新的包含实体模型和 Windows Forms App 的解决方案。关闭在本章之前的示例中使用的 BooksExamples 解决方案。

步骤 1：为实体数据模型创建类库项目
执行第 22.5 节中的步骤，创建一个名为 AddressExample 的类库项目，该项目包含 AddressBook.mdb 数据库的实体数据，该数据库仅包含包含 AddressID、FirstName、LastName、Email 和 PhoneNumber 列的 Addresses 表。将实体数据模型设为 AddressModel。AddressBook.mdb 数据库位于本章示例的 Databases 文件夹中。

步骤 2：为地址簿应用创建 Windows 项目
执行第 22.5.2 节中的步骤，在 AddressExample 解决方案中创建一个名为 AddressBook 的新 Windows 项目。将 Form 的文件名设置为 Contacts.cs，然后将 Form 的 Text 属性设置为 Address Book。将 AddressBook 项目设为解决方案的启动项目。

步骤 3：将 Address 对象作为数据源
将实体数据 Address 对象作为数据源，就像你在第 22.5 节的步骤 1 中对 Author 执行的那样。

步骤 4：显示每行的详情
在设计视图中，在 Data Sources 窗口中选择 Address 节点。点击 Address 的箭头并选择 Details 选项，指示 IDE 应该创建一组 Label-TextBox 对来一次显示单条记录的详情。

## 22.9 地址簿案例研究

步骤 5：将 Address 节点拖到 Form 上
从 Form 拖动节点。这会自动创建 Navigator 和 TextBoxes。在设计视图中，在 Data Sources 窗口中选择 Address 节点。点击 Address 的箭头并选择 Details 选项，指示 IDE 应该创建一组 Label-TextBox 对来一次显示单条记录的详情。

步骤 5：将 Address 设置为只读
虽然我们在程序期间维护了一个 dbcontext，如果用户更改了姓氏，记录将保持在内存中的顺序。第 36–39 行对对象。

步骤 6：添加控件允许用户指定姓氏
为了允许用户搜索，添加名为 findLabel 的 Label、名为 findTextBox 的 TextBox 和名为 findButton 的按钮。将这些控件放在 findGroup 中，然后设置 Name。

步骤 7：允许用户返回浏览
为了允许用户在搜索后返回所有联系人，添加名为 browseAll 的按钮。

## 22.9.2 地址簿应用代码

Contacts.cs 后台代码分为几个图表（图 22.41–45）以便于。

Refresh 方法
如之前的示例所示，我们必须将地址源与数据库连接。在本示例中，我们声明了 DbContext。在第 22 行创建一个新的 DbContext。我们这样做是为了根据编辑重新排序记录。

```c
// Fig. 22.41: Contact.cs
// 操作地址簿。
using System;
using System.Data;
using System.Data.Entity;
using System.Data.Validation;
using System.Linq;
using System.Windows.Forms;

namespace AddressBook
{
    public partial class Contacts : Form
    {
        public Contacts()
        {
            InitializeComponent();
        }

        // Entity Framework DbContext
        private BindingExample.AddressBookEntities dbcontext = null;

        // 按名称填充我们的 bindingSource 的行
        private void RefreshContacts()
        {
            // 释放旧 DbContext，如果有
            if (dbContext != null)
            {
                dbContext.Dispose();
            }

            // 创建新的 DbContext以便根据编辑重新排序记录
            dbContext = new AddressExample.AddressBookEntities();

            // 使用 LINQ 排序 Addresses 表的内容
            dbContext.Addresses
.OrderBy(entry => entry.LastName).ThenBy(entry => entry.FirstName).Load();

            // 为 addressBindingSource 指定 DataSource
            addressBindingSource.DataSource = dbcontext.Addresses.Local;
            addressBindingSource.MoveFirst(); // 转到第一个结果
            TextBox.Clear(); // 清除 TextBox
        }
    }
}
```

图. 22.41 | 创建 BooksEntities 并定义供其他方法使用的 RefreshContacts 方法。

Contacts_Load 方法
Contacts_Load 方法（图 22.42）调用 RefreshContacts（第 50 行），以便在应用程序启动时显示第一条记录。与一样，你通过双击 Form 的标题栏来创建 Load 事件程序。

