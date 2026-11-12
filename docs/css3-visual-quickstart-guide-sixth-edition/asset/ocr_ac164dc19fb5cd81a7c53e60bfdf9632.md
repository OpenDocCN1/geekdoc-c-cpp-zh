| Value |
|---|
| top |
| bottom |
| inherit |

Code 8.10 Added to list-table-properties.css — The caption-side property lets you specify whether the caption should appear above (top) or below (bottom) the table.

```
/* *** list-table-properties.css ***/
table {
  caption-side: bottom;
}
```

![](bbox=[0.065, 0.395, 0.445, 0.745])

The caption is forced to the bottom of the table rather than its natural position at the top.

# Setting the Position of a Table Caption

The <caption> tag lets you embed identifying text in a table. You can set the align attribute in the tag to define where the caption should appear in relation to the table, but this is being deprecated in favor of the CSS caption-side property (Table 8.10), which does the same thing.

# To set the position of a caption in relation to its table:

+   1. Add the caption side property to your CSS. Type caption-side, followed by a colon (:) (Code 8.10). caption-side:
+   2. Type a keyword indicating which side of the table you want the caption to appear: top or bottom. bottom;