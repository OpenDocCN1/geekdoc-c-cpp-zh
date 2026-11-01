![](bbox=[0.07, 0.15, 0.62, 0.55])

FIGURE 4-10

8. You can now rearrange the ImageView views on the View window so that they overlap each other.

9. In Xcode, add the following statements that appear in bold to the UsingViewsViewController.m file:

```
#import "UsingViewsViewController.h"

@implementation UsingViewsViewController

@synthesize pageControl;
@synthesize imageView1, imageView2;

- (void)viewDidLoad {

    //---initialize the first imageview to display an image---
    [imageView1 setImage:[UIImage imageNamed:@"iMac_old.jpeg"]];
    tempImageView = imageView2;

    //---make the first imageview visible and hide the second---
    [imageView1 setHidden:NO];
    [imageView2 setHidden:YES];

    //---add the event handler for the page control---
    [pageControl addTarget:self action:@selector(pageTurning:) forControlEvents:UIControlEventValueChanged];
```