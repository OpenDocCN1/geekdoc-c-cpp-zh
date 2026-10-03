
// Excel Excel 对象模型定义的相关对象；// excelApp.Workbooks.Add();

`Workbook excelWB = // Factory`

```
```

> 实例化 COM 对象的语法与创建托管 C# 对象的语法无法区分

## 核心要点

使用互操作程序集创建一个 RCW，通过它实例化并控制 COM 对象的生命周期。你可以像调用普通托管对象的方法一样，通过 RCW 调用 COM 对象的方法。RCW 隐藏了该对象是 COM 对象的事实，并对方法参数和返回值进行封送。

### 创建 COM 对象

互操作程序集包含了 COM 组件类型库中定义的每个 COM 接口的托管版本。COM 类型库还定义了一个或多个类（称为 `coclasses`），应用程序可以实例化这些类，并实现一个或多个 COM 接口。互操作程序集为每个 `coclass` 定义了一个托管封装器，并赋予该封装器与 `coclass` 相同的名称，但添加了 `Class` 后缀。互操作程序集还包含每个 COM 接口的托管版本。你通过创建该托管 `coclass` 的实例来创建 COM 对象，但通过适当的托管接口来引用该类。

## 将 Visual C# 代码与动态语言及 COM 组件集成 15-27

在典型的 COM 组件中，单个 `coclass` 可能作为组件所实现的对象模型的入口。在这种情况下，`coclass` 通常提供工厂方法，用于创建实现类型库提供的其他 COM 接口的其他类型的对象。你通过 RCW 使用这些工厂方法来实例化围绕这些类型的托管封装器。

例如，微软为 Microsoft Excel® 提供的 COM 库定义了一个名为 `ApplicationClass` 的 `coclass`，它作为 Office Excel 对象模型的入口。它还定义了该 `coclass` 实现的相应 COM 接口的托管封装器，称为 `Application`。你通过与 COM 接口关联的托管封装器通过 RCW 实例化 COM 类型。例如，要启动 Excel 运行，你创建一个 `Application` 对象的新实例。

> **注意：** 要实例化 COM 对象，请始终使用 `coclass` 实现的接口的托管封装器，而不是 `coclass` 本身的托管版本。

## 在 COM 对象上调用方法

### 可选参数

| Visual C# 4.0 | `excelChart excelChart = ...; excelChart.ChartWizard(dataRange, Excel.X1ChartType.xlLine, Type.Missing, Excel.X1RowCol.xl1Columns, 1, 1, Type.Missing, Speed versus Distance, "Distance", Type.Missing);` |
| :--- | :--- |
| Visual C# 4.0 | `excelChart excelChart = ...; excelChart.ChartWizard(Title: "Speed versus Distance", Source:dataRange, Gallery:Excel.X1ChartType.xlLine, PlotBy:Excel.X1RowCol.xl1Columns, CategoryLabels: 1, SeriesLabels: 1, ValueTitle: "Distance", CategoryTitle: "Speed");` |

### 动态类型与 COM 绑定器

| Visual C# 4.0 | `excel.Range range = (Excel.Range)excel.Cells[5, 10];` |
| :--- | :--- |
| Visual C# 4.0 | `excel.Range range = excel.Cells[5, 10];` |

## 关键点

创建 COM 对象后，你可以通过运行时可调用包装器（RCW）与其进行交互，调用其方法并设置其属性。COM 对象上可用的方法和属性使用与访问 Visual C# 对象时相同的语法。RCW 在你的 Visual C# 代码和 COM 对象之间进行数据封送。

## 处理可选参数

如果你检查了许多执行 COM 互操作的 Visual C# 应用程序，你可能会看到某些方法将 `Type.Missing` 值作为一个或多个参数进行传递。许多 COM 组件是用 C++ 等语言编写的，这些语言支持可选参数。在 Visual C# 4.0 之前，你必须为 COM 方法指定的每个参数提供参数，即使你想省略该参数并使用 COM 组件定义的默认值。解决办法是指定值为 `Type.Missing` 的值，这会导致 RCW 在调用 COM 组件时省略该参数，从而让 COM 组件使用默认值。

C# 4.0 通过支持具名参数和可选参数规避了这个问题。RCW 现在将 COM 方法的所有可选参数定义为具有默认值 `Type.Missing` 的 C# 可选参数。现在，当你调用 COM 组件的方法时，可以按名称指定参数，并省略任何你想保持为默认值的参数。该语法与调用实现默认参数值的 C# 方法的语法相同。

例如，Office 对象模型中 `Chart` 类型的 `ChartWizard` 方法接收了大量参数，所有这些参数都有默认值。在 Visual C# 4.0 之前，当使用任何一个默认值时，你必须使用类似于下面代码示例的代码。

```csharp
Excel.Chart excelChart = ...;
excelChart.ChartWizard(dataRange, Excel.X1ChartType.xlLine,
Type.Missing, Excel.X1RowCol.xlColumns,
1, 1, Type.Missing,
"Speed versus Distance",
"Speed", "Distance", Type.Missing);
```

在 C# 4.0 中，你可以使用具名参数。RCW 为 `ChartWizard` 方法实现了默认参数值（将它们设置为 `Type.Missing`）。你省略的任何参数都会作为缺失值传递到 Office Excel COM 库，并获得它们的默认值，如下代码示例所示。

```csharp
Excel.Chart excelChart = ...;
excelChart.ChartWizard(Title: "Speed versus Distance",
Source: dataRange,
Gallery: Excel.X1ChartType.xlLine,
PlotBy: Excel.X1RowCol.xlColumns,
CategoryLabels: 1, SeriesLabels: 1,
ValueTitle: "Distance",
CategoryTitle: "Speed");
```

具名参数的额外优势是使你的代码更易理解和维护。

## 避免强制转换

你可能在旧版 C# 应用程序中注意另一个特性是使用强制转换来转换许多 COM 方法的类型。在 C# 4.0 之前，所有 COM 对象都作为对象类型引用。为 C# 4.0 生成的 RCW 将对象引用作为 `dynamic` 返回。这使得运行时可以在应用程序运行时动态确定类型。例如，在 Office Excel 对象模型中，`Worksheet` 通过 `Cells` 属性暴露工作表中的单元格。你可以创建一个由一组连续单元格组成的 Office Excel `Range` 对象。在 Visual C# 4.0 之前，你必须使用类似于示例的代码。查询 `Cells` 属性返回的集合是一个对象，你必须将其转换为 `Range` 对象才能将其存储在 `Range` 引用中。

```csharp
Excel.Range range = (Excel.Range)excel.Cells[5, 10];
```

在 C# 4.0 中，查询 `Cells` 属性返回的值现在是 `dynamic` 的，运行时不需要强制转换即可确定正确的类型，如下代码示例所示。

```csharp
Excel.Range range = excel.Cells[5, 10]; // 不需要强制转换
```

**问题：** 如果你省略了 COM 方法的参数，RCW 使用什么值作为默认值？

## 扩展阅读

## 在 COM 方法调用中处理异常

当你调用 COM 对象中的方法时，它会返回一个 `HRESULT` 值来报告错误。`S_OK` 值表示方法成功。任何其他值都表示错误，且值本身指定了错误原因。RCW 不会将 `HRESULT` 值作为返回值传回托管客户端应用程序。RCW 不返回任何值，或者返回所有成功的值。

如果 COM 方法尝试传回一个除 `S_OK` 以外的 `HRESULT`，CLR 将触发并抛出托管异常。CLR 会自动将已知的 `HRESULT` 值映射到等效托管异常。例如，`HRESULT E_NULLREFERENCE` 会导致 CLR 抛出 `NullReferenceException`。你可以在 Visual Studio 2005 文档找到完整的 `HRESULT` 映射列表。

如果方法返回无法识别的 `HRESULT` 值，CLR 将抛出 `COMException`。COM 方法返回的 `HRESULT` 值可以在 COM 对象的 `ErrorCode` 属性中可用。此外，如果 COM 对象支持 `IErrorInfo` 接口，COM 对象的 `Message` 属性将由 `IErrorInfo.GetDescription` 方法返回的字符串填充，`Source` 属性由 `IErrorInfo.GetSource` 方法填充，`HelpLink` 属性包含 `IErrorInfo.GetHelpFile` 和 `IErrorInfo.GetContext` 方法返回的信息。

## 无需主程序集的部署

- .NET Framework 4 支持无 PIA 部署：
- 将引用的互操作类型直接嵌入程序集中
- 未被引用的 PIA 类型将被省略
- 无需随应用程序部署 PIA
- 在 Visual Studio 程序集属性中将 `Embed Interop Types` 设置为 `true`

![](img/3ef84844c6ac82b838fffa6448b2346_445_0.png)

## 关键点

大型 COM 库和组件的 PIA 可能定义大量的类型和方法。因此，在 .NET Framework 4 之前，你必须确保安装应用程序的每台计算机都正确部署了应用程序使用的每个 PIA。部署 PIA 需要管理员权限。

.NET Framework 4 现在支持智能无 PIA 部署。当你在设计运行时将 PIA 添加到应用程序时，该 PIA 会暴露名为 `Embed Interop Types` 的属性。如果你将此属性设置为 `true`，当你生成应用程序时，应用程序使用的 PIA 互操作类型将编译到你的程序集中。因此，你不需要随应用程序部署 PIA。此外，你的程序集将仅包含应用程序使用的 PIA 类型；任何未引用的类型都将被省略。这确保了程序集的大小保持尽可能小。

**问题：** 如果你指定了无 PIA 部署，当你部署使用 COM 组件的应用程序时，是否仍然需要部署该 COM 组件？

## 实验：将 Visual C# 代码与动态语言及 COM 组件集成

- 练习 1：将使用动态语言编写的代码集成到 Visual C# 应用程序中
- 练习 2：在 Visual C# 应用程序中使用 COM 组件

### 登录信息

| 虚拟机 | 10266A-GEN-DEV |
| :--- | :--- |
| 用户名 | Student |
| 密码 | Pa$$wrd |

预计耗时：60 分钟

## 目标

完成本实验后，你将能够：

- 实例化使用动态语言定义的对象，并从 Visual C# 应用程序中调用其方法。
- 实例化 COM 组件并在 Visual C# 应用程序中调用其方法。

## 介绍

在本实验中，你将使用 DLR（动态语言运行时）从 Visual C# 应用程序访问在 IronRuby 或 IronPython 脚本中定义的对象。你还将使用 COM 互操作性在 Visual C# 应用程序中实例化并使用 COM 组件。

## 实验设置

对于本实验，你将使用可用的虚拟机环境。在开始实验之前，你必须：

- 启动 10266A-GEN-DEV 虚拟机，然后使用以下凭据登录：
  - 用户名：Student
  - 密码：Pa$$w0rd

## 实验场景

![](img/3ef84844c6ac82b838cfffa6448b2346_449_0.png)

Fabrikam, Inc. 使用 Visual C# 以外的技术和编程语言来驱动其开发的某些设备。此外，Fabrikam, Inc. 将 Microsoft Office 等软件产品的功能整合到某些应用程序中。你被要求将使用这些技术编写的一些组件集成到支持各种设备的 Visual C# 软件中。

## 练习 1：将使用动态语言编写的代码集成到 Visual C# 应用程序中

### 场景

Fabrikam, Inc. 拥有大量的 Python 和 Ruby 脚本，其中包含了经过验证和彻底测试的代码。尽管 Visual C# 现在是 Fabrikam, Inc. 的首选开发语言，但使用 Visual C# 重新实现并完全测试这些脚本将既昂贵又耗时。相反，你被要求将这些脚本提供的功能直接集成到你的 Visual C# 应用程序中。

你将使用 DLR 调用一个 IronRuby 脚本和一个 IronPython 脚本（提供了两种语言的脚本），使用这些脚本中定义的类型创建对象，并调用这些对象暴露的方法。

此练习的主要任务如下：

1. 检查 Python 和 Ruby 代码。
2. 打开启动项目。
3. 创建一个 Python 对象并调用 Python 方法。
4. 测试 Python 代码。
5. 创建一个 Ruby 对象并调用 Ruby 方法。
6. 测试 Ruby 代码。

### 任务 1：检查 Python 和 Ruby 代码

1. 使用用户 Student 和密码 PassSword 登录 10266A-GEN-DEV 虚拟机。
2. 打开 Visual Studio 2010。
3. 使用记事本打开 `E:\Labfiles\Lab 15\Python` 文件夹下的 `Shuffler.py` 文件。
4. 在记事本中检查 Python 代码。

   `Shuffler.py` 文件包含一个名为 `Shuffler` 的 Python 类，该类提供了一个名为 `Shuffle` 的方法。`Shuffle` 方法接受一个名为 `data` 的参数，该参数包含项目集合。`Shuffle` 方法实现了 Fisher-Yates-Durenfeld 算法来随机洗牌 `data` 中的项目。

   Python 类还暴露了一个名为 `CreateShuffler` 的函数，用于创建 `Shuffler` 类的新实例。你将从 Visual C# 中使用此方法创建一个 `Shuffler` 对象。

5. 关闭记事本。
6. 使用记事本打开 `E:\Labfiles\Lab 15\Ruby` 文件夹下的 `Trapezoid.rb` 文件。
7. 在记事本中检查 Ruby 代码。

   `Trapezoid.rb` 文件包含一个名为 `Trapezoid` 的 Ruby 类，该类模拟了简单的四边形。构造函数接受左下角、底边长度和高度。

   > **注意：** `Trapezoid` 类模拟了可能的四边形。
   > **注意：** `to_s` 方法返回四边形的字符串表示。
   > **注意：** DLR 绑定器将对 `to_s` 方法的调用转换为 .NET Framework 的调用。

   `area` 方法计算四边形的面积。

   Ruby 文件还提供了一个 `CreateTrapezoid` 函数，创建 `Trapezoid` 类的新实例。

8. 关闭记事本。

### 任务 2：打开启动项目

- 打开 `E:\Labfiles\Lab 15\Starter\DynamicInterop` 文件夹下的 `DynamicInterop` 解决方案。

### 任务 3：创建一个 Python 对象并调用 Python 方法

1. 检查 `InterTestWindow.xml` 文件。

   该窗口包含两个标签：Python Test 和 Ruby Test。

   Python Test 标签允许你将值放入 Data 框并指定它是文本还是数值。当你点击 Shuffle 时，数据会被封装并传递给 `Shuffle` 方法。`Shuffle` 方法在 WPF 窗口中显示洗牌后的数据。

2. 添加下表所示程序集的引用。

| 程序集 | 路径 |
| :--- | :--- |
| IronPython | `C:\Program Files\IronPython 2.6 for .NET 4.0` |
| IronPython.Modules | `C:\Program Files\IronPython 2.6 for .NET 4.0` |
| Microsoft.Dynamic | `C:\Program Files\IronPython 2.6 for .NET 4.0` |
| Microsoft.Scripting | `C:\Program Files\IronPython 2.6 for .NET 4.0` |

3. 审查任务。
4. 在 `InterTestWindow` 文件中找到 `TODO：添加包含 IronPython 和 Microsoft.Scripting 的命名空间`。
5. 在代码后台，添加 `using` 语句将 `IronPython.Hosting` 和 `Microsoft.Scripting` 引入作用域。
6. 检查 `pythonPath` 和 `pythonCode` 字符串。`pythonPath` 指定 Python 库安装目录。`pythonCode` 指定脚本的名称和位置。
7. 在 `shuffle_Click` 方法中找到 `TODO：使用脚本中的 CreateShuffler 方法创建 Shuffler 类实例`。
8. 在 TODO 注释后，添加代码执行以下任务：

   a. 使用 `Python` 类的静态方法 `CreateEngine` 创建一个 `pythonEngine` 对象。
