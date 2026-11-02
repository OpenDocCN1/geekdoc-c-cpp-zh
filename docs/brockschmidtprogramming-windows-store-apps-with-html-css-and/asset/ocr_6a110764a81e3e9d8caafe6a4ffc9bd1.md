![](bbox=[0.14, 0.09, 0.72, 0.26])

FIGURE 7-14 The HTML ListView item templates sample showing multisize items through cell spanning.

Tip #1 If you start playing with this sample and make changes to the CSS in any given scenario, be aware that it does not scope the CSS for each scenario to the associated page, which can mean that styles from the most recently loaded scenario are used by the others. To correct this, I’ve added such scoping to the modified sample in this chapter’s companion content.

Tip #2 If you alter items in a cell spanning layout, call the ListView.recalculateItemPosition method after the change is made. If you’re using a data source other than the Binding.List, also call the IListDataSource.beginEdits before making changes and endEdits afterwards.

The basic idea of cell spanning is to define a layout grid based on the size of the smallest item. For best performance, make the grid as coarse as possible, where every other element in the ListView is a multiple of that size.

You define the cell grid through the CellSpanningLayout.groupInfo property. This is a function that returns an object with three properties: enableCellSpanning, which is set to true (unless you want GridLayout behavior), and cellWidth and cellHeight, which contain the pixel dimensions of your minimum cell. In the sample (see js/data.js), this function is named groupInfo like the layout’s property. I’ve given it a different name here (and omitted some other bits) for clarity:

```
function cellSpanningInfo() {
  return {
    enableCellSpanning: true,
    cellWidth: 310,
    cellHeight: 80
  };
}
```

Tip In thinking about the layout of your ListView, know that there are three styles in the WinJS stylesheets that set default item spacing. You can override these with the same selectors depending on your orientation, and they’re important to know for calculations that we’ll see shortly:

```
.win-horizontal .win-gridlayout .win-container {
  margin: 5px;
}
.win-vertical .win-gridlayout .win-container {
  margin: 5px 24px 5px 7px;
}
.win-rtl > .win-vertical .win-gridlayout .win-container {
  margin: 5px 7px 5px 24px;
}
```