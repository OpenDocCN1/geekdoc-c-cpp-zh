
```
}
public string ToString(string format)
{
    return ToString(format, null);
}
public string ToString(string format, IFormatProvider formatProvider)
{
    switch (format)
    {
        case null:
        case "N":
            return ToString();
        case "F":
            return FirstName;
        case "L":
            return LastName;
        case "C":
            return Country;
        case "S":
            return Starts.ToString();
        case "W":
            return Wins.ToString();
        case "A":
            return String.Format("{0} ({1}, {2}); starts: {3}, wins: {4}",
                FirstName, LastName, Country, Starts, Wins);
        default:
            throw new FormatException(String.Format(
                "Format {0} not supported", format));
    }
}
```

代码片段 DataLib/Racer.cs

第二个实体类是 Team。该类仅包含名称和用于车队冠军的年份数组。

```
[Serializable]
public class Team
{
    public Team(string name, params int[] years)
    {
        this.Name = name;
        this.Years = years;
    }

    public string Name { get; private set; }
    public int[] Years { get; private set; }
}
```

代码片段 DataLib/Team.cs

Formula1 类在 GetChampions() 方法中返回车手列表。该列表填充了 1950 年至 2008 年的所有一级方程式冠军：

```
using System.Collections.Generic;

namespace Wrox.ProCSharp.LINQ
{
    public static class Formula1
    {
        private static List<Racer> racers;

        public static IList<Racer> GetChampions()
        {
            if (racers == null)
            {
                racers = new List<Racer>(40);
                racers.Add(new Racer("Nino", "Farina", "Italy", 33, 5,
                    new int[] { 1950 },
                    new string[] { "Alfa Romeo" }));
                racers.Add(new Racer("Alberto", "Ascari", "Italy", 32, 10,
                    new int[] { 1952, 1953 },
                    new string[] { "Ferrari" }));
                racers.Add(new Racer("Juan Manuel", "Fangio", "Argentina", 51, 24,
                    new int[] { 1951, 1954, 1955, 1956, 1957 },
                    new string[] { "Alfa Romeo", "Maserati", "Ferrari" }));
                racers.Add(new Racer("Mike", "Hawthorn", "UK", 45, 3,
                    new int[] { 1958 },
                    new string[] { "Ferrari" }));
                racers.Add(new Racer("Phil", "Hill", "USA", 48, 3,
                    new int[] { 1961 },
                    new string[] { "Ferrari" }));
                racers.Add(new Racer("John", "Surtees", "UK", 111, 6,
                    new int[] { 1964 },
                    new string[] { "Ferrari" }));
                racers.Add(new Racer("Jim", "Clark", "UK", 72, 25,
                    new int[] { 1963, 1965 },
                    new string[] { "Lotus" }));
                racers.Add(new Racer("Jack", "Brabham", "Australia", 125, 14,
                    new int[] { 1959, 1960, 1966 },
                    new string[] { "Cooper", "Brabham" }));
                racers.Add(new Racer("Denny", "Hulme", "New Zealand", 112, 8,
                    new int[] { 1967 },
                    new string[] { "Brabham" }));
                racers.Add(new Racer("Graham", "Hill", "UK", 176, 14,
                    new int[] { 1962, 1968 },
                    new string[] { "BRM", "Lotus" }));
                racers.Add(new Racer("Jochen", "Rindt", "Austria", 60, 6,
                    new int[] { 1970 },
                    new string[] { "Lotus" }));
                racers.Add(new Racer("Jackie", "Stewart", "UK", 99, 27,
                    new int[] { 1969, 1971, 1973 },
                    new string[] { "Matra", "Tyrrell" }));
                //...
                return racers;
            }
        }
    }
}
```

代码片段 DataLib/Formula1.cs

当在多个列表之间进行查询时，下面提供的 GetConstructorChampions() 方法返回所有车队冠军的列表。车队冠军自 1958 年以来就存在。

```
private static List<Team> teams;
public static IList<Team> GetConstructorChampions()
{
    if (teams == null)
    {
        teams = new List<Team>()
        {
            new Team("Vanwall", 1958),
            new Team("Cooper", 1959, 1960),
            new Team("Ferrari", 1961, 1964, 1975, 1976, 1977, 1979, 1982, 1983, 1999, 2000, 2001, 2002, 2003, 2004, 2007, 2008),
            new Team("BRM", 1962),
            new Team("Lotus", 1963, 1965, 1968, 1970, 1972, 1973, 1978),
            new Team("Brabham", 1966, 1967),
            new Team("Matra", 1969),
            new Team("Tyrrell", 1971),
            new Team("McLaren", 1974, 1984, 1985, 1988, 1989, 1990, 1991, 1998),
            new Team("Williams", 1980, 1981, 1986, 1987, 1992, 1993, 1994, 1996, 1997),
            new Team("Benetton", 1995),
            new Team("Renault", 2005, 2006 )
        };
        return teams;
    }
}
```

## LINQ 查询

使用这些准备好的列表和实体，你可以执行 LINQ 查询，例如，查询按获胜次数从高到低排序的巴西世界冠军。要实现这一点，你可以使用 List<T> 类的方法，例如 FindAll() 和 Sort() 方法。然而，使用 LINQ 一旦你习惯了，就有更简单的语法：

```
private static void LinqQuery()
{
    var query = from r in Formula1.GetChampions()
                where r.Country == "Brazil"
                orderby r.Wins descending
                select r;

    foreach (Racer r in query)
    {
        Console.WriteLine("{0:A}", r);
    }
}
```

该查询的结果显示按顺序排列的巴西世界冠军：

```
Ayrton Senna, Brazil; starts: 161, wins: 41
Nelson Piquet, Brazil; starts: 204, wins: 23
Emerson Fittipaldi, Brazil; starts: 143, wins: 14
```

语句

```
from r in Formula1.GetChampions()
where r.Country == "Brazil"
orderby r.Wins descending
select r;
```

是一个 LINQ 查询。from、where、orderby、descending 和 select 子句是此查询中的预定义关键字。

查询表达式必须以 from 子句开头，以 select 或 group 子句结尾。在两者之间，你可以 optionally 使用 where、orderby、join、let 和额外的 from 子句。

![](img/d7d2ffa0a76feaab821930e95daace93_333_0.png)

## 扩展方法

编译器会修改 LINQ 查询以调用方法而不是使用查询语法。LINQ 为 IEnumerable<T> 接口提供了各种扩展方法，因此你可以在实现该接口的任何集合上使用 LINQ 查询。

扩展方法使得可以为最初不提供该方法的类编写方法。你还可以为实现特定接口的任何类添加方法，以便多个类可以使用相同的实现。

例如，你是否希望 String 类拥有 Foo() 方法？String 类是密封的，因此无法从该类继承。你可以做一个扩展方法，如以下代码所示：

```
public static class StringExtension
{
    public static void Foo(this string s)
    {
        Console.WriteLine("Foo invoked for {0}", s);
    }
}
```

扩展方法被定义为静态方法，其中第一个参数定义了它扩展的类型，并且它在静态类中声明。Foo() 方法扩展了 string 类，如第一个参数所定义。为了区分扩展方法与普通静态方法，扩展方法还要求第一个参数使用 this 关键字。

确实，现在可以使用 Foo() 方法与 string 类型：

```
string s = "Hello";
s.Foo();
```

结果在控制台中显示 Foo invoked for Hello，因为 Hello 是传递给 Foo() 方法的字符串。

这看起来可能违反了面向对象的规则，因为为一个类型定义了新方法，而没有更改该类型或从它派生。然而事实并非如此。扩展方法无法访问其扩展类型的私有成员。调用扩展方法只是调用静态方法的一种新语法。对于 string，你可以通过以下方式调用 Foo() 方法获得相同的结果：

```
string s = "Hello";
StringExtension.Foo(s);
```

要调用静态方法，请写出类名后跟方法名。扩展方法是以不同方式调用静态方法。你不必提供静态方法定义的类的名称。相反，由于参数类型选择了静态方法。你只需要导入包含该类的命名空间，即可在 String 类的作用域中获得 Foo() 扩展方法。

定义 LINQ 扩展方法的一个类是 System.Linq 命名空间中的 Enumerable。你只需要导入该命名空间即可打开此类扩展方法的作用域。以下代码展示了 Where() 扩展方法的一个示例实现。第一个参数
