```
```
forState:UIControlStateNormal];
[self.unitsButton setTitleColor:[UIColor blueColor]
                        forState:UIControlStateHighlighted];
[self.unitsButton addTarget:self
                     action:@selector(changeUnits:)
           forControlEvents:UIControlEventTouchUpInside];
self.weightTextField.rightView = self.unitsButton;
self.weightTextField.rightViewMode = UITextFieldViewModeAlways;}
```
```

We start by creating a custom button. Then we configure it. It’s 17 points tall and 25 points wide, with a light gray background. We also configure its title. It uses a 12-point bold system font and is center aligned. It’s important to center the title; as the user changes units, we will switch the button’s label between “lbs” and “kg.” Centering the label gives the button a nice, consistent appearance, even when the label’s size changes.

Next, we set the default title to “lbs” and then assign text colors for the different control states. Normally the text is dark gray, but when the button is highlighted, the text turns blue.

We also assign the changeUnits: action to our button’s UIControlEventTouchUp Inside event. This is identical to drawing a connection between a button’s Touch UpInside event and the desired action in Interface Builder. When the unitsButton is touched, the system will call changeUnits:.

Finally, we assign the unit button to the text field’s rightView property. This will cause it to appear inside the text field along the right side. We then set the view mode so that our button is always visible.

As always, since we assigned the button in viewDidLoad, we should clear it in viewDidUnload. Navigate down to viewDidUnload and add the following line:

```
```
self.unitsButton = nil;
```
```

Finally, add a method stub for our changeUnits: action. We will flesh out this method after adding the change units view to our storyboard.

```
```
- (IBAction)changeUnits:(id)sender {
    // method stub
}
```
```