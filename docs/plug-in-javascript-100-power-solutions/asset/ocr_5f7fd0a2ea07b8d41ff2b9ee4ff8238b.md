# Variables, Arrays, and Functions

| Variable/Constant | Description |
| :--- | :--- |
| MOUSE_DOWN | Global integer set to true if a mouse button is currently held down, otherwise false |
| MOUSE_IN | Global integer set to true if the mouse pointer is currently within the browser window, otherwise false |
| MOUSE_X | Global integer containing the current horizontal coordinate of the mouse pointer |
| MOUSE_Y | Global integer containing the current vertical coordinate of the mouse pointer |
| SCROLL_X | Global integer containing the amount the browser has scrolled vertically, in pixels |
| SCROLL_Y | Global integer containing the amount the browser has scrolled horizontally, in pixels |
| KEY_PRESS | Global integer containing the value of the last key pressed |
| ZINDEX | Global integer containing the maximum z-index of any object accessed via the plug-ins |
| CHAIN_CALLS | Global array containing plug-ins that have been chained and which are yet to be executed |
| INTERVAL | Global integer containing the time in milliseconds between calls to a repeated event |
| UNDEF | Global string containing the value 'undefined' |
| HID | Global string containing the value 'hidden' |
| VIS | Global string containing the value 'visible' |
| ABS | Global string containing the value 'absolute' |
| FIX | Global string containing the value 'fixed' |
| REL | Global string containing the value 'relative' |
| TP | Global string containing the value 'top' |
| BM | Global string containing the value 'bottom' |
| LT | Global string containing the value 'left' |
| RT | Global string containing the value 'right' |
| BROWSER | Global string containing the name of the current browser |
| NavCheck | Subfunction to check for the existence of a string in the browser User string |

# How It Works

Let's look first at each of this plug-in's global variable definitions:

+   * MOUSE_DOWN This variable is updated by the two inline, anonymous functions (later in the plug-in) that are attached to the document.`onmouseup` and `document.`onmousedown` events. With it you can quickly make a check to see