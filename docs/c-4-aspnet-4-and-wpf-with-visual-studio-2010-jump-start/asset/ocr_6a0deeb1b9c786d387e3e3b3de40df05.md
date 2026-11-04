In addition to allowing multiple forms or applications to use the same resources, merged dictionaries allow a single window to load more than one resource dictionary. This can be handy if you want to use separate dictionaries to hold different groups of resources. For example, you might have separate dictionaries to hold button resources, label resources, and list resources.

You can also use multiple resource dictionaries in the same application to switch easily between different appearances. For example, the ResourceDictionaries example program uses the following code to merge two resource dictionaries, ResBlue.xaml and ResRed.xaml:

Available for download on Wrox.com

```
<Window.Resources>
    <ResourceDictionary>
        <ResourceDictionary.MergedDictionaries>
            <ResourceDictionary Source="ResBlue.xaml"/>
            <ResourceDictionary Source="ResRed.xaml"/>
        </ResourceDictionary.MergedDictionaries>
    </ResourceDictionary>
</Window.Resources>
```

Because the file ResRed.xaml is loaded second, the resource values in that file take precedence. This figure shows the ResourceDictionaries program using the values in this resource dictionary.

![](bbox=[0.25, 0.46, 0.6, 0.62])

By simply switching the order of these two resource dictionaries, you can completely change the application's appearance. The following figure shows the ResourceDictionaries program using the values in the ResBlue.xaml resource dictionary.

![](bbox=[0.25, 0.71, 0.6, 0.84])

The later section “Skins” explains how to switch an application’s appearance in a similar manner at run time.