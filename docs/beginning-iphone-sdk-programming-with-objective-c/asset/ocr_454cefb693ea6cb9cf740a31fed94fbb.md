![](bbox=[0.087, 0.095, 0.532, 0.412])

FIGURE 4-15

# How It Works

When the View is loaded, you first wire it up so that when the user taps one of its buttons, it triggers a method. In this case, the method is segmentChanged:.

```
```objective-c
[segmentedControl addTarget:self action:@selector(segmentChanged:)
           forControlEvents:UIControlEventValueChanged];
```
```

In the segmentChanged: method, you determine which button was clicked (via the selectedSegmentIndex property of the segmented control) and show and hide the relevant views:

```
```objective-c
- (IBAction)segmentChanged:(id)sender {
    NSInteger selectedSegment = segmentedControl.selectedSegmentIndex;
    if (selectedSegment == 0) {
        //---toggle the correct view to be visible---
        [self.view1 setHidden:NO];
        [self.view2 setHidden:YES];
    }
    else{
        //---toggle the correct view to be visible---
        [self.view1 setHidden:YES];
        [self.view2 setHidden:NO];
    }
}
```
```