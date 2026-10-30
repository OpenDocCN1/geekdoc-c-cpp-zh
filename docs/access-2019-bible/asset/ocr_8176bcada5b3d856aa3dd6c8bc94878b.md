# The Ribbon creation process

Briefly, creating custom Ribbons is a five-step process:

+   1. Design the Ribbon and compose the XML that defines the Ribbon.
+   2. Write VBA callback routines (described in the following section) that support the Ribbon's operations.
+   3. Create the USysRibbons table.
+   4. Provide a Ribbon name and add the custom Ribbon's XML to the USysRibbons table.
+   5. Specify the custom Ribbon's name in the Access Options dialog box.

None of these steps is particularly intuitive, especially when it comes to composing the XML and writing callback routines. Your best bet is to find an example that is reasonably close to what you want and customize its XML to suit your purposes.

# Using VBA callbacks

A callback is code that is passed to another entity for processing, Each procedure you write to support operations on a Ribbon is passed to the “Ribbon processor” in Access that actually performs the Ribbon’s actions. This is very unlike the event-driven code you’ve been working with in Access. Clicking a button on a form directly triggers the code in the button’s Click event procedure. A Ribbon’s callback procedure is linked to the Ribbon but is internally processed by Access and does not directly run in response to the click on the Ribbon.

To fully understand this process, imagine that Access contains a process that constantly monitors activity on the Ribbon. As soon as the user clicks a Ribbon control, the Ribbon processor springs into action, retrieving the callback procedure associated with the control and performing the actions specified in the callback.

This means that there are no Click, DblClick, or GotFocus events associated with the Ribbon in Access. Instead, you bind a callback to a Ribbon control through the XML that defines the Ribbon. Each Ribbon control includes a number of action attributes that can be attached to callbacks, and the Ribbon processor takes over when the user invokes a control’s action.

Here is an example. The following XML statements define a button control on a Ribbon:

```
<button id="ViewProducts"
label="All Products"
size="large"
imageMso="FindDialog"
onAction="OpenProductsForm"
tag="frmProductsDisplay"/>
```