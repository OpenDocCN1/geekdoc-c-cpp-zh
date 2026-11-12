```
```objc
- (NSInteger)tableView:(UITableView *)tableView
numberOfRowsInSection:(NSInteger)section
{
    id <NSFetchedResultsSectionInfo> sectionInfo =
        [[self.fetchedResultsController sections]
            objectAtIndex:section];
    return [sectionInfo numberOfObjects];
}
```
```

Here, we get the section information for the given section index. This gives us direct access to the array of objects, as well as to the section’s name and index title. In this case, we are only interested in the number of objects.

Then we change the way we access our WeightEntry objects in tableView:cellForRowAtIndexPath:. Here, we access them directly from our fetched request controller.

```
```objc
- (UITableViewCell *)tableView:(UITableView *)tableView
        cellForRowAtIndexPath:(NSIndexPath *)indexPath
{
    static NSString *CellIdentifier = @"History Cell";
    HistoryCell *cell =
    [tableView dequeueReusableCellWithIdentifier:CellIdentifier];
    WeightEntry* entry =
    [self.fetchedResultsController objectAtIndexPath:indexPath];
    [cell configureWithWeightEntry:entry
                defaultUnits:getDefaultUnits()];
    return cell;
}
```
```