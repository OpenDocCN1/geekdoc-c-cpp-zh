

ConsoleListControl 使其自身显示。IListable 接口要求一个只读属性 ColumnValues。

## LISTING 7.2: Implementing and Using Interfaces

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
    public Contact(string firstName, string lastName, string address, string phone) : base(null)
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
                "Address" };
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
                "Year" };
        }
    }
}

// ...
}

class Program
{
    public static void Main()
    {
        Contact[] contacts = new Contact[6];
        contacts[0] = new Contact(
            "Dick", "Traci",
            "123 Main St., Spokane, WA  99037",
            "123-123-1234");
        contacts[1] = new Contact(
            "Andrew", "Littman",
            "1417 Palmary St., Dallas, TX 55555",
            "555-123-4567");
        contacts[2] = new Contact(
            "Mary", "Hartfelt",
            "1520 Thunder Way, Elizabethton, PA 44444",
            "444-123-4567");
        contacts[3] = new Contact(
            "John", "Lindherst",
            "1 Aerial Way Dr., Monterey, NH 88888",
            "222-987-6543");
        contacts[4] = new Contact(
            "Pat", "Wilson",
            "565 Irving Dr., Parksdale, FL 22222",
            "123-456-7890");
        contacts[5] = new Contact(
            "Jane", "Doe",
            "123 Main St., Aurora, IL 66666",
            "333-345-6789");

        // Classes are cast implicitly to
        // their supported interfaces.
        ConsoleListControl.List(Contact.Headers, contacts);

        Console.WriteLine();

        Publication[] publications = new Publication[3] {
            new Publication("Celebration of Discipline",
                "Richard Foster", 1978),
            new Publication("Orthodoxy",
                "G.K. Chesterton", 1908),
            new Publication(
                "The Hitchhiker's Guide to the Galaxy",
                "Douglas Adams", 1979)
        };
        ConsoleListControl.List(
            Publication.Headers, publications);
    }
}

class ConsoleListControl
{
    public static void List(string[] headers, IListable[] items)
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

Listing 7.2 的结果显示在 Output 7.1 中。

## OUTPUT 7.1

```
First Name  Last Name  Phone        Address
Dick        Traci      123-123-1234 123 Main St., Spokane, WA 99037
Andrew      Littman    555-123-4567 1427 Palmary St., Dallas, TX 55555
Mary        Hartfelt   444-123-4567 1520 Thunder Way, Elizabethton, PA 44444
John        Lindherst  222-987-6543 1 Aerial Way Dr., Monterey, NH 88888
Pat         Wilson     123-456-7890 565 Irving Dr., Parksdale, FL 22222
Jane        Doe        333-345-6789 123 Main St., Aurora, IL 66666

Title                          Author            Year
Celebration of Discipline      Richard Foster     1978
Orthodoxy                      G.K. Chesterton    1908
The Hitchhiker's Guide to the Galaxy Douglas Adams   1979
```

在 Listing 7.2 中，ConsoleListControl 可以显示看似不相关的类（Contact 和 Publication）。只要类实现了所需的接口，任何类都可以被显示。因此，Console ListControl.List() 方法依赖于多态性来适当地显示其接收到的对象集合。每个类都有自己对 ColumnValues 的实现，并且将类转换为 IListable 仍然允许调用该类的特定实现。

## Interface Implementation

声明类实现接口与从基类派生类似：实现的接口与基类一起出现在以逗号分隔的列表中。基类说明符（如果有）必须排在前面，但其余顺序并不重要。类可以实现多个接口，但只能直接派生自一个基类。示例见 Listing 7.3。

## LISTING 7.3: Implementing an Interface

```
public class Contact : PdaItem, IListable, IComparable
{
    // ...

    #region IComparable Members
    /// <summary>
    ///
    /// </summary>
    /// <param name="obj"></param>
    /// <returns>
    /// Less than zero:     This instance is less than obj.
    /// Zero                This instance is equal to obj.
    /// Greater than zero   This instance is greater than obj.
    /// </returns>
    public int CompareTo(object obj)
    {
        int result;
        Contact contact = obj as Contact;

        if (obj == null)
        {
            // This instance is greater than obj.
            result = 1;
        }
        else if (obj.GetType() != typeof(Contact))
        {
            // Use C# 6.0 nameof operator in message to
            // ensure consistency in the Type name.
            throw new ArgumentException(
                $"The parameter is not a of type { nameof(Contact) }",
                nameof(obj));
        }
        else if (Contact.ReferenceEquals(this, obj))
        {
            result = 0;
        }
        else
        {
            result = LastName.CompareTo(contact.LastName);
            if (result == 0)
            {
                result = FirstName.CompareTo(contact.FirstName);
            }
        }
        return result;
    }
    #endregion

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
}
```

一旦类声明实现接口，接口的所有成员都必须被实现。抽象类可以提供接口成员的抽象实现。非抽象实现可以在方法体中抛出 NotImplementedException 类型异常，但无论如何必须提供该成员的实现。

接口的一个重要特性是它们永远不能被实例化；你不能使用 new 来创建接口，因此接口没有构造函数或终结器。接口实例只能通过实例化实现该接口的类型来获得。此外，接口不能包含静态成员。接口的一个关键用途是多态性，而在没有实现类型的实例的情况下，多态性几乎没有价值。

