```
NSarray *array = [[movieTitles allKeys]
    sortedArrayUsingSelector:@selector(compare:)];

//---save the keys in the years property---
self.years = array;

//---Search---
self.tableView.tableHeaderView = searchBar;
searchBar.autocorrectionType = UITextAutocorrectionTypeYes;

//---copy all the movie titles in the
// listOfMovies array---
listOfMovies = [[NSMutableArray alloc] init];
for (NSString *year in array)   //---get all the years---
{
    //---get all the movies for a particular year---
    NSArray *movies = [movieTitles objectForKey:year];
    for (NSString *title in movies) {
        [listOfMovies addObject:title];
    }
}
//---used for storing the search result---
searchResult = [[NSMutableArray alloc] init];

isSearchOn = NO;
canSelectRow = YES;

[super viewDidLoad];
self.clearsSelectionOnViewWillAppear = NO;
}

- (NSInteger)numberOfSectionsInTableView:(UITableView *)aTableView {
    // Return the number of sections.
    //return 1;
    if (isSearchOn)
        return 1;
    else
        return [years count];
}

- (NSInteger)tableView:(UITableView *)aTableView
numberOfRowsInSection:(NSInteger)section {

    // Return the number of rows in the section.
    //return 10;
    if (isSearchOn) {
        return [searchResult count];
    } else {
        //---check the current year based on the section index---
        NSString *year = [years objectAtIndex:section];
        //---returns the movies in that year as an array---
        NSArray *movieSection = [movieTitles objectForKey:year];
        //---return the number of movies for that year as the number
        // of rows in that section ---
```