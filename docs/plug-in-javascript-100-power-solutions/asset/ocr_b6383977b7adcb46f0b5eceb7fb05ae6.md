# RollOver(O)

You've almost certainly seen and used rollover images that change as the mouse passes over them, but what about making rollover objects do the same? That's what this plug-in does. With it, rollovers can contain HTML, images, and anything else you like, making it much more powerful than simple image rollovers.

8-9 shows an advertisement from a classified ads site.
When you move the mouse over it, it rolls to show the new details in Figure 8-10.

# About the Plug-In

This plug-in takes two objects that can be images, divs, or spans containing HTML and/or images. It creates a rollover so that the second object is displayed when the mouse passes across the first. It requires the following arguments:

+   * ro1 an object or ID or an array of objects or object IDs—if it is an array, then ro2 must also be an array with the same number of elements
* ro2 an object or ID or an array of objects or object IDs—this should only be if rol is an array

# Variables, Arrays, and Functions

| a | Local array containing the objects in ro1 and ro2 |
| w, h | Local variable containing the width and height of the objects |
| x, y | Local variable containing the top left coordinates of the objects |
| iid | Local variable containing the result of calling setInterval() used for later calling clearInterval() |
| MOUSE_X, MOUSE_Y | Global variables containing the current horizontal and vertical positions of the mouse pointer |
| Hide | Plug-in to hide an object |
| HideToggle() | Plug-in to toggle the hidden/shown state of an object |
| Locate() | Plug-in to move an object to another location and assign it a position property such as 'relative' or 'absolute', and so on |
| onmouseover | Event of rol that calls the DoRoll() function |
| DoRoll() | Subfunction to move a rollover from ro2 and then set a repeating interrupt to the RollCheck() sub-function to see if the mouse has moved away |
| RollCheck() | Subfunction that returns every INTERVAL milliseconds when it is called unless the mouse has moved away from ro2, in which case the objects are rolled back again

# How It Works

This plug-in supports arrays as well as single objects and is unique among all the plug-ins in that, if the first argument is an array, the second one must also be an array.