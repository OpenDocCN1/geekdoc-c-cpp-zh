**TABLE 27.4**

### Fit Deformation Dialog Box Buttons

| Toolbar Button | Name | Description |
|---|---|---|
| [icon] | Mirror Horizontally | Mirrors the selection horizontally |
| [icon] | Mirror Vertically | Mirrors the selection vertically |
| [icon] | Rotate 90 degrees CCW | Rotates the selection 90 degrees counterclockwise |
| [icon] | Rotate 90 degrees CW | Rotates the selection 90 degrees clockwise |
| [icon] | Delete Control Point | Deletes the selected control point |
| [icon] | Reset Curve | Returns the curve to its original form |
| [icon] | Delete Curve | Deletes the selected curve |
| [icon] | Get Shape | Selects a separate spline to use as a profile |
| [icon] | Generate Path | Replaces the current path with a straight line |
| [icon] | Lock Aspect | Maintains the relationship between height and width |

# Modifying Loft subobjects

When you select a Loft object, you can work with its subobjects in the Modify panel. The subobjects for a Loft include Path and Shape. The Path subobject opens the Path Commands rollout. This rollout has only a single button—Put—for creating a copy of the Loft path. If you click this button, the Put To Scene dialog box appears, enabling you to give the path a name and select to create it as a Copy or an Instance.

If your path is created as an Instance, you can edit it to control the Loft path.

# Tip

**Scaling or transforming a cross section has no effect on the Loft because there isn’t any way to access the shape transform. If you add an XForm modifier on the cross section, then you can control its transform after it is lofted.**

The Shape subobject opens the Shape Commands rollout. This rollout also includes a Put button along with some additional controls. The Path Level value adjusts the shape’s position on the path. The Compare button opens the Compare dialog box, which is discussed in the following section. The Reset button returns the shape to its former state before any rotation or scaling has taken place, and the Delete button deletes the shape entirely.