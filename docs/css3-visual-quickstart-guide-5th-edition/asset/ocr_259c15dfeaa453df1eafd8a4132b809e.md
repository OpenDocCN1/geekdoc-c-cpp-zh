+   - Makes browser styles consistent.

Ensures values across all browser types and versions are the same. Because browsers slightly vary their default style values, a good reset will allow your designs to appear with greater consistency regardless of how your visitor is viewing it.

To use a CSS reset, simply add the desired code at the top of your CSS code. That's it. The code does the rest.

# A simple CSS reset

The easiest way to reset styles is to use the universal selector and set the default styles you want applied to all tags, as shown in Code 13.4. Remember that you want to keep your CSS reset compact. Code 13.5 does the same thing but removes spaces and returns.

Code 13.4 cssreset-simple.css—This version of the CSS uses

the universal selector to reset the browser default values of several key properties including margin, padding, border, outline, height, vertical-align, and text-decoration.

```
* {margin: 0;
padding: 0;
border: 0;
outline: 0;
line-height: 1.4em;
vertical-align: baseline;
text-decoration: none; }
```

Code 13.5 cssreset-simple.css—The same code as 13.4, but it's compressed by removing all line breaks and spaces.

> *** CSS3 VOS | Chapter 13 |
*** cssreset-simple.css ***

```
*{margin:0;padding:0;border:0;
- line-height:1.4em;
- baseline;text-decoration:none;}
```

This is a quick way to reset the most important styles, but it has one drawback: IE6 does not recognize the universal selector. If you are concerned about supporting IE6, you will want to include all the HTML tags in the selector list. The advantage of using the universal selector, other than compactness, is that it will always apply itself to new HTML tags as they become.