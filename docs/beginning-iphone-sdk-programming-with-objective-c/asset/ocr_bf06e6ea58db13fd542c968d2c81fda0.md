# TRY IT OUT Making a Selection in a Table View

1. Using the same project created earlier, add the following statements that appear in bold to the TableViewExampleViewController.m file:

```
#import "TableViewExampleViewController.h"
@implementation TableViewExampleViewController
NSMutableArray *listOfMovies;
- (void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath {
    NSString *movieSelected = [listOfMovies objectAtIndex:[indexPath row]];
    NSString *msg = [[NSString alloc] initWithFormat:@"You have selected %@", movieSelected];
    UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Movie selected" message:msg delegate:self cancelButtonTitle:@"OK" otherButtonTitles:nil];
    [alert show];
    [alert release];
    [movieSelected release];
    [msg release];
}
```

2. Press Command-R to test the application on the iPhone Simulator.

3. Select a row by tapping it. When a row is selected, you see an alert view displaying the row you have selected (see Figure 10-9).

# How It Works

One of the events in the UITableViewDelegate protocol is tableView:didSelectRowAtIndexPath:, which is fired when the user selects a row in the Table view. One of the parameters contained in tableView:didSelectRowAtIndexPath: event is of the type NSIndexPath. The NSIndexPath class represents the path of a specific item in a nested array collection.

For this event, to know which row has been selected, you simply call the row property of the NSIndexPath object (indexPath) and then use the row number to reference against the listOfMovies array:

```
NSString *movieSelected = [listOfMovies objectAtIndex:[indexPath row]];
```

![](bbox=[0.7, 0.55, 0.9, 0.9])