# Chapter 14

# Creating a Pen

The simplest way to create a pen object is first to declare an object of the CPen class:

```
CPen aPen;        // Declare a pen object
```

This object now needs to be initialized with the properties you want. You do this using the class member function CreatePen(), which is declared in the CPen class as:

```
BOOL CreatePen (int aPenStyle, int aWidth, COLORREF aColor);
```

The function returns TRUE as long as the pen is successfully initialized and FALSE otherwise. The first argument defines the line style that you want to use when drawing. You must specify it with one of the following symbolic values:

| Pen Style | Description |
|---|---|
| PS_SOLID | The pen draws a solid line. |
| PS_DASH | The pen draws a dashed line. This line style is valid only when the pen width is specified as 1. |
| PS_DOT | The pen draws a dotted line. This line style is valid only when the pen width is specified as 1. |
| PS_DASHDOT | The pen draws a line with alternating dashes and dots. This line style is valid only when the pen width is specified as 1. |
| PS_DASHDOTDOT | The pen draws a line with alternating dashes and double dots. This line style is valid only when the pen width is specified as 1. |
| PS_NULL | The pen doesn’t draw anything. |
| PS_INSIDEFRAME | The pen draws a solid line, but unlike PS_SOLID, the points that specify the line occur on the edge of the pen rather than in the center, so that the drawn object never extends beyond the enclosing rectangle. |

The second argument to the CreatePen() function defines the line width. If aWidth has the value 0, the line drawn is 1 pixel wide, regardless of the mapping mode in effect. For values of 1 or more, the pen width is in the units determined by the mapping mode. For example, a value of 2 for aWidth in MM_TEXT mode is 2 pixels; in MM_LOENGLISH mode the pen width is 0.02 inches.

The last argument specifies the color to be used when drawing with the pen, so you could initialize a pen with the statement:

```
aPen.CreatePen(PS_SOLID, 2, RGB(255,0,0));  // Create a red solid pen
```

Assuming that the mapping mode is MM_TEXT, this pen draws a solid red line that is 2 pixels wide.

# Using a Pen

To use a pen, you must select it into the device context in which you are drawing. To do this, you use the CDC class member function SelectObject(). To select the pen you want to use, you call this function