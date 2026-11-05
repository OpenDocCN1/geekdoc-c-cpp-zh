| Event | EventArgs | Description |
|---|---|---|
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