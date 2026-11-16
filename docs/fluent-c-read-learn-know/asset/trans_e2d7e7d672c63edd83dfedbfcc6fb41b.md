

## 多个触发条件

对于像 XAML 这样的声明式编程语言，有很多值得说的地方。它使得某些问题（比如布局 UI）更容易思考和实现。但几乎从定义上讲，以声明式方式进行任何条件处理都是困难的。触发器有所帮助；它们允许你根据单个属性的值设置属性，但只能针对单个属性。MultiTrigger 通过允许你评估多个属性来扩展触发器范式，但只能使用逻辑与。

```xml
<Style ...>
    <Setter Property="FontFamily" Value="Arial" />
    <Style.Triggers>
        <Trigger Property="IsEnabled" Value="false" />
        <Setter Property="FontWeight" Value="Light" />
    </Trigger>
    </Style.Triggers>
</Style>
```

基本的 Trigger 是一个简单的 if 语句。这个读作：“如果文本被禁用，则将其设为轻量。否则将其设为正常。” 或者也许，“除非 IsEnabled 为 false，否则将 FontWeight 设为正常”，这取决于你如何思考。

MultiTrigger 是一个稍微复杂的 if 语句，条件通过 AND 组合。这个读作：“如果文本已启用且已选中，则将其设为粗体。” 注意 MultiTrigger 可以与基本触发器和普通设置器组合。

```xml
<Style ...>
    <Setter Property="FontFamily" Value="Arial" />
    <Style.Triggers>
        <Trigger Property="IsEnabled" Value="false" />
        <Setter Property="FontWeight" Value="Light" />
    </Trigger>
    <MultiTrigger>
        <MultiTrigger.Conditions>
            <Condition "IsEnabled" Value="true" />
            <Condition "IsSelected" Value="true" />
        </MultiTrigger.Conditions>
        <Setter Property="FontWeight" Value="Bold" />
    </MultiTrigger>
    </Style.Triggers>
</Style>
```

## 戴上你的思考帽

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_743_0.png)

你能否重写 MultiTrigger 示例，包括 Style 中其他触发器和设置器所暗示的所有条件，用 C#？

如何将此 C# 翻译为样式？

```csharp
if (this.IsEnabled || this.IsFocused)
this.FontWeight = FontWeight.Bold;
else
this.FontWeight = FontWeight.Normal;
```

## 你做得怎么样？

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_744_0.png)

你当然有权不同意，但我认为 XAML 更冗长，但更易于理解。嵌套的 if 语句非常非常复杂，而且容易出错。

```csharp
this.FontFamily = SystemFonts.Arial;
```

```csharp
if (this.IsEnabled == true)
{
    if (this.IsSelected == true)
        this.FontWeight = FontWeights.Bold;
    else
        this.FontWeight = FontWeights.Normal;
}
else
    this.FontWeight = FontWeights.Light;
```

你不能使用 MultiTrigger 表示逻辑或。（如果你尝试过，不要难过；这是一个陷阱问题。）

在这种情况下，你有两种选择：要么像我在这里所做的那样，在每个 Trigger 中重复设置器，要么（更好）创建一个键控样式，在 Trigger 内部设置它：

```csharp
if (this.IsEnabled || this.IsFocused)
    this.FontWeight = FontWeight.Bold;
else
    this.FontWeight = FontWeight.Normal;
```

```xml
<Setter Property="Style" Value="<keys/> />
```

```xml
<Style>
<Setter Property="FontWeight" Value="Normal" />
<Setter.Triggers>
<Trigger Property="IsEnabled" Value="true" />
<Setter Property="FontWeight" Value="Bold" />
</Trigger>
<Trigger Property="IsFocused" Value="true" />
<Setter Property="FontWeight" Value="Bold" />
</Trigger>
</Setter.Triggers>
</Style>
```

## 样式和触发器陷阱

“它是对的，但不起作用。” 这句话足以让任何程序员心惊胆战。而且你会说这句话的频率远高于“熊吃掉了我的冰淇淋。” 你已经看到了一个例子：那个不太起作用的按钮触发器。让我们再看几个：

- 为我们为 Window 创建的隐式样式添加两个触发器：一个用于 IsLoaded，一个用于 IsEnabled。在每个触发器内，将 Background 属性设置为不同的值。运行应用程序时，显示哪个背景？

- 更改触发器声明的顺序。现在显示哪个背景？

- 在 ResourceDictionary 的末尾添加另一个隐式 Button 样式（在 TextBox 样式之后）。在普通 Setter（不是 Trigger）中设置 Background 属性为 Bisque。运行应用程序时，按钮显示哪个背景？

- 现在交换文件中的两个 Button 样式。显示哪个？

- 在 ResourceDictionary 的末尾添加另一个隐式 Window 样式。使用普通 Setter 将 Background 设置为 Aqua。现在显示哪个背景？

### 独立练习
你能推断出当多个 Setter 或 Trigger 适用时，决定属性最终值的规则吗？

## 组合触发器和样式

你推断出同时适用于触发器和样式的规则了吗？触发器优先于样式，并且无论哪种有两个或更多，最后声明的那个获胜。

## 谁是赢家？

触发器 2。尽管样式 B 优先于样式 A，因为它在后面声明，但触发器优先于样式，因此最后适用的触发器被应用。

| 样式 A |
| --- |
| 触发器 1 |
| 触发器 2 |
| 样式 B |

现在，我们在上一页玩过的例子有点傻。你不会为互斥的属性定义触发器，也不会在单个文件中为同一元素定义两个隐式模板。如果你这样做，追踪问题会相当容易。但当你使用多个 ResourceDictionaries 时，这种事情很容易发生。

可怜的程序员该怎么办？WPF 正在做你告诉它做的事（你只是没有告诉它你以为你告诉它的事），所以粗心的调试不会帮助你，但这里有一些提示：

## 意识到问题

仅仅知道这种事情是如何发生的就能很有帮助。

## 使隐式样式通用

如果你的隐式样式只设置每个元素实例都真正有效的属性，你的生活会更轻松。我知道引用样式的语法有点丑陋，所以很诱人选择“最常用”的样式作为默认值，但这从长远来看会造成问题。（是的，你正在听经验之声的话。）

## 从最通用到最具体组织样式

尝试将样式从最通用（例如基本颜色和字体资源）到最具体（仅在少数情况下适用的样式）进行组织，并在将它们添加到合并字典时，确保按此顺序添加。这不是完美的解决方案，但它将有助于防止样式相互覆盖。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_746_0.png)

什么时候你会动态引用资源而不是静态引用？

你必须在 ResourceDictionary 内的元素声明中添加什么标记扩展？

为了使字典对整个应用程序可用，ResourceDictionary.MergedDictionaries 集合通常定义在什么文件中？

你声明什么属性来基于另一个属性？

你如何创建隐式样式？

包含必填信息的文本框在未选中时应为红色和斜体，在未启用时应为粉色，在聚焦且 CanUndo 为 true 时应为粗体。编写样式。

## 事件触发器

如果属性触发器由属性值的变化激活，你猜什么会激活事件触发器？猜一个事件不会给你金星。具体来说，是 RoutedEvent。还有另一个区别。事件触发器只执行操作。属性触发器可以通过其 EnterActions 和 ExitActions 集合执行操作，但它们主要用于设置属性。两种触发器的语法几乎相同。

```xml
<Trigger Property="Property" Value="Value">
<Setters>
...
</Setters>
<EnterActions>
...
</EnterActions>
<ExitActions>
...
</ExitActions>
```

```xml
<EventTrigger RoutedEvent="Event">
<Actions>
...
</Actions>
<EnterActions>
...
</EnterActions>
<ExitActions>
...
</ExitActions>
```

属性触发器需要属性名和值。事件触发器只需要事件名。

你不需要显式指定 Setters 或 Actions 集合元素。

两种触发器都包括 EnterActions 和 ExitActions 集合，它们实际上是特殊的事件触发器，但对事件触发器没有意义，会被忽略。

