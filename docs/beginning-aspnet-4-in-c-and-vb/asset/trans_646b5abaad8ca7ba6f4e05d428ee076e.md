
```
writer.WriteStartElement("Red");
writer.WriteValue(BackColor.R);
writer.WriteEndElement();

writer.WriteStartElement("Green");
writer.WriteValue(BackColor.G);
writer.WriteEndElement();

writer.WriteStartElement("Blue");
writer.WriteValue(BackColor.B);
writer.WriteEndElement();

writer.WriteStartElement("Width");
writer.WriteValue(Width);
writer.WriteEndElement();

writer.WriteStartElement("Height");
writer.WriteValue(Height);
writer.WriteEndElement();

writer.WriteStartElement("X");
writer.WriteValue(DesktopLocation.X);
writer.WriteEndElement();

writer.WriteStartElement("Y");
writer.WriteValue(DesktopLocation.Y);
writer.WriteEndElement();

writer.WriteStartElement("WindowState");
writer.WriteValue(WindowState.ToString());
writer.WriteEndElement();

writer.WriteEndElement();

writer.Flush();
writer.Close();

storStream.Close();
storFile.Close();
}
```

与使用注册表时相比，这段代码稍多一些，主要是由于构建放置在隔离存储中的 XML 文档所需的代码。下面展示了此代码中发生的第一件重要事情：

```
IsolatedStorageFile storFile = IsolatedStorageFile.GetUserStoreForDomain();
IsolatedStorageFileStream storStream = new
    IsolatedStorageFileStream("SelfPlacingWindow.xml",
    FileMode.Create, FileAccess.Write);
```

在这里，使用用户、程序集和域类型的访问创建了一个 IsolatedStorageFile 实例。使用 IsolatedStorageFileStream 对象创建了一个流，该流创建了虚拟的 SelfPlacingWindow.xml 文件。

从那里开始，创建了一个 XmlTextWriter 对象来构建 XML 文档，并将 XML 内容写入 IsolatedStorageFileStream 对象实例：

```
System.Xml.XmlTextWriter writer = new
    System.Xml.XmlTextWriter(storStream, Encoding.UTF8);
```

创建 XmlTextWriter 对象后，所有值都会逐节点写入 XML 文档。当所有内容都写入 XML 文档后，一切都会关闭并存储在隔离存储中。

从存储中读取是通过 ReadSettings() 方法完成的。该方法在以下代码示例中给出：

```
bool ReadSettings()
{
    IsolatedStorageFile storFile = IsolatedStorageFile.GetUserStoreForDomain();
    string[] userFiles = storFile.GetFileNames("SelfPlacingWindow.xml");

    foreach (string userFile in userFiles)
    {
        if(userFile == "SelfPlacingWindow.xml")
        {
            listBoxMessages.Items.Add("Successfully opened file " +
                userFile.ToString());

            StreamReader storStream =
                new StreamReader(new IsolatedStorageFileStream("SelfPlacingWindow.xml",
                FileMode.Open, storFile));
            System.Xml.XmlTextReader reader = new
                System.Xml.XmlTextReader(storStream);

            int redComponent = 0;
            int greenComponent = 0;
            int blueComponent = 0;

            int X = 0;
            int Y = 0;

            while (reader.Read())
            {
                switch (reader.Name)
                {
                    case "Red":
                        redComponent = int.Parse(reader.ReadString());
                        break;
                    case "Green":
                        greenComponent = int.Parse(reader.ReadString());
                        break;
                    case "Blue":
                        blueComponent = int.Parse(reader.ReadString());
                        break;
                    case "X":
                        X = int.Parse(reader.ReadString());
                        break;
                    case "Y":
                        Y = int.Parse(reader.ReadString());
                        break;
                    case "Width":
                        this.Width = int.Parse(reader.ReadString());
                        break;
                    case "Height":
                        this.Height = int.Parse(reader.ReadString());
                        break;
                    case "WindowState":
                        this.WindowState = (FormWindowState)FormWindowState.Parse
                            (WindowState.GetType(), reader.ReadString());
                        break;
                    default:
                        break;
                }
            }
        }
    }
}
```

```
this.BackColor =
    Color.FromArgb(redComponent, greenComponent, blueComponent);
this.DesktopLocation = new Point(X, Y);

listBoxMessages.Items.Add("Background color: " + BackColor.Name);
listBoxMessages.Items.Add("Desktop location: " + 
    DesktopLocation.ToString());
listBoxMessages.Items.Add("Size: " + new Size(Width, Height).ToString());
listBoxMessages.Items.Add("Window State: " + WindowState.ToString());

storStream.Close();
storFile.Close();
}
}
return true;
```

使用 GetFileNames() 方法，将 SelfPlacingWindow.xml 文档从隔离存储中取出，然后放入流中并使用 XmlTextReader 对象进行解析：

```
IsolatedStorageFile storFile = IsolatedStorageFile.GetUserStoreForDomain();
string[] userFiles = storFile.GetFileNames("SelfPlacingWindow.xml");

foreach (string userFile in userFiles)
{
    if(userFile == "SelfPlacingWindow.xml")
    {
        listBoxMessages.Items.Add("Successfully opened file " + 
            userFile.ToString());

        StreamReader storStream =
            new StreamReader(new IsolatedStorageFileStream("SelfPlacingWindow.xml",
            FileMode.Open, storFile));
```

在 XML 文档包含在 IsolatedStorageFileStream 对象中后，它会使用 XmlTextReader 对象进行解析：

```
System.Xml.XmlTextReader reader = new
    System.Xml.XmlTextReader(storStream);
```

之后，它通过 XmlTextReader 从流中提取。然后元素值被推回应用程序。你会发现——正如在 SelfPlacingWindow 示例中使用注册表记录和检索应用程序状态值所实现的那样——使用隔离存储与使用注册表一样有效。应用程序记住颜色、大小和位置的方式与之前一样。

## 摘要

在本章中，你研究了如何使用 .NET 基础类从 C# 代码访问文件系统和注册表。你已经看到，在这两种情况下，基础类都公开了简单但功能强大的对象模型，使得在这些领域执行几乎任何操作都变得非常简单。对于文件系统，这些操作包括复制文件；移动、创建和删除文件和文件夹；以及读写二进制和文本文件。对于注册表，这些操作是创建、修改或读取键。

本章还回顾了隔离存储以及如何从应用程序中使用它来存储应用程序状态。

本章假设你是从具有足够访问权限来执行代码所需任何操作的账户运行代码的。显然，安全问题很重要，它将在第 21 章中讨论。

下表列出了 System.Data.Common 命名空间中找到的类。

| 类 | 描述 |
|---|---|
| DataColumnMapping | 将数据库中列的名称映射到 DataTable 内的列名称。 |
| DataTableMapping | 将数据库中的表名映射到 DataSet 内的 DataTable。 |

## 数据库特定类

除了上一节介绍的共享类之外，ADO.NET 还包含许多数据库特定的类。这些类实现了 System.Data 命名空间中定义的一组标准接口，从而在必要时可以以通用方式使用这些类。例如，SqlConnection 和 OleDbConnection 类都派生自 DbConnection 类，后者实现了 IDbConnection 接口。下表列出了数据库特定的类。

| 类 | 描述 |
|---|---|
| SqlCommand, OleDbCommand, and ODBCCommand | 用作 SQL 语句或存储过程调用的包装器。本章后面将展示 SqlCommand 类的示例。 |
| SqlCommandBuilder, OleDbCommandBuilder, and ODBCCommandBuilder | 用于从 SELECT 语句生成 SQL 命令（如 INSERT、UPDATE 和 DELETE 语句）。 |
| SqlConnection, OleDbConnection, and ODBCConnection | 用于连接到数据库，与 ADO 连接类似。本章后面将展示示例。 |
| SqlDataAdapter, OleDbDataAdapter, and ODBCDataAdapter | 用于保存选择、插入、更新和删除命令，然后用于填充 DataSet 并更新数据库。本章介绍了 SqlDataAdapter 的示例。 |
| SqlDataReader, OleDbDataReader, and ODBCDataReader | 用作只向前、连接的数据读取器。本章展示了一些 SqlDataReader 的示例。 |
| SqlParameter, OleDbParameter, and ODBCParameter | 用于定义存储过程的参数。本章展示了如何使用 SqlParameter 类的示例。 |
| SqlTransaction, OleDbTransaction, and ODBCTransaction | 用于数据库事务，以对象形式封装。 |

ADO.NET 类最重要的特性是它们设计为以断开连接的方式工作，这在当今高度以 Web 为中心的世界中非常重要。现在常见的实践是构建一个服务（如在线书店），连接到服务器，检索一些数据，然后在客户端处理这些数据，然后重新连接并将数据传回进行处理。ADO.NET 的断开连接特性使这种行为成为可能。

经典的 ADO 2.1 引入了断开连接的记录集，允许从数据库检索数据，传递给客户端进行处理，然后重新附加到服务器。由于断开连接的行为不是原始设计的一部分，因此过去使用起来很麻烦。ADO.NET 类则不同——除了一个情况（[provider]DataReader）之外，它们都设计为脱离数据库离线使用。
