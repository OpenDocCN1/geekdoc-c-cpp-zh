So the rules would be applied only to list items that were inside `nav` elements – not “ordinary” lists. To see the effect of each declaration, we’ll follow the same method described in the tip on page 28, by adding the empty rules and then adding in the declarations one at a time. If you add in the declarations in the order described below it will help you to understand how the stylesheet works.

# **1.**

```
nav ul {
  list-style-type: none;
}
nav ul li {
}
nav ul li:last-child {
}
nav ul li a {
}
```

Removes the bullet points from lists inside `nav` elements. You can change the appearance of the bullet point or remove it completely using the `list-style-type` declaration.

+   - `list-style-type: none;` removes the bullet point
+   - `list-style-type: square;` changes them to squares.

![](bbox=[0.422, 0.242, 0.983, 0.367])

# **2.**

```
nav ul {
  list-style-type: none;
  background-color: #B577B5;
}
nav ul li {
}
nav ul li:last-child {
}
nav ul li a {
}
```

Changes the background color of the list (the `ul` element) to a darker purple (`#B577B5` is the hexadecimal value for this color).

![](bbox=[0.422, 0.472, 0.982, 0.609])

# **3.**

```
nav ul {
  list-style-type: none;
  background-color: #B577B5;
  border: 4px solid #111111;
}
nav ul li {
}
nav ul li:last-child {
}
nav ul li a {
}
```

Adds a 4-pixel-wide border to the list. The border is solid, rather than dotted or dashed, and is a solid black (`#111111` is the hexadecimal value for this color). Try changing:

+   - the pixel width of the border
+   - the border style from **solid** to **dotted** or **dashed**
+   - the hexadecimal value to one you choose from an online color picker (see page 31).

![](bbox=[0.422, 0.832, 0.982, 0.961])