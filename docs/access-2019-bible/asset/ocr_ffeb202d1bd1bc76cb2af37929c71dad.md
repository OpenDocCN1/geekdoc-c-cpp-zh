# Programming Events

An Access event is the result of consequence of some user action. An Access event occurs when a user moves from one record to another in a form, closes a report, or clicks a command button on a form. Even moving the mouse generates a continuous stream of events.

Access applications are event driven, and Access objects respond to many types of events. Access events are hooked into specific object properties. For example, checking or unchecking a check box triggers a MouseDown, a MouseUp, and a Click event. These events are hooked into the check box through the OnMouseDown, OnMouseUp, and OnClick properties, respectively. You use VBA to compose event procedures that run whenever the user clicks the check box.

Access events can be categorized into seven groups:

+   - **Windows (form, report) events:** Opening, closing, and resizing
+   - **Keyboard events:** Pressing or releasing a key
+   - **Mouse events:** Clicking or pressing a mouse button
+   - **Focus events:** Activating, entering, and exiting
+   - **Data events:** Changing the current row, deleting, inserting, or updating
+   - **Print events:** Formatting and printing
+   - **Error and timing events:** Happening after an error has occurred or some time has passed

In all, Access supports more than 50 different events that can be harnessed through VBA event procedures.

Of these types of events, by far the most common are the keyboard and mouse events on forms. As you’ll see in the following sections, forms and most controls recognize keyboard and mouse events. In fact, exactly the same keyboard and mouse events are recognized by forms and controls. The code you write for a mouse-click event on a command button is exactly the same sort of code that you might write for the mouse-click on a form.

In addition, most Access object types have their own unique events. The following sections discuss the most commonly programmed events. Many ActiveX controls you might use in your Access applications may have their own unique and special events. When using an unfamiliar control or a new type of object in your Access applications, be sure to check out what events and properties are supported by the control or object.

# Understanding how events trigger VBA code

You can create an event procedure that runs when a user performs any one of the many different events that Access recognizes. Access responds to events through special form and control properties. Reports have a similar set of events, tailored to the special needs and requirements of reports.