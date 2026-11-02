Now, even when we declare the capability, geolocation is still subject to user consent, as mentioned in Chapter 1. When you first run the app with the capability set, then, you should see a popup like this, which appears in the user's chosen color scheme to indicate that it's a message from the system:

![](bbox=[0.15, 0.23, 0.78, 0.37])

If the user blocks access here, the error handler will be invoked with an error of "Canceled." (This is also what you get if the Geolocator object goes out of scope while the consent prompt is visible, even if you click Allow, which is again why I create the object outside the `app.onready` handler.)

Keep in mind that this consent dialog will appear only once for any given app, even across debugging sessions (unless you change the manifest or uninstall the app, in which cases the consent history is reset). After that, the user can at any time change their consent in the Settings > Permissions panel as shown in Figure 2-18, and we'll learn how to deal with such changes in Chapter 9. For now, if you want to test your app's response to the consent dialog, go to the Start screen and uninstall the app from its tile. You'll then see the popup when you next run the app.

![](bbox=[0.15, 0.68, 0.45, 0.88])

FIGURE 2-18 Any permissions that are subject to user consent can be changed at any time through the Settings Charm > Permissions pane.

# Sidebar: Writing Code in Debug Mode

Because of the dynamic nature of JavaScript, it's impressive that the Visual Studio team figured out how to make the IntelliSense feature work quite well in the Visual Studio editor. (If you're unfamiliar with IntelliSense, it's the productivity service that provides auto-completion for code