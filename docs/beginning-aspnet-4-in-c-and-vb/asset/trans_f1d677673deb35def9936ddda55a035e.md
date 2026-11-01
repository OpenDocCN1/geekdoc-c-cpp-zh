
`[Description]` 属性定义在 `Message` 属性上，用于在 Visual Studio 的属性网格中提供有关该属性的额外信息，如图 44-8 所示。

目前来看，该活动完全可用；然而，有几个方面需要改进以使其更易于使用。正如本章前面 `Pick` 等活动所示，一个活动可能具有某些强制属性，如果未定义这些属性，则会在设计表面上产生错误标记。要使你的活动具有相同的行为，你需要扩展代码。

![](img/d7d2ffa0a76feaab821930e95daace93_1378_0.png)

## Activity Validation

当活动放置在设计表面上时，Designer 会在两个地方查找验证信息。最简单的验证形式是在参数属性上添加 `[RequiredArgument]` 属性。如果参数未定义，则会在活动名称右侧显示感叹号标记，如图 44-9 所示。

![](img/d7d2ffa0a76feaab821930e95daace93_1378_1.png)

如果将鼠标悬停在该标记上，会显示一个工具提示，提示“未提供必需活动参数‘Message’的值。” 这是一个编译错误，因此在执行应用程序之前你需要为此参数定义一个值。

在存在多个可能相关的属性的情况下，你可以重写 `CacheMetadata` 方法以添加一些额外的验证代码。该方法在活动执行之前被调用；在其中你可以检查强制参数是否已定义，并可选择为传递的参数添加额外的元数据。你还可以通过调用传递给 `CacheMetadata` 方法的 `CodeActivityMetadata` 对象上的 `AddValidationError` 重载之一来添加额外的验证错误（或警告）。

现在你已经完成了活动验证，下一步要做的是更改活动的渲染行为，因为当前的设计器体验是为你提供的，并且可以变得更有趣。

## Designers

当活动在屏幕上呈现时，通常会为其关联一个设计器。设计器的任务是提供该活动的屏幕表示，在 Workflow 4 中此表示使用 XAML 实现。如果你之前没有使用过 XAML，我们建议在继续之前查看第 35 章“Core WPF”。

活动的设计时体验通常与活动本身创建在单独的程序集中，因为在运行时不需要此设计体验。Visual Studio 包含一个 Activity Designer Library 项目类型，这是一个理想的起点，因为当你使用此模板创建项目时，会提供一个默认活动设计器，你可以根据需要对其进行修改。

在设计器的 XAML 中，你可以提供任何你想要的内容——包括动画（如果需要）。就用户界面而言，少即是多，我们建议查看现有的活动以了解什么是合适的。

首先，我们将创建一个简单的设计器并将其与 `DebugWrite` 活动关联。以下代码显示了在向项目添加活动设计器时（或在构建新的活动设计器库项目时）为你创建的模板。同样，此代码可在 04_CustomActivities 解决方案中找到。

```
<sap:ActivityDesigner x:Class="Activities.Presentation.DebugWriteDesigner"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:sap="clr-namespace:System.Activities.Presentation;
assembly=System.Activities.Presentation"
xmlns:sapv="clr-namespace:System.Activities.Presentation.View;
assembly=System.Activities.Presentation"

<Grid>

</Grid>
</sap:ActivityDesigner>
```

创建的 XAML 只是构造了一个网格，并包含了一些导入的命名空间，这些命名空间可能被你的活动需要。显然，模板中的内容很少，因此首先我们添加一个标签和一个文本框，用于定义消息。

```
<Grid>
  <Grid.ColumnDefinitions>
    <ColumnDefinition Width="Auto"/>
    <ColumnDefinition Width="*"/>
  </Grid.ColumnDefinitions>
  <TextBlock Text="Message" Margin="0,0,5,0"/>
  <TextBox Text="{Binding Path=ModelItem.Message, Mode=TwoWay}" Grid.Column="1"/>
</Grid>
```

此处的 XAML 在活动的 Message 属性与文本框之间构造了一个绑定。在设计器 XAML 中，你始终可以使用 ModelItem 引用来引用正在设计的活动。

为了将上面定义的设计器与 DebugWrite 活动关联，你还需要修改活动并添加 Designer 属性（你也可以实现 IRegisterMetadata 接口，但本章不再进一步介绍）。

```
[Designer("Activities.Presentation.DebugWriteDesigner, Activities.Presentation")]
public class DebugWrite : CodeActivity
{
  ...
}
```

这里，我们使用 [Designer] 属性来定义设计器与活动之间的链接。最好使用此属性的字符串版本，因为这样可以确保活动程序集中没有对设计程序集的引用。

现在当你在 Visual Studio 中使用 DebugWrite 活动的一个实例时，你会看到类似于图 44-10 的内容

![](img/d7d2ffa0a76feaab821930e95daace93_1379_0.png)

问题在于 Message 属性——它没有显示属性网格中定义的值，而且如果你尝试通过在文本框中键入来设置值，你会收到异常。

原因在于你试图将一个简单的文本值绑定到 InArgument<string> 类型，为此你需要使用 Workflow 4 中提供的另外两个内置类——ExpressionTextBox 和 ArgumentToExpressionConverter。设计器的完整 XAML 现在如下所示。我们已对添加或修改的行加了粗体。

```
<sap:ActivityDesigner x:Class="Activities.Presentation.DebugWriteDesigner"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:sap="clr-namespace:System.Activities.Presentation;
assembly=System.Activities.Presentation"
xmlns:sapv="clr-namespace:System.Activities.Presentation.View;
assembly=System.Activities.Presentation"
xmlns:sadc="clr-namespace:System.Activities.Presentation.Converters;
assembly=System.Activities.Presentation"
>
<sap:ActivityDesigner.Resources>
  <sadc:ArgumentToExpressionConverter x:Key="argConverter"/>
</sap:ActivityDesigner.Resources>
<Grid>
  <Grid.ColumnDefinitions>
    <ColumnDefinition Width="Auto"/>
    <ColumnDefinition Width="*"/>
  </Grid.ColumnDefinitions>
  <TextBlock Text="Message" Margin="0,0,0,0" />
  <sapv:ExpressionTextBox Grid.Column="1"
    Expression="{Binding Path=ModelItem.Message, Mode=TwoWay,
      Converter={StaticResource argConverter},
      ConverterParameter=In}"
    OwnerActivity="{Binding ModelItem}"/>
</Grid>
</sap:ActivityDesigner>
```

*代码下载 04_CustomActivitiesFirst*

我们在文件中添加了一个新的命名空间——System.Activities.Presentation.View。它包含用于在屏幕上的表达式与活动的 Message 属性之间转换的转换器——这就是 ArgumentToExpressionConverter，它已添加到 XAML 文件的资源中。

然后我们用 ExpressionTextBox 替换了标准的 TextBox 控件。此控件用于允许用户输入表达式以及简单文本，因此 DebugWrite 活动可以包含一个结合运行工作流中许多值的表达式，而不仅仅是一个简单的文本字符串。进行这些更改后，活动的行为更像内置活动。

## Custom Composite Activities

活动的一个常见需求是创建复合活动——即包含其他子活动的活动。你已经看到了示例，例如 Pick 活动和 Parallel 活动。

复合活动的执行完全由程序员决定——例如，你可以有一个随机活动只调度其一个子活动，或有一个活动根据当前星期几跳过某些子活动。最简单的执行模式是执行所有子活动，但作为开发者你可以决定子活动的执行方式以及活动何时完成。

我们创建的第一种复合活动是“重试”活动。尝试一次操作，如果失败则重试多次然后再失败是很常见的。该活动的伪代码如下：

```
int iterationCount = 0;
bool looping = true;
while ( looping )
{
  try
  {
    // Execute the activity here
    looping = false;
  }
  catch (Exception ex)
  {
    iterationCount += 1;
    if ( iterationCount >= maxRetries )
      rethrow;
  }
}
```
