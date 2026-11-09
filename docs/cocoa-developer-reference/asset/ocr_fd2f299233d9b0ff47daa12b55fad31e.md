Figure 8.17

The start and stop buttons have been linked to their corresponding methods. Clicking the button triggers the method.

![](bbox=[0.213, 0.243, 0.753, 0.531])

# Creating a link using a selector

An action is a target, triggered by an event. In IB, event triggers are listed as Sent Actions. Although you’ve just dragged a link from the App Delegate to a button, in reality the message passes in the opposite direction, from the button to the delegate.

This distinction isn’t critical in this application. But sometimes it’s more convenient to drag a link from a button or other UI object to a link destination object, and then select one of its available methods.

Click the Counter App Delegate again, and click the diagonal cross to the left of the startCount link. This deletes the link; it’s the standard IB link removal option. You’ll re-create the link using an alternative approach.

Click Push Button (Start). Under the Sent Actions tab, you’ll see a single circle, labeled selector. A selector is a programmable method variable. It works like a pointer, but it points to a method and not to an object.