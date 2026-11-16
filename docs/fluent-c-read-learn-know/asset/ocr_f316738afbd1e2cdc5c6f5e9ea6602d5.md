# XAML COLLECTIONS

In the last exercise we saw that XAML makes it unnecessary to explicitly add elements to the elements that contain them because the ownership hierarchy is implicit in the way the element tags are nested. XAML even makes it easy to add all the items of a collection using a very similar syntax:

This is called COLLECTION PROPERTY SYNTAX, and like a lot of things in XAML, you don't need to worry too much about it. It just works.

```
<Element>
<Element.CollectionProperty>
<Item />
<Item />
...
</Element.CollectionProperty>
</Element>
```

The XAML compiler is smart enough to know that the items nested inside a Collection Property are children of the Collection.

# PUT ON YOUR THINKING HAT

![](bbox=[0.11, 0.68, 0.2, 0.82])

One of the WPF elements that has collection properties is the Grid layout panel. (We'll look at layout panels in detail in the next chapter.) Like other panel controls, the Grid can contain multiple children, and it organizes those children into rows and columns. The rows are defined as <RowDefinition> elements in the <Grid.RowDefinitions> collection and columns are <ColumnDefinition> elements in the <Grid.ColumnDefinitions> collection. Using collection property syntax, can you write the XAML that declares a <Grid> element with three rows and three columns? Don't worry about any other attributes or properties.