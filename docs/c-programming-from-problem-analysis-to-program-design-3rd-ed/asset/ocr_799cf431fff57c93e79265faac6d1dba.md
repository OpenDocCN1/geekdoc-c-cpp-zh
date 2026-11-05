Also shown in Figure 15–10 a new menu option, **Style**, which includes features to **Add a Style Rule** or **Build a Style** is included. By definition a **style sheet** includes a list of rules. Each rule consists of a selector and one or more declaration blocks. The declaration block is enclosed in curly braces. Inside the block you will find a property, colon, and a value. Like C#, each property assignment ends with a semicolon. Example 15–2 shows the CSS for the body that was included when the Web site was created.

# Example 15-2

```
```css
body
{
    background: #b6b7bc;
    font-size: .80em;
    font-family: "Helvetica Neue", "Lucida Grande", "Segoe UI",
                 Arial, Helvetica, Verdana, sans-serif;

    margin: 0px;
    padding: 0px;
    color: #696969;
}
```
```

You can go directly into the Sites.css file and type new values or add additional property lines. Another option, a better option, is to use the **Modify Style** configuration wizard. As you look back at Figure 15–10, you will notice that the **Properties** window has a single entry, **Style**. It does not matter which of the elements or classes you select, there is always just that one property. You can select an element using the **Outline** window or from the actual .css file in the center window. Both ways will reveal the property for the item you select. When you click the ellipsis for the **Style** value, the **Modify Style** dialog box shown in Figure 15–11 is revealed.

![](bbox=[0.177, 0.59, 0.63, 0.894])

Figure 15-11   Modify Style