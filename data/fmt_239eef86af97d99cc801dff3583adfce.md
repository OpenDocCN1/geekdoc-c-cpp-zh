
```
<ListBox.ItemsPanel>
<ItemsPanelTemplate>
<WrapPanel Orientation="Horizontal" HorizontalAlignment="Stretch" />
</ItemsPanelTemplate>
</ListBox.ItemsPanel>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_365.png)

图 18-11 显示了 `PlanetsPanel` 程序的运行情况。如果你加宽 `ListBox`，它用于排列项目的 `DockPanel` 也会随之增大。如果你将 `Window` 调得足够宽，`DockPanel` 将有空间在每行放置另一个项目，因此它将以三列显示项目，而不是图中所示列。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_366_0.png)

图 18-11

## 视图模板

`TreeView` 控件的工作方式与 `ListBox` 和 `ComboBox` 不同，因为它显示的是分级数据而不是简单列表中的项。

在 `TreeView` 中，你必须为树的每个节点指定两个内容：用于显示项和节点的数据，以及深入树树的路径。

例如，考虑一个组织结构图，它列出了包含部门的各个区域，而部门又包含员工。当 `TreeView` 到达部门节点时，你的程序必须告诉它显示什么（例如部门名称）以及如何深入树树（通过列出部门的员工）。

图 18-12 中的 `OrgTreeView` 示例程序显示了公司组织结构图，部门按经理或项目显示。为了更容易理解这些项目，区域名称为红色，部门名称为蓝色并以“department”一词结尾，经理名称在蓝色框内，项目名称在金黄色框内，员工名称为纯黑色文本。

左侧的 `TreeView` 显示区域、每个区域的部门、每个部门的经理以及每个经理的直接下属员工。右侧的 `TreeView` 显示区域、每个区域的部门、项目以及每个项目的团队成员。

下表描述了程序后台代码（code-behind）中定义的类以及这些类拥属性：

| 类 | 属性 | 数据类型 |

| --- | --- | --- |

| Region | RegionName | String |

| | Departments | List of Department |

| Department | Name | String |

| | | List of Manager |

| | | List of Project |

| Manager | Title | String |

| | | List of Employee |

| Project | Name | String |

| | Description | String |

| | TeamLead | Employee |

| | TeamMembers | List of Employee |

| Employee | FirstName | String |

| | LastName | String |

| | Extension | String |

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_367_0.png)

图 18-12

### 绑定集合 | 331

`Manager` 类派生自 `Employee` 类，因此它也继承了 `Employee` 类的 `FirstName`、`LastName` 和 `Extension` 属性。

生成这些显示的 View 控件在它们的 `Resources` 部分包含了 `HierarchicalDataTemplate` 对象，用于描述控件在每个节点上执行的操作。例如，以下代码显示了控件如何处理 `Region` 对象：

```
<HierarchicalDataTemplate
DataType="(x:Type local:Region)"
ItemsSource="Binding Path=RegionName">
  <TextBlock Text="(Binding Path=RegionName)" Foreground="Red">
    <OuterGlowBitmapEffect />
  </TextBlock>
  <TextBlock.BitmapEffect>
</TextBlock>
</HierarchicalDataTemplate>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_368_0.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_368_1.png)

`HierarchicalDataTemplate` 有三个关键属性：

- 第一，它的 `DataType` 属性告诉我们此模板持有的内容。当 `TreeView` 在其数据中遇到 `Region` 对象时，之前的模板就会激活。
- 第二，模板的 `ItemsSource` 属性告诉 `TreeView` 应该查找此项的子项。之前的代码表明 `Region` 对象拥有名为 `Departments` 的子项。你可以使用 `ItemsSource` 属性让树（Tree）沿着数据层级结构中的路径。
- 第三，`HierarchicalDataTemplate` 提供了显示每个节点数据的模板。此示例在 `TextBlock` 中显示了 `Region` 的 `RegionName` 属性。

图 18-2 左侧的 `TreeView` 使用以下 `HierarchicalDataTemplate` 来显示部门对象的数据：

```
<HierarchicalDataTemplate
DataType="(x:Type local:Department)"
ItemsSource="Binding Path=Managers">
  <TextBlock Text="(Binding Path=Name)" Foreground="Blue"/>
</HierarchicalDataTemplate>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_368_2.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_368_3.png)

此模板的 `ItemsSource` 属性表明，部门节点的子项是由对象的 `Managers` 属性提供的，因此 `TreeView` 遵循对象的 `Managers` 路径。

相比之下，图 18-12 右侧 `TreeView` 使用的代码是：

```
<HierarchicalDataTemplate
DataType="(x:Type local:Department)"
ItemsSource="Binding Path=Projects">
  <TextBlock Text="(Binding Path=Name)" Foreground="Blue"/>
</HierarchicalDataTemplate>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_368_4.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_368_5.png)

此模板的 `ItemsSource` 属性使 `TreeView` 使用部门的 `Projects` 属性来构建子节点。

## 绑定主从详情数据

图 18-12 显示的 `OrgChartTreeView` 示例以树形格式显示了分级数据，但还有其他显示此类数据的方法。

例如，图 18-13 显示的 `OrgChartMasterDetail` 示例在左上角的 `ListBox` 中列出了区域列表。当你点击其中一个时，程序会显示该区域的部门列表。当你选择一个部门时，程序会显示该部门的经理列表。当你选择一个经理时，程序会显示汇报给该经理的员工列表。右侧的 `ListBox` 显示相同的数据，只是它们遵循部门项目。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_369_0.png)

图 18-13

`OrgChartMasterDetail` 程序在左上角的 `ListBox` 中列出了区域列表。当你点击其中一个时，程序会显示该区域的部门列表。当你选择一个部门时，程序会显示该部门的经理列表。当你选择一个经理时，程序会显示汇报给该经理的员工列表。右侧的 `ListBox` 显示相同的数据，只是它们遵循部门项目。

`OrgChartMasterDetail` 程序构建了区域、部门、项目和员工对象，这 ` `TreeView` 程序使用的。。代码代码 ` ``  使用作为 `DataContext` 的值。

```
spManager.DataContext = regions;
spProject.DataContext = regions;
```

以下代码显示了程序定义的第一个 `ListBox`：

```
<HierarchicalDataTemplate
DataType="(x:Type local:Region)"
ItemsSource="Binding Path=RegionName">
  <TextBlock Text="(Binding Path=NameName Foreground="="">
    <OuterGlowBitmapEffect />
  </TextBlock>
  </TextBlock.
Effect

</



>
</
>
```

### 绑定 XAML | 331

`Manager` 类派生自 `Employee` 类，因此它也继承了 `Employee` 类的 `FirstName`、`LastName` 和 `Extension` 属性。

生成这些显示的 View 控件在它们的 `Resources` 部分包含了 `HierarchicalDataTemplate` 对象，用于描述控件在每个节点上执行的操作。例如，以下代码显示了控件如何处理 `Region` 对象：

### OrgChartDetail

这里的惊喜是 `ItemsSource` 值（Binding）。该值让控件从 `DataContext` 构建项。

以下代码显示了第一个 `ListBox` 显示对应的部门：

```
<ListBox Name="lstDepartment" Margin="20,0,0,0"
ItemsSource="Binding ElementName=lstManagerRegion, Path=SelectedItems.Departments">
<ListBox.ItemTemplate>
<DataTemplate>
<TextBlock Text="{Binding Path=Name}" Foreground="DarkBlue"/>
</DataTemplate>
</ListBox.ItemTemplate>
</ListBox>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_370_0.png)

此控件的 `ItemsSource` 属性绑定到 `lstManagerRegion` `ListBox` 的 `Departments` 属性。当你从 `lstManagerRegion` `ListBox` 中选择一个区域时，这个 `ListBox` 将填充该项的 `Departments` 列表。

其他主从关系（部门/经理、经理/员工、部门/项目、项目/员工）的绑定工作类似。`ListBox` 拥有 `ItemsSource` 属性，使用带有 `ElementName` 的绑定来主 `ListBox`，并将 `Path` 设置为选中项目的适当属性。

图 18-12 显示的 `ChartTreeView` 视图和图 18-13 显示的 `OrgChartMasterDetail` 程序在代码中构建数据。程序的 `Window_Loaded` 事件处理器创建表示组织结构图的对象。以下代码显示了这些程序共享的一部分代码：

```
private void Window_Loaded(object sender, RoutedEventArgs e)
{
    // 定义员工。
    Employee emp_a = new Employee() { FirstName = "Alice", LastName = "Able", Extension = "1111" };
    Employee emp_b = new Employee() { FirstName = "Ben", LastName = "Better", Extension = "2222" };
    ...
}
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_370_1.png)

```csharp
// 定义 Managers。
Manager mgr_a = new Manager
{FirstName = "Mindy", LastName = "Most",
Extension = "0001", Title = "Manager of OR";
...
mgr_a.Reports.Add(emp_a);

// 省略了大量代码
```

```csharp
// 创建一个区域列表。
List<Region> regions = new List<Region>();
regions.Add(div_work);
regions.Add(div_acro);

// 让 Tree 控件显示此列表。
trvByManager.ItemsSource = regions;
trvByProject.ItemsSource = regions;
```

## OrgChartTreeView 和 OrgChartMasterDetail

代码开始创建 `TreeView` 显示的各个。例如，之前的代码显示了程序如何创建 `Employee` 和 `Manager` 对象，并将一个 `Employee` 添加到 `Manager` 的 `Reports` 列表中。同样地，代码创建了 `Project`、`Department` 和 `Region` 对象，通过将它们添加到每个对象的各个属性中，将所有对象连接起来。

代码最后完成了工作，是创建一个包含它已创建的两个 `Region` 对象的列表，并将 `TreeView` 控件的 `ItemsSource` 属性设置为该列表。

其余代码虽然很长，但相当直观。可以从书籍网站下载示例程序以查看详情。

在 code-bind 中像代码中这样创建复杂的数据结构是常见的，但并不是唯一的方法。另一种方法是在 XAML 代码中构建对象。

要做到这一点，需要使用类似于在 XAML 中定义项目命名空间的命名空间声明。该语句意味着你可以使用前缀 `local` 来引用代码-bind 中的中的类。

```xml
xmlns:local=clr-namespace:OrgChartTreeView
```

现在，XAML 代码可以使用 code-bind 类作为数据类型来定义你需要的数据。例如，`OrgChart` 示例演示了这种方法。例如，XAML 代码显示了一个 `Manager` 对象：

```xml
<Manager FirstName="Mindy" LastName="Most" Extension="0001"
  Title="Manager of OR">
  <Manager.Reports>
    <Employee FirstName="Alice" LastName="Able" Extension="1111"/>
    <Employee FirstName="Ben" LastName="Better" Extension="2222"/>
  </Manager.Reports>
</Manager>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_371_0.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_371_1.png)

## 绑定 XML

代码从一个 `local:Manager` 元素开始，使用属性对应对象的 `FirstName`、`LastName`、`Extension` 和 `Title` 属性。

`Manager` 类有一个 `Reports` 属性，包含一个 `Employee` 对象的数组（XAML 不支持 `List<Employee>` 数据类型，因此为了此示例，我将后台代码定义转换为了数组）。XAML 代码使用 `local:Manager.Reports` 属性指向 `Employee` 对象的数组。

`OrgChart` 程序使用它的 `Windows.Resources` 创建了一个包含两个 `local:Region` 对象的数组。在后续代码中，很容易此数组作为程序 `TreeView` 控件的数据源：

```xml
<TreeView Name="trvByManager" Background="Transparent"
Grid.Row="1" Column="0" ItemsSource={StaticResource regions}">
</TreeView>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_372_0.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_372_1.png)

其余代码虽然很长，但并不简单。程序中的 `HierarchicalDataTemplates` 与 `OrgChartTreeView` 程序中使用的完全相同。你可以从项目网站下载它以查看剩余细节。

> 不完全相同

> 尽管 `OrgChartTreeView` 和 `OrgChartXml` 看起来产生了相同的结果，但实际数据略有不同。`OrgChartTreeView` 程序多次复用了相同的对象。例如，员工 `Alice` 出现在两个 `Manager` 的 `Reports` 控件中，既是 `ACROBAT` 项目的 `TeamLead`，也是该项目的 `TeamMember`。`OrgChartTreeView` 程序创建了一个 `Employee` 对象来表示 `Alice`，然后将其添加到所有这些位置。
