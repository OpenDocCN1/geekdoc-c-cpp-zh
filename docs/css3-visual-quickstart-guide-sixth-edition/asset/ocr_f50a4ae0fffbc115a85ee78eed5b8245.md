# 2. Type a value for the margin.

```
.35em .2em .2em 0;
```

Use one of the following values:

+   A length value

+   A percentage, which creates a margin proportional to the parent element's width

+   auto, which returns control of the margins to the browser's discretion

You can enter one to four values, separated by spaces, to define the margins as follows:

+   One value sets the margin for all four sides equally.

+   Two values set the top/bottom margins and left/right margins.

+   Three values set the top margin, the left/right margins (the same), and the bottom margin.

+   Four values set each margin clockwise, starting from top: top, right, bottom, and left.

# 3. You can also set the margin for just one side of the box independently without setting the other three margins.

```
margin-bottom: 60px;
```

This is useful when used with an inline style to override margins set elsewhere. To do this, specify the margin side you want to define (margin-top, margin-bottom, margin-left, or margin-right) and enter a legitimate margin value from Table 10.10.

You can also set margins for the <body> tag; in which case the margins define the distance that elements nested in the body should appear from the top and left sides of the browser window.

# Setting Negative Margins

Although you can use negative margins (for example, margin:-5em;) to create interesting effects for overlapping pieces of text, this method is frowned upon because various browsers present different results.

Overlapping text is better achieved using CSS positioning (see Chapter 11).

Be careful when setting negative margins around a hypertext link. If one element has margins that cause it to cover the link, the link will not work as expected.