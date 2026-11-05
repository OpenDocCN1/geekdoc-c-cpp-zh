
然后你需要确保已为代码添加了良好的注释。你需要在创建新方法或逻辑不明显的代码行时尽快养成这个习惯。反过来，代码中注释过多也并非好主意。那么什么时候应该注释，什么时候不应该？一个很好的经验法则是，仅当代码背后的逻辑不明显时才注释代码。

在以下代码清单中，第一个清单（代码清单 43）中的逻辑很明显，因此实际上不需要注释。然而，在代码清单 44 中，应通过注释解释取模运算符的使用，因为这样做的原因并不明显。

```csharp
//Bad comment: Calculate the available quantity
int QtyAvailable = MaxBinQuantity - CurrentBinQuantity;
```

*代码清单 43：不必要的代码注释*

```csharp
//Good comment: Use modulus to determine if the factor produces any scrap
return volumeToCut % factor;
```

*代码清单 44：注释清楚地解释了逻辑*

注释良好的方法可能如下所示。

```csharp
/// <summary>
/// Calculate any remainder after the modulus operation between volume
and factor
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

*代码清单 45：注释良好的方法*

添加相关注释后，你需要生成解决方案。你需要注意在生成文档文件期间生成过程中可能收到的任何警告。这些警告通常与源代码中缺少 XML 注释有关。最好继续通过向方法和属性添加清晰且相关的代码注释来修复这些问题。

生成完成后，你的 XML 文档将位于配置生成设置时指定的路径中。在此示例中，生成的 XML 文档包含代码契约描述。

```xml
<?xml version="1.0"?>
<doc>
    <assembly>
        <name>CodeContractsDemo</name>
    </assembly>
    <members>
        <member name="T:ERPWarehouseIntegration">
            <summary>
                ERP Warehouse Integration class to manage the cutting of steel volume and available bin quantities
            </summary>
        </member>
        <member name="P:ERPWarehouseIntegration.MaxBinQuantity">
            <summary>
                The maximum bin quantity for bins
            </summary>
        </member>
        <member name="P:ERPWarehouseIntegration.CurrentBinQuantity">
            <summary>
                The current bin quantity available
            </summary>
        </member>
        <member name="M:ERPWarehouseIntegration.ProductionVolumePerBin(System.Int32,System.Int32)">
            <summary>
                Calculate the production volume of steel per bin
            </summary>
            <param name="binVolume" />
            <param name="factor" />
            <returns>Bin Volume less Remainder</returns>
            <ensures description="The factor used will result in scrap. Please modify the cutting factor." csharp="result == binVolume" vb="result = binVolume">result == binVolume</ensures>
        </member>
        <member name="M:ERPWarehouseIntegration.CutSteel(System.Int32,System.Int32)">
            <summary>
                Calculate any remainder after the modulus operation between volume and factor
            </summary>
            <param name="volumeToCut" />
            <param name="factor" />
            <returns>Remainder after cutting</returns>
        </member>
        <member name="M:ERPWarehouseIntegration.BinQtyAvailable">
            <summary>
                Ensure that a non-negative value is returned for available bin quantity
            </summary>
            <returns>Available bin quantity</returns>
            <ensures csharp="result &gt;= 0" vb="result &gt;= 0">result &gt;= 0</ensures>
        </member>
        <member name="M:ERPWarehouseIntegration.EnsureAllBinsFilled(System.Int32@,System.Int32,System.Int32)">
            <summary>
                Ensure that all bins are filled and that the steel volume does not exceed the maximum bin volume
            </summary>
            <param name="binOverCount" />
            <param name="binVol" />
            <param name="steelVol" />
            <ensures description="The steel volume exceeds the bin volume" csharp="binOverCount == 0" vb="binOverCount = 0">binOverCount == 0</ensures>
        </member>
    </members>
</doc>
```

代码清单 46：生成的 XML 文档文件

我们轻松地为代码生成了简洁的 XML 文档，而无需任何繁重工作。如果你定期注释代码，生成的文档将保持最新，并真实反映代码的状态。

## 创建用户友好的文档

生成的 XML 文件很好，但还需要另一步来创建格式良好、人类可读的 HTML 类型文档。为此，我将使用 Sandcastle Help File Builder，你可以从 GitHub 的 github.com/EWSoftware/SHFB 下载。在引导安装过程中，请务必阅读每个屏幕的说明和注释，因为它们包含你需要注意的重要信息。

我建议阅读更多关于使用 Sandcastle Help File Builder 的教程。这个工具提供了如此多的功能，以至于需要真正深入了解这个出色的工具。然而，就本书而言，除了向你展示如何创建基本的 .chm 帮助文件之外，我不会进一步详述。

在使用 Sandcastle Help File Builder 之前，你必须确保项目具有命名空间。否则，你将在帮助文件生成时看到以下错误。

![](img/0a07386735fd4e6427d20aa9bc165f5d_50_0.png)

*图 36：生成输出错误*

```csharp
SHFB: Error BE0033: No APIs found to document. See error topic in
help file for details.
    at SandcastleBuilder.Utils.BuildEngine.BuildProcess.Build()
```

*代码清单 47：Sandcastle Help File Builder 错误*

我只需为类添加一个命名空间，如代码清单 48 所示。

```csharp
namespace CodeContractsDemoProject
{
    /// <summary>
    /// ERP Warehouse Integration class to manage the cutting of steel
    /// volume and available bin quantities
    /// </summary>
    public class ERPWarehouseIntegration
    {
```

*代码清单 48：为类添加了命名空间*

完成此操作后，如果 **Sandcastle Help File Builder** 尚未打开，请打开它。在 **项目资源管理器** 中，右键单击 **文档源** 节点，并添加项目生成到的 .dll 或 .exe（通常是 bin 文件夹）。我选择将 XML 文档输出到我的 bin 文件夹。

![](img/0a07386735fd4e6427d20aa9bc165f5d_51_0.png)

*图 37：项目 bin 文件夹*

选择 .exe 文件后，Sandcastle Help File Builder 也会自动拾取 XML 文档文件并将其添加为文档源。添加的文件将显示在 **项目资源管理器** 的 **文档源** 节点下。

![](img/0a07386735fd4e6427d20aa9bc165f5d_51_1.png)

*图 38：文档源和摘要*

**项目属性** 选项卡中还有其他多个部分可供修改和设置。需要记住配置的一个重要部分是 **摘要** 部分。你需要确保已在 **项目属性** 选项卡的 **摘要** 页面中添加命名空间摘要注释。单击 **编辑命名空间摘要** 按钮以打开 **命名空间摘要** 窗口。

![](img/0a07386735fd4e6427d20aa9bc165f5d_52_0.png)

*图 39：命名空间摘要窗口*

选择要为其添加摘要的命名空间，并在 **编辑所选命名空间的摘要** 文本框中输入摘要说明。完成后，单击 **关闭** 按钮并保存项目。

现在，你已准备好生成 Sandcastle Help File Builder 项目，它将按你的指定生成帮助文件。

支持的帮助文件格式类型：

- HTML 帮助 1 (chm)
- MS Help Viewer (mshc)
- Open XML (docx)
- Markdown (md)
- 网站 (HTML/ASP.NET)

