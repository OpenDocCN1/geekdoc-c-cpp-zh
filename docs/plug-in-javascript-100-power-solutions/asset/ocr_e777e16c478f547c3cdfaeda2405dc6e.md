# Chapter 10: Audio and Visual Effects 291

# Variables, Arrays, and Functions

| | |
|---|-|
| newdiv | New div object created to use for the frame |
| LB_DIV | Object ID of the new div |
| cursor | Style property of id that sets the mouse cursor to a pointer when it is over, indicating that it is clickable |
| overflow | Style property of document.body set to 'hidden' during the display of id to prevent scrolling |
| zIndex | Style properties of both the frame and id, to bring them to the forefront of the browser |
| onclick | Event of id set to dismiss the light if clicked |
| HID | Global variable with the value 'hidden' |
| ABS | Global variable with the value 'absolute' |
| ZINDEX | Global variable containing the highest zIndex used so far |
| DismissLB() | Subfunction to dismiss the light |
| Hide() | Plug-in to hide an object |
| Show() | Plug-in to show a previously hidden object |
| Position() | Plug-in to set an object's style position property |
| Locate() | Plug-in to set an object's style position property and move it to a new location |
| Resize() | Plug-in to resize an object |
| Opacity() | Plug-in to set an object's opacity |
| Center() | Plug-in to center an object in the browser |
| GetWindowWidth() | Plug-in to return the width of the browser |
| GetWindow() | Plug-in to return the height of the browser |
| Fade() | Plug-in to fade the opacity of an object to a new level |
| FadeIn() | Plug-in to fade the opacity of an object to 0 |
| FadeOut() | Plug-in to fade the color of an object between two colors |
| ColorFade() | Plug-in to fade two or more plug-ins in a sequence |
| Chain | Plug-in to insert values into a string |
| InsVars() | | |
| createElement() | Function to create a new HTML element |
| setAttribute() | Function to set an attribute of an HTML element |
| appendChild() | Function to append a child HTML element |

# How It Works

This plug-in starts by setting the mouse cursor when over id into a pointer, to indicate that it is clickable (doing so dismisses the light box), like this:

```
S(id).cursor = 'pointer'
```