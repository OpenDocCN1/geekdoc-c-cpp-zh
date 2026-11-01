10. Type the following statements highlighted in bold in the ScrollingViewsViewController.m file:

```
```objc
#import "ScrollingViewsViewController.h"

@implementation ScrollingViewsViewController

@synthesize textField;
@synthesize scrollView;

//---size of keyboard---
CGRect keyboardBounds;

//---size of application screen---
CGRect applicationFrame;

//---original size of ScrollView---
CGSize scrollViewOriginalSize;

-(void) moveScrollView:(UIView *) theView {

//---get the y-coordinate of the view---
CGFloat viewCenterY = theView.center.y;

//---calculate how much visible space is left---
CGFloat freeSpaceHeight = applicationFrame.size.height -
keyboardBounds.size.height;

//---calculate how much the scrollview must scroll---
CGFloat scrollAmount = viewCenterY - freeSpaceHeight / 2.0;

if (scrollAmount < 0) scrollAmount = 0;

//---set the new scrollView contentSize---
scrollView.contentSize = CGSizeMake(
applicationFrame.size.width,
applicationFrame.size.height +
keyboardBounds.size.height);

//---scroll the ScrollView---
[scrollView setContentOffset:CGPointMake(0, scrollAmount) animated:YES];
}

//---when a TextField view begins editing---
-(void) textFieldDidBeginEditing:(UITextField *)textFieldView {
[self moveScrollView:textFieldView];
}

//---when a TextField view is done editing---
-(void) textFieldDidEndEditing:(UITextField *) textFieldView {
[UIView beginAnimations:@"back to original size" context:nil];
scrollView.contentSize = scrollViewOriginalSize;
```
```