Think of a selector as a generic placeholder for methods. It can be filled with any method you choose. When you link to a selector, you fill the placeholder with a specific method. The method is triggered when the user interacts with the object.

![](bbox=[0.119, 0.203, 0.188, 0.258])

# NOTE

For more information about selectors, see Chapter 9.

With a button, the method is triggered when the user clicks the button. Selectors are used throughout Cocoa. For example, click the Main Menu item, and use the reveal triangles to drill down to the menu Item (Undo) object in the menu. You'll see that a sent action to a method called undo : is already defined. Click the delete cross. The method is deleted, and you can see that the menu item uses a selector to specify its action, as shown in Figure 8.18.

# Figure 8.18

Many objects use a selector to define the method is triggered when the user interacts with them. Selectors are the core feature of the Cocoa menu system.

![](bbox=[0.236, 0.497, 0.77, 0.789])