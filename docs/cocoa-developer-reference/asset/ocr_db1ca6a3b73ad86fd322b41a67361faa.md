The template is designed for a very simple two-view app. Apps rarely are this simple, and it is more useful as an example of two techniques: switching views with the `presentModalViewController:` method and using protocol/delegate communication between views. The flipside view includes a delegate property, used as a link to the main view controller. When the user requests a return, the flipside view triggers a custom `flipsideViewControllerDidFinish:` method in the delegate. In the delegate—which is the main controller—this method calls the `dismissModalViewControllerAnimated:` method, and the modal view disappears and is replaced by the main view. You can populate both views with further features as needed.

![](bbox=[0.103, 0.297, 0.172, 0.351])

# TIP

The Done button and the Navigation bar on the flipside view are large and distractingly visible. A more typical app might implement the Done feature with a button, a segmented switch, or one of the touch methods. To simplify the flipside view, open its nib file, delete the Navigation bar, and replace it with an alternative return method.

# Figure 19.20

The main view in the Utility Application template uses a light info button graphic to swap views. The flipside view includes a less subtle navigation bar and Done button.

![](bbox=[0.168, 0.461, 0.815, 0.852])