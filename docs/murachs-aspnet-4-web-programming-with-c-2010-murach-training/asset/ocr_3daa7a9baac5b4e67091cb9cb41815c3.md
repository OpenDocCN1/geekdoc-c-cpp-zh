# Common block elements

| Element | Description |
|---|---|
| div | Lets you structure a page into logical divisions that can be formatted and positioned with CSS. This element can contain text, inline elements, and other block elements. |
| h1 | Creates a level-1 heading with content in bold at 200% of the base font size. |
| h2 | Creates a level-2 heading with content in bold at 150% of the base font size. |
| h3 | Creates a level-3 heading with content in bold at 117% of the base font size. |
| h4 | Creates a level-4 heading with content in bold at 100% of the base font size. |
| h5 | Creates a level-5 heading with content in bold at 83% of the base font size. |
| h6 | Creates a level-6 heading with content in bold at 67% of the base font size. |
| p | Creates a paragraph of text at 100% of the base font size. |

# A page that uses block elements

```
<div id="page">
    <div id="main">
        <h1>Murach Books</h1>
        <h2>New! HTML, XHTML, and CSS</h2>
        <p>This book teaches you how to develop web pages the professional way, using HTML/XHTML to provide the content and structure of the elements on a page and CSS to format and lay out those elements.</p>
    </div>
    <div id="footer">
        <p>&copy; Copyright 2010 Mike Murach &amp; Associates, Inc.</p>
    </div>
</div>
```

# The page displayed in a web browser

![](bbox=[0.15, 0.56, 0.75, 0.7])

# Description

+   - *Block elements* are the main building blocks of a web site and can contain other elements. Each block element begins on a new line.
+   - You can use div elements to define divisions within the body of a document. This can help indicate the overall structure of the page.
+   - The base font and font size for headings and paragraphs are determined by the browser. You can change these values using CSS.