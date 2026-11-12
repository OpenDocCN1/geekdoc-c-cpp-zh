In our case, we want to update the current date and make sure our text field is ready to receive new information. Implement the viewWillAppear: method as shown:

```
```objective-c
- (void)viewWillAppear:(BOOL)animated {
    // Sets the current time and date.
    self.currentDate = [NSDate date];
    self.dateLabel.text =
        [NSDateFormatter localizedStringFromDate:self.currentDate
            dateStyle:NSDateFormatterLongStyle
            timeStyle:NSDateFormatterShortStyle];
    // Clear the text field.
    self.weightTextField.text = @"";
    [self.weightTextField becomeFirstResponder];
    [super viewWillAppear:animated];
}
```
```

Here we create a new NSDate object set to the current date and time. We then use the NSDateFormatter class method localizedStringFromDate:dateStyle:timeStyle: to produce a properly localized string representation. As you might expect, the formatting of dates and times also varies greatly from country to country and language to language. The NSDateFormatter lets us easily create date strings based on the device’s language and region settings.

> **NOTE:** Both NSNumberFormatter and NSDateFormatter are subclasses of the NSFormatter abstract class. NSFormatter is designed to act as a base class for objects that format, validate, or parse strings. For more information on using formatters or even creating your own, see the Data Formatting Guide in Apple’s documentation.

![](bbox=[0.0, 0.721, 0.268, 0.863])

Next, we clear the text field and make it the first responder. Making a text field the first responder will automatically display the keyboard. Now, we’ve already linked the text field’s Did End On Exit event to the saveWeight: method. This method will be called whenever the keyboard’s Done button is pressed.