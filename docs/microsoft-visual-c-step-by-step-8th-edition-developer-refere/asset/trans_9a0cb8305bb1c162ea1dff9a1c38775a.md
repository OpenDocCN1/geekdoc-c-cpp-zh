

using BinaryTree;

记住，这个命名空间包含 Tree<TItem> 类。

6. 在 Program 类的 Main 方法之后，添加一个名为 InsertIntoTree 的方法。该方法应声明为静态 void 方法，接受一个 Tree<TItem> 参数和一个名为 data 的 TItem 元素的 params 数组。tree 参数应按引用传递，原因将在后面的步骤中说明。

方法定义应如下所示：

```
static void InsertIntoTree<TItem>(ref Tree<TItem> tree,
    params TItem[] data)
{
}
```

7. 用于插入到二叉树的 TItem 类型必须实现 IComparable<TItem> 接口。修改 InsertIntoTree 方法的定义并添加以下代码中以粗体显示的 where 子句：

```
static void InsertIntoTree<TItem>(ref Tree<TItem> tree,
    params TItem[] data) where TItem :IComparable<TItem>
{
}
```

8. 向 InsertIntoTree 方法添加以下示例中以粗体显示的语句。

这些语句遍历 params 列表，使用 Insert 方法将每个项添加到树中。如果 tree 参数指定的值最初为 null，则会创建一个新的 Tree<TItem>；这就是为什么 tree 参数按引用传递的原因。

```
static void InsertIntoTree<TItem>(ref Tree<TItem> tree,
params TItem[] data) where TItem : IComparable<TItem>
{
    foreach (TItem datum in data)
    {
        if (tree == null)
        {
            tree = new Tree<TItem>(datum);
        }
        else
        {
            tree.Insert(datum);
        }
    }
}
```

## 测试 InsertIntoTree 方法

- 1. 在 Program 类的 Main 方法中，添加以下以粗体显示的语句，这些语句创建了一个用于保存字符数据的新的 Tree，使用 InsertIntoTree 方法用一些示例数据填充它，然后使用 Tree 的 WalkTree 方法显示它：

```
static void Main(string[] args)
{
    Tree<char> charTree = null;
    InsertIntoTree<char>(ref charTree, 'M', 'X', 'A', 'M', 'Z', 'Z', 'N');
    string sortedData = charTree.WalkTree();
    Console.WriteLine($"Sorted data is: {sortedData}");
}
```

- 2. 在 Build 菜单上，单击 Build Solution，验证解决方案是否编译成功，并在必要时更正任何错误。

- 3. 在 Debug 菜单上，单击 Start Without Debugging。
- 程序运行并按以下顺序显示字符值：
- A M M N X Z Z

- 4. 按 Enter 键返回到 Visual Studio 2015。

## 协变和泛型接口

第 8 章演示了你可以使用 object 类型保存任何其他类型的 value 或 reference。例如，以下代码完全合法：

```
string myString = "Hello";
object myObject = myString;
```

记住，从继承的角度来看，String 类派生自 Object 类，因此所有字符串都是对象。

现在考虑以下泛型接口和类：

```
interface IWrapper<T>
{
    void SetData(T data);
    T GetData();
}
class Wrapper<T> : IWrapper<T>
{
    private T storedData;
    void IWrapper<T>.SetData(T data)
{
```

```
this.storedData = data;
}

T IWrapper<T>.GetData()
{
    return this.storedData;
}
}
```

Wrapper<T> 类在指定类型周围提供了一个简单的包装器。IWrapper 接口定义了 Wrapper<T> 类实现以存储数据的 SetData 方法，以及 Wrapper<T> 类实现以检索数据的 GetData 方法。你可以创建此类的一个实例并像这样用它包装一个字符串：

```
Wrapper<string> stringWrapper = new Wrapper<string>();
IWrapper<string> storedStringWrapper = stringWrapper;
storedStringWrapper.SetData("Hello");
Console.WriteLine($"Stored value is
{storedStringWrapper.GetData()}");
```

代码创建了一个 Wrapper<string> 类型的实例。它通过 IWrapper<string> 接口引用该对象以调用 SetData 方法。 （Wrapper<T> 类型显式实现其接口，因此你必须通过适当的接口引用调用方法。）代码还通过 IWrapper<string> 接口调用 GetData 方法。如果运行此代码，它会输出消息“Stored value is Hello”。

看看以下代码行：

```
IWrapper<object> storedObjectWrapper = stringWrapper;
```

此语句与前面代码示例中创建 IWrapper<string> 引用的语句类似，不同之处在于类型参数是 object 而不是 string。这段代码合法吗？记住所有字符串都是对象（正如前面所示，你可以将字符串值分配给对象引用），因此从理论上讲，此语句看起来很有希望。然而，如果你尝试它，该语句将无法编译，并显示消息“Cannot implicitly convert type ‘Wrapper<string>’ to ‘IWrapper<object>’。”

你可以尝试显式转换，如下所示：

```
IWrapper<object> storedObjectWrapper =
(IWrapper<object>)stringWrapper;
```

此代码可以编译，但在运行时会失败，并出现 InvalidCastException 异常。问题在于，虽然所有字符串都是对象，但反之则不

成立。如果允许此语句，你可以编写如下代码，最终尝试将 Circle 对象存储在字符串字段中：

```
IWrapper<object> storedObjectWrapper =
(IWrapper<object>)stringWrapper;
Circle myCircle = new Circle();
storedObjectWrapper.SetData(myCircle);
```

IWrapper<T> 接口被称为不变的。即使类型 A 派生自类型 B，也不能将 IWrapper<A> 对象分配给 IWrapper<B> 类型的引用。默认情况下，C# 实现此限制以确保代码的类型安全。

## 协变接口

假设你用以下示例中所示的 IStoreWrapper<T> 和 IRetrieveWrapper<T> 接口代替 IWrapper<T>，并像这样在 Wrapper<T> 类中实现这些接口：

```
interface IStoreWrapper<T>
{
    void SetData(T data);
}

interface IRetrieveWrapper<T>
{
    T GetData();
}

class Wrapper<T> : IStoreWrapper<T>, IRetrieveWrapper<T>
{
    private T storedData;

    void IStoreWrapper<T>.SetData(T data)
    {
        this.storedData = data;
    }

    T IRetrieveWrapper<T>.GetData()
    {
        return this.storedData;
    }
}
```

在功能上，Wrapper<T> 类与之前相同，只是你通过不同的接口访问 SetData 和 GetData 方法。

```
Wrapper<string> stringWrapper = new Wrapper<string>();
IStoreWrapper<string> storedStringWrapper = stringWrapper;
storedStringWrapper.SetData("Hello");
```

```
IRetrieveWrapper<string> retrievedStringWrapper = stringWrapper;
Console.WriteLine($"Stored value is
{retrievedStringWrapper.GetData()}");
```

那么，以下代码合法吗？

```
IRetrieveWrapper<object> retrievedObjectWrapper = stringWrapper;
```

简短的答案是否定的，它无法编译并出现与之前相同的错误。但如果你仔细想想，虽然 C# 编译器认为此语句不是类型安全的，但假设此原因的原因不再有效。IRetrieveWrapper<T> 接口仅允许你使用 GetData 方法读取 Wrapper<T> 对象中保存的数据，并且它不提供任何更改数据的方式。在此类情况下，其中类型参数仅作为泛型接口中方法的返回值出现，你可以通知编译器某些隐式转换是合法的，并且它不必强制严格的类型安全。你通过在声明类型参数时指定 out 关键字来实现这一点，如下所示：

```
interface IRetrieveWrapper<out T>
{
    T GetData();
}
```

此功能称为协变。你可以将 IRetrieveWrapper<A> 对象分配给 IRetrieveWrapper<B> 引用，只要从类型 A 到类型 B 存在有效的转换，或者类型 A 派生自类型 B。以下代码现在可以编译并按预期运行：

```
// string derives from object, so this is now legal
IRetrieveWrapper<object> retrievedObjectWrapper = stringWrapper;
```

你只能在类型参数作为方法的返回类型出现时使用 out 修饰符指定类型参数。如果使用类型参数指定任何方法参数的类型，则 out 修饰符是非法的，你的代码将无法编译。此外，协变仅适用于引用类型。这是因为值类型不能形成继承层次结构。因此，以下代码将无法编译，因为 int 是值类型：

```
Wrapper<int> intWrapper = new Wrapper<int>();
IStoreWrapper<int> storedIntWrapper = intWrapper; // this is legal
...
// the following statement is not legal - ints are not objects
IRetrieveWrapper<object> retrievedObjectWrapper = intWrapper;
```
