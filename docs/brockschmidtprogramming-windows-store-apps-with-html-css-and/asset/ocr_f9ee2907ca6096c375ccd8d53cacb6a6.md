![](bbox=[0.15, 0.12, 0.88, 0.55])

FIGURE 7-4 ListView elements as shown in the Grid App template home page. (All colored items are added labels and lines.)

There’s quite a bit going on with the ListView in this project, so we’ll take one part at a time. For starters, the control’s markup in pages/groupedItems/groupedItems.html is very basic, where the only option is to indicate that the items have no selection behavior:

```
<div class="groupeditems list win-selectionstylefilled" aria-label="List of groups"
  data-win-control="WinJS.UI.ListView"
  data-win-options="{ selectionMode: 'none' }"
  layout: { type: WinJS.UI.GridLayout, groupHeaderPosition: 'top' } >
</div>
```

Switching over to pages/groupedItems/groupedItems.js, the page’s ready method handles initialization:

```
ready: function (element, options) {
  var listView = element.querySelector(".groupeditemslist").winControl;
  listView.groupHeaderTemplate = element.querySelector(".headerTemplate");
  listView.itemTemplate = element.querySelector(".itemtemplate");
  listView.addEventListener("groupheaderinvoked", this.groupHeaderInvoked.bind(this));
  listView.oniteminvoked = this._itemInvoked.bind(this);
  listView.itemDataSource = Data.items.dataSource;
  listView.groupDataSource = Data.groups.dataSource;
  listView.element.focus();
}
```