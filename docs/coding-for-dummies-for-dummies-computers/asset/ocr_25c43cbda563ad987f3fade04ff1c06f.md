The HTML tree is called the *DOM* or *document object model*.

# ### Child selector

The Parody Non-Tech Twitter account anchor tags are immediate children of the paragraph tags. If you wanted to style just the Parody Non-Tech Twitter accounts, you can use the *child selector*, which selects the immediate children of a specified element. A child selector is created by first listing the parent selector, then a greater-than sign (>), and finally the child selector.

In the following example, the anchor tags that are immediate children of the paragraph tags are selected, and those hyperlinks are styled with a red font color and without any underline. The Parody Tech Twitter accounts are not styled because they are direct children of the list item tag. (See Figure 7-7.)

```
~~~css
p > a {
  color: red;
  text-decoration: none;
}
~~~
```

![](bbox=[0.23, 0.55, 0.64, 0.81])

**Figure 7-7:** Child selector used to style the Parody Non-Tech Twitter accounts.

If you use just the *a* selector here, all the links on the page would be styled instead of just a selection.

# ### Descendant selector

The Parody Tech Twitter account anchor tags are descendants, or located within, the unordered list. If you wanted to style just the Parody Tech Twitter accounts, you can use the *descendant selector*, which selects not just immediate children of a specified element but all elements nested within the