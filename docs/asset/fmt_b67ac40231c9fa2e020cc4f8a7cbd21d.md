
## 对 Silverlight 单元测试框架的元数据配置进行调整

- 对 `Silverlight` 单元测试框架的元数据配置进行一些调整，以便它执行 `nUnit` 测试而不是 `Microsoft Test (MSTest)` 测试。

- 如果你设法完成了所有这些而没有搞砸任何事情，理论上你可以使用 `nUnit` 对你的 `Silverlight` 应用程序执行测试。然而，这并不总是那么容易，而且像 `GalaSoft` 的 `MVVM Light` 框架这样的引用的存在只会使事情进一步复杂化。

由于这最后一个原因，以及许多其他原因，我不建议你费心尝试让 `nUnit` 测试在 `Windows Phone 7` 上工作。我是 `nUnit` 测试框架的忠实粉丝，总的来说，我更喜欢它而不是 `MSTest` 框架。然而，目前还没有适用于 `Windows Phone 7` 的工具和集成支持。

我不喜欢这种方法的另一件事是，测试执行环境是一个真正的 `Silverlight` 环境。尽管对 `Visual Studio` 项目进行了各种 `hack` 式修改，但你编写的测试仍有可能尝试做一些在 `Windows Phone 7` 应用程序中不可能做的事情，而你的测试仍然会通过。我更倾向于在真正的 `WP7` 环境中执行我的单元测试，我将在下一节中展示这一点。

如果在你购买并阅读本书时，`WP7` 上对 `nUnit` 的原生支持已经变得更好、更易用，并且更深入地集成到 `Visual Studio` 中，那么请随意将其作为你选择的测试框架。

## 使用 Silverlight 单元测试框架

正如我在讨论使用 `nUnit` 在 `Windows Phone 7` 上进行单元测试时所提到的，在撰写本书时，单元测试与原生工具和 `IDE` 的集成几乎不存在。让 `Silverlight` 单元测试在 `Windows Phone 7` 上工作感觉有点“`hack`”风格。然而，如果你对 `TDD` 或自动化单元测试有任何兴趣，这是值得的。我们也可以放心，未来单元测试体验只会变得更好。

要开始，你需要一个 `Silverlight 3` 版本的 `Silverlight` 工具包，可在 `http://silverlight.codeplex.com` 获取。如果你今天去那里，你会找到 `Silverlight 4` 工具包和用于 `Windows Phone 7` 的 `Silverlight` 工具包。`Silverlight 4` 工具包与 `Windows Phone 7` 不兼容（你不能从 `WP7` 项目添加对 `SL4` 程序集的引用），而 `Windows Phone 7` 工具包不包含 `Silverlight` 单元测试框架。这就是事情开始感觉有点 `hack` 式的地方。

如果你不想在互联网上搜寻包含 `Silverlight` 单元测试框架的预编译 `Silverlight 3` 二进制文件，你可以使用我在本章附带的代码示例中包含的那些。这些是预构建的 `SL3` 程序集，你可以从 `Windows Phone 7` 应用程序中引用它们。考虑到这一点，让我们开始测试吧。

首先，你需要一个计划测试的应用程序。在本章的其余部分，我将继续使用 `Mnemuse` 应用程序，因为它已经是一个 `MVVM` 应用程序，理论上应该比传统应用程序更容易测试。其次，你需要一个将包含测试的应用程序。

如果你以前在 `Visual Studio 2010` 中做过任何单元测试，或者使用过 `nUnit` 测试运行器，这看起来可能会很别扭。如果你以前在 `iOS` 中做过单元测试，这应该感觉像是为应用程序测试创建一个新的应用程序目标。原因是 `Visual Studio 2010` 中没有用于显示测试结果的 `UI`，也没有集成的测试运行器。简而言之，我们需要一个 `WP7` 应用程序来执行我们的测试并显示结果。幸运的是，该 `UI` 的 `99.9%` 来自 `Silverlight` 单元测试框架，并且与 `Windows Phone 7` 兼容。

现在，你的 `Visual Studio 2010` 解决方案中有两个应用程序——一个是你的真实应用的 `WP7` 应用，另一个是你的测试应用的 `WP7` 应用——你需要向测试应用添加一些引用：

- 对你的真实应用程序的引用（在我们的例子中，这是 `Mnemuse` 项目）。
- 对 `Microsoft.Silverlight.Testing` 的引用（这来自 `SL` 单元测试框架，通常被亲切地称为 `SLUT`）。
- 对 `Microsoft.VisualStudio.QualityTools.UnitTesting.Silverlight` 的引用（同样来自 `v3 SLUT` 二进制文件）。
- 对 `GalaSoft.MvvmLight.Extras.WP7` 的引用。
- 对 `GalaSoft.MvvmLight.WP7` 的引用。

有了这些引用，你现在需要用于显示测试执行结果的 `UI`。幸运的是，`Silverlight` 单元测试框架的 `UI` 比

在测试项目中新建一个名为 `Tests` 的子文件夹（如果你觉得这有些多余，我们稍后还会需要其他文件夹）。在该文件夹中，放入一个名为 `EmptyTest` 的测试类，包含清单 17.2 所示的代码。

### 清单 17.2 EmptyTest.cs

```
using Microsoft.VisualStudio.TestTools.UnitTesting;
using Microsoft.Silverlight.Testing;

namespace Mnemuse.Tests.Tests
{
[TestClass]
public class EmptyTest : SilverlightTest
{
    /// <summary>
    /// This method tests the actual test harness to make sure we
    /// always get a green light when there are no tests in the system.
    /// </summary>
    [TestMethod]
    [Description(
"This is a dummy test that will always pass. If this fails, test framework is broken.")]
    [Tag("framework")]
    public void AlwaysTrue()
    {
        Mnemuse.ViewModel.Book b =
            new ViewModel.Book(); // make sure we can see our target app!
        Assert.IsTrue(true);
    }
}
}
```

你首先应该注意到，该测试类继承自基类 `SilverlightTest`。对于像这样的空测试来说，这并不是完全必要的，但当我们开始编写具有一定复杂度的测试时，使用这个基类就变得更加重要了。

接下来你会看到 `TestMethod` 特性。凡是用此特性修饰的方法都可以供测试执行工具使用。我们还为该方法提供了描述，然后使用 `Tag` 特性提供了一个标签。测试执行工具允许我们运行匹配特定标签或标签集合的所有测试。如果我们只想在特定时间运行选定的测试套件，而不是运行所有可见测试，这就很方便了。

最后，我在测试应用程序中创建了视图模型的一个实例，只是为了证明我们可以不受限制地访问该项目。如果创建该实例时抛出异常，我们就会知道测试工具的“管道”存在一些问题，需要在继续任何其他测试之前修复它。最后，我们只需断言 `true` 的值是 `true`。这应该总是产生一个“绿色”（通过）的测试，如图 17.1 所示。

![](img/04a00d46bb1059867d95707babd62ee7_256_0.png)

图 17.1 `SLUT WP7` 测试工具 `UI` 中显示的一个通过（passing）的测试

现在我们已经确信单元测试框架配置运行正常，测试执行 `UI` 也能正常工作，让我们编写一个更复杂的单元测试。如果我们一直坚持做 `TDD`，那么可能编写的一个测试是：只要在单本书上执行 `RemoveBookCommand` 命令，该执行就会导致发送 `RemoveBookMessage`。

这可能看起来像一个很容易编写的测试，但我们需要考虑消息是异步发送的。我们需要能够断言消息确实被发送了。但如果消息在后台发送，我们该怎么做呢？答案是我们的单元测试需要订阅该消息。接下来的问题就变成了如何将该消息的异步接收与单元测试的执行关联起来。幸运的是，`Silverlight` 单元测试框架提供了一个非常方便的特性，我们可以专门用它来修饰方法：`Asynchronous`。

在 `Tests` 文件夹中创建一个名为 `BookTest` 的新测试类，并让代码看起来如清单 17.3 所示。

### 清单 17.3 BookTest.cs——异步单元测试

```
using Microsoft.Silverlight.Testing;
using Microsoft.VisualStudio.TestTools.UnitTesting;
using GalaSoft.MvvmLight.Messaging;
using Mnemuse.Messages;
using Mnemuse.ViewModel;

using System.Diagnostics;

namespace Mnemuse.Tests.Tests
{
[TestClass]
public class BookTest : SilverlightTest
{
    [ClassInitialize]
    public void Init()
    {
    }

    [TestMethod]
    [Asynchronous]
    public void RemoveCommandExecuteSendsMessage()
    {
        Messenger.Default.Register<RemoveBookMessage>(this,
            (m) => {
                Debug.WriteLine(
                    "Received book removal message from Book view model.");
                EnqueueTestComplete();
            });
        Book b = new Book();
        b.RemoveBookCommand.Execute(null);
    }

    [ClassCleanup]
    public void Cleanup()
    {
    }
}
}
```

这里的关键是 `EnqueueTestComplete` 方法。没有这个调用的异步测试方法永远不会结束，而永不结束的测试就是失败的测试。我们的测试代码一收到 `RemoveBookMessage` 就调用这个方法。因为当时我们的测试代码是唯一发送消息的代码，所以我们知道 `Book` 模型通过了测试，因为我们执行了 `RemoveBookCommand`，并因此异步收到了一条 `RemoveBookMessage` 实例。

如果我们想在单元测试中更彻底一点，可以确保收到的移除消息包含我们为测试创建的那本书：

```
[TestMethod]
[Asynchronous]
public void RemoveCommandExecuteSendsMessage()
{
```

```csharp

Book b = new Book();

Messenger.Default.Register<RemoveBookMessage>(this,

(m) => {

Debug.WriteLine(

"Received book removal message from Book view model.");

Assert.AreEqual(b, m.Book);

EnqueueTestComplete();

});

b.RemoveBookCommand.Execute(null);

}

```
```

## 模拟与存根

我们现在是快乐的开发者，内心充满自信与喜悦，这股自信和喜悦只能来自构建出了一套 `100%` 通过（绿色）结果的测试。带着这股新获得的自信，我们投入下一个视图模型：`MainViewModel`。`MainViewModel` 由 `ViewModelLocator` 创建和维护。我希望我的视图模型测试尽可能贴近应用程序运行时的真实情况，因此我想从 `ViewModelLocator` 类中获取 `MainViewModel` 的测试实例。

我在测试方面已经有过一些经历，所以我知道服务提供程序是一个依赖项，它会彻底破坏我在隔离环境中进行测试的能力。我将需要创建一个虚拟的服务提供程序，供我的视图模型在测试期间使用。我需要它主要有两个原因：第一，从视图模型中移除对底层持久化机制的依赖（该机制可能是 Web 服务，而不是隔离存储）；第二，保证服务提供程序方法调用返回的值是可预测的。这些可预测的值让我在断言时可以拿来比较。

因此，我的服务提供程序是针对接口构建的。这样我就可以创建一个模拟服务提供程序，如清单 17.4 所示。

### 清单 17.4 MockMnemoserviceProvider.cs

```
```csharp

using System;

using Mnemos.Model;

using System.Collections.Generic;

namespace Mnemos.Tests.Mocks

{

	public class MockMnemosServiceProvider : IMnemosServiceProvider

	{

		private List<Book> bookList;

		private List<Character> characterList;

		public MockMnemosServiceProvider()

	}

```
```

```
[ClassInitialize]
public void Init()
{
    dummyProvider = new MockMnemuseServiceProvider();
    ViewModelLocator.CreateMain();
    main = ViewModelLocator.MainStatic;
}

[ClassCleanup]
public void Cleanup()
{
    main.Cleanup();
    main = null;
}

[TestMethod]
[Description(
"Verifies that executing the AddBookCommand adds a book to book list")]
public void AddCommandExecuteAddsBook()
{
    // Arrange
    int oldBookCount = main.Books.Count;

    // Act
    main.AddBookCommand.Execute(null);

    // Assert
    Assert.AreEqual(oldBookCount + 1, main.Books.Count);
}
}
```

这一切看起来都很直接。看看 `AddCommandExecuteAddsBook` 方法的代码，我们可以看到这条“口诀”的三个步骤。在 `arrange` 步骤中，我们对视图模型中当前存储的书籍数量做一次快照。然后通过执行 `AddBookCommand` 来 `act`。最后，我们 `assert`：在动作完成后，列表中的书籍比开始时多了一本。

这似乎没问题，但这时有什么东西让我后脖颈的汗毛竖了起来，而且不是我的猫在朝我呼吸。我创建了虚拟服务提供程序；我创建并初始化了视图模型；我安排了、行动了、也断言了。

哦，不。

我没有任何办法告诉视图模型去使用那个虚拟服务提供程序！我知道每当视图模型添加一本书时，服务提供程序就会被调用以保存书籍的模型。这可能（碰巧）对隔离存储有效，但如果我改用 Web 服务，我的测试很快就会变得棘手。这就是为什么测试周期被称为“红、绿、重构”，而不是“红、绿，完成”。

## 重构。再次。

幸运的是，我们不需要做太多事情就能让它工作。我们只需要在 `ViewModelLocator` 类上的 `ServiceProvider` 属性上添加一个公共 `setter` 即可。这将使我们能够提供自己的服务提供程序实现，以便在调用 `ViewModelLocator` 类的 `CreateMain()` 方法时，`MainViewModel` 类将获得适当的服务提供程序实例。

以下是新的 `ServiceProvider` 属性：

```
public static IMnemuseServiceProvider ServiceProvider
{
    get
    {
        if (serviceProvider == null)
            serviceProvider = new MnemuseServiceProvider();
        return serviceProvider;
    }
    set
    {
        serviceProvider = value;
    }
}
```

然后我们修改测试类上的 `Init()` 方法，以确保 `ViewModelLocator` 类使用虚拟服务提供程序：

```
[ClassInitialize]
public void Init()
{
    dummyProvider = new MockMnemuseServiceProvider();
    ViewModelLocator.ServiceProvider = dummyProvider;
    ViewModelLocator.CreateMain();
    main = ViewModelLocator.MainStatic;
}
```

现在我们可以运行我们的测试应用程序，看看是否最终完全变绿。如图 17.2 所示，我们的单元测试确实达到了 `100%` 的通过率。我们现在可以继续使用 `TDD` 来为我们的视图模型添加新功能和功能，以及创建额外的单元测试来测试可能已经编写的功能。这确保了从现在开始，我们可以确信新的代码添加不会破坏以前正常工作的代码。
