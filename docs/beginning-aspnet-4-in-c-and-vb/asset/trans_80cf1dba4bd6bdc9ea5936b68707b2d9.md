
要查看导航的实际效果，请创建一个新的 Visual Studio 2010 项目，类型为 Silverlight Navigation Application，命名为 EventRegistration。该项目模板包含预定义的样式、一个主页面以及位于 Views 文件夹中可进行导航的几个页面。

MainPage.xaml 包含一个 Frame 元素。该元素以 navigation 别名前缀，其引用程序集 System.Windows.Controls.Navigation 中的 .NET 命名空间 System.Windows.Controls。 这里使用的另一个别名是 uriMapper，其引用同一程序集中的 .NET 命名空间 System.Windows.Navigation。 Frame 元素用作不同页面的父容器。 通过设置 Source 属性，将首次加载的页面从默认页面更改为 /Welcome 页面。 UriMapper 类将 URI 转换为对象。因此，无需指定 /Views/Welcome.xaml 作为导航源页面，只需 /Welcome 即可，并将其翻译为 Views 目录中的 Welcome.xaml 文件。

全部样式在此引用均定义为文件 Styles.xaml 中的资源。该文件已添加到 App.xaml 中的应用程序资源文件。

```
<Border x:Name="ContentBorder" Style="{StaticResource ContentBorderStyle}">
<navigation:Frame x:Name="ContentFrame"
Style="{StaticResource ContentFrameStyle}"
Source="/Welcome" Navigated="ContentFrame_Navigated"
NavigationFailed="ContentFrame_NavigationFailed">
<navigation:Frame.UriMapper>
<uriMapper:UriMapper>
<uriMapper:UriMapping Uri="" MappedUri="/Views/Home.xaml"/>
<uriMapper:UriMapping Uri="/{pageName}" MappedUri="/Views/{pageName}.xaml"/>
</uriMapper:UriMapper>
</navigation:Frame.UriMapper>
</navigation:Frame>
</Border>
```

*代码片段 WCFRegistration/MainPage.xaml*

MainPage.xaml 包含徽标和应用程序名称部分，以及 HyperlinkButton 控件以让用户在应用程序的主页面之间导航。徽标使用资源 LogoIcon 指定，该资源在文件 Styles.xaml 中使用 Path 元素定义。 HyperlinkButton 元素的样式也在样式文件中定义。 NavigateUri 属性被设置为一个 Uri，该 Uri 使用前面所示的 UriMapper 定义进行映射。

```
<Grid x:Name="NavigationGrid" Style="{StaticResource NavigationGridStyle}">
<Border x:Name="BrandingBorder"
Style="{StaticResource BrandingBorderStyle}">
<StackPanel x:Name="BrandingStackPanel"
Style="{StaticResource BrandingStackPanelStyle}">
<ContentControl x:Name="LogoIcon"/>
<TextBlock x:Name="ApplicationNameTextBlock"
Style="{StaticResource ApplicationNameStyle}"
Text="CN Innovation"/>
</StackPanel>
</Border>
<Border x:Name="LinksBorder" Style="{StaticResource LinksBorderStyle}">
<StackPanel x:Name="LinksStackPanel"
Style="{StaticResource LinksStackPanelStyle}">
<HyperlinkButton x:Name="Link1"
Style="{StaticResource LinkStyle}"
NavigateUri="/Home" TargetName="ContentFrame"
Content="home"/>
<Rectangle x:Name="Divider1"
Style="{StaticResource DividerStyle}"/>
<HyperlinkButton x:Name="Link2"
Style="{StaticResource LinkStyle}"
NavigateUri="/About" TargetName="ContentFrame"
Content="about"/>

</StackPanel>
</Border>
</Grid>
```

由于 Frame 元素的 Source 属性直接引用它，因此在加载 Silverlight 控件时显示 Welcome 页面。 该页面仅包含一个 TextBlock 元素，其中包含有关应用程序的信息，该元素包含在 Border 元素中以定义一些视觉效果，而 Border 元素又包含在 Canvas 元素中用于定位。

```
<navigation:Page x:Class="Wrox.ProCSharp.Silverlight.Views.Welcome"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
xmlns:navigation="clr-namespace:System.Windows.Controls.Navigation;
assembly=System.Windows.Controls.Navigation"
Title="Welcome Page">
<Canvas x:Name="LayoutRoot">
<Canvas.Resources>
<!-- Storyboard Resources -->
</Canvas.Resources>
<Border x:Name="border1" Canvas.Left="0" Canvas.Top="0" Width="240"
Height="90" CornerRadius="9">
<Border.Effect>
<DropShadowEffect ShadowDepth="7" BlurRadius="3"
Color="DarkGreen" />
</Border.Effect>
<Border.Background>
<LinearGradientBrush StartPoint="0.5,0" EndPoint="0.5,1">
<GradientStop x:Name="gradient1" Offset="0"
Color="DarkGreen" />
<GradientStop x:Name="gradient2" Offset="0.4" Color="Green" />
<GradientStop x:Name="gradient3" Offset="0.7"
Color="MediumSeaGreen" />
<GradientStop x:Name="gradient4" Offset="0.9"
Color="LightGreen" />
</LinearGradientBrush>
</Border.Background>
<TextBlock HorizontalAlignment="Center" VerticalAlignment="Center"
Text="Event Registration" FontFamily="Comic Sans MS"
FontSize="24" Foreground="Wheat" />
</Border>
</Canvas>
</navigation:Page>
```

代码片段 WCFRegistration/Views/Welcome.xaml

在 Canvas 元素的 Resources 部分中，定义了两个 Storyboard 元素以执行动画。 这与你在第 35 章中看到的 WPF 动画非常相似。 在动画方面可以检测到这两种技术之间的细微差异；例如，Silverlight 中的动画不定义你在 WPF 中熟悉的 AccelerationRatio 和 DecelerationRatio 属性。 然而，你可以使用关键帧动画或缓动函数获得相同的功能。 缓动函数在 Silverlight 中出现早于 WPF，后者在 .NET 4 中扩展以包含此功能。

```
<Canvas.Resources>
<Storyboard x:Name="startStoryboard">
<DoubleAnimation From="0" To="400" Duration="00:00:4"
Storyboard.TargetName="border1"
Storyboard.TargetProperty="(Canvas.Left)">
<DoubleAnimation.EasingFunction>
    <CircleEase EasingMode="EaseIn" />
</DoubleAnimation.EasingFunction>
</DoubleAnimation>
<DoubleAnimation From="0" To="300" Duration="00:00:4"
    Storyboard.TargetName="border1"
    Storyboard.TargetProperty="(Canvas.Top)">
    <DoubleAnimation.EasingFunction>
        <BounceEase Bounces="4" EasingMode="EaseIn" />
    </DoubleAnimation.EasingFunction>
</DoubleAnimation>
</Storyboard>
<Storyboard x:Name="endStoryboard">
    <DoubleAnimation To="50" Duration="00:00:4"
        Storyboard.TargetName="border1"
        Storyboard.TargetProperty="(Canvas.Left)">
        <DoubleAnimation.EasingFunction>
            <CircleEase EasingMode="EaseOut" />
        </DoubleAnimation.EasingFunction>
    </DoubleAnimation>
    <DoubleAnimation To="50" Duration="00:00:4"
        Storyboard.TargetName="border1"
        Storyboard.TargetProperty="(Canvas.Top)">
        <DoubleAnimation.EasingFunction>
            <ElasticEase EasingMode="EaseOut" Springiness="4"
                Oscillations="3" />
        </DoubleAnimation.EasingFunction>
    </DoubleAnimation>
    <ColorAnimation Duration="00:00:4"
        Storyboard.TargetName="gradient1"
        Storyboard.TargetProperty="Color" To="DarkBlue" />
    <ColorAnimation Duration="00:00:4"
        Storyboard.TargetName="gradient2"
        Storyboard.TargetProperty="Color" To="Blue" />
    <ColorAnimation Duration="00:00:4"
        Storyboard.TargetName="gradient3"
        Storyboard.TargetProperty="Color"
        To="MediumBlue" />
    <ColorAnimation Duration="00:00:4"
        Storyboard.TargetName="gradient4"
        Storyboard.TargetProperty="Color" To="LightBlue" />
    <DoubleAnimation Duration="00:00:4" BeginTime="00:00:2"
        Storyboard.TargetName="border1"
        Storyboard.TargetProperty="Width" To="500" />
    <DoubleAnimation Duration="00:00:4" BeginTime="00:00:2"
        Storyboard.TargetName="border1"
        Storyboard.TargetProperty="Height" To="300" />
</Storyboard>
</Canvas.Resources>
```

![](img/d7d2ffa0a76feaab821930e95daace93_1161_0.png)

第一个故事板动画 startStoryboard 在 OnNavigateTo 事件处理程序中通过调用 Begin() 方法启动。 第一个故事板动画的 Completed 事件被设置为 Lambda 表达式，以便在第一个完成后启动第二个故事板 endStoryboard。 当第二个故事板完成后，使用 NavigationService.Navigate() 导航到 Home 页面。
