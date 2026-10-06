Using Qt's model/view architecture, we can use models that fetch only the data that is actually needed for display in the view, making it possible to handle very large data sets without compromising performance. And by registering a model with two or more views, we can give the user the opportunity to view and interact with the data in different ways, with little overhead. Qt automatically keeps multiple views in sync, reflecting changes to one in all the others, as illustrated in Figure 10.2. An additional benefit of the model/view architecture is that if we decide to change how the underlying data set is stored, we just need to change the model; the views will continue to behave correctly.

# Figure 10.2. One model can serve multiple views

![](bbox=[0.09, 0.35, 0.54, 0.46])

In many situations, we need to present only relatively small numbers of items to the user. In these common cases, we can use Qt's convenience item view classes (QListWidget, وكذلك, QTreeWidgetItem) and populate them with items directly. These classes behave in a similar way to the item view classes provided by earlier versions of Qt. They store their data in "items" (e.g., QWidgetItem contains QWidgetItemItems). Internally, the convenience classes use custom models and the view, making the possible items visible to the user.

For large data sets, duplicating the data is not an option. In these cases, we can use Qt's views (QListView, UITableView, QTreeView) in conjunction with a data model, which can be a custom model or one of Qt's predefined models. For example, if the data set is held in a database, we can combine a QTableView with QSqlTableModel.

# Using the Item View Convenience Classes

Using Qt's item view subclasses is usually simpler than defining a custom model and is appropriate when we don't need the benefits of separating the model and the view. We use this technique in Chapter 4 when we subclass QWidgetItem and QTableWidgetItem to implement spreadsheet functionality.

In this section, we will show how to use the item view subclasses to display items. The first example shows a read-only QListWidget (Figure 10.3), with