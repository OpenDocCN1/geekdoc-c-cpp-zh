A small demonstration of this can be found in scenarios 2 and 3 of the [HTML ListView incremental loading behavior sample](#), which adds more items to a Binding.List when needed from within the item renderer.

# ## Drag and Drop

It’s very natural when one is looking at a collection of neat stuff to want to copy or move some of that neat stuff to some other location in the app. [HTML5 drag and drop](#) provides a standard for how this works between elements, and the ListView is capable of participating in such operations with both mouse and touch.

To briefly review the standard, a draggable element has the `draggable="true"` attribute. It becomes a source of a `dataTransfer` object (that carries the data) and sees `dragstart`, `drag`, `dragenter`, `dragleave`, `dragover`, and `dragend` events at appropriate times (for a concise reference, see [DragEvent](#) on MSDN). A target element, for its part, will see `dragenter`, `dragleave`, `dragover`, and `drop` events and have access to the `dataTransfer` object. There’s more to it, of course, such as drop effects that can be set within various events in response to the state of the Ctrl and Alt keys, but those are the basics.

The ListView implements these parts of the HTML5 spec on your behalf, surfacing similar events and giving you access to the `dataTransfer` object, whose `setData` and `getData` methods are what you use to populate and retrieve the data involved.

There are four ways the ListView can participate in drag and drop. First, it can be made reorderable within itself, independent of exchanging items with other sources or targets. Second, it can be made a drag source, so you can drag items from the ListView to other HTML5 drag targets. Third, the ListView can be a drop target and accept data dragged from other HTML5 sources. And fourth, items within a ListView can themselves be individual drop targets. (Note that ListView and HTML5 drag and drop is not presently enabled between apps, just within an app.)

Let’s go through each of these possibilities using examples from the [HTML ListView reorder and drag and drop sample](#). Reordering in a ListView is perhaps the simplest: it requires nothing more than setting the `itemsReorderable` option to true, as demonstrated in scenario 1 (`html/scenario1.html`):

```
```html
<div id="listView" data-win-control="WinJS.UI.ListView" data-win-options="{
    itemDataSource: myData.dataSource, itemTemplate: smallListIconTextTemplate,
    itemsReorderable: true, layout: { type: WinJS.UI.GridLayout } }">
</div>
```
```

That’s it—with this one option and no other code (you can see that `js/scenario1.js` does nothing else), you get the behavior shown in [Video 7-3](#), for both single and multiple items (shown with the mouse as it’s more efficient). Under the covers, reordering of the ListView fundamentally means moving items in the data source, in response to which the ListView updates its display. To be precise, the ListView uses the `moveBefore` and `moveAfter` methods of `IListDataSource` to do the reordering. This implies, of course, that the data source itself is reorderable. If it isn't, you'll get an exception