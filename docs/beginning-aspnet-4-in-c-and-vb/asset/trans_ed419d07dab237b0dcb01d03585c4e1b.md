

完成所有这些更改后，您可以编译程序集，然后创建一个新的工作流项目。若要将该活动添加到工具箱，请打开一个工作流，然后显示工具箱的上下文菜单并单击“选择项”。

然后，您可以浏览包含该活动的程序集，一旦将其添加到工具箱中，它的外观将类似于图 57-12。图标有点不完美，但已经足够接近了。

![](img/d7d2ffa0a76feaab821930e95daace93_1828_0.png)

在下一节关于自定义复合活动的内容中，您将再次看到 ActivityToolboxItem，因为该类提供了一些额外的功能，只有在将复合活动添加到设计图面时才需要这些功能。

回顾一下，您创建了自定义的 WriteLineActivity，通过创建 WriteLineValidator 添加了验证逻辑，使用 WriteLineDesigner 和 WriteLineTheme 类创建了设计器和主题，为活动创建了位图，最后创建了 WriteLineToolboxItem 类来修改活动的显示名称。

## 自定义复合活动

活动有两种主要类型。从 Activity 派生的活动可以被视为工作流中的可调用函数。从 CompositeActivity 派生的活动（如 ParallelActivity、IfElseActivity 和 ListenActivity）是其他活动的容器。它们的设计时行为与简单活动有很大不同，因为它们会在设计器上呈现一个区域，供子活动放置。

在本节中，您将创建一个可称为 DaysOfWeekActivity 的活动。此活动可用于根据当前日期执行工作流的不同部分。例如，对于周末到达的订单，您可能需要执行与工作日到达的订单不同的工作流路径。在此示例中，您将了解一些高级工作流主题，到本节结束时，您应该会很好地理解如何使用自己的复合活动扩展系统。此示例的代码也包含在 03 CustomActivities 解决方案中。

首先，您创建一个自定义活动，该活动具有一个默认值为当前日期/时间的属性。您将允许将该属性设置为另一个值，该值可以来自工作流中的另一个活动，也可以来自工作流执行时传递给它的参数。此复合活动将包含多个分支——这些分支将由用户定义。每个分支都将包含一个枚举常量，用于定义该分支将在哪一天（或哪些天）执行。以下示例定义了该活动及两个分支：

```
DaysOfWeekActivity
  SequenceActivity: Monday, Tuesday, Wednesday, Thursday, Friday
    <other activities as appropriate>
  SequenceActivity: Saturday, Sunday
    <other activities as appropriate>
```

对于此示例，您需要一个定义星期几的枚举——该枚举将包含 [Flags] 特性（因此您不能使用 System 命名空间中定义的内置 DayOfWeek 枚举，因为它不包含 [Flags] 特性）。

```csharp
[Flags]
[Editor(typeof(FlagsEnumEditor), typeof(UITypeEditor))]
public enum WeekdayEnum: byte
{
    None = 0x00,
    Sunday = 0x01,
    Monday = 0x02,
    Tuesday = 0x04,
    Wednesday = 0x08,
    Thursday = 0x10,
    Friday = 0x20,
    Saturday = 0x40
}
```

此外，还包含一个用于此类型的自定义编辑器，该编辑器允许您根据复选框选择枚举值。此代码可在下载中找到。

定义好枚举类型后，您就可以初步尝试实现该活动本身。自定义复合活动通常派生自 CompositeActivity 类，因为该类除其他功能外，还定义了一个 Activities 属性，该属性是所有从属活动的集合。

```csharp
public class DaysOfWeekActivity: CompositeActivity
{
    /// <summary>
    /// Get/Set the day of week property
    /// </summary>
    [Browsable(true)]
    [Category("Behavior")]
    [Description("Bind to a DateTime property, set a specific date time, or leave blank for DateTime.Now")]
    [DefaultValue(typeof(DateTime), "*")]
    public DateTime Date
    {
        get { return (DateTime)base.GetValue(DaysOfWeekActivity.DateProperty); }
        set { base.SetValue(DaysOfWeekActivity.DateProperty, value); }
    }

    /// <summary>
    /// Register the DayOfWeek property
    /// </summary>
    public static DependencyProperty DateProperty =
        DependencyProperty.Register("Date", typeof(DateTime),
            typeof(DaysOfWeekActivity));
}
```

Date 属性提供了常规的 getter 和 setter，我们还添加了许多标准特性，以便它在属性浏览器中正确显示。不过，这段代码看起来与普通的 .NET 属性有些不同，因为 getter 和 setter 不是使用标准字段来存储它们的值，而是使用所谓的 DependencyProperty。

Activity 类（因此也包括此类，因为它最终派生自 Activity）派生自 DependencyObject 类，此类定义了一个以 DependencyProperty 为键的值字典。WF 使用这种获取/设置属性值的间接方式来实现绑定；也就是说，将一个活动的属性链接到另一个活动的属性。例如，在代码中传入传出参数是很常见的，有时按值传递，有时按引用传递。WF 使用绑定将属性值链接在一起——因此在此示例中，您可能在工作流上定义了一个 DateTime 属性，而该活动可能需要在运行时绑定到该值。在本章后面，您将看到一个绑定的示例。

如果您生成此活动，它不会做太多事情；实际上，它甚至不允许将子活动放置到其中，因为您还没有为活动定义 Designer 类。

## 添加设计器

正如您在本章前面看到的 WriteLineActivity，每个活动都可以有一个关联的 Designer 类，用于更改该活动的设计时行为。您在 WriteLineActivity 中看到了一个空白的 Designer，但对于复合活动，您需要重写几个方法以添加一些特殊处理：

```csharp
public class DaysOfWeekDesigner: ParallelActivityDesigner
{
    public override bool CanInsertActivities
    (HitTestInfo insertLocation, ReadOnlyCollection<Activity> activities)
    {
        foreach (Activity act in activities)
```

除了定义依赖属性之外，您还需要用于在任意活动上获取和设置该值的方法。这些方法通常定义为复合活动上的静态方法，如以下代码所示：

```csharp
public static void SetWeekday(Activity activity, object value)
{
    if (null == activity)
        throw new ArgumentNullException("activity");
    if (null == value)
        throw new ArgumentNullException("value");

    activity.SetValue(DaysOfWeekActivity.WeekdayProperty, value);
}

public static object GetWeekday(Activity activity)
{
    if (null == activity)
        throw new ArgumentNullException("activity");

    return activity.GetValue(DaysOfWeekActivity.WeekdayProperty);
}
```

您还需要进行另外两项更改，才能使这个额外的属性附加到 SequenceActivity 上显示出来。第一项是创建扩展程序提供程序（extender provider），告诉 Visual Studio 将额外属性包含在 sequence activity 中。第二项是注册此提供程序，这可以通过重写 Activity 设计器的 Initialize 方法并添加以下代码来完成：

```csharp
protected override void Initialize(Activity activity)
{
    base.Initialize(activity);
    IExtenderListService iels = base.GetService(typeof(IExtenderListService))
        as IExtenderListService;

    if (null != iels)
    {
        bool extenderExists = false;
        foreach (IExtenderProvider provider in iels.GetExtenderProviders())
        {
            if (provider.GetType() == typeof(WeekdayExtenderProvider))
            {
                extenderExists = true;
                break;
            }
        }
        if (!extenderExists)
        {
            IExtenderProviderService ieps =
                base.GetService(typeof(IExtenderProviderService))
                as IExtenderProviderService;
            if (null != ieps)
                ieps.AddExtenderProvider(new WeekdayExtenderProvider());
        }
    }
}
```

前面代码中对 GetService 的调用允许自定义 Designer 查询宿主（此处为 Visual Studio）提供的服务。您向 Visual Studio 查询 IExtenderListService，它提供了一种枚举所有可用扩展程序提供程序的方法；如果未找到 WeekdayExtenderProvider 服务的实例，则查询 IExtenderProviderService 并添加新的提供程序。

