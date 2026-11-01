![](bbox=[0.095, 0.088, 0.355, 0.225])

FIGURE 37-9

A figure aligns horizontally and vertically and can be anchored to the page, content, a column, or a paragraph. The Figure in the following code is anchored to the page center but with a horizontal and vertical offset. The WrapDirection is set so that both left and right columns wrap around the figure. Figure 37-10 shows the result of the wrap:

```
```xml
<Paragraph>
    <Figure HorizontalAnchor="PageCenter" HorizontalOffset="20"
        VerticalAnchor="PageCenter" VerticalOffset="20" WrapDirection="Both">
        <Paragraph Background="LightGray" FontSize="24">
            <Run>Lyrics Samples</Run>
        </Paragraph>
    </Figure>
</Paragraph>
```
```

![](bbox=[0.095, 0.46, 0.728, 0.608])

FIGURE 37-10

Floater and Figure are both used to add content that is not in the main flow. Although these two features seem similar, the characteristics of these elements are quite different. The following table explains the differences between Floater and Figure.

| CHARACTERISTICS | FLOATER | FIGURE |
|---|---|---|
| Position | A floater cannot be positioned. It is rendered where space is available. | A figure can be positioned with horizontal and vertical anchors. It can be docked relative to the page, content, column, or paragraph. |
| Width | A floater can be placed only within one column. If the width is set larger than the column size, it is ignored. | A figure can be sized across multiple columns. The width of a figure can be set to 0.5 pages or 2 columns. |
| Pagination | If a floater is larger than a column height, the floater breaks and paginates to the next column or page. | If a figure is larger than a column height, only the part of the figure that fits in the column is rendered; the other content is lost. |