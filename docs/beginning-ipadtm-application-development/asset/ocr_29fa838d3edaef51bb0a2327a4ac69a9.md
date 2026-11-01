# TRY IT OUT Mapping an XIB file to a View Controller

codefile TableView.zip available for download at Wrox.com

+   1. Create a new Split View-based Application project and name it TableView.
+   2. Examine the files in the TableView project, particularly the files created under the Classes and Resources folders (see Figure 7-12). Double-click the MainWindow.xib file to edit it in Interface Builder.
+   3. As shown in Chapter 4, the MainWindow.xib file contains a Split View Controller (see Figure 7-13).

The left side of the Split View Controller view is mapped to the RootViewController class (see Figure 7-14).

![](bbox=[0.7, 0.2, 0.95, 0.45])

FIGURE 7-12

![](bbox=[0.05, 0.5, 0.7, 0.82])

FIGURE 7-13

4. The RootViewController class uses the UITableViewController class (instead of the UIViewController class) and hence the left side of the Split View Controller will display a Table view:

```
#import <UIKit/UIKit.h>

@class DetailViewController;

@interface RootViewController : UITableViewController {
```