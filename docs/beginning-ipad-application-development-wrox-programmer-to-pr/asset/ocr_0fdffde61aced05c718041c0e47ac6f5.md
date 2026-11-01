```
self.popoverController = pc;
}

// Called when the view is shown again in the split view,
// invalidating the button and popover controller.
- (void)splitViewController:(UISplitViewController *)svc
willShowViewController:(UIViewController *)aViewController
invalidatingBarButtonItem:(UIBarButtonItem *)barButtonItem {
    [navigationBar.topItem setLeftBarButtonItem:nil animated:YES];
    self.popoverController = nil;
}

// Ensure that the view controller supports rotation and that the
// split view can therefore show in both portrait and landscape.
- (BOOL)shouldAutorotateToInterfaceOrientation:
(UIInterfaceOrientation)interfaceOrientation {
    return YES;
}

- (void)viewDidUnload {
    // Release any retained subviews of the main view.
    // e.g. self.myOutlet = nil;
    self.popoverController = nil;
}

- (void)dealloc {
    [popoverController release];
    [navigationBar release];

    [detailItem release];
    [super dealloc];
}

@end
```

There are two important events you need to handle in this controller (both events are defined in the UISplitViewControllerDelegate protocol):

+   - splitViewController:willHideViewController:withBarButtonItem:forPopoverController: — Fired when the iPad switches to portrait mode (where the PopoverView will be shown and the Table View will be hidden).
+   - splitViewController:willShowViewController:invalidatingBarButtonItem: — Fired when the iPad switches to landscape mode (where the PopoverView will be hidden and the Table View will be shown).