# Here are the contents of FluentDictionary.xaml:

When you added the file to the project, Visual Studio created the ResourceDictionary tag for you. Good thing, too; who wants to type those namespaces?

I picked DarkTurquoise. You could have picked a different standard color, or specified one using the hexadecimal values.

```
<ResourceDictionary ... >
    <SolidColorBrush x:Key="SolidBackground"
        Color="DarkTurquoise" />
</ResourceDictionary>
```

```
<Application ... >
    <Application.Resources>
        <ResourceDictionary>
            <ResourceDictionary.MergedDictionaries>
                <ResourceDictionary Source="FluentDictionary.xaml" />
            </ResourceDictionary.MergedDictionaries>
        </ResourceDictionary>
    </Application.Resources>
</Application>
```

App.xaml already has an <Application.Resources> tag, but don't feel bad if you had to check the syntax to get to the MergedDictionaries element. It always seems to me that there's one more ResourceDictionary than there should be.

I'm wrong about that, of course. The Resources property is a collection, not a ResourceDictionary. The <ResourceDictionary> tag is an element in that collection, and the MergedDictionaries property contains another collection, with yet another ResourceDictionary contained in it.

![](bbox=[0.72, 0.775, 0.9, 0.885])