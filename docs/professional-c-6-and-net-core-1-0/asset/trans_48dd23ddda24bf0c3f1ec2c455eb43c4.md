

如果你已完成向列表中添加元素，并且不想再添加更多元素，可以通过调用 TrimExcess 方法去除不需要的容量；但是，由于重新分配需要时间，如果项数超过容量的 90%，TrimExcess 将不起作用：

```
intList.TrimExcess();
```

## 集合初始化器

还可以使用集合初始化器向集合赋值。集合初始化器的语法类似于数组初始化器，后者在第 7 章中说明。使用集合初始化器时，在集合初始化时，值在大括号内赋给集合：

```
var intList = new List<int>() {1, 2};
var stringList = new List<string>() {"one","two"};
```

> 注意 集合初始化器不会反映在编译程序集的 IL 代码中。编译器会将集合初始化器转换为对初始化器列表中每一项调用 Add 方法。

## 添加元素

可以使用 Add 方法向列表添加元素，如下例所示。泛型实例化类型定义了 Add 方法的参数类型：

```
var intList = new List<int>();
intList.Add(1);
intList.Add(2);
```

```
var stringList = new List<string>();
stringList.Add("one");
stringList.Add("two");
```

变量 racers 被定义为类型 List<Racer>。使用 new 运算符创建相同类型的新对象。由于 List<T> 类是用具体类 Racer 实例化的，现在只能通过 Add 方法添加 Racer 对象。在下面的示例代码中，创建了五位 F1 赛车手并添加到集合中。前三位使用集合初始化器添加，后两位通过显式调用 Add 方法添加（代码文件 ListSamples/Program.cs）：

```
var graham = new Racer(7,"Graham","Hill","UK", 14);
var emerson = new Racer(13,"Emerson","Fittipaldi","Brazil", 14);
var mario = new Racer(16,"Mario","Andretti","USA", 12);
```

```
var racers = new List<Racer>(20) {graham, emerson, mario};
```

```
racers.Add(new Racer(24,"Michael","Schumacher","Germany", 91));
racers.Add(new Racer(27,"Mika","Hakkinen","Finland", 20));
```

使用 List<T> 类的 AddRange 方法，可以一次向集合添加多个元素。AddRange 方法接受 IEnumerable<T> 类型的对象，因此也可以传递数组，如下所示：

```
racers.AddRange(new Racer[] {
    new Racer(14,"Niki","Lauda","Austria", 25),
    new Racer(21,"Alain","Prost","France", 51)});
```

> 注意 集合初始化器只能在声明集合时使用。AddRange 方法可以在集合初始化之后调用。如果在创建集合后动态获取数据，则需要调用 AddRange。

如果在实例化列表时已知集合的某些元素，也可以将任何实现 IEnumerable<T> 的对象传递给类的构造函数。这与 AddRange 方法非常相似：

```
var racers = new List<Racer>(
    new Racer[] {
        new Racer(12,"Jochen","Rindt","Austria", 6),
        new Racer(22,"Ayrton","Senna","Brazil", 41) });
```

## 插入元素

可以使用 Insert 方法在指定位置插入元素：

```
racers.Insert(3, new Racer(6,"Phil","Hill","USA", 3));
```

InsertRange 方法提供了插入多个元素的能力，类似于前面展示的 AddRange 方法。

如果设置的索引大于集合中的元素数量，则会抛出 ArgumentOutOfRangeException 类型的异常。

## 访问元素

所有实现 IList 和 IList<T> 接口的类都提供索引器，因此可以通过使用索引器并传入项编号来访问元素。第一个项可以用索引值 0 访问。例如，指定 racers[3] 可以访问列表的第四个元素：

```
Racer r1 = racers[3];
```

当使用 Count 属性获取元素数量时，可以使用 for 循环遍历集合中的每一项，也可以使用索引器访问每一项：

```
for (int i = 0; i < racers.Count; i++)
{
    WriteLine(racers[i]);
}
```

> 注意 对集合类的索引访问可用于 ArrayList、StringCollection 和 List<T>。

因为 List<T> 实现了 IEnumerable 接口，所以也可以使用 foreach 语句遍历集合中的项：

```
foreach (var r in racers)
{
    WriteLine(r);
}
```

> 注意 第 7 章解释了编译器如何解析 foreach 语句以使用 IEnumerable 和 IEnumerator 接口。

## 移除元素

可以按索引移除元素，或传递要移除的项。这里从集合中移除第四个元素：

```
racers.RemoveAt(3);
```

也可以直接将 Racer 对象传递给 Remove 方法来移除该元素。按索引移除速度更快，因为这里必须搜索集合才能找到要移除的项。Remove 方法首先在集合中搜索，使用 IndexOf 方法获取项的索引，然后使用该索引移除项。IndexOf 首先检查项类型是否实现了 IEquatable<T> 接口。如果实现了，则调用该接口的 Equals 方法，在集合中查找与传递方法相同的项。如果未实现该接口，则使用 Object 类的 Equals 方法比较各项。Object 类中 Equals 方法的默认实现会对值类型进行逐位比较，但对于引用类型仅比较引用。

> 注意 第 8 章“运算符和强制转换”解释了如何重写 Equals 方法。

在下面的示例中，变量 graham 引用的赛车手从集合中移除。变量 graham 是在填充集合时早些时候创建的。由于 IEquatable<T> 接口和 Object.Equals 方法没有在 Racer 类中重写，因此无法创建一个与要移除项内容相同的新对象并将其传递给 Remove 方法：

```
if (!racers.Remove(graham))
{
WriteLine("object not found in collection");
}
```

RemoveRange 方法从集合中移除多个项。第一个参数指定开始移除项的索引；第二个参数指定要移除的项数：

```
int index = 3;
int count = 5;
racers.RemoveRange(index, count);
```

要从集合中移除所有具有某些特定特征的项，可以使用 RemoveAll 方法。此方法在搜索元素时使用 Predicate<T> 参数，这将在后面讨论。要从集合中移除所有元素，请使用 ICollection<T> 接口定义的 Clear 方法。

## 搜索

有多种方法可以搜索集合中的元素。你可以获取找到项的索引，或获取项本身。可以使用 IndexOf、LastIndexOf、FindIndex、FindLastIndex、Find 和 FindLast 等方法。若仅检查某项是否存在，List<T> 类提供 Exists 方法。

IndexOf 方法需要一个对象作为参数，如果在集合中找到该项，则返回该项的索引。如果未找到该项，则返回 -1。请记住，IndexOf 使用 IEquatable<T> 接口来比较元素（代码文件 ListSamples/Program.cs）：

```
int index1 = racers.IndexOf(mario);
```

使用 IndexOf 方法时，还可以指定不搜索整个集合，而是指定搜索开始的索引以及应迭代比较的元素数。

除了使用 IndexOf 方法搜索特定项之外，还可以搜索具有某些特定特征的项，这些特征可以用 FindIndex 方法定义。FindIndex 需要一个 Predicate 类型的参数：

```
public int FindIndex(Predicate<T> match);
```

Predicate<T> 类型是一个返回布尔值且需要类型 T 作为参数的委托。如果谓词返回 true，则表示匹配，并且找到了元素。如果返回 false，则未找到元素，并继续搜索。

```
public delegate bool Predicate<T>(T obj);
```

对于使用 Racer 对象作为类型 T 的 List<T> 类，你可以传递一个返回 bool 并定义一个

