
```csharp
    /// <summary>
    /// Fill the bin with the volume of steel
    /// </summary>
    /// <param name="steelVolume"></param>
    public void FillBin(int steelVolume)
    {
        Contract.Requires(steelVolume > 0);
        Contract.Ensures(steelVolume <= this.MaxVolume);
    }

    /// <summary>
    /// Empty the bin of all steel contained
    /// </summary>
    /// <param name="steelVolume"></param>
    /// <returns></returns>
    public bool PurgeBin(int steelVolume)
    {
        Contract.Requires(steelVolume > 0);
        Contract.Ensures(steelVolume <= this.MaxVolume);
        Contract.Ensures(Contract.Result<bool>() == true);

        // Purge bin and return successful result
        return true;
    }

    /// <summary>
    /// Perform a partial bin fill
    /// </summary>
    /// <param name="steelVolume"></param>
    /// <returns></returns>
    public bool FillBinPartially(int steelVolume)
    {
        Contract.Requires(steelVolume > 0);
        Contract.Ensures(steelVolume < this.MaxVolume);
        Contract.Ensures(Contract.Result<bool>() == true);

        return true;
    }
}
```

*代码清单 59：重复的契约*

现在我们可以利用 **Abbreviator** 方法来简化代码，并在多个方法中引用它们。使用 **Abbreviator** 方法后，代码可以重构如下。

```csharp
public class AbbreviatorDemo
{
    /// <summary>
    /// The factor for the cutting volume
    /// </summary>
    public int Factor { get; private set; }

    /// <summary>
    /// The maximum volume a bin can contain
    /// </summary>
    public int MaxVolume { get; private set; }

    /// <summary>
    /// Fill the bin with the volume of steel
    /// </summary>
    /// <param name="steelVolume"></param>
    public void FillBin(int steelVolume)
    {
        ValidSteelAndMaxVolume(steelVolume);
    }

    /// <summary>
    /// Empty the bin of all steel contained
    /// </summary>
    /// <param name="steelVolume"></param>
    /// <returns></returns>
    public bool PurgeBin(int steelVolume)
    {
        ValidSteelAndMaxVolume(steelVolume);
        EnsurePositiveResult();

        // Purge bin and return successful result
        return true;
    }

    /// <summary>
    /// Perform a partial bin fill
    /// </summary>
    /// <param name="steelVolume"></param>
    /// <returns></returns>
    public bool FillBinPartially(int steelVolume)
    {
        ValidSteelAndMaxVolume(steelVolume);
        EnsurePositiveResult();

        return true;
    }

    /// <summary>
    /// Abbreviator method for steel and max volume
    /// </summary>
    /// <param name="steelVolume"></param>
    [ContractAbbreviator]
    private void ValidSteelAndMaxVolume(int steelVolume)
    {
        Contract.Requires(steelVolume > 0);
        Contract.Ensures(steelVolume <= this.MaxVolume);
    }

    /// <summary>
    /// Abbreviator method for successful result
    /// </summary>
    [ContractAbbreviator]
    private void EnsurePositiveResult()
    {
        Contract.Ensures(Contract.Result<bool>() == true);
    }
}
```

*代码清单 60：使用 Abbreviator 方法*

我添加了两个新方法 ValidSteelAndMaxVolume 和 EnsurePositiveResult，并为它们添加了 [ContractAbbreviator] 特性。这使我能够减少方法中重复的代码契约集合。当查看受契约约束的方法时，这样更易于阅读，功能也更清晰。另一点需要记住的是，如果需要，Abbreviator 方法可以包含对其他 Abbreviator 方法的调用。

## 第 4 章 测试代码契约

### Pex 演变为 IntelliTest

你们中的许多人可能熟悉 Pex，而 Pex 已经演变为 IntelliTest，这大概不会令你感到意外。IntelliTest 是 Visual Studio Enterprise 2015 中的一项集成功能。代码契约与 IntelliTest 集成良好，并且开始使用 IntelliTest 非常容易。

### 入门：创建 IntelliTest

如前所述，IntelliTest 已集成到 Visual Studio Enterprise 2015 中。如果你希望在其他版本的 Visual Studio 2015 中集成 IntelliTest，可以在 Visual Studio 2015 UserVoice 网站上发出你的声音。Microsoft 中 Visual Studio 团队的人员确实会密切关注这个网站——你的投票绝不会白费。

开始使用 IntelliTest 非常简单。让我们回顾一下上一章中处理过的一个方法。

```csharp
/// <summary>
/// Calculate the production volume of steel per bin
/// </summary>
/// <param name="binVolume"></param>
/// <param name="factor"></param>
/// <returns>Bin Volume less Remainder</returns>
public int ProductionVolumePerBin(int binVolume, int factor)
{
    Contract.Ensures(Contract.Result<int>() == binVolume, "The factor used will result in scrap. Please modify the cutting factor.");

    int remainder = CutSteel(binVolume, factor);
    return binVolume - remainder;
}

/// <summary>
/// Calculate any remainder after the modulus operation between volume and factor
/// </summary>
/// <param name="volumeToCut"></param>
/// <param name="factor"></param>
/// <returns>Remainder after cutting</returns>
private int CutSteel(int volumeToCut, int factor)
{
    // Use modulus to determine if the factor produces any scrap
    return volumeToCut % factor;
}
```

*代码清单 61：为方法创建 IntelliTest*

和之前一样，前面的代码清单告诉调用方法：受契约约束的方法将导致切割体积始终等于料箱体积。这意味着所有钢材都已被完美切割，使用特定因子不会产生边角料。

要为 ProductionVolumePerBin() 方法生成新的 IntelliTest，请右键单击该方法，并从上下文菜单中选择“创建 IntelliTest”。

![](img/0a07386735fd4e6427d20aa9bc165f5d_69_0.png)

*图 45：创建 IntelliTest*

Visual Studio 现在将显示“创建 IntelliTest”窗口，你可以在其中为生成的 IntelliTest 配置附加设置。

![](img/0a07386735fd4e6427d20aa9bc165f5d_70_0.png)

*图 46：创建 IntelliTest 设置*

如果你是第一次创建 IntelliTest，你会看到 **MSTest** 是 **测试框架** 下列出的唯一选项。不过，如果需要，你也可以安装第三方单元测试框架（稍后会详细介绍）。完成后，单击 **确定**。

![](img/0a07386735fd4e6427d20aa9bc165f5d_70_1.png)

*图 47：测试项目已添加到解决方案*

Visual Studio 现在将为你创建测试项目。完成该过程后，新项目将显示在“解决方案资源管理器”窗口中。

![](img/0a07386735fd4e6427d20aa9bc165f5d_71_0.png)

*图 48：已创建 IntelliTest*

展开 ERPWarehouseIntegrationTest.cs 文件，你会看到已创建一个名为 ProductionVolumePerBinTest 的测试。

```csharp
// <copyright file="ERPWarehouseIntegrationTest.cs">Copyright © 2015</copyright>
using System;
using Microsoft.Pex.Framework;
using Microsoft.Pex.Framework.Validation;
using Microsoft.VisualStudio.TestTools.UnitTesting;

namespace CodeContractsDemoProject.Tests
{
    /// <summary>This class contains parameterized unit tests for ERPWarehouseIntegration</summary>
    [PexClass(typeof(ERPWarehouseIntegration))]
    [PexAllowedExceptionFromTypeUnderTest(typeof(InvalidOperationException))]
    [PexAllowedExceptionFromTypeUnderTest(typeof(ArgumentException), AcceptExceptionSubtypes = true)]
    [TestClass]
    public partial class ERPWarehouseIntegrationTest
```

Visual Studio 将继续生成你的项目，然后启动 **IntelliTest 探索结果** 窗口。此窗口显示所有可能的方法参数，这些参数将导致被测方法获得最大的代码覆盖率。现在你可以概览该方法在测试中的表现。

![](img/0a07386735fd4e6427d20aa9bc165f5d_73_0.png)

*图 50：IntelliTest 探索结果*

我们可以立即看到三个测试失败，一个测试通过。在 **IntelliTest 探索结果** 窗口的右侧，**详细信息** 和 **堆栈跟踪** 显示在可折叠节点中。让我们更仔细地查看测试结果。

### 测试 2：通过

**ProductionVolumePerBin()** 方法必须始终使切割体积等于料箱体积。从测试 2 中使用的变量可以看出，它通过了，因为料箱体积为 **0**，并且该方法的结果也为 **0**。

```csharp
[TestMethod]
[PexGeneratedBy(typeof(ERPWarehouseIntegrationTest))]
public void ProductionVolumePerBinTest33()
{
    ERPWarehouseIntegration eRPWarehouseIntegration;
    int i;
    eRPWarehouseIntegration = new ERPWarehouseIntegration();
    i = this.ProductionVolumePerBinTest(eRPWarehouseIntegration, 0, 1);
}
```
