![](bbox=[0.05, 0.15, 0.95, 0.51])

Do the same thing for the detail view controller, but set its cell identifier to Detail Cell.

Next, open HistoryViewController.m and navigate to the numberOfSectionsInTableView: method. We need to get rid of the #warning directive before our code will compile. Also, if we want to be able to open the detail view, we need to have at least one section and one row. To do this, modify the method as shown here:

```
- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView
{
    // TODO temporary code to get the interface to run
    // Return the number of sections.
    return 1;
}
```

We need to do something similar in tableView:numberOfRowsInSection:. This method should return the number of rows for a given section. Let's give ourselves a single row, so we can test out our connections.