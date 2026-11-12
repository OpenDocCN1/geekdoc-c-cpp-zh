# # Creating a Multi-Column Text Layout

Although you'll learn how to create a column grid layout in Chapter 13, you can use the new column properties to create balanced columns of text, similar to a newspaper style. Although not useful for extremely long columns of text, text columns can be a great way to give intro blurbs some style.

# ## To set up multi-column text:

+   1. Start your declaration by typing the column-count property name, followed by a colon (:) along with the number of columns (Tables 10.20 and 10.23) you want as an integer (Code 10.13).
+   -webkit-column-count: 2;
+   -moz-column-count: 2;
+   column-count: 2;

+   2. Add the column-gap property name, followed by a colon (:) along with the width of the separation (called a gutter) you want between the columns (Table 10.22). This can be any standard length value.
+   -webkit-column-gap: 4em;
+   -moz-column-gap: 4em;
+   column-gap: 4em;

```
Code 10.13 Added to box-properties.css—When applied to Code 101, the first paragraph splits into two columns with a line between them A.
/*** box-properties.css ***/
article h2 + p {
  -webkit-column-count: 2;
  -moz-column-count: 2;
  column-count: 2;
  -webkit-column-gap: 50px;
  -moz-column-gap: 5%;
  column-gap: 5%;
  -webkit-column-rule: 2px groove
    • rgba(0,0,0,.5);
  -moz-column-rule: 2px groove
    • rgba(0,0,0,.5);
  column-rule: 2px groove rgba(0,0,0,.5);
}
```

| Value | Browser Support |
|---|---|
| <integer> | ●10 ◇ ◇ ◇ ● |
| auto | ●10 ◇ ◇ ◇ ● |

| Value | Browser Support |
|---|---|
| <border-width> | ●10 ◇ ◇ ◇ ● |
| <border-style> | ●10 ◇ ◇ ◇ ● |
| <color> | ●10 ◇ ◇ ◇ ● |