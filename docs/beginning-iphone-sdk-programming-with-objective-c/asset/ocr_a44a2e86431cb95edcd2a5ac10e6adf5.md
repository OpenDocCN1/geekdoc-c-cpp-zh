```
NSArray *movieSection = [movieTitles objectForKey:year];

//--- get the particular movie based on that row---
cell.text = [movieSection objectAtIndex:[indexPath row]];

return cell;
}
```

Finally, you implement the tableView:titleForHeaderInSection: method to retrieve the year as the header for each section:

```
- (NSString *)tableView:(UITableView *)tableView
titleForHeaderInSection:(NSInteger)section {
    //--- get the year as the section header---
    NSString *year = [years objectAtIndex:section];
    return year;
}
```

# Adding Indexing

The list of movies is pretty short, so scrolling through the list is not too much of a hassle. However, imagine that the list contains 10,000 titles spanning 100 years. In this case, scrolling from the top of the list to the bottom of the list can take a long time. A very useful feature of the Table view is its ability to display an index on the right side of the view. An example is the A–Z index list available in your Contacts list (see Figure 10-19).

To add an index list to your Table view, you just need to implement the sectionIndexTitlesForTableView: method and return the array containing the section headers, which is the years array in this case:

```
- (NSArray *)sectionIndexTitlesForTableView:(UITableView *)tableView {
    return years;
}
```

![](bbox=[0.75, 0.55, 0.95, 0.85])

FIGURE 10-19

> **NOTE** Before you run the application, be sure to change the style of the Table view back to Plain. If you set it to Grouped style, the index will overlap with the layout of the Table view.

Figure 10-20 shows the index displayed on the right side of the Table view.