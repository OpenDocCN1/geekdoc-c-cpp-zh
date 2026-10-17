
```csharp
public class ExposureTimeConverter : IValueConverter
{
    public object Convert(object value, Type targetType, object parameter,
        CultureInfo culture)
    {
        object result = DependencyProperty.UnsetValue;
        
        if (value != null)
        {
            decimal exposure = (decimal)value;
            exposure = Decimal.Round(1 / exposure);
            result = String.Format("1/{0} sec.", exposure.ToString());
        }
        
        return result;
    }
    
    public object ConvertBack(object value, Type targetType, object parameter,
        CultureInfo culture)
    {
        object result = DependencyProperty.UnsetValue;
        
        if (value != null)
        {
            string exposure = ((string)value).Substring(2);
            result = (1 / Decimal.Parse(exposure));
        }
        
        return result;
    }
}
```

创建好转换器后，你可以将其作为资源添加到 XAML 文件中，如下所示。这里假设存在一个映射到定义 `ExposureTimeConverter` 的 CLR 命名空间的 XML 命名空间 `er`：

```xml
<er:ExposureTimeConverter x:Key="ExposureTimeConverterReference" />
```

最后，你可以在自己的绑定中使用该转换器，方法是将其添加到 XAML 中的绑定里。以下展示了使用新转换器的曝光时间 `Label1` 的绑定：

```xml
<Label Content="{Binding Path=Metadata.ExposureTime,
    Converter={StaticResource ExposureTimeConverterReference}}" />
```

实现了 `IValueConverter` 接口的转换器只能转换单个值。虽然这对许多转换器来说已经足够，但有时需要从多个源属性，甚至多个源对象生成最终值。例如，`PhotoViewer` 应用程序显示图像的大小，但 `Photo` 类不包含 `Size` 属性。它确实包含 `Width` 和 `Height` 属性，可用于显示大小。要创建一个可与多个值配合工作的转换器，你需要创建一个实现了 `IMultiValueConverter` 的类。清单 18.5 展示了多值转换器的示例。在生产应用程序中，你应该确保转换在面临异常时是健壮的。为了使示例保持简单，此处省略了异常处理代码。

## 清单 18.5 大小多值转换器

```csharp
public class PhotoSizeConverter : IMultiValueConverter
{
    public object Convert(object[] values, Type targetType, object parameter,
        CultureInfo culture)
    {
        if (values[0] == null || values[1] == null)
        {
            return String.Empty;
        }
        else if (values[0] == DependencyProperty.UnsetValue ||
                 values[1] == DependencyProperty.UnsetValue)
        {
            return String.Empty;
        }
        else
        {
            return String.Format("{0}x{1}", values[0], values[1]);
        }
    }

    public object[] ConvertBack(object value, Type[] targetTypes,
        object parameter, CultureInfo culture)
    {
        if ((string)value == String.Empty)
        {
            return new object[2];
        }
        else
        {
            string[] sSize = new string[2];
            sSize = ((string)value).Split('x');

            object[] size = new object[2];
            size[0] = UInt32.Parse(sSize[0]);
            size[1] = UInt32.Parse(sSize[1]);
            return size;
        }
    }
}
```

在 XAML 中将多值转换器添加为资源的方式与单值转换器相同，但将其用作绑定的一部分则有所不同。不再使用像之前那样简单的绑定，你需要使用 `MultiBinding`。`MultiBinding` 允许你将目标的属性绑定到一组源属性列表，并获取单个值。由于 `MultiBinding` 由独立的 `Binding` 元素组成，如有必要，每个绑定都可以有自己的转换器。

清单 18.6 展示了如何在 XAML 中使用 `PhotoSizeConverter`。

## 清单 18.6 使用多值转换器

```xml
<Label1> <Label.Content> <MultiBinding Converter="{StaticResource PhotoSizeConverterReference}"> <Binding Path="Metadata.Width"/> <Binding Path="Metadata.Height"/> </MultiBinding> </Label.Content> </Label1>
```

`MultiBinding` 中各个 `Binding` 元素出现的顺序，就是这些值在传递给 `Convert` 方法的数组中的存储顺序。

无论是单值还是多值转换器，它们都具有文化感知能力。`Convert` 和 `ConvertBack` 方法都有一个 `culture` 参数，可以根据文化信息来更改转换。

`Convert` 和 `ConvertBack` 方法还有一个名为 `parameter` 的参数，可用于更改转换。此参数提供了灵活性，使得单个转换器可以根据转换器参数参数的值产生不同的格式。

### ConverterParameter 属性

> `MultiBinding` 的 `ConverterParameter` 属性不是 `DependencyProperty`，因此你不能对其进行绑定。如果你需要 `IMultiValueConverter` 根据其他某个源属性的值表现不同，你需要找到提供该值的替代方式。一个简单的选项是将该值作为列表中的最后一个绑定元素包含进来。

**小心！**

例如，如果你为 `AddressBook` 应用程序创建一个 `NameConverter`，可以根据 `DisplayAsStyle` 枚举以不同的格式显示联系人的名和姓，XAML 可能如清单 18.7 所示。

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

若要创建额外的数据转换器并修改绑定以便在 `PhotoViewer` 应用程序中使用它们，请遵循以下步骤。

1. 如果您尚未这样做，请将列表 18.4 和列表 18.5 中显示的转换器添加到 `PhotoViewer` 应用程序中。
2. 为曝光模式、闪光模式、镜头光圈和焦距添加转换器。所有这些的 `ConvertBack` 方法都应返回 `Binding.DoNothing`，这指示绑定引擎不执行任何操作。对于曝光模式和闪光模式转换器，`Convert` 方法应返回代表枚举值的“友好”名称。镜头光圈值通常以“f值”表示，因此镜头光圈转换器的 `Convert` 方法应返回格式化为 `String.Format(“f / {0:#.#}”, value)` 的值。焦距转换器的 `Convert` 方法应返回格式化为 `String.Format(“{0} mm”, value)` 的值。
3. 修改 `Resources.xaml` 文件，将转换器作为资源添加。
4. 修改 `MainWindow.xaml` 文件，根据需要为 `Label` 元素添加适当的转换器。请记住，对于 `Size` 转换器，您需要使用 `MultiBinding`。
5. 运行应用程序并选择一个包含图像的目录。当您选择图像时，详细信息应发生变化并使用转换器进行显示。

## 绑定到集合

到目前为止，您一直在处理与单个对象的绑定。那么，显示所选目录中文件的列表框是如何绑定的？这是绑定到一个对象集合，具体来说，是在第 9 小时“处理数组和集合”中，您在 `MainWindow` 类中创建的 `PhotoCollection` 实例。通常，您会使用 `ItemsControl`（如 `ListBox`、`ListView` 或 `TreeView`）来显示集合，并将 `ItemsSource` 属性绑定到集合实例。默认情况下，`ItemsSource` 属性支持单向绑定。

列表 18.8 显示了 `PhotoViewer` 应用程序用于执行此操作的 XAML。

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

如果您希望集合能够被数据绑定引擎使用，以便插入或删除操作自动更新 UI 元素，则该集合必须实现 `System.Collections.Specialized.INotifyCollectionChanged` 接口。此接口定义了应在集合发生更改时引发的 `CollectionChanged` 事件。

WPF 提供了 `ObservableCollection<T>` 类，您将其用作 `PhotoCollection` 类的基础类，该类已经实现了 `INotifyCollectionChanged` 接口。除非您有高级场景并希望实现自己的集合用于数据绑定，否则应考虑使用 `ObservableCollection<T>`。

为了完全支持值传递，集合中支持可绑定属性的每个对象还必须实现 `INotifyPropertyChanged` 接口。

表 18.1 显示了为不同的源集合类型创建的默认视图。

### 表 18.1 默认视图

| **源集合类型** | **集合视图类型** | **备注** |
| :--- | :--- | :--- |
| IEnumerable | 基于 CollectionView 的内部类型 | 无法对项进行分组 |
| IList | ListCollectionView |  |
| IBindingList | BindingListCollectionView |  |

### 排序

集合视图允许您根据提供的比较条件对数据应用顺序或更改默认顺序。由于集合视图是基于客户端的数据视图，且不对底层集合进行任何更改，因此可以应用或移除排序，而无需重新查询集合内容。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_416_1.png)

### 创建 CollectionViewSource

您还可以使用 `CollectionViewSource` 直接在 XAML 中创建视图，它是继承自 `CollectionView` 的类的 XAML 代理，如下所示：

```xml
<Window.Resources>
    <CollectionViewSource x:Key="view" Source="{Binding Source={x:Static Application.Current}, Path=Contacts}" />
</Window.Resources>
```

这创建了一个名为 `view` 的新资源，该资源绑定到当前应用程序对象的 `Contacts` 集合。

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

`SortDescription` 结构体的 `propertyName` 参数支持通过“点”符号表示法引用嵌套属性。例如，要为 `Contact.XfnRelationships.Me` 属性创建 `SortDescription`，您需要为 `propertyName` 参数值使用：

`"XfnRelationships.Me"`

当对数据类型为枚举的属性进行排序时，项的顺序与枚举声明中的顺序相同。

### 顺便说一下

### 分组

除了用于查看 `IEnumerable` 集合的内部类之外，所有集合视图都支持分组功能。这允许用户将数据划分为逻辑组。组可以是显式的，即由用户决定；或者是隐式的，即组是根据数据动态生成的。

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

要为 `AddressBook` 应用程序添加筛选功能，以显示所有姓氏以字母“D”开头的联系人，请实现如列表 18.11 所示的方法。

### 列表 18.11 用于筛选的方法
