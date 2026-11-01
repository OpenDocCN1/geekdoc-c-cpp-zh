
Remember, you use the Add Sibling button to add a new item within the same level. Use the Add Child button to add a new child item under the current level.

7. The Root.plist file should now look like Figure 11-11.

![](img/16991b58db5894715c4a443315e06a22_300_0.png)

FIGURE 11-11

8. Modify the entire Root.plist file so that it looks like Figure 11-12. Ensure that the capitalization of each key and value pairs is correct.

![](img/16991b58db5894715c4a443315e06a22_300_1.png)

FIGURE 11-12

6. In the FlipsideViewController.h file, insert the following code that appears in bold:

```objective-c
@protocol FlipsideViewControllerDelegate;

@interface FlipsideViewController : UIViewController <UIPickerViewDataSource, UIPickerViewDelegate> {
    id <FlipsideViewControllerDelegate> delegate;

    IBOutlet UITextField *loginName;
    IBOutlet UITextField *password;
    IBOutlet UIPickerView *favoriteColor;
}
@property (nonatomic, retain) UITextField *loginName;
@property (nonatomic, retain) UITextField *password;
@property (nonatomic, retain) UIPickerView *favoriteColor;

@property (nonatomic, assign) id <FlipsideViewControllerDelegate> delegate;
- (IBAction)done;

@end

@protocol FlipsideViewControllerDelegate
- (void)flipsideViewControllerDidFinish:(FlipsideViewController *)controller;
@end
```

7. In the FlipsideViewController.m file, add the following statements:

```objective-c
#import "FlipsideViewController.h"

@implementation FlipsideViewController

@synthesize delegate;
@synthesize loginName;
@synthesize password;
@synthesize favoriteColor;
```

8. In Interface Builder, connect the outlets and action to the various views. In the FlipsideView.xib window, do the following:

- Control-click and drag the File's Owner item to the first TextField view and select loginName.
- Control-click and drag the File's Owner item to the second TextField view and select password.
- Control-click and drag the File's Owner item to the Picker view and select favoriteColor.
- Control-click and drag the Picker view to the File's Owner item and select dataSource.
- Control-click and drag the Picker view to the File's Owner item and select delegate.

9. Right-click the File's Owner item to verify that all the connections are connected properly (see Figure 11-16).

```objective-c
[colors addObject:@"Green"];
[colors addObject:@"Blue"];

[super viewDidLoad];
self.view.backgroundColor = [UIColor viewFlipsideBackgroundColor];
}

//---number of components in the Picker view---
- (NSInteger)numberOfComponentsInPickerView:(UIPickerView *)thePickerView {
    return 1;
}

//---number of items(rows) in the Picker view---
- (NSInteger)pickerView:(UIPickerView *)thePickerView
    numberOfRowsInComponent:(NSInteger)component {
    return [colors count];
}

//---populating the Picker view---
- (NSString *)pickerView:(UIPickerView *)thePickerView titleForRow:(NSInteger)row
    forComponent:(NSInteger)component {
    return [colors objectAtIndex:row];
}

//---the item selected by the user---
- (void)pickerView:(UIPickerView *)thePickerView didSelectRow:(NSInteger)row
    inComponent:(NSInteger)component {
    favoriteColorSelected = [colors objectAtIndex:row];
}

- (void)dealloc {
    [colors release];
    [favoriteColorSelected release];
    [loginName release];
    [password release];
    [favoriteColor release];
    [super dealloc];
}
```

13. That’s it! Press Command-R to test the application on the iPhone Simulator. Figure 11-17 shows the UI of the application for the Main and Flipside views.

> **NOTE** Note that the compiler may generate a warning because you have not implemented the `loadSettings:` action in the `MainViewController.m` file yet. This is all right, as you just want to check out how the user interface looks.

## How It Works

To load the values of the preferences settings, you use a class known as the NSUserDefaults:

```objective-c
NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
```

The preceding statement returns the one-and-only instance of the NSUserDefaults class. Think of NSUserDefaults as a common database that you can use to store your application preference settings.

To retrieve the values of the preference settings, you use the objectForKey: method and specify the name of the preference setting you want to retrieve:

```objective-c
NSString *strLoginName = [defaults objectForKey:@"login_name"];
NSString *strPassword = [defaults objectForKey:@"password"];
NSString *strColor = [defaults objectForKey:@"color"];
```

## Resetting the Preference Settings Values

Sometimes you may want to reset the values of the preference settings of your application. This is especially true if you have made an error in the Root.plist file and want to reset all the settings. The easiest way to do this is to remove the application from the phone or Simulator. To do so, simply tap and hold the application’s icon, and when the icons start to wiggle, tap the X button to remove the application. The preference settings associated with the application will also be removed.

Another way to clear the values of the preference settings would be to navigate to the folder containing your application (on the iPhone Simulator). The applications on the iPhone Simulator are stored in the following folder: ~/Library/Application Support/iPhone Simulator/User/Applications/ (note that the tilde symbol (~) represents your home directory and not your root hard disk). Inside this folder, you need to find the folder containing your application. Within the application folder is a Library/Preferences folder. Delete the file ending with application_name.plist (see Figure 11-19) and your preferences settings will now be reset.

![](img/16991b58db5894715c4a443315e06a22_310_0.png)

FIGURE 11-19

```objective-c
[defaults setObject:password.text forKey:@"password"];
[defaults setObject:favoriteColorSelected forKey:@"color"];
}
[self.delegate flipsideViewControllerDidFinish:self];
```

2. Press Command-R to test the application on the iPhone Simulator. When the application is loaded, tap the i icon to switch to the Flipside view. Make some changes to the login name, password, and favorite color (see Figure 11-20). When you press Done, all the changes are made to the phone. When you return to the Main view, tapping the Load Settings Values button displays the updated settings values.

![](img/16991b58db5894715c4a443315e06a22_312_0.png)

FIGURE 11-20

## How It Works

You use the same approach to save the values back to the preferences settings as you do to retrieve those settings; that is, you use the NSUserDefaults class:

```objective-c
NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
[defaults setObject:loginName.text forKey:@"login_name"];
[defaults setObject:password.text forKey:@"password"];
[defaults setObject:favoriteColorSelected forKey:@"color"];
```

Rather than use the objectForKey: method, you now use the setObject:forKey: method to save the values.

A particular challenge for the Flipside view is that the existing value for the favorite color must be displayed in a Picker view; therefore, during the viewDidLoad: method, you need to load the values of the preferences settings and then determine the index of the Picker view to display the correct color. You do this via the indexOfObject: method of the NSMutableArray class:

```objective-c
//---find the index of the array for the color saved---
favoriteColorSelected = [[NSString alloc] initWithString:
    [defaults objectForKey:@"color"]];
int selIndex = [colors indexOfObject:favoriteColorSelected];

//---display the saved color in the Picker view---
[favoriteColor selectRow:selIndex inComponent:0 animated:YES];
```

## SUMMARY

In this chapter, you have seen how you can make use of the Application Preferences feature of the iPhone to save your application's preferences to the Settings application. Doing so allows you to delegate most of the mundane tasks of saving and loading an application's preferences settings to the OS. All you need to do is to use the `NSUserDefaults` class to programmatically access the preferences settings.

## EXERCISES

1. You have learned that you can use the `NSUserDefaults` class to access the preferences settings values for your application. What are the methods for retrieving and saving the values?

2. What are the two ways in which you can remove the preferences settings for an application?

3. What is the difference between the Add Child button and the Add Sibling button in the Property List editor?
