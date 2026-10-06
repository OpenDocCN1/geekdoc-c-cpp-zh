
Note

The second application is more fun! You use the knowledge gained from your first application to build a simple calculator that does operations with fractions. You can use your Fraction class that you worked with earlier in the book, as well as a modified Calculator class. This time, your calculator needs to know how to work with fractions.

Let's dive right into the first program. The pedagogy used in this chapter is not to cover all the details; as noted, there's simply not enough space to do that here. Instead, we walk you through the steps to give you the necessary foundation for you to explore and learn more concepts on your own with a separate Cocoa or iOS programming text.

Figure 21.1 shows the first application you develop for the iPhone, running on the iPhone simulator (more about that shortly).

# Figure 21.1. First iPhone application.

![](img/6897a0c84e438cb4e5aad2d8a2fad0b8_695_0.png)

This application is designed so that when you press the button labeled “1” the corresponding digit appears in the display (see Figure 21.2). That's all it does! This simple application lays the groundwork for the second fraction calculator application.

# Figure 21.2. iPhone application results.

![](img/6897a0c84e438cb4e5aad2d8a2fad0b8_696_0.png)

By this point in the book, you should be quite comfortable using Xcode if you've been using it throughout to enter and test your programs. This time we'll also be using a feature of Xcode that lets you design your user interface by placing UI elements such as tables, labels, and buttons in a window that resembles the iPhone’s screen. Like any powerful development tool, this feature does take some getting used to.

# Note

Prior to the release of Xcode 4, the UI was designed using a separate application called Interface Builder.

Apple distributes an iPhone simulator as part of the iOS SDK. The simulator replicates much of your iPhone environment, including its home screen, Safari web browser, Contacts application, and so on. The simulator makes it much easier to debug your applications; you don't have to download each iteration of your application to an actual iPhone device and debug it there. This can save you a lot of time and effort.

To run applications on an iOS device, you need to register for the iOS developer program and pay a $99 fee (as of the time of this writing) to Apple. In turn, you will receive an activation code that will allow you to test and install applications on an iOS device. Unfortunately, you cannot develop applications even for your own iOS device without going through this process. Note that the application we develop in this chapter will be loaded and tested on the iPhone simulator and not on an iPhone device.

# Creating a New iPhone Application Project

Let's get to developing your first application. After you install the iOS SDK, start up the Xcode application. Select File, New, then New Project... Under iOS (and if you don't see this in the left pane, you haven't installed the iOS SDK), click on Application. You should see a window, as shown in Figure 21.3.

# Figure 21.3. Starting a new iOS project.

![](img/6897a0c84e438cb4e5aad2d8a2fad0b8_698_0.png)

Here you see templates that provide starting points for different types of applications, as summarized in the Table 21.1.

# Table 21.1. iOS Application Templates

| Application Type | Description |
| --- | --- |
| Master-Detail | For an application that uses a navigation controller. Contacts are a sample application of this type. Generates a split view-based application for a large-screen device as iPad |
| OpenGL Game | For OpenGL ES graphics-based applications as games |
| Page-based Application | For an application that uses a page view controller to manage the display of pages |
| Single View Application | For an application starting with a single view. You draw into the view and then display it in the window |
| Tabbed Application | For applications that use tabs. An example would be the Music application |
| Utility Application | For an application that has a flipside. The Stock Quote application is an example of this type |
| Empty Application | For an application that starts with your main iPhone window. You can use this as the starting point for any application. |

Returning to your New Project window, select Single View Application in the top right pane and then click on the Next button. Type in iPhone_1 for the Product Name, whatever you choose as the Company Identifier, set the Device Family to iPhone, check User Automatic Reference Counting, and uncheck Use Story Board and Include Unit Tests. Your screen should resemble Figure 21.4.

# Figure 21.4. Selecting project options.

![](img/6897a0c84e438cb4e5aad2d8a2fad0b8_699_0.png)

Click on Next. You can specify where to create your new project folder, and don't worry about whether the Source Control box is checked. Your screen should now look like Figure 21.5.

# Figure 21.5. Specifying where to store the project folder.

| Name | Date Modified |
| --- | --- |
| To Be Filed | 10:23 PM |
| DFT | 10:35 AM |
| ClassroomM shared files | 10:35 AM |
| Public | 10:35 AM |
| Sony | 7/22/11 |
| Digital Film Tree | 7/22/11 |
| Unlisted 3rt | 7/20/11 |
| Should've Been There | 7/20/11 |
| misc | 7/13/11 |
| Documentation | 6/23/11 |
| iOS Programming Class | 6/6/11 |
| ClassroomM | 5/20/11 |
| books | 1/11/11 |

![](img/6897a0c84e438cb4e5aad2d8a2fad0b8_700_0.png)

Now click Create. As you know from previous projects you created with Xcode, a new project will be created for you that contains templates for files you'll want to use. This is shown in Figure 21.6, where the iPhone_1 folder reveals five files: iPhone_1AppDelegate.h, iPhone_1AppDelegate.m, iPhone_1ViewController.h, iPhone_1ViewController.m, and MainWindow.nib. The rightmost pane contains, among other things, orientations supported by your application and the application's icon. We'll ignore this pane here.

# Figure 21.6. New iOS project iPhone_1 is created.

Depending on your settings and previous uses of Xcode, your window might not appear precisely as depicted in Figure 21.6. You can choose to follow along with whatever your current layout resembles or else try to make it match the figure more closely.

In the top-left corner of your Xcode window, you see a drop-down labeled Xcode Scheme. Because we're not developing this application to run directly on the iPhone, you want the SDK set up to run with the iPhone simulator. Select the iPhone simulator from the Scheme dropdown as shown in Figure 21.7.

# Figure 21.7. Selecting the iPhone simulator.

![](img/6897a0c84e438cb4e5aad2d8a2fad0b8_701_0.png)

# Entering Your Code

Now we're ready to modify some of your project files. Notice that a class called AppDelegate was created for you, where in this example project name is iPhone_1. An application delegate subclass is created for every new iOS application. In general, in this class are methods that control the application. This includes such things as what to do when the application starts, when it enters and leaves the background, when the system tells it's using too much memory, and when it terminates. We won't make any changes to this class in either of the examples.

A second class was also created for you called ViewController. As you can see, Xcode creates interface and implementation selections for you in the corresponding .h and .m files. A view controller is responsible for managing the display of one or more "views" on your display. We have only one view in this application, as depicted in Figure 21.1. It's uncommon for applications to present many different views and to have multiple view controllers to manage them.

So view controller class will be responsible for handling the event of pressing the button labeled “1.” We'll define a method to respond to that action when it occurs in the iPhone's window, in our example, the pressing of a button. You'll see shortly how you make the connection between that event to the execution of a specific method.

Your objects can also have instance variables whose values correspond to some control in your iPhone's window, such as the name on a label or the text displayed in an editable text box. These variables are known as outlets, and you'll see how you connect an instance variable to an actual control in the iPhone's window.

For our first application, we need a method that responds to the action of pressing the button labeled 1. We also need an outlet variable that contains (among other information) the text to be displayed in the label that we create at the top of the iPhone's window.

Edit the file iPhone_1ViewController.h to add a new UILabel property called display and declare an action method click1 to respond to the pressing of the button. Your interface file should appear as shown in Program 21.1. (The comment lines automatically inserted at the head of the file are not shown here.)

# Program 21.1. iPhone_1ViewController.h

```
@import <UIKit/UIKit.h>

@interface iPhone_1ViewController : UIViewController

@property (strong, nonatomic) IBOutlet *display;
- (void)click1:(id)sender;

@end
```
