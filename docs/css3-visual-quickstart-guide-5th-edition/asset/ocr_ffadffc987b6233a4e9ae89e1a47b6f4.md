# Setting the Table Layout

Different browsers use different methods to calculate how a particular table should be displayed. Two primary table-layout (Table 8.6) methods are favored:

+   - Fixed method bases its layout on the width of the table and the width of columns in the first row. This method is generally faster than automatic.

+   - Automatic uses the table column width along the amount of content in the table data cell width. This will generally render more slowly than the fixed method, but it also produces more accurate results for widths throughout the table.

Table 8.6 Table-Layout Values

| Value | Compatibility |
|---|---|
| fixed | IE5.5, O5, S1, C1, CSS2 |
| auto | O5, S1, C1, CSS2 |
| inherit | IE5.5, O5, S1, C1, CSS2 |

Code 8.6 list-table-properties: The table-layout property forces you the browser to use either the fixed or auto methods for rendering tables. I've also cheated a little here and set the width and margin for the table, which you will not learn until Chapter 10.

```
*** CSS V5 | Chapter 8 |
- list-table-properties.css ***

ul {
  list-style: circle url(../images/bullet-01.png) inside;
}

av.global ul {
  list-style: none;
}

table {
  table-layout: auto;
  width: 75%;
  margin: 40px auto;
}
```

To set the table layout method:

+   - Add the table layout property to a CSS rule for a table element. Type table-layout, followed by a colon (:) on table elements (Code 8.6).

table-layout: