If you save the new nib and build and run the app, it will load and display the AView nib design, as shown in Figure 19.26.

# Figure 19.26

Running the app loads the new nib and displays it.

![](bbox=[0.185, 0.237, 0.831, 0.629])

The new button remains unlinked. It flashes when tapped, but does nothing. To fix that, add a `showBView:` method to `FirstAppViewController.m` with code to load and display the B view.

```
```objective-c
- (IBAction) showBView: (id) sender
{
    self.bViewController = [[BViewController alloc] initWithNibName:
        @"BViewController" bundle:nil];
    [aViewController.view removeFromSuperview];
    [self.view insertSubview:bViewController.view atIndex:0];
}
```
```

This is almost identical to the code in `viewDidLoad`. It loads the BViewController nib file, then calls `removeFromSuperview` to unlink the previously visible view from the view array and release it. The last line inserts the B view into the hierarchy to display it.