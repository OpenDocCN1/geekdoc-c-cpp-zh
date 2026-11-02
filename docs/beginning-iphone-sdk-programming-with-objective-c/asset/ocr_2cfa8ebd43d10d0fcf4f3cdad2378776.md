# CHAPTER 6 EXERCISE SOLUTIONS

# Answer to Question 1

```
```objective-c
-(BOOL)shouldAutorotateToInterfaceOrientation:
(UIInterfaceOrientation)interfaceOrientation {

    return (interfaceOrientation == UIInterfaceOrientationLandscapeLeft ||
            interfaceOrientation == UIInterfaceOrientationLandscapeRight);
}
```
```

# Answer to Question 2

The frame property defines the rectangle occupied by the view, with respect to its superview (the view that contains it). Using the frame property allows you to set the positioning and size of a view. Besides using the frame property, you can also use the center property, which sets the center of the view, also with respect to its superview. You usually use the center property when you are performing some animation and just want to change the position of a view.

# CHAPTER 7 EXERCISE SOLUTIONS

# Answer to Question 1

```
```objective-c
mySecondViewController *vc = [[MySecondViewController alloc]
                              initWithNibName:nil
                              bundle:nil];
```
```

# Answer to Question 2

```
```objective-c
- (void)viewDidLoad
{
    //---create a CGRect for the positioning---
    CGRect frame = CGRectMake(10, 10, 300, 50);

    //---create a Label view---
    label = [[UILabel alloc] initWithFrame:frame];
    label.textAlignment = UITextAlignmentCenter;
    label.font = [UIFont fontWithName:@"Verdana" size:20];
    label.text = @"This is a label";

    //---create a Button view---
    frame = CGRectMake(10, 250, 300, 50);
    button = [[UIButton buttonWithType:UIButtonTypeRoundedRect]
              initWithFrame:frame];
}
```
```