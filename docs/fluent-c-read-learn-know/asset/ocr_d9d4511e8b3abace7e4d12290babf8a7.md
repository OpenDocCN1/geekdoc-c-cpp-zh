# # OBJECT SHARING

Before we talk about some of the other cool things you can do with the CollectionView, we need to take a minute to look at how you share objects between XAML and the code-behind. So far in our sample applications the communication between the two has been very simple, but in real applications the communication often needs to be more complete. Here's how:

# ## TO REFERENCE A XAML ELEMENT IN CODE

This one's easy. You just give the element a name, and then you can refer to it by name in code:

```
`<Element x:Name="MyElement">`
```

`this.MyElement`

# ## TO REFERENCE A XAML RESOURCE IN CODE

Unlike element names, resource keys that you declare in XAML aren't visible as members of the Window. (Which makes sense, really. They're not members of the Window class.) If you need to access them from code, one way is to use the FindResource() or TryFindResource() method defined by FrameworkElement:

You pass the ResourceKey as a String.

```
`.Style buttonStyle = (Style) this.FindResource("MyButtonStyle");`
```

FindResource() returns an Object, so you'll need to cast it.

Another option is to access the Resources collection of an element, which contains an instance of a ResourceDictionary that can be accessed by key:

```
`Style buttonStyle = (Style)this.ButtonElement.Resources("MyButtonStyle");`
```