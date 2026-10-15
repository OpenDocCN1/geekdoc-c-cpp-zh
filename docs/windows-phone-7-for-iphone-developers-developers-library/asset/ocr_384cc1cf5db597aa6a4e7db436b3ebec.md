For those familiar with .NET programming, this pattern might seem entirely backward. .NET programmers, especially those used to Windows Forms or ASP.NET programming, are used to gathering the data themselves and then stuffing the data into a control through some kind of data-binding mechanism. The concept of the controller being a passive participant that is invoked only when the UI control needs it often seems very strange indeed.

However strange it might seem to C# developers, this pattern is incredibly powerful and works amazingly well for iOS. Each type of delegate is required to expose a certain set of methods (some of which are optional, a very important point) so that the class utilizing the delegate can be assured that all delegated functionality is provided.

The agreement between a delegate and the class doing the delegation is very often defined explicitly in the form of a protocol. For example, the UITableViewController class is a handy controller that comes pre-equipped to conform to the two different protocols required by the UITableView control: UITableViewDelegate (the protocol that deals with handling events that occur within the control) and UITableViewDataSource (the protocol that defines how a delegate must provide rows, cells, groups, and other data for the table view).

Table 4.1 shows just a few of the methods that are part of the two delegate protocols that define the communication between the UITableView control and your application. As you will see later in this chapter, this pattern is very different from the way Silverlight controls communicate with your application in Windows Phone 7 applications.

# Table 4.1 Some Delegate Methods for iOS Table View Controllers

| Protocol | Method | Description |
|---|---|---|
| UITableViewDelegate | tableView:willSelectRowAtIndexPath: | Used to perform actions before selecting a row |
| UITableViewDelegate | tableView:didSelectRowAtIndexPath: | Invoked after a row has been selected by the user |
| UITableViewDataSource | tableView:cellForRowAtIndexPath: | Returns a configured cell to be rendered by the table view in the appropriate place |
| UITableViewDataSource | numberOfSectionsInTableView: | Returns the number of section groups in the view |
| UITableViewDataSource | tableView:numberOfRowsInSection: | Returns the number of rows in a given section |