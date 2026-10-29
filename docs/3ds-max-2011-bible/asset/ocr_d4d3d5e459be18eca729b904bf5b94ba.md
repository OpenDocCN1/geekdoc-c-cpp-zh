# Part V: Animation and Rendering Basics

# Using constraints

You can apply constraints to selected objects using the Animation ⇔ Constraints menu. The constraints contained within this menu include Attachment, Surface, Path, Position, Link, LookAt, and Orientation.

All constraints have the same controller icon displayed in the Motion panel or the Track View.

After you select one of the constraints from the Animation ⇔ Constraints menu, a dotted link line extends from the current selected object to the mouse cursor. You can select a target object in any of the viewports to apply the constraint. The cursor changes to a plus sign when it is over a target object that can be selected. Selecting a constraint from the Constraints menu also opens the Motion panel, where the settings of the constraint can be modified.

You also can apply constraints using the Assign Controller button found in the Motion panel and in the Track View window.

# Cross-Ref

> Find out more about the Track View window in Chapter 36, “Working with Function Curves in the Track View.”

# Working with the constraints

Each constraint is slightly different, but learning how to use these constraints will help you control the animated objects within a scene. You can apply several constraints to a single object. All constraints that are applied to an object are displayed in a list found in the Motion panel. From this list, you can select which constraint to make active and which to delete. You also can cut and paste between objects.

# Attachment constraint

The Attachment constraint determines an object’s position by attaching it to the face of another object. This constraint lets you attach an object to the surface of another object. For example, you could animate the launch of a rocket ship with booster rockets that are attached with the Attachment constraint. The booster rockets would move along with the ship until the time when they are jettisoned.

The pivot point of the object that the constraint is applied to is attached to the target object. At the top of the Attachment Parameters rollout is a Pick Object button for selecting the target object to attach to. You can use this button to change the target object or to select the target object if the Animation ⇔ Constraints menu wasn’t used. There is also an option to align the object to the surface. The Update section enables you to manually or automatically update the attachment values.

# Note

> **The Attachment constraint shows up in the Position track of the Assign Controller rollout as the Position List controller. To minimize the effect of other controllers, set their Weight values in the Position List rollout to 0.**

The Key Info section of the Attachment Parameters rollout displays the key number and lets you move between the various keys. The Time value is the current key value. In the Face field, you can specify the exact number of the face to attach to. To set this face, click the Set Position button and drag over the target object. The A and B values represent Barycentric coordinates for defining how the object lies on the face. You can change these coordinate values by entering values or by dragging the red cross-hairs in the box below the A and B values. The easiest way to position an object is to use the Set Position button to place the object and then to enhance its position with the A and B values. The Set Position button stays active until you click it again.

The TCB section sets the Tension, Continuity, and Bias values for the constraint. You also can set the Ease To and Ease From values.