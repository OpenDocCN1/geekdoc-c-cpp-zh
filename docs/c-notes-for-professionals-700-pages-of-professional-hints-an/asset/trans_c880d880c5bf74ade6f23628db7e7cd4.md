
### 第89.4节：标准事件声明

事件声明：

```
public event EventHandler<EventArgsT> EventName;
```

事件处理程序声明：

```
public void HandlerName(object sender, EventArgsT args) { /* Handler logic */ }
```

订阅事件：

动态方式：

```
EventName += HandlerName;
```

通过设计器：

- 1. 单击控件属性窗口上的事件按钮（闪电图标）
- 2. 双击事件名称：

![](img/5da9b5c72747b887ec63f57c832400bf_519_0.png)

- 3. Visual Studio 将生成事件代码：

```
private void Form1_Load(object sender, EventArgs e)
{
}
```

调用方法：

```
EventName(SenderObject, EventArguments);
```

### 第89.5节：匿名事件处理程序声明

事件声明：

```
public event EventHandler<EventArgsType> EventName;
```

使用 lambda 运算符 => 声明事件处理程序并订阅该事件：

```
EventName += (obj, eventArgs) => { /* Handler logic */ };
```

使用委托匿名方法语法声明事件处理程序：

```
EventName += delegate(object obj, EventArgsType eventArgs) { /* Handler Logic */ };
```

声明并订阅不使用事件参数的事件处理程序，因此可以使用上述语法而无需指定参数：

```
EventName += delegate { /* Handler Logic */ }
```

调用事件：

```
EventName?.Invoke(SenderObject, EventArguments);
```

### 第89.6节：非标准事件声明

事件可以是任何委托类型，而不仅仅是 EventHandler 和 EventHandler<T>。例如：

```
//Declaring an event
public event Action<Param1Type, Param2Type, ...> EventName;
```

其用法与标准 EventHandler 事件类似：

```
//Adding a named event handler
public void HandlerName(Param1Type parameter1, Param2Type parameter2, ...) {
    /* Handler logic */
}
EventName += HandlerName;

//Adding an anonymous event handler
EventName += (parameter1, parameter2, ...) => { /* Handler Logic */ };

//Invoking the event
EventName(parameter1, parameter2, ...);
```

可以在单个语句中声明多个相同类型的事件，类似于字段和局部变量（不过这通常可能不是个好主意）：

```
public event EventHandler Event1, Event2, Event3;
```

这声明了三个独立的事件（Event1、Event2 和 Event3），它们都是 EventHandler 类型。

注意：尽管某些编译器可能会在接口和类中接受此语法，但 C# 规范（v5.0 §13.2.3）为接口提供的语法不允许这样做，因此在接口中使用它可能在不同

```
}
```

你可以通过允许使用者更改新值来增强示例，然后该值将用于属性。为此，只需在类中应用这些更改即可。

将 NewPrice 的定义更改为可设置：

```
public int NewPrice { get; set; }
```

更改 Price 的定义，使其在调用 OnPriceChanging 之后使用 e.NewPrice 作为属性值：

```
int price;
public int Price
{
    get { return price; }
    set
    {
        var e = new PriceChangingEventArgs(price, value);
        OnPriceChanging(e);
        price = e.NewPrice;
    }
}
```

## 第90章：表达式树

| 参数 | 详细信息 |
|---|---|
| TDelegate | 用于表达式的委托类型 |
| lambdaExpression | lambda 表达式（例如 num => num < 5） |

表达式树是以树状数据结构排列的表达式。树中的每个节点都是一个表达式的表示，而表达式就是代码。Lambda 表达式的内存中表示就是表达式树，它保存查询的实际元素（即代码），但不保存其结果。表达式树使 lambda 表达式的结构变得透明且明确。

### 第90.1节：使用 lambda 表达式创建表达式树

以下是由 lambda 创建的最基本的表达式树。

```
Expression<Func<int, bool>> lambda = num => num == 42;
```

要“手动”创建表达式树，应使用 Expression 类。

上面的表达式等价于：

```
ParameterExpression parameter = Expression.Parameter(typeof(int), "num"); // num argument
ConstantExpression constant = Expression.Constant(42, typeof(int)); // 42 constant
BinaryExpression equality = Expression.Equals(parameter, constant); // equality of two expressions (num == 42)
Expression<Func<int, bool>> lambda = Expression.Lambda<Func<int, bool>>(equality, parameter);
```

### 第90.2节：使用 API 创建表达式树

```
using System.Linq.Expressions;

// Manually build the expression tree for
// the lambda expression num => num < 5.
ParameterExpression numParam = Expression.Parameter(typeof(int), "num");
ConstantExpression five = Expression.Constant(5, typeof(int));
BinaryExpression numLessThanFive = Expression.LessThan(numParam, five);
Expression<Func<int, bool>> lambda1 = Expression.Lambda<Func<int, bool>>(
    numLessThanFive,
    new ParameterExpression[] { numParam });
```

### 第90.3节：编译表达式树

```
// Define an expression tree, taking an integer, returning a bool.
Expression<Func<int, bool>> expr = num => num < 5;

// Call the Compile method on the expression tree to return a delegate that can be called.
Func<int, bool> result = expr.Compile();

// Invoke the delegate and write the result to the console.
Console.WriteLine(result(4)); // Prints true

// Prints True.

// You can also combine the compile step with the call/invoke step as below:
```

```
Console.WriteLine(expr.Compile()());
```

### 第90.4节：解析表达式树

```
using System.Linq.Expressions;

// Create an expression tree.
Expression<Func<int, bool>> exprTree = num => num < 5;

// Decompose the expression tree.
ParameterExpression param = (ParameterExpression)exprTree.Parameters[0];
BinaryExpression operation = (BinaryExpression)exprTree.Body;
ParameterExpression left = (ParameterExpression)operation.Left;
ConstantExpression right = (ConstantExpression)operation.Right;

Console.WriteLine("Decomposed expression: {0} => {1} {2} {3}",
    param.Name, left.Name, operation.NodeType, right.Value);

// Decomposed expression: num => num LessThan 5
```

### 第90.5节：表达式树基础

表达式树以树状数据结构表示代码，其中每个节点都是一个表达式

表达式树支持对可执行代码进行动态修改、在各种数据库中执行 LINQ 查询以及创建动态查询。你可以编译并运行由表达式树表示的代码。

它们还用于动态语言运行时（DLR），以提供动态语言与 .NET Framework 之间的互操作性，并使编译器编写者能够发出表达式树而不是 Microsoft 中间语言（MSIL）。

表达式树可以通过以下方式创建

- 1. 匿名 lambda 表达式，
- 2. 使用 System.Linq.Expressions 命名空间手动创建。

### 通过 Lambda 表达式创建表达式树

当 lambda 表达式被赋给 Expression 类型变量时，编译器会发出代码来构建表示该 lambda 表达式的表达式树。

以下代码示例展示了如何让 C# 编译器创建表示 lambda 表达式 num => num < 5 的表达式树。

```
Expression<Func<int, bool>> lambda = num => num < 5;
```

### 使用 API 创建表达式树

表达式树也可以使用 Expression 类创建。该类包含用于创建特定类型表达式树节点的静态工厂方法。

以下是几种类型的树节点。

- 1. ParameterExpression
- 2. MethodCallExpression

以下代码示例展示了如何使用 API 创建表示 lambda 表达式 num => num < 5 的表达式树。

```
```csharp
ParameterExpression numParam = Expression.Parameter(typeof(int), "num");
ConstantExpression five = Expression.Constant(5, typeof(int));
BinaryExpression numLessThanFive = Expression.LessThan(numParam, five);
Expression<Func<int, bool>> lambda1 = Expression.Lambda<Func<int, bool>>(numLessThanFive, new
ParameterExpression[] { numParam });
```
```

### 第90.6节：使用访问者检查表达式的结构

通过重写 ExpressionVisitor 的一些方法来定义新的访问者类：

```
```csharp
class PrintingVisitor : ExpressionVisitor {
    protected override Expression VisitConstant(ConstantExpression node) {
        Console.WriteLine("Constant: {0}", node);
        return base.VisitConstant(node);
    }
    protected override Expression VisitParameter(ParameterExpression node) {
        Console.WriteLine("Parameter: {0}", node);
        return base.VisitParameter(node);
    }
    protected override Expression VisitBinary(BinaryExpression node) {
        Console.WriteLine("Binary with operator {0}", node.NodeType);
        return base.VisitBinary(node);
    }
}
```
```

调用 Visit 以在现有表达式上使用此访问者：

```
```csharp
Expression<Func<int,bool>> isBig = a => a > 1000000;
var visitor = new PrintingVisitor();
visitor.Visit(isBig);
```
```

### 第90.7节：了解表达式 API

我们将使用表达式树 API 创建 CalculateSalesTax 树。用通俗的话说，以下是创建该树所需步骤的摘要。

- 1. 检查产品是否应纳税
- 2. 如果应纳税，则将行总计乘以适用税率并返回该金额
- 3. 否则返回 0

```
```csharp
//For reference, we're using the API to build this lambda expression
orderLine => orderLine.IsTaxable ? orderLine.Total * orderLine.Order.TaxRate : 0;

//The orderLine parameter we pass in to the method. We specify it's type (OrderLine) and the name of the parameter.
ParameterExpression orderLine = Expression.Parameter(typeof(OrderLine), "orderLine");

//Check if the parameter is taxable; First we need to access the is taxable property, then check if it's true
PropertyInfo isTaxableAccessor = typeof(OrderLine).GetProperty("IsTaxable");
MemberExpression getIsTaxable = Expression.MakeMemberAccess(orderLine, isTaxableAccessor);
UnaryExpression isLineTaxable = Expression.IsTrue(getIsTaxable);
```
```
