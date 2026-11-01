
![](img/744c5ec15e15ca7891c98be71dc25d13_274_0.png)

FIGURE 8-7

- 5. Change the Type of Item 0 to Dictionary and expand it by clicking the arrow displayed to the left of it (see Figure 8-8). Click the Add Child button to add a child to Item 0.

![](img/744c5ec15e15ca7891c98be71dc25d13_274_1.png)

FIGURE 8-8

- 6. A new item is added under Item 0 (see Figure 8-9). Click the Add Sibling button to add another item under Item 0.

![](img/744c5ec15e15ca7891c98be71dc25d13_274_2.png)

FIGURE 8-9

- 7. Remember, you use the Add Sibling button to add a new item within the same level. Use the Add Child button to add a new child item under the current level.

- 8. The Root.plist file should now look like Figure 8-10.

![](img/744c5ec15e15ca7891c98be71dc25d13_274_3.png)

FIGURE 8-10

```
[favoriteColor release];
[super dealloc];
}
```

code snippet ApplicationSettingsViewController.m

- 8. That's it! Press Command-R to test the application on the iPhone Simulator. Figure 8-16 shows the PickerView loaded with the three colors.

![](img/744c5ec15e15ca7891c98be71dc25d13_281_0.png)

FIGURE 8-16

## How It Works

So far, all the work that has been done prepares the UI for displaying the values retrieved from the preferences settings. In particular, you need to prepare the Picker view to display a list of colors from which the user can choose.

To load the Picker view with the three colors, ensure that the ApplicationSettingsViewController class conforms to the UIPickerViewDataSource and UIPickerViewDelegate protocols:

```
@interface ApplicationSettingsViewController : UIViewController
<UIPickerViewDataSource, UIPickerViewDelegate> {
```

The UIPickerViewDataSource protocol defines the methods to populate the Picker view with items while the UIPickerViewDelegate protocol defines the methods to enable users to select an item from the Picker view.

In the ApplicationSettingsViewController.m file, you first create an NSMutableArray object to store the list of colors available for selection, in the viewDidLoad method:

```objc
- (void)viewDidLoad {
    //--create an array containing the colors values---
    colors = [[NSMutableArray alloc] init];
    [colors addObject:@"Red"];
    [colors addObject:@"Green"];
    [colors addObject:@"Blue"];

    [super viewDidLoad];
}
```

To set the number of components (columns) in the Picker view, implement the numberOfComponentsInPickerView: method:

```objc
//---number of components in the Picker view---
- (NSUInteger)numberOfComponentsInPickerView: (UIPickerView *)thePickerView {
    return 1;
}
```

To set the number of items (rows) you want to display in the Picker view, implement the pickerView:numberOfRowsInComponent: method:

```objc
//---number of items(rows) in the Picker view---
- (NSUInteger)pickerView:(UIPickerView *)thePickerView
numberOfRowsInComponent:(NSUInteger)component {
    return [colors count];
}
```

To populate the Picker view with the three colors, implement the pickerView:titleForRow:forComponent: method:

```objc
//---populating the Picker view---
- (NSString *)pickerView:(UIPickerView *)thePickerView
titleForRow:(NSInteger)row
forComponent:(NSInteger)component {
    return [colors objectAtIndex:row];
}
```

To save the color selected by the user in the Picker view, implement the pickerView:didSelectRow:inComponent: method:

```objc
//---the item selected by the user---
- (void)pickerView:(UIPickerView *)thePickerView didSelectRow:(NSUInteger)row
inComponent:(NSUInteger)component {
    favoriteColorSelected = [colors objectAtIndex:row];
}
```

The color selected will now be saved in the favoriteColorSelected object.

## Loading the Settings Values

With the user interface of the application ready, it is now time to see how you can programmatically load the values of the preference settings and then display them in your application. This display is useful because it gives your user a chance to view the values of the settings without needing to go to the Settings application.

## TRY IT OUT Loading Settings Values

- 1. Using the project created in the previous section, insert the following method to the ApplicationSettingsController.m file:

Available for download on Wrox.com

```
- (IBAction) loadSettings: (id) sender{

NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
loginName.text = [defaults objectForKey:@"login_name"];
password.text = [defaults objectForKey:@"password"];

//---find the index of the array for the color saved---
favoriteColorSelected = [[NSString alloc] initWithString:
[defaults objectForKey:@"color"]];

int selIndex = [colors indexOfObject:favoriteColorSelected];

//---display the saved color in the Picker view---
[favoriteColor selectRow:selIndex inComponent:0 animated:YES];
}
```

code snippet ApplicationSettingsController.m

- 2. Press Command-R to test the application on the iPhone Simulator. When the application is loaded, tap on the Load Settings Values button and you should see the settings values displayed in the Text Field views and the PickerView (see Figure 8-17).

![](img/744c5ec15e15ca7891c98be71dc25d13_283_0.png)

FIGURE 8-17

## How It Works

To load the values of the preferences settings, you use a class known as the NSUserDefaults:

```
NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
```

The preceding statement returns the one-and-only-one instance of the NSUserDefaults class. Think of NSUserDefaults as a common database that you can use to store your application preference settings.

To retrieve the values of the preference settings, you use the objectForKey: method and specify the name of the preference setting you want to retrieve:

```
loginName.text = [defaults objectForKey:@"login_name"];
password.text = [defaults objectForKey:@"password"];

//---find the index of the array for the color saved---
favoriteColorSelected = [[NSString alloc] initWithString:
    [defaults objectForKey:@"color"]];
```

## Resetting the Preference Settings Values

Sometimes you may want to reset the values of the preference settings of your application. This is especially true if you have made an error in the Root.plist file and want to reset all the settings. The easiest way to do this is to remove the application from the device or Simulator. To do so, simply tap and hold the application’s icon, and when the icons start to wriggle, tap the X button to remove the application. The preference settings associated with the application will also be removed.

Another way to clear the values of the preference settings would be to navigate to the folder containing your application (on the iPhone Simulator). The applications on the iPhone Simulator are stored in the following folder: ~/Library/Application Support/iPhone Simulator/<version_no>/Applications/ (note that the tilde symbol (~) represents your home directory and not your root hard disk). Inside this folder, you need to find the folder containing your application. Within the application folder is a Library/Preferences folder. Delete the file ending with application_name.plist (see Figure 8-18) and your preferences settings will now be reset.

![](img/744c5ec15e15ca7891c98be71dc25d13_284_0.png)

## Saving the Settings Values

Now that you have seen how to load the values of preferences settings, use the following Try It Out to see how to save the values back to the preferences settings. This allows users to directly modify their preferences settings from within your application, instead of using the Settings application to do so.

## TRY IT OUT  Saving Settings Values

- 1. Using the same project created in the previous section, insert the following method in the ApplicationSettingsViewController.m file:

```
-(IBAction) saveSettings: (id) sender {
NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
[defaults setObject:loginName.text forKey:@"login_name"];
[defaults setObject:password.text forKey:@"password"];
[defaults setObject:favoriteColorSelected forKey:@"color"];

UIAlertView *alert = [[UIAlertView alloc]
initWithTitle:@"Settings Values Saved"
message:@"Settings Saved"
delegate:nil
cancelButtonTitle:@"Done"
otherButtonTitles:nil];
[alert show];
[alert release];
}
```

- 2. Press Command-R to test the application on the iPhone Simulator. Make some changes to the login name, password, and favorite color. When you click the Save Settings Value button, all the changes are made to the device (see Figure 8-19). When you restart the application, clicking the Load Settings Values button displays the updated settings values.

## How It Works

You use the same approach to save the values back to the preferences settings as you do to retrieve those settings; that is, you use the NSUserDefaults class:

```
NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
[defaults setObject:loginName.text forKey:@"login_name"];
[defaults setObject:password.text forKey:@"password"];
[defaults setObject:favoriteColorSelected forKey:@"color"];
```

Rather than use the objectForKey: method, you now use the setObject:forKey: method to save the values.
