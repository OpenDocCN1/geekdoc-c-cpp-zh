```
@property (nonatomic, retain) IBOutlet UINavigationBar *navigationBar;
@property (nonatomic, retain) id detailItem;
@end
```

Notice that the DetailsViewController class implements the following protocols:

+   - **UIPopoverControllerDelegate** — It implements this protocol so that if the PopoverView is about to be dismissed, you have a chance to be notified (so you can prevent its dismissal, for example).
+   - **UISplitViewControllerDelegate** — It needs to implement this protocol because when the iPad changes orientation, it needs to hide/display the PopoverView.

Examine the content of the DetailsViewController.m file:

```
#import "DetailViewController.h"
#import "RootViewController.h"

@implementation DetailViewController

@synthesize navigationBar, popoverController, detailItem;

/*
 ---Other commented out code are omitted from this code listing---
 */

/*
 When setting the detail item, update the view and dismiss
 the popover controller if it's showing.
 */
- (void)setDetailItem:(id)newDetailItem {
    if ([detailItem != newDetailItem]) {
        [detailItem release];
        detailItem = [newDetailItem retain];

        // Update the view.
        navigationBar.topItem.title = [detailItem description];
    }

    if (popoverController != nil) {
        [popoverController dismissPopoverAnimated:YES];
    }
}

- (void)splitViewController:(UISplitViewController *)svc
    willHideViewController:(UIViewController *)aViewController
 withBarButtonItem:(UIBarButtonItem *)barButtonItem
  forPopoverController:(UIPopoverController *)pc {
    barButtonItem.title = @"Root List";
    [navigationBar.topItem setLeftBarButtonItem:barButtonItem
        animated:YES];
```