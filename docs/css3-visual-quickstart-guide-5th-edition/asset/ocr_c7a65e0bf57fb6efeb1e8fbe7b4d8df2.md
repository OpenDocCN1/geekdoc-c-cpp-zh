# TABLE 8.8 Border-Collapse Values

| Value | Compatibility |
| --- | --- |
| collapse | IE5.5, FF1, O5, S1, C3, CSS2 |
| separate | IE5.5, FF1, O5, S1, C3, CSS2 |
| inherit | IE5.5, O5, S1, C3, CSS2 |

# # Collapsing Borders Between Table Cells

Every table data cell defined by the `<td>` tag has four borders: top, right, bottom, and left. The **border-collapse** property (Table 8.8) allows you to set a table so that each table data cell share its borders with an adjacent table data cell rather than creating a separate border for each.

Code 8.8 `list-table-properties.css`—The-collapse property lets you remove any space between the table data cells, giving each a single border A (on the following page), but border spacing being ignored. Use **separate** to allow **border-spacing** to work (on the following page):

## To collapse the borders in a table:

```
*** CSS3 VOS | Chapter 8 |
| list-table-properties.css ***

ul {
  list-style: url(../images/bullet-01.png) inside;
}

nav.global {
  list-style: none;
}

table {
  table-layout: auto;
  border-spacing: 8px;
  border-collapse: separate;
  width: 75%;
  margin: 40px auto;
}

caption, table caption {
  font: italic 1.25em Constantia, Georgia;
  Times, 'Times New Roman', Serif;
}

t {
  font-size: 1.25em;
}

td {
  vertical-align: top;
  padding: .5em;
  background-color: rgba(200, 200, 180,.25);
  border: 1px solid rgb(200, 200, 180);
}
```

+   1. Add the border collapse property to a table element. Type border-collapse, followed by a colon () (Code 8.8).
   border-collapse:

+   2. Specify how borders should collapse.
   Type one of the following to how you want to display the borders in the table:
   * collapse will make adjacent table data cells share a common border; however, you won't be able to set cell-spacing if borders are collapsed.
   * separate will maintain borders for each table data cell.

List and Table Properties 223