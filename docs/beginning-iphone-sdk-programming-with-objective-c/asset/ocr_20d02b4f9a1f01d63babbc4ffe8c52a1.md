The first view you create is the UIView object, which allows you to use it as a container for more views:

```
```objc
//---create a UIView object---
UIView *view =
[[UIView alloc] initWithFrame:[[UIScreen mainScreen].applicationFrame];

//---set the background color to lightgray---
view.backgroundColor = [UIColor lightGrayColor];
```
```

Next, you create a Label view and set it to display a string:

```
```objc
//---create a Label view---
CGRect frame = CGRectMake(10, 15, 300, 20);
UILabel *label = [[UILabel alloc] initWithFrame:frame];
label.textAlignment = UITextAlignmentCenter;
label.backgroundColor = [UIColor clearColor];
label.font = [UIFont fontWithName:@"Verdana" size:20];
label.text = @"This is a label";
label.tag = 1000;
```
```

Notice that you have also set the tag property, which is very useful for allowing you to search for particular views during runtime.

You also create a Button view by calling the buttonWithType: method with the UIButtonTypeRoundedRect constant. This method returns a UIRoundedRectButton object (which is a subclass of UIButton).

```
```objc
//---create a Button view---
frame = CGRectMake(10, 70, 300, 50);

UIButton *button = [UIButton buttonWithType:UIButtonTypeRoundedRect];
button.frame = frame;
[button setTitle:@"Click Me, Please!" forState:UIControlStateNormal];
button.backgroundColor = [UIColor clearColor];
button.tag = 2000;
```
```

You then wire an event handler for its Touch Up Inside event so that when the button is tapped, the buttonClicked: method is called:

```
```objc
[button AddTarget:Self action:@selector(buttonClicked:)
forControlEvents:UIControlEventTouchUpInside];
```
```

Finally, you add the label and button views to the view you created earlier:

```
```objc
[view addSubview:label];  [view addSubview:button];
```
```

Finally, you assign the view object to the view property of the current View Controller:

```
```objc
self.view = view;
```
```