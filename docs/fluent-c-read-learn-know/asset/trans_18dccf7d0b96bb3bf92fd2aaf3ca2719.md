

## 重用属性

好吧，你已经了解了如何从头创建依赖项属性，但请设想一下：你正在构建一个自定义控件，并希望它具有一个 Background 属性。与其他实现 Background 属性的 WPF 类一样，你希望它是一个依赖项属性，可以从其祖先继承值，并且可以进行动画处理或数据绑定。当然，你可以从头构建它，但直接“借用”已经存在的依赖项属性不是更简单吗？

可以。AddOwner() 方法正是用来做这件事的。只需找到公开该属性的类，创建一个支持字段，并将你的类添加为该依赖项属性的所有者。你的 Background 属性将表现得就好像是你自己声明的一样。

```
public static DependencyProperty <name> = <OwningClass>.<Property>.AddOwner(typeof(<newOwner>));
```

```
public static DependencyProperty BackgroundProperty = Control.Background.AddOwner(typeof(MyClass));
```

如果在调用 AddOwner() 方法时未指定 PropertyMetadata，属性系统将通过合并定义该属性的基类的元数据值来生成元数据。在实践中，这意味着元数据将与你借用属性的类中的元数据相同，这正是你想要的。

如果你需要不同的元数据，或者只是想确保你的属性版本具有你想要的精确元数据，可以使用接受新元数据作为参数的 AddOwner() 方法重载。

```
public static DependencyProperty <name> = <OwningClass>.<Property>.AddOwner(typeof(<newOwner>), new PropertyMetadata(<...>));
```

## 属性回调

有三个位置可以“挂钩”到设置依赖项属性值的过程中。你可以通过创建回调过程，并将它们提供给属性的 Register...() 方法来实现。

- 1. ValidateValueCallback 在这里被调用。它仅接收属性的值。

验证发生在类级别，而不是实例级别。正如我们将看到的，这意味着它在某些情况下无法使用。

确定基值 | 计算表达式 | 应用动画 | 验证 | 强制

- 2. CoerceValueCallback 在这里被调用。它接收对象的副本和新值。

- 3. PropertyChangedCallback 在过程结束时被调用。它接收对象的副本和 DependencyPropertyChangedEventArgs 的实例。

PropertyChangedCallback 通常会引发 OnPropertyChanged 事件，但也可能执行其他一些操作。我们将在下一章中介绍 WPF 事件。

现在，重要的是要理解，虽然任何依赖项属性都可以在这些回调中实现行为，但并非必须如此。这不仅影响你创建的属性，也影响你使用 FCL 对象上定义的依赖项属性时的情况。调用方法总会带来少量（或大量）开销，因此只有需要回调行为的属性才会实现它们。

这通常不会造成任何问题（WPF 架构师对可能需要和不需要的功能考虑得很周全），但偶尔你会发现没有属性更改事件。你通常可以使用 OverrideMetadata 方法来绕过这个问题，但这种情况非常罕见，所以你真的不需要担心，只需知道如果需要，该功能是存在的。

## 验证回调

让我们看看回调实际是如何工作的。回调只是标准的 C# 方法，你可以在其中执行所需的任何操作。但是，依赖项属性元数据的属性以及传递给验证方法的值本身并不是方法；它们是委托类型的实例，因此回调方法必须符合委托指定的签名。（请记住，委托只是一种带有方法的数据类型，而不是例如 String 或 RecipeItem 类的实例。）让我们从 ValidateValueCallback 委托开始，它定义一个接受 Object 作为参数并返回 bool 的方法：

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_623_0.png)

### 创建验证回调

验证回调接收一个表示依赖项属性值的单个参数。由于参数定义为 Object，你几乎肯定需要将其强制转换为适当的类型：

```
private static bool ValidateAmount(Object value)
{
    int newValue = (int)value;
    if (<is valid>)
        return true;
    else
        return false;
}
```

如果值对属性有效，该方法应返回 true；如果无效，则返回 false。但请注意，你只能访问值，而不能访问属性或包含它的实例，因此只能执行离散验证。例如，你可以测试 Amount 是否为正值（这是任何 RecipeItem 所必需的），但无法执行诸如“如果 Volume 大于零，则 Weight 必须为零”之类的测试，因为这需要访问 RecipeItem 类的其他属性。

## 强制值回调

与验证回调不同，CoerceValueCallback 委托引用的方法是 PropertyMetadata 的一部分，因此它可以访问包含该属性的实例。该委托定义具有以下签名的方法：

```
Object <MethodName>(DependencyObject d, Object baseValue)
```

### 创建强制值回调

强制值回调最常用于两种情况：

- 当你希望将属性限制在特定范围内（例如小于 10,000 的正整数），但又希望可以覆盖该限制（使用验证回调无法实现），或者
- 有效值范围取决于其他属性的值。

第二种情况可能是最常见的（而且出乎意料地常见）。例如，在我们的 RecipeItem 类中，某些属性是互斥的。食谱可能指定一个鸡蛋（Count = 1）或 57 克鸡蛋（Weight = 57），但同时做两者是不明智的。你可以在强制值回调中施加此限制，该回调大致如下所示：

```
public static Object CoerceCount(DependencyObject d, Object baseValue)
{
    RecipeItem theItem = (RecipeItem)d;
    if (theItem.Weight > 0)
        theItem.Count = 0;
    return theItem.Count;
}
```

## 属性更改回调

依赖项属性的最后一种回调类型是属性更改回调，这可能是你最常使用的一种，因为它允许你的类的使用者挂钩更改（与其他仅允许从类内部进行操作的回调不同）。与强制值回调方法一样，PropertyChangedCallback 委托引用的方法声明为 PropertyMetadata 的一部分，并可以访问所有者实例。该委托定义具有以下签名的方法：

```
void <MethodName>(DependencyObject d, DependencyPropertyChangedEventArgs e)
```

与直接接收值不同，第二个参数是 DependencyPropertyChangedEventArgs 的实例，它公开了旧值和新值，以及对属性本身的引用。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_625_0.png)

### 创建属性更改回调

与其他依赖项属性回调不同，属性更改回调不参与值计算管道。相反，它在所有计算执行完毕后被调用。请注意，该方法定义为 void，并且尽管 DependencyPropertyChangedEventArgs 参数中可见旧值和新值，但所有属性都是只读的，因此你无法直接更改值。

当然，你可以在方法中直接设置属性，但这会触发另一次管道遍历。这通常是个坏主意，因为方法会在新计算结束时再次被调用，并触发又一次遍历，再一次，再一次……你的应用程序可能会陷入无限循环。虽然在属性更改回调方法中重新设置属性值是可疑的做法，但执行其他操作（例如设置不同实例属性的值）本身并没有什么固有的问题。

然而，回调最常见的用途是引发属性更改事件。因为事件可以由类内外的多个方法处理，引发事件允许客户端类响应属性更改。

