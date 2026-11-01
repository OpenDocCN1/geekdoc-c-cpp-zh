# CHAPTER 3 EXERCISE SOLUTIONS

# Answer to Question 1

In the .h file:

```
```objc
//---declare an outlet---
IBOutlet UITextField *nameTextField;
///...
//---expose the outlet as a property---
@property (nonatomic, retain) UITextField *nameTextField;
```
```

In the .m file:

```
```objc
@implementation BasicUIViewController

//---generate the getters and setters for the property---
@synthesize nameTextField;
- (void)dealloc {
    //---release the outlet---
    [nameTextField release];
    [super dealloc];
}
```
```

# Answer to Question 2

In the .h file:

```
```objc
- (IBAction)btnClicked:(id)sender;
```
```

In the .m file:

```
```objc
@implementation BasicUIViewController
///...
- (IBAction)btnClicked:(id)sender {
    //---your code for the action here---
}
```
```

# Answer to Question 3

Use the Alert view when you simply want to notify the user when something happens. Use an action sheet when you need the user to make a selection, usually from a set of options.

# Answer to Question 4

```
```objc
- (void)loadView {
    //---create a UIView object---
    UIView *view =
        [[UIView alloc] initWithFrame:[UIScreen mainScreen].applicationFrame];
```
```