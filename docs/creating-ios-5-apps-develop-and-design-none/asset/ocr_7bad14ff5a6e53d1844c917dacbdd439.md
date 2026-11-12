In most graphical user interfaces, a modal view is a view that must be dismissed (usually by clicking an OK or Cancel button) before the user can perform any other actions in the application. This forces the user to focus on whatever is inside the modal view—they must finish dealing with it before they can move on. On desktop applications, we generally use modal view to display things like Save or Print dialogs. On the iPhone, modal views cover the entire screen (though the iPad has a few additional options).

So, what does this all mean? Well, we’re tracing through how the objects in our application get created. The UIApplicationMain() method creates an instance of the UIApplication and of our HWAppDelegate class.

Next, UIApplicationMain() looks up the main storyboard in our application’s info.plist file. It then loads the storyboard’s initial scene, displaying our main view controller’s view in our application’s window. Our application is then ready for user input.

If the user touches the info button, our segue launches. This loads the flipside view controller and displays it as a modal view. When the user presses the Done button, it calls flipside view controller’s done: action. We know this dismisses the flipside view, but we don’t yet know how this works. To see that, we have to examine the application’s code.

# EXAMINING THE CODE

While the storyboard gives us a good overview of our application, to really understand it we will need to dig into the code. Don’t worry if it doesn’t all make sense yet, we will go over Objective-C in more detail in Chapter 2. For now, we just want to get a feel for the things are and what they do.

Let’s start with HWAppDelegate.h. This declares the interface for the HWAppDelegate class. You won’t find anything terribly surprising here. HWAppDelegate implements the UIApplicationDelegate protocol—which allows it to act as an application delegate.

A delegate is an object that acts on behalf of, or in coordination with, another object. The delegate typically acts as an assistant to the main, delegating object. The main object will call predefined methods on the delegate in response to specified events. The delegate then uses those methods to monitor and control the delegating object. This allows us to alter the delegating object’s behavior without changing the object itself.