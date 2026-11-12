| Value | | | | | | |
|---|---|---|---|---|---|---|
| <length> | ○ | ○ | ○ | ○ | ○ | ○ |
| inherit | ○ | ○ | ○ | ○ | ○ | ○ |

Code 8.7 Added to list-table-properties: The border-spacing property works like a margin around the table data cell A.

```
table {
 border-spacing: 8px;
}
```

![](bbox=[0.065, 0.345, 0.455, 0.715])

Code 8.7 applied to Code 8.1: Spacing out data cells can make them easier for users to scan.

# Setting the Space Between Table Cells

Although table data cells and table header cells can use many of the box properties we'll explore in Chapter 10, they cannot use the margin property. Instead, CSS has the border-spacing property (Table 8.7) property, which sets an equal amount of space between data cells' top, bottom, left, and right sides.

# To collapse the borders in a table:

+   1. Add the border spacing property to the CSS rule for a table element. Type border-spacing, followed by a colon (:) (Code 8.7). border-spacing:

+   2. Specify the spacing between table data cells. 8px;

Type a length value (such as 8px) to specify the distance between cells. (See “Values and Units Used in This Book” in the Introduction.) Alternatively, use inherit to use the same border spacing as a cell’s parent element.