# # REFERENCING RESOURCES

As we'll see, it's possible to define a style that applies to all elements of a given type automatically, but most of the time you'll have to reference the ResourceKey directly using one of the two XAML markup extensions that define how WPF treats the resource.

STATIC RESOURCES are evaluated once, when the XAML is first parsed at runtime. This is what you'll use most often.

```
<property>="{StaticResource <key>}"
```

```
<Label FontFamily="{StaticResource MainFont}" >
```

DYNAMIC RESOURCES are evaluated when the XAML is first parsed at runtime, and they change their values as the value of the resource changes.

```
<property>="{DynamicResource <key>}"
```

```
<Label FontFamily="{DynamicResource MainFont}" >
```

![](bbox=[0.09, 0.71, 0.91, 0.9])