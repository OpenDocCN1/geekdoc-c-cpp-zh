
- (void)addCountryViewControllerDidFinish:
(AddCountryViewController *)controller;

When the user presses the Done button in this view, you invoke the done: method:

```
//---invokes the method defined in the protocol---
- (IBAction)done {
    [self.delegate addCountryViewControllerDidFinish:self];
}
```

In the FlipsideViewController.m file, you need to implement the protocol defined in the additional view, which is AddCountryViewControllerDelegate:

```
//---implements the AddCountryViewControllerDelegate protocol---
@interface FlipsideViewController : UIViewController <AddCountryViewControllerDelegate> {
```

Specifically, you need to implement the addCountryViewControllerDidFinish: method, which dismisses the view controller:

```
//---defines the addCountryViewControllerDidFinish: method---
- (void)addCountryViewControllerDidFinish:
(AddCountryViewController *)controller {
    [self dismissModalViewControllerAnimated:YES];
}
```

Finally, you define the add: method, which shows the additional view using the vertical transition:

```
//---defines the add: action---
- (IBAction)add {
    AddCountryViewController *controller = [[AddCountryViewController alloc]
        initWithNibName:@"AddCountryView"
        bundle:nil];
    controller.delegate = self;
    //---use the vertical transition---
    controller.modalTransitionStyle = UIModalTransitionStyleCoverVertical;
    [self presentModalViewController:controller animated:YES];
    [controller release];
}
```

## SUMMARY

In this chapter, you saw the Utility Application template provided by the iPhone SDK to help developers create Utility Applications. Understanding how the transitioning between the Views works is important because it allows you to extend the template for your custom use. In Chapter 10, you will see how Utility Applications are often used together with application settings to persist users’ preferences and data.

## WHAT YOU HAVE LEARNED IN THIS CHAPTER

| TOPIC | KEY CONCEPTS |
|---|---|
| Create a Utility Application | Use the Utility Application template provided by the iPhone SDK. |
| Transition between views in a Utility Application | Use the `modalTransitionStyle` property and set it to one of the following values: `UIModalTransitionStyleFlipHorizontal`, `UIModalTransitionStyleCoverVertical`, and `UIModalTransitionStyleCrossDissolve`. |
| Add a new view to a Utility Application | First, create a new XIB file and its accompanying `UIViewController` subclass (`.h` and `.m` files). Next, define a protocol in the view controller and expose an instance of the protocol delegate as a property. |

## PART III

## Displaying and Persisting Data

- **CHAPTER 10:** Using the Table View
- **CHAPTER 11:** Application Preferences
- **CHAPTER 12:** Database Storage Using SQLite3
- **CHAPTER 13:** File Handling

![](img/16991b58db5894715c4a443315e06a22_258_0.png)

## Using the Table View

## WHAT YOU WILL LEARN IN THIS CHAPTER

- How to manually add a Table view to a View, and wire the data source and delegate to your View Controller
- How to handle the various events in the table view to populate it with items
- How to handle the various events in the Table view so that users can select the items contained within it
- How to display text and images in the rows of the table view
- How to display the items from a property list in a table view
- How to group the items in a table view into sections
- How to add indexing to the table view
- How to add search capabilities to the table view
- How to add disclosures and checkmarks to rows in the table view

One of the most commonly used views in iPhone applications is the Table view. The Table view is used to display lists of items from which users can select, or they can tap it to display more information. Figure 10-1 shows a Table view in action in the Settings Application.

In Chapter 8, you had your first taste of the Table view when you developed a Navigation-based Application project. That chapter didn't fully dive into how the Table view works, and a lot of details were purposely left out. The Table view is such an important topic that it deserves a chapter on its own.

Hence, in this chapter, you examine the Table view in more details and understand the various building blocks that make it such a versatile view.

## A SIMPLE TABLE VIEW

The best way to understand how to use a table view in your application is to create a new View-based Application project and then manually add a Table view to the view and wire it to a View Controller. That way, you understand the various building blocks of the Table view.

Without further ado, use the following Try It Out to create a new project and see how to put a Table view together!

![](img/16991b58db5894715c4a443315e06a22_259_0.png)

## TRY IT OUT  Using a Table View

Codefile [TableViewExample.zip] available for download at Wrox.com

+   1. Create a new View-based Application project and name it TableViewExample.
+   2. Double-click the TableViewExampleViewController.xib file to edit it in Interface Builder.
+   3. Drag the Table View Object from the Library and drop it onto the View window (see Figure 10-2).

![](img/16991b58db5894715c4a443315e06a22_259_1.png)

+   4. Right-click the Table view and connect the dataSource outlet to the File’s Owner item (see Figure 10-3). Do the same for the delegate outlet.

![](img/16991b58db5894715c4a443315e06a22_260_0.png)

FIGURE 10-3

+   5. In the `TableViewExampleViewController.h` file, add the following statement that appears in bold:

```
```objc
#import <UIKit/UIKit.h>

@interface TableViewExampleViewController : UIViewController
    <UITableViewDataSource> {
}

@end
```
```

> > **NOTE** Strictly speaking, if you have connected the dataSource outlet to the File’s Owner item, you don’t need to add the preceding statement. Either you write the preceding statement (`UITableViewDataSource`) or connect the outlet in Interface Builder. However, doing both doesn’t hurt anything. There is one advantage to adding the `<UITableViewDataSource>` protocol, though — the compiler will warn you if you forget to implement any mandatory methods in your code, helping to prevent errors.

6. In the `TableViewExampleViewController.m` file, add the following statements that appear in bold:

```
#import "TableViewExampleViewController.h"

@implementation TableViewExampleViewController

NSMutableArray *listOfMovies;

//---insert individual row into the table view---
- (UITableViewCell *)tableView:(UITableView *)tableView
    cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    static NSString *CellIdentifier = @"Cell";

    //---try to get a reusable cell---
    UITableViewCell *cell = [tableView
        dequeueReusableCellWithIdentifier:CellIdentifier];

    //---create new cell if no reusable cell is available---
    if (cell == nil) {
        cell = [[[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault
                    reuseIdentifier:CellIdentifier] autorelease];
    }

    //---set the text to display for the cell---
    NSString *cellValue = [listOfMovies objectAtIndex:indexPath.row];
    cell.textLabel.text = cellValue;

    return cell;
}

//---set the number of rows in the table view---
- (NSInteger)tableView:(UITableView *)tableView
    numberOfRowsInSection:(NSInteger)section {

    return [listOfMovies count];
}

- (void)viewDidLoad {
    //---initialize the array---
    listOfMovies = [[NSMutableArray alloc] init];

    //---add items---
    [listOfMovies addObject:@"Training Day"];
    [listOfMovies addObject:@"Remember the Titans"];
    [listOfMovies addObject:@"John Q."];
    [listOfMovies addObject:@"The Bone Collector"];
    [listOfMovies addObject:@"Ricochet"];
    [listOfMovies addObject:@"The Siege"];
    [listOfMovies addObject:@"Malcolm X"];
    [listOfMovies addObject:@"Antwone Fisher"];
    [listOfMovies addObject:@"Courage Under Fire"];
}
```
