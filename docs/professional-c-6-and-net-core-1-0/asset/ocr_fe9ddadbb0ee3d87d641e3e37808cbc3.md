```
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="Frames Sample" Height="500" Width="800">
<Frame Source="http://www.cninnovation.com" Grid.Row="1" />
</Window>
```

![](bbox=[0.105, 0.14, 0.895, 0.511])

# Figure 34.1

> NOTE In Chapter 32, “Windows Apps: User Interfaces,” you can read how to use the Frame class to navigate between pages. With WPF, you can also use the Frame class for navigation.

# Headered Content Controls

Content controls with a header are derived from the base class HeaderedContentControl, which itself is derived from the base class ContentControl. The HeaderedContentControl class has a property Header to define the content of the header and HeaderTemplate for complete customization of the header. The controls derived from the base class HeaderedContentControl are listed in the following table.