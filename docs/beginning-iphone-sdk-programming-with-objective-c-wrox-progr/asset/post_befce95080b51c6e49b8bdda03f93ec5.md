
The UITableViewDataSource protocol contains several events that you can implement to supply data to the Table view. Two events that you have handled in this example are:

- `tableView:numberOfRowsInSection:`
- `tableView:cellForRowAtIndexPath:`

The tableView:numberOfRowsInSection: event indicates how many rows you want the Table view to display. In this case, you set it to the number of items in the listOfMovies array.

//---insert individual row into the table view---
- (NSInteger)tableView: (UITableView *)tableView
    numberOfRowsInSection: (NSInteger)section {

    return [listOfMovies count];

}
The tableView:cellForRowAtIndexPath: event inserts a cell in a particular location of the Table display. In this case, you set it for each row of the Table view.

> **NOTE** The tableView:cellForRowAtIndexPath: event is not fired continuously from start to finish. For example, if the Table view has 100 rows to be displayed, the event is fired continuously for the first, say, 10 rows that are visible. When the user scrolls down the Table view, the tableView:cellForRowAtIndexPath: event is fired for the next couple of visible rows.

Here, you retrieve the individual item from the array and insert it into the Table view:

- (UITableViewCell *)tableView: (UITableView *)tableView
    cellForRowAtIndexPath: (NSIndexPath *)indexPath {

    static NSString *cellIdentifier = @"Cell";

    //---try to get a reusable cell---
    UITableViewCell *cell = [tableView
        dequeueReusableCellWithIdentifier:cellIdentifier];

    //---create new cell if no reusable cell is available---
    if (cell == nil) {
        cell = [[[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault
                    reuseIdentifier:cellIdentifier] autorelease];
    }

    //---set the text to display for the cell---
    NSString *cellValue = [listOfMovies objectAtIndex:indexPath.row];
    cell.textLabel.text = cellValue;

    return cell;
}
Specifically, you use the dequeueReusableCellWithIdentifier: method of the UITableView class to obtain an instance of the UITableViewCell class. The dequeueReusableCellWithIdentifier: method returns a reusable Table view cell object. This is important because if you have a large table (say, with 10,000 rows) and you create a single UITableViewCell object for each row, you would generate a great performance and memory hit. Also, because a Table view displays only a fixed number of rows at any one time, reusing the cells that have been scrolled out of view would make sense. This is exactly what the dequeueReusableCellWithIdentifier: method does. So, for example, if 10 rows are visible in the Table view, only 10 UITableViewCell objects are ever created — they always get reused when the user scrolls through the Table view.

## Adding a Header and Footer

You can display a header and footer for the Table view by simply implementing the following two methods in your View Controller:

- (NSString *)tableView:(UITableView *)tableView titleForHeaderInSection:(NSUInteger)section {
    //---display "Movie List" as the header---
    return @"Movie List";
}

- (NSString *)tableView:(UITableView *)tableView titleForFooterInSection:(NSUInteger)section {
    //---display "by Denzel Washington" as the footer---
    return @"by Denzel Washington";
}
![](img/16991b58db5894715c4a443315e06a22_264_0.png)

If you insert the preceding statements in the TableViewExampleViewController.m file and rerun the application, you see the header and footer of the Table view as shown in Figure 10-5.

## Adding an Image

In addition to text, you can display an image next to the text of a cell in a Table view. Suppose you have an image named apple.jpeg in the Resources folder of your project (see Figure 10-6).

![](img/16991b58db5894715c4a443315e06a22_264_1.png)

> NOTE You can simply drag and drop an image to the Resources folder of Xcode. When prompted, ensure that you save a copy of the image in your project.

To display an image next to the text of a cell, insert the following statements that appear in bold into the tableView:cellForRowAtIndexPath: method:

```objc
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
    cell.text = cellValue;
    
    UIImage *image = [UIImage imageNamed:@"apple.jpeg"];
    cell.imageView.image = image;
    
    return cell;
}
```

Press Command-R to test the application and you see that the image is displayed next to each row (see Figure 10-7).

Notice that the UITableViewCell object already has the imageView property. All you need to do is to create an instance of the UIImage class and then load the image from the Resources folder of your project.

## Displaying the Item Selected

So far, you have seen how to populate the Table view with items by ensuring that your View Controller conforms to the UITableViewDataSource protocol. This protocol takes care of populating the Table view, but if you want to select the items in a Table view, you need to conform to another protocol, UITableViewDelegate.

![](img/16991b58db5894715c4a443315e06a22_265_0.png)

FIGURE 10-7

The UITableViewDelegate protocol contains events that allow you to manage selections, edit and delete rows, and display a header and footer.

To use the UITableViewDelegate protocol, modify the TableViewExampleViewController.h file by adding the statement in bold as follows:

#import <UIKit/UIKit.h>

@interface TableViewExampleViewController : UIViewController
<UITableViewDataSource,
UITableViewDelegate>{
}

@end
Strictly speaking, if you have connected the delegate outlet to the File's Owner item previously (see Figure 10-8), you don't need to add the preceding statement (UITableViewDelegate). Either you write the preceding statement or connect the outlet in Interface Builder. However, doing both doesn't hurt.

![](img/16991b58db5894715c4a443315e06a22_266_0.png)

FIGURE 10-8

The following Try It Out shows how you can allow users to make selections in a Table view.

> NOTE The row property of the NSIndexPath class is one of the additions made by the UIKit framework to enable the identification of rows and sections in a Table view. So be aware that the original class definition of the NSIndexPath class does not contain the row property.

After the selected movie is retrieved, you simply display it using the UIAlertView class:

NSString *msg = [[NSString alloc] initWithFormat:@"You have selected %@", movieSelected];

UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Movie selected" message:msg delegate:self cancelButtonTitle:@"OK" otherButtonTitles:nil];
## Indenting

Another event in the UITableViewDelegate protocol is tableView:indentationLevelForRowAtIndexPath:. When you handle this event, it is fired for every row that is visible on the screen. To set an indentation for a particular row, simply return an integer indicating the level of indentation:

- (NSInteger)tableView:(UITableView *)tableView indentationLevelForRowAtIndexPath:(NSIndexPath *)indexPath {
    return [indexPath row] % 2;
}
In the preceding example, the indentation alternates between 0 and 1, depending on the current row number. Figure 10-10 shows how the Table view looks if you insert the preceding code in the TableViewExampleViewController.m file.

![](img/16991b58db5894715c4a443315e06a22_268_0.png)

## DISPLAYING SECTIONS

In the previous sections, you create a View-based Application project and then manually add a Table view to the View window and connect the data source and delegate to the File's Owner item. You then handle all the relevant events defined in the two protocols, UITableViewDelegate and UITableViewDataSource, so that you can populate the Table view with items as well as make them selectable.
