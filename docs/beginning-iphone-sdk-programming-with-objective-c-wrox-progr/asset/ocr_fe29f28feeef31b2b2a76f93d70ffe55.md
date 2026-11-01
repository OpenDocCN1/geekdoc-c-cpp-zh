![](bbox=[0.12, 0.14, 0.64, 0.45])

# FIGURE 8-23

4. Back in Xcode, add the following lines that appear in bold to DetailsViewController.h:

```
#import <UIKit/UIKit.h>

@interface DetailsViewController : UIViewController {
    IBOutlet UILabel *label;
    NSString *textSelected;
}
@property (nonatomic, retain) UILabel *label;
@property (nonatomic, retain) NSString *textSelected;
-(id) initWithTextSelected:(NSString *) text;
@end
```

5. Back in Interface Builder, set the Class property of the File's Owner item for the DetailsView.xib window to be DetailsViewController.

6. Control-click and drag the File's Owner item to the Label view and select label. Doing so connects the Label view to the label outlet.

7. Control-click the File's Owner Item to the View item and select view. This action connects the View Controller to the view.