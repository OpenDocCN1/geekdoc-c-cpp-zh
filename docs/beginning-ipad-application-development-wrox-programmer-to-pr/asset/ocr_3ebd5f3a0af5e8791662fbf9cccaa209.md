2. In the MySecondViewController.m file, you provide the implementation for the buttonClicked: action:

```
- (IBAction) buttonClicked: (id) sender{
    UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Action invoked!"
                                                     message:@"Button clicked!"
                                                    delegate:self
                                           cancelButtonTitle:@"OK"
                                           otherButtonTitles:nil];
    [alert show];
    [alert release];
}
```

3. To connect the relevant event (Touch Up Inside) of the Button view with the buttonClicked: action, add the following bold code to the viewDidLoad() method:

```
- (void)viewDidLoad {
    //---create a CGRect for the positioning---
    CGRect frame = CGRectMake(10, 10, 300, 50);
    //---create a Label view---
    label = [[UILabel alloc] initWithFrame:frame];
    label.textAlignment = UITextAlignmentCenter;
    label.font = [UIFont fontWithName:@"Verdana" size:20];
    label.text = @"This is a label";
    //---create a Button view---
    frame = CGRectMake(10, 250, 300, 50);
    button = [UIButton buttonWithType:UIButtonTypeRoundedRect];
    button.frame = frame;
    [button setTitle:@"OK" forState:UIControlStateNormal];
    button.backgroundColor = [UIColor clearColor];
    //---add the action handler and set current class as target---
    [button addTarget:self
            action:@selector(buttonClicked:)
        forControlEvents:UIControlEventTouchUpInside];
    //---add the views to the current View---
    [self.view addSubview:label];
    [self.view addSubview:button];
    [super viewDidLoad];
}
```

4. That's it! Press Command-R to test the application on the iPhone Simulator. Clicking the OK button displays an alert view (see Figure 4-24).

![](bbox=[0.78, 0.78, 0.95, 0.95])