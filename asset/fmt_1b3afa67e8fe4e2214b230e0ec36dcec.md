
```csharp
hours = hh;
minutes = mm;
``` // 编译错误：seconds 未初始化

```
```csharp
struct Time
{
    private int hours = 0; // 编译错误
    private int minutes;
    private int seconds;
    ...
}
```

```csharp
struct Time
{
    private int hours, minutes, seconds;
    ...
}
```

```csharp
class Example
{
    private Time currentTime;
    public void Method(Time parameter)
    {
        Time localVariable;
        ...
    }
}
```

```csharp
struct Time
{
    private int hours, minutes, seconds;
    ...
    public Time(int hh, int mm)
    {
        hours = hh;
        minutes = mm;
        seconds = 0;
    }
}
```

```csharp
struct Date
{
    private int year;
    private Month month;
    private int day;
}
```

```csharp
struct Date
{
    private int year;
    private Month month;
    private int day;
    public Date(int ccyy, Month mm, int dd)
    {
        this.year = ccyy - 1900;
        this.month = mm;
        this.day = dd - 1;
    }
}
```

```csharp
struct Date
{
    public void AdvanceMonth()
    {
        this.month++;
        if (this.month == Month.December + 1)
        {
            this.month = Month.January;
            this.year++;
        }
    }
}
static void doWork()
{
    Date weddingAnniversaryCopy = weddingAnniversary;
    Console.WriteLine($"Value of copy is {weddingAnniversaryCopy}");
}
static void doWork()
{
    ...
    weddingAnniversary.AdvanceMonth();
    Console.WriteLine($"New value of weddingAnniversary is {weddingAnniversary}");
    Console.WriteLine($"Value of copy is still {weddingAnniversaryCopy}");
}
```

2017年7月4日
副本的值为 2017年7月4日
weddingAnniversary 的新值为 2017年8月4日
副本的值仍然为 2017年7月4日

```csharp
class Date
{
    ...
}
```

2017年7月4日
副本的值为 2017年7月4日
weddingAnniversary 的新值为 2017年8月4日
副本的值仍然为 2017年8月4日

```csharp
enum Season { Spring, Summer, Fall, Winter }
currentSeason = Spring; // 错误
currentSeason = Season.Spring; // 正确
```

```csharp
struct Time
{
    public Time(int hh, int mm, int ss) { ... }
    ...
    private int hours, minutes, seconds;
}
```

```csharp
int[] pins; // 个人识别码
int size = int.Parse(Console.ReadLine());
int[] pins = new int[size];
int[] pins = new int[4]{ 9, 3, 7, 2 };
Random r = new Random();
int[] pins = new int[4]{ r.Next() % 10, r.Next() % 10, r.Next() % 10 };
int[] pins = new int[3]{ 9, 3, 7, 2 }; // 编译错误
int[] pins = new int[4]{ 9, 3, 7, 2 }; // 编译错误
int[] pins = new int[4]{ }; // OK
Time[] schedule = { new Time(12,30), new Time(5,30) };
var names = new string[] { "John", "Francesca" };
var names = new[][] { "Diana", "James", 99, 100 };
var names = new[] { 1, 2, 3.5, 99.999 };
var names = new[] { new Name { Name = "John", Age = 53 },
    new Name { Name = "Diana", Age = 53 },
    new Name { Name = "James", Age = 26 },
    new Name { Name = "Francesca", Age = 23 } };
try
{
    int[] pins = { 9, 3, 7, 2 };
    Console.WriteLine(pins[4]); // 错误，第4个和最后一个元素索引为 3
} catch (IndexOutOfRangeException)
{
}
int[] pins = { 9, 3, 7, 2 };
for (int index = 0; index < pins.Length; index++)
{
    int pin = pins[index];
    Console.WriteLine(pin);
}
int[] pins = { 9, 3, 7, 2 };
foreach (int pin in pins)
{
    Console.WriteLine(pin);
}
var names = new[] { new Name { Name = "John", Age = 50 },
    new Name { Name = "Diana", Age = 50 },
    new Name { Name = "James", Age = 23 },
    new Name { Name = "Francesca", Age = 21 } };
foreach (var familyMember in names)
{
    Console.WriteLine($"Name: {familyMember.Name}, Age: {familyMember.Age}");
}
```

```csharp
public void ProcessData(int[] data)
{
    foreach (int i in data)
    {
        ...
    }
}
public int[] ReadData()
{
    Console.WriteLine("How many elements?");
    string reply = Console.ReadLine();
    int numElements = int.Parse(reply);
    int[] data = new int[numElements];
    for (int i = 0; i < numElements; i++)
    {
        Console.WriteLine($"Enter data for element {i}");
        reply = Console.ReadLine();
        int elementData = int.Parse(reply);
        data[i] = elementData;
    }
    return data;
}
{
    static void Main(string[] args)
    {
        ...
    }
    static void Main(string[] args)
    {
        foreach (string filename in args)
        {
            ProcessFile(filename);
        }
    }
}
```
MyUtil C:\Temp\TestData.dat C:\Users\John\Documents\MyDoc.txt
int[] pins = { 9, 3, 7, 2 };
int[] alias = pins; // alias 和 pins 指向同一个数组实例
int[] pins = { 9, 3, 7, 2 };
int[] copy = new int[pins.Length];
for (int i = 0; i < pins.Length; i++)
{
    copy[i] = pins[i];
}
```

```csharp
try
{
    for (int handNum = 0; handNum < NumHands; handNum++)
    {
        ...
    }
    north.Text = hands[0].ToString();
    south.Text = hands[1].ToString();
    east.Text = hands[2].ToString();
    west.Text = hands[3].ToString();
}
catch (Exception ex)
{
    ...
    class Person
    {
        public string Name;
        public int Age;
        public Person(string name, int age)
        {
            this.Name = name;
            this.Age = age;
        }
    }
    Person[] family = new Person[] {
        new Person("John", 53),
        new Person("Diana", 53),
        new Person("James", 26),
        new Person("Francesca", 23)
    };
}
```

```csharp
Person findYoungest()
{
    int youngest = 0;
    for (int i = 1; i < family.Length; i++)
    {
        if (family[i].Age < family[youngest].Age)
        {
            youngest = i;
        }
    }
    return family[youngest];
}
var mostYouthful = findYoungest();
Console.WriteLine($"Name: {mostYouthful.Name}, Age: {mostYouthful.Age}");
foreach (Person familyMember in family)
{
    Console.WriteLine($"Name: {familyMember.Name}, Age: {familyMember.Age}");
}
Name: John, Age: 53
Name: Diana, Age: 53
Name: James, Age: 26
Name: Francesca, Age: 24
struct Person
{
    public string Name;
    public int Age;
    public Person(string name, int age)
    {
        this.Name = name;
        this.Age = age;
    }
}
Name: John, Age: 53
Name: Diana, Age: 53
Name: James, Age: 26
Name: Francesca, Age: 23
```

```csharp
ref Person findYoungest()
{
    int youngest = 0;
    for (int i = 1; i < family.Length; i++)
    {
        if (family[i].Age < family[youngest].Age)
        {
            youngest = i;
        }
    }
    return ref family[youngest];
}
ref var mostYouthful = ref findYoungest();
foreach (Person familyMember in family)
{
    Console.WriteLine($"Name: {familyMember.Name}, Age: {familyMember.Age}");
}
```

Name: John, Age: 53

Name: Diana, Age: 53

Name: James, Age: 26

Name: Francesca, Age: 24

```csharp
// 不要尝试这样做；它无法通过编译
ref int danglingReference()
{
    int i;
    ... // 使用 i 计算一个值
    return ref i;
}
```

```csharp
bool[] flags = { true, false, true, true, false };
bool[] flags = { true, false, true, false };
for (int i = 0; i < flags.Length; i++)
{
    Console.WriteLine(flags[i]);
}
foreach (bool flag in flags)
{
    Console.WriteLine(flag);
}
bool[] flags = ...;
int noOfElements = flags.Length;
```

```csharp
int[,] table;
table = new int[4,6];
int[][] items;
items = new int[4][];
items[0] = new int[3];
items[1] = new int[10];
items[2] = new int[40];
items[3] = new int[25];
```

```csharp
class Console {
  public static void WriteLine(Int32 value);
  public static void WriteLine(Double value);
  public static void WriteLine(Decimal value);
  public static void WriteLine(Boolean value);
  public static void WriteLine(String value);
}
```

```csharp
class Util {
  public static int Min(int[] paramList) {
    
  }
}
```
// 验证调用者是否提供了至少一个参数。
// 如果没有，抛出一个 ArgumentException 异常——无法在空列表中
// 找到最小值。

```csharp
if (paramList == null || paramList.Length == 0) {
  throw new ArgumentException("Util.Min: 参数不足");
}
```
// 将参数列表中找到的最小值设置为第一个项
currentMin = paramList[0];
// 遍历参数列表，搜索是否有任何项
// 比 currentMin 持有的值小
foreach (int i in paramList)
{
  // 如果循环发现一个比 currentMin 持有的值小的项，
  //将 currentMin 设置为该值
  if (i < currentMin) {
