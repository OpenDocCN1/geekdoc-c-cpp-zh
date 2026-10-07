
这是数据类的一种不可变实现，旨在防止在存储数据后对其进行任何更改。将这些单独类与它们对应的变变类进行比较，并注意以下一些有趣的细节：

- C# 关键字 `readonly` 被用于数据字段。这保证了字段值在初始初始化后就无法更改。
- 构造函数是设置值的唯一方式。
- 使用了公共字段 `public fields` 来存储值。这在如今已非常不常见了，因为属性 `properties` 几乎无处不在。虽然可以使用属性，但通常是没必要的。使用属性的主要原因之一是它们与 .NET Windows Forms 实现的标准数据绑定机制完全兼容。但在本章所解释的实际实现中，它被用于算法的频率远大于直接用于 UI 展示——例如，由于它根本无法被更改，这消除了数据绑定很大比例的用例！你在这里有一个选择。在这种情况下，我选择了使用公共字段，因为这也有助于本章后部分的自动克隆机制。
- `GetValue()` 的实现完全没有变化。
- 测试代码中唯一的区别是使用了构造函数而不是初始化语法来实例化类。

通过几个简单的更改，之前概述的所有考虑因素现在都变得无关了。根据本章开头引入的术语定义，`GetValue()` 函数是一个工作单元。在它的执行环境中，`Product.Price` 和 `Count` 的值不能更改。因此，此示例中使用的数据结构是持久的。

关于这种持久性数据结构，有三个有趣的问题：

- 你什么时候认为一个数据结构是持久的？例如，一个数据结构可能会引用另一个非持久的数据结构。
- 如果数据确实需要更改会发生什么？在示例中，你必须假设产品会在某时刻更改价格。
- 持久性数据结构总是最佳答案吗？

关于这些问题的答案，请继续往下看。

### 深度的问题

在本章开头解释数据结构的持久性时，重点在于从特定工作单元的角度来看，存储在内部的数据不应该看起来发生变化。上一个示例中选择的技术实现是不可变数据类型。这并不是实现持久性数据结构的唯一方法，但由于其简单性，它是一种常用方法。

数据的不可变性是渐进的，扁平不可变 `flat immutability` 和深度不可变 `deep immutability` 之间存在区别。扁平不可变意味着特定数据结构层的值不能更改。深度不可变意味着这些值所引的所有数据结构也是不可变的。前一个示例中的数据结构同时满足这两个条件。你可以将 `PersistentOrderLine` 与 `MutableProduct` 结合，在这种情况下，你将拥有具有扁平而非深度不可变性的数据结构。通常，深度不可变是优的，但在实践中，数据结构的组合可能非常有意义。正如你将看到的，即使是具有扁平不可变的列表等复杂数据结构，实现起来并不困难。但深度不可变更多地取决于这些结构的使用方式——即你在它们中存储了什么数据——而不是取决于它们的实现。这足以回答第一个问题了。

### 克隆

第二个问题也涉及到由相互关联的对象网络所产生的“树”的深度。对于不可变对象，现实世界中数据往往偶尔发生更改的事实是通过克隆过程来管理的。基本上，为了对对象应用更改，你会创建一个与原始对象在某些或多个点上不同的对象副本。

### 自动克隆

克隆的另一个问题是 C# 中应用克隆的语法。之前的示例展示了通过向类的构造函数传递一个旧值和一个新值来构建新版本的“鸡”。遗憾的是，在实际应用中这并不会简单，因为你的数据结构会复杂得多，这意味着你必须传递许多仅从对象的旧版本读取的构造函数，以创建一个只有一个更改值的克隆对象。与许多函数式编程语言不同，C# 并没有提供创建修改后克隆的语法支持，这从编码和可靠性的角度来看使得克隆变得非常繁琐。

`FClib` 实现了一些功能，可以在一定程度上帮助自动化克隆过程，尽管这是有代价的。代码没有使用反射，而是被编译为表达式树 `expression trees`，以动态访问属性值并构造新对象；借助此功能创建克隆的过程仍然比在 C# 中手动创建相同对象要得多。

在这些库的帮助下，可以这样构建克隆的鸡和订单行：

```csharp
var chicken = new PersistentProduct('Rubber Chicken', 10.99m);
var orderLine = new PersistentOrderLine(chicken, 5);
```

```csharp
chicken = chicken.CloneWith(new Dictionary<string, object>(
  "Price", 8.49m
));
orderLine = orderLine.CloneWith(new Dictionary<string, object>(
  "Product", chicken
));
```

`Clone<T>` 方法被实现为一个扩展方法：

```csharp
public static T CloneWith<T>(T source, Dictionary<string, object> newValues) {
  return (T) GetCreator(typeof(T), newValues);
}
```

`GetCreator()` 是一个返回创建特定类型新对象的函数。返回的函数接受源对象作为参数并带有新值。以下是 `GetCreator()` 的代码，包含了它所使用的缓存，以便在多次克隆相同类型时提高效率：

```csharp
static ConcurrentDictionary<Type, Func<object, Dictionary<string, object>, object>> creators = 
new ConcurrentDictionary<Type, Func<object, Dictionary<string, object>, object>>() { });
```

```csharp
static Func<object, Dictionary<string, object>, object> GetCreator(Type type) {
  return creators.GetOrAdd(type, k => CreateCreator(k));
}
```

# 第 16 章 保持数据不变

当需要生成新的创建器时，`CreateCreator` 函数承担了繁重工作：

```csharp
static Func<object, IDictionary<string, object>, object> CreateCreator(Type type) {
    var ctors = type.GetConstructors();
    if (ctors.Length > 1)
        throw new InvalidOperationException(String.Format(
        "Can't clone {0} because it has more than one constructor.", type));
    var ctor = ctors[0];
    var cparams = ctor.GetParameters();
    var paramCount = cparams.Length;
    var paramArray = new Expression[paramCount];
    var sourceParam = Expression.Parameter(typeof(object), "s");
    var dictParam = Expression.Parameter(typeof(IDictionary<string, object>), object, "d");
    for (int i = 0; i < paramCount; i++) {
        ConstantExpression paramName = Expression.Constant(cparams[i].Name);
        paramArray[i] = Expression.Convert(
            Expression.Call(
                Expression.Call(GetOptionValueMethod, dictParam, paramName),
                OptionObject.GetValueMethod,
                Expression.Lambda(
                    Expression.Invoke(
                        Expression.Call(GetAccessorMethod, Expression.Constant(type), paramName),
                        sourceParam
                    ))
                )),
            cparams[i].ParameterType);
    }
    Expression<Func<object, IDictionary<string, object>, object>> exp =
        Expression.New(ctor, paramArray),
        sourceParam, dictParam).Compile();
    return exp;
}
```

```csharp
static Option<object> GetOptionValue(IDictionary<string, object> dict, string key)
{
    object result;
    if (dict.TryGetValue(key, out result))
        return result.ToOption();
    return Option.None;
}
```

```csharp
static MethodInfo getOptionValueMethod() => GetOptionValueMethod;
static MethodInfo GetOptionValueMethod {
    get {
        if (getOptionValueMethod == null) {
            getOptionValueMethod =
                new Func<IDictionary<string, object>, string, Option<object>>(GetOptionValue).Method;
        }
    }
}
```

![](img/0bf1584a2ce4017291813385353496b6_193_0.png)

```csharp
return getOptionValueMethod;
}
static MethodInfo optionObjectGetValueMethod;
static MethodInfo optionObjectGetValueMethod {
  get {
  if (optionObjectGetValueMethod == null) {
    optionObjectGetValueMethod = typeof(object).GetMethod("*Value", BindingFlags.Instance | BindingFlags.Public);
  }
  return optionObjectGetValueMethod;
}
}
```

代码片段 `CloningExtensions.cs`

这在某种程度上是非常命令式的代码，这种选择是因为所处理的是命令式结构，特别是参数数组，并且出于效率考虑。该函数使用表达式树来构建并编译针对给定类型的实际创建函数。这比使用反射快得多，起初看起来可能令人困惑，但是一种更具维护性且易于阅读的方法。

> 有关于表达式树的更多信息，请参见第 7 章。

最后，代码的 `GetAccessor()` 部分也存在类似的基础，在后面的代码中已经引用过：

```csharp
static Dictionary<Type, ConcurrentDictionary<string, Func<object, object>>> accessors =
new ConcurrentDictionary<Type, ConcurrentDictionary<string, Func<object, object>>>(x => x);
static object GetAccessor(Type type, string valueName) {
  Func<object, object> result;
  ConcurrentDictionary<string, Func<object, object>> typeAccessors;
  if (accessors.TryGetValue(type, out typeAccessors)) {
    if (typeAccessors.TryGetValue(valueName, out result))
      return result;
  }
  result = CreateAccessor(type, valueName);
  if (typeAccessors == null) {
```

```csharp
typeAccessors = new ConcurrentDictionary<string, Func<object, object>>(){ 
accessors[type] = typeAccessors;
typeAccessors[valueName] = result;
return result;
}
```

```csharp
static MethodInfo getAccessorMethod;
static MethodInfo GetAccessorMethod {
  get {
if (getAccessorMethod == null) {
getAccessorMethod = typeof(CloningExtensions).GetMethod("Accessor", BindingFlags.Static | BindingFlags.NonPublic);
}
return getAccessorMethod;
}
}
static Func<object, object> CreateAccessor(Type type, string valueName) {
```
