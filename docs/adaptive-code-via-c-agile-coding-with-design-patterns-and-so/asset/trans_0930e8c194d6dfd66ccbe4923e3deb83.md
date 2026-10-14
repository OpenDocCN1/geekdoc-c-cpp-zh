

本示例中的谓词与先前示例中的略有不同，它展示了后置条件的一种常见用法：测试返回值是否有效。检查运费是否为正数（实际上，应为非负数）需要了解返回值。返回值有时（但并非总是）是方法内部声明并定义的局部变量。你可以简单地断言要返回的值大于零，但这并非真正万无一失。要访问从方法实际返回的值，可以使用 `Contract.Result` 方法来获取。这个泛型方法接受方法的返回类型，并返回方法最终返回的结果。这样，你便可以确保后续任何行都无法在违反后置条件并抛出异常的情况下，用无效值替换有效值。

## 数据不变式

类中的每个方法通常都包含自己的前置条件和后置条件，但数据不变式涉及整个类。代码契约允许你在类上创建一个私有方法，其中包含类不变式的声明性定义。

每个不变式都由 `Contract` 静态类的另一个方法定义，如清单7-18所示。

### 清单7-18 数据不变式可以通过专门为此目的而设计的方法来保护。

单击此处查看代码图像

```
public class ShippingStrategy
{
    public ShippingStrategy(decimal flatRate)
    {
        this.flatRate = flatRate;
    }

    [ContractInvariantMethod]
    private void ClassInvariant()
    {
        Contract.Invariant(this.flatRate > 0m, "Flat rate must be positive and non-zero");
    }

    protected decimal flatRate;
}
```

`Contract.Invariant` 方法遵循与 `Requires` 和 `Ensures` 方法相同的模式：它接受一个布尔谓词，该谓词必须为 true 才能满足契约。在此示例中，还提供了第二个字符串参数，用于在契约未能满足且不变式未受保护时描述故障。客户端可以根据需要多次调用 `Invariant` 方法，因此最好将不变式分解为最细粒度，而不是使用 `&&` 运算符将它们全部逻辑与运算在一起。这样做能让你精确了解哪个数据不变式被违反，从而获得最大收益。

如果这是一个普通的私有方法，你将需要在每个方法的开头和结尾调用该方法，以确保不变式得到正确保护。幸运的是，你可以通过使用 `ContractInvariantMethod` 特性标记该方法，让代码契约替你完成这项工作。请记住，特性不需要 `Attribute` 后缀，因此在示例中将其缩短为 `ContractInvariantMethod`。这会将此方法标记为代码契约在进入和离开方法时必须调用的方法，以确认类的数据不变式未被违反。标记为 `ContractInvariantMethod` 的方法必须先决条件：返回 `void` 且不接受参数。不过，它可以是 public 或 private，并且你可以选择任意名称来描述该方法。类可以有多个 `ContractInvariantMethod`，因此逻辑分组也是可行的。方法体只能调用 `Contract.Invariant` 方法。

## 接口契约

这里要介绍的代码契约最后一个特性是接口契约。到目前为止，你将所有对 `Contract.Requires`、`Contract.Ensures` 和 `Contract.Invariant` 的调用都嵌入到了类实现本身中。如前所述，`Contract` 类的静态特性使得这些代码无处不在，并且难以移除或将来更改以支持其他替代库。这在一定程度上与自适应的代码库（理想状态）相悖，但出于务实的原因，一些基础设施上的妥协是可以接受的。

一个更直接的问题在于，当代码契约被大量应用于类时，可读性会下降。实际上，这并不是代码契约本身的缺陷，而是普遍认真应用契约的结果。前置条件、后置条件和数据不变式自然会在代码中实现，但这些代码往往会增加噪声与信号之比。

如清单7-19中针对正在进行的 `ShippingStrategy` 示例所示，接口契约除了提供另一个有用的特性之外，还可以缓解这个问题。

### 清单7-19 一个专用的类可以为接口的每个实现定义前置条件、后置条件和不变式。

单击此处查看代码图像

```
[ContractClass(typeof(ShippingStrategyContract))]
interface IShippingStrategy
{
    decimal CalculateShippingCost(
        float packageWeightInKilograms,
        Size<float> packageDimensionsInInches,
        RegionInfo destination);
}
//...
[ContractClassFor(typeof(IShippingStrategy))]
public abstract class ShippingStrategyContract : IShippingStrategy
{
    public decimal CalculateShippingCost(float packageWeightInKilograms, Size<float> packageDimensionsInInches, RegionInfo destination)
    {
        Contract.Requires<ArgumentOutOfRangeException>(packageWeightInKilograms > 0f,
```
```
"Package weight must be positive and non-zero");
    Contract.Requires<ArgumentOutOfRangeException>(packageDimensionsInInches.X > 0f &&
    packageDimensionsInInches.Y > 0f, "Package dimensions must be positive and non-zero");

    Contract.Ensures(Contract.Result<decimal>() > 0m);

    return decimal.One;
}

[ContractInvariantMethod]
private void ClassInvariant()
{
    Contract.Invariant(flatRate > 0m, "Flat rate must be positive and non-zero");
}
}
```

对于接口契约，你当然需要一个接口来使用。在此示例中，`CalculateShippingCost` 方法已被提取到它自己的 `IShippingStrategy` 接口中。将要应用契约的是这个接口，而不是单个实现。这是与先前示例的一个重要区别，因为它意味着该接口的所有实现都将获得已应用的契约。这样，你便可以在一个几乎不提供实现和使用指令的简单接口上，增加更强大的要求和保证。

在编写接口契约时，你还需要一个类来实现接口的方法，但只填充对 `Contract.Requires` 和 `Contract.Ensures` 方法的调用。抽象类 `ShippingStrategyContract` 提供了此功能，看起来与先前示例类似，但先前示例缺少的是方法的实际功能。即使在生产代码中，这也是契约类中包含代码的极限。此外，还有一个 `ContractInvariantMethod` 来容纳任何对 `Contract.Invariant` 的调用，就像这个类是真正的实现一样。

要将接口与契约类实现关联起来，遗憾的是，你需要通过特性进行双向引用。这有点不幸，因为它给接口增加了噪声，如果能避免就更好了。尽管如此，通过用 `ContractClass` 特性标记接口，用 `ContractClassFor` 特性标记契约类，你就可以一次性编写前置条件、后置条件和数据不变式保护代码，并将其应用于接口的所有后续实现。`ContractClass` 和 `ContractClassFor` 特性都接受一个 `Type` 参数。`ContractClass` 应用于接口，并传入契约类类型；而 `ContractClassFor` 应用于契约类，并传入接口类型。

到此，对代码契约的介绍以及根据里氏替换原则规则对契约的涉猎就结束了。最后需要强调一个重要的点。无论是手动实现还是使用代码契约实现，如果前置条件、后置条件或不变式失败，客户端都不应捕获异常。捕获异常表示客户端可以从这种状况中恢复，而在契约被破坏时，这很少有可能，甚至可能根本无法恢复。理想情况下，所有契约违例都将发生在功能测试期间，并且

