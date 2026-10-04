argument to each you supply a function that is executed for each item. The following each example alerts the contents of each table cell by looping over the items in the matched set and then calling alert. Again, you can try this out with your jQueryDemos.aspx page:

```
$('#DemoTable td').each(function()
{
    alert(this.innerHTML);
});
```

Two other important methods include parent and prev. These methods are used in DOM traversing, where you can “walk” up and down the document tree finding elements that are either below or above an item, or at the same level.

The prev method selects a matched element’s direct sibling. To see how this works, take a look at this:

```
alert($('#DemoTable td:contains("Row 1 Cell 2")').prev()[0].innerHTML);
```

What do you think this alerts? If you guessed “Row 1 Cell 1,” you’re right. The $ selector first selects the table cell in the second column of the first row by the text it contains. The prev method then returns its first sibling: the cell to the left of it. Because a matched set is a collection even if it contains only a single item, you still need to use an indexer (with [0]) to refer to that first item. The table cell then exposes an .innerHTML property that returns the content of the cell.

Finally, take a look at parent:

```
alert($('#DemoTable td:contains("Row 1 Cell 2")').parent()[0].innerHTML);
```

If you run this code in the demo page, you get the result shown in Figure 11-5.

If you’re not seeing this exact same HTML, make sure that the line that begins with alert is the only one inside your document ready function, because the other examples may influence the HTML for the table.

The selector is the same as in the previous example. The parent function then points to the <tr> around the matched table cell. Alerting the innerHTML then returns the HTML for the two cells that this row contains.

![](bbox=[0.58, 0.56, 0.88, 0.71])

# Common Mistakes When Working with jQuery

Depending on the complexity of the jQuery functionality you’re using, writing the code can be quite challenging. You need to take care of the proper capitalization, parentheses, brackets, commas, and more. When you find your jQuery code doesn’t run or has unexpected behavior, check to see if your code is suffering from the following problems.