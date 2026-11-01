to implement the sectionIndexTitlesForTableView: method and return the array containing the section headers, which is the years array in this case:

```
- (NSArray *)sectionIndexTitlesForTableView: (UITableView *)tableView {
    return years;
}
```

> NOTE If the Table view's Style property is set to Grouped, the index will overlap with the layout of the Table view.

Figure 7-29 shows the index displayed on the right side of the Table view.

![](bbox=[0.1, 0.42, 0.42, 0.9])

FIGURE 7-29