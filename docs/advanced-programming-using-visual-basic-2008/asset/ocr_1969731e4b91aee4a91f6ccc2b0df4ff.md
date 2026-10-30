# The TableAdapter and TableAdapterManager

Although the user can make changes to the dataset in memory, no changes are made to the original data source until you execute the Update method of the TableAdapter or the UpdateAll method of the TableAdapterManager. You can choose to perform updates after every change, or once when the program terminates.

The TableAdapterManager, which is new for Visual Studio 2008, manages updates to multiple related tables. For single tables, such as we are updating first, a TableAdapter is all that is needed. If you use the Update Wizard to update a database application created in an earlier version of Visual Basic, you do not generate a TableAdapterManager and updates are performed with the TableAdapter.Update method. By default, in new database applications that you create with Visual Studio 2008, creating a TableAdapter also creates a TableAdapterManager.

Later in this chapter in the section "Updating Related Tables," you will learn about hierarchical updates performed with a TableAdapterManager. You can prevent the automatic addition of a TableAdapterManager in a single-table application by setting the dataset's HierarchicalUpdate property to false before dragging any tables or fields to a form.

Both the TableAdapter.Update and TableAdapter.UpdateAll methods save the changes from the dataset to the original data source.

# The Update and UpdateAll Methods—General Form

```
TableAdapter.Update(DataSet.table)
TableAdapterManager.UpdateAll(DataSet)
```

Notice that the TableAdapterManager.UpdateAll method specifies only the dataset name; the TableAdapter.Update method can specify only the dataset name if it has only one table; otherwise you must supply DataSetName.TableName.

# The Update and UpdateAll Methods—Examples

```
PublishersTableAdapter.Update(ContactsDataSet.Publishers)
PublishersTableAdapter.Update(ContactsDataSet)
TableAdapterManager.UpdateAll(ContactsDataSet)
```

You can decide when to execute an update method. You can save the change every time an add, edit, or delete occurs, or you can wait until the program terminates. Or combine the two techniques by providing a Save option on a menu or button and then prompting for unsaved changes when the program terminates. This technique matches Office applications: You can save a document any time you want, but if you try to close without saving the changes, a dialog box displays.