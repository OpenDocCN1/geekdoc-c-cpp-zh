```
```css
a:link{
    color: rgb(6,69,173);
    text-decoration: none;
}
a:visited {
    color: rgb(11,0,128)
}
a:hover {
    text-decoration: underline
}
a:active {
    color: rgb(250,167,0)
}
```
```

![](bbox=[0.122, 0.307, 0.206, 0.381])

Remember to include the colon between the a selector and the link state.

![](bbox=[0.122, 0.386, 0.206, 0.458])

Although explaining why is out of the scope of this book, CSS specifications insist that you define the various link states in the order shown here — link, visited, hover, and then active. However, it is acceptable to not define a link state, as long as this order is preserved.

The various link states are known as *pseudo-class selectors*. Pseudo-class selectors add a keyword to CSS selectors and allow you to style a special state of the selected element.

![](bbox=[0.23, 0.539, 0.864, 0.922])

**Figure 6-6:** Wikipedia.org page showing link, visited, hover, and active states.