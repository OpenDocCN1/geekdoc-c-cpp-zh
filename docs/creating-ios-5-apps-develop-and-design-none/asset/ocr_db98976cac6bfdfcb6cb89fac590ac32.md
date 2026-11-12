Here, we're just bracketing our changes with calls to beginUpdates and endUpdates. If we make multiple changes to our table, all the changes will be animated at once. For example, if a row is moved, we first delete it from its old location in the table and then insert it into its new location. This ensures that the deletion and insertion are animated simultaneously.

Next, we need to implement controller:didChangeObject:atIndexPath:forChangeType:newIndexPath:. This method is called whenever the underlying data changes.

```
```objc
- (void)controller:(NSFetchedResultsController *)controller
   didChangeObject:(id)anObject
       atIndexPath:(NSIndexPath *)indexPath
     forChangeType:(NSFetchedResultsChangeType)type
        newIndexPath:(NSIndexPath *)newIndexPath
{
    UITableView *tableView = self.tableView;
    WeightEntry* entry;
    HistoryCell* cell;
    switch(type)
    {
        case NSFetchedResultsChangeInsert:
            [tableView
             insertRowsAtIndexPaths:
             [NSArray arrayWithObject:newIndexPath]
             withRowAnimation:UITableViewRowAnimationAutomatic];
            break;
        case NSFetchedResultsChangeDelete:
            [tableView
             deleteRowsAtIndexPaths:
             [NSArray arrayWithObject:indexPath]
```
```