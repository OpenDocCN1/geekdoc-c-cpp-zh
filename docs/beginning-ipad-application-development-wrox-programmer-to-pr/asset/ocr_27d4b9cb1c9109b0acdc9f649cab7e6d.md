```
// Configure the cell.
//cell.textLabel.text = [NSString stringWithFormat:@"Row %d", indexPath.row];
cell.textLabel.text = [listOfMovies objectAtIndex:indexPath.row];

return cell;
}
- (void)tableView:(UITableView *)aTableView
didSelectRowAtIndexPath:(NSIndexPath *)indexPath {
/*
When a row is selected, set the detail view controller's detail item to
the item associated with the selected row.
*/
// [detailViewController.detailItem =
// [NSString stringWithFormat:@"Row %d", indexPath.row];

detailViewController.detailItem =
    [NSString stringWithFormat:@"%@",
        [listOfMovies objectAtIndex:indexPath.row]];
}
- (void)dealloc {
    [listOfMovies release];
    [super dealloc];
}
```

# 8. Add the following bold statements to the DetailViewController.m file:

```
#import "DetailViewController.h"
#import "RootViewController.h"

@implementation DetailViewController

@synthesize navigationBar, popoverController, detailItem;

@synthesize imageView;

/*
When setting the detail item, update the view and dismiss the
popover controller if it's showing.
*/
- (void)setDetailItem:(id)newDetailItem {
    if (detailItem != newDetailItem) {
        [detailItem release];
        detailItem = [newDetailItem retain];

        // Update the view.
        navigationBar.topItem.title = [detailItem description];

        NSString *imageName = [NSString
            stringWithFormat:@"%@.jpg",navigationBar.topItem.title];
    }
}
```