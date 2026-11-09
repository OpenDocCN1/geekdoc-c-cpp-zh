
```java
public class DeviceController {
    …

    public void sendShutDown() {
        try {
            tryToShutDown();
        } catch (DeviceShutDownError e) {
            logger.log(e);
        }
    }

    private void tryToShutDown() throws DeviceShutDownError {
        DeviceHandle handle = getHandle(DEV1);
        DeviceRecord record = retrieveDeviceRecord(handle);

        pauseDevice(handle);
        clearDeviceWorkQueue(handle);
        closeDevice(handle);
    }

    private DeviceHandle getHandle(DeviceID id) {
        …
        throw new DeviceShutDownError("Invalid handle for: " + id.toString());
        …
    }
    …
}
```

注意这看起来干净多了。这不仅仅是美学问题。代码更好是因为两个纠缠在一起的问题——设备关闭算法和错误处理——现在被分开了。你可以分别审视每一个问题并独立理解它们。

## 先编写你的 `Try-Catch-Finally Statement`

关于异常最有趣的事情之一是它们在程序中*定义了范围*。当你在`try-catch-finally`语句的`try`部分执行代码时，你就是在声明执行可以在任何一点中止，然后在`catch`处恢复。

从某种意义上说，`try`块就像事务。无论`try`中发生什么，你的`catch`都必须使程序保持一致的状态。因此，在编写可能抛出异常的代码时，最好从`try-catch-finally`语句开始。这有助于你定义该代码的用户应该期待什么，无论`try`中执行的代码出了什么问题。

让我们看一个例子。我们需要编写一些代码来访问文件并读取一些序列化对象。

我们从一个单元测试开始，该测试表明当文件不存在时我们会得到一个异常：

```java
@Test(expected = StorageException.class)
public void retrieveSectionShouldThrowOnInvalidFileName() {
    sectionStore.retrieveSection("invalid - file");
}
```

测试驱动我们创建这个桩代码：

```java
public List<RecordedGrip> retrieveSection(String sectionName) {
    // dummy return until we have a real implementation
    return new ArrayList<RecordedGrip>();
}
```

我们的测试失败了，因为它没有抛出异常。接下来，我们修改实现，使其尝试访问一个无效文件。这个操作会抛出异常：

```java
public List<RecordedGrip> retrieveSection(String sectionName) {
    try {
        FileInputStream stream = new FileInputStream(sectionName);
    } catch (Exception e) {
        throw new StorageException("retrieval error", e);
    }
    return new ArrayList<RecordedGrip>();
}
```

现在我们的测试通过了，因为我们已经捕获了异常。此时，我们可以进行重构。我们可以缩小捕获的异常类型，使其与`FileInputStream`构造函数实际抛出的类型匹配：`FileNotFoundException`

```java
public List<RecordedGrip> retrieveSection(String sectionName) {
    try {
        FileInputStream stream = new FileInputStream(sectionName);
        stream.close();
    } catch (FileNotFoundException e) {
        throw new StorageException("retrieval error", e);
    }
    return new ArrayList<RecordedGrip>();
}
```

现在我们已经用`try-catch`结构定义了范围，就可以使用TDD来构建我们需要的其余逻辑。该逻辑将被添加到`FileInputStream`的创建和`close`之间，并且可以假装一切正常。

尝试编写能够强制抛出异常的测试，然后向你的处理程序添加行为以满足这些测试。这将促使你先构建`try`块的事务范围，并帮助你维护该范围的事务性质。

## 使用非受检异常

争论已经结束。多年来，Java程序员一直在争论受检异常的利弊。当受检异常在Java的第一个版本中引入时，它们似乎是一个伟大的想法。每个方法的签名都会列出它可能传递给调用者的所有异常。此外，这些异常是方法类型的一部分。如果你的签名与代码所能做的不匹配，你的代码根本无法编译。

当时，我们认为受检异常是一个伟大的想法；是的，它们可以带来*某些*好处。然而，现在很明显，它们对于生产健壮的软件并不是必需的。C#没有受检异常，尽管进行了勇敢的尝试，C++也没有。Python和Ruby也没有。然而，用所有这些语言编写健壮的软件是可能的。既然如此，我们必须真正决定——受检异常是否值得付出代价。

代价是什么？受检异常的代价是违反开闭原则¹。如果你在代码中的一个方法中抛出受检异常，而catch在其上三层，*你必须在从你到catch之间的每个方法的签名中声明该异常*。这意味着软件低层的更改可能会迫使许多更高层级更改签名。即使被更改的模块并不关心这些变化，它们也必须被重新构建和重新部署。

考虑一个大型系统的调用层次结构。顶层的函数调用它们下面的函数，这些函数又调用更下面的函数，如此无限循环。现在假设某个最底层的函数被修改为必须抛出一个异常。如果该异常是受检的，那么函数签名必须添加一个`throws`子句。但这意味着每个调用我们修改过的函数的函数也必须被修改：要么捕获新异常，要么在其签名中附加相应的`throws`子句。如此无限循环。最终结果是，更改从软件的最底层级逐级传递到最高层级！封装被打破了，因为所有在抛出路径上的函数都必须了解那个低层异常的细节。鉴于异常的目的是让你能够远距离处理错误，受检异常以这种方式破坏封装实在遗憾。

如果你正在编写一个关键库，受检异常有时是有用的：你必须捕获它们。但在一般的应用程序开发中，依赖成本超过了收益。

## 为异常提供上下文

你抛出的每个异常都应提供足够的上下文，以确定错误的来源和位置。在Java中，你可以从任何异常中获取堆栈跟踪；然而，堆栈跟踪无法告诉你失败操作的意图。

创建信息丰富的错误消息，并将它们与异常一起传递。提及失败的操作和失败的类型。如果你在应用程序中记录日志，请传递足够的信息，以便在你的`catch`中记录错误。

## 根据调用者的需求定义异常类

对错误进行分类的方法有很多。我们可以按来源分类：它们来自哪个组件？或者按类型分类：它们是设备故障、网络故障还是编程错误？然而，当我们在应用程序中定义异常类时，我们最关心的问题应该是*它们如何被捕获*。

让我们看一个异常分类不佳的例子。下面是一个针对第三方库调用的`try-catch-finally`语句。它涵盖了调用可能抛出的所有异常：

```java
ACMEPort port = new ACMEPort(12);

try {
    port.open();
} catch (DeviceResponseException e) {
    reportPortError(e);
    logger.log("Device response exception", e);
} catch (ATM1212UnlockedException e) {
    reportPortError(e);
    logger.log("Unlock exception", e);
} catch (GMXError e) {
    reportPortError(e);
    logger.log("Device response exception");
} finally {
    ...
}
```

该语句包含大量重复代码，我们不应感到惊讶。在大多数异常处理情况下，无论实际原因是什么，我们所做的工作都相对标准。我们必须记录错误，并确保我们能够继续。
