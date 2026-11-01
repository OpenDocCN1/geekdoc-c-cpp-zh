
```objc
return [movieSection count];
}
- (UITableViewCell *)tableView:(UITableView *)tableView
    cellForRowAtIndexPath:(NSIndexPath *)indexPath {
    
    static NSString *CellIdentifier = @"CellIdentifier";
    
    // Dequeue or create a cell of the appropriate type.
    UITableViewCell *cell = [tableView
        dequeueReusableCellWithIdentifier:CellIdentifier];
    
    if (cell == nil) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault
            reuseIdentifier:CellIdentifier] autorelease];
        cell.accessoryType = UITableViewCellAccessoryNone;
    }
    
    // Configure the cell.
    if (isSearchOn) {
        NSString *cellValue = [searchResult objectAtIndex:indexPath.row];
        cell.textLabel.text = cellValue;
    } else {
        //---get the year---
        NSString *year = [years objectAtIndex:[indexPath section]];
        //---get the list of movies for that year---
        NSArray *movieSection = [movieTitles objectForKey:year];
        //---get the particular movie based on that row---
    }
    cell.textLabel.text = [movieSection objectAtIndex:[indexPath row]];
    }
    return cell;
}
- (NSString *)tableView:(UITableView *)tableView
titleForHeaderInSection:(NSUInteger)section {
    //---get the year as the section header---
    NSString *year = [years objectAtIndex:section];
    if (isSearchOn)
        return nil;
    else
        return year;
}
- (NSArray *)sectionIndexTitlesForTableView:(UITableView *)tableView {
    if (isSearchOn)
        return nil;
    else
        return years;
}
- (void)dealloc {
```

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_259_0.png)

**FIGURE 7-34**

## How It Works

That is quite a lot of work, isn’t it? But not to worry: It is actually quite easy to follow. First, you add an outlet to connect to the search bar:

```
IBOutlet UISearchBar *searchBar;
```

You define two Boolean variables so that you can track whether the search process is ongoing and whether the user can select the rows in the Table view:

```
BOOL isSearchOn;
BOOL canSelectRow;
```

You then define two NSMutableArray objects so that you can use one to store the list of movies and use another to temporarily store the result of the search:

```
NSMutableArray *listOfMovies;
NSMutableArray *searchResult;
```

When the view is first loaded, you first associate the Search Bar with the Table view and then copy the entire list of movie titles from the NSDictionary object into the NSMutableArray:

```objc
//---Search---
self.tableView.tableHeaderView = searchBar;
searchBar.autocorrectionType = UITextAutocorrectionTypeYes;

//---copy all the movie titles in the dictionary into the listOfMovies array---
listOfMovies = [[NSMutableArray alloc] init];
for (NSString *year in array)    //---get all the years---
{
    //---get all the movies for a particular year---
    NSArray *movies = [movieTitles objectForKey:year];
    for (NSString *title in movies)
    {
        [listOfMovies addObject:title];
    }
}

//---used for storing the search result---
searchResult = [[NSMutableArray alloc] init];

isSearchOn = NO;
canSelectRow = YES;
```

When the user taps the Search Bar, the searchBarTextDidBeginEditing: event (one of the methods defined in the UISearchBarDelegate protocol) fires. In this method, you add a Done button to the top-right corner of the screen. When the Done button is clicked, the doneSearching: method is called (which you define next).

```objc
//---fired when the user taps on the searchbar---
- (void)searchBarTextDidBeginEditing:(UISearchBar *)searchBar {
    isSearchOn = YES;
    canSelectRow = NO;
    self.tableView.scrollEnabled = NO;

    //---add the Done button at the top---
    self.navigationItem.rightBarButtonItem =
    [[[UIBarButtonItem alloc]
        initWithBarButtonSystemItem:UIBarButtonSystemItemDone
        target:self action:@selector(doneSearching:)]
        autorelease];
}
```

The doneSearching: method makes the Search Bar resign its First Responder status (thereby hiding the keyboard). At the same time, you reload the Table view by calling the reloadData method of the Table view. This causes the various events associated with the Table view to be fired again.

```objc
//---done with the searching---
- (void) doneSearching:(id)sender {
    isSearchOn = NO;
    canSelectRow = YES;
    self.tableView.scrollEnabled = YES;
    self.navigationItem.rightBarButtonItem = nil;

    //---hides the keyboard---
    [searchBar resignFirstResponder];

    //---refresh the TableView---
    [self.tableView reloadData];
}
```

As the user types into the Search Bar, the searchBar:textDidChange: event is fired for each character entered. In this case, if the Search Bar has at least one character, you call the searchMoviesTableView method (which you define next):

```
//---fired when the user types something into the searchbar---
- (void)searchBar:(UISearchBar *)searchBar textDidChange:(NSString *)searchText {

    //---if there is something to search for---
    if ([searchText length] > 0) {
        isSearchOn = YES;
        canSelectRow = YES;
        self.tableView.scrollEnabled = YES;
        [self searchMoviesTableView];
    }
    else {
        //---nothing to search---
        isSearchOn = NO;
        canSelectRow = NO;
        self.tableView.scrollEnabled = NO;
    }
    [self.tableView reloadData];
}
```

The searchMoviesTableView method performs the searching on the listOfMovies array. You use the rangeOfString:options: method of the NSString class to perform a case-insensitive search of each movie title using the specified string. The returning result is an NSRange object, which contains the location and length of the search string in the string being searched. If the length is more than zero, this means that a match has been found, and hence you add it to the searchResult array:

```
//---performs the searching using the array of movies---
- (void) searchMoviesTableView {
    //---clears the search result---
    [searchResult removeAllObjects];

    for (NSString *str in listOfMovies)
    {
        NSRange titleResultsRange = [str rangeOfString:searchBar.text options:NSCaseInsensitiveSearch];

        if (titleResultsRange.length > 0)
            [searchResult addObject:str];
    }
}
```

To display one of these images, insert the following statement that appears in bold in the tableView :cellForRowAtIndexPath: event:

```
- (UITableViewCell *)tableView:(UITableView *)tableView
cellForRowAtIndexPath:(NSIndexPath *)indexPath {
    static NSString *CellIdentifier = @"CellIdentifier";
    
    // Dequeue or create a cell of the appropriate type.
    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:CellIdentifier];
    if (cell == nil) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:CellIdentifier] autorelease];
        cell.accessoryType = UITableViewCellAccessoryDetailDisclosureButton;
    }
    
    // Configure the cell.
    if (isSearchOn) {
        NSString *cellValue = [searchResult objectAtIndex:indexPath.row];
        cell.textLabel.text = cellValue;
    } else {
        //---get the year---
        NSString *year = [years objectAtIndex:[indexPath section]];
        //---get the list of movies for that year---
        NSArray *movieSection = [movieTitles objectForKey:year];
        //---get the particular movie based on that row---
        cell.textLabel.text = [movieSection objectAtIndex:[indexPath row]];
    }
    
    return cell;
}
```

You can use the following constants for the accessoryType property:

- UITableViewCellAccessoryDetailDisclosureButton
- UITableViewCellAccessoryCheckmark
- UITableViewCellAccessoryDisclosureIndicator

Figure 7-36 shows the different types of images corresponding to the three preceding constants.

Of the three image types, only the UITableViewCellAccessoryDetailDisclosureButton can handle a user's tap event. (The other two images are used for display only.) To handle the event when the user taps the Disclosure button, you need to implement the tableView:accessoryButtonTappedForRowWithIndexPath: method:

```
- (void)tableView:(UITableView *)tableView
accessoryButtonTappedForRowWithIndexPath:(NSIndexPath *)indexPath {
    //---insert code here---
    // e.g. navigate to another view to display detailed information, etc
}
```
