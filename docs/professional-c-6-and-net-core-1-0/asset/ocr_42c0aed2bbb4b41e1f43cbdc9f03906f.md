```
Press">\n        <Setter Property="Background" Value="Red" />\n    </DataTrigger>\n    <DataTrigger Binding="{Binding Publisher}"\nValue="Dummies">\n        <Setter Property="Background" Value="Yellow" />\n    </DataTrigger>\n    <DataTrigger Binding="{Binding Publisher}"\nValue="Wiley">\n        <Setter Property="Background" Value="DarkGray" />\n    </DataTrigger>\n</Style.Triggers>\n</Style>\n</Window.Resources>\n<Grid>\n    <ListBox x:Name="list1" />\n</Grid>\n</Window>
```

In the code-behind, the list with the name `list1` is initialized to contain several `Book` objects (code file `TriggerSamples/DataTriggerWindow.xaml.cs`):

```
public DataTriggerWindow()\n{\n    InitializeComponent();\n\n    list1.Items.Add(new Book\n    {\n        Title = "Professional C# 6 and .NET Core 1.0",\n        Publisher = "Wrox Press"\n    });\n    list1.Items.Add(new Book\n    {\n        Title = "C# 5 All-in-One for Dummies",\n        Publisher = "For Dummies"\n    });\n    list1.Items.Add(new Book\n    {\n        Title = "HTML and CSS: Design and Build Websites",\n        Publisher = "Wiley"\n    });\n}
```

When you run the application, the `ListBoxItem` elements are formatted according to the publisher value, as shown in [Figure 34.11](#).