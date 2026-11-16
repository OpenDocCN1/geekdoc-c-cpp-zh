# METHOD OVERLOADING

C#, and indeed all the .NET languages, allows you to define multiple methods with the same name, distinguished by their signatures. This process is called OVERLOADING, and the methods are called OVERLOADS. It saves you thinking up or remembering different method names for methods that vary only by their signature. Here's how the process works:

```
MessageBox.Show("message");
MessageBox.Show("message", "caption");
Window MyWindow = new Window();
MyWindow.Show();
```

Different classes can define methods with the same name. These aren't overloads—the simple fact that they belong to different classes distinguishes them.

The MessageBox.Show() overloads are distinguished by their signatures:

```
public static MessageBoxResult Show(string message);
public static MessageBoxResult Show(string message, string caption);
```

The return type (MessageBoxResult in this example) is not technically part of the signature, so you can't define two methods with the same name that are distinguished only by the values they return.

+   - It's really not a good idea to have overload with different return types anyway. It's too confusing.

The parameters are given the same name, but that isn't a requirement. Remember: the name isn't technically part of the signature; it's the type that distinguishes them.

![](bbox=[0.08, 0.72, 0.91, 0.9])