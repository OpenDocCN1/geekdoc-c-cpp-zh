specified element. A descendant selector is created by first listing the parent selector, a space, and finally the descendant selector you want to target.

In the following example, as shown in Figure 7-8, the anchor tags which are descendants of the unordered list are selected, and those hyperlinks are styled with a blue font color and are crossed out. The Parody Non-Tech Twitter accounts are not styled because they are not descendants of an unordered list.

```
ul a {
    color: blue;
    text-decoration: line-through;
}
```

![](bbox=[0.232, 0.374, 0.64, 0.625])

Figure 7-8: Child selector used to style the Parody Tech Twitter accounts.

**Tip:** Interested in styling just the first anchor tag within a list, like the Modern Seinfeld Twitter account, or the second list item, like the Vinod Coleslaw Twitter account? Go to w3schools.com and read more about the first-child (www.w3schools.com/cssref/sel_firstchild.asp), and nth-child selectors (www.w3schools.com/cssref/sel_nth-child.asp).

# ### Naming HTML elements

The other way of styling specific elements in CSS is to name your HTML elements. You name your code by using either the id or class attribute, and then style your code by referring to the id or class selector.