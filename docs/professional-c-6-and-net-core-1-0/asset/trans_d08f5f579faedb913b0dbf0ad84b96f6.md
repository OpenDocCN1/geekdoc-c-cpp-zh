

对象是否相同（深度比较）？

浅比较时，对象指向内存中的同一位置，而深度比较则通过对象的值和属性来判断相等性。你可以根据深度需求执行相等性检查，以帮助你决定要验证的内容。

> **NOTE** *不要被诱惑去重载比较运算符而调用从 `System.Object` 继承的实例版本的 `Equals` 方法。如果你这样做，然后尝试评估 `(objA == objB)`，当 `objA` 恰好为 `null` 时，你会得到一个异常，因为 .NET 运行时会尝试评估 `null.Equals(objB)`。反过来操作是安全的（重写 `Equals` 以调用比较运算符）。*

你还需要重载 != 运算符。这里是简单的做法：

```
public static bool operator !=(Vector left, Vector right) => !(left == right);
```

现在重写 `Equals` 和 `GetHashCode` 方法。当重写 == 运算符时，这些方法始终应该被重写。否则编译器会发出警告。

```
public override bool Equals(object obj)
{
    if (obj == null) return false;
    return this == (Vector)obj;
}
```

```
public override int GetHashCode() =>
    X.GetHashCode() + (Y.GetHashCode() << 4) + (Z.GetHashCode() << 8);
```

`Equals` 方法可以依次调用 == 运算符。哈希码的实现应快速且对同一对象始终返回相同的值。该方法在使用字典时很重要。在字典内部，它用于为对象构建树，因此最好将返回的值分布在整数范围内。`double` 类型的 `GetHashCode` 方法返回 `double` 的整数表示。对于 `Vector` 类型，底层类型的哈希值只是相加。为了使哈希码具有不同的值——例如，对于值 (5.0, 2.0, 0.0) 和 (2.0, 5.0, 0.0)——在数字相加之前，返回的哈希值的 Y 和 Z 值会分别进行 4 位和 8 位的位移。

对于值类型，你还应实现接口 `IEquatable<T>`。该接口是基类 `Object` 定义的 `Equals` 方法的强类型版本。既然其他代码都已就位，你可以轻松实现它：

```
public bool Equals(Vector other) => this == other;
```

像往常一样，你应该用一些测试代码快速确认你的重写是否有效。这次你将定义三个 Vector 对象并比较它们（代码文件 OverloadingComparisonSample/Program.cs）：

```
static void Main()
{
    var vect1 = new Vector(3.0, 3.0, -10.0);
    var vect2 = new Vector(3.0, 3.0, -10.0);
    var vect3 = new Vector(2.0, 3.0, 6.0);

    WriteLine($"vect1 == vect2 returns {(vect1 == vect2)}");
    WriteLine($"vect1 == vect3 returns {(vect1 == vect3)}");
    WriteLine($"vect2 == vect3 returns {(vect2 == vect3)}");

    WriteLine();

    WriteLine($"vect1 != vect2 returns {(vect1 != vect2)}");
    WriteLine($"vect1 != vect3 returns {(vect1 != vect3)}");
    WriteLine($"vect2 != vect3 returns {(vect2 != vect3)}");
}
```

运行示例会在命令行产生以下结果：

```
vect1 == vect2 returns True
vect1 == vect3 returns False
vect2 == vect3 returns False

vect1 != vect2 returns False
vect1 != vect3 returns True
vect2 != vect3 returns True
```

## 可以重载哪些运算符？

并非所有可用的运算符都可以重载。你可以重载的运算符列在下表中：

| 类别 | 运算符 | 限制 |
|----------|-----------|--------------|
| 算术二元 | `+`, `*`, `/`, `-`, `%` | 无 |
| 算术一元 | `+`, `-`, `++`, `--` | 无 |
| 位运算二元 | `&`, \|, `^`, `<<`, `>>` | 无 |
| 位运算一元 | `!`, `~`, `true`, `false` | `true` 和 `false` 运算符必须成对重载。 |
| 比较 | `==`, `!=`, `<`, `>`, `<=`, `>=` | 比较运算符必须成对重载。 |
| 赋值 | `+=`, `-=`, `*=`, `/=`, `>>=`, `<<=`, `%=`, `&=`, \|=, `^=` | 你不能显式重载这些运算符；当你重载 `+`、`-`、`%` 等单个运算符时，它们会被隐式重写。 |
| 索引 | `[]` | 你不能直接重载索引运算符。索引器成员类型在第 2 章中讨论，允许你在类和结构上支持索引运算符。 |
| 转换 | `()` | 你不能直接重载转换运算符。用户定义的转换（在本章最后一节讨论）允许你定义自定义转换行为。 |

> **NOTE** 你可能会想知道重载 `true` 和 `false` 运算符的原因。有一个很好的理由：什么整数值是 true 或 false 取决于你使用的技术或框架。许多技术中，0 为 false，1 为 true；其他技术定义任何非 0 值都为 true。你也可以找到将 –1 定义为 false 的技术。

## 实现自定义索引运算符

自定义索引器不能使用运算符重载语法实现，但可以使用与属性非常相似的语法实现。

首先查看访问数组元素的情况。这里创建了一个 int 元素的数组。第二行代码使用索引器访问第二个元素并传递 42。第三行使用索引器访问第三个元素并将元素传递给变量 x。

```
int[] arr1 = {1, 2, 3};
arr1[1] = 42;
int x = arr1[2];
```

> **NOTE** 数组在第 7 章中解释。

CustomIndexerSample 使用了这些依赖项和命名空间：

### 依赖项

- NETStandard.Library

### 命名空间

- System
- System.Collections.Generic
- System.Linq
- static System.Console

要创建自定义索引器，首先创建一个 Person 类，具有只读属性 FirstName、LastName 和 Birthday（代码文件 CustomIndexerSample/Person.cs）：

```
public class Person
{
    public DateTime Birthday { get; }
    public string FirstName { get; }
    public string LastName { get; }

    public Person(string firstName, string lastName, DateTime birthDay)
    {
        FirstName = firstName;
        LastName = lastName;
        Birthday = birthDay;
    }

    public override string ToString() => $"{FirstName} {LastName}";
}
```

类 PersonCollection 定义了一个包含 Person 元素的私有数组字段，以及一个构造函数，可以传递多个 Person 对象（代码文件 CustomIndexerSample/PersonCollection.cs）：

```
public class PersonCollection
{
    private Person[] _people;

    public PersonCollection(params Person[] people)
    {
        _people = people.ToArray();
    }
}
```

为了允许使用索引器语法访问 PersonCollection 并返回 Person 对象，你可以创建一个索引器。索引器看起来与属性非常相似，因为它也包含 get 和 set 访问器。不同之处在于名称。指定索引器使用 `this` 关键字。`this` 关键字后跟的括号指定与索引一起使用的类型。数组提供 int 类型的索引器，因此这里也使用 int 类型来直接传递给包含的数组 `_people`。set 和 get 访问器的使用与属性非常相似。get 访问器在检索值时被调用，set 访问器在右侧传递（Person 对象）时被调用。

```
public Person this[int index]
{
    get { return _people[index]; }
    set { _people[index] = value; }
}
```

使用索引器时，你不仅可以定义 int 类型作为索引类型。任何类型都可以使用，如下所示使用 DateTime 结构作为索引类型。此索引器用于返回具有指定生日的所有人。因为多个人的生日可能相同，所以返回的不是单个 Person 对象，而是具有接口 `IEnumerable<Person>` 的人员列表。使用的 `Where` 方法基于 lambda 表达式进行过滤。`Where` 方法定义在命名空间 `System.Linq` 中：

```
public IEnumerable<Person> this[DateTime birthDay]
{
    get { return _people.Where(p => p.Birthday == birthDay); }
}
```

使用 DateTime 类型的索引器提供检索人员对象，但不允许设置人员对象，因为只有 get 访问器而没有 set 访问器。从 C# 6 开始，存在一种简写表示法来创建相同的代码，使用表达式体成员（与属性中可用的相同语法）：

```
public IEnumerable<Person> this[DateTime birthDay] =>
    _people.Where(p => p.Birthday == birthDay);
```

示例应用程序的主方法创建一个 PersonCollection 对象并向构造函数传递四个 Person 对象。使用第一个 WriteLine 方法，使用 int 参数的索引器的 get 访问器访问第三个元素。在 foreach 循环中，使用 DateTime 参数的索引器传递指定日期（代码文件 CustomIndexerSample/Program.cs）：

```
static void Main()
{
    var p1 = new Person("Ayrton","Senna", new DateTime(1960, 3, 21));
    var p2 = new Person("Ronnie","Peterson", new DateTime(1944, 2, 14));
    var p3 = new Person("Jochen","Rindt", new DateTime(1942, 4, 18));
    var p4 = new Person("Francois","Cevert", new DateTime(1944, 2, 25));
    var coll = new PersonCollection(p1, p2, p3, p4);

    WriteLine(coll[2]);
```

