```
Title ="Professional C# 6",
Publisher ="Wrox Press"
};
```

With the XAML code, the Title property is in OneWay mode to the Text property of a TextBlock, and the Publisher is bound without specifying a mode, which means it is bound OneTime (code file CompiledBindingSample/Views/LifetimeSample.xaml):

```
<StackPanel>
    <TextBlock Text="{x:Bind Book.Title, Mode=OneWay}" />
    <TextBlock Text="{x:Bind Book.Publisher}" />
</StackPanel>
```

Next, several AppBarButton controls are bound to change the lifetime of the compiled binding. The Click event of one button is bound to the method OnChangeBook. This method changes the title of the book. If you try this out, the title gets immediately updated because a OneTime binding was done (code file CompiledBindingSample/Views/LifetimeSample.xaml.cs):

```
public void OnChangeBook()
{
    Book.Title ="Professional C# 6 and .NET Core 5";
}
```

However, you can stop the tracking of the binding. Invoking the method StopTracking using the Bindings property of the page (this property is created if you are using compiled binding) removes all binding listeners. When you call this method before invoking the method OnChangeBook, the update of the book is not reflected in the user interface:

```
private void OnStopTracking()
{
    Bindings.StopTracking();
}
```

To explicitly update the user interface from bound sources, you can invoke the Update method. Calling this method reflects changes not only from OneWay or TwoWay bindings, but also OneTime bindings:

```
private void OnUpdateBinding()
{
    Bindings.Update();
}
```

For bringing the listeners back in place to make immediate updates to the user interface, the Initialize method needs to be invoked.

Initialize, Update, and StopTracking are the three important methods for controlling the lifetime with compiled binding.

# Using Resources for Compiled Data Templates

Defining data templates using compiled binding is easy; you just need to specify the x:DataType attribute with the data template because this