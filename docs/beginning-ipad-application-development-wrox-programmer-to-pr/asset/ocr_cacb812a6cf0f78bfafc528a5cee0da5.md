In the doneEditing: method (which is fired when the user dismisses the keyboard by tapping the return key), you make the View the first responder:

```
-(IBAction) doneEditing: (id) sender {
    //---when keyboard is hidden, make the view
    // the first responder
    // or else the Shake API will not work---
    [self.view becomeFirstResponder];
}
```

If you don't do this, the three motion-sensing events are not fired. The key point to remember is that something must be the first responder.

The motionBegan: event is fired when the OS suspects that the device is being shaken. If eventually the OS determines that the action is not a shake, the motionCancelled: event is fired. When the OS finally determines that the action is a shake action, the motionEnded: event is fired.

# Performing an Action When the Device Is Shaken

Now modify your project so that when the iPad is shaken, the DatePicker view is reset to today's date.

# TRY IT OUT Resetting the DatePicker when Shaken

1. In the ShakeViewController.m file, add the following statements that appear in bold:

```
- (void)ResetDatePicker {
    [datePicker setDate:[NSDate date]];
}
```

```
- (void)motionEnded:(UIEventSubtype)motion withEvent:(UIEvent *)event {
    if ([event.subtype == UIEventSubtypeMotionShake]) {
        NSLog(@"motionEnded:");
        [self ResetDatePicker];
    }
}
```

2. Press Command-R to test the application on the iPhone Simulator. Set the DatePicker view to some date. Choose Hardware ⇧ Shake Gesture to simulate shaking the device. Notice that the DatePicker view now resets to today's date.

# How It Works

In this example, you first added a ResetDatePicker method to reset the DatePicker view to today's date:

```
- (void)ResetDatePicker {
    [datePicker setDate:[NSDate date]];
}
```