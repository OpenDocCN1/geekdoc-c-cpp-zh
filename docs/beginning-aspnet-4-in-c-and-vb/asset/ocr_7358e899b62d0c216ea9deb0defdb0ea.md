```
Height = 40,
Fill = new RadialGradientBrush(Colors.Yellow, Colors.DarkRed)
};
FixedPage.SetLeft(ellipse, 500);
FixedPage.SetTop(ellipse, 50);
return ellipse;
}
```

The method GetDateContent() accesses the menus collection to add a date range to the document:

```
private UIElement GetDateContent()
{
    string dateString = String.Format("{0:d} to {1:d}", menus[0].Day, menus[menus.Count - 1].Day);
    var text1 = new TextBlock
    {
        FontSize = 24,
        HorizontalAlignment = HorizontalAlignment.Center
    };
    text1.Inlines.Add(new Bold(new Run(dateString)));
    FixedPage.SetLeft(text1, 130);
    FixedPage.SetTop(text1, 90);
    return text1;
}
```

Finally the method GetMenuContent() creates and returns a Grid control. This grid contains columns and rows that contain the date, menu, and price information:

```
private UIElement GetMenuContent()
{
    var grid1 = new Grid { ShowGridLines = true };

    grid1.ColumnDefinitions.Add(new ColumnDefinition
        { Width= new GridLength(50)});
    grid1.ColumnDefinitions.Add(new ColumnDefinition
        { Width = new GridLength(300)});
    grid1.ColumnDefinitions.Add(new ColumnDefinition
        { Width = new GridLength(70) });

    for (int i = 0; i < menus.Count; i++)
    {
        grid1.RowDefinitions.Add(new RowDefinition
            { Height = new GridLength(40) });

        var t1 = new TextBlock(
            new Run(String.Format("{0:ddd}", menus[i].Day)));
        t1.VerticalAlignment = VerticalAlignment.Center;
        t1.Margin = new Thickness(5, 2, 5, 2);
        Grid.SetColumn(t1, 0);
        Grid.SetRow(t1, i);
        grid1.Children.Add(t1);

        var t2 = new TextBlock(new Run(menus[i].Menu));
        t2.VerticalAlignment = VerticalAlignment.Center;
        t2.Margin = new Thickness(5, 2, 5, 2);
        Grid.SetColumn(t2, 1);
        Grid.SetRow(t2, i);
        grid1.Children.Add(t2);

        var t3 = new TextBlock(new Run(menus[i].Price.ToString()));
        t3.VerticalAlignment = VerticalAlignment.Center;
        t3.Margin = new Thickness(5, 2, 5, 2);
        Grid.SetColumn(t3, 2);
```