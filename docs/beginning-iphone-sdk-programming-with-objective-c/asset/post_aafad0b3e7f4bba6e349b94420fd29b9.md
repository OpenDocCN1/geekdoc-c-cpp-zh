
Press Command-R to test the application and change the screen rotation. What do you notice? Well, the orientation of the application does not change — it is still displayed in portrait mode. In order to support different orientations, all the View Controllers contained within the UITabBarController object must support the same orientations. That is to say, if one View Controller supports landscape left mode, then all the View Controllers must also support landscape left mode. Hence, in the following Try It Out, you modify the application to support all orientations.

## TRY IT OUT Supporting Screen Rotations

- 1. Using the same project created earlier, observe in the Identity Inspector window that the Second Tab Bar item is set to the base class UIViewController.
- 2. Right-click the Classes group in Xcode and choose Add ⇧ New Files. Select the UIViewController subclass file template and name it SecondViewController.m (uncheck the “With XIB for user interface” option because you already have an XIB file — SecondView.xib).
- 3. Change the Class name for the Second Tab Bar item to SecondViewController.
- 4. Double-click on the SecondView.xib file in Xcode to edit it in Interface Builder. Select the File’s Owner item and in the Identity Inspector window, change its Class to SecondViewController.
- 5. In the FirstViewController.m, SecondViewController.m, and SearchViewController.m files, ensure that you return YES for the shouldAutorotateToInterfaceOrientation: method:
- 6. That’s it! Press Command-R and you should now be able to rotate the application to any orientation (see Figure 8-16).

```objective-c
- (BOOL)shouldAutorotateToInterfaceOrientation:(UIInterfaceOrientation) interfaceOrientation {
    return YES;
}
```

![](img/aab2d775c46f70cd606f2e58e2521324_226_0.png)

FIGURE 8-16

## How It Works

You may recall that the original project files created by the Tab Bar Application template contain only one view controller — `FirstViewController` — which corresponds to the first view in the Tab Bar View Controller. The second view is represented by the `SecondView.xib`, but it does not have a corresponding View Controller class. To ensure that this view supports all orientations, you need to add a new View Controller class to the project so that it can override the implementation provided by the base `UIViewController` class. You then override the `shouldAutorotateToInterfaceOrientation:` method so that each View Controller returns `YES` to support all orientations.

## MAXIMUM NUMBER OF TAB BAR ITEMS

The Tab Bar supports at most five Tab Bar Items. After you have more than five items, you will see a More item, and touching the More item displays the rest of the items in a Table View (see Figure 8-17).

![](img/aab2d775c46f70cd606f2e58e2521324_227_0.png)

## NAVIGATION-BASED APPLICATIONS

Tab Bar applications are suitable for situations in which you have several views, each view displaying different information so the user can quickly switch among them. However, sometimes you have hierarchical data that requires users to move from one screen to another based on what they have selected. In this situation, it is better to use a Navigation-based application.

To see how a Navigation-based application works, you can create one now, in the following Try It Out.

## TRY IT OUT Creating a Navigation-Based Application

Codefile [NavApplication.zip] available for download at Wrox.com

- 1. Using Xcode, create a Navigation-based Application project and name it NavApplication.
- 2. Observe the files created by the template (see Figure 8-18). As usual, there are the application delegate files, as well as a View Controller named RootViewController. There are two XIB files: RootViewController.xib and MainWindow.xib.

![](img/aab2d775c46f70cd606f2e58e2521324_228_0.png)

FIGURE 8-18

- 3. Examine the content of the NavApplicationAppDelegate.h file:

```objc
@interface NavApplicationAppDelegate : NSObject <UIApplicationDelegate> {
    UIWindow *window;
    UINavigationController *navigationController;
}
@property (nonatomic, retain) IBOutlet UIWindow *window;
@property (nonatomic, retain) IBOutlet UINavigationController
*navigationController;
@end
```

- 4. Instead of using a generic View Controller, it is now using a UINavigationController class. The UINavigationController class is a specialized View Controller that manages the navigation of hierarchical content.

- 5. Examine the content of the NavApplicationAppDelegate.m file, in particular the applicationDidFinishLaunching: method:

```objc
#import "NavApplicationAppDelegate.h"
#import "RootViewController.h"
@implementation NavApplicationAppDelegate
@synthesize window;
@synthesize navigationController;
#pragma mark -
#pragma mark Application lifecycle
- (void)applicationDidFinishLaunching:(UIApplication *)application {
    // Override point for customization after app launch
    [window addSubview:[navigationController view]];
    [window makeKeyAndVisible];
}
```

- 6. Here, you are adding the view of the navigation controller to the current view to make it visible when the application is loaded.

- 7. Double-click the MainWindow.xib file to edit it in Interface Builder. Figure 8-19 shows that the MainWindow.xib window (shown in List View) contains a Navigation Controller item. The Navigation Controller item itself contains a Navigation Bar item as well as a View that is loaded from the RootViewController class.

![](img/aab2d775c46f70cd606f2e58e2521324_230_0.png)

FIGURE 8-19

- 8. Double-click the RootViewController.xib file to open it in Interface Builder. Observe that by default, the Navigation-Application template uses a Table view for the root View Controller (See Figure 8-20).

> NOTE Navigation-based applications do not necessarily have to use the Table view. However, because the Table view is such a popular view and is often used in a Navigation-based application, Apple has included it by default into the Navigation-based Application template. The Table view is discussed in more detail in Chapter 10.

![](img/aab2d775c46f70cd606f2e58e2521324_231_0.png)

FIGURE 8-20

- 9. Press Command-R to test the application. By itself, the application doesn't show much; all you see are rows of lines (see Figure 8-21). You learn how to populate the Table view next.

- 10. In the RootViewController.m file, add the following statements highlighted in bold to declare and initialize an array containing a list of movies:

```objective-c
#import "RootViewController.h"

@implementation RootViewController

NSMutableArray *listOfMovies;

- (void)viewDidLoad {

    //---initialize the array---
    listOfMovies = [[NSMutableArray alloc] init];

    //---add items---
    [listOfMovies addObject:@"Training Day"];
    [listOfMovies addObject:@"Remember the Titans"];
```

![](img/aab2d775c46f70cd606f2e58e2521324_231_1.png)

FIGURE 8-21

```objective-c
[listOfMovies addObject:@"John Q."];
[listOfMovies addObject:@"The Bone Collector"];
[listOfMovies addObject:@"Ricochet"];
[listOfMovies addObject:@"The Siege"];
[listOfMovies addObject:@"Malcolm X"];
[listOfMovies addObject:@"Andrew Fisher"];
[listOfMovies addObject:@"Courage Under Fire"];
[listOfMovies addObject:@"He Got Game"];
[listOfMovies addObject:@"The Pelican Brief"];
[listOfMovies addObject:@"Glory"];
[listOfMovies addObject:@"The Preacher's Wife"];

//---get the title of the navigation bar---
self.navigationItem.title = @"Movies";

[super viewDidLoad];

- (void)dealloc {
    [listOfMovies release];
    [super dealloc];
}
```

- 11. Insert the following statement in bold in the `tableView:numberOfRowsInSection:` method to specify the number of rows to display for the Table view:

```objective-c
//---specify the number of rows in the table view---
- (NSInteger)tableView:(UITableView *)tableView
        numberOfRowsInSection:(NSInteger)section {

    //---set it to the number of items in the array---
    return [listOfMovies count];
}
```

- 12. Insert the following statements in bold in the `tableView:cellForRowAtIndexPath:` method to specify the appearance of each cell:

```objective-c
//--- Customize the appearance of table view cells---
- (UITableViewCell *)tableView:(UITableView *)tableView
        cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    static NSString *CellIdentifier = @"Cell";

    UITableViewCell *cell = [tableView
        dequeueReusableCellWithIdentifier:CellIdentifier];
    if (cell == nil) {
        cell = [[[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault
                                    reuseIdentifier:CellIdentifier]
                autorelease];
```
