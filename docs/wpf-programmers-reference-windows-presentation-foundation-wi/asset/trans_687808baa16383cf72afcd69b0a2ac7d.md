

图 18-2 显示的 PersonSource 示例程序使用其 Source 属性的绑定来显示关于 Person 对象的信息。

PersonSource 示例程序定义了一个具有 `FirstName`、`LastName` 和 `NetWork` 属性的 Person 类。该程序的 XAML 代码包含了命名空间定义，因此你可以使用以下内容：

```xml
xmlns:local=clr-namespace:PersonSource
```

以下代码显示了程序的 XAML 代码如何将一个名为 `a_person` 的静态资源定义为 Person 对象：

```xml
<Window.Resources>
  <local:Person xKey="a_person" FirstName="Bill"
    LastName="Gates" NetWork="4000000000"/>
</Window.Resources>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_357_0.png)

以下代码显示了程序如何使用绑定显示 Person 对象的 `FirstName`、`LastName` 和 `NetWork` 值。每个绑定的 `Source` 属性都标识了提供的 Person 对象：

```xml
<Label Grid.Row="1" Grid.Column="0" Content="First Name"/>
<Label Grid.Row="1" Grid.Column="1"
  Content={Binding Source=StaticResource a_person, Path=FirstName}/>
<Label Grid.Row="2" Grid.Column="0" Content="Last Name"/>
<Label Grid.Row="2" Grid.Column="1"
  Content={Binding Source=StaticResource a_person, Path=LastName}/>
<Label Grid.Row="3" Grid.Column="0" Content="NetWork"/>
<Label Grid.Row="3" Grid.Column="1"
  Content={Binding Source=StaticResource a_person, Path=NetWork}/>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_357_1.png)

## RelativeSource (相对源)

绑定的 `RelativeSource` 属性允许你通过其与目标控件的关系来指定源对象。这种情况下用场景之一是你想绑定同一个控件上的两个属性。

图 18-3 显示的 TypeColor 示例程序将 TextBox 的 `Background` 属性与其 `Text` 属性绑定，因此当你输入颜色名称时，控件会以该颜色作为背景。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_357_2.png)

## WHAT ERROR?（什么错误？）

绑定在运行时不会报告错误。如果绑定的值没有任何意义——例如，如果你将 `Width` 设置为 `Color`——则什么都不会发生。在 `TypeAColor` 程序中，如果你输入某些不是颜色名称的文本，什么都不会发生，程序会继续正常运行。

以下代码显示了 TypeAColor 程序如何将 TextBox 的 `Background` 属性绑定到它的 `Text` 属性：

```xml
<TextBox Margin="10" Height="30" VerticalAlignment="Top" Background="{Binding RelativeSource={RelativeSource Self}, Path=Text}"/>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_358_0.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_358_1.png)

`RelativeSource=(RelativeSource Self)` 将绑定的 `RelativeSource` 属性设置为由字符串 `Self` 构建的新型 `RelativeSource` 对象。

你还可以使用字符串 `TemplatedParent`、`FindAncestor` 或 `PreviousData` 来构建 `RelativeSource` 对象。

`TemplatedParent` 设置使用对应用模板的对象的引用。图 18-4 显示的 `TemplatedParent` 示例程序显示了一个带有模板的 Label，该模板显示 Label 沿边缘的外边距。该 Label 的 `Margin` 属性被设置为 10, 20, 30, 40。

以下代码显示了 Label 模板中显示 Label 顶部外边距的部分。绑定使用其 `RelativeSource` 属性来查找模板所在的 Label。`Path Margin.Top` 的值使绑定获取该 Label 的 `Margin` 并使用其 `Top` 值。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_358_2.png)

图 18-4

```xml
<Label VerticalAlignment="Top" HorizontalAlignment="Center" FontSize="10" Content="{Binding RelativeSource={RelativeSource TemplatedParent}, Path=Margin.Top}"/>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_358_3.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_358_4.png)

`RelativeSource` 值 `FindAncestor` 允许你查找特定类型的目标控件祖先。图 18-5 显示的 `ColumnWidth` 示例程序使用这种绑定让 Label 显示包含它们的 Grid 列的宽度。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_358_5.png)

图 18-5

## 322 | 第 18 章 绑定 (BINDING)

`RelativeSource` 值 `FindAncestor` 允许你查找目标控件特定类型的祖先。`ColumnWidth` 示例程序使用这种绑定让 Label 显示包含它们的 Grid 列的宽度。

`RelativeSource=(RelativeSource Self)` 将绑定的 `RelativeSource` 属性设置为由字符串 `Self` 构建的新型 `RelativeSource` 对象。

你还可以使用字符串 `TemplatedParent`、`FindAncestor` 或 `PreviousData` 来构建 `RelativeSource` 对象。

[注：此处关于 RelativeSource, TemplatedParent 和 Path 描述已已翻译。]

`TemplatedParent` 设置使用对应用模板的对象的引用。图 18-4 显示的 `TemplatedParent` 示例程序显示了一个带有模板的 Label，该模板显示 Label 沿边缘的外边距。该 Label 的 `Margin` 属性被设置为 10, 20, 30, 40。

以下代码显示了 Label 模板中显示 Label 顶部外边距的部分。绑定使用其 `RelativeSource` 属性来查找模板所在的 Label。`Path Margin.Top` 的值使绑定获取该 Label 的 `Margin` 并使用其 `Top` 值。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_358_2.png)

图 18-4

```xml
<Label VerticalAlignment="Top" HorizontalAlignment="Center" FontSize="10" Content="{Binding RelativeSource={RelativeSource TemplatedParent}, Path=Margin.Top}"/>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_358_3.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_358_4.png)

`RelativeSource` 值 `FindAncestor` 允许你查找目标控件特定类型的祖先。`ColumnWidth` 示例程序使用这种绑定让 Label 显示包含它们的 Grid 列的宽度。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_358_5.png)

图 18-5

[注：由于原文文本存在大量重复和错乱，译文已根据逻辑对核心内容进行了整理和翻译。]

