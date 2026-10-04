Note that the header, PageWrapper, nav, and footer elements have an exact width of 844 pixels. This way, the site fits nicely on screens with a size of 1024 x 768 pixels, still a reasonably common screen size for many of today's computers, without being squeezed between the Windows borders. Systems with bigger screens center the site in the available space. This centering is done by the PageWrapper element, which has its margin set to auto. This means the available space on the left and right sides (not at top and bottom) is equally divided, effectively centering the PageWrapper element in the browser window. As an alternative to fixed width layouts, you can create a responsive layout that adapts to the visitor's screen size. The Bootstrap framework mentioned earlier makes this very easy.

Note also that the MainContent section and the aside are positioned next to each other. You do this with the CSS float property:

```
section#MainContent
{
  width: 664px;
  float: left;
}
```

```
aside
{
  background-color: Gray;
  width: 180px;
  float: left;
}
```

This tells the MainContent to "float" on the left side of content that follows it, effectively placing the aside to the right of it. You will need to tell the aside to float as well; if you leave it out, it will be placed at the left of the page, right where you applied the CSS. If you have multiple aside elements in your site (which is a common practice), you can target this aside that acts as a sidebar by adding an id attribute (such as Sidebar) just as I did with the MainContent section element and then update the CSS as follows:

```
aside#Sidebar
{
  ...
}
```

The combined width of the MainContent and aside elements adds up to 844 pixels, which is exactly the width of their parent element: the PageWrapper.

To end the float and tell the footer element to be placed directly under the MainContent and aside elements, the clear property is used to clear any float (left or right) that may be in:

```
footer
{
  background-color: #C0C0C0;
  width: 844px;
  clear: both;
}
```

The gray backgrounds are just temporarily added to the code, so it's easier to see what <div> ends up where. In future exercises, you modify the CSS again to fit the scheme of the Planet Wrox website.