
## 答案

- 1. 如果要按比例分配行或列（当存在固定尺寸或自动尺寸的行或列时，使用剩余空间），你可以使用所谓的**星号尺寸**（star sizing）。要使用星号尺寸，你需要指定星号符号（*）作为值。在使用星号尺寸时，你可以指定一个权重值，以控制分配给该元素的可用空间比例。例如，高度使用 * 的行将获得一倍的可用空间，而使用 2* 的行将获得两倍的可用空间。
- 2. 路由事件是指不仅可以在触发事件的元素上，还可以在元素树中的多个监听器上调用处理程序的事件。

## 练习

本章没有练习题。

# 使用数据绑定和验证

**本小时您将学到：**

- 理解数据绑定
- 数据转换
- 绑定到集合
- 处理数据模板
- 验证数据

在上一小时中，您学习了如何创建 Windows 演示基础（WPF）应用程序，并看到了 WPF 如何使您能够干净地将应用程序的用户界面部分与业务逻辑分离开来。您学习了如何处理由用户界面引发的事件，以便您的应用程序除了看起来美观之外还能完成其他功能。虽然通过仔细的用户界面设计可以控制用户输入，但验证输入以确保输入信息正确也是常见的做法。除了接受和验证用户输入外，应用程序通常还需要向用户显示数据——无论是出于信息目的还是为了让用户修改数据。在 WPF 应用程序中，使用数据绑定最轻松地完成此任务。

您已经在 AddressBook 和 PhotoViewer 应用程序中使用了 WPF 的数据绑定功能。事实上，这两个应用程序的大部分都使用了绑定，不仅将控件绑定到后端数据，还将控件的属性绑定到其他控件的属性。

在本小时中，您将更深入地了解如何使用 WPF 的数据绑定功能，以及如何验证用户输入的数据，以确保其符合应用程序需求中指定的业务规则。

## 理解数据绑定

WPF 中的数据绑定功能使应用程序能够以简单且一致的方式呈现和交互数据。您可以将元素绑定到来自各种来源的数据，包括 CLR 对象和 XML。数据绑定使您能够在用户界面控件和业务逻辑之间建立连接。如果数据提供了必要的通知，且绑定具有必要的设置，当数据更改时，绑定到它的用户界面元素将自动反映这些更改。此外，数据绑定还使底层数据源能够自动更新，以反映通过用户界面所做的更改。

如图 18.1 所示，您可以将数据绑定视为绑定目标和绑定源之间的桥梁。大多数绑定包含以下四个组件：

- 绑定目标对象
- 目标属性
- 绑定源对象
- 绑定源对象中要使用的值的路径

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_406_0.png)

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_406_1.png)

绑定目标必须始终是 DependencyObject，它表示参与依赖属性系统的对象。WPF 提供的所有用户界面对象都继承自 UIElement，而 UIElement 又继承自 DependencyObject。目标属性也必须是依赖属性，即由 DependencyProperty 对象支持的属性。幸运的是，大多数 UIElement 属性都是依赖属性，并且除了只读属性外，默认支持数据绑定。

再次查看图 18.1，您会看到绑定可以从源到目标（OneWay），从目标到源（OneWayToSource），或者双向（TwoWay）：

- 在 **OneWay** 绑定中，源属性的更改会自动更新目标，通常用于隐式只读的控件绑定时。
- 在 **TwoWay** 绑定中，源属性或目标属性的更改会更新另一方，通常用于可编辑表单或其他完全交互界面。大多数属性默认为 **OneWay** 绑定；但是，某些属性（如用户可编辑控件的属性，例如 `TextBox` 的 `Text` 属性）默认为 **TwoWay** 绑定。
- 在 **OneWayToSource** 中，目标属性的更改会自动更新源。您可以将其视为 **OneWay** 绑定的反向操作。
- 还有一种 **OneTime** 绑定模式，它使源属性仅用于初始化目标。当这种情况发生时，后续的更改不会更新目标。

对于 **TwoWay** 或 **OneWayToSource** 绑定，为了更新源属性，它们会监听目标属性的变化。为了知道何时应更新源，绑定使用 `UpdateSourceTrigger` 属性。当 `UpdateSourceTrigger` 的值为 `PropertyChanged` 时，源属性会在目标属性更改时立即更新。如果值为 `LostFocus`，源属性仅在目标属性在用户界面中失去焦点时更新。对于大多数依赖属性，`UpdateSourceTrigger` 属性的默认值是 `PropertyChanged`。某些属性，如 `TextBox` 的 `Text` 属性，默认为 `LostFocus`。

## 创建绑定

在上一小时中，您编写了一个事件处理程序，直接设置 `Label` 控件的 `Content` 属性（参见第 17 章中的列表 17.7）。虽然您编写的代码有效，但缺少一些重要的部分。如果您将事件处理程序更改为列表 18.1 中显示的代码，`Label` 将不再显示路径。显然，这不是期望的行为。

**列表 18.1** 创建绑定

```csharp
using (FolderBrowserDialog folderBrowser = new FolderBrowserDialog())
{
    folderBrowser.ShowNewFolderButton = false;
    if (folderBrowser.ShowDialog(this) == System.Windows.Forms.DialogResult.OK)
    {
        this.photos.Path = folderBrowser.SelectedPath;
    }
}

e.Handled = true;
```

一种选择是将 `photos.Path` 属性和 `ImagesDirectory.Content` 属性都设置为相同的值。更好的选择是使用 WPF 的数据绑定功能，以便每次 `photos.Path` 属性更改时，`ImagesDirectory.Content` 属性都能自动反映该更改。

通过在 ImagesDirectory Label 的 XAML 中添加以下属性可以轻松实现：

```xml
Content="{Binding Path=Path}"
```

此属性告诉 Label，Content 属性绑定到具有名为 Path 的属性的某个对象。

接下来，您需要修改 Path 属性的 set 访问器，以便在其值更改时提供通知。您可以通过在设置 directoryInfo 字段后添加以下一行来实现：

```csharp
this.OnPropertyChanged (new PropertyChangedEventArgs ("Path"));
```

## 您知道吗？

### INotifyPropertyChanged 接口

由于 PhotoCollection 类继承自 ObservableCollection< T >，它已经包含了必要的 System. ComponentModel. INotifyPropertyChanged 接口。该接口定义了一个公共事件：PropertyChanged 事件。您也可以在自定义类中使用此接口。通常，您需要实现必要的事件和一个类似于此处显示的事件处理程序：

```csharp
protected virtual void OnPropertyChanged (PropertyChangedEventArgs e)  
{  
if (this.PropertyChanged != null)  
{
this.PropertyChanged (this, e);
}
}
```

任何值更改后需要通知的属性都应调用 OnPropertyChanged 方法。

如果您仔细观察，会注意到没有指定源对象；但源对象是四个必需组件之一。实际上，如果没有指定绑定源，绑定实际上什么也不做。

这是如何工作的？当绑定引擎遇到未指定源的绑定时，它会向上遍历可视元素的层次结构，寻找 DataContext。当它找到一个 DataContext 时，它会将其用作绑定源。

