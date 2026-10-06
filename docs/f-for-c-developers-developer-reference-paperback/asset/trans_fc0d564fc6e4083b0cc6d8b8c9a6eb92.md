

> 注意：对象表达式中不支持自动实现的属性。对象表达式中的属性只能通过旧语法进行声明。

如果该字段需要是可变的，另一种方法是使用引用单元（reference cell）。代码列表 6-6 显示了如何在对象表达式内部和外部定义引用单元。代码列表 6-7 显示了如何扩展基类。

# 列表 6-6 带有属性的对象表达式

```fsharp
// 第一个接口
type IMInterface =
    abstract F : unit -> unit
    abstract Prop0 : string with get, set
    abstract Prop1 : string with get, set

// 在 objExpression 外部定义一个引用单元
let myData = ref ""

// 使用对象表达式实现接口
let objExpression =
    // 在 objExpression 内部定义一个引用单元
    let x = ref ""
    new IMInterface with
        member.F() = printf "hello object expression"
        member.Prop0 with get() = !x and set(v) = x := v
        member.Prop1 with get() = !myData and set(v) = myData := v

// 设置 Prop0 并打印结果
objExpression.Prop0 <- "set Prop0"
printf "%s" objExpression.Prop0

// 设置 Prop1 并打印结果
objExpression.Prop1 <- "set Prop1"
printf "%s" objExpression.Prop1
```

# 列表 6-7 基于类的对象表达式

```fsharp
// 定义接口
type IMInterface2 =
    abstract F2 : unit -> unit

// 抽象类定义
[AbstractClass]
type MyAbstractClass() =
    abstract F : unit -> unit
    member.this.F2() = printf "my abstract class"
```

```fsharp
// 带有抽象类和接口的对象表达式
let objExpressionInterfaceAbstract =
    {
        new MyAbstractClass() with
            override this.F() = printf "implement the abstract class"
            interface IInterface2 with
                member this.F2() = printf "from interface2"
    }

// 使用对象表达式重写 ToString 方法
let objExpressionExtendObject =
    {
        new System.Object() with
            override this.ToString() = "hello from object expression"
    }
```

与 C# 类似，基类（包含一些具体的类成员实现）在派生类定义中必须位于所有接口之前。在 F# 对象表达式中，抽象类必须出现在任何内容之前。换句话说，如果在 `objExpressionInterfaceAbstract` 中将 MyAbstractClass 放在 IInterface2 之后，代码将无法编译。

列表 6-8 是一个实现 WPF 命令的真实示例。WPF 命令通常不涉及类的构造。这是使用对象表达式的绝佳场所。从示例代码可以看出，对象表达式可以拥有在外部无法直接访问的字段。变量 `event1` 可以被视为对象表达式中实现的私有字段。此示例还显示了带参数的对象表达式（如 `createCommand`）可以作为类工厂根据内容创建对象。

# 列表 6-8 使用对象表达式的 WPF 命令

```fsharp
// 生成 WPF 命令的类工厂
let createCommand actionExecute =
    let event1 = Event<ICommand>()
        new ICommand with
            member this.CanExecute(obj) = actionExecute(obj)
            member this.Execute(obj) = actionExecute(obj)
            member this.CanExecuteChanged(handler) =
                event1.Add(handler)
            member this.RemoveExecuteChanged(handler) =
                event1.Remove(handler)

// 创建一个无所事且始终可以执行的虚拟命令
let dummyCommand = createCommand(
  (fun -> ()) // 执行无操作
  (fun -> true) // 命令始终可以执行
)
```

在你的模块中有函数和变量，并且需要一种方法为 C# 方法提供功能的情况。在模块内部组织代码最快的方法是使用对象表达式。列表 6-9 显示了一个包含三个项目的示例。以下显示了如何使用 F# 对象表达式来组织代码：

- 首先，创建一个 C# 项目，在其中定义了接口 `IMInterface`。该项目将被其他 C# 项目和 F# 项目引用。
- 其次，创建一个 C# 项目并定义了一个类 `MyFunction`，它接受 `IMInterface` 作为参数。
- 最后，一个 F# 项目创建了对象表达式并将其传递给该类。

# 列表 6-9 使用对象表达式组织代码

```csharp
// 第一个 C# 项目中的 IMInterface 定义
public interface IMInterface {
  void MyFunction();
  int MyProperty { get; set; }
}

// 第二个 C# 项目中的 MyFunction 定义
public class MyClass {
  public void MyFunction(IMInterface obj) {
    // 我的操作
  }
}
```

# 使用对象表达式组织并调用 C# 函数

```fsharp
// 函数库
module MyFunctionLibrary =
    let myFunction () = // 其他操作

// 使用对象表达式从模块中组织代码
let myData =
    let data = ref 0
    { new IMInterface with
        member.MyFunction() = MyFunctionLibrary.myFunction()
        member.MyProperty with get() = !data and set(v) = data := v
    }

// 使用对象表达式调用 C# 方法
let instance = new MyClass()
instance.MyFunction(myData)
```

对象表达式有一些限制。对象的类型信息是由编译器生成的；因此，类型名称对用户并不友好。对象的类型是密封的，所以当你真的需要复杂的继承体系时，这种类型并没有帮助。

# 处理 Option（选项）

列表 6-10 定义了一个返回 `int` option 的函数。根据 MSDN 文档，Option 具有以下特性：

> F# 中的 option 用于实际值可能不存在的情况。Option 有一个底层类型并可以持有该类型的值。

对于 C# 开发者来说，列表 6-10 类似于 6-11，后者使用了 `Nullable<T>`。C# 函数返回 `NULL`，F# 函数返回 `None`。表 6-1 显示了 option 的成员。

| 属性或方法 | 类型 | 描述 |
| :--- | :--- | :--- |
| None | 'T option | None 值。这是一个静态属性。 |
| IsNone | Boolean | 如果 option 是 None，则返回 TRUE。 |
| IsSome | Boolean | 如果 option 有值，则返回 TRUE。 |
| Some | 'T option |  None，但它返回 Some。 |
| Value | 'T | 获取底层值。如果没有值（None），将抛出 NullReferenceException。 |

`NULL` 和 `None` 之间存在细微区别。首先，F# 类和其他引用对象不接受 `NULL` 作为有效值。例如，列表 2-16 中的 `GetDistance` 函数无法传递 `NULL`。

# 列表 6-10 返回 int option 的函数

```fsharp
// 只返回偶数 option 的函数
let filterOutOddNumber a =
    if a % 2 = 0 then Some(a)
    else None
```

# 列表 6-11 C# 函数过滤奇数

```csharp
static Nullable<int> FilterOutOddNumber(int a) {
    if (a % 2 == 0) {
        return a;
    }
    else {
        return null;
    }
}
```

F# 函数 `GetDistance` 无法接受 `NULL` 参数并不是错误。实际上，这是一个经过仔细设计的 F# 特性。列表 6-12 显示了如何在 C# 和 F# 中检查用户输入。C# 代码看起来完美，直到你发现 `str` 可能为空！所以你必须先检查 `str != null` 然后执行工作。而这种错误只能在运行时捕获。

