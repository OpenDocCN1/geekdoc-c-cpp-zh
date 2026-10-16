

and namespaces:

## CalculatorContract (Class Library)

Namespaces

System.Collections.Generic

## SimpleCalculator (Class Library)

References

CalculatorContract

System.Composition.AttributedModel

Namespaces

System

System.Collections.Generic

System.Composition

## AdvancedCalculator (Class Library)

References

CalculatorContract

System.Composition.AttributedModel

Namespaces

System

System.Collections.Generic

System.Composition

## SimpleHost (Console Application)

References

CalculatorContract

SimpleCalculator

System.Composition.AttributedModel

System.Composition.Hosting

System.Composition.Runtime

System.Composition.TypedParts

Namespaces

System

System.Collections.Generic

System.Composition

System.Composition.Hosting

static System.Console

在此示例中，创建了一个控制台应用程序（Package）来托管来自库的计算器部件。为了使主机与计算器部件保持独立，需要三个项目。其中一个项目 CalculatorContract 包含由插件程序集和托管可执行文件共同使用的契约。项目 simpleCalculator 包含部件并实现了由契约程序集定义的契约。主机使用契约程序集来调用部件。

程序集 CalculatorContract 中的契约由两个接口定义：ICalculator 和 IOperation。ICalculator 接口定义了 GetOperations 和 Operate 方法。GetOperations 方法返回插件计算器支持的所有操作列表，而通过 Operate 方法调用一个操作。此接口具有灵活性，因为计算器可以支持不同的操作。如果接口改为定义 Add 和 Subtract 方法而不是灵活的 Operate 方法，则需要新版本的接口来支持 Divide 和 Multiply 方法。然而，使用本示例中定义的 ICalculator 接口，计算器可以提供任意数量的操作和任意数量的操作数（代码文件 AttributeBasedSample/CalculatorContract/ICalculator.cs）：

```
public interface ICalculator
{
    IList<IOperation> GetOperations();
    double Operate(IOperation operation, double[] operands);
}
```

ICalculator 接口使用 IOperation 接口来返回操作列表并调用操作。IOperation 接口定义了只读属性 Name 和 NumberOperands（代码文件 AttributeBasedSample/CalculatorContract/IOperation.cs）：

```
public interface IOperation
{
    string Name { get; }
    int NumberOperands { get; }
}
```

CalculatorContract 程序集不需要引用 System.Composition 程序集。它仅包含简单的 .NET 接口。

插件程序集 simpleCalculator 包含实现了契约所定义接口的类。类 Operation 实现了接口 IOperation。此类仅包含接口所定义的两个属性。接口定义了属性的 get 访问器；内部 set 访问器用于在程序集内部设置属性（代码文件 AttributeBasedSample/SimpleCalculator/Operation.cs）：

```
public class Operation: IOperation
{
    public string Name { get; internal set; }
    public int NumberOperands { get; internal set; }
```

Calculator 类通过实现 ICalculator 接口提供了此插件的功能。Calculator 类作为部件导出，如 Export 属性所定义。此属性在 NuGet 包 System.Composition.AttributedModel 中的 System.Composition 命名空间中定义（代码文件 AttributeBasedSample/SimpleCalculator/Calculator.cs）：

```
[Export(typeof(ICalculator))]
public class Calculator: ICalculator
{
    public IList<IOperation> GetOperations() =>
        new List<IOperation>()
        {
            new Operation { Name="+", NumberOperands=2},
            new Operation { Name="-", NumberOperands=2},
            new Operation { Name="/", NumberOperands=2},
            new Operation { Name="*", NumberOperands=2}
        };

    public double Operate(IOperation operation, double[] operands)
    {
        double result = 0;
        switch (operation.Name)
        {
            case"+":
                result = operands[0] + operands[1];
                break;
            case"-":
                result = operands[0]-operands[1];
                break;
            case"/":
                result = operands[0] / operands[1];
                break;
            case"*":
                result = operands[0] * operands[1];
                break;
            default:
                throw new InvalidOperationException($"invalid operation {operation.Name}");
        }
        return result;
    }
}
```

托管应用程序是一个控制台应用程序（Package）。部件使用 Export 属性来定义导出的内容；对于托管应用程序，Import 属性定义了使用的内容。在这里，Import 属性标注了 Calculator 属性，该属性设置并获取实现 ICalculator 的对象。因此，任何实现此接口的计算器插件都可以在此处使用（代码文件 AttributeBasedSample/SimpleHost/Program.cs）：

```
class Program
{
    [Import]
    public ICalculator Calculator { get; set; }
    //etc.
}
```

在控制台应用程序的入口方法 Main 中，创建了 Program 类的新实例，然后调用 Bootstrapper 方法。在 Bootstrapper 方法中，创建了一个 ContainerConfiguration。使用 ContainerConfiguration，可以使用流畅 API 来配置此对象。方法 WithPart<Calculator> 查找 Calculator 类的导出，以便使其可从组合主机获得。CompositionHost 实例使用 ContainerConfiguration 的 CreateContainer 方法创建（代码文件 AttributeBasedSample/SimpleHost/Program.cs）：

```
public static void Main()
{
    var p = new Program();
    p.Bootstrapper();
    p.Run();
}

public void Bootstrapper()
{
    var configuration = new ContainerConfiguration()
        .WithPart<Calculator>();
    using (CompositionHost host = configuration.CreateContainer())
    {
        //etc.
    }
}
```

除了使用方法 WithPart（它也有重载和泛型版本以及非泛型版本）之外，你还可以使用 WithParts 添加部件列表，并使用 WithAssembly 或 WithAssemblies 添加程序集的导出。

使用 CompositionHost，你可以使用 GetExport 和 GetExports 方法访问导出的部件：

```
Calculator = host.GetExport<ICalculator>();
```

你也可以使用更“神奇”的方式。无需指定需要访问的所有导出类型，你可以使用 SatisfyImports 方法，它是 CompositionHost 的扩展方法。第一个参数需要一个具有导入的对象。由于 Program 类本身定义了一个带有 Import 属性的属性，因此可以将 Program 类的实例传递给 SatisfyImports 方法。调用 SatisfyImports 后，你会看到 Program 类的 Calculator 属性被填充（代码文件 AttributeBasedSample/SimpleHost/Program.cs）：

```
using (CompositionHost host = configuration.CreateContainer())
{
    host.SatisfyImports(this);
}
```

有了 Calculator 属性，你就可以使用接口 ICalculator 的方法。GetOperations 调用之前创建的插件的方法，返回四个操作。在询问用户应调用哪个操作并请求操作数值后，调用插件方法 Operate：

```
public void Run()
{
    var operations = Calculator.GetOperations();
    var operationsDict = new SortedList<string, IOperation>();
    foreach (var item in operations)
    {
        WriteLine($"Name: {item.Name}, number operands:" +
            $"{item.NumberOperands}");
        operationsDict.Add(item.Name, item);
    }
    WriteLine();
    string selectedOp = null;
    do
    {
        try
        {
            Write("Operation?");
            selectedOp =ReadLine();
            if (selectedOp.ToLower() =="exit" ||
                !operationsDict.ContainsKey(selectedOp))
                continue;
            var operation = operationsDict[selectedOp];
            double[] operands = new double[operation.NumberOperands];
            for (int i = 0; i < operation.NumberOperands; i++)
            {
                Write($"\t operand {i + 1}?");
                string selectedOperand = ReadLine();
                operands[i] = double.Parse(selectedOperand);
            }
            WriteLine("calling calculator");
            double result = Calculator.Operate(operation, operands);
            WriteLine($"result: {result}");
        }
        catch (FormatException ex)
        {
            WriteLine(ex.Message);
            WriteLine();
            continue;
        }
    } while (selectedOp !="exit");
}
```

应用程序一次示例运行的输出如下所示：

```
Name: +, number operands: 2
Name: -, number operands: 2
Name: /, number operands: 2
Name: *, number operands: 2
Operation? +
    operand 1? 3
    operand 2? 5
calling calculator
result: 8
Operation? -
    operand 1? 7
    operand 2? 2
calling calculator
result: 5
Operation? exit
```

在主机应用程序中无需任何代码更改，就可以使用完全不同的库作为部件。项目

