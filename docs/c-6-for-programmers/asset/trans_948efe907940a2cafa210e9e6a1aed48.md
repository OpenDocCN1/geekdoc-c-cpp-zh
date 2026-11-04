
-   获取所有作者及其所著书籍ISBN的列表，按姓氏排序，然后按名字排序（图20.27）。
-   获取所有作者及其所著书籍书名的列表，按姓氏排序，然后按名字排序；对于每位作者，将其书名按字母顺序排序（图20.28）。
-   获取按作者分组的所有书籍书名列表，作者按姓氏排序，然后按名字排序；对于给定作者，将书名按字母顺序排序（图20.29）。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_691_0.png)

**图20.27** | 使用LINQ连接表的应用，显示作者列表及其所著书籍的ISBN。作者按姓氏排序，然后按名字排序。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_691_1.png)

**图20.28** | 使用LINQ连接表的应用，显示作者列表及其所著书籍的书名。作者按姓氏排序，然后按名字排序，给定作者的书名按字母顺序排序。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_692_0.png)

**图20.29** | 使用LINQ连接表的应用，显示按作者分组的书名列表。作者按姓氏排序，然后按名字排序，给定作者的书名按字母顺序排序。

## “使用LINQ连接表”应用的GUI

对于此示例（图20.30–图20.33），请执行20.5.2节中的步骤，在之前示例所在的同一解决方案中创建一个名为JoinQueries的新Windows Forms应用程序项目。将Form1.cs源文件重命名为JoiningTableData.cs。将窗体的Text属性设置为“Joining Tables with LINQ”。务必添加对Books-Examples和EntityFramework库的引用，将连接字符串添加到项目的App.Config文件中，并将JoinQueries项目设置为启动项目。我们为outputTextBox设置了以下属性：

-   **Font属性：** 设置为Lucida Console，以便以等宽字体显示输出。
-   **Multiline属性：** 设置为True，以便可以显示多行文本。
-   **Anchor属性：** 设置为Top、Bottom、Left、Right，以便可以调整窗口大小，outputTextBox也会随之调整大小。
-   **Scrollbars属性：** 设置为Vertical，以便可以滚动查看输出。

## 创建DbContext

代码使用实体数据模型类将Books数据库中各表中的数据组合起来，并以三种不同方式显示作者与书籍之间的关系。为了便于展示，我们将类JoiningTableData的代码分成了几个图（图20.30–20.33）。和之前的示例一样，DbContext对象（图20.30，第19行）允许程序与数据库交互。

数据库中相应作者的ISBN。两个from子句的组合结果是一个集合，包含所有作者及其所著书籍的ISBN。这两个from子句将两个范围变量引入到此查询的作用域中——其他子句可以访问这两个范围变量，以组合多个表中的数据。第25行按作者的LastName（姓氏）排序结果，然后按FirstName（名字）排序。第26行创建了一个匿名类型，包含来自Authors表的作者的FirstName和LastName，以及来自Titles表的该作者的一本书的ISBN。

## 匿名类型

回顾第9.3.5节，LINQ查询的select子句可以创建一个匿名类型，其属性在初始化列表中指定——在本例中为FirstName、LastName和ISBN（第26行）。请注意，匿名类型的所有属性都是公共且只读的。由于该类型没有名称，因此必须使用隐式类型局部变量来存储对匿名类型对象的引用（例如，第31行）。此外，除了匿名类型中的ToString方法之外，编译器还提供了一个Equals方法，该方法会比较调用方法的匿名对象的属性和作为参数接收的匿名对象的属性。

## 将作者姓名与其所著书籍的书名组合

第二个查询（图20.32，第38–42行）给出类似的输出，但使用外键关系来获取作者所写的每本书的书名。

```csharp
// get authors and titles of each book they co-authored
var authorsAndTitles =
    from book in dbcontext.Titles
    from author in book.Authors
    orderby author.LastName, author.FirstName, book.Title1
    select new {author.FirstName, author.LastName, book.Title1};

outputTextBox.AppendText("\r\n\r\nAuthors and titles:");

// display authors and titles in tabular format
foreach (var element in authorsAndTitles)
{
    outputTextBox.AppendText($"{element.FirstName,-10} " +
        $"{element.LastName,-10} {element.Title1}");
}
```

**图20.32** | 获取作者及其所著书籍书名的列表。

第一个from子句（第39行）从Titles表中获取每本书。第二个from子句（第40行）使用Title类中生成的Authors属性来仅获取当前书籍的作者。实体数据模型使用存储在数据库AuthorISBN表中的外键信息来获取相应的作者。作者对象使我们能够访问当前书籍作者的姓名。select子句（第42行）使用author和book范围变量从Authors表获取每位作者的FirstName和LastName，并从Titles表获取该作者的一本书的书名。

## 按作者整理书籍书名

大多数查询返回的结果中的数据以行和列的关系型表格形式排列。最后一个查询（图20.33，第55–62行）返回分层结果。结果中的每个元素包含一位作者的姓名以及该作者所著书籍的书名列表。LINQ查询通过使用select子句中的嵌套查询来实现这一点。外层查询遍历数据库中的作者。内层查询接收特定作者，并检索该作者写的所有书名。select子句（第58–62行）创建一个具有两个属性的匿名类型：

-   属性Name（第58行）初始化为一个字符串，该字符串用空格分隔作者的姓和名。
-   属性Titles（第59–62行）初始化为嵌套查询的结果，该结果返回当前作者所写的每本书的书名。

在本例中，我们为新匿名类型中的每个属性提供了名称。创建匿名类型时，可以使用格式“name = value”为每个属性指定名称。

```csharp
53  // get authors and titles of each book
54  // they co-authored; group by author
55  var titlesByAuthor =
56      from author in dbcontext.Authors
57      orderby author.LastName, author.FirstName
58      select new { Name = author.FirstName + " " + author.LastName,
59                  Titles =
60                      from book in author.Titles
61                      orderby book.Title
62                      select book.Title};

64  outputTextBox.AppendText("\r\n\r\nTitles grouped by author:");

66  // display titles written by each author, grouped by author
67  foreach (var author in titlesByAuthor)
68  {
69      // display author's name
70      outputTextBox.AppendText($"\r\n\t{author.Name}:");

72      // display titles written by that author
73      foreach (var title in author.Titles)
74      {
75          outputTextBox.AppendText($"\r\n\t\t{title}");
76      }
77  }
78 }
79 }
80 }
```

**图20.33** | 获取按作者分组的书名列表。

嵌套查询中的范围变量book使用Titles属性遍历当前作者的书。给定书籍的Title1属性返回数据库中Titles表该行的Title列。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_697_0.png)

**图20.35** | Master/Detail应用的完成设计。

## 步骤2：为Authors表添加数据源

按照20.5.3节中的步骤为Authors表添加数据源。尽管你将显示每位作者的Titles表中的记录，但不需要为该表添加数据源。标题信息将从Author实体数据模型类中的Titles导航属性获取。

## 步骤3：创建GUI元素

接下来，你将使用**设计**视图，通过从**数据源**窗口拖放项到窗体上来创建GUI组件。在之前的小节中，你从**数据源**窗口拖动一个对象到窗体上以创建DataGridView。IDE允许你指定从**数据源**窗口拖放对象到窗体上时将创建的控件类型。操作步骤如下：

-   1. 切换到Details类的**设计**视图。
-   2. 单击**数据源**窗口中的**Author**节点——它应变为一个下拉列表。通过单击向下箭头打开下拉列表，并选择Details选项——这表示我们希望生成代表Authors表每一列的Label–TextBox对。
-   3. 将**Author**节点从**数据源**窗口拖到**设计**视图中的窗体上。这将创建authorBindingSource、authorBindingNavigator以及代表表中每一列的Label–TextBox对。初始时，控件显示如图20.36所示。我们按图20.35所示重新排列了控件。
-   4. 默认情况下，**Titles**导航属性在实体数据模型类中实现为HashSet<Titles>。要正确地将数据绑定到GUI控件上，必须将其改为ObservableCollection<Title>。为此，展开

