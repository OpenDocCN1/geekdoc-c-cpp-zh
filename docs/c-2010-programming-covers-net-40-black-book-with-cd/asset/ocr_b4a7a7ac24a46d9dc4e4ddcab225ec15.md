```
<TextBox Grid.Row="1" Margin="10,10,10,10" Textwrapping="Wrap" Text="Common Name:Baby Panda Scientific Name:Ailuropoda Melanoleuca Genus:Ailuropoda Location:Sichuan, Shaanxi, and the Gansu provinces of China" IsReadOnly="True" Background="LightBlue"/>
<Image Source="Baby Panda.jpg" Grid.Row="1" Grid.Column="1" Margin="10,10,10,10"/>
<TextBox Grid.Row="2" Margin="10,10,10,10" Textwrapping="Wrap" Text="Common Name: Domestic Cat Scientific Name: Felis Catus Genus: Felis" IsReadOnly="True" Background="LightBlue"/>
<Image Source="My Myla.jpg" Grid.Row="2" Grid.Column="1" Margin="10,10,10,10"/>
<my:GridSplitter x:Name="split1" Height="20" Width="250" Grid.Row="2" Grid.Column="1" Grid.ColumnSpan="2" HorizontalAlignment="Stretch" VerticalAlignment="Top" Background="SteelBlue"/>
<my:GridSplitter x:Name="split2" Height="250" Width="20" Grid.Row="1" Grid.Column="1" Grid.RowSpan="2" HorizontalAlignment="Left" VerticalAlignment="Stretch" Background="SteelBlue"/>
</Grid>
</UserControl>
```

In Listing 17.7, you can see that two GridSplitter controls, split1 and split2, are added in the third row and second row. The first GridSplitter control, split1, exists in the third row of the Grid control and spans two columns. The HorizontalAlignment property of split1 is set to Stretch, which implies that it adjusts the size of the row by expanding or contracting its contents. The second GridSplitter control, split2, has its VerticalAlignment property set to Stretch, which allows the columns to be resized.

NOTE

> The Baby Panda.jpg and My Myla.jpg images are added to the current project folder by selecting TextImageAppCS→Add→Existing Item in Solution Explorer.

+   2. Press the F5 key on the keyboard to run the TextImageAppCS application. The output appears, as shown in Figure 17.32:

![](bbox=[0.23, 0.535, 0.73, 0.865])

Figure 17.32: Output of the TextImageAppCS Application

+   3. Click and drag either of the GridSplitter controls. Notice that the rows and columns are automatically resized, as shown in Figure 17.33: