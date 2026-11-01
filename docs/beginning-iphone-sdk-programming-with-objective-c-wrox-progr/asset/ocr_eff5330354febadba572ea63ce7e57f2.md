> NOTE You can simply drag and drop an image to the Resources folder of Xcode. When prompted, ensure that you save a copy of the image in your project.

To display an image next to the text of a cell, insert the following statements that appear in bold into the tableView:cellForRowAtIndexPath: method:

```
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
```

Press Command-R to test the application and you see that the image is displayed next to each row (see Figure 10-7).

Notice that the UITableViewCell object already has the imageView property. All you need to do is to create an instance of the UIImage class and then load the image from the Resources folder of your project.

# Displaying the Item Selected

So far, you have seen how to populate the Table view with items by ensuring that your View Controller conforms to the UITableViewDataSource protocol. This protocol takes care of populating the Table view, but if you want to select the items in a Table view, you need to conform to another protocol, UITableViewDelegate.

![](bbox=[0.7, 0.6, 0.92, 0.9])

FIGURE 10-7