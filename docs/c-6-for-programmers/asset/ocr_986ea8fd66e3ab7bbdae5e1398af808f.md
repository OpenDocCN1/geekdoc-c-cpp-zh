of Fig. 14.7. Event delegates are multicast—they represent a set of delegate objects that all have the same signature. When an event occurs, the event sender calls every method referenced by the multicast delegate. This is known as event multicasting. Event delegates derive from class MulticastDelegate, which derives from class Delegate (both from namespace System). For most cases, you'll specify only one event handler for a particular event on a control.

# 14.3.4 Another Way to Create Event Handlers

For the GUI app in Fig. 14.5, you double clicked the Button control on the Form to create its event handler. This technique creates an event handler for a control's default event—the event that's most frequently used with that control. Controls can generate many different events, and each one can have its own event handler. For instance, your app also can provide an event handler for a Button's MouseHover event, which occurs when the mouse pointer remains positioned over the Button for a short period of time. We now discuss how to create an event handler for an event that's not a control's default event.

# Using the Properties Window to Create Event Handlers

You can create event handlers through the Properties window. If you select a control on the Form, then click the Events icon (the lightning bolt icon in Fig. 14.8) in the Properties window, that control's events are listed in the window. You can double click an event's name to display in the editor an existing event handler for that event, or to create the event handler if it does not yet exist in your code. You also can select an event, then use the drop-down list to its right to choose an existing method that should be used as the event handler for that event. The methods that appear in this drop-down list are the Form class's methods that have the proper signature to be an event handler for the selected event. You can return to viewing the properties of a control by selecting the Properties icon (Fig. 14.8).

![](bbox=[0.18, 0.8, 0.82, 0.92])

Fig. 14.8 | Viewing events for a Button control in the Properties window.

A single method can handle events from multiple controls. For example, consider an app that displays CheckBoxes that represent bold and italic fonts. The user could select bold, italic or both. In this case, the font's style depends on both CheckBoxes, so their events could be handled by the same method, which would determine each CheckBox's state to determine the user's selected font style