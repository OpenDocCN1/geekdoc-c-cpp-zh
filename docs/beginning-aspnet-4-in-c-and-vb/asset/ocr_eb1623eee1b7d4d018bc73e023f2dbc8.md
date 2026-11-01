To illustrate priority binding, use the PriorityBindingDemo project to create the Data class. Accessing the ProcessSomeData property needs some time that is simulated by calling the Thread.Sleep() method:

```
```csharp
public class Data
{
    public string ProcessSomeData
    {
        get
        {
            Thread.Sleep(8000);
            return "the final result is here";
        }
    }
}
```
```

code snippet PriorityBindingDemo/Data.cs

The Information class gives information to the user. The information from property Info1 is returned immediately while Info2 returns information after five seconds. With a real implementation, this class could be associated with the processing class to get an estimated timeframe for the user:

```
```csharp
public class Information
{
    public string Info1
    {
        get
        {
            return "please wait...";
        }
    }
    public string Info2
    {
        get
        {
            Thread.Sleep(5000);
            return "please wait a little more";
        }
    }
}
```
```

code snippet PriorityBindingDemo/Information.cs

In the MainWindow.xaml file, the Data and Information classes are referenced and initiated within the resources of the Window:

```
```xml
<Window.Resources>
    <local:Data x:Key="data" />
    <local:Information x:Key="info" />
</Window.Resources>
```
```

code snippet PriorityBindingDemo/MainWindow.xaml

PriorityBinding is done in place of normal binding within the Content property of a Label. Priority Binding consists of multiple Binding elements where all but the last one have the IsAsync property set to True. Because of this, if the first binding expression result is not immediately available, the binding process chooses the next one. The first binding references the ProcessSomeData property of the Data class that needs some time. Because of this, the next binding comes into play and references the Info2 property of the Information class. Info2 does not return a result immediately, and because IsAsync is set, the binding process does not wait but continues to the next binding. The last binding uses the Info1 property and immediately returns a result. If it doesn't return a result immediately, you would wait for the result because IsAsync is set to the default, False: