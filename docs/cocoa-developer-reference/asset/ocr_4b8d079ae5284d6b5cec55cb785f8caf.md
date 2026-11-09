Save the file and choose File▸ Reload All Class Files in Interface Builder to add the new `showView:` method as a linkable action. Click the round rect button in the view to select it. Click the Connections tab in the Inspector window to reveal a list of events. Link the button's Touch Down event to the First Responder object, as shown in Figure 19.27. Select the `showView:` method from the floating pop-up menu when it appears.

# Figure 19.27

Linking a button event to First Responder, which bypasses the class controller and sends it to the app's root view controller.

![](bbox=[0.17, 0.335, 0.81, 0.715])

# CAUTION

The list of user events is a standard feature in UIKit. Objects display the full list in IB, but most generate only some of the events; for example, round rect buttons do not support editing, so they never send the Editing Changed event. Text fields do not generate Touch Down events. If your view is not generating events as it should, double-check the events you have linked here.