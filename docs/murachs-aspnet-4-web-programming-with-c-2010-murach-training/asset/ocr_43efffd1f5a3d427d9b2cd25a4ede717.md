# The CSS for the Future Value form

```
/* The styles for the elements */
body
{
    font-family: Arial, Helvetica, sans-serif;
    font-size: 85%;
    margin: 0;
    padding: 0;
    background-color: #D3D3D3;
}
h1
{
    font-size: 140%;
    color: #0000FF;
    margin-top: 20px;
    margin-bottom: 15px;
}

/* The style for the page division */
#page
{
    width: 500px;
    margin: 0 auto;
    padding: 10px;
    background-color: White;
}

/* The style for the paragraphs that contain
the text that identifies the server controls */
.label
{
    float: left;
    width: 140px;
    margin-top: 2px;
    margin-bottom: 5px;
}
```

# Notes

+   - Each browser can have its own defaults for font family and font size. Because of that, you’ll want to set these properties explicitly in the style for the body element.
+   - You typically set the margins and padding for the body to zero so the body starts at the outer edges of the browser window. Then, if you set the left and right margins of the page division to auto, the page will be centered within the window.
+   - Each browser also has its own defaults for the spacing above and below headings and paragraphs. To control this spacing, you can set the margins and padding for these elements. The padding controls the space between the contents of the element and the border around it, if there is one, and the margins affect the space outside the border.
+   - You can use the float property to display a block element or image to the left or right of the block elements that follow it. This technique can be used to align the controls on a form without using a table.