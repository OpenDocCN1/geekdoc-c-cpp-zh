![](bbox=[0.285, 0.064, 0.67, 0.478])

Figure 10.3: Contacts table view

When we're working within one view, this isn't too much of an issue. We have a direct relationship between the view elements being manipu-lated by the user and the elements displayed by the view. However, what about any other view that exists in the hierarchy that is not currently being displayed but still has elements that are being manipulated?

A good example of this is the Contacts application that exists on every Cocoa Touch device. The primary view for this application is a table listing all the contacts in the database, as shown in Figure 10.3.

In addition to this table view, we also have a detail view that displays a single contact, as shown in Figure 10.4, on the following page. It is this detail view that handles all the editing of a contact. However, when a detail of that contact gets edited that is also displayed in the parent table view, how does that table view get notified to update its display values?