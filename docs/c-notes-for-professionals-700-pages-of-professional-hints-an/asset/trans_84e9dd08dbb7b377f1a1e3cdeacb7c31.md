
// ...
    goto label1;
}

请注意 while 循环的条件可以是任意的，无论多么复杂，只要它求值（或返回）为布尔值（bool）即可。它也可以包含返回布尔值（此类函数求值结果与 `a==x` 这样的表达式相同类型）的函数。例如，

```
while (AgriculturalService.MoreCornToPick(myFarm.GetAddress()))
{
    myFarm.PickCorn();
}
```

## 第 52.31 节：null

引用类型的变量可以保存对实例的有效引用或空引用。空引用是引用类型变量以及可空值类型的默认值。

null 是表示空引用的关键字。

作为表达式，它可用于将空引用赋给上述类型的变量：

```
object a = null;
string b = null;
int? c = null;
List<int> d = null;
```

非可空值类型不能被赋值为空引用。以下所有赋值都是无效的：

```
int a = null;
float b = null;
decimal c = null;
```

空引用不应与各种类型的有效实例混淆，例如：

- 空列表 (new List<int>())
- 空字符串 ("")
- 数字零 (0, 0f, 0m)
- 空字符 ( '\0' )

有时，有意义检查某个对象是否为空或空/默认值对象。可以使用 System.String.IsNullOrEmpty(String) 方法进行检查，或自行实现等效方法。

```
private void GreetUser(string userName)
{
    if (String.IsNullOrEmpty(userName))
    {
        //The method that called us either sent in an empty string, or they sent us a null reference.
        //Either way, we need to report the problem.
        throw new InvalidOperationException("userName may not be null or empty.");
    }
    else
    {
        //userName is acceptable.
        Console.WriteLine("Hello, " + userName + "!");
    }
}
```

## 第 52.32 节：continue

立即将控制权传递给封闭循环结构（for、foreach、do、while）的下一次迭代：

```csharp
for (var i = 0; i < 10; i++)
{
    if (i < 5)
    {
        continue;
    }
    Console.WriteLine(i);
}
```

输出：

5
6
7
8
9

在 .NET Fiddle 上实时演示

```csharp
var stuff = new [] {"a", "b", null, "c", "d"};
foreach (var s in stuff)
{
    if (s == null)
    {
        continue;
    }
    Console.WriteLine(s);
}
```

输出：

a
b
c
d

在 .NET Fiddle 上实时演示

## 第 52.33 节：string

string 是 .NET 数据类型 System.String 的别名，允许存储文本（字符序列）。

记法：

```csharp
string a = "Hello";
var b = "world";
```

```csharp
var f = new string(new []{ 'h', 'i', '!' }); // hi!
```

字符串中的每个字符都使用 UTF-16 编码，这意味着每个字符至少需要 2 字节的存储空间。

## 第 52.34 节：return

> > MSDN: return 语句终止其所在方法的执行并将控制权返回给调用方法。它还可以返回一个可选值。如果方法为 void 类型，则可以省略 return 语句。

```csharp
public int Sum(int valueA, int valueB)
{
    return valueA + valueB;
}
```

```csharp
public void Terminate(bool terminateEarly)
{
    if (terminateEarly) return; // method returns to caller if true was passed in
    else Console.WriteLine("Not early"); // prints only if terminateEarly was false
}
```

## 第 52.35 节：unsafe

unsafe 关键字可用于类型或方法声明，或声明内联块。

该关键字的目的是为所讨论的块启用 C# 的不安全子集。不安全子集包括指针、栈分配、C 风格数组等特性。

不安全代码不可验证，因此其使用不被推荐。编译不安全代码需要向 C# 编译器传递一个开关。此外，CLR 要求运行的程序集具有完全信任。

尽管存在这些限制，不安全代码在使某些操作更高效（例如数组索引）或更简单（例如与某些非托管库的互操作）方面仍有合理用途。

作为一个非常简单的示例

```csharp
// compile with /unsafe
class UnsafeTest
{
    unsafe static void SquarePtrParam(int* p)
    {
        *p *= *p; // the '*' dereferences the pointer.
        //Since we passed in "the address of i", this becomes "i *= i"
    }

    unsafe static void Main()
    {
        int i = 5;
        // Unsafe method: uses address-of operator (&):
        SquarePtrParam(&i); // "&i" means "the address of i". The behavior is similar to "ref i"
        Console.WriteLine(i); // Output: 25
    }
}
```

在使用指针时，我们可以直接更改内存位置的值，而不必按名称寻址。请注意，这通常需要使用 fixed 关键字，以防止垃圾回收器移动对象时可能发生的内存损坏（否则，您可能会收到错误 CS0212）。由于已被“固定”的变量无法写入，我们通常还必须有一个第二个指针，其初始指向与第一个相同的位置。

```csharp
void Main()
{
    int[] intArray = new int[] { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

    UnsafeSquareArray(intArray);
    foreach(int i in intArray)
        Console.WriteLine(i);
}

unsafe static void UnsafeSquareArray(int[] pArr)
{
    int len = pArr.Length;

    //in C or C++, we could say
    // int* a = &(pArr[0])
    // however, C# requires you to "fix" the variable first
    fixed(int* fixedPointer = &(pArr[0]))
    {
        //Declare a new int pointer because "fixedPointer" cannot be written to.
        // "p" points to the same address space, but we can modify it
        int* p = fixedPointer;

        for (int i = 0; i < len; i++)
        {
            *p *= *p; //square the value, just like we did in SquarePtrParam, above
            p++;      //move the pointer to the next memory space.
                      // NOTE that the pointer will move 4 bytes since "p" is an
                      // int pointer and an int takes 4 bytes

            //the above 2 lines could be written as one, like this:
            // "*p *= *p++;"
        }
    }
}
```

输出：

1
4
9
16
25
36
49
64
81
100

unsafe 还允许使用 stackalloc，它会在栈上分配内存，类似于 C 运行时库中的 _alloca。我们可以按如下方式修改上述示例以使用 stackalloc：

```csharp
unsafe void Main()
{
    const int len=10;
    int* seedArray = stackalloc int[len];

    //We can no longer use the initializer “{ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10}” as before.
    // We have at least 2 options to populate the array. The end result of either
    // option will be the same (doing both will also be the same here).

    //FIRST OPTION:
    int* p = seedArray; // we don't want to lose where the array starts, so we
                        // create a shadow copy of the pointer
    for(int i=1; i<=len; i++)
        *p++ = i;
    //end of first option

    //SECOND OPTION:
    for(int i=0; i<len; i++)
        seedArray[i] = i+1;
    //end of second option

    UnsafeSquareArray(seedArray, len);
    for(int i=0; i< len; i++)
        Console.WriteLine(seedArray[i]);
}
```

```csharp
//Now that we are dealing directly in pointers, we don't need to mess around with
// “fixed”, which dramatically simplifies the code
unsafe static void UnsafeSquareArray(int* p, int len)
{
    for (int i = 0; i < len; i++)
        *p *= *p++;
}
```

（输出与上面相同）

## 第 52.36 节：switch

`switch` 语句是一种控制语句，从候选列表中选择要执行的 switch 部分。switch 语句包含一个或多个 switch 部分。每个 switch 部分包含一个或多个 `case` 标签，后跟一个或多个语句。如果没有 case 标签包含匹配的值，控制权将转移到 `default` 部分（如果存在）。严格来说，C# 不支持 case 穿透。然而，如果一个或多个 `case` 标签为空，执行将跟随包含代码的下一个 `case` 块的代码。这允许将多个 `case` 标签分组以使用相同的实现。在以下示例中，如果 month 等于 12，则 `case 2` 中的代码将被执行，因为 case 标签 12、1 和 2 被分组。如果 `case` 块不为空，则在下一个 `case` 标签之前必须存在 `break`，否则编译器会报错。

```csharp
int month = DateTime.Now.Month; // this is expected to be 1-12 for Jan-Dec

switch (month)
{
    case 12:
    case 1:
    case 2:
        Console.WriteLine("Winter");
        break;
    case 3:
    case 4:
    case 5:
        Console.WriteLine("Spring");
        break;
}
```
