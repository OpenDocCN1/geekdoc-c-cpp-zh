

没有任何一个函数比 GetHashCode() 引发更多的讨论和更多的困惑。继续阅读以消除所有这些困惑。

如果你定义的类型永远不会用作容器中的键，那么这无关紧要。表示窗口控件、Web 页面控件或数据库连接的类型不太可能用作集合中的键。在这些情况下，什么都不要做。所有引用类型都会有一个正确的哈希码，即使它非常低效。值类型应该是不可变的（参见第 20 条），在这种情况下，默认实现始终有效，尽管它也很低效。在你创建的大多数类型中，最好的方法是完全避免 GetHashCode() 的存在。

总有一天，你会创建一个旨在用作哈希键的类型，并且你需要编写自己的 GetHashCode() 实现，所以请继续阅读。基于哈希的容器使用哈希码来优化搜索。每个对象生成一个称为哈希码的整数值。对象根据该哈希码的值存储在桶中。要搜索对象，你请求其键并仅搜索该桶。在 .NET 中，每个对象都有一个哈希码，由 System.Object.GetHashCode() 确定。GetHashCode() 的任何重载都必须遵循以下三条规则：

- 1. 如果两个对象相等（由 operator== 定义），它们必须生成相同的哈希值。否则，哈希码无法用于在容器中查找对象。
- 2. 对于任何对象 A，A.GetHashCode() 必须是实例不变量。无论对 A 调用什么方法，A.GetHashCode() 始终必须返回相同的值。这确保了放入桶中的对象始终在正确的桶中。
- 3. 哈希函数应针对所有输入在所有整数中生成随机分布。这才是从基于哈希的容器中获得效率的方式。

编写正确且高效的哈希函数需要对类型有深入了解，以确保遵循规则 3。System.Object 和 System.ValueType 中定义的版本不具备这一优势。这些版本必须在几乎不了解你特定类型的情况下提供最佳默认行为。Object.GetHashCode() 使用 System.Object 类中的内部字段来生成哈希值。创建每个对象时，都会分配一个唯一的对象键，作为整数存储。这些键从 1 开始，每次创建任何类型的新对象时都会递增。对象标识字段在 System.Object 构造函数中设置，之后无法修改。Object.GetHashCode() 将此值作为给定对象的哈希码返回。

现在根据这三条规则来审视 Object.GetHashCode()。如果两个对象相等，Object.GetHashCode() 返回相同的哈希值，除非你重写了 operator==。System.Object 的 operator==() 版本测试对象标识。GetHashCode() 返回内部对象标识字段。这行得通。但是，如果你提供了自己的 operator== 版本，也必须提供自己的 GetHashCode() 版本，以确保遵循第一条规则。有关相等性的详细信息，请参见第 6 条。

第二条规则得到了遵循：对象创建后，其哈希码永远不会更改。

第三条规则，即针对所有输入在所有整数中生成随机分布，并不成立。除非你创建大量对象，否则数字序列并非所有整数中的随机分布。Object.GetHashCode() 生成的哈希码集中在整数范围的低端。

这意味着 Object.GetHashCode() 正确但不高效。如果你基于自己定义的引用类型创建哈希表，System.Object 的默认行为是一个可用但缓慢的哈希表。当你创建旨在用作哈希键的引用类型时，应该重写 GetHashCode() 以针对你的特定类型在所有整数中获得更好的哈希值分布。

在介绍如何编写自己的 GetHashCode() 重写之前，本节将针对相同的三条规则审视 ValueType.GetHashCode()。System.ValueType 重写了 GetHashCode()，为所有值类型提供默认行为。其版本返回类型中定义的第一个字段的哈希码。请参考此示例：

```
public struct MyStruct
{
    private string msg;
    private int id;
    private DateTime epoch;
}
```

MyStruct 对象返回的哈希码是由 msg 字段生成的哈希码。以下代码片段始终返回 true，前提是 msg 不为 null：

```
MyStruct s = new MyStruct();
s.SetMessage("Hello");
return s.GetHashCode() == s.GetHashCode();
```

第一条规则规定，两个相等的对象（由 operator==() 定义）必须具有相同的哈希码。在大多数情况下，值类型遵循此规则，但你可以打破它，就像引用类型一样。ValueType.operator==() 比较结构体中的第一个字段以及其他每个字段。这满足规则 1。只要你为 operator== 定义的任何重写都使用第一个字段，它就会起作用。任何第一个字段不参与类型相等性的结构体都违反此规则，从而破坏 GetHashCode()。

第二条规则规定，哈希码必须是实例不变量。只有当结构体中的第一个字段是不可变字段时，才遵循该规则。如果第一个字段的值可以更改，哈希码也可能更改。这违反了规则。是的，如果在对象生命周期内可以修改第一个字段，那么你创建的任何结构体的 GetHashCode() 都会失效。这是不可变值类型是你最佳选择的又一个原因（参见第 20 条）。

第三条规则取决于第一个字段的类型及其使用方式。如果第一个字段在所有整数中生成随机分布，并且第一个字段分布在结构体的所有值中，那么结构体也会生成均匀分布。但是，如果第一个字段通常具有相同的值，则违反此规则。请考虑对前面结构体的小更改：

```
public struct MyStruct
{
    private DateTime epoch;
    private string msg;
    private int id;
}
```

如果 epoch 字段设置为当前日期（不包括时间），则在给定日期创建的所有 MyStruct 对象都将具有相同的哈希码。这阻止了所有哈希码值之间的均匀分布。

总结默认行为，Object.GetHashCode() 对引用类型工作正确，尽管它不一定生成高效的分布。（如果你重写了 Object.operator==()，则可能会破坏 GetHashCode()。）ValueType.GetHashCode() 只有在结构体的第一个字段是只读字段时才有效。ValueType.GetHashCode() 只有在结构体的第一个字段包含其输入中有意义子集的值时，才会生成高效的哈希码。

如果你打算构建更好的哈希码，需要对类型施加一些约束。理想情况下，你应该创建一个不可变值类型。对于不可变值类型，可工作的 GetHashCode() 规则比对不受约束的类型更简单。请再次审视这三条规则，这次是在构建可工作的 GetHashCode() 实现的上下文中。

首先，如果两个对象相等（由 operator==() 定义），它们必须返回相同的哈希值。用于生成哈希码的任何属性或数据值也必须参与类型的相等性测试。显然，这意味着用于相等性的相同属性也用于哈希码生成。有可能让属性参与相等性但不用于哈希码计算。System.ValueType 的默认行为正是如此，但这通常意味着规则 3 经常被违反。相同的数据元素应同时参与两项计算。

第二条规则是 GetHashCode() 的返回值必须是实例不变量。假设你定义了一个引用类型 Customer：

```
public class Customer
{
    private string name;
    private decimal revenue;

    public Customer(string name)
    {
        this.name = name;
    }

    public string Name
    {
        get { return name; }
        set { name = value; }
    }

    public override int GetHashCode()
    {

