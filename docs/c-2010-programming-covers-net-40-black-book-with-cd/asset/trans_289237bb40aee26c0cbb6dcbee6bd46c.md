

## 复合几何

复合几何类包括 GeometryGroup 和 CombinedGeometry 类。你也可以通过调用 Geometry 类的静态方法 Combine() 来创建复合几何。复合几何类及其功能在表 12.16 中列出：

表 12.16：复合几何类

| Class | Description |
|---|---|
| GeometryGroup | 指复合几何对象 |
| CombinedGeometry | 合并两个几何体定义的区域 |

GeometryGroup 类表示一个复合几何体，其中包含其他 Geometry 对象。GeometryGroup 类可从任意数量的几何对象创建复合几何体。你可以使用 GeometryGroup 类的 FillRule 属性来指定几何体的组合方式。

另一方面，CombinedGeometry 类表示由两个 Geometry 对象组合定义的 2-D 几何形状。你可以使用 CombinedGeometry 类的 GeometryCombineMode 属性来指定两个几何体应如何组合。GeometryCombineMode 属性的值可以设置为：Union、Intersect、Exclude 或 Xor。

## WPF 中的画刷

在 WPF 中，你可以使用画刷为元素应用背景和前景颜色。WPF 中的画刷用于绘制各种形状。这些画刷派生自 Freezable 基类并支持更改通知。例如，如果你更改一个画刷，使用该画刷的元素会重新绘制自身。WPF 中的画刷在 Brush 类中定义，该类定义在 System.Windows.Media.Brush 命名空间中。WPF 中可用的不同类型的画刷在表 12.17 中列出：

表 12.17：画刷类

| Class | Description |
|---|---|
| SolidColorBrush | 用纯色绘制区域 |
| LinearGradientBrush | 用线性渐变绘制区域 |
| RadialGradientBrush | 用径向渐变绘制区域 |
| DrawingBrush | 用绘图绘制区域 |
| ImageBrush | 用图像绘制区域 |
| VisualBrush | 用可视对象绘制区域 |

Brush 类的继承层次结构如下：

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Freezable
        System.Windows.Media.Animation.Animatable
          System.Windows.Media.Brush
```

Brush 类的重要属性在表 12.18 中列出：

表 12.18：Brush 类的属性

| Property | Description |
|---|---|
| CanFreeze | 检索一个值，该值指示对象是否可以被设为不可修改 |
| DependencyObjectType | 检索一个值，该值包装此实例的 CLR 类型 |
| Dispatcher | 检索与 DispatcherObject 类关联的值 |
| HasAnimatedProperties | 检索一个值，该值指示是否有一个或多个 AnimationClock 对象与此对象的任何依赖属性关联 |
| IsFrozen | 检索一个值，该值指示对象当前是否可修改 |
| IsSealed | 检索一个值，该值声明此实例当前是否为只读 |
| Opacity | 检索或设置 Brush 对象的透明度程度 |
| RelativeTransform | 检索或设置使用相对坐标应用于画刷的变换 |
| Transform | 获取或设置应用于画刷的变换 |

有助于制作 WPF 应用程序的不同类型的画刷如下：

- SolidColorBrush
- LinearGradientBrush
- RadialGradientBrush
- DrawingBrush
- ImageBrush
- VisualBrush

这些类型的画刷将在后面的章节中讨论。

## SolidColorBrush 类

SolidColorBrush 类定义了单一颜色的画刷。它用于用单一颜色填充图形形状，例如矩形、椭圆、多边形和路径。你可以通过将 Background 属性设置为定义纯色的字符串来定义纯色。你可以使用预定义的系统画刷，例如 Red、Blue 或 Yellow 来用纯色绘制区域。你可以通过添加以下代码将 SolidColorBrush 对象添加到你的应用程序中：

```
<SolidColorBrush .../>
```

SolidColorBrush 类的继承层次结构如下：

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Freezable
        System.Windows.Media.Animation.Animatable
          System.Windows.Media.Brush
            System.Windows.Media.SolidColorBrush
```

SolidColorBrush 类的重要属性在表 12.19 中列出：

表 12.19：SolidColorBrush 类的属性

| Property | Description |
|---|---|
| Color | 获取或设置当前 SolidColorBrush 对象的颜色 |

## LinearGradientBrush 类

LinearGradientBrush 类用于创建绘制区域的画刷，该区域具有线性渐变，即从一种颜色逐渐变为另一种颜色的渐变填充。它对元素应用平滑的颜色变化，并创建混合填充。LinearGradientBrush 类定义 StartPoint 和 EndPoint 属性。它们为应用线性渐变分配 2-D 坐标。StartPoint 属性的默认值是 0，EndPoint 属性是 1，这会创建对角渐变。这些属性允许你选择第一个颜色开始变化的点以及颜色变化以最终颜色结束的点。要创建渐变，你需要为每种颜色添加 GradientStops 属性，并使用 0 到 1 的 Offset 值将每种颜色放置在你的渐变中。你可以通过添加以下代码片段将 LinearGradientBrush 对象添加到你的应用程序中：

```
<LinearGradientBrush>
<!-- GradientStops -->
</LinearGradientBrush>
```

LinearGradientBrush 类的继承层次结构如下：

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Freezable
        System.Windows.Media.Animation.Animatable
          System.Windows.Media.Brush
            System.Windows.Media.GradientBrush
              System.Windows.Media.LinearGradientBrush
```

LinearGradientBrush 类的重要属性在表 12.20 中列出：

表 12.20：LinearGradientBrush 类的属性

| Property | Description |
|---|---|
| ColorInterpolationMode | 获取或设置 ColorInterpolationMode 枚举，该枚举指定渐变颜色的插值方式 |
| EndPoint | 获取或设置线性渐变的结束 2-D 坐标 |
| GradientStops | 获取或设置画刷的渐变停止点 |
| MappingMode | 获取或设置 BrushMappingMode 枚举，该枚举指定渐变画刷的定位坐标是相对于输出区域绝对还是相对 |
| SpreadMethod | 获取或设置扩散方法类型，该方法指定如何在要绘制的对象边界内开始或结束绘制渐变 |
| StartPoint | 获取或设置线性渐变的起始 2-D 坐标 |

## RadialGradientBrush 类

RadialGradientBrush 类与 LinearGradientBrush 类相似，因为它用渐变填充填充区域。区别在于渐变的应用方式。RadialGradientBrush 类填充的渐变以圆形模式从中心点向外辐射。你可以使用 GradientOrigin 属性来标识渐变中第一个颜色开始的点。GradientOrigin 属性的默认值是 0.5，表示填充区域的中间。渐变从 GradientOrigin 属性中的点以圆形方式向外辐射，这是起始点。RadialGradientBrush 类是填充圆形形状和创建光照效果的良好选择。你可以通过添加以下代码片段将 RadialGradientBrush 对象添加到你的应用程序中：

```
<RadialGradientBrush>
<!-- GradientStops -->
</RadialGradientBrush>
```

RadialGradientBrush 类的继承层次结构如下：

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Freezable
        System.Windows.Media.Animation.Animatable
          System.Windows.Media.Brush
            System.Windows.Media.GradientBrush
              System.Windows.Media.RadialGradientBrush
```

RadialGradientBrush 类的重要属性在表 12.21 中列出：

表 12.21：RadialGradientBrush 类的属性

| Property | Description |
|---|---|
| Center | 获取或设置径向渐变最外层圆的中心 |

