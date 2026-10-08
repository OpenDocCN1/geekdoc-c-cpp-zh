
# Working with Your Own Classes

Because classes form the basis of your Cocoa projects, you use them frequently. Most often, you create a class to store and manipulate the data for your application. Cocoa calls this type of class a Model. The class that takes care of displaying your data is the View. A third class — a Controller mediates between the Model and the View.

Here’s how you create and use your own class in board terms:

- 1. Create a class.
- 2. Build an interface.
- 3. Add a Controller class and connect it to the interface.
- 4. Define the methods for the class.
- 5. Define an action for the class.

To try your working with classes in Objective-C, follow these steps:

- 1. Create a Cocoa project.
  Launch Xcode and choose File:New Project. In the dialog that appears, choose Cocoa Application from the list of choices, name the project, and create it.

- 2. Create a class.
  You can create classes in Xcode or Interface Builder. For this class, use Xcode:
  - a. Choose File:New File.
  - b. In the window that appears, choose Objective-C Class and click Next.
  - c. In the next pane that appears, name the implementation file of the new class. Name it Driver.m, as shown in Figure 6-1.

This is the class you’ll use to create a taxi driver object. When you create the Driver class, header and implementation files — Driver.h and Driver.m, respectively — appear in your project.

- 3. Create a new Controller class:
  - a. Double-click mainMenu.xib in Xcode to show Interface Builder.
  - b. In the Library window, search for object and drag an NSObject item to the project window.
  - c. Press Cmd+D and name the new class MyViewController in the Identity Inspector, as shown in Figure 6-2.

This class will communicate with your interface.

- 4. Create an interface:
  - a. In Interface Builder, open the default window in your NIB file.
  - b. From the Library window, drag a push button (an NSButton), a check box, and four Label controls to display your window.

You use two of the Label controls to display the name of your cab driver and the driver for your trip. The other two Label controls are simply labels for the interface (Fare and Driver):

![](img/ea40cad434a338535474e82c1a6ace20_140_0.png)

**Figure 6-1:** Create a class to represent a taxi driver.

![](img/ea40cad434a338535474e82c1a6ace20_140_1.png)

**Figure 6-2:** Name the class MyController in the Identity Inspector window.

Figure 6-3 shows the interface with the empty Label controls selected.

![](img/ea40cad434a338535474e82c1a6ace20_141_0.png)

- 5. Add outlets to the MyController class.

For this project, you need to define three outlets as part of the MyController class:

- a. In the XIB project window, select the MyController class (Figure 6-2).
- b. Press Cmd+6 to open the Inspector window and add three outlets (distanceCheckbox, driverDisplay, and fareDisplay) to the class.

The driverDisplay and fareDisplay outlets give you access to the two Label controls in the interface, so you can display the fare and the name of the driver. The third outlet (distanceCheckbox) permits you to find out whether Distance > 10 miles check is selected.

Figure 6-4 shows the new outlets.

- 6. Add an action to the MyController class.

Add one action to MyController and name it calculateFare: (note the required trailing colon), as shown in Figure 6-5. This is the action that the Calculate Fare button triggers. When a user clicks this button, the application displays the name of the cabbie and calculates the fare based on one parameter: distance. If the trip is longer than ten miles, the program returns a fare. If the trip is less than ten miles, the program returns a different fare.

![](img/ea40cad434a338535474e82c1a6ace20_142_0.png)

Figure 6-4: Add three outlets to the My Controller class.

![](img/ea40cad434a338535474e82c1a6ace20_142_1.png)

![](img/ea40cad434a338535474e82c1a6ace20_142_2.png)

![](img/ea40cad434a338535474e82c1a6ace20_142_3.png)

Figure 6-5: Add a calculateFare: action to the My Controller class.

- 7. Wire the interface to the MyController instance.

You can't do anything with the three outlets and one action in your code until you connect them to the interface.

- a. Control+drag from the MyController instance in the NIB file window to the Label that's adjacent to the Fare label.
- b. In the small black connections list overlay that appears when you let go of the mouse, choose fareDisplay.

With MyController selected in the project window, press ⌘+5 to see the connections you make them.

- c. Repeat the same process for the other Label controls and the NSButton that looks like a check box by connecting them to their respective outlets (driverDisplay and distanceCheckbox).

Figure 6-6 shows the completed connections.

- 8. Create the files for MyController.

Select the MyController class in the project window and choose File:Write Class Files. The MyController.h and MyController.m files are added to your project in Xcode.

![](img/ea40cad434a338535474e82c1a6ace20_143_0.png)

![](img/ea40cad434a338535474e82c1a6ace20_143_1.png)

Figure 6-6: The My Controller outlets and actions.

9. After you complete your work in Interface Builder, choose File:Save to save the NIB file.

10. Return to Xcode to add code that makes your project work.

You find the following four files: Driver.h, Driver.m, MyController.h, and MyController.m. See Figure 6-7. If the Driver and MyController header and implementation files aren't in the Classes folder already, move them there. When you create them, they appear in whatever folder was last selected in your project. It helps keep things organized.

Continue with the following sections to finish your project.

![](img/ea40cad434a338535474e82c1a6ace20_144_0.png)

Figure 6-7: Move the Controller header and implementation files to the Classes folder in Xcode.

### Defining the class

Click the Driver.h file to view its contents. The Driver class serves as the model. To this file, add the following code to define the class interface:

```objective-c
#import <Cocoa/Cocoa.h>

@interface Driver : NSObject {
    NSString *firstName;
}
- (int)go:(BOOL)distance;
- (NSString *)firstName;
- (void)setFirstName:(NSString *)name;
@end
```

The code begins by including the appropriate header files:

```objective-c
#import <Cocoa/Cocoa.h>
```

The Cocoa framework provides basic functionality for your Cocoa applications.

The code then defines a Driver class, which inherits functionality from NSObject:

```objective-c
@interface Driver : NSObject {
    NSString *firstName;
}
@end
```

Almost all classes that you use in Cocoa inherit from NSObject. In fact, all classes in this book inherit from the NSObject superclass. NSObject is the primary base class for programming in Cocoa. You can think of NSObject as a kind of generic class that contains methods and variables for creating objects. When you're creating a class based on a window, button, or some other element, use NSObject. In this example, you're defining a class (Driver), which is an NSObject. The Driver class has a firstName instance variable that stores the taxi driver.

The rest of the code defines the three methods for the Driver class:

```objective-c
- (int)go:(BOOL)distance;
```

The first method, go, is what your code executes when a user wants the driver to take him somewhere. go has one parameter: a Boolean that represents the distance. For this example, imagine the cab driver changes rate for short trips (less than ten miles) and another rate for longer trips. Because this rate scheme includes only two prices, you can use a Boolean variable to determine which rate to charge. A Boolean can have one of two possible values: YES or NO.

The remaining two methods set and get the name of the cab driver. Later, you assign the name of the cab driver with setFirstName when you create an instance from this class:

```objective-c
- (void)setFirstName:(NSString *)name;
```
