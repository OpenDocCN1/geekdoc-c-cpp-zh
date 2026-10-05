

```csharp
Controller control = new Controller();
FoldingMachine folder = new FoldingMachine();
WeldingMachine welder = new WeldingMachine();
PaintingMachine painter = new PaintingMachine();
...
control.Add(folder.StopFolding);
control.Add(welder.FinishWelding);
control.Add(painter.PaintOff);
...
control.Shutdown();
...
```

```csharp
...
private Auditor auditor = null;
private Shipper shipper = null;

public MainPage()
{
    ...
    this.auditor = new Auditor();
    this.shipper = new Shipper();
}
```

```csharp
private void CheckoutButtonClick(object sender, RoutedEventArgs e)
{
  try {
    // 执行结账处理
    if (this.requestPayment())
    {
      this.auditor.AuditOrder(this.order);
      this.shipper.ShipOrder(this.order);
    }
    ...
  }
...}
```

```csharp
public class CheckoutController
{
    public delegate void CheckoutDelegate(Order order);
}
```

```csharp
public class CheckoutController
{
    public delegate void CheckoutDelegate(Order order);
    public CheckoutDelegate CheckoutProcessing = null;
}
```

```csharp
public class CheckoutController
{
    public delegate void CheckoutDelegate(Order order);
    public CheckoutDelegate CheckoutProcessing = null;

    private bool requestPayment()
    {
        // 在此处处理支付逻辑
        // 此示例中未实现支付逻辑
        // 简单返回 true 表示已收到付款
        return true;
    }
}
```

```csharp
public class CheckoutController
{
    public delegate void CheckoutDelegate(Order order);
    public CheckoutDelegate CheckoutProcessing = null;

    private bool requestPayment()
    {
        ...
    }

    public void StartCheckoutProcessing(Order order)
    {
        // 执行结账处理
        if (this.requestPayment())
        {
            if (this.CheckoutProcessing is not null)
            {
                this.CheckoutProcessing(order);
            }
        }
    }
}
```

```csharp
public ... class MainPage : ...
{
    ... private Auditor auditor = null;
    private Shipper shipper = null;
    private CheckoutController checkoutController = null;
    ...
}
```

```csharp
public MainPage()
{
    ...
    this.auditor = new Auditor();
    this.shipper = new Shipper();
    this.checkoutController = new CheckoutController();
}
```

```csharp
public MainPage()
{
  ...
  this.checkoutController = new CheckoutController();
  this.checkoutController.CheckoutProcessing += this.auditor.AuditOrder;
  this.checkoutController.CheckoutProcessing += this.shipper.ShipOrder;
}
```

```csharp
private void CheckoutButtonClicked(object sender, RoutedEventArgs e)
{
    try
{
        // 执行结账处理
        this.checkoutController.StartCheckoutProcessing(this.order);

        // 显示订单摘要
        ...
    }
    ...
}
```

```csharp
this.stopMachinery += folder.StopFolding;
```

```csharp
void StopFolding(int shutDown); // 在指定的秒数后关闭
```

```csharp
void FinishFolding()
{
    folder.StopFolding(0); // 立即关闭
}
```

```csharp
this.stopMachinery += folder.FinishFolding;
```

```csharp
this.stopMachinery += () => folder.StopFolding(0);
```

```csharp
event delegateTypeName eventName
```

```csharp
class TemperatureMonitor
{
    public delegate void StopMachineryDelegate();
    ...
}
```

```csharp
class TemperatureMonitor
{
    public delegate void StopMachineryDelegate();
    public event StopMachineryDelegate MachineOverheating;
    ...
}
```

```csharp
class TemperatureMonitor
{
    public delegate void StopMachineryDelegate();
    public event StopMachineryDelegate MachineOverheating;
    ...
}

TemperatureMonitor tempMonitor = new TemperatureMonitor();
...
tempMonitor.MachineOverheating += () => { folder.StopFolding(0); };
tempMonitor.MachineOverheating += welder.FinishWelding;
tempMonitor.MachineOverheating += painter.PaintOff;
```

```csharp
class TemperatureMonitor
{
    public delegate void StopMachineryDelegate();
    public event StopMachineryDelegate MachineOverheating;
    ...
    private void Notify()
    {
        if (this.MachineOverheating is not null)
        {
            this.MachineOverheating();
        }
    }
    ...
}
```

```csharp
public delegate void RoutedEventHandler(Object sender, RoutedEventArgs e);
```

```csharp
public class ButtonBase:
  ...
{
    public event RoutedEventHandler Click;
    ...
  }

public class Button: ButtonBase
{
  ...
}
```

```csharp
partial class MainPage : 
global::Windows.UI.Xaml.Controls.Page,
global::Windows.UI.Xaml.Markup.IComponentConnector,
global::windows.UI.Xaml.Markup.IComponentConnector2
{
    ...
    public void Connect(int connectionId, object target)
    {
        switch(connectionId)
        {
            case 1:
            {
                this.okay = (global::Windows.UI.Xaml.Controls.Button)(target);
                ...
                ((global::Windows.UI.Xaml.Controls.Button)this.okay).Click += this.okayClick;
                ...
            }
            break;
            default:
                break;
        }
        this..contentLoaded = true;
    }
    ...
}
```

```csharp
public sealed partial class MainPage : Page
{
    ...
    private void okayClick(object sender, RoutedEventArgs e)
    {
        // 处理 Click 事件
    }
}
```

```csharp
private void CheckoutButtonClicked(object sender, RoutedEventArgs e)
{
    try
    {
        // 执行结账处理
        this.checkoutController.StartCheckoutProcessing(this.order);

        // 显示订单摘要
        MessageDialog dlg = new MessageDialog(...);
        _ = dlg.ShowAsync();
        ...
    }
    ...
}
```

```csharp
this.stopMachinery += folder.StopFolding;
```

```csharp
```
```sharp
class TemperatureMonitor
{
    public delegate void StopMachineryDelegate();
    ...
}
```

```csharp
class TemperatureMonitor
{
    public delegate void StopMachineryDelegate();
    public event StopMachineryDelegate MachineOverheating;
    ...
}
```

