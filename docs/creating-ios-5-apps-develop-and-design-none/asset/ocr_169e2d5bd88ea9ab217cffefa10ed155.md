Now, lets walk through the method’s implementation a step at a time.

```
```objc
#pragma mark - Private Methods

- (void)updateSaveAndEditStatus {
    if (self.weightHistory == nil) {

        // Disable editing.
        [self.weightTextField resignFirstResponder];
        self.weightTextField.enabled = NO;
        return;
    }
```
```

Here, we check to see if we have a nil-valued weightHistory property. This typically happens when our enter weight scene appears onscreen before our document loads. This happens almost every time the app launches.

We simply make sure our text field is not the first responder, and then we disable the text field. This prevents the user from making any changes until after our WeightHistory document is ready to go.

```
```objc
    UIDocumentState state =
        self.weightHistory.documentState;
    if (state & UIDocumentStateSavingError) {

        // Display save warning.
        [UIView
            animateWithDuration:0.25f
            animations:^{
                self.saveWarningLabel.alpha = 1.0f;
            }];
    } else {
        // Hide save warning.
        [UIView
            animateWithDuration:0.25f
```
```