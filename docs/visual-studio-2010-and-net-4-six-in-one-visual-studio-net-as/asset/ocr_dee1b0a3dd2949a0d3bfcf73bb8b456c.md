The big advantage of prototype designs is that it ends the user role-play of his her day using the prototype and give feedback if some information is not displayed or hard to reach. Dynamic prototypes are cheap to create and modify, and thus, allow experimenting with different approaches to the UI. Once accepted by the client, prototypes can also serve as part of the developer's specification, showing the general layout, fields to display, and interactivity to implement in a self-explaining way.

SketchFlow is available for both WPF and Silverlight, and using the styling and templating features of these platforms to enable its sketchy flow. End users can view the sketches in the SketchFlow Player. The SketchFlow Player also allows the customer to provide feedback by adding textual comments, and drawing on the sketch UI with the mouse.

# # Triggers, Actions, and Behaviors

Triggers and actions can be thought of as reusable, customizable, designer-friendly event handlers. An action is a piece of .NET that does something — changes a property, a Story, moves around, plays a sound, opens a link — basically anything a piece of code can do. Actions also have parameters that further enhance their usability.

The trigger is the "event" that activates the action. When a specific event occurs, TimerTrigger (fires at specific intervals), and KeyTrigger (fires when a specified key is pressed). There are other triggers available in the Blend Gallery, such as the MouseGestureTrigger that fires when the mouse is moved in a pre-specified way, or a doubleclick trigger.

To apply an action to a piece of UI Blend, the action can be drawn from the Assets panel to the "Objects and Timeline", or the UI itself on the design surface. A trigger is automatically added, but its parameters can be changed, or the entire trigger replaced in the property inspector for the action.

Actions and triggers are attached to a DependencyObject by default. If a trigger or action only makes sense on a specific element (like an action that selects the next or previous item in the ListBox), the action can be changed when specifying the generic class, and Blend will not allow you using it on the wrong element.

Behaviors are used when simple triggers are not enough. Just like an action, it is attached to a target element (AssociatedObject), and provides two methods to override — OnAttached and OnChanged. In these methods, the event can be hooked up to the — AssociatedObject, and basically, any functionality can be done. A good Behavior example is the MouseDragElementBehavior that makes the associated object "draggable" without any further code — it handles the MouseLeftDown, MouseMove, and MouseLeftButtonUp in one single page.

There is no limit to what actions and behaviors can do. You can find a physics engine embedded in behaviors that move UI elements and handle gravity and collision, and one of the built-in Blend samples is a breakout-style game called "Beehive", where the entire logic of the game is coded using triggers, actions, and behaviors.