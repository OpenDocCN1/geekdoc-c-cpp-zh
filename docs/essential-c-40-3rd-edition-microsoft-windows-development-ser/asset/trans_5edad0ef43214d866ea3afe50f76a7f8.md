
是哪个类实现了这些方法。结果是多态，因为每个压缩类都有相同的方法签名，但对该签名有各自的实现。

接口的命名约定是使用 Pascal 大小写，并加上 I 前缀。清单 7.1 中所示的 IFileCompression 接口就是这样一个名称和接口定义的示例。

### 清单 7.1：定义接口

```
interface IFileCompression
{
    void Compress(string targetFileName, string[] filelist);
    void Uncompress(
        string compressedFileName, string expandDirectoryName);
}
```

IFileCompression 定义了类用于与其他压缩相关类协作的方法。定义接口的强大之处在于能够在不修改调用代码的情况下在不同实现之间切换，前提是每个压缩类都实现 IFileCompression 接口。

接口的一个关键特征是它没有实现也没有数据。方法声明在标题后使用单个分号代替花括号。字段（数据）不能出现在接口上。当接口要求派生类拥有某些数据时，它使用属性而不是字段。由于属性作为接口声明的一部分不包含任何实现，因此它不引用支持字段。

鉴于接口的目的是在多个类之间定义契约，定义私有或受保护成员会使其他类无法访问它们，从而违背了接口的目的。因此，C# 不允许在接口成员上使用访问修饰符，而是自动将它们定义为 public。

## 通过接口实现多态

考虑另一个示例（请参见清单 7.2）：IListable 定义了类需要支持的成员，以便 ConsoleListControl 类可以显示它。因此，任何实现 IListable 的类都将具有使用 ConsoleListControl 显示自身的能力。IListable 接口要求一个只读属性 ColumnValues。

### 清单 7.2：实现和使用接口

```
interface IListable
{
    // Return the value of each column in the row.
    string[] ColumnValues
    {
        get;
    }
}
```

```
public abstract class PdaItem
{
    public PdaItem(string name)
    {
        Name = name;
    }

    public virtual string Name { get; set; }
}
```

```
class Contact : PdaItem, IListable
{
    public Contact(string firstName, string lastName,
        string address, string phone) : base(null)
    {
        FirstName = firstName;
        LastName = lastName;
        Address = address;
        Phone = phone;
    }

    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string Address { get; set; }
    public string Phone { get; set; }

    public string[] ColumnValues
    {
        get
        {
            return new string[]
            {
                FirstName,
                LastName,
                Phone,
                Address
            };
        }
    }

    public static string[] Headers
    {
        get
        {
            return new string[] {
                "First Name", "Last Name",
                "Phone",
                "Address"
            };
        }
    }
    // ...
}
```

```
class Publication : IListable
{
    public Publication(string title, string author, int year)
    {
        Title = title;
        Author = author;
        Year = year;
    }

    public string Title { get; set; }
    public string Author { get; set; }
    public int Year { get; set; }

    public string[] ColumnValues
    {
        get
        {
            return new string[]
            {
                Title,
                Author,
                Year.ToString()
            };
        }
    }

    public static string[] Headers
    {
        get
        {
            return new string[] {
                "Title",
                "Author",
                "Year"
            };
        }
    }
    // ...
}
```

```
class Program
{
    public static void Main()
    {
        Contact[] contacts = new Contact[6];
        contacts[0] = new Contact(
            "Dick", "Traci",
            "123 Main St., Spokane, WA 99037",
            "123-123-1234");
        contacts[1] = new Contact(
            "Andrew", "Littman",
            "1417 Palmy St., Dallas, TX 55555",
            "555-123-4567");
        contacts[2] = new Contact(
            "Mary", "Hartfelt",
            "1528 Thunder Way, Elizabethton, PA 44444",
            "444-123-4567");
        contacts[3] = new Contact(
            "John", "Lindhurst",
            "1 Aerial Way Dr., Monterey, NH 88888",
            "222-987-6543");
        contacts[4] = new Contact(
            "Pat", "Wilson",
            "565 Irving Dr., Parksdale, FL 22222",
            "123-456-7890");
        contacts[5] = new Contact(
            "Jane", "Doe",
            "123 Main St., Aurora, IL 66666",
            "333-345-0789");
        // Classes are cast implicitly to
        // their supported interfaces
        ConsoleListControl.List(Contact.Headers, contacts);
        Console.WriteLine();
        Publication[] publications = new Publication[3] {
            new Publication("Celebration of Discipline",
                "Richard Foster", 1978),
            new Publication("Orthodoxy",
                "G.K. Chesterton", 1908),
            new Publication(
                "The Hitchhiker's Guide to the Galaxy",
                "Douglas Adams", 1979
            );
        ConsoleListControl.List(
            Publication.Headers, publications);
    }
}
```

```
class ConsoleListControl
{
    public static void List(string[] headers, IList[] items)
    {
        int[] columnWidths = DisplayHeaders(headers);
        for (int count = 0; count < items.Length; count++)
        {
            string[] values = items[count].ColumnValues;
            DisplayItemRow(columnWidths, values);
        }
    }

    /// <summary>Displays the column headers</summary>
    /// <returns>Returns an array of column widths</returns>
    private static int[] DisplayHeaders(string[] headers)
    {
        // ...
    }

    private static void DisplayItemRow(
        int[] columnWidths, string[] values)
    {
        // ...
    }
}
```

清单 7.2 的结果显示在输出 7.1 中。

### 输出 7.1：

| 名 | 姓 | 电话 | 地址 |
| :--- | :--- | :--- | :--- |
| Dick | Traci | 123-123-1234 | 123 Main St., Spokane, WA 99037 |
| Andrew | Littman | 555-123-4567 | 1417 Palmy St., Dallas, TX 55555 |
| Mary | Hartfelt | 444-123-4567 | 1528 Thunder Way, Elizabethton, PA 44444 |
| John | Lindhurst | 222-987-6543 | 1 Aerial Way Dr., Monterey, NH 88888 |
| Pat | Wilson | 123-456-7890 | 565 Irving Dr., Parksdale, FL 22222 |
| Jane | Doe | 333-345-0789 | 123 Main St., Aurora, IL 66666 |

| 标题 | 作者 | 年份 |
| :--- | :--- | :--- |
| Celebration of Discipline | Richard Foster | 1978 |
| Orthodoxy | G.K. Chesterton | 1908 |
| The Hitchhiker's Guide to the Galaxy | Douglas Adams | 1979 |

在清单 7.2 中，ConsoleListControl 可以显示看似无关的类（Contact 和 Publication）。可显示的类仅由其是否实现所需接口来定义。因此，ConsoleListControl.List() 方法依赖多态来适当显示传递给它的任何一组对象。每个类都有 ColumnValues 的自己的实现，将类转换为 IListable 仍然允许调用该特定类的实现。

## 接口实现

声明类实现接口与从基类派生类似，因为已实现的接口出现在与基类一起的逗号分隔列表中（接口之间的顺序无关紧要）。唯一的区别是类可以实现多个接口。示例出现在清单 7.3 中。

### 清单 7.3：实现接口

```
public class Contact : PdaItem, IListable, IComparable
{
  // ...
}
#region IComparable Members
/// <summary>
/// </summary>
/// <param name="obj"></param>
/// <returns>
/// Less than zero:   This instance is less than obj.
/// Zero              This instance is equal to obj.
/// Greater than zero This instance is greater than obj.
/// </returns>
```

```
public int CompareTo(object obj)
{
    int result;
    Contact contact = obj as Contact;
    if (obj == null)
    {
        // This instance is greater than obj.
        result = 1;
    }
    else if (!(obj is Contact))
    {
        throw new ArgumentException("obj is not a Contact");
    }
    else if (Contact.ReferenceEquals(this, obj))
    {
        result = 0;
    }
    else
    {
        result = LastName.CompareTo(contact.LastName);
        if (result == 0)
            result = FirstName.CompareTo(contact.FirstName);
    }
    return result;
}
#endregion
```

```
#region IListable Members
string[] IListable.ColumnValues
{
    get
    {
        return new string[]
        {
            FirstName,
            LastName,
            Phone,
            Address
        };
    }
}
#endregion
```

一旦类声明实现接口，就必须实现接口的所有成员。成员实现可能会抛出一个
