

```csharp
if (PreviousExecutionState == ApplicationExecutionState.Terminated)
{
    // TODO: 从之前挂起的应用程序加载状态
    // 将 frame 放入当前窗口
    Window.Current.Content = frame;
}

if (PreviousActivated == false)
{
    if (frame.Content == null)
    {
        /// <summary>
        /// 当导航栈未恢复时，导航到第一页，
        /// 通过传递必需信息作为导航参数来配置新页面
        /// <param name="navigation">MainPage 的类型</param>
        frame.Navigate(typeof(MainPage), e.Arguments);
    }
    // 确保当前窗口处于激活状态
    Window.Current.Activate();
}

/// <summary>
/// 当导航到特定页面失败时
/// </summary>
/// <summary>
/// 导航失败的 frame
/// <param name="sender">关于导航失败的详细信息</param>
/// <param name="e">详情</param>
/// </summary>
private void OnNavigationFailed(object sender, NavigationFailedEventArgs e)
{
    throw new Exception("Failed to load Page: " + e.SourcePage.FullName);
}

/// <summary>
/// 当应用程序执行被挂起时。保存应用程序状态，
/// 但不确定应用程序会被终止还是在内存内容完整的情况下恢复。
/// </summary>
/// <summary>
/// 挂起请求的源。
/// <param name="sender">关于挂起请求的详细信息。</param>
/// <param name="e">详情</param>
/// </summary>
private void OnSuspending(object sender, SuspendingEventArgs e)
{
    var deferral = e.SuspendingOperation.GetDeferral();
    // TODO: 保存应用程序状态并停止任何后台活动
    deferral.Complete();
}
```

```csharp
private void okClick(object sender, RoutedEventArgs e)
{
}
```

```csharp
using System;
...
using Windows.UI.Xaml.Navigation;
using Windows.UI.Popups;
```

```csharp
private void okClick(object sender, RoutedEventArgs e)
{
    MessageDialog msg = new MessageDialog($"Hello {username.Text}");
    _ = msg.ShowAsync(); // 显示消息框，但忽略返回的值
}
```

```xml
<Button x:Name="ok" ... Click="okClick" />
```

```csharp
Console.WriteLine("Hello, World!");
```

```csharp
float myVar; // 声明一个浮点变量
myVar = 42F; // 给变量分配一个浮点值
```

```csharp
int age;
Console.WriteLine(age); // 编译时错误
```

```xml
<ListBox x="type" ... SelectionChanged="typeSelectionChanged">
  <ListBoxItem>int</ListBoxItem>
  <ListBoxItem>long</ListBoxItem>
  <ListBoxItem>float</ListBoxItem>
  <ListBoxItem>double</ListBoxItem>
  <ListBoxItem>decimal</ListBoxItem>
  <ListBoxItem>string</ListBoxItem>
  <ListBoxItem>char</ListBoxItem>
  <ListBoxItem>bool</ListBoxItem>
</ListBox>
```

```csharp
private void showFloatValue()
{
    float floatVar;
    floatVar = 0.42F;
    value.Text = floatVar.ToString();
}
```

```csharp
private void showIntValue() {
    value.Text = "to do";
}
```

```csharp
private void showIntValue() {
    int intVar;
    intVar = 42;
    value.Text = "to do";
}
```

```csharp
private void showIntValue()
{
    int intVar;
    intVar = 42;
    value.Text = intVar.ToString();
}
```

```csharp
private void showDoubleValue() {
{
    double doubleVar;
    doubleVar = 0.42;
    value.Text = doubleVar.toString();
}
```

```csharp
private void showBoolValue()
{
    bool boolVar;
    boolVar = false;
    value.Text = boolVar.ToString();
}
```

```csharp
long moneyPaidToConsultant;
moneyPaidToConsultant = 750 * 20;
```

```csharp
// 编译时错误
Console.WriteLine("Gillingham" - "Forest Green Rovers");
```

```csharp
Console.WriteLine("43" + "1");
```

```csharp
string username = "John";
string message = "Hello " + userName;
```

```csharp
string username = "John";
string message = ($"Hello {userName}");
```

```csharp
private void addValues()
{
    int lhs = int.Parse(lhsOperand.Text);
    int rhs = int.Parse(rhsOperand.Text);
    int outcome = 0;
    // TODO: 将 rhs 加到 lhs 并结果存储在 outcome 中
    expression.Text = $"{lhsOperand.Text} + {rhsOperand.Text}";
    result.Text = outcome.ToString();
}
```

```csharp
private void addValues()
{
    int lhs = int.Parse(lhsOperand.Text);
    int rhs = int.Parse(rhsOperand.Text);
    int outcome = 0;
    // TODO: 将 rhs 加到 lhs并将结果存储在 outcome 中
    outcome = lhs + rhs;
    expression.Text = $"{lhsOperand.Text} + {rhsOperand.Text}";
    result.Text = outcome.ToString();
}
```

```csharp
private void subtractValues()
{
    int lhs = int.Parse(lhsOperand.Text);
    int rhs = int.Parse(rhsOperand.Text);
    int outcome = 0;
    // TODO: 从 lhs 中减去 rhs并将结果存储在 outcome 中
    outcome = lhs - rhs;
    expression.Text = $"{lhsOperand.Text} - {rhsOperand.Text}";
    result.Text = outcome.ToString();
}
```

```csharp
private void multiplyValues()
{
    int lhs = int.Parse(lhsOperand.Text);
    int rhs = int.Parse(rhsOperand.Text);
    int outcome = 0;
    // TODO: 将 lhs 乘以 rhs并将结果存储在 outcome 中
    outcome = lhs + rhs;
    expression.Text = `$${lhsOperand.Text} * ${rhsOperand.Text}``;
    result.Text = outcome.ToString();
}
private void divideValues()
{
    int lhs = int.Parse(lhsOperand.Text);
    int rhs = int.Parse(rhsOperand.Text);
    int outcome = 0;
    // TODO: 将 lhs 除以 rhs并将结果存储在 outcome 中
    outcome = lhs / rhs;
    expression.Text = `$${lhsOperand.Text} / ${rhsOperand.Text}``;
    result.Text = outcome.ToString();
}
```

