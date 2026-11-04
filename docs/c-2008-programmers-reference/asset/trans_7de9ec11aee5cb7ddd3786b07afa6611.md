
```csharp
"poze","prescription","privacy assured","product for less",
"products for less","protect yourself","psychic"
};
```

```csharp
//---for generic version of the class---
public IEnumerator<string> GetEnumerator()
{
}

//---for non-generic version of the class---
System.Collections.IEnumerator System.Collections.IEnumerable.GetEnumerator()
{
}
```

注意，对于 IEnumerable 接口的泛型版本，你需要实现两个版本的 GetEnumerator() 方法——一个用于类的泛型版本，一个用于非泛型版本。

```csharp
public class SpamPhraseList : IEnumerable<string>
{
    private class SpamPhraseListEnum : IEnumerator<string>
    {
        private int index = -1;
        private SpamPhraseList spamlist;

        public SpamPhraseListEnum(SpamPhraseList sl)
        {
            this.spamlist = sl;
        }

        //---for generic version of the class---
        string IEnumerator<string>.Current
        {
            get
            {
                return spamlist.Phrases[index];
            }
        }

        //---for non-generic version of the class---
        object System.Collections.IEnumerator.Current
        {
            get
            {
                return spamlist.Phrases[index];
            }
        }
        bool System.Collections.IEnumerator.MoveNext()
        {
            index++;
            return index < spamlist.Phrases.Length;
        }
        void System.Collections.IEnumerator.Reset()
        {
            index = -1;
        }
        void IDisposable.Dispose() { }
    }
```

```csharp
protected string[] Phrases =
    new string[]{
        "pain relief","paxil","pharmacy","phendimetrazine",
        "phentermine","phentermine","pheramones","pherimones",
        "photos of singles","platinum-celebs","poker-chip",
        "poze","prescription","privacy assured","product for less",
        "products for less","protect yourself","psychic"
    };
```

```csharp
public IEnumerator<string> GetEnumerator()
{
    return new SpamPhraseListEnum(this);
}

//---for non-generic version of the class---
System.Collections.IEnumerator System.Collections.IEnumerable.GetEnumerator()
{
    return new SpamPhraseListEnum(this);
}
```

在此示例中，SpamPhraseListEnum 类实现了 IEnumerator<string> 接口并提供了 Current 属性以及 MoveNext() 和 Reset() 方法的实现。

要打印出 SpamPhraseList 对象中包含的所有元素，你可以使用上一节中使用的相同语句：

```csharp
SpamPhraseList list = new SpamPhraseList();
foreach (string s in list) //---error---
Console.WriteLine(s);
```

在幕后，编译器为 foreach 语句生成的代码如下：

```csharp
SpamPhraseList list = new SpamPhraseList();
IEnumerator<string> s = list.GetEnumerator();
while (s.MoveNext())
    Console.WriteLine((string)s.Current);
```

## 使用 IComparer<T> 和 IComparable<T> 实现比较

在对象集合上你经常需要执行的一项任务是排序。你需要知道对象的顺序，以便相应地对它们进行排序。能够比较的对象实现了 IComparable 接口（该接口的泛型等价物是 IComparable<T>）。考虑以下示例：

```csharp
string[] Names = new string[] {
    "John", "Howard",
    "Margaret", "Brian" };
foreach (string n in Names)
    Console.WriteLine(n);
```

这里，Names 是一个包含四个字符串的字符串数组。此代码打印出以下内容：

```text
John
Howard
Margaret
Brian
```

你可以使用抽象静态类 Array 中的 Sort() 方法对 Names 数组进行排序，如下所示：

```csharp
Array.Sort(Names);
foreach (string n in Names)
    Console.WriteLine(n);
```

现在输出是已排序的名称数组：

```text
Brian
Howard
John
Margaret
```

在这种情况下，字符串数组可以排序的原因是 String 类型本身实现了 IComparable 接口，因此 Sort() 方法知道如何正确地对数组进行排序。同样适用于 int、single、float 等其他类型。

如果你有自己的类型并且希望它可排序怎么办？假设你有如下定义的 Employee 类：

```csharp
public class Employee
{
    public string FirstName
    { get; set; }

    public string LastName
    { get; set; }

    public int Salary
    { get; set; }

    public override string ToString()
    {
        return FirstName + ", " + LastName +
            " $" + Salary;
    }
}
```

你可以像这样将多个 Employee 对象添加到 List 对象中：

```csharp
List<Employee> employees = new List<Employee>();
employees.Add(new Employee()
{
    FirstName = "John",
    LastName = "Smith",
    Salary = 4000
});
employees.Add(new Employee()
{
    FirstName = "Howard",
    LastName = "Mark",
    Salary = 1500
});
employees.Add(new Employee()
{
    FirstName = "Margaret",
    LastName = "Anderson",
    Salary = 3000
});
employees.Add(new Employee()
{
    FirstName = "Brian",
    LastName = "Will",
    Salary = 3000
});
```

要对包含你的 Employee 对象的 List 对象进行排序，可以使用以下语句：

```csharp
employees.Sort();
```

然而，此语句会导致运行时错误（参见图 13-4），因为 Sort() 方法不知道 Employee 对象应如何排序。

![](img/a977a875c7c627b45d939729705a252e_438_0.png)

图 13-4

为了解决这个问题，Employee 类需要实现 IComparable<T> 接口，然后实现 CompareTo() 方法：

```csharp
public class Employee : IComparable<Employee>
{
    public string FirstName
    { get; set; }

    public string LastName
    { get; set; }

    public int Salary
    { get; set; }

    public override string ToString()
    {
        return FirstName + ", " + LastName +
            " $" + Salary;
    }

    public int CompareTo(Employee emp)
    {
        return this.FirstName.CompareTo(emp.FirstName);
    }
}
```

CompareTo() 方法接受一个 Employee 参数，你将 Employee 类的 FirstName 属性的当前实例（由 this 表示）与参数的 FirstName 属性进行比较。这里，你使用 String 类的 CompareTo() 方法（FirstName 为 String 类型）来执行比较。

CompareTo(obj) 方法的返回值具有以下表中所示的可能值。

| 值 | 含义 |
|---|---|
| 小于零 | 当前实例小于 obj。 |
| 零 | 当前实例等于 obj。 |
| 大于零 | 当前实例大于 obj。 |

现在，当你对包含 Employee 对象的 List 对象进行排序时，Employee 对象将按名字排序：

```csharp
employees.Sort();
foreach (Employee emp in employees)
    Console.WriteLine(emp.ToString());
```

这些语句产生以下输出：

```text
Brian, Will $3000
Howard, Mark $1500
John, Smith $4000
Margaret, Anderson $3000
```

要使用 LastName 而不是 FirstName 对 Employee 对象进行排序，只需按如下方式更改 CompareTo() 方法：

```csharp
public int CompareTo(Employee emp)
{
    return this.LastName.CompareTo(emp.LastName);
}
```

输出变为：

```text
Margaret, Anderson $3000
Howard, Mark $1500
John, Smith $4000
Brian, Will $3000
```

同样，要按薪水排序，你比较 Salary 属性：

```csharp
public int CompareTo(Employee emp)
{
    return this.Salary.CompareTo(emp.Salary);
}
```

输出现在为：

```text
Howard, Mark $1500
Margaret, Anderson $3000
Brian, Will $3000
John, Smith $4000
```

而不是使用你要比较的类型中的 CompareTo() 方法，你可以手动执行比较，如下所示：

```csharp
public int CompareTo(Employee emp)
{
    if (this.Salary < emp.Salary)
        return -1;
    else if (this.Salary == emp.Salary)
        return 0;
    else
        return 1;
}
```

Employee 对象的排序方式由 CompareTo() 方法的实现决定。如果 CompareTo() 使用 FirstName 属性进行比较，则排序基于 FirstName 属性。为了让用户可以选择使用哪个字段对对象进行排序，你可以使用 IComparer<T> 接口。

为此，首先在 Employee 类内部声明一个私有类并将其命名为 SalaryComparer。

```csharp
public class Employee : IComparable<Employee>
{
    private class SalaryComparer : IComparer<Employee>
    {
        public int Compare(Employee e1, Employee e2)
        {
            if (e1.Salary < e2.Salary)
                return -1;
            else if (e1.Salary == e2.Salary)
                return 0;
            else
                return 1;
        }
    }

    public string FirstName
    { get; set; }

    public string LastName
    { get; set; }

    public int Salary
```
