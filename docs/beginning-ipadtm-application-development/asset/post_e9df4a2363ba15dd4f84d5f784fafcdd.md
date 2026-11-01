
## SUMMARY

This chapter explored the Table view and explained how to customize it to display items in the various forms. You also learned how to implement search functionality in the Table view, which is an essential function in real-world applications.

## EXERCISES

1. Name the two protocols that your View Controller must conform to when using the Table view in your view. Briefly describe their uses.
2. Which is the method to implement if you want to add an index in a Table view?
3. Name the three disclosure and checkmark images that you can use. Which one of them handles user taps?

Answers to the Exercises can be found in Appendix A.

## WHAT YOU LEARNED IN THIS CHAPTER

| TOPIC | KEY CONCEPTS |
|---|---|
| Add items to a Table view | Handle the various events in the `UITableViewDataSource` protocol. |
| Allow users to select rows in a Table view | Handle the various events in the `UITableViewDelegate` protocol. |
| Add images to rows in a Table view | Use the `imageView` property of the `UITableViewCell` class and set it to an instance of the `UIImage` class containing an image. |
| Use a property list with a Table view | Use the following code snippet to locate the property list:<br>`NSString *path = [[NSBundle mainBundle] pathForResource:@"Movies" ofType:@"plist"];`<br>Then use a combination of `NSDictionary` and `NSArray` objects to retrieve the key/value pairs stored in the property list. |
| Group items in a Table view in sections | Implement the following methods:<br>- `numberOfSectionsInTableView:`<br>- `tableView:numberOfRowsInSection:`<br>- `tableView:titleForHeaderInSection:` |
| Add an index to a Table view | Implement the `sectionIndexTitlesForTableView:` method. |
| Add disclosure and checkmark images to a row in a Table view | Set the `accessoryType` property of an `UITableViewCell` object to one of the following:<br>- `UITableViewCellAccessoryDetailDisclosureButton`<br>- `UITableViewCellAccessoryCheckmark`<br>- `UITableViewCellAccessoryDisclosureIndicator` |
| Implement a search in a Table view | Use the Search Bar view and handle the various events in the `UISearchBarDelegate` protocol. |

In the next Try It Out, you modify the Root.plist file so that you can use it to store some user's credentials. This is very useful in cases where you are writing an application that requires users to log in to a server. When the user uses your application for the first time, he will supply his login credentials, such as username and password. Your application can then store the credentials in the application preferences so that the next time the user uses your application, the application can automatically retrieve the credentials without asking the user to supply them.

> NOTE For more information on the use of each key, refer to Apple's "Settings Application Schema Reference" documentation. The easiest way to locate it is to do a Web search for the title. The URL is: http://developer.apple.com/iPhone/library/documentation/PreferenceSettings/Conceptual/SettingsApplicationSchemaReference/Introduction/Introduction.html.

## TRY IT OUT Modifying the Application Preferences

1. In Xcode, select the Root.plist file and remove all four items under the PreferenceSpecifiers key. You do so by selecting individual items under the PreferenceSpecifiers key and then pressing the Delete key.

2. To add a new item under the PreferenceSpecifiers key, select the PreferenceSpecifiers key and click the Add Child button (see Figure 8-5).

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_273_0.png)

FIGURE 8-5

3. A new item is added for you. To add additional items, click the Add Sibling button (see Figure 8-6). Click the Add Sibling button three more times.

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_273_1.png)

FIGURE 8-6

4. The Root.plist file should now look like Figure 8-7.

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_274_0.png)

FIGURE 8-7

5. Change the Type of Item 0 to Dictionary and expand it by clicking the arrow displayed to the left of it (see Figure 8-8). Click the Add Child button to add a child to Item 0.

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_274_1.png)

FIGURE 8-8

6. A new item is added under Item 0 (see Figure 8-9). Click the Add Sibling button to add another item under Item 0.

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_274_2.png)

FIGURE 8-9

7. Remember, you use the Add Sibling button to add a new item within the same level. Use the Add Child button to add a new child item under the current level.

8. The Root.plist file should now look like Figure 8-10.

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_274_3.png)

FIGURE 8-10

The following preference specifiers are used in this example:

- **PSGroupSpecifier** Used to display a group for the settings. In this case, all the settings are grouped under the Account Information group.
- **PSTextFieldSpecifier** Specifies a text field.
- **PSMultiValueSpecifier** Specifies a list of selectable values. The Titles item contains a list of visible text that users can select from. The Values item is the corresponding value for the text selected by the user. For example, if the user selects Blue Color as his favorite color, the value Blue will be stored on the iPhone.

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_276_0.png)

FIGURE 8-12

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_277_0.png)

FIGURE 8-13

## PROGRAMMATICALLY ACCESSING THE SETTINGS VALUES

The preferences settings are of little use if you can't programmatically access them from within your application. In the following sections, you modify the application so that you can load the preferences settings as well as make changes to them programmatically.

First, use the following Try It Out to prepare the UI by connecting the necessary outlets and actions.

### TRY IT OUT Preparing the UI

1. Using the project created in the previous section, double-click the ApplicationSettingsViewController.xib file to edit it in Interface Builder.

2. Populate the View window with the following views (see Figure 8-14):

   - Round Rect Button
   - Label

```objc
[favoriteColor release];
[super dealloc];
}
```

code snippet ApplicationSettingsViewController.m

8. That's it! Press Command-R to test the application on the iPhone Simulator. Figure 8-16 shows the PickerView loaded with the three colors.

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_281_0.png)

FIGURE 8-16

### How It Works

So far, all the work that has been done prepares the UI for displaying the values retrieved from the preferences settings. In particular, you need to prepare the Picker view to display a list of colors from which the user can choose.

To load the Picker view with the three colors, ensure that the ApplicationSettingsViewController class conforms to the UIPickerViewDataSource and UIPickerViewDelegate protocols:

```objc
@interface ApplicationSettingsViewController : UIViewController
<UIPickerViewDataSource, UIPickerViewDelegate> {
```

The UIPickerViewDataSource protocol defines the methods to populate the Picker view with items while the UIPickerViewDelegate protocol defines methods to enable users to select an item from the Picker view.

In the ApplicationSettingsViewController.m file, you first create an NSMutableArray object to store the list of colors available for selection, in the viewDidLoad method:

```objc
- (void)viewDidLoad {
    //---create an array containing the colors values---
    colors = [[NSMutableArray alloc] init];
```

### TRY IT OUT Loading Settings Values

1. Using the project created in the previous section, insert the following method to the ApplicationSettingsViewController.m file:

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_283_0.png)

```objc
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

code snippet ApplicationSettingsViewController.m

2. Press Command-R to test the application on the iPhone Simulator. When the application is loaded, tap on the Load Settings Values button and you should see the settings values displayed in the Text Field views and the PickerView (see Figure 8-17).

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_283_1.png)

FIGURE 8-17
