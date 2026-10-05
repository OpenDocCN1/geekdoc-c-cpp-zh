
向栈中推入元素：
9 已推入栈中
3 已推入栈中
7 已推入栈中
2 已推入栈中
栈现在包含：

```
2
7
3
9
```

从栈中弹出元素：
2 已从栈中弹出
7 已从栈中弹出
3 已从栈中弹出
9 已从栈中弹出

```csharp
using System;
using System.Collections.Generic;
...
Dictionary<string, int> ages = new Dictionary<string, int>();

// 填充 Dictionary
ages.Add("John", 57); // 使用 Add 方法
ages.Add("Diana", 57);
ages["James"] = 30; // 使用数组表示法
ages["Francesca"] = 27;

// 使用 foreach 语句迭代
// 迭代器生成一个 KeyValuePair 
Console.WriteLine("The Dictionary contains:");
foreach (KeyValuePair<string, int> element in ages)
{
    string name = element.Key;
    int age = element.Value;
    Console.WriteLine($"Name: {name}, Age: {age}");
}
```

```csharp
using System;
using System.Collections.Generic;
...
SortedList<string, int> ages = new SortedList<string, int>();

// 填充 SortedList // 使用 Add 方法
ages.Add("John", 57);
ages.Add("Diana", 57);
ages["James"] = 30; // 使用数组表示法
ages["Francesca"] = 27;

// 使用 foreach 语句迭代
// 迭代器生成一个 KeyValuePair 项
Console.WriteLine("The SortedList contains:");
foreach (KeyValuePair<string, int> element in ages)
{
    string name = element.Key;
    int age = element.Value;
    Console.WriteLine($"Name: {name}, Age: {age}");
}
```

```csharp
using System;
using System.Collections.Generic;

HashSet<string> employees = new HashSet<string>(new string[] { "Fred", "Bert", "Harry", "John" });
HashSet<string> customers = new HashSet<string>(new string[] { "John", "Sid", "Harry", "Diana" });

employees.Add("James");
customers.Add("Francesca");

Console.WriteLine("Employees:");
foreach (string name in employees)
{
    Console.WriteLine(name);
}

Console.WriteLine("");
Console.WriteLine("Customers:");
foreach (string name in customers)
{
    Console.WriteLine(name);
}

Console.WriteLine("Customers who are also employees:");
customers.IntersectWith(employees);
foreach (string name in customers)
{
    Console.WriteLine(name);
}
```

- 员工：
- Fred
- Bert
- Harry
- John
- James

- 客户：
- John
- Sid
- Harry
- Diana
- Francesca

- 也是员工的客户：
- John
- Harry

```csharp
List<int> numbers = new List<int>(){10, 9, 8, 7, 7, 6, 5, 10, 4, 3, 2, 1};
```

```csharp
Dictionary<string, int> ages = new Dictionary<string, int>()
{
    ["John"] = 53,
    ["Diana"] = 53,
    ["James"] = 26,
    ["Francesca"] = 23
};
```

```csharp
struct Person
{
    public int ID { get; set; }
    public string Name { get; set; }
    public int Age { get; set; }
}
...
// 创建并填充人员列表
List<Person> personnel = new List<Person>()
{
    new Person() { ID = 1, Name = "John", Age = 57 },
    new Person() { ID = 2, Name = "Diana", Age = 57 },
    new Person() { ID = 3, Name = "James", Age = 30 },
    new Person() { ID = 4, Name = "Francesca", Age = 27 }
};
```
