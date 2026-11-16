
## Here are the contents of FluentDictionary.xaml:

When you added the file to the project, Visual Studio created the ResourceDictionary tag for you. Good thing, too; who wants to type those namespaces?

I picked DarkTurquoise. You could have picked a different standard color, or specified one using the hexadecimal values.

```xml
<ResourceDictionary ... >
    <SolidColorBrush x:Key="SolidBackground"
        Color="DarkTurquoise" />
</ResourceDictionary>
```

```xml
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

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_730_0.png)

## REFERENCING RESOURCES

As we'll see, it's possible to define a style that applies to all elements of a given type automatically, but most of the time you'll have to reference the ResourceKey directly using one of the two XAML markup extensions that define how WPF treats the resource.

STATIC RESOURCES are evaluated once, when the XAML is first parsed at runtime. This is what you'll use most often.

```xml
<property>="{StaticResource <key>}"
```

```xml
<Label FontFamily="{StaticResource MainFont}" >
```

DYNAMIC RESOURCES are evaluated when the XAML is first parsed at runtime, and they change their values as the value of the resource changes.

```xml
<property>="{DynamicResource <key>}"
```

```xml
<Label FontFamily="{DynamicResource MainFont}" >
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_731_0.png)

## HOW'D YOU DO?

What did you decide?

```xml
<Window ...
Background="{StaticResource SolidBackground}">
```

The background color isn't going to change, so there's no reason to make it a dynamic resource.

Dynamic resources incur a small performance penalty. These things add up, so you shouldn't use them unless you need to.

## MAKE A NOTE—STATIC RESOURCES

The Framework Library defines several classes that expose static properties relating to the system configuration, including SystemColors, SystemFonts and SystemParameters. You'll often want these to be dynamic resources so they'll update if the user changes the values while the application is running. In order to do that, you need to reference the resource key version of the property (the SystemColors.MenuBarColorKey property instead of SystemColors.MenuColor property, for example). Because these properties are static, you need to use another markup extension, x:Static.

```xml
{DynamicResource {x:Static SystemFonts.CaptionFontFamilyKey}}
```

The x:Static extension is required whenever you're referring to a static property, field, enumeration value or constant.

x:Static is most often used in the context of resources, but you'll need it anywhere you reference one of these objects in XAML.

## RESOURCES IN CODE

It's very unusual to need to create or even reference resources in code, and it's far more verbose than XAML but you can if you need to.

### TO CREATE A RESOURCEDICTIONARY

> Nothing tricky here...

```csharp
ResourceDictionary <rd> = new ResourceDictionary();
```

### TO ADD A RESOURCE TO A DICTIONARY

> The ResourceKey and Resource are both Object types

```csharp
<rd>.Add(<ResourceKey>,<Object>);
```

### TO REFERENCE A RESOURCEDICTIONARY

All of these methods are defined on FrameworkElement and FrameworkContentElement, so they're available throughout WPF. The resources are always dynamic.

```csharp
FindResource(<ResourceKey>);
```

or

```csharp
TryFindResource(<ResourceKey>);
```

> These method return an object, so you'll need to cast the object returned.

```csharp
MyButton.Background = (Brush)this.TryFindResource("MyBrush");
```

The Try... version returns a null if the resource isn't found, rather than throwing an error.

### TAKE A BREAK

Feel free to play with creating and referencing resources in code, but you really only need to remember that it's possible, because you're not going to do it often (if ever). For now, why don't you take a quick break before we tackle styles.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_733_0.png)

## BASIC STYLING

Resources are helpful, but defining individual resources can lead to some really verbose (not to mention tedious) code. The solution is to define a style, which is at its most basic is a resource that contains a collection of property values that can be applied all at once.

```xml
<Style x:Key="BoldItalicLabel" >
    <Setter Property="FontFamily" Value="Arial" />
    <Setter Property="Foreground">
        <Setter.Value>
            <SolidColorBrush Color="Black" />
        </Setter.Value>
    </Setter>
</Style>
```

The Style contains a collection of Setter elements, each of which has a Property and a Value.

This is a simple example, but the Value property can be as complex as you need.

### KEYED STYLES

Styles can be declared inside a resource dictionary or in the Resources collection of an element. In either case, you can give it a key and reference it using the same syntax you use to reference a Resource.

```xml
<ResourceDictionary>
    <Style x:Key="LabelStyle" >
        <Setter Property="Label.FontFamily" Value="Arial" />
    </Style>
</ResourceDictionary>
<Label Style="{StaticResource LabelStyle}">Hello!</Label>
```

### TARGETED STYLES

If you add a TargetType to the Style, you don't need to keep specifying the element as part of the Setter.Property definition. You'll almost always do this when you declare a Style inside the Resources collection of an element.

```xml
<ResourceDictionary>
    <Style x:Key="LabelStyle" TargetType="Label">
        <Setter Property="FontFamily" Value="Arial" />
    </Style>
</ResourceDictionary>
<Label Style="{StaticResource LabelStyle}">Hello!</Label>
```

You can address properties directly, which saves a lot of typing.

### IMPLICIT STYLES

If you declare a style's TargetType but don't give it a key, you don't need to keep specifying the element as part of the Setter.Property definition, and you don't need to apply it explicitly to elements of that type, it will become the default.

```xml
<ResourceDictionary>
    <Style TargetType="Label">
        <Setter Property="FontFamily" Value="Arial" />
    </Style>
</ResourceDictionary>
<Label>Hello!</Label>
```

> In .NET 4.0, the Background property of an implicit style won't work for the Window if you're using a merged dictionary. Use a keyed style instead.

### PUT ON YOUR THINKING HAT

Can you build a resource dictionary to define the visual appearance of this window? Remember to set up a merged dictionary inside app.xaml to get access to the dictionary.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_735_0.png)

The gradients used for the backgrounds of the Window and Buttons have the same GradientStopsCollection, but different start and end points. How can you avoid defining the stops twice?

There are two types of label.

All of the text on the window has the same FontFamily and FontSize. How can you specify that only once? (Hint: Dependency property inheritance still works, even if the properties are set via a Style.)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_735_1.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_736_0.png)

## HOW'D YOU DO?

The exact fonts and colors you choose aren't important. You probably chose different key names, too. That doesn't matter either.

### MAINWINDOW.XAML:

Need the key because of that nasty bug

Need the keys here, too, because there isn't a single style

```xml
<Window ... Style="{StaticResource WindowStyle}">
<Grid>
...
<Label ... Style="{StaticResource BasicLabel}">First Optional Item:</Label>
<Label ... Style="{StaticResource BasicLabel}">Second Optional Item:</Label>
<Label ... Style="{StaticResource RequiredLabel}">Required Item:</Label>
<Label ... Style="{StaticResource RequiredLabel}">Second Required Item:</Label>
<TextBox Grid.Row="0" Grid.Column="1">First Option</TextBox>
<StackPanel Grid.Row="4" Grid.Column="0" Grid.ColumnSpan="2"
Orientation="Horizontal" Height="35">
<Button>Submit</Button>
<Button>Cancel</Button>
</StackPanel>
</Grid>
</Window>
```

We don't need to reference styles here, because they're applied implicitly.

- Quitting the key here makes this
- an implicit style that will be applied
- to both the buttons.
