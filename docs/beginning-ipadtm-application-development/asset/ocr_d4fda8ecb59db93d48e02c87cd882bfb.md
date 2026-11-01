When an item is selected in the Table view, you pass the movie selected to the DetailViewController object via its detailItem property:

```
- (void)tableView:(UITableView *)aTableView
didSelectRowAtIndexPath:(NSIndexPath *)indexPath {

    /*
     When a row is selected, set the detail view controller's
     detail item to the item associated with the selected row.
     */
    //detailViewController.detailItem =
    //    [NSString stringWithFormat:@"Row %d", indexPath.row];

    detailViewController.detailItem =
        [NSString stringWithFormat:@"%@",
         [listOfMovies objectAtIndex:indexPath.row]];
}
```

In the DetailViewController.m file, you modified the setDetailItem: method (which is really a setter for the detailItem property) so that an image can be displayed. For the image name, you simply append a .jpg to the movie name:

```
- (void)setDetailItem:(id)newDetailItem {
    if (detailItem != newDetailItem) {
        [detailItem release];
        detailItem = [newDetailItem retain];
    }
    // Update the view.
    navigationBar.topItem.title = [detailItem description];

    NSString *imageName = [NSString
        stringWithFormat:@"%@.jpg",navigationBar.topItem.title];
    imageView.image = [UIImage imageNamed:imageName];
    }

    if (popoverController != nil) {
        [popoverController dismissPopoverAnimated:YES];
    }
}
```

# THE TAB BAR APPLICATION TEMPLATE

You have seen the use of three types of application templates provided by the iPhone SDK: View-based Application, Window-based Application, and Split View-based Application. A fourth type of application template exists for the iPad: The Tab Bar application template. The following Try it Out uses the Tab Bar Application template to create a project and shows what a Tab Bar application looks like. Download the necessary project files as indicated here.