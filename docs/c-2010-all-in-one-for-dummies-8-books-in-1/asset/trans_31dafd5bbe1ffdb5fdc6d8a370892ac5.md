

## 426 使用 System.DataNamespace

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_451_0.png)

**图 2-9:** 表格选项下拉列表。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_451_1.png)

**图 2-10:** 创建部件详细数据表单。

注意，每个字段都获得了一个智能标签（SmartTag），它允许你为文本框中的值指定查询。你还可以通过更改数据源（Data Sources）面板中的值来预设使用的控件（参考图 2-10）。

此外，页面顶部添加了一个 VCR 栏（技术上称为 BindingNavigator）。当你运行应用程序时，可以使用 VCR 栏在表格记录之间循环切换。

最后，在页面底部的组件托盘（Component Tray）中了四个四个代码对象：DataSet、BindingSource、DataAdapter 和 BindingNavigator 对象。

## 使用 System.DataNamespace 427

点击播放按钮，你可以看到 VCR 栏的工作。你可以无问题地遍历数据库中的项目，如图 2-11 所示。这与在 Access 或 FoxPro 中工作非常相似，但具有企业级的质量！

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_452_0.png)

图 2-11: 运行示例。

更棒的是，按照以下步骤创建一个子表界面：

- 1. 点击表格旁边的加号 (+)，在数据源面板中打开 Part 表。
- 2. 向下滚动，直到看到嵌套在 Orders 表中的 PartFaultsPart 表。
- 注意，该表出现了两次。你需要 Parts 下方的那个。
- 3. 将该表的实例拖到表单上，并放置在在本节早些时候表单上放置的 Parts 字段下方（参考图 2-10）。
- 4. 点击播放按钮运行示例，如图 2-12 所示。

你拥有了一个运行良好且易于使用的父/子表单，包含了部件和部件故障。在其他环境中，创建此表单需要你编写数百行代码。凭借 C# 提供的为数据源选择程序的能力，该表单几乎达到了企业级就绪。这非常顺滑。

## 428 使用 System.DataNamespace

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_453_0.png)

图 2-12: 一个完整的编辑表单。

## 编写数据代码

然而，在大多数企业开发环境中，你不会使用可视化工具来构建数据访问软件。通常，已经存在一套基础架构。

这是因为企业软件通常有特定的需求，管理这些规范的最简单方法是使用独特且自定义的代码。简而言之，某些组织不希望按照微软的方式完成工作。

## 可视化工具的输出

企业环境之所以不使用可视化工具，是因为它们输出的代码相当复杂。如果你切换到代码视图（Code View），右键点击对象实例（例如 PartsTableAdapter 对象）并选择“转到定义”，你将看到设计器背后的代码。

图 2-13 显示了你到达那里时看到的内容。代码窗口顶部附近的区域被标记为 Windows Form 设计器生成的代码，你禁禁注意到该部分之前的行号在二十多，而之后的行号在四百多。那是大量的生成的代码。

这段代码没有问题，但它是刻意设计成通用的，以支持任何人可能对其执行的任何操作。企业客户通常希望确保所有工作都以相同的方式完成。由于这个原因，他们经常定义一种特定的数据代码格式，并期望他们的软件人员使用它，而不是可视化工具。

## 使用 System.Data Namespace 429

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_454_0.png)

图 2-13: 生成的代码。DataSets 如何

## 基础数据代码

示例项目的代码很简单：

```csharp
using:
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
```

```csharp
namespace Accessing_Data
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void partsBindingNavigatorsSaveItem(object sender, EventArgs e)
        {
            this.Validate();
            this.partsBindingSource.EndEdit();
            this.tableDataAdapter.UpdateAll(this.assets_MaintenanceDataSet);
        }
    }
}
```

第三卷
第2章 访问数据

## 430 使用 System.Data Namespace

```csharp
private void Form_Load(object sender, EventArgs e)
{
    // 此部分在 OCR 中似乎是碎片化的，
    // 但根据所提供的文本逻辑进行推断。
}
```

