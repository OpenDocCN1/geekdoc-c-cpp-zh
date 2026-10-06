# 374 Plug-In JavaScript: 100 Power Solutions

FIGURE 13-6
Add cursor trails to the mouse pointer by calling this plug-in.

![](bbox=[0.305, 0.115, 0.836, 0.318])

each, the built-in Windows cursor trail utility. It also allows you to select your images for the trail. Figure 13-6 shows a cursor trail created using the mouse pointer image supplied with this plug-in on the pluginjavascript.com website.

# About the Plug-In

This plug-in creates a trail of images that follow the mouse pointer. It requires the following arguments:

+   - image The URL of an image to use for the trail
- length The length of the trail, with smaller numbers being shorter
- state If 1 or true the trails are turned on; a value of 0 or false turns them off

# Variables, Arrays, Functions

| j | Local variable for iterating through the ten images |
| w | Local variable containing the width of the browser |
| h | Local variable containing the height of the browser |
| c | Local variable containing the string 'CT_' |
| newimg | Local variable containing each new image as it is created |
| zIndex | Property of each image set to bring in front of all other elements |
| ABS | Global variable with the value 'absolute' |
| MOUSE_X & MOUSE_Y | Global variables containing the horizontal and vertical mouse coordinates |
| ZINDEX | Global variable containing the highest zIndex property so far used |
| Goto() | Plug-in to move an object to a new location |
| Hide() | Plug-in to hide an object |
| Show() | Plug-in to show an object that has been hidden |