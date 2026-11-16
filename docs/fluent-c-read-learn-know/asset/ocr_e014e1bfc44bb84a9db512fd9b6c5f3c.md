# HOW'D YOU DO?

Here's the full definition of the ListBox:

```
<ListBox ... ItemsSource="{Binding}" >
<ListBox.ItemTemplate>
<DataTemplate>
<Label x:Name="itemLabel" Content="{Binding Path=Name}" />
<DataTemplate.Triggers>
<DataTrigger Binding="{Binding Path=Available}". Value="0">
<Setter Property="Foreground" Value="Red">
TargetName="itemLabel"/>
</DataTrigger>
</DataTemplate.Triggers>
</DataTemplate>
</ListBox.ItemTemplate>
</ListBox>
```

![](bbox=[0.525, 0.385, 0.88, 0.625])

# TAKE A BREAK

One of the things I really like about WPF is that once you know how one part of it works, you know a lot about how other parts of it work. That's certainly true of templates. Each type has little idiosyncrasies, but they have more in common than not.

So now that we have our ListBox working properly, why don't you take a break before we explore some of the other functionality WPF provides when you're working with collections?