background resource. You can use a style to make the buttons share a common background, width, height, and other properties.

To create a style for a group of buttons, make one button with the properties you want in the style. Then select the button, open the Object menu, expand the Edit Style submenu, and select "Edit a Copy."

This creates a style and opens it for editing. Use the Properties window to set any additional property values for the style. When you are finished, click the "Return to Scope" button under the Figure 3-25.

Having created a style, you can use it to control others. Select a control, open the Object menu, expand the Edit Style submenu, expand its Resource menu, and select the style you want to apply.

Note that Expression Blend will only apply a style to an object that is compatible with the one you used to define the style. For example, if you define a Button style, you can not apply it to a Label.

![](bbox=[0.595, 0.102, 0.815, 0.315])

Figure 3-24

# EDITING STYLES

> If you need to edit a style, open the Resources window, find the style that you want to edit, and click the "Edit Resource" button to its right.

![](bbox=[0.595, 0.375, 0.815, 0.445])

Figure 3-25

# RESOURCES WINDOW

The Resources window lets you view and edit resources. Figure 3-26 shows the Resources window.

The Resources window lets you edit some values directly. For example, in Figure 3-26 you can type a new value for btnwidth in its textbox.

The Resources window provides editors for other values. If you click on the colored area to the right of the btnBrush resource, a brush editing area appears similar to the one you use to define a brush in the Properties window.

![](bbox=[0.595, 0.675, 0.875, 0.845])

Figure 3-26

# OBJECTS AND TIMELINE

The Objects and Timeline area shown in Figure 3-27 lets you edit objects and storyboards. Usually you use this area to select controls so you can change their properties in the Properties window.