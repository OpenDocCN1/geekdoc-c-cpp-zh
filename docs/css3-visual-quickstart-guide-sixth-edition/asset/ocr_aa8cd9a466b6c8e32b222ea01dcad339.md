# TABLE 8.4 List-Style-Position Values

| Value | | | | | |
|---|---|---|---|---|---|
| inside | ● | ● | ● | ● | ● |
| outside | ● | ● | ● | ● | ● |
| inherit | ● | ● | ● | ● | ● |

+   * Outside...Magnus es, domine, et laudabilis valde: magna virtus tua, et sapientiae tuae non est numerus. et laudare te vult homo.

+   * Inside...Magnus es, domine, et laudabilis valde: magna virtus tua, et sapientiae tuae non est numerus. et laudare te vult homo.

Outside is generally how bulleted lists are presented. You may want to override that by using inside.

Code 8.4 Added to list-table-properties: The list-style-position property allows you to specify how lines of text flow under the bullet.

```
/*** list-table-properties.css ***/
ul {
 list-style-position: outside;
}
nl.list {
 list-style-position: inside;
}
```

![](bbox=[0.07, 0.58, 0.46, 0.79])

Code 8.4 applied to Code 8.1: outside pushes the image bullet over, while inside pulls the disc bullet back.

# Setting Bullet Positions

Often, the text of a bulleted list item is longer than one line. Using the list-style-position property (Table 8.4), you can specify the position of wrapping text in relation to the bullet. Wrapped text that is indented to start below the first letter of the first line below text is called a hanging indent.

# To define the line position for wrapped text in a list item:

+   1. Add the list-style-position property to your declarations. Type list-style-position, followed by a colon (:) (Code 8.4).
+   list-style-position:

+   2. Specify the position type.
+   inside;
+   Type one of the following values to set text indentation:
+   > inside aligns the left edge of the bullet with the left edge of subsequent text.
+   > outside left aligns the first line of text with subsequent text, placing the bullet as a hanging indent.

> TIP Generally, bulleted lists that have a hanging indent (outside position) stand out much better than those without a hanging indent (inside position).