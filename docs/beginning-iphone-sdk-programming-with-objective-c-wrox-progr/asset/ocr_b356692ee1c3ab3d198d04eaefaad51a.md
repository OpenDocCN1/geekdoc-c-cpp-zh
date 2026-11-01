Specifically, you use the dequeueReusableCellWithIdentifier: method of the UITableView class to obtain an instance of the UITableViewCell class. The dequeueReusableCellWithIdentifier: method returns a reusable Table view cell object. This is important because if you have a large table (say, with 10,000 rows) and you create a single UITableViewCell object for each row, you would generate a great performance and memory hit. Also, because a Table view displays only a fixed number of rows at any one time, reusing the cells that have been scrolled out of view would make sense. This is exactly what the dequeueReusableCellWithIdentifier: method does. So, for example, if 10 rows are visible in the Table view, only 10 UITableViewCell objects are ever created — they always get reused when the user scrolls through the Table view.

# Adding a Header and Footer

You can display a header and footer for the Table view by simply implementing the following two methods in your View Controller:

```
- (NSString *)tableView:(UITableView *)tableView titleForHeaderInSection:(NSUInteger)section {
    //---display "Movie List" as the header---
    return @"Movie List";
}

- (NSString *)tableView:(UITableView *)tableView titleForFooterInSection:(NSUInteger)section {
    //---display "by Denzel Washington" as the footer---
    return @"by Denzel Washington";
}
```

![](bbox=[0.75, 0.5, 0.9, 0.78])

If you insert the preceding statements in the TableViewExampleViewController.m file and rerun the application, you see the header and footer of the Table view as shown in Figure 10-5.

# Adding an Image

In addition to text, you can display an image next to the text of a cell in a Table view. Suppose you have an image named apple.jpeg in the Resources folder of your project (see Figure 10-6).

![](bbox=[0.7, 0.8, 0.95, 0.95])