
```
var fields = fieldsCollector.GetAllFields();
foreach (var field in fields)
    Console.WriteLine($"'{field.Key}': '{field.Value}'");
```

## 演示

对于此 JSON 对象

```
{
  "User": "John",
  "Workdays": {
    "Monday": true,
    "Tuesday": true,
    "Friday": false
  },
  "Age": 42
}
```

预期输出为：

```
User: 'John'
Workdays.Monday: 'True'
Workdays.Tuesday: 'True'
Workdays.Friday: 'False'
Age: '42'
```

## 第84章：Lambda 表达式

### 第84.1节：Lambda 表达式作为委托初始化的简写

```
public delegate int ModifyInt(int input);
ModifyInt multiplyByTwo = x => x * 2;
```

上述 Lambda 表达式语法等价于以下冗长的代码：

```
public delegate int ModifyInt(int input);

ModifyInt multiplyByTwo = delegate(int x){
    return x * 2;
};
```

### 第84.2节：Lambda 表达式作为事件处理程序

Lambda 表达式可用于处理事件，这在以下情况很有用时：

- 处理程序很短。
- 处理程序永远不需要取消订阅。

下面给出了可能使用 lambda 事件处理程序的良好情况：

```
smtpClient.SendCompleted += (sender, args) => Console.WriteLine("Email sent");
```

如果在代码的某个未来点需要取消注册已注册的事件处理程序，则应将事件处理程序表达式保存到变量中，并通过该变量进行注册/取消注册：

```
EventHandler handler = (sender, args) => Console.WriteLine("Email sent");

smtpClient.SendCompleted += handler;
smtpClient.SendCompleted -= handler;
```

这样做而不是简单地逐字重写 lambda 表达式以取消订阅它 (-=) 的原因是 C# 编译器不一定会认为这两个表达式相等：

```
EventHandler handlerA = (sender, args) => Console.WriteLine("Email sent");
EventHandler handlerB = (sender, args) => Console.WriteLine("Email sent");
Console.WriteLine(handlerA.Equals(handlerB)); // May return "False"
```

请注意，如果向 lambda 表达式添加额外语句，则所需的 surrounding 大括号可能会被意外省略，而不会导致编译时错误。例如：

```
smtpClient.SendCompleted += (sender, args) => Console.WriteLine("Email sent");
emailSendButton.Enabled = true;
```

这将编译，但会导致将 lambda 表达式 (sender, args) => Console.WriteLine("Email sent"); 添加为事件处理程序，并立即执行语句 emailSendButton.Enabled = true;。要修复此问题，必须在大括号中包围 lambda 的内容。可以通过从开始就使用大括号，在向 lambda 事件处理程序添加额外语句时保持谨慎，或从开始就用圆括号包围 lambda 来避免这种情况：

```
smtpClient.SendCompleted += ((sender, args) => Console.WriteLine("Email sent"));
//Adding an extra statement will result in a compile-time error
```

### 第84.3节：Lambda 表达式具有多个参数或无参数

使用 => 运算符左侧的括号来表示多个参数。

```
delegate int ModifyInt(int input1, int input2);
ModifyInt multiplyTwoInts = (x,y) => x * y;
```

同样，空的一组括号表示该函数不接受参数。

```
delegate string ReturnString();
ReturnString getGreeting = () => "Hello world.";
```

### 第84.4节：Lambdas 可同时作为 `Func` 和 `Expression` 发出

假设以下 Person 类：

```
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
}
```

以下 lambda：

```
p => p.Age > 18
```

可以作为参数传递给以下两种方法：

```
public void AsFunc(Func<Person, bool> func)
public void AsExpression(Expression<Func<Person, bool>> expr)
```

因为编译器能够将 lambda 既转换为委托又转换为 Expressions。

显然，LINQ 提供程序严重依赖 Expressions（主要通过 IQueryable<T> 接口公开），以便能够解析查询并将其转换为存储查询。

### 第84.5节：在语句 Lambda 中放置多个语句

与表达式 lambda 不同，语句 lambda 可以包含多个由分号分隔的语句。

```
delegate void ModifyInt(int input);

ModifyInt addOneAndTellMe = x =>
{
    int result = x + 1;
    Console.WriteLine(result);
};
```

请注意，语句被大括号 {} 包围。

请记住，语句 lambda 不能用于创建表达式树。

### 第84.6节：Lambdas 同时用于 `Func` 和 `Action`

通常 lambda 用于定义简单函数（通常在 linq 表达式的上下文中）：

```
var incremented = myEnumerable.Select(x => x + 1);
```

这里返回是隐式的。

然而，也可以用 lambda 传递操作：

```
myObservable.Do(x => Console.WriteLine(x));
```

### 第84.7节：使用 lambda 语法创建闭包

请参阅有关闭包的讨论的备注。假设我们有一个接口：

```
public interface IMachine<TState, TInput>
{
    TState State { get; }
    public void Input(TInput input);
}
```

然后执行以下操作：

```
IMachine<int, int> machine = ...;
Func<int, int> machineClosure = i => {
    machine.Input(i);
    return machine.State;
};
```

现在 machineClosure 引用一个从 int 到 int 的函数，其幕后使用 machine 引用的 IMachine 实例来进行计算。即使 machine 引用超出作用域，只要 machineClosure 对象被维护，原来的 IMachine 实例将被保留为 'closure' 的一部分，由编译器自动定义。

警告：这可能意味着相同的函数调用在不同时间返回不同的值（例如，在此示例中如果机器保持其输入的总和）。在许多情况下，这可能是意外的，并且应避免在任何函数式风格的代码中使用 - 意外和意外的闭包可能是错误的来源。

### 第84.8节：将 Lambda 表达式作为参数传递给方法

```
List<int> l2 = l1.FindAll(x => x > 6);
```

这里 x => x > 6 是一个 lambda 表达式，充当谓词，确保只返回大于 6 的元素。

### 第84.9节：基本 lambda 表达式

```
Func<int, int> add1 = i => i + 1;
Func<int, int, int> add = (i, j) => i + j;
```

```
~~~csharp
// Behaviourally equivalent to:

int Add1(int i)
{
    return i + 1;
}

int Add(int i, int j)
{
    return i + j;
}

...

Console.WriteLine(add1(42)); //43
Console.WriteLine(Add1(42)); //43
Console.WriteLine(add(100, 250)); //350
Console.WriteLine(Add(100, 250)); //350
~~~
```

### 第84.10节：使用 LINQ 的基本 lambda 表达式

```
~~~csharp
// assume source is {0, 1, 2, ..., 10}

var evens = source.Where(n => n%2 == 0);
// evens = {0, 2, 4, ... 10}

var strings = source.Select(n => n.ToString());
// strings = {"0", "1", ..., "10"}
~~~
```

### 第84.11节：具有语句块体的 Lambda 语法

```
~~~csharp
Func<int, string> doubleThenAddElevenThenQuote = i => {
    var doubled = 2 * i;
    var addedEleven = 11 + doubled;
    return $"{addedEleven}'";
};
~~~
```

### 第84.12节：使用 System.Linq.Expressions 的 Lambda 表达式

```
~~~csharp
Expression<Func<int, bool>> checkEvenExpression = i => i%2 == 0;
// lambda expression is automatically converted to an Expression<Func<int, bool>>
~~~
```

## 第85章：通用 Lambda 查询构建器

### 第85.1节：QueryFilter 类

此类保存谓词过滤器值。

```
public class QueryFilter
{
    public string PropertyName { get; set; }
    public string Value { get; set; }
    public Operator Operator { get; set; }
    // In the query {a => a.Name.Equals("Pedro")}
    // Property name to filter - propertyName = "Name"
    // Filter value - value = "Pedro"
    // Operation to perform - operation = enum Operator.Equals
    public QueryFilter(string propertyName, string value, Operator operatorValue)
    {
        PropertyName = propertyName;
        Value = value;
        Operator = operatorValue;
    }
}
```

枚举以保存操作值：

```
public enum Operator
{
    Contains,
    GreaterThan,
    GreaterThanOrEqual,
    LessThan,
    LessThanOrEqualTo,
    StartsWith,
    EndsWith,
    Equals,
    NotEqual
}
```

### 第85.2节：GetExpression 方法

```
public static Expression<Func<T, bool>> GetExpression<T>(IList<QueryFilter> filters)
{
    Expression exp = null;
    // Represents a named parameter expression. {parm => parm.Name.Equals()}, it is the parm part
    // To create a ParameterExpression need the type of the entity that the query is against and a name
    // The type is possible to find with the generic T and the name is fixed parm
    ParameterExpression param = Expression.Parameter(typeof(T), "parm");
    // It is good practice never trust in the client, so it is wise to validate.
    if (filters.Count == 0)
        return null;
    // The expression creation differ if there is one, two or more filters.
    if (filters.Count != 1)
    {
```
