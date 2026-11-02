# How It Works

The preceding example is a bit more interesting than the examples earlier in the chapter. Basically, you added a new XIB file and a corresponding View Controller class to the project. This new View window will be used to display the movie that you have touched in the View containing the Table view.

Now, in order for the View window containing the Table view to be able to pass the name of the movie selected to the details View window, you would need to create a property on the details View window. This is done through the textSelected property:

```
```objc
@property (nonatomic, retain) NSString *textSelected;
```
```

At the same time, you create method called initWithTextSelected: so that the calling view can set the value of the textSelected property:

```
```objc
- (id) initWithTextSelected: (NSString *) text {
    self.textSelected = text;
    [label setText:[self textSelected]];
    return self;
}
```
```

To navigate from the View containing the Table view to the details view, you use the pushViewController: method of the UINavigationController object within the tableView:didSelectRowAtIndexPath: method:

```
```objc
//--create an instance of the DetailsViewController---
if (self.detailsViewController == nil)
{
    DetailsViewController *d = [[DetailsViewController alloc]
                                initWithNibName:@"DetailsView"
                                bundle:[NSBundle mainBundle]];
    self.detailsViewController = d;
    [d release];
}

//--set the movies selected in the method of the
// DetailsViewController---
[self.detailsViewController initWithTextSelected:message];

//---navigate to the details view---
[self.navigationController pushViewController:self.detailsViewController
                                     animated:YES];
```
```

# Missing Back Button

Recall that earlier on, you set the title of the navigation item in the RootViewController.m file like this:

```
```objc
- (void)viewDidLoad {

    //--initialize the array---
    listOfMovies = [[NSMutableArray alloc] init];

    //--add items---
```
```