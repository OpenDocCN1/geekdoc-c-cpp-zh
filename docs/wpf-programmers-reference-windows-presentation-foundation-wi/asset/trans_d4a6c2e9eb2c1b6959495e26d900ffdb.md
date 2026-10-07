
# 第 13 章

第 13 章包含以下示例程序：

-   ButtonResources — 显示类似按钮的矩形，与 ButtonValues 程序显示的类似，但它使用了 Resources 来使代码更具一致性。类似于图 13-1。[第第 213-215 页]。
-   ButtonStyles — 显示类似按钮的矩形，与 ButtonValues 程序显示的类似，但它使用了 Styles 来使代码更加简单且易于维护。类似于图 13-1。[第第 220, 221, 226, 229 页]。
-   Values — 通过为每个按钮选择单独的属性值来显示类似按钮的矩形。图 13-1。[第 213 页]。
-   ControlStyle — 使用各种 Styles 的两个 Buttons 和一个 Label。一个 Button 和 Label 共享相同的 Style。图 13-3。[第 220 页]。
-   ImageTriggers — 显示一组 Opacity = 0.5 的 Images 和 Labels。当 IsMouseOver 为 True 时，触发器会将 Opacity 更改为 1，并将控件的 LayoutTransform 属性设置为一个 ScaleTransform 对象，以放大控件。图 13-10。[第 231 页]。
-   InheritedStyles — 演示使用 BasedOn 关键字相互继承的 Styles。图 13-6。[第 226 页]。
-   IsActiveTrigger — 在 Window 的 IsActive 属性和 TextBox 的 Focused 属性上使用 Triggers。图 13-11。[第 233 页]。
-   MouseOverTriggers — 演示在 Button MouseOver 属性上使用 Triggers，以便在鼠标悬停时时放大 Button。图 13-8。[第 230 页]。
-   LabelAndRectangle — 显示共享相同 Style 的 Button、Label 和 Rectangle。图 13-4。[第 221 页]。
-   MenuMouseOverTriggers — 使用 MenuItem MouseOver 触发器来更改 MenuItem 的 LayoutTransform 和 BitmapEffect 属性。图 13-9。[第 231 页]。
-   RedRectangles — 使用命名样式来设置矩形的属性。图 13-2。[第 217 页]。
-   TextTriggers — 演示 TextBox 和 ComboBox Text 属性上的 Triggers 以高
-   AnimatedText — 演示使用 StringUsingKeyFrames 对象使文本一次出现几个字符。图 14-10。[第 254 页]。
-   AnimationWithoutStories — 使用后台代码（code-behind）来动画 Ell 的 Canvas.Left 和 Canvas.Top 属性。图 14-12。[第 259 页]。
-   BouncingBall — 显示一个在接触“地面”时播放声音的跳球。演示了样曲线关键帧和 ParallelTimeline 对象以播放带有声音的反向动画。图 14-11。[第 258 页]。
-   CentralizedTriggers — 使用集中在 Canvas 中的 EventTriggers 来处理 Canvas 中控件发起的 MouseLeftButton 事件。图 14-2。[第 238 页]。
-   GrowingButtons — 演示了带有 Setters 的属性触发器、带有 Storyboards 的属性触发器以及带有 Storyboards 的事件触发器这三者的组合。图 14-4。[第 243 页]。
-   JumpingButton — 显示了一个动画单个控件属性的非常简单的 Storyboard 代码是有多复杂。[第 261 页]。
-   ToggleButton — 演示了一个在 EnterActions 和 ExitActions 部分中执行 Storyboards 的属性触发器。图 14-3。[第 242 页]。
-   RepeatingSound — 运行一个播放声音的动画。[第 257 页]。
-   RovingButton — 显示一个遵循矩形路径的 Button。演示了启动、暂停、恢复、停止和移除 Storyboard 的方法。图 14-6。[第 248 页]。
-   RovingDiscrete — 显示一个离散跳转遵循矩形路径的 Button。演示了启动、暂停、恢复、停止和移除 Storyboard 的方法。类似于图 14-6。[第 251 页]。
-   RovingMixedKeyFrames — 使用线性关键帧、离散关键帧、路径动画和简单的线性动画使 Button 遵循路径。演示了启动、暂停、恢复、停止和移除 Storyboard 的方法。图 14-9。[第 252 页]。
-   RovingWithKeyFrames — 使用带有线性关键帧的 DoubleAnimationUsingKeyFrames 对象使按钮遵循矩形路径。演示了启动、暂停、恢复、停止和移除 Storyboard 的方法。类似于图 14-6。[第 249 页]。
-   RovingWithPath — 显示一个遵循路径的 Button。演示了启动、暂停、恢复、停止和移除 Storyboard 的方法。图 14-8。[第 251 页]。
-   RovingWithSplines — 使用带有样条关键帧的 DoubleAnimationUsingKeyFrames 对象使按钮遵循矩形路径。按钮在跨越路径的每一侧时缓慢开始、加速，然后在角处减速。类似于图 14-6。[第 250 页]。
-   SoundEvents — 用户点击按钮或鼠标悬停在第二个按钮上时播放声音。[第 256 页]。
-   SpinButton — 使按钮在点击时旋转 360 度。演示了作为资源的 Storyboard。图 14-1。[第 237 页]。
-   SplineGraph — 显示带有控制点的样条曲线图。图 14-7。[第 249 页]。

# 第 15 章

第 15 章包含以下示例程序：

-   BetterLabelTemplate — 演示尊重客户端 Background、BorderBrush、BorderThickness、HorizontalAlignment 和 VerticalContentAlignment 属性的 Label 温度。图 15-3。[第 266 页]。
-   DisabledLabelTemplate — 演示当 Label 禁用时显示多行文本和独特外观的 Label 温度。图 15-5。[第 268 页]。
-   EllipseButton — 演示对正常、禁用默认按钮使用不同外观的椭圆形 Button。鼠标悬停在按钮上时使用动画显示“闪烁”高亮。图 15-9 到 15-12。[第 275–277 页]。
-   GlassButton — 演示对正常、禁用和默认按钮使用不同外观的半透明 Button。图 15-6 到 15-8。[第 270–271 页]。
-   InterestingLabelTemplates — 演示两个 Label 温度——一个显示边框，另一个显示多行文本。图 15-4。[第 266 页]。
-   ShowTemplate — 显示控件默认模板的 XAML 代码。图 15-13。[第 281 页]。
-   SimpleLabelTemplate — 演示带有预设画刷的简单 Label 温度。图 15-2。[第 265 页]。
-   SliderParts — 此程序仅显示一个 Slider，很容易看到它的部分。图 15-1。[第 263 页]。

# 第 16 章

第 16 章包含以下示例程序：

-   AnimatedSkins — 通过动画属性值让用户切换皮肤，使用户看到一种皮肤变成另一种。图 16-9 到 16-11。[第 295-296 页]。
-   OrderTracking — 使用资源字典为不同的用户显示三种皮肤之一。图 16-7。[第 289 页]。
-   ShowThemes — 使用 RelativeSource = FindAncestor 的绑定显示 Aero、Luna 和 Royale 主题。图 16-1 和 16-3。[第 284 页]。
-   SkinInterfaces — 让用户在运行时加载 XAML 来切换皮肤。图 16-12。[第 298 页]。
-   Skins — 让用户在运行时加载资源文件来切换皮肤。图 16-8。[第 293 页]。

