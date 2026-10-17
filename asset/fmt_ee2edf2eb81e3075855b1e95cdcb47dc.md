
## 输出 4-1

- 组键: `SCW`
- `SCW10`
- `SCW1`
- `SCW2`
- `SCW11`
组键: `NUT`
- `NUT10`
- `NUT1`
- `NUT2`
- `NUT11`

## 在 keySelector 表达式中处理空值

编写键选择器时，需要小心处理源数据中的空值。如果在尝试调用 `Substring` 方法时，任何部分号字符串的值为空，列表 4-1 所示的代码将失败。通常情况下空值会被安全处理，但如果范围变量在键选择器函数内部处理，则适用标准的空处理规则。因此，在尝试访问这些范围变量的属性或调用方法之前，必须确认元素为空。

以下代码在首次访问迭代查询时会抛出 `NullReferenceException`：

```
string[] partNumbers = new string[] { "SCW10", null,
"SCW2", "SCW11", null, "NUT1", "NUT2", null };
// 注意 - 源数据中的空值可能会破坏你的分组
// 表达式。此分组将失败。
var q = from pn in partNumbers
    group pn by pn.Substring(0,3);
```

为了防止这种情况发生，请检查键选择表达式是否存在空值，并允许分组被正确处理，如下所示代码所示：

```c
string[] partNumbers = new string[] { "SCW10", null,
"SCW2", "SCW11", null, "NUT1", "NUT2", null };
```

三元运算符 (`?`) 和空合并运算符 (`??`) 为处理潜在的空值提供了简便的语法。列表 4-2 展示了它们的用法。

## 使用三元运算符 (?) 和空合并运算符 (??)

三元运算符将常见的 `(条件) 然后 (真值表达式) 否则 (假值表达式)` 代码模式缩短为 `(条件) ? (真值表达式) : (假值表达式)`。这在查询表达式中处理空值时特别有用，因为此时完整的 `if-else` 语句并不是有效的语法。

空合并运算符用于在变量为空值时定义一个默认值，即 `x = (变量) ?? (空时的默认值)`。列表 4-2 展示了这种用法。

## 列表 4-2 使用空合并运算符和三元运算符保护 keySelector 表达式免受空值的示例

```csharp
// 使用三元运算符 (? 如所示
// 防止空数据影响
var q1 = from c in Contact.SampleData()
    group c by
        c.State == null ? "(null)" : c.State;
```

```csharp
// 使用空合并运算符 (??)
// 防止空数据影响
var q2 = from c in Contact.SampleData()
    group c by
        c.State ?? "(null)";
```

## 按复合键分组（多个值）

要使用多个一个值作为键进行分组（通常称为复合键），你需要将分组选择器指定为匿名类型（匿名类型在第 2 章“介绍 LINQ to Objects”中引入）。此匿名类型可以指定任意数量的键值，任何包含相同值的元素都将忠实地分在一组。

列表 4-3 展示了通过分组表达式指定多个键值的简单性。在本例中，`LastName` 和 `State` 字段被用于分组，将具有相同姓氏和相同状态的所有联系放在一个组。此示例的控制台输出位于输出 4-2。

列表 4-3 匿名类型可以按多个值分组（复合键）——使用输出 4-2

```csharp
/* 这使用了我们在表 2-2 中看到的相同数据，
但我添加了 2 个 Gottshall（一个在相同状态，
另一个在其他状态），以及 2 个 Gauwain - */
```

## 如何分组元素

| 名字 | 姓 | 州 |
| --- | --- | --- |
| Barney | Gottshall | CA |
| Mandy | Gottshall | CA | *新增 |
| Bernadette | Gottshall | WA | *新增 |
| Armando | Valdes | WA |
| Adam | Gauvain | AK |
| Chris | Gauvain | AK | *新增 |
| Anthony | Gauvain | CA | *新增 |
| Jeffrey | Deane | CA |
| Collin | Zeeman | FL |
| Stewart | Kagel | WA |
| Chance | Lard | WA |
| Blaine | Reifsteck | TX |
| Mack | Kamph | TX |
| Ariel | Hazelgrove | OR |

```c
/* var q = from c in Contact.SampleData()
   group c by new { c.LastName, c.State };
foreach (var grp in q)
{
   Console.WriteLine("Group - {0}, {1} - count = {2}",
   grp.Key.LastName,
   grp.Key.State,
   grp.Count());
}
```

## 输出 4-2

```
Group - Gottshall, CA - count = 2
Group - Gottshall, WA - count = 1
Group - Valdes, WA - count = 1
Group - Gauvain, AK - count = 2
Group - Gauvain, CA - count = 1
Group - Deane, CA - count = 1
Group - Zeeman, FL - count = 1
Group - Kagel, WA - count = 1
Group - Lard, WA - count = 1
Group - Reifsteck, TX - count = 1
Group - Kamph, TX - count = 1
Group - Hazelgrove, OR - count = 1
```

# 82 第 4 章 数据的分组与连接

使用匿名类型作为分组键选择器来实现多属性分组并非必须的。一个包含所有参与键属性的命名类型也可以实现相同的目的，尽管这种方法更为复杂，因为构造的类型需要自定义重写 `GetHashCode` 和 `Equals` 方法，以强制按属性值而非引用相等性进行比较。列表 4-4 展示了使用 `LastName` 和 `State` 字段创建一个支持复合键的类的机制。结果与输出 4-2 所示相同。

注意：编写良好的 `GetHashCode` 实现超出了本书的范围。我在此示例中使用了一个简单的实现——更多细节请参阅 MSDN 文章，有关如何重写 `GetHashCode` 实现的建议，地址为 `http://msdn.microsoft.com/en-us/library/system.object.gethashcode.aspx`。

## 列表 4-4 使用普通类类型创建复合连接键

```csharp
public class LastName {
    public string LastName { get; set; }
    public string State { get; set; }
    // 遵循 MSDN 指南 -
    // http://msdn.microsoft.com/en-us/library/
    // ms173147(VS.80).aspx
    public override bool Equals(object obj) {
        if (this != obj) {
            LastName item = obj as LastName;
            if (item == null) return false;
            if (State != item.State) return false;
            if (LastName != item.LastName) return false;
        }
        return true;
    }
}
```

# 如何分组元素 83

```csharp
// 遵循 MSDN 指南 -
// http://msdn.microsoft.com/en-us/library/
// system.object.getethashcode.aspx
public override int GetHashCode()
{
    int result = State != null ? State.GetHashCode() : 0;
    result = result ^
    (LastName != null ? LastName.GetHashCode() : 2);
    return result;
}
```

```csharp
var q = from c in Contact.SampleData()
    group c by new LastNameState {
    LastName = c.LastName, State = c.State };
```

## 指定你自己的键值比较函数

分组的默认行为是使用所测试类型的 `equals` 比较来等同键的相等性。这并不总是适用于你的需求，你可以重写此行为并指定你的分组函数。要实现自定义比较器，你需要构建一个实现 `IComparer<T>` 接口的类，并将此类作为参数传递给 `GroupBy` 方法。

`IComparer<T>` 接口的定义如下：

```csharp
public interface IComparer<T>
{
    public bool Equals(T x, T y);
    public int GetHashCode(T obj);
}
```

`Equals` 方法用于表示一个对象的实例与另一个对象的实例具有相同的相等性。重写此方法允许使用特定逻辑根据对象内部的数据来确定对象的相等性（也就是说，尽管两个对象是在不同的时间构造的，在编译器看来它们是不同的对象，但我们希望根据它们内部值的特定组合或算法来认为它们是相等的）。

# 84 第 4 章 数据的分组与连接

`GetHashCode` 方法用于哈希算法和数据结构（如哈希表）。该方法的实现根据对象实例中包含的至少一个值返回一个整数值。生成的哈希码可以被其他数据结构作为唯一值（但不保证唯一）。它的设计初图是分割集合中实例的快速方法，或作为相等性的捷径（`GetHashCode` 可用于此 `Equals` 操作符的实现）。下面的示例演示了自定义相等函数的一种可能用途。

### 1. 编写 Soundex 算法以返回一个字符后跟三个数字数字，例如 A123 或 V456。
### 2. 为给定字符串实现 `GetHashCode`。这使用字符的 ASCII 值乘以 1000 并加上 Soundex 码的三位数字后缀来构建整数，例如 A123 将变为 (65 * 1000) + 123 = 65123。
### 3. 通过对输入 x 和 y 分调用 `GetHashCode` 然后比较返回的结果来实现 `Equals` 方法。如果哈希码匹配则返回 true（这在其他 `GetHashCode` 实现中并非如此）。

构建构建 Soundex 相等性的方法是使用 Soundex (`http://en.wikipedia.org/wiki/Soundex`)，它将为发音相似的名字分组。Soundex 码如列表 4-5 所示。

# 如何分组元素 85

在决定你想要的行为时，必须考虑空值和空字符串。我决定我想让空或空字符串项位于一个组中，但这种空处理逻辑应该根据具体的实现进行考虑。（可能空字符串应该与空位于不同的组；这取决于具体情况。）

列表 4-5 自定义的 SoundexEqualityComparer 允许发音相似的字符串被轻松分组

```csharp
public class SoundexEqualityComparer
: EqualityComparer<string>
{
    public bool Equals(string x, string y)
    {
        return GetHashCode(x) == GetHashCode(y);
    }
    public int GetHashCode(string obj)
    {
        // 例如将发音码 A123，
        // 转换为整数：65123
        int result = 0;
        string s = soundex(obj);
        if (String.IsNullOrEmpty(s) == false)
            result = Convert.ToInt32(s[0]) * 1000 +
            Convert.ToInt32(s.Substring(1, 3));
        return result;
    }
}
private string soundex(string s)
{
    // 列在
    // http://en.wikipedia.org/wiki/Soundex 的算法。
    // 根据输入的发音构建格式为：
    // [A-Z][0-6][0-6][0-6] 的字符串代码。
    if (String.IsNullOrEmpty(s))
        return null;
}
```

```csharp
StringBuilder result =
  new StringBuilder(s.Length);
```

```csharp
// 添加第一个字符，然后循环处理
// 字符串的过程中进行映射
result.Append(source[0]);
char previous = ' ';
```

```csharp
for (int i = 1; i < source.Length; i++)
{
  // 映射到 soundex 数值
  char mappedTo = '0';
  char thisChar = source[i];
```

```csharp
if ("BFPV".Contains(thisChar))
    mappedTo = '1';
  else if ("CGKSQZ".Contains(thisChar))
    mappedTo = '2';
  else if ("DT".Contains(thisChar))
    mappedTo = '3';
  else if ('L' == thisChar)
    mappedTo = '4';
  else if ("MN".Contains(thisChar))
    mappedTo = '5';
  else if ('R' == thisChar)
    mappedTo = '6';
```

```csharp
// 忽略相邻的重复字符
// 非匹配字符
  if (mappedTo != previous && mappedTo != '0')
{
    result.Append(mappedTo);
    previous = mappedTo;
}
```

```csharp
while (result.Length < 4) result.Append("0");
```

```csharp
return result.ToString(0, 4);
}
```

列表 4-6 展示了如何使用自定义相等比较器（在本例中为 SoundexEqualityComparer）。控制台输出如输出 4-3 所示。

## 列表 4-6 调用新的 SoundexEqualityComparer，用于按发音相似名称分组——参见输出 4-3

```csharp
string[] names = new string[] { "Janet", "Janette", "Joanne",
"Jo-anne", "Katy", "Katie", "Ralph", "Ralphe" };
var q = names.GroupBy(s => s,
new SoundexEqualityComparer());
foreach (var group in q)
{
    Console.WriteLine(group.Key);
    foreach (var name in group)
        Console.WriteLine(" - (0)", name);
}
```
