
## Explanation

- **EventArgs** is the base class for all event data. Other than its constructor, the EventArgs class inherits all its methods only from Object, though it does add a public static field *empty*, which represents an event with no state (to allow for the efficient use of events with no state).
- In case an event has no data to pass, then the passed event argument will be of type EventArgs, which has no public properties, being essentially a placeholder. If there is data to pass, say the location of a mouseclick or which key was pressed, then the event argument will be of a type derived from EventArgs, and it will have properties for the data being passed.
- The general signature for an event handler is as follows
- Some events use the base class EventArgs, but EventArgs contain no useful additional information about the event. The controls that do require their event handlers to know additional information about the event will pass in an object of a type derived from EventArgs.
- For example, the TreeView AfterCollapse event handler receives an argument of type TreeViewEventArgs, derived from EventArgs. TreeViewEventArgs has the properties Action and Node, each of which has values specific to the actual event.

```
private void Handler (object sender, EventArgs e)
```

```
Private Sub Handler (ByVal sender As Object, ByVal e As EventArgs)
```

## 11. Mouse Events

### 1. Common Control Events

| Event | Event argument | Description |
|---|---|---|
| Click | EventArgs | Raised when a control is clicked by the mouse. |
| ControlAdded | ControlEventArgs | Raised when a new control is added to Control.ControlCollection. |
| ControlRemoved | ControlEventArgs | Raised when a control is removed from Control.ControlCollection. |
| DockChanged | EventArgs | Raised if the Dock property— i.e., which edge of the parent container the control is docked to—is changed, either by user interaction or program control. |
| DoubleClick | EventArgs | Raised when a control is double-clicked. If a control has both a Click and DoubleClick event handler, the DoubleClick will be preempted by the Click event. |
| Enter | EventArgs | Raised when a control receives focus. Suppressed for Form objects. For nested controls, cascades up and down the container hierarchy. |
| Layout | LayoutEventArgs | Raised when any change occurs that affects the layout of the control (e.g., the control is resized or child controls are added or removed). |
| Leave | EventArgs | Raised when focus leaves the control. |
| Move | EventArgs | Raised when a control is moved. |
| Paint | PaintEventArgs | Raised when a control is redrawn. |
| ParentChanged | EventArgs | Raised when the parent container of a control changes. |
| Resize | EventArgs | Raised when a control is resized. Generally preferable to use the Layout event. |
| SizeChanged | EventArgs | Raised when the Size property is changed, either by user interaction or programmatic control. Generally preferable to use the Layout event. |
| TextChanged | EventArgs | Raised when the Text property changes, either by user interaction or programmatic control. |
| Validating | CancelEventArgs | Raised when a control is validating. If CancelEventArgs.Cancel property set true, then all subsequent focus events are suppressed. Suppressed if Control.CausesValidation property set false. |
| Validated | EventArgs | Raised when a control completes validation. Suppressed if the CancelEventArgs.Cancel property passed to the Validating event is set true. Suppressed if Control.CausesValidation property set false. |

### 2. Control Drag-and-Drop events

| Event | Event argument | Description |
|---|---|---|
| DragDrop | DragEventArgs | Raised when a drag-and-drop operation is completed. |
| DragEnter | DragEventArgs | Raised when an object is dragged onto the control. At the time this event is raised, the drag operation is still in progress (i.e., the user hasn't yet let the mouse button go up). |
| DragLeave | DragEventArgs | Raised when an object is dragged off of the control. |
| DragOver | DragEventArgs | Raised when an object is dragged over the control. |
| GiveFeedback | GiveFeedbackEventArgs | Raised during a drag operation to allow modification to the mouse pointer. |

### 3. Control Mouse events

| Event | Event argument | Description |
|---|---|---|
| MouseEnter | EventArgs | Raised when mouse pointer enters control. |
| MouseMove | MouseEventArgs | Raised when mouse pointer moved over control. |
| MouseHover | EventArgs | Raised when mouse hovers over control. |
| MouseDown | MouseEventArgs | Raised when mouse button pressed while mouse pointer is over control. |
| MouseWheel | MouseEventArgs | Raised when mouse wheel moved while control has focus. |
| MouseUp | MouseEventArgs | Raised when mouse button released while mouse pointer is over control. |
| MouseLeave | EventArgs | Raised when mouse pointer leaves control. |

## 12. Keyboard Events

Keyboard events provide access to implementation of keystrokes generated events.

### 1. Key Events for all controls

| Event | Event data | Description |
|---|---|---|
| KeyDown | KeyEventArgs | Raised when a key is pressed. The KeyDown event occurs prior to the KeyPress event. |
| KeyPress | KeyPressEventArgs | Raised when a character generating key is pressed. The KeyPress event occurs after the KeyDown event and before the KeyUp event. |
| KeyUp | KeyEventArgs | Raised when a key is released. |

- The KeyDown and KeyPress events are not the same as they are fired at different points in the keyboard event stream and contain different information in the EventArgs object.
- The KeyEventArgs event data associated with the KeyDown and KeyUp events provides low-level information about the keystroke.
- This information is used to determine if an upper- or lowercase character was pressed. It also tells if any modifier keys (Alt, Ctrl, or Shift) were pressed along with it in combination.

### 2. KeyEventArgs properties (KeyDown and KeyUp)

| Property | Data type | Description |
|---|---|---|
| Alt | Boolean | Read-only value indicating if the Alt key was pressed. `true` if pressed, `false` otherwise. |
| Control | Boolean | Read-only value indicating if the Ctrl key was pressed. `true` if pressed, `false` otherwise. |
| Shift | Boolean | Read-only value indicating if the Shift key was pressed. `true` if pressed, `false` otherwise. |
| Modifiers | Keys | Read-only flags indicating the combination of modifier keys (Alt, Ctrl, Shift) pressed. Modifier keys can be combined using the bitwise OR operator. |
| Handled | Boolean | Value indicating if the event was handled. `false` until set otherwise. |
| KeyCode | Keys | Read-only value containing the key code for the key pressed. Typical values include the A key, Alt, and BACK (backspace). |
| KeyData | Keys | Read-only value containing the key code for the key pressed, combined with modifier flags to indicate combination of modifier keys (Alt, Ctrl, Shift). |
| KeyValue | integer | Key code property expressed as a read-only integer. |

### 3. Unicode and ASCII Characters

- Each character in the American Standards Committee for Information Interchange (ASCII) character set is represented by a single byte (8 bits) of data, representing 256 characters. The first 128 characters (represented by 7 bits) are standardized and usually referred to as low-order ASCII characters. The upper 128 characters are not standardized, although many well established character sets use all 256 characters.
- Unicode characters are a superset of the ASCII character set. They are represented by two bytes, which allows a maximum of 65,536 characters. The Unicode technology was introduced to allow easier representation of languages other than English, especially Asian languages such as Chinese and Japanese, which do not have limited alphabets. Unicode also allows for character sets containing many more characters than an ASCII character set, such as special symbols and stylings of characters.

### 4. KeyPressEventArgs properties (KeyPress)

| Property | Description |
|---|---|
| Handled | Boolean value indicating if the event was handled. false until set otherwise. When true, the keystroke is not displayed. |
| KeyChar | Read-only value of type char containing the composed ASCII character. |

## Example 1

```
//illustration of Button events
using System;
using System.Drawing;
using System.Collections;
using System.ComponentModel;
using System.Windows.Forms;
using System.Data;

public class EventsForm : Form{
private Button m_nameButton;
private Button m_okButton;
private Label m_nameLabel;
private Container m_components = null;

public EventsForm(){
initializeComponents();
}
private void initializeComponents(){
m_nameLabel=new Label();
m_nameButton = new Button();
m_okButton = new Button();

SuspendLayout();

m_nameLabel.Location=new Point(16,16);
m_nameLabel.Text="Click User NAME button";
m_nameLabel.Size=new Size(300,23);
