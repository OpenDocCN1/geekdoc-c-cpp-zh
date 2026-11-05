
### Section 89.4: Standard Event Declaration

Event declaration:

```
public event EventHandler<EventArgsT> EventName;
```

Event handler declaration:

```
public void HandlerName(object sender, EventArgsT args) { /* Handler logic */ }
```

Subscribing to the event:

Dynamically:

```
EventName += HandlerName;
```

Through the Designer:

- 1. Click the Events button on the control's properties window (Lightning bolt)
- 2. Double-click the Event name:

![](img/5da9b5c72747b887ec63f57c832400bf_519_0.png)

- 3. Visual Studio will generate the event code:

```
private void Form1_Load(object sender, EventArgs e)
{
}
```

Invoking the method:

```
EventName(SenderObject, EventArguments);
```

### Section 89.5: Anonymous Event Handler Declaration

Event declaration:

```
public event EventHandler<EventArgsType> EventName;
```

Event handler declaration using lambda operator => and subscribing to the event:

```
EventName += (obj, eventArgs) => { /* Handler logic */ };
```

Event handler declaration using delegate anonymous method syntax:

```
EventName += delegate(object obj, EventArgsType eventArgs) { /* Handler Logic */ };
```

Declaration & subscription of an event handler that does not use the event's parameter, and so can use the above syntax without needing to specify parameters:

```
EventName += delegate { /* Handler Logic */ }
```

Invoking the event:

```
EventName?.Invoke(SenderObject, EventArguments);
```

### Section 89.6: Non-Standard Event Declaration

Events can be of any delegate type, not just EventHandler and EventHandler<T>. For example:

```
//Declaring an event
public event Action<Param1Type, Param2Type, ...> EventName;
```

This is used similarly to standard EventHandler events:

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

It is possible to declare multiple events of the same type in a single statement, similar to with fields and local variables (though this may often be a bad idea):

```
public event EventHandler Event1, Event2, Event3;
```

This declares three separate events (Event1, Event2, and Event3) all of type EventHandler.

Note: Although some compilers may accept this syntax in interfaces as well as classes, the C# specification (v5.0 §13.2.3) provides grammar for interfaces that does not allow it, so using this in interfaces may be unreliable with different

```
}
```

You can enhance the example by allowing the consumer to change the new value and then the value will be used for property. To do so it's enough to apply these changes in classes.

Change the definition of NewPrice to be settable:

```
public int NewPrice { get; set; }
```

Change the definition of Price to use e.NewPrice as value of property, after calling OnPriceChanging :

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

## Chapter 90: Expression Trees

| Parameter | Details |
|---|---|
| TDelegate | The delegate type to be used for the expression |
| lambdaExpression | The lambda expression (ex. num => num < 5) |

Expression Trees are Expressions arranged in a treelike data structure. Each node in the tree is a representation of an expression, an expression being code. An In-Memory representation of a Lambda expression would be an Expression tree, which holds the actual elements (i.e. code) of the query, but not its result. Expression trees make the structure of a lambda expression transparent and explicit.

### Section 90.1: Create Expression Trees with a lambda expression

Following is most basic expression tree that is created by lambda.

```
Expression<Func<int, bool>> lambda = num => num == 42;
```

To create expression trees 'by hand', one should use Expression class.

Expression above would be equivalent to:

```
ParameterExpression parameter = Expression.Parameter(typeof(int), "num"); // num argument
ConstantExpression constant = Expression.Constant(42, typeof(int)); // 42 constant
BinaryExpression equality = Expression.Equals(parameter, constant); // equality of two expressions (num == 42)
Expression<Func<int, bool>> lambda = Expression.Lambda<Func<int, bool>>(equality, parameter);
```

### Section 90.2: Creating Expression Trees by Using the API

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

### Section 90.3: Compiling Expression Trees

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

### Section 90.4: Parsing Expression Trees

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

### Section 90.5: Expression Tree Basic

Expression trees represent code in a tree-like data structure, where each node is an expression

Expression Trees enables dynamic modification of executable code, the execution of LINQ queries in various databases, and the creation of dynamic queries. You can compile and run code represented by expression trees.

These are also used in the dynamic language run-time (DLR) to provide interoperability between dynamic languages and the .NET Framework and to enable compiler writers to emit expression trees instead of Microsoft intermediate language (MSIL).

Expression Trees can be created Via

- 1. Anonymous lambda expression,
- 2. Manually by using the System.Linq.Expressions namespace.

### Expression Trees from Lambda Expressions

When a lambda expression is assigned to Expression type variable , the compiler emits code to build an expression tree that represents the lambda expression.

The following code examples shows how to have the C# compiler create an expression tree that represents the lambda expression num => num < 5.

```
Expression<Func<int, bool>> lambda = num => num < 5;
```

### Expression Trees by Using the API

Expression Trees also created using the Expression Class. This class contains static factory methods that create expression tree nodes of specific types.

Below are few type of Tree nodes.

- 1. ParameterExpression
- 2. MethodCallExpression

The following code example shows how to create an expression tree that represents the lambda expression num => num < 5 by using the API.

```
```csharp
ParameterExpression numParam = Expression.Parameter(typeof(int), "num");
ConstantExpression five = Expression.Constant(5, typeof(int));
BinaryExpression numLessThanFive = Expression.LessThan(numParam, five);
Expression<Func<int, bool>> lambda1 = Expression.Lambda<Func<int, bool>>(numLessThanFive, new
ParameterExpression[] { numParam });
```
```

### Section 90.6: Examining the Structure of an Expression using Visitor

Define a new visitor class by overriding some of the methods of ExpressionVisitor:

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

Call Visit to use this visitor on an existing expression:

```
```csharp
Expression<Func<int,bool>> isBig = a => a > 1000000;
var visitor = new PrintingVisitor();
visitor.Visit(isBig);
```
```

### Section 90.7: Understanding the expressions API

We're going to use the expression tree API to create a CalculateSalesTax tree. In plain English, here's a summary of the steps it takes to create the tree.

- 1. Check if the product is taxable
- 2. If it is, multiply the line total by the applicable tax rate and return that amount
- 3. Otherwise return 0

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
