```
- (IBAction)pinBtnClicked:(id)sender {
    //---append the pin entered to the string---
    [secretPin appendString:[sender titleForState:UIControlStateNormal]];
}
- (IBAction)btnClicked:(id)sender {
    //---if the user has entered the pin correctly---
    if ([secretPin isEqualToString: @"2345"]) {
        NSString *str = [[NSString alloc]
            initWithFormat:@"Hello, %@", nameTextField.text ];
        UIAlertView *alert = [[UIAlertView alloc]
            initWithTitle:@"Hello"
            message: str
            delegate:self
            cancelButtonTitle:@"OK"
            otherButtonTitles:nil, nil];
        [alert show];
        [alert release];
        [str release];
    }
}
- (void)viewDidLoad {
    //---init the string with an initial capacity of 1---
    secretPin = [[NSMutableString alloc] initWithCapacity:1];
    [super viewDidLoad];
}
- (void)dealloc {
    [nameTextField release];
    [secretPin release];
    [super dealloc];
}
```

In the preceding code, when the View is loaded, you initialize the mutable string secretPin with an initial capacity of one. A mutable string is a string whose content can be edited. In this case, you initialize it by setting its initial length to one. Whenever the user presses the buttons labeled 1 to 5, the pinBtnClicked: method is called. You use the titleForState: method together with the UIControlStateNormal constant to extract the text displayed on the button and then append it to the secretPin string:

```
[secretPin appendString:[sender titleForState:UIControlStateNormal]];
```

> **WARNING** The UIControlStateNormal constant represents the normal state of a view (control). Some other possible states are UIControlStateHighlighted (when the view is highlighted) and UIControlStateDisabled (when the view is disabled).

![](bbox=[0.1, 0.91, 0.16, 0.97])