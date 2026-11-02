![](bbox=[0.13, 0.08, 0.9, 0.35])

FIGURE 6-6 Changing properties of objects in either the array or the list will change the properties in the other, because both are still referencing the same object.

All of this is important to keep in mind as you're building more complex UI around a data source of some kind, whether using controls like the ListView or a custom control built on the List. That is, if you have code that modifies the array—or UI capabilities in the control to modify the List—you'll know how the list and the array will be correspondingly affected. Otherwise you might be left scratching your head wondering just why certain changes to the list or array (item replacement) don't affect the other whereas other changes (via properties) do!

Indeed, in scenario 2 you might notice that the span element that's data-bound to the item from List.getAt(0) automatically updates when changes came through the List but not when they came through the array. This is because the binding mechanics are watching the list's item, not the array item sitting beneath it. In such cases, be sure to make modifications through only the List.

It's also good to know how the array and List relate when you start using projections of the List, because changes to the projections will propagate to the original List as well, as we'll see next.

# ## List Projections

The idea of a *projection* comes from the world of databases and data sources to mean a particular view of a data source that is yet completely connected to that source. Projections are typically used to massage a raw data source into something more suitable for data binding to your UI but without altering the original source.

For example, a data source for your personal contacts might have those contacts listed in any order and would of course contain the entire collection of those contacts. In an app's UI, however, you probably want to sort and resort those contacts by one or more fields in each record. Each time you change the sort order in the UI, you'd create another sorted projection and bind the UI to it. Again, creating a projection doesn't alter the data source. At the same time, changing properties of an item in the projection, inserting or removing items, or otherwise modifying the projection does propagate those changes back to the source. Similarly, if you add, remove, or change items in the underlying