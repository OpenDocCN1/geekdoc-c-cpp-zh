4. Drag and drop some Label objects from the Object Library onto the detail view, as shown in Figure 8–9. Make sure that the bottom Label controls are set to the width of the view. This is so that they can hold a fairly long amount of text. The two Label objects with the text “Label” in them are the ones we’re going to hook up to two of the values from our Book object: the Title and Author(s).

# # Adding Instance Variables

Next, we're going to add some instance variables to the DetailViewController class. These instance variables will correspond to the detail view's labels.

+   1. First, open the DetailViewController.h file and delete the detailDescriptionLabel property—we’ve deleted it from the interface and we don't need it anymore.

+   2. Next, we'll add two fields that represent the labels on the detail view that we want to store our book data into, as shown in Listing 8–14

**Listing 8-14.** Modifying DetailViewController.h file to include the new Labels.

```
#import <UIKit/UIKit.h>

@interface DetailViewController : UIView

@property (strong, atomic) id detailItem;

@property (strong, atomic) IBOutlet UILabel *titleLabel;
@property (strong, atomic) IBOutlet UILabel *authorLabel;

@end
```

+   3. If you recall from Chapter 7, the IBOutlet identifiers included in the properties let that these instance variables (titleLabel and authorLabel) are controls that appear in a view. Next, right-click on the label right below the “Title” and drag a New Referencing Outlet to the topmost object called the “File’s Owner”, as shown in Figure 8–10.