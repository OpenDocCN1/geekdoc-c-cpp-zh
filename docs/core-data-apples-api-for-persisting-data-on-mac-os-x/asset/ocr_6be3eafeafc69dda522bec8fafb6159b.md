![](bbox=[0.18, 0.072, 0.733, 0.273])

Figure 3.4: Accessing an existing NSFormatter on an element

# NSObjectController

NSObjectController shares a lot of similarities with the NSArrayController discussed earlier. However, unlike the NSArrayController, the NSObjectController is designed to represent one instance rather than an array of instances. One common usage of the NSObjectController is to represent the selected object of an NSArrayController, thereby making it clearer as to what data is being displayed in the interface elements that are bound to the NSObjectController as opposed to an NSArrayController. Another common usage is to have an entire interface, such as a detail sheet or child window, be bound to the values within an NSObjectController and then have the File’s Owner reference and populate that NSObjectController. In this design, the File’s Owner (usually a subclass of NSWindowController) simply has to populate the NSObjectController with a call to -setContent:, and the entire UI will get populated automatically. This again makes the maintenance of the code very easy and also improves readability.

# NSOutlineView

If we wanted to change the look of our application, we could display a single NSOutlineView instead of the two table views we have currently. With an NSOutlineView, we could display a list of recipes with a hierarchy of ingredients listed under them, as depicted in Figure 3.5, on the next page.

NSOutlineView shares a lot in common with the NSTableView object. In fact, it is a subclass of NSTableView. The major difference is that the NSOutlineView displays data in both a column format as well as a hier-