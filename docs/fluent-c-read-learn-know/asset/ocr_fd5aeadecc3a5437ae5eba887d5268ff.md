# # RESOURCES IN CODE

It's very unusual to need to create or even reference resources in code, and it's far more verbose than XAML but you can if you need to.

# ## TO CREATE A RESOURCEDICTIONARY

> Nothing tricky here...

```
ResourceDictionary <rd> = new ResourceDictionary();
```

# ## TO ADD A RESOURCE TO A DICTIONARY

> The ResourceKey and Resource are both Object types

```
<rd>.Add(<ResourceKey>,<Object>);
```

# ## TO REFERENCE A RESOURCEDICTIONARY

All of these methods are defined on FrameworkElement and FrameworkContentElement, so they're available throughout WPF. The resources are always dynamic.

```
FindResource(<ResourceKey>);
```

or

```
TryFindResource(<ResourceKey>);
```

> These method return an object, so you'll need to cast the object returned.

```
MyButton.Background = (Brush)this.TryFindResource("MyBrush");
```

The Try... version returns a null if the resource isn't found, rather than throwing an error.

# ## TAKE A BREAK

Feel free to play with creating and referencing resources in code, but you really only need to remember that it's possible, because you're not going to do it often (if ever). For now, why don't you take a quick break before we tackle styles.

![](bbox=[0.1, 0.77, 0.19, 0.89])