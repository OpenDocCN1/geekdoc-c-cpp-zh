
## PaintBox Refinements

After some consideration, we might decide that the evolution of the PaintBox project could be broken down into the following refinement steps:

- Establish the basic user interface.
- Allow the user to draw basic shapes using different stroke colors.
- Allow the user to cut, copy, and paste shapes.
- Allow the user to select, move, and fill shapes.
- Allow the user to modify the dimensions of shapes.
- Allow the user to save and reload drawings.
- Include final touches such as the splash screen.

Note, first of all, that these refinements focus on breaking down the functionality of the system. Additional refinements may be necessary as we get into the iterative process. For instance, we may decide that we need a refinement to address problems that were discovered in previous refinements.

The listed refinements could have been broken down further. For example, one refinement could have been devoted to the ability to draw one particular type of shape. The level of refinement, just like many other decisions when developing a software system, is a judgment call. The developer must decide what is best in any particular situation.

The order in which we tackle the refinements is also important. The user interface refinement seems to be a logical first step because all other activity relies on it. We may decide that the ability to save and reload a drawing would be nice to have early for testing purposes. We might also note that being able to select an object is fundamental to operations such as move and cut/copy/paste. After further analysis, we end up with the set of refinements shown in Figure J.2.

| Refinement | Description |
|---|---|
| 1 | Present the basic graphical user interface, including the main frame, buttons, menus, menu items, and the drawing area. The select and shape buttons work together as a radio button set (only one can be chosen at a time). No functionality for these interface elements is included at this time. Exiting the program is provided only by the frame’s window close button. |
| 2 | Add support for drawing the four basic shapes: lines, ovals, rectangles, and polylines. The chosen shape button determines what shape is drawn. The stroke color button can be used to set the stroke color for the next shape drawn. The color button causes a separate dialog box to appear to allow color selection. |
| 3 | Add support for saving and loading drawings. This includes the functionality of the open, save, and save as File menu items. When the open, new, or exit File menu options are chosen, check to see if the current drawing has been modified since last saved, and if so prompt to see if the user wants to save the drawing. |
| 4 | Provide the ability to select and move shapes on the drawing surface. Simple graphic selection blocks should be presented on the shape’s outline to indicate the currently selected shape. Once selected, the mouse can be used to drag the shape to another location on the drawing surface. |
| 5 | Add the functionality for the cut, copy and paste Edit menu items. Once selected, a shape can be cut or copied. Once a shape has been cut or copied, it can be pasted (perhaps multiple times) onto the drawing surface at a fixed offset to the original position. Edit menu items that are not valid at any given time are disabled. For example, unless a shape is selected, the cut and copy menu items cannot be chosen. |
| 6 | Add support for filling and reshaping a shape. Once a shape has been selected, the fill color button can be used to determine its fill color. A menu item on the Edit menu can be used to remove the fill of any filled object (make it transparent). The currently selected shape will now have a reshape handle that can be used to change the dimensions of the shape. |
| 7 | Add some extra functionality to the program. These additions include a splash screen that appears when the system is initially executed, an about dialog box, keyboard shortcuts for all menu items, and packaging the application into an executable JAR file. |

FIGURE J.2 Functional refinements for the PaintBox project

### PaintBox Refinement #1

Most of the classes used for the interface come from predefined libraries. We use Swing technology whenever reasonable. For example, we can use a JPanel for the overall interface space, as well as separate JPanel objects to organize the button tools and the drawing area. The JButton class will serve well for the buttons. Classes such as JMenuBar and JMenuItem will serve to implement the menus.

Figure J.3 shows a class diagram that represents the classes that are important to the first refinement of the PaintBox project. Note that it does not include all classes that might be needed, nor does it address anything other than the needs of this one refinement.

The detailed design and implementation for the interface refinement might develop similarly to other graphical projects we’ve developed in previous chapters.

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_735_0.png)

FIGURE J.3 A class diagram for the interface refinement of the PaintBox project

We can create listener objects and methods as appropriate but not concern ourselves with their inner workings at this time. That is, our focus in this refinement is to present the user interface, not to create any of the functionality behind the interface. During the development of this refinement, we modify the details of the user interface until it appears just the way we’d like it.

At the end of the first refinement, we are left with a completely implemented program that presents only the user interface. The buttons do nothing when pushed, and the menu items do nothing when selected. We have no way of creating a drawing yet.

What we do have, however, is a complete entity that has been debugged and tested to the level of this refinement. We may show it to the client at this point and get further input. Any changes that result from these discussions can be incorporated into future refinements. Figure J.4 shows the PaintBox program after the first refinement has been completed.

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_736_0.png)

FIGURE J.4 The PaintBox application after refinement #1

### PaintBox Refinement #2

The next refinement to address is the ability to draw basic shapes, because all other operations use drawn shapes in one way or another. Therefore, in this refinement we focus on providing the processing power behind the buttons that draw shapes and specify color.

Most of the objects and classes that we will use in this refinement are not predefined as they were in the interface refinement. We might consider using the

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_738_0.png)

FIGURE J.5 A class diagram for the second refinement of the PaintBox project

### Remaining PaintBox Refinements

For space reasons, the code for the various PaintBox refinements is not presented in the text. The full implementation of the first two refinements can be downloaded with the rest of the book's examples. The remaining refinements are left as projects.

The refinements of the PaintBox program continue until all requirements issues and problems have been addressed. This type of evolutionary development is crucial for medium- and large-scale development efforts. Figure J.7 shows the PaintBox program after all of the seven refinements have been completed.

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_740_0.png)

FIGURE J.7 The PaintBox program after all of the seven refinements have been completed

This page intentionally left blank

## GUI Events

Throughout the Graphics Track sections of this book, we’ve discussed various events that components might generate. The goal of this appendix is to put the event/component relationship into context.

The events listed in Figure K.1 are generated by every Swing component. That is, we can set up a listener for any of these events on any component.

Some events are generated only by certain components. The table in Figure K.2 maps the components to the events that they can generate. Keep in mind that these events are in addition to the ones that all components generate. If a component does not generate a particular kind of event, a listener for that event cannot be added to that component.

We have discussed some of the events in Figures K.1 and K.2 at appropriate points in this text; we have left others for your independent exploration. Applying the basic concept of component/event/listener interaction is often just a matter of knowing which components generate which events under which circumstances.

Of course, many events occur in a GUI that have no bearing on the current program. For example, every time a mouse is moved across a component, many mouse motion events are generated. However, this doesn’t mean we must listen for them. A GUI is defined in part by the events to which we choose to respond.

Despite our heavy coverage of GUI development in this book, we’ve still only scratched the surface. The following list describes a few other Java GUI containers and components that are not covered in depth in this text:

| Event | Represents |
|---|---|
| Component Event | Changing a component’s size, position, or visibility. |
| Focus Event | Gaining or losing the keyboard focus. |
| Key Event | Pressing, releasing, and clicking keyboard keys. |
| Mouse Event | Clicking the mouse button and moving the mouse into and out of a component’s drawing area. |
| Mouse Motion Event | Moving or dragging a mouse over a component. |

FIGURE K.1 Events that are generated by every Swing component
