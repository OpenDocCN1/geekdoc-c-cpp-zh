```
```objective-c
NSString* message = @"There are no changes that "
                  @"can be undone at this time.";
UIAlertView* alert = [[UIAlertView alloc]
                      initWithTitle:title
                      message:message
                      delegate:nil
                      cancelButtonTitle:@"OK"
                      otherButtonTitles:nil];
[alert show];
[alert release];
}
}
```
```

iOS typically uses the shake gesture to trigger undo commands; however, it’s very easy to accidentally trigger shake gestures. Therefore, we should have the user confirm the undo command before we actually perform it.

This method handles that for us. If we have an undo action available, it creates an alert message using the action name. Otherwise, it displays a message letting the user know that it cannot undo anything at this time.

Note that our code doesn’t actually do anything until the user taps the Undo button. We catch this in the alertView:didDismissWithButtonIndex: method.

```
```objective-c
# pragma mark - alert view delegate methods
- (void)alertView:(UIAlertView *)alertView
didDismissWithButtonIndex:(NSInteger)buttonIndex {
    // Undo the last action if it is confirmed.
    if (buttonIndex == 1) {
        [self.undoManager undo];
    }
}
```
```