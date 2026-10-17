
# 第 7 章 实现第一个用户故事

## 为 Session Mock 提供 Save 方法存根

最后的障碍是为 Session mock 提供一个 `Save` 方法的存根实现。在这种情况下，你必须使用 `Save` 方法来返回你在类的 `Establish_context` 方法中生成的 `ItemType` Id：

```csharp
session.Setup(s => s.Save(_itemType)).Returns(_itemID);
```

### `Establish_context` 的完整实现

```csharp
protected override void Establish_context()
{
    var randomNumberGenerator = new Random();
    _itemTypeId = randomNumberGenerator.Next(32000);

    var sessionFactory = new Mock<ISessionFactory>();
    var session = new Mock<ISession>();

    session.Setup(s => s.Save(_itemType)).Returns(_itemID);

    sessionFactory.Setup(sf => sf.OpenSession()).Returns(session.Object);
    _itemRepository = new ItemRepository(sessionFactory.Object);
}
```

### 运行通过的测试

如图 7-15 所示，测试现在通过了。

这个通过的测试意味着你已经完成了此功能。在工作环境中，你可能会在以后回来进行重构，但这个通过的测试证明了该功能根据要求是完整的，并且可以集成到代码库的其他部分。

如果你像我认识的大多数开发者一样，你有一种想要修改代码并添加让它变得“更好”的东西的冲动。克制这种冲动。添加未请求的功能（有时被称为“镀金”）往往产生的问题比它解决的更多。功能的添加会消耗时间，增加代码库的复杂度，产生维护开销，并可能影响需求覆盖系统中其他区域的行为。不要掉入“好吧，除非你真的需要它”的陷阱。除非业务要求额外的功能，否则它是不需要的。这不是懒惰，而是在保持代码库尽可能简单的同时，为业务提供所需的功能。在当前的示例中，一个记录在案的需求已完成。该需求已翻译成单元测试。满足此需求的代码就是“完成”的定义。

## 编写下一个测试

有了这个测试，是时候查看用户故事或功能，并确定是否需要编写更多测试了。在这种情况下，你确定想写一个测试来确保如果有人尝试向存储库保存 null 对象将抛出异常。与其他功能或需求一样，第一步是打开 `ItemRepositoryTests.cs`（如果尚未打开），并为此测试创建一个新类，它继承自 `when_working_with_the_item_type_repository`：

```csharp
public class class_and_saving_invalid_item_type :
    when_working_with_the_item_type_repository
{
}
```

接下来，你添加一个方法来验证测试结果是否符合你的预期——在这种情况下，即抛出了 `ArgumentNullException`：

```csharp
public class class_and_saving_invalid_item_type :
    when_working_with_the_item_type_repository
{
    private Exception _result;

    [Test]
    public void then_argument_null_exception_should_be_raised()
    {
        _result.ShouldBeInstanceOf(typeof(ArgumentNullException));
    }
}
```

此代码将 `_result` 声明为 `Exception` 类型，它是 `ArgumentNullException` 的基类型。这是因为虽然你期望调用 `ItemRepository` 会抛出异常，但你想验证抛出的异常类型。如果你将 `_result` 声明为你正在寻找的特定类型（在本例中为 `ArgumentNullException`），并且抛出了完全不同的内容（例如 `NullReferenceException` 异常），你的测试在评估结果之前就会遇到运行时错误。通过将 `_result` 声明为 `Exception` 类型的变量，无论具体类型是什么，都可以存储抛出的异常。

那么，`_result` 是如何填充的？上一个示例使用了 `Base_of` 方法的重写实现，该方法调用了方法并返回了结果：

```csharp
protected override void Base_of()
{
    _result = _itemRepository.Save(_itemType);
}
```

在这种情况下，由于你需要捕获调用 `Save` 方法时抛出的异常，你需要以不同的方式构造 `Because_of` 方法。你需要将 `Save` 调用放置在 `Try/Catch` 块中，并将异常存储在 `_result` 中：

```csharp
protected override void Because_of()
{
    try
    {
        _itemRepository.Save(null);
    }
    catch (Exception exception)
    {
        _result = exception;
    }
}
```

如果你尝试运行此测试，将得到编译错误。`invalid_type` 类没有 `_itemRepository` 变量的声明。该变量是在之前的测试 `saving_a_valid_item_type` 中创建并实例化的。你也可以在 `invalid_type` 中这样做。虽然单元测试中的某些代码重复是可以接受的，但你仍然希望单元测试代码尽可能 DRY（不要重复自己）。`saving_a_valid_item_type` 和 `saving_invalid_item_type` 类都继承自 `when_working_with_the_item_type_repository` 以减少代码复杂度，在基类中移动创建 `_itemRepository` mock 的声明：

```csharp
public class when_working_with_the_item_type_repository : Specification
{
    protected IItemRepository _itemTypeRepository;

    protected override void Establish_context()
    {
        base.Establish_context();
        _itemTypeRepository = new ItemRepository(sessionFactory.Object);
    }
}
```

你从 `saving_a_valid_item_type` 类中删除 `_itemRepository` 的声明，并删除实例化 `ItemRepository` 实例的行：

```csharp
public class and_saving_a_valid_item_type :
    when_working_with_the_item_type_repository
{
    private int _result;
    private ItemType _testItemType;
    private int _itemTypeId;

    protected override void Establish_context()
    {
        base.Establish_context();

        var randomNumberGenerator = new Random();
        _itemTypeId = randomNumberGenerator.Next(32000);

        var sessionFactory = new Mock<ISessionFactory>();
        var session = new Mock<ISession>();

        session.Setup(s => s.Save(_testItemType)).Returns(_itemTypeId);

        sessionFactory.Setup(sf => sf.OpenSession()).Returns(session.Object);
    }
}
```

你移动了 `ItemTypeRepository` mock 的声明和实例化，但 `ItemTypeRepository` mock 依赖于 `SessionFactory` 的 mock，而 `SessionFactory` 实际上依赖于 `Session` 对象。你需要将这些创建为 `when_working_with_the_item_type_repository` 类的实例变量：

```csharp
public class when_working_with_the_item_type_repository : Specification
{
    protected ITypeRepository _itemTypeRepository;
    protected Mock<ISessionFactory> _sessionFactory;
    protected Mock<ISession> _session;
}
```

```csharp
protected override void Establish_context()
{
    base.Establish_context();

    _sessionFactory = new Mock<ISessionFactory>();
    _session = new Mock<ISession>();

    _itemTypeRepository = new ItemTypeRepository(_sessionFactory.Object);
}
```

接下来，你需要将用于桩 `SessionFactory` mock 对象的 `OpenSession` 方法的代码行，从 `and_saving_a_valid_item_type` 类的 `Establish_context` 方法移动到 `when_working_with_the_item_type_repository` 类的 `Establish_context` 方法中：

```csharp
protected override void Establish_context()
{
    base.Establish_context();

    _sessionFactory = new Mock<ISessionFactory>();
    _session = new Mock<ISession>();

    _sessionFactory.Setup(sf => sf.OpenSession()).Returns(_session.Object);
    _itemTypeRepository = new ItemTypeRepository(_sessionFactory.Object);
}
```

此更改使得 `and_saving_a_valid_item_type` 类的 `Establish_context` 方法看起来如下：

```csharp
protected override void Establish_context()
{
    base.Establish_context();

    var randomNumberGenerator = new Random();
    _itemTypeId = randomNumberGenerator.Next(32000);

    _session.Setup(s => s.Save(_testItemType)).Returns(_itemTypeId);
}
```

你需要的最后一个更改是让 `and_saving_a_valid_item_type` 类的 `Establish_context` 方法使用来自 `when_working_with_the_type_repository` 成员变量 `_session`：

```csharp
protected override void Establish_context()
{
    base.Establish_context();

    var randomNumberGenerator = new Random();
    _itemTypeId = randomNumberGenerator.Next(32000);

    _session.Setup(s => s.Save(_testItemType)).Returns(_itemTypeId);
}
```
