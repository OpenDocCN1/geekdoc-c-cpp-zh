

```
Text="{Binding FirstName, Mode=TwoWay}" .../>
    <TextBox Grid.Row="1" Grid.Column="7" x:Name="lastName" ...
Text="{Binding LastName, Mode=TwoWay}" .../>
    ...
    <TextBox Grid.Row="3" Grid.Column="3" Grid.ColumnSpan="3" x:Name="email" ... Text="{Binding EmailAddress, Mode=TwoWay}" .../>
    ...
    <TextBox Grid.Row="5" Grid.Column="3" Grid.ColumnSpan="3" x:Name="phone" ... Text="{Binding Phone, Mode=TwoWay}" .../>
</Grid>
<Grid x:Name="customersColumnarView" Margin="10,20,10,20" ...>
    ...
    <TextBox Grid.Row="0" Grid.Column="1" x:Name="cId" ...
Text="{Binding CustomerID, Mode=TwoWay}" .../>
    ...
    <TextBox Grid.Row="2" Grid.Column="1" x:Name="cFirstName" ...
Text="{Binding FirstName, Mode=TwoWay}" .../>
    <TextBox Grid.Row="3" Grid.Column="1" x:Name="cLastName" ...
Text="{Binding LastName, Mode=TwoWay}" .../>
    ...
    <TextBox Grid.Row="4" Grid.Column="1" x:Name="cEmail" ...
Text="{Binding EmailAddress, Mode=TwoWay}" .../>
    ...
    <TextBox Grid.Row="5" Grid.Column="1" x:Name="cPhone" ...
Text="{Binding Phone, Mode=TwoWay}" .../>
</Grid>
```

Binding 规范中的 Mode 参数指示数据绑定是单向的还是双向的。默认情况下为单向。 将 Mode 设置为 TwoWay 会导致用户所做的任何更改都传回控件所绑定的对象。

- 2. 在 Debug 菜单上，单击 Start Debugging 以再次构建并运行应用。

- 3. 在宽视图中打开应用时，将电子邮件地址更改为 john@treyresearch.com，然后调整窗口大小以在窄视图中显示应用。
+ 请注意，尽管数据绑定已更改为 TwoWay 模式，窄视图中显示的电子邮件地址仍未更新——它仍然是 john@contoso.com。

- 4. 返回 Visual Studio 并停止调试。

很明显，某些功能没有正常工作！问题现在不是数据未更新，而是视图未显示数据的最新版本。 （如果您在 Customer 类的 EmailAddress 属性的 set 访问器中恢复断点并在调试器中运行应用，您会看到每当您更改电子邮件地址的值并将焦点移出 TextBox 控件时，调试器都会到达断点。）尽管看起来如此，数据绑定过程并不是魔术，数据绑定并不知道其所绑定的数据何时被更改。 对象需要通过向 UI 发送 *PropertyChanged* 事件来通知数据绑定任何修改。 此事件是 *INotifyPropertyChanged* 接口的一部分，所有支持双向数据绑定的对象都应实现此接口。 您将在下一个练习中实现此接口。

## 在 *Customer* 类中实现 *INotifyPropertyChanged* 接口

- 1. 在 Visual Studio 中，在代码和文本编辑器窗口中显示 Customer.cs 文件。

- 2. 在文件顶部的文件列表中添加以下 *using* 指令：

```
using System.ComponentModel;
```

*INotifyPropertyChanged* 接口定义在此命名空间中。

- 3. 修改 *Customer* 类的定义以指定它实现了 *INotifyPropertyChanged* 接口，如此处以粗体所示：

Click here to view code image

```
class Customer : INotifyPropertyChanged
```

- 4. 在 *Customer* 类中的 *Phone* 属性之后，添加以下代码中以粗体显示的 *PropertyChanged* 事件：

Click here to view code image

```
class Customer : INotifyPropertyChanged
{
    ...
    public string _phone;
    public string Phone {
        get { return this._phone; }
        set { this._phone = value; }
    }

    public event PropertyChangedEventHandler PropertyChanged;
}
```

此事件是 *INotifyPropertyChanged* 接口定义的唯一项目。 实现此接口的所有对象都必须提供此事件，并且每当它们想要通知外部世界属性值已更改时，都应引发此事件。

- 5. 在 *Customer* 类中，在 *PropertyChanged* 事件之后添加以下以粗体显示的 *OnPropertyChanged* 方法：

Click here to view code image

```
class Customer : INotifyPropertyChanged
{
    ...
    public event PropertyChangedEventHandler PropertyChanged;
```

```
protected virtual void OnPropertyChanged(string propertyName)
{
    if (PropertyChanged != null)
    {
        PropertyChanged(this,
            new PropertyChangedEventArgs(propertyName));
    }
}
```

*OnPropertyChanged* 方法引发 *PropertyChanged* 事件。 传递给 *PropertyChanged* 事件的 *PropertyChangedEventArgs* 参数应指定已更改的属性的名称。 此值作为参数传递给 *OnPropertyChanged* 方法。

6. 修改 *Customer* 类中每个属性的属性 set 访问器，以便在它们包含的值被修改时调用 *OnPropertyChanged* 方法，如此处以粗体所示：

Click here to view code image

```
class Customer : INotifyPropertyChanged
{
    public int _customerID;
    public int CustomerID
    {
        get { return this._customerID; }
        set
        {
            this._customerID = value;
            this.OnPropertyChanged(nameof(CustomerID));
        }
    }
    public string _title;
    public string Title
    {
        get { return this._title; }
        set
        {
            this._title = value;
            this.OnPropertyChanged(nameof(Title));
        }
    }
    public string _firstName;
    public string FirstName
    {
        get { return this._firstName; }
        set
        {
            this._firstName = value;
            this.OnPropertyChanged(nameof(FirstName));
        }
    }
}
```

```
public string _lastName;
public string LastName
{
    get { return this._lastName; }
    set
    {
        this._lastName = value;
        this.OnPropertyChanged(nameof(LastName));
    }
}

public string _emailAddress;
public string EmailAddress
{
    get { return this._emailAddress; }
    set
    {
        this._emailAddress = value;
        this.OnPropertyChanged(nameof(EmailAddress));
    }
}

public string _phone;
public string Phone
{
    get { return this._phone; }
    set
    {
        this._phone = value;
        this.OnPropertyChanged(nameof(Phone));
    }
}
...
}
```

## nameof 运算符

在 Customer 类中演示的 nameof 运算符是 C# 中鲜为人知但非常有用的功能，适用于此类代码。 它返回作为其参数传递的变量的名称作为字符串。 如果不使用 nameof 运算符，您将不得不使用硬编码的字符串值。 例如：

Click here to view code image

```
public int CustomerID
{
    get { return this._customerID; }
    set
    {
        this._customerID = value;
        this.OnPropertyChanged("CustomerID");
    }
}
```

虽然使用字符串值需要输入的字符更少，但请考虑如果您需要在将来更改属性名称会发生什么。 使用字符串方法，您还需要修改字符串值。 如果您没有这样做，代码仍然可以编译和运行，但运行时对属性值所做的任何更改都不会被通知，从而导致难以找到的错误。 使用 nameof 运算符，如果您更改了属性名称但忘记更改 nameof 的参数，代码将无法编译，从而立即提醒您存在应快速轻松修复的错误。

- 7. 在 Debug 菜单上，单击 Start Debugging 以再次构建并运行应用。
- 8. 当 Customers 表单出现时，将电子邮件地址更改为 john@treyresearch.com，并将电话号码更改为 222-2222。
- 9. 调整窗口大小以在窄视图中显示应用，并验证电子邮件地址和电话号码是否已更改。
- 10. 将名字更改为 James，将窗口展开以显示宽视图，并验证名字是否已更改。
- 11. 返回 Visual Studio 并停止调试。

## 使用 ComboBox 控件进行数据绑定

使用 TextBox 或 TextBlock 等控件进行数据绑定相对简单。 另一方面，ComboBox 控件需要更多关注。 问题在于 ComboBox 控件实际上显示了两件事：用户可以从中选择项目的下拉列表中的值列表和

