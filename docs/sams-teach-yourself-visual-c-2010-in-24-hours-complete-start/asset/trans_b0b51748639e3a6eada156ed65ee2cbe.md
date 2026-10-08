
## 列表 18.7 使用转换器参数

```xml
<TextBlock>
    <TextBlock.Text>
        <MultiBinding Converter="{StaticResource nameConverter}"
                      ConverterParameter="LastNameFirstName">
            <Binding Path="FirstName"/>
            <Binding Path="LastName"/>
        </MultiBinding>
    </TextBlock.Text>
</TextBlock>
```

## 试一试

### 创建和使用转换器

若要创建额外的数据转换器并修改绑定以便在 PhotoViewer 应用程序中使用它们，请遵循以下步骤。

1.  如果您尚未这样做，请将列表 18.4 和列表 18.5 中显示的转换器添加到 PhotoViewer 应用程序中。
2.  为曝光模式、闪光模式、镜头光圈和焦距添加转换器。所有这些的 `ConvertBack` 方法都应返回 `Binding.DoNothing`，这指示绑定引擎不执行任何操作。对于曝光模式和闪光模式转换器，`Convert` 方法应返回代表枚举值的“友好”名称。镜头光圈值通常以“f值”表示，因此镜头光圈转换器的 `Convert` 方法应返回格式化为 `String.Format(“f / {0:#.#}”, value)` 的值。焦距转换器的 `Convert` 方法应返回格式化为 `String.Format(“{0} mm”, value)` 的值。
3.  修改 `Resources.xaml` 文件，将转换器作为资源添加。
4.  修改 `MainWindow.xaml` 文件，根据需要为 `Label` 元素添加适当的转换器。请记住，对于 `Size` 转换器，您需要使用 `MultiBinding`。
5.  运行应用程序并选择一个包含图像的目录。当您选择图像时，详细信息应发生变化并使用转换器进行显示。

## 绑定到集合

到目前为止，您一直在处理与单个对象的绑定。那么，显示所选目录中文件的列表框是如何绑定的？这是绑定到一个对象集合，具体来说，是在第 9 小时“处理数组和集合”中，您在 MainWindow 类中创建的 PhotoCollection 实例。通常，您会使用 ItemsControl（如 ListBox、ListView 或 TreeView）来显示集合，并将 ItemsSource 属性绑定到集合实例。默认情况下，ItemsSource 属性支持单向绑定。

列表 18.8 显示了 PhotoViewer 应用程序用于执行此操作的 XAML。

### 列表 18.8 绑定 ItemsControl

```xml
<ListBox
    Name="PhotosListBox"
    Margin="5"
    SelectionMode="Extended"
    SelectedIndex="0"
    IsSynchronizedWithCurrentItem="True"
    ItemsSource="{Binding}"
    Style="{StaticResource PhotoListBoxStyle}"
</ListBox>
```

列表 18.8 中显示的代码使用了空绑定语法 `{Binding}`，这使得 `ListBox` 使用其父级的 `DataContext`。由于省略了路径，`ItemsSource` 属性绑定到整个对象。

## 使用集合视图

当您已将 `ItemsControl` 绑定到集合时，您可以使用集合视图对数据进行排序、筛选或分组。集合视图是绑定源集合之上的一层，使您能够基于排序、筛选或分组查询来导航和显示数据，而不改变底层集合。由于视图不会改变底层集合，您可以创建引用相同源头的多个视图，从而以不同方式显示相同的数据。

当您直接绑定到集合时，实际上您是绑定到 WPF 为该集合创建的默认视图。此默认视图由绑定到同一集合的所有绑定共享。如果您需要在代码隐藏文件中访问默认视图，可以使用静态的 `CollectionViewSource.GetDefaultView` 方法。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_416_0.png)

### 实现集合

如果您希望集合能够被数据绑定引擎使用，以便插入或删除操作自动更新 UI 元素，则该集合必须实现 System.Collections.Specialized.INotifyCollectionChanged 接口。此接口定义了应在集合发生更改时引发的 CollectionChanged 事件。

WPF 提供了 ObservableCollection<T> 类，您将其用作 PhotoCollection 类的基础类，该类已经实现了 INotifyCollectionChanged 接口。除非您有高级场景并希望实现自己的集合用于数据绑定，否则应考虑使用 ObservableCollection<T>。

为了完全支持值传递，集合中支持可绑定属性的每个对象还必须实现 INotifyPropertyChanged 接口。

表 18.1 显示了为不同的源集合类型创建的默认视图。

### 表 18.1 默认视图

| **源集合类型** | **集合视图类型** | **备注** |
| :--- | :--- | :--- |
| IEnumerable | 基于 CollectionView 的内部类型 | 无法对项进行分组 |
| IList | ListCollectionView | |
| IBindingList | BindingListCollectionView | |

### 排序

集合视图允许您根据提供的比较条件对数据应用顺序或更改默认顺序。由于集合视图是基于客户端的数据视图，且不对底层集合进行任何更改，因此可以应用或移除排序，而无需重新查询集合内容。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_416_1.png)

### 创建 CollectionViewSource

您还可以使用 CollectionViewSource 直接在 XAML 中创建视图，它是继承自 CollectionView 的类的 XAML 代理，如下所示：

```xml
<Window.Resources>
    <CollectionViewSource x:Key="view" Source="{Binding Source={x:Static Application.Current}, Path=Contacts}" />
</Window.Resources>
```

这创建了一个名为 view 的新资源，该资源绑定到当前应用程序对象的 Contacts 集合。

### 列表 18.9 更改视图的排序顺序

```csharp
// 假设 view 已在其他地方实例化，
// 并且 view 中包含的对象有一个名为 LastName 的属性。

// 清除可能已添加的任何现有 SortDescriptions。
// 只有在更改排序时才需要这样做。
view.SortDescriptions.Clear();

// 添加一个新的排序，将按 LastName 属性升序排序。
view.SortDescriptions.Add(
    new SortDescription("LastName", ListSortDirection.Ascending));
```

### SortDescription 结构

SortDescription 结构体的 propertyName 参数支持通过“点”符号表示法引用嵌套属性。例如，要为 Contact.XfnRelationships.Me 属性创建 SortDescription，您需要为 propertyName 参数值使用：
"XfnRelationships.Me"

当对数据类型为枚举的属性进行排序时，项的顺序与枚举声明中的顺序相同。

### 顺便说一下

### 分组

除了用于查看 IEnumerable 集合的内部类之外，所有集合视图都支持分组功能。这允许用户将数据划分为逻辑组。组可以是显式的，即由用户决定；或者是隐式的，即组是根据数据动态生成的。

列表 18.10 显示了如何为集合视图添加分组。

### 列表 18.10 在视图上添加分组

```csharp
// 假设 view 已在其他地方实例化，
// 并且 view 中包含的对象有一个名为 LastName 的属性。

// 清除可能已添加的任何现有 GroupDescriptions。
view.GroupDescriptions.Clear();

PropertyGroupDescription groupDescription = new PropertyGroupDescription();
groupDescription.PropertyName = "LastName";
view.GroupDescriptions.Add(groupDescription);
```

### 筛选

筛选更改视图显示的数据，而不改变底层集合。将筛选视为生成数据子集。筛选涉及使用委托来执行实际的筛选操作。

要为 AddressBook 应用程序添加筛选功能，以显示所有姓氏以字母“D”开头的联系人，请实现如列表 18.11 所示的方法。

### 列表 18.11 用于筛选的方法

```csharp
private void NameFilter(object sender, FilterEventArgs e)
{
    Contact contact = e.Item as Contact;
    if (contact != null)
    {
        e.Accepted = contact.LastName.StartsWith("D");
    }
    else
    {
        e.Accepted = false;
    }
}
```

如果您直接使用其中一个 CollectionView 类，您将使用 Filter 属性设置回调。但是，如果您使用 CollectionViewSource，则需要添加事件处理程序，如下所示：

```csharp
view.Filter += new FilterEventHandler(NameFilter);
```

### 当前项指针

由于 WPF 始终通过视图将集合绑定，因此所有到集合的绑定都有一个当前项指针。无论您是使用集合的默认视图还是指定自己的视图，这都是成立的。排序操作保留在最后一个选定项上的当前项指针，但集合视图会围绕它进行重构。例如，如果选定项在排序前位于列表开头，排序后它可能位于列表中间。如果应用筛选器且选定项在筛选发生后仍保留在视图中，则它继续作为选定项；否则，筛选后视图的第一个项将成为当前项。Path 值中的斜杠 (/) 字符指示视图的当前项。

列表 18.12 显示了一些绑定，并假设数据上下文是一个集合视图。

