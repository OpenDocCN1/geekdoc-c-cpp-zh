The next interesting parts of the MainViewController that we need to implement are the UITableViewDelegate and UITableViewDataSource methods.

# Implementing the -numberOfSectionsInTableView: Method

Download Recipe?/Classes/MainViewController.m

```
```objc
- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView
{
    return [[[self resultsController] sections] count];
}
```
```

To be able to ask for the number of rows in a section, the UITableView must first know the number of sections. In this method, we request the sections property of the NSFetchedResultsController, which returns an NSArray of NSFetchedResultsSectionInfo implementations. Since we need to know only the number of sections, we return a call to -count on the resulting NSArray.

# Implementing the -tableView:numberOfRowsInSection: Method

One of the first methods that gets called as the table view is being realized is the -tableView:numberOfRowsInSection: method, which tells the UITableView how many rows are going to be displayed.

Download Recipe?/Classes/MainViewController.m

```
```objc
- (NSInteger)tableView:(UITableView *)tableView
numberOfRowsInSection:(NSInteger)section
{
    id <NSFetchedResultsSectionInfo> sectionInfo = nil;
    sectionInfo = [[self resultsController] sections] objectAtIndex:section];
    return [sectionInfo numberOfObjects];
}
```
```

In this method, we request a reference to the NSFetchedResultsSectionInfo instance for the specified section. The result is an implementation of the protocol that contains a count of the number of objects in the section as well as a reference to the objects and the name of the section. For this method, we return the result of a call to the numberOfObjects property.

# Implementing the -tableView:cellForRowAtIndexPath: Method

The one method that tends to be the most complex in a UITableView-Controller is the -tableView:cellForRowAtIndexPath: method. This method is responsible for initializing (or dequeuing) the UITableViewCell object that will be displaying a particular row in the table.