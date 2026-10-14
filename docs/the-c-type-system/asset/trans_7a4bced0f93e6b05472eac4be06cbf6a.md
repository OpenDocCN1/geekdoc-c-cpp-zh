

```
public readonly struct Speed
{
    public Speed(double amount)
        => Amount = amount;

    public double Amount { get; }
}
```

*Listing 1-6: Making Speed immutable*

为了确保 Speed 实例不可更改，我们也将其设为 readonly。编译器随后会确保 Speed 的任何成员都不能修改状态，并且会拒绝任何尝试更改实例的编译。

将我们的类型设计为不可变，使得在代码检查期间更容易推理代码，因为我们不需要考虑类型实例可能以各种方式更改的情况。这在多线程程序中尤其重要，但在某些情况下，使值类型变为只读也可以通过允许编译器使用某些优化来提高性能。

## Value Validation

在为我们的类型引入了构造函数后，我们可以使用这些构造函数来检查无效参数，并在用户传递非法值时引发异常。例如，速度的合理值必须为非负数。在 Listing 1-7 中，我们检查传递给构造函数的数值是否小于 0，如果是则抛出异常。

```
public Speed(double amount)
{
    if(amount < 0)
        throw new ArgumentOutOfRangeException(
            paramName: nameof(amount),
            message: "Speed must be positive");
    Amount = amount;
}
```

*Listing 1-7: Prohibiting out-of-range values*

Speed 的构造函数验证了提供的值，并且由于构造函数是为 Speed 提供值的唯一方式，我们确保只能创建合法的 Speed 值。我们应该使用构造函数来禁止其他非法参数值，例如 double.NaN，甚至可能添加光速作为上限。如果我们尝试使用非法值创建 Speed，将会得到运行时异常。

ArgumentOutOfRangeException 类型在标准库中定义，是一个描述性命名的类型的良好示例。请注意，在 Listing 1-7 中，我们为 ArgumentOutOfRangeException 构造函数命名了参数，该构造函数接受两个普通字符串参数（paramName: 和 message:）。否则，这些参数的顺序很容易混淆，尤其是名称相似的 ArgumentException 接受的参数顺序是相反的！

在 Speed 的构造函数中验证参数值是封装的一个例子：我们将验证逻辑放在一个地方，而不是分散在任何使用它的<|message|> 方法中。现在，任何使用 Speed 实例的方法都会自动受益于 Speed 构造函数执行的范围检查。

> 创建我们自己的类型的主要好处之一是，我们封装了它们的职责，从而减少了使用它们的方法的职责。最小化重复代码是使我们的代码更清晰、更易于使用并且维护难度大大降低的又一种方式。

Speed 的构造函数建立了一个类不变式——对于类型的任何实例在其生命周期内必须保持的条件——规定 Speed 值永远不会小于 0。由于我们使 Speed 不可变，不变式永远不会被破坏。一旦创建了有效的 Speed 实例，其值永远不会改变，并且不可能创建具有无效值的 Speed 实例。

## Testing

通过将验证封装在 Speed 类型中，我们也可以独立于依赖它的任何算法来测试类不变式。在 Listing 1-8 中，我们尝试使用负值创建 Speed 实例，以测试构造函数是否抛出异常。

```
[Test]
public void Speed_cannot_be_negative()
{
    Assert.That(
        () => new Speed(-1),
        Throws.TypeOf<ArgumentOutOfRangeException>());
}
```

*Listing 1-8: Testing constraints on Speed*

由于验证代码封装在 Speed 类型中，我们只需要这一个测试即可。我们不需要分别测试 Displacement 或任何其他使用 Speed 的方法是否拒绝无效速度值。所有针对 Displacement 的测试都可以专注于确保算法正确，而无需担心参数验证。

因此，使用类型表示领域概念有几个优点。使用我们的类型的代码由于类型的自描述特性而更清晰。我们分离了关注点，使程序更容易理解，测试更集中、更具体。这使得测试更简单，并且在被测试的代码需要更改时更容易维护。

## Refactoring

现在我们已经解决了 Displacement 方法参数的问题，让我们查看其方法体，看看是否可以通过重构实现来进一步改进。Listing 1-9 显示了我们当前的 `Displacement` 代码。

```
public static (double, double)
Displacement(Angle angle, Speed speed, TimeSpan elapsedTime)
{
    var x = speed.Amount * elapsedTime.TotalSeconds * Math.Cos(angle.Size);
    var y = speed.Amount * elapsedTime.TotalSeconds * Math.Sin(angle.Size)
          - 0.5 * 9.81 * Math.Pow(elapsedTime.TotalSeconds, 2);

    return (x, y);
}
```

*Listing 1-9: The current Displacement implementation*

此代码工作正确，但我们有一些需要处理的问题。通过使用 Speed、Angle 和 TimeSpan 类型作为参数，我们使代码变得更冗长，需要访问这些参数的属性来获取其值。请注意，我们在这里使用 TotalSeconds 属性；一个常见错误是使用 TimeSpan 对象的 Seconds 属性，而本意是获取所表示的总秒数，但 Seconds 只返回 TimeSpan 的秒分量。给定一个精确表示 1 分钟的 TimeSpan，Seconds 属性将返回 0，而 TotalSeconds 的值将为 60。

如果 Displacement 方法可以直接在算法中使用变量，将会更清晰，如下所示：

```
var x = speed * elapsedTime * Math.Cos(angle);
var y = speed * elapsedTime * Math.Sin(angle)
      - 0.5 * 9.81 * Math.Pow(elapsedTime, 2);
```

算法还依赖于三个硬编码值。这样的魔术数字通常表明我们需要提供名称来阐明其目的。常见的是在多个地方使用相同的魔术数字，因此如果出于任何原因该值发生变化，我们就需要查找每个用法并确保全部更新。

虽然我们可以看到乘以 0.5 与除以 2 相同，但 9.81 的含义要不那么明显。0.5 和 Math.Pow 调用中使用的 2 只是算术值；为它们命名可能会掩盖其目的而不是澄清。另一方面，9.81 显得具有更重要的目的。再次，为了理解这个数字的含义，我们需要先验知识，即 9.81 是地球重力对物体影响的近似值。我们将首先通过简单地为该值命名来解决此问题。

## Replacing Magic Numbers with Named Constants

用描述性名称替换代码中的魔术数字可以使其对不熟悉算法细节的读者更清晰。一种方法是创建新的值类型，类似于 Speed，来表示该测量值。然而，当我们只需要少数几个众所周知的数值时，使用命名常量来表示它们通常更简单。目前，我们只需要一个值（地球重力）。Listing 1-10 显示了我们可以通过赋予其有意义的名称来指示该值目的的一种方法。

```
public static class Gravity
{
    public const double Earth = 9.81;
}
```

*Listing 1-10: Simple encoding of magic numbers*

虽然重力的命名常量是魔术数字的最简单替代方案，但我们错失了利用 Acceleration 或类似的更通用类型的机会。做到这一点将给予我们最大的灵活性，但也会增加复杂性和维护成本。保持代码简单也有其自身的好处。

我们应该记住，像这样的 const 值会被编译器烘焙到我们的代码中，因此如果我们更改 Gravity.Earth 的值但编译时使用的是使用相同常量的预构建程序集，整个程序可能会对同一常量使用两个不同的值。出于简洁和简单性的考虑，我们将保留 const 值并用 Gravity.Earth 常量替换 Displacement 中的硬编码数字，以便人类读者立即知道其含义：

```
--snip-- - 0.5 * Gravity.Earth * Math.Pow(elapsedTime.TotalSeconds, 2);
```

现在如果我们想要使用更精确的重力近似值，我们只需要更改常量的值，而不是搜索魔术数字 9.81 的所有用法，前提是我们必须记住重新编译使用该常量的任何其他模块。

## Simplifying Properties and Values

我们的 Displacement 方法现在对它使用的变量的含义更加明确。Listing 1-11 显示了其当前实现。

```
public static (double, double)
Displacement(Angle angle, Speed speed, TimeSpan elapsedTime)
{
    ① var x = speed.Amount * elapsedTime.TotalSeconds
        ② * Math.Cos(angle.Size);
    ③ var y = speed.Amount * elapsedTime.TotalSeconds * Math.Sin(angle.Size)
        - 0.5 * Gravity.Earth * Math.Pow(elapsedTime.TotalSeconds, 2);

    return (x, y);
}
```

*Listing 1-11: Displacement using explicit property access*

如前所述，访问 angle、speed 和 elapsedTime 的属性使得实现相当冗长。如果 Displacement 方法可以直接访问这些属性，将会更整洁、更易读
