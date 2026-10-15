# Chapter 11: Working with Typography and Documents in WPF

In Listing 11.3, we have used the Capitals property of the OpenType font to display the text in capital letters. We have also used the Variants property to create a subscript text.
The output of Listing 11.3 is shown in Figure 11.3:

![](bbox=[0.35, 0.16, 0.65, 0.28])

Figure 11.3: Showing the Output of the ManipulatingTypography Application

# Wrapping the Text

In WPF, when text is typed inside a TextBlock control, the text appears in a continuous line. However, you can use the TextBlock.TextWrapping property to display the text in the next line when it reaches right edge of the TextBlock control. Possible values for this property are WrapWithOverflow, NoWrap, and Wrap. By default, the value of this property is set to NoWrap. Let’s create a WPF application named TextWrapping (also available on the CD-ROM) to learn how to wrap the text. For this, add the code given in Listing 11.4 to MainWindow.xaml of TextWrapping:

# Listing 11.4: Showing the Code to Wrap the Text

```
<window x:Class="textwrapping.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="120" Width="300">
    <Grid>
        <TextBlock FontFamily="Century Gothic" FontSize="15" FontWeight="Bold"
            TextAlignment="Left" TextWrapping="Wrap">
            This is an example of text wrapping in a TextBlock. The text appears as
            in the next line.
        </TextBlock>
    </Grid>
</window>
```

In Listing 11.4, we have added some text to the TextBlock control and set the TextWrapping property to Wrap. The output of Listing 11.4 is shown in Figure 11.4:

![](bbox=[0.33, 0.75, 0.66, 0.88])

Figure 11.4: Showing the Output of the TextWrapping Application

# Trimming the Text

In WPF, you can trim the text when it goes beyond the length of the container by using the TextTrimming property. This property takes any of the three values: None, CharacterEllipsis, and WordEllipsis. Table 11.25 lists the values of the TextTrimming property:

# Table 11.25: Showign the List of the TextTrimming Property Values

| Members | Description |
|---|---|
| None | Does not trim the text |
| CharacterEllipsis | Trims the text at the character boundary and draws an ellipsis in place of the remaining text |
| WordEllipsis | Trims the text at the word boundary and draws an ellipsis in place of the remaining text |