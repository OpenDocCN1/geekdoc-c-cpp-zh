

## 德米特法则

不幸的是，德米特法则与丰收女神毫无关系。它以西北大学的德米特项目命名，该项目正是在此开发。它还被称为最少知识原则（但那可没那么有趣，对吧？）

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_459_0.png)

与开闭原则（OCP）一样，德米特法则解决了类之间耦合的问题。它基本上规定，你应该只与自己实例化的对象交互，而不与它们实例化的对象交互。让我们看一个示例：

MyClass 具有一个属性，该属性是 MyFriend 的实例。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_459_1.png)

MyFriend 具有一个属性，该属性是 MyFriendsFriend 的实例。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_459_2.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_459_3.png)

根据德米特法则，在 MyClass 中做以下任何事情都是合法的：

```
aFriend = new MyFriend();
aFriend.aFriendlyProperty = 3;
aFriend.aFriendsFriend = new MyFriendsFriend();
```

但你不应该这样做：

```
aFriend.aFriendsFriend.aDistantProperty = 5;
```

### 问题在哪里...

...当然，是脆弱性。假设应用程序已经使用了一段时间（足够让你忘记它的工作细节——比如说一周），你发现 aDistantProperty 根本不应该是一个单一属性，而应该是一个集合。这是一个重大变更，你知道你将不得不更新所有实例化 MyFriendsFriend 的类。很丑陋，但无可奈何。

Visual Studio 有一个实用工具可以帮助你；只需高亮显示 aDistantProperty，然后从上下文菜单中选择“查找所有引用”。但“查找所有引用”有一些局限性：它无法跨语言工作（如果 MyClass 是用 VB.NET 编写的呢？），也无法跨目标不同版本 .NET Framework 的项目或不同解决方案工作。这是一个有用的工具，但并不完美。

因此，第一个问题是，你可能直到 MyClass 中对 aDistantProperty 的引用出错时才会发现它。而等到它出错时，你可能已经转到下一个项目了。即使你找到了那个二级引用，它也增加了已经困难任务的复杂性，因为每当你对功能进行重大更改时，你需要了解正在更改的类，以及受该更改影响的所有类。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_460_0.png)

### 德米特法则的宜与不宜

我们已经看到一个违反德米特法则的示例，即引用属性的属性的属性。（明白了吗？）但该原则（和本章讨论的一切一样，它是原则，而非法律）可以阐述为一些特定情况：

### 可以引用：

- 你自己的属性的属性：
  ```
  MyFriend aFriend {get; set;}
  this.aFriend.aFriendProperty = 3;
  ```

- 实例变量的属性：
  ```
  MyFriend aFriend = new MyFriend();
  this.aFriend.aFriendsFriend = new MyFriendsFriend();
  ```

- 参数的属性：
  ```
  void DoSomething(MyFriend x)
  {
      x.aFriendlyProperty = 4;
  }
  ```

- 静态类的属性：
  ```
  Fonts.SystemFontFamilies;
  ```

### 不应该引用：

- 其他任何东西

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_461_0.png)

### 你做得怎么样？

以下是我能想到的三种处理该问题的方法。你想到了其他方法吗？

### 在引用类中实例化变量

```
void DoSomething(RecipeBase recipe)
{
    RecipeItem current = recipe.Items[0];
    MessageBox.Show(current.Amount.ToString());
}
```

因为 current 在方法中实例化，所以引用其属性并不违反德米特法则。

### 从 RecipeItem 公开属性

可以通过定义一个返回二手属性的属性（但在处理集合属性时这很棘手）或定义一个返回该属性的方法来实现：

```
public class RecipeItem
{
    int GetAmount(int itemNumber)
    {
        return this.Items[itemNumber].Amount;
    }
}
```

当你需要做的不仅仅是引用属性时，这是一个合理的解决方案。

### 忽略它

像任何设计原则一样，德米特法则是值得考虑的，但并非绝对必须遵守。换句话说，它就像限速（违反可能会有严重后果），而不是热力学定律（在科幻小说之外无法违反）。是的，违反德米特法则可能会导致维护噩梦。但是，像我们第一个示例中那样，为一行代码实例化一个变量，在我看来只是冗余（而且并不能真正解决问题），而第二个示例虽然确实解决了违规问题，但会用大量用处有限的包装函数使你的类变得臃肿。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_463_0.png)

### 复习

让我们从简单的开始。你能将每个定义与其描述的原则或策略匹配起来吗？

- **单一职责原则**：类应该对扩展开放，对修改关闭。
- **退化类**：没有客户端类应该依赖于低级类。相反，两者都应该依赖于抽象。
- **依赖倒置**：这个短语用于描述一个类，该类用空方法重写其从基类继承的方法之一。
- **开闭原则**：一个类应该只有一个变化的原因。
- **里氏替换原则**：对象应该只引用其自身的成员，以及它直接实例化的对象的成员。
- **凝聚力级别**：子类型必须（完全）可替换基类型。
- **德米特法则**：这是一种思考方法，用于衡量一个方法多大程度上符合单一职责原则。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_464_0.png)

### 更多复习

以下是一些违反本章讨论的一个或多个原则的代码片段。你能识别出每个片段违反了哪个原则，并提出解决方案吗？
（为了练习起见，假设解决方案是合理的。）

```
public override DoSomething() {}
```

```
public class MyClass
{
public MyRecipe BakedGoodsRecipe {get; set;}
}
```

```
public void DoSomething()
{
DisplayCurrentTime();
CalculateSalary();
UpdateCustomer();
}
```

```
public void DoSomething()
{
int CurrentValue = this.CurrentFriend.FriendsFriend.DistantProperty;
}
```

### 恭喜！你已完成本章。在进入下一章之前，花一分钟思考一下你所取得的成就...

列出你在本章学到的三件事：

- 1
- 2
- 3

你认为为什么需要知道这些东西才能成为一名 C# 程序员？

本章中有什么是你觉得需要更详细理解的吗？如果有，你打算怎么做？

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_466_0.png)

## 设计模式

那么，设计模式到底是什么？基本上，它是对常见问题的解决方案。有时模式以类图的形式表达，但更多时候是描述“谁做什么”场景的高层次图表。设计模式的想法最初由建筑师 Christopher Alexander 提出，他的著作 *永恒的建造之道* 和 *模式语言* 为常见的建筑问题提出了模式。它由 Gamma、Helm、Johnson 和 Vlissides（臭名昭著的“四人组”）在其有影响力的 *设计模式：可复用面向对象软件的基础* 中应用于软件工程。

在上一章中，我们探讨了理论家们为设计更好、更强健的软件所提出的一些原则。原则当然普遍适用于任何编程情况。而模式则是针对特定问题的通用解决方案。在本章中，我们将探讨几个在 .NET 开发中重要的模式，并查看一些在技术上不属于模式但行为有点类似的软件架构。

> 这种语言的元素被称为模式的实体。每个模式都描述了在我们环境中反复出现的问题，然后描述了解决该问题的核心，以这种方式，你可以百用百新，而永远不会以相同的方式做两次。
> 
> - Christopher Alexander, *模式语言*

