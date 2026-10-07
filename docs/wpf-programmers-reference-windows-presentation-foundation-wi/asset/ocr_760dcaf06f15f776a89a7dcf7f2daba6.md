# ODD FORMATTING

The XAML code for the caffeine formula $C_8H_{10}N_4O_2$ is formatted somewhat strangely, with line breaks inside the Run elements. If the Runs are placed on separate lines, WPF adds some space around them, spreading the formula out and making it look odd. This also allows the FlowDocument to break the formula in the middle.

The unusual formatting keeps the text on one logical line in the XAML code so the pieces of the formula stay together.

(To make even more confusing, if you copy-and-paste the formula's XAML code in Visual Studio, the editor reformats the code to place each Run on a separate line, making the result ugly again.)

# Section

A Section groups other block-level elements such as Paragraphs, Lists, and Tables. A Section adds some additional space around its contents so you can use it to separate parts of the document.

For example, you could place two groups of paragraphs in different sections to increase the spacing between the two groups slightly. The effect is somewhat subtle, however, so you may want to include section headers in a distinctive font to make the break more obvious.

A Section can also change the appearance of the objects it contains by setting its Background, Foreground, FontSize, BorderBrush, and other properties.

# Table

A Table displays its contents in rows and columns. The Table.Columns element attribute the widths of the columns. For example, the following code fragment defines five columns. The first has a width of 100 pixels, and the other columns divide the remaining width evenly.

```
<Table CellSpacing="5">
<TableColumns>
  <TableColumn Width="100"/>
  <TableColumn />
  <TableColumn />
  <TableColumn />
  <TableColumn />
</TableColumns>
..
</Table>
```

![](bbox=[0.045, 0.693, 0.103, 0.733])