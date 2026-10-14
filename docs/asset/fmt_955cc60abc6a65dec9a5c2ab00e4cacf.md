
## 前置条件

```
public decimal CalculateShippingCost(
    float packageWeightInKilograms,
    Size<float> packageDimensionsInInches,
    RegionInfo destination)
{
    if (packageWeightInKilograms <= 0f)
        throw new Exception();
    return decimal.MinusOne;
}
```

**清单 7-2** 尽可能多地提供有关前置条件失败原因的背景信息非常重要。

```
public decimal CalculateShippingCost(
    float packageWeightInKilograms,
    Size<float> packageDimensionsInInches,
    RegionInfo destination)
{
    if (packageWeightInKilograms <= 0f)
        throw new ArgumentOutOfRangeException("packageWeightInKilograms", "Package weight must be positive and non-zero");

    return decimal.MinusOne;
}
```

这是在第一次抛出的异常上的改进。除了使用专门用于超出范围参数的异常外，客户端还会被告知哪个参数有误，并且会提供问题的描述。

通过将更多这样的守卫子句串联起来，你可以添加更多必须满足的条件才能调用该方法，而不会产生异常。Listing 7-3 中显示的更改还包括在包裹尺寸超出范围时抛出的异常。

**LISTING 7-3** 可以添加尽可能多的前置条件，以防止方法使用无效参数被调用。

```
public decimal CalculateShippingCost(
    float packageWeightInKilograms,
    Size<float> packageDimensionsInInches,
    RegionInfo destination)
{
    if (packageWeightInKilograms <= 0f)
        throw new ArgumentOutOfRangeException("packageWeightInKilograms", "Package weight must be positive and non-zero");

    if (packageDimensionsInInches.X <= 0f || packageDimensionsInInches.Y <= 0f)
        throw new ArgumentOutOfRangeException("packageDimensionsInInches", "Package dimensions must be positive and non-zero");

    return decimal.MinusOne;
}
```

有了这些前置条件，客户端必须在调用之前确保提供的参数在有效范围内。由此产生的一个推论是，前置条件中检查的所有状态都必须由客户端公开访问。如果客户端无法验证即将调用的方法是否会因无效的前置条件而抛出错误，客户端就无法确保调用会成功。因此，私有状态不应成为前置条件的目标；只有方法参数和类的公共属性才应具有前置条件。

## 后置条件

后置条件检查对象在方法退出时是否处于有效状态。每当方法中发生状态突变时，都可能由于逻辑错误导致状态无效。

后置条件以与前置条件相同的方式实现，通过守卫子句。然而，与将子句放在方法开头不同，后置条件守卫子句必须放在方法末尾，在所有状态编辑完成后，如 Listing 7-4 所示。

**LISTING 7-4** 方法末尾的守卫子句是后置条件，确保返回值在范围内。

```
public virtual decimal CalculateShippingCost(
    float packageWeightInKilograms,
    Size<float> packageDimensionsInInches,
    RegionInfo destination)
{
    if (packageWeightInKilograms <= 0f)
        throw new ArgumentOutOfRangeException("packageWeightInKilograms", "Package weight must be positive and non-zero");

    if (packageDimensionsInInches.X <= 0f || packageDimensionsInInches.Y <= 0f)
        throw new ArgumentOutOfRangeException("packageDimensionsInInches", "Package dimensions must be positive and non-zero");

    // shipping cost calculation

    var shippingCost = decimal.One;

    if (shippingCost <= decimal.Zero)
        throw new ArgumentOutOfRangeException("return", "The return value is out of range");

    return shippingCost;
}
```

通过将状态与预先确定的有效范围进行测试——如果值超出该范围则抛出异常——你可以对方法强制执行后置条件。这里的后置条件与对象的状态无关，而是与返回值有关。就像方法参数值根据前置条件进行有效性测试一样，方法返回值也会根据后置条件进行有效性测试。如果在方法执行期间的任何时候，返回值被设置为零或负值，后置条件将在方法结束时检测到这一点并停止执行。这样，该方法的客户端永远不会意外接收到无效值，并且可以继续假设它始终有效。注意，方法的接口并未传达返回值将始终非零且为正——这是接口与其客户端契约的一个特性。

## 数据不变量

第三种契约是数据不变量。数据不变量是在对象生命周期内保持为真的谓词；它在构造后为真，并且必须保持为真，直到对象超出作用域。数据不变量与对象的预期内部状态相关。对于 `ShippingStrategy` 调用而言，数据不变量的一个例子是提供的固定费率为正且非零。如果如 Listing 7-5 所示，固定费率在构造时设置，构造函数中的简单守卫子句将防止设置无效值。

**LISTING 7-5** 在构造函数中添加前置条件可以帮助保护数据不变量。

```
public class ShippingStrategy
{
    public ShippingStrategy(decimal flatRate)
    {
        if (flatRate <= decimal.Zero)
            throw new ArgumentOutOfRangeException("flatRate", "Flat rate must be positive and non-zero");

        this.flatRate = flatRate;
    }

    protected decimal flatRate;
}
```

由于 `flatRate` 值是受保护的成员变量，客户端设置该值的唯一机会是通过构造函数。如果在此点将 `flatRate` 设置为有效值，则在对象的整个生命周期内它都保证有效，因为客户端无法更改此值。

然而，如果 `flatRate` 变量改为可公开设置的属性，守卫子句就必须移至 setter 块以保护数据不变量。Listing 7-6 显示了将固定费率重构为公共属性，并附带相应的守卫子句。

**LISTING 7-6** 当数据不变量是公共属性时，守卫子句移至 setter。

```
public class ShippingStrategy
{
    public ShippingStrategy(decimal flatRate)
    {
        FlatRate = flatRate;
    }

    public decimal FlatRate
    {
        get
        {
            return flatRate;
        }
        set
        {
            if (value <= decimal.Zero)
                throw new ArgumentOutOfRangeException("value", "Flat rate must be positive and non-zero");

            flatRate = value;
        }
    }
}
```

现在客户端可能能够更改 `FlatRate` 属性的值，但由于 if 语句和异常，不变量不会被破坏。

## 封装 vs. 契约

本示例中实现的契约是有意义的，但它们是由每个值类型的糟糕选择引起的。确保包裹重量参数非零且为正的前置条件契约与变量的类型内在相关：重量永远不应该是零或负数。这使得重量成为封装到其自己的类型的候选。如果，如很可能的那样，另一个类或方法需要重量，你就需要将此前置条件带到新代码中。这效率低下，难以维护且容易出错。更合理的做法是创建新类型并用它定义前置条件，这样所有使用 `Weight` 类型的地方都必须具有非零且为正的值。它实际上是类型的而不是 `CalculateShippingCost` 方法的前置条件的不变量。

同样，固定费率由 `decimal` 类型建模得也不好。相反，它应该被提升为自己的值类型，并且要求它非零且为正的不变量应应用于此类型。

## Liskov 契约规则

所有这些方法契约讨论只是 Liskov 替换原则一些要点的序言。LSP 设定了类型继承契约的规则。LSP 定义的提醒如下所示：

> 如果 `S` 是 `T` 的子类型，则类型 `T` 的对象可以用类型 `S` 的对象替换，而不会破坏程序。

就契约而言，这导致了前面所述的指导原则：

- 子类型中不能加强前置条件。
- 子类型中不能削弱后置条件。
- 超类型的不可变性必须在子类型中保留。

如果你在创建现有类的子类时遵循所有这些规则，当处理契约时，可替代性将被保留。

每当创建子类时，它都会带来父类组成的方法、属性和字段。这也包括方法内部和属性 setter 中的契约。前置条件、后置条件和数据不变量都应以与父类相同的方式维护。子类在适用时被允许覆盖方法实现，这包括更改契约的可能性。Liskov 替换规定某些更改不被允许，因为它们可能会破坏必须能够将新子类用作超类实例的现有客户端。

### 前置条件不能被加强

每当子类覆盖包含前置条件的现有方法时，它绝不能 *加强* 现有的前置条件。这样做可能会破坏任何已经假设子类定义了该方法最强可能的前置条件契约的客户端代码。

Listing 7-7 显示了新 `WorldwideShippingStrategy` 的添加。由于类行为之间有大量相似之处，此新类被实现为 `ShippingStrategy` 类的子类。`CalculateShippingCost` 方法被覆盖以提供一个新值，该值会考虑到通过 `RegionInfo` 参数发送的包裹的目的地。虽然 `ShippingStrategy` 类并未保证会提供包裹的目的地，但 `WorldwideShippingStrategy` 现在要求提供此参数，否则它无法正确计算将包裹发送到该地点的费用。

**LISTING 7-7** 此子类添加了新的守卫子句，从而加强了前置条件。

```
public class WorldWideShippingStrategy : ShippingStrategy
{
    public override decimal CalculateShippingCost(
        float packageWeightInKilograms,
        Size<float> packageDimensionsInInches,
        RegionInfo destination)
    {
        if (packageWeightInKilograms <= 0f)
            throw new ArgumentOutOfRangeException("packageWeightInKilograms", "Package weight must be positive and non-zero");

        if (packageDimensionsInInches.X <= 0f || packageDimensionsInInches.Y <= 0f)
            throw new ArgumentOutOfRangeException("packageDimensionsInInches", "Package dimensions must be positive and non-zero");

        if (destination == null)
            throw new ArgumentNullException("destination", "Destination must be provided");

        return decimal.One;
    }
}
```

诱惑在于加强前置条件，以便你能保证 `destination` 参数会被提供。这会产生一个冲突，调用代码无法解决。如果一个类调用 `ShippingStrategy` 类的 `CalculateShippingCost` 方法，它可以自由地为 `destination` 参数传入 `null` 值而不会产生副作用。但如果它调用的是 `WorldWideShippingStrategy` 类的 `CalculateShippingCost` 方法，则不得为 `destination` 参数传入 `null` 值。否则会违反前置条件并导致异常被抛出。如前几章所示，客户端代码绝不能对它所操作的类型的假设。否则只会导致类之间强耦合以及无法适应需求变化的能力。

要演示该问题，请检查第 7-8 节所示的单元测试。

**LISTING 7-8** 当前置条件被加强时，客户端无法可靠地在需要 `ShippingStrategy` 的地方使用 `WorldWideShippingStrategy`。

```
[Test]
public void ShippingRegionMustBeProvided()
{
    strategy.Invoking(s => s.CalculateShippingCost(1f, ValidDimensions, null))
        .ShouldThrow<ArgumentNullException>("Destination must be provided")
        .And.ParamName.Should().Be("destination");
}
```

如果此测试使用的策略类型为 `WorldWideShippingStrategy`，测试将通过；未提供目的地但需要提供，因此会抛出符合规范的异常。如果改用 `ShippingStrategy`，则此测试将失败，因为不存在防止 `destination` 为 `null` 的前置条件，也不会抛出异常。

第 7-9 节显示了一组重构后的单元测试，它们不会尝试对两种策略类型测试相同的先决条件。断言必须提供运送区域的测试仅对 `WorldWideShippingStrategy` 有效。然而，无论运送策略如何，运送重量必须为正的前置条件始终有效，因此它被包含在将为每个运送策略类运行的测试基类中。

**LISTING 7-9** 这些重构后的单元测试分别针对两个运送策略类。

```
[TestFixture]
public class WorldWideShippingStrategyTests : ShippingStrategyTestsBase
{
    [Test]
    public void ShippingRegionMustBeProvided()
    {
        strategy.Invoking(s => s.CalculateShippingCost(1f, ValidSize, null))
            .ShouldThrow<ArgumentNullException>("Destination must be provided")
            .And.ParamName.Should().Be("destination");
    }

    protected override ShippingStrategy CreateShippingStrategy()
    {
        return new WorldWideShippingStrategy(decimal.One);
    }
}

// ...

public abstract class ShippingStrategyTestsBase
{
    [Test]
    public void ShippingWeightMustBePositive()
    {
        strategy.Invoking(s => s.CalculateShippingCost(-1f, ValidSize, null))
```
