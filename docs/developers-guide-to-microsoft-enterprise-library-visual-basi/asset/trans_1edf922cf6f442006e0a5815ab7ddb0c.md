

将值 "CorpData42" 注入名为 DataSource 的属性，并使用名为 StdLogger 的映射方法解析类型 ILogger，并将结果注入 Logger 属性。

```
<register type="MyOtherObject">
    <property name="BusinessComponent" />
    <property name="DataSource" value="CorpData42" />
    <property name="Logger" dependencyName="StdLogger" dependencyType="ILogger" />
</register>
```

## 运行时配置

你可以在运行时通过调用 Unity 容器的 RegisterType 方法，为目标类的任何公共属性配置注入。这使你对该过程有很大的控制权。以下代码执行与你刚才看到的配置文件示例相同的依赖注入过程。请注意使用 ResolvedParameter 类型来指定 Unity 应使用的命名映射，以解析 ILogger 接口。

```
myContainer.RegisterType(Of MyOtherObject)(
    New InjectionProperty("BusinessComponent"), _
    New InjectionProperty("DataSource", "CorpData42"), _
    New InjectionProperty("Logger", _
        New ResolvedParameter(GetType(ILogger), "StdLogger") _
    )
)
```

你也可以在构造函数和方法调用注入以及属性注入中使用 ResolvedParameter 类型，并且在配置注入时，还有其他类型的注入参数类可用于更专业的任务。

## 使用特性进行配置

若要为属性指定注入，你可以将 Dependency 特性应用于该属性，以指示该属性定义并公开的类型是类的依赖项。以下代码演示了名为 MyNewObject 的类的属性注入，该类将类型 Database 的实例引用作为属性公开。

```
Public Class MyNewObject

    Private theDB As Database

    <Dependency> _
    Public Property CustomerDB() As Database
        Get
            Return theDB
        End Get
        Set(ByVal value As Database)
            theDB = value
        End Set
    End Property
End Class
```

当你应用 **依赖** 特性而不指定名称时，容器将返回指定的默认类型（未注册的注册）或该类型的新实例。在使用特性进行属性注入时，若要指定命名注册，请将名称作为 **依赖** 特性的参数，如下所示。

```
Public Class MyNewObject

    Private theDB As Database

    <Dependency("LocalDB")> _
    Public Property NamedDB() As Database
        Get
            Return theDB
        End Get
        Set(ByVal value As Database)
            theDB = value
        End Set
    End Property

End Class
```

## 方法调用注入

方法调用注入比构造函数和属性设置器注入少见，但在两种特定情况下很有用。首先，构造函数注入仅在实例化对象新实例时（执行构造函数时）有效，而方法调用注入适用于对象的现有实例。例如，当 Unity 解析注册为单例的实例，或当你调用容器的 **BuildUp** 方法时，它将执行该方法。

其次，虽然属性设置器注入也适用于现有实例，但它要求公开公共属性。使用方法调用注入意味着你不需要公开公共属性，即可将值注入已解析类型的现有实例中。

通常的做法是公开一个公共初始化方法，将要解析并获取其引用的对象作为参数。Unity 将填充参数，然后调用该方法。在方法执行过程中，你将解析的类型存储在类的局部变量中。

方法调用注入默认不会发生，必须通过配置文件、在运行时以编程方式配置，或向方法应用特性来进行配置。

## 设计时配置

为方法参数指定依赖注入的技术与你之前看到的构造函数参数非常相似。以下配置文件摘录定义了名为 MyNewObject 的类型中名为 Initialize 的方法的两个参数的依赖项。Unity 将通过容器解析名为 customerDB 的参数的类型，并将结果注入目标对象的该参数中。它还将字符串值“Customer Services”注入名为 departmentName 的参数中。

```
<register type="MyNewObject">
    <method name="Initialize">
        <param name="customerDB" />
        <param name="departmentName" value="Customer Services" />
    </method>
</register>
```

你也可以使用 dependencyName 和 dependencyType 特性，以与属性注入时完全相同的方式指定 Unity 应如何解析参数的类型。如果你的类中有多个方法重载，Unity 将使用你在配置中定义的参数集来确定要填充和执行的实际方法。

## 运行时配置

与构造函数和属性注入一样，你可以在运行时通过调用 Unity 容器的 RegisterType 方法，为目标类的任何公共方法配置注入。以下代码实现与你刚才看到的配置摘录相同的结果。

```
myContainer.RegisterType(Of MyNewObject)(
    New InjectionMethod("Initialize", GetType(Database), "CustomerServices") _
)
```

此外，你可以以与构造函数注入时完全相同的方式指定类型的生存期，并使用命名依赖项。

## 使用特性进行配置

你可以将 InjectionMethod 特性应用于方法，以指示方法参数中定义的任何类型都是类的依赖项。以下代码演示了最常见的场景：为名为 MyNewObject 的类将依赖对象实例保存在类级别变量中，该类公开一个名为 Initialize 的方法，该方法以类型 Database 的实例和实现 ILogger 接口的具体类型的实例作为参数。

```
Public Class MyNewObject
    Private theDB As Database
    Private theLogger As ILogger

    <InjectionMethod()> _
    Public Sub Initialize(customerDB As Database, loggingComponent As ILogger)
        ' assign the dependent objects to class-level variables
        theDB = customerDB
        theLogger = loggingComponent
    End Sub
End Class
```

你还可以将 **依赖** 特性添加到参数，以指定 Unity 应使用的注册名称来解析参数类型，这与你之前看到的使用特性的构造函数注入相同。并且，与构造函数注入一样，方法的所有参数都必须能通过容器解析。如果其中任何参数是 Unity 无法创建的值类型，你必须确保为该类型在容器中有合适的注册，或使用依赖项重写来设置值。

## 更多依赖注入机会

除了我们在此处展示的定义依赖项的技术之外，Unity 还允许你将要解析的类型及其依赖项指定为泛型类型。你还可以指定任何类型（包括泛型类型）的数组作为依赖项。你甚至可以让 Unity 自动解析数组的所有成员，或自己指定数组的各个成员。

## 解析类的填充实例

在定义对象图依赖项后，你必须通过容器解析此层次结构根节点的类型，以启动依赖注入过程。在 Unity 中，你使用 **解析** 方法启动该过程，指定你希望 Unity 填充其依赖项的对象类型。以下代码从容器中解析 **MyNewObject** 类型的填充实例。

```
Dim theInstance As MyNewObject = container.Resolve(Of MyNewObject)()
```

这将返回注册为默认类型的实例（注册时未指定名称）。如果你想解析带有名称注册的类型，请将此名称作为 **解析** 方法的参数指定。你还可以考虑使用隐式类型而不是指定类型，以使你的代码较少依赖于解析过程的结果。

```
Dim theInstance = container.Resolve(Of MyNewObject)("Registration Name")
```

或者，在解析映射类型时，你可以选择将返回类型定义为接口类型。例如，如果你在接口 **IMyType** 和具体类型 **MyNewObject** 之间注册了类型映射，则在解析时应考虑使用以下代码。

