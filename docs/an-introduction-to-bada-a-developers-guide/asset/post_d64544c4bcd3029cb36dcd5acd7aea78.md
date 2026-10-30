
## 3.2 Using the UI Framework

Implementing the application lifecycle effectively and appropriately is one important aspect of making the best use of the bada frameworks. A second is using the GUI frameworks to create an effective, good-looking, and easy-to-use GUI. The touch UI on bada has a host of nice features, and the built-in apps showcase them well. In the following sections we take a deeper look at bada’s control and graphics classes, which provide the building blocks for creating the app GUI.

### 3.2.1 Control Hierarchy

The bada UI classes provide a useful set of ready-made Control types. All UI elements, including Frame and Form, derive from the Control class as shown in Figure 3.2 which shows the most important classes of the Control hierarchy.

Note that, for reasons of clarity, the diagram does not show all the UI controls that derive from Control, but it does show the relationship between Control and Container.

Control is the base class for all GUI elements, and Frame and Form are the app’s top-level GUI objects.

![](img/a257d5fd53a79a244a20e587cd2f08f6_93_0.png)

Figure 3.2 The Control hierarchy.

### 3.2.2 More about UI Controls

Forms contain content. Content types include plain text, directly embedded images, and standard or custom controls. Controls that derive from the Container class can also be containers for nested controls. As well as containing content, controls are active and can respond to user events such as touches, multi-touches, and gestures.

As you would expect, bada provides a comprehensive set of standard controls, such as buttons, pickers, and edit areas, as well as more specialised controls including animations, Flash movies, and overlay panels that enable controls to be layered (for example to overlay player-like controls on a video frame).

Applications can also derive and customise their own controls, if there is no suitable standard control that meets the application’s needs.

All controls must be both drawn and shown in order to display, either synchronously using the Draw() and Show() methods, or asynchronously using RequestRedraw(). Note that the synchronous drawing methods should not be called from within a call-back. Instead, use the asynchronous RequestRedraw() method, which returns immediately after queuing the redraw request.

Container controls have an OnDraw() method that is called by the framework before any child controls are drawn, enabling any custom drawing to be performed in the Container (for example, drawing a bitmap background). Subsequent drawing of child controls will overwrite the relevant regions of the Container’s canvas, allowing a Container’s background to be drawn behind any controls that populate it.

> Note: A control only becomes displayable after it has been added to a displayable container. Whether a control is displayable will also determine whether its child controls, if any, are displayable. For this reason, a general rule is that no methods of the control should be called until after it has been added to its container, to avoid possible unexpected behaviour, for example related to displayability.

Drawing is therefore performed in the following order by the framework:

- 1. Calls the Form’s Draw() method.
- 2. Calls the Form’s OnDraw() method, since Form is a Container.
- 3. Calls the Draw() method of the first child control, if any.
- 4. Calls the OnDraw() method of the first child control, if any, if the child is a Container.
- 5. Calls the Draw() method of the second child control, etc.

Note that only Container controls have the OnDraw() method.

| Draw() | Draws the control to the canvas of the containing Window, which will normally be the Application Frame, since Frame is Window-derived (but e.g. Form is not). |
| Show() | Copies the Window canvas content to the displayable frame buffer. |
| RequestRedraw() | Asynchronous method that invokes Draw() and Show(), and returns immediately. |
| OnDraw() | Called by the framework when a Container control is drawn to enable any custom drawing to be performed before drawing any nested controls. |

Shown below is a selection of some of the standard Control-derived classes provided by bada, organised by the kind of user interactions you'll need when you design your user interface.

## Simple Buttons and Labels

- Button
- CheckButton
- Label

![](img/a257d5fd53a79a244a20e587cd2f08f6_95_0.png)

![](img/a257d5fd53a79a244a20e587cd2f08f6_95_1.png)

![](img/a257d5fd53a79a244a20e587cd2f08f6_95_2.png)

This group of controls is for generic buttons, presenting the user with tick box choices and in the case of the Label control displaying non-editable text or images.

## Pickers

ColorPicker

![](img/a257d5fd53a79a244a20e587cd2f08f6_96_0.png)

DatePicker

![](img/a257d5fd53a79a244a20e587cd2f08f6_96_1.png)

RadioGroup

![](img/a257d5fd53a79a244a20e587cd2f08f6_96_2.png)

Slider

![](img/a257d5fd53a79a244a20e587cd2f08f6_96_3.png)

TimePicker

![](img/a257d5fd53a79a244a20e587cd2f08f6_96_4.png)

These are controls which let the user select a colour, a date or time or, in the case of a RadioGroup, make one choice from a list of options. The slider allows the user to choose a value from a range.

## Lists

CustomList

![](img/a257d5fd53a79a244a20e587cd2f08f6_97_0.png)

ExpandableList

![](img/a257d5fd53a79a244a20e587cd2f08f6_97_1.png)

GroupedList

![](img/a257d5fd53a79a244a20e587cd2f08f6_97_2.png)

IconList

![](img/a257d5fd53a79a244a20e587cd2f08f6_97_3.png)

bada gives you lots of choice when it comes to displaying lists, from lists of icons to a CustomList where individual items can have different layouts. We use a simple list in BuddyFix to display the list of buddies.

## Editable Controls

EditDate

![](img/a257d5fd53a79a244a20e587cd2f08f6_97_4.png)

EditField

![](img/a257d5fd53a79a244a20e587cd2f08f6_97_5.png)

### 3.3.1 More about Canvas

The Canvas class enables direct access to the device display for drawing. Whenever you want to do direct drawing using graphical primitives (such as Line, Rectangle, Ellipse, Polygon, and so on, as well as TextElement for text and Bitmap for images, which are all members of the Osp::Graphics namespace), then you must use a Canvas.

You can explicitly construct a normal (global) Canvas object from anywhere in your GUI:

```
// Construct a "normal" or global canvas
Canvas* pCanvas = new Canvas();
pCanvas->Construct();
```

Note that Canvas is always constructed in two-phases by allocating with operator new and initialising with Construct() (see Chapter 4, on two-phase construction).

A normal Canvas overlays the application Frame and bypasses the window (and Control) hierarchy, providing direct access to the display and overwriting anything within its display rectangle (including your current Form and any Controls it contains). If no rectangle is specified in construction, a normal Canvas is full-screen size.

This means that Canvas can be used to set a full-screen background image. (Recall that both Frame and Form allow their background colour to be set, but will not load an image as background.)

Once Canvas is drawn, any subsequent Draw() calls will overwrite it, allowing Controls (for example) to be drawn on top of it. However, this will only be as robust as the sequence of Draw() calls in your code. So use this with care.

The more typical way of using Canvas, which operates within the window and control hierarchy (and therefore does not risk unintended overwriting of other GUI elements) is to request a local ‘window’ Canvas object. Every Control-derived object, from Form down through the Control hierarchy, owns a window Canvas object:

```
// Get the window canvas
Canvas* pCanvas = GetCanvasN();
```

In this case, the Canvas shares the context of its owning Control, including its display region and any other properties of the local graphics context that have been set. Typically, the caller then sets any desired display properties and draws, enabling a Canvas to be used to draw display primitives or background bitmaps directly to the screen within the context of a given Control, to create text or other graphics.

In practice, Canvas is most useful in the context of Container controls such as Frame, Form, and Panel.
