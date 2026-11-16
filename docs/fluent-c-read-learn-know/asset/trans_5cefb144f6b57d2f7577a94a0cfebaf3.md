

## 回到男孩们

回到第 1 章，我们了解过厨师需要的一个应用程序。当 Gordon 在拟定甜点菜单时，他需要能够从列表中选择一种食材，并查看库存数量和可用数量。是时候开始构建它了，或者至少是一个简单的版本。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_819_0.png)

- 食材类
  - 属性
    - 已分配
    - 可用
    - 描述
    - 名称
    - 库存
  - 方法
    - 食材

我们将用来跟踪食材的类如下...

| 字段 | 值 |
|---|---|
| 名称 | 奶油馅 |
| 描述 | |
| 库存 | 100 |
| 已分配 | 50 |
| 可用 | 50 |

...下面是我们将构建（并绑定）的表单。

### 动动脑筋

创建一个新项目，并添加 Ingredient 类声明。你可以对属性使用 C# 自动实现属性功能。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_819_1.png)

## 做得怎么样？

你需要回去检查语法吗？没关系；我们已经有一段时间没这么做了。重要的是，你让它运行起来了。

```csharp
public class Ingredient
{
    public Ingredient(string name, int onHand, int allocated)
    {
        this.Name = name;
        this.OnHand = onHand;
        this.Allocated = allocated;
        this.Available = OnHand - Allocated;
    }

    public string Name { get; set; }

    public string Description { get; set; }

    public int OnHand { get; set; }

    public int Allocated { get; set; }

    public int Available { get; set; }
}
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_820_0.png)

### 独立练习

继续构建上一页所示的窗口。我敢说你能做得比我的更漂亮。

## 构建可绑定集合

要让我们的应用程序运行起来，我们不需要该类的单个实例，而是需要一个集合。你知道更改通知是 WPF 绑定的核心，因此在构建要用作绑定源的自定义项集合时，你需要实现它。你可以手动实现 INotifyCollectionChanged 接口，这并不困难，因为它只有一个方法，但有一种更简单的方法——System.Collections.ObjectModel 命名空间中的 ObservableCollection<T> 泛型可以为你完成所有工作。你只需要从 ObservableCollection<T> 派生一个类，添加你的项目，就可以开始了。

### 从 ObservableCollection<T> 派生一个类：

```csharp
class MyBindable : ObservableCollection<MyType>
{
    : base()
    {
        ... properties or methods unique to your
        class...
    }
}
```

你需要调用基类的构造函数。

### 实例化类并添加项：

```csharp
public MyBindable items = new MyBindable();
items.Add(new MyType());
```

你不必将可观察集合分配给 DataContext；你可以使用任何有效的 XAML 语法来引用它，但 DataContext 通常是最简单的方法。

### 实例可用于绑定：

```csharp
this.DataContext = MyBindable;
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_821_0.png)

### 动动脑筋

向项目中添加一个名为 SampleIngredients 的 ObservableCollection 类。在构造函数中，向集合添加三个或四个 Ingredient。

然后编写代码，在 MainWindow() 构造函数中实例化集合并设置 Window.DataContext。最后，绑定 ListBox。运行应用程序时，ListBox 的内容看起来会很奇怪；这并不意味着你做错了什么。我们马上就会修复它。

## 做得怎么样？

当然，如果你为添加到 SampleIngredients 集合中的 Ingredient 实例选择不同的值，也没关系。

### 这是集合类：

```csharp
public class SampleIngredients : ObservableCollection<Ingredient>
{
    public SampleIngredients() : base()
    {
        Add(new Ingredient("Pastry Cream", 100, 50));
        Add(new Ingredient("Genoise Layers", 10, 0));
        Add(new Ingredient("Chocolate Ganache", 50, 35));
    }
}
```

### 这是设置 DataContext 的代码：

```csharp
public MainWindow()
{
    InitializeComponent();

    SampleIngredients Ingredients = new SampleIngredients();
    this.DataContext = Ingredients;
}
```

### 最后，这是绑定 ListBox 的 XAML：

```xml
<ListBox ... ItemsSource="{Binding}" />
```

但这并不是我们真正想要的，对吧？

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_822_0.png)

## 更多模板

默认情况下，ListBox（或任何项控件）通过调用 ToString() 来显示其内容，如果你不在类中重写 ToString() 方法（我们也没有），它只会返回类名。这作为该方法的默认行为并不糟糕，但这几乎从来不是你希望 ListBox 做的事情。当然，答案是告诉 ListBox 你*确实*希望它做什么。

如果你在 WPF 类库中搜索一下，你会发现几个具有以单词“Template”结尾的属性的对象。就像我们在上一章中学习的控件模板一样，所有这些属性都接受从抽象 FrameworkTemplate 类派生的类的实例，并且它们的工作原理基本相同。（但只有控件模板支持 VisualStateManager。）

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_823_0.png)

我们在上一章中探索了控件模板。

ItemsPanelTemplate 定义项控件用于显示其内容的面板。

DataTemplate 定义项本身的可视化树。在模板内部，你将控件绑定到要显示的属性的 Path。

### 动动脑筋

你能将 ListBox 的 ItemTemplate 属性设置为一个 DataTemplate，以在 Label 中显示每个 Ingredient 的名称吗？

## 做得怎么样？

我总是忘记必须在 ItemTemplate 内部声明 DataTemplate，所以如果你在这方面遇到困难，你并不孤单。

```xml
<ListBox ... ItemsSource="{Binding}" >
    <ListBox.ItemTemplate>
        <DataTemplate>
            <Label Content="{Binding Path=Name}" />
        </DataTemplate>
    </ListBox.ItemTemplate>
</ListBox>
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_824_0.png)

这样就好多了！

### 请注意

- 你在 DataTemplate 中定义的可视化树将应用于控件 Items 集合中的每个项。
- 尽管我们的示例非常简单，但你可以根据需要使模板尽可能复杂。ItemTemplate 也不支持 VisualStateManager，但正如我们将看到的，你可以使用触发器来控制应用程序的可视化行为。
- 我们将模板直接放在控件声明中，但当然它也可以包含在控件模板中。

## 数据触发器

就像 ControlTemplate 一样，DataTemplate 包含一个 Triggers 集合。理论上，两个集合都可以包含任何类型的触发器，但 DataTemplate 最常包含 DataTrigger 或 MultiDataTrigger 的实例。与由依赖属性的值激活的属性触发器不同，DataTrigger 由 Binding 的值激活，这不仅意味着它特别适合在数据模板中使用，还意味着数据触发器可以由任何可用作绑定源的内容激活，而不仅仅是依赖属性。

```xml
<DataTemplate>
  <Label x:Name="itemLabel" ... />
  <DataTemplate.Triggers>
    <DataTrigger Binding="{Binding Path=...}" Value="...">
      <Setter Property="..." Value="..." TargetName="itemLabel" />
    </DataTrigger>
  </DataTemplate.Triggers>
</DataTemplate>
```

触发器 Path 中指定的属性不需要在模板可视化树中使用。

使用 DataTrigger 时有个棘手的地方。你需要设置 TargetName 属性。由于你通常会更改模板可视化树中的某个内容，因此需要为该元素命名。

### 动动脑筋

向项目中添加一个 DataTemplate，当可用数量为零时，将模板标签的文本显示为红色。你可能需要更改示例 Ingredient 类的构造函数，以便拥有一个符合条件的 Ingredient。（我已经这么做了。）

