# HOW'D YOU DO?

It doesn't matter if you declared your objects in a different order, as long as the project will compile.

```
public static readonly RoutedEvent MyDefaultEvent =
EventManager.RegisterRoutedEvent("MyDefault", RoutingStrategy.Bubble,
typeof(RoutedEventHandler), typeof(MainWindow));

public event RoutedEventHandler MyDefault
{
    add { AddHandler(MyDefaultEvent, value); }
    remove { RemoveHandler(MyDefaultEvent, value); }
}

protected void OnMyDefault()
{
    RoutedEventArgs e = new RoutedEventArgs(MainWindow.MyDefaultEvent);
    RaiseEvent(e);
}
```

```
public class CustomArgs : RoutedEventArgs
{
    public int MyProp { get; set; }
}
```

```
// public delegate void MyCustomHandler(object sender, CustomArgs e);

public static readonly RoutedEvent MyCustomEvent =
EventManager.RegisterRoutedEvent("MyCustom", RoutingStrategy.Bubble,
typeof(MyCustomHandler), typeof(Window));

public event MyCustomHandler MyCustom
{
    add { AddHandler(MyCustomEvent, value); }
    remove { RemoveHandler(MyCustomEvent, value); }
}
```