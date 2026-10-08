
![](img/b5597c749e848b27b0d305153ae16106_410_0.png)

The design surface will be read-only until the problem is corrected. While the XAML can still be edited, this effectively renders the designer unable to work with the project. Ensuring that the visual designers and Blend always call blendability. There are other cases when run-time and design time behave differently. For example, neither Binder nor Coder the constructor of the UserControl is displayed. Therefore, some properties may not be set in design mode.

To differentiate between design and run time, developers can use the DesignerProperties.IsDesignMode Boolean property. If this value is true the design code can be switched to a design-time behavior, and provide dummy data in the data object, instead of trying to reach a live database. This dummy data can be used by the designer to set up bindings in a what-you-see-is-what-you-get (WYSIWYG) manner.

## Design Time Sample in Blend

Designers do not have to rely on developers to create sample data for their bindings or to experiment with different ways of presenting data. Blend offers a featured called sample data. This is essentially an XML "database" that can be created visually in Blend, and used as a data-binding source with simple drag-and-drop operations.

The cool thing about sample data is that the number of records can be changed very easily, and there are tons of built-in sample data types that create random lorem ipsum text, company names, person names, prices, email addresses, images, and so on. Figure 8-49 shows how design-time data is used in Blend to create a list of charts with designer's names and prices.

![](img/b5597c749e848b27b0d305153ae16106_411_0.png)

FIGURE 8-49: Using sample data in Blend

The sample data can also be used as a real data source for simple applications or parts of an application that displays some data but do not need server functionality. The sample “database” can be set up, and then the randomly generated data can be changed manually.

## SketchFlow

SketchFlow is a prototyping tool, built into Expression Blend (Figure 8-50). Dynamic prototypes are much more than wireframes that most developer use to mock-up screens. Prototypes are interactive, can contain sample (or even data), and have the navigation functionality in place.

![](img/b5597c749e848b27b0d305153ae16106_411_1.png)

FIGURE 8-50: Editing SketchFlow prototypes in Expression Blend. The design of the UI intentionally looks like a paper drawing to direct the attention to the content and layout, instead of the subtle things like shades of color and precise placement.

The big advantage of prototype designs is that it ends the user role-play of his her day using the prototype and give feedback if some information is not displayed or hard to reach. Dynamic prototypes are cheap to create and modify, and thus, allow experimenting with different approaches to the UI. Once accepted by the client, prototypes can also serve as part of the developer's specification, showing the general layout, fields to display, and interactivity to implement in a self-explaining way.

SketchFlow is available for both WPF and Silverlight, and using the styling and templating features of these platforms to enable its sketchy flow. End users can view the sketches in the SketchFlow Player. The SketchFlow Player also allows the customer to provide feedback by adding textual comments, and drawing on the sketch UI with the mouse.

## Triggers, Actions, and Behaviors

Triggers and actions can be thought of as reusable, customizable, designer-friendly event handlers. An action is a piece of .NET that does something — changes a property, a Story, moves around, plays a sound, opens a link — basically anything a piece of code can do. Actions also have parameters that further enhance their usability.

The trigger is the "event" that activates the action. When a specific event occurs, TimerTrigger (fires at specific intervals), and KeyTrigger (fires when a specified key is pressed). There are other triggers available in the Blend Gallery, such as the MouseGestureTrigger that fires when the mouse is moved in a pre-specified way, or a doubleclick trigger.

To apply an action to a piece of UI Blend, the action can be drawn from the Assets panel to the "Objects and Timeline", or the UI itself on the design surface. A trigger is automatically added, but its parameters can be changed, or the entire trigger replaced in the property inspector for the action.

Actions and triggers are attached to a DependencyObject by default. If a trigger or action only makes sense on a specific element (like an action that selects the next or previous item in the ListBox), the action can be changed when specifying the generic class, and Blend will not allow you using it on the wrong element.

Behaviors are used when simple triggers are not enough. Just like an action, it is attached to a target element (AssociatedObject), and provides two methods to override — OnAttached and OnChanged. In these methods, the event can be hooked up to the — AssociatedObject, and basically, any functionality can be done. A good Behavior example is the MouseDragElementBehavior that makes the associated object "draggable" without any further code — it handles the MouseLeftDown, MouseMove, and MouseLeftButtonUp in one single page.

There is no limit to what actions and behaviors can do. You can find a physics engine embedded in behaviors that move UI elements and handle gravity and collision, and one of the built-in Blend samples is a breakout-style game called "Beehive", where the entire logic of the game is coded using triggers, actions, and behaviors.

## Model-View-ViewModel Pattern

Even though Behaviors can be used to do amazing things, it is probably not the best architectural pattern to follow for building applications that need total designer-developer separation. An emerging pattern, called Model-View-ViewModel (MVVM) seems to be the ideal solution. Blend itself is built with MVVM, as well as tons of other WPF and Silverlight projects.

MVVM may sound familiar — it has a lot to do with the Model-View-Controller (MVC) pattern. MVVM is designed to take full advantage of the advanced-data binding capabilities of WPF and Silverlight. Following are the goals of the MVVM pattern:

- Separate logic and data from presentation
- Make the UI testable by itself
- Avoid spreading UI logic into many, hard-to-find places (such as event handlers of user controls)

Following are the main components of MVVM:

- Model — The represents business data (such as books, authors, orders, and so on). In implementations, the Model also “knows” how to send itself back to the server, or retrieve whatever model objects
- View — The is essentially the UI. In case of WPF and Silverlight, it is the XAML code. MVVM insists on no code-behind for the View — UI-specific coding should be done with behaviors. However, sometimes it is more efficient and cost-effective to put some code in the code-behind, but you have to know and understand the rules to use when to break them.
- ViewModel — The data that represents the View. It connects the View with the Model, showing the status of the View (such as whether the user has logged in). The ViewModel is wired to the View via data binding — the ViewModel is set as the DataContext in XAML. The View can inform the ViewModel of events via a loose commanding mechanism. For example, if the user clicks the “Delete” button, a command is invoked.

There are a lot of different MVVM approaches and implementations to be found on the web — probably many to decide which one to use. Some work with WPF, some prefer Silverlight, and work with both. They all have strengths and weaknesses. Following are some recommendations, but feel free to find (or even create) your own preferred frameworks:

- Laurent Bugion’s MVVM Light Toolkit (http://www.galaso.ch/mvvm/started)
- Microsoft’s Patterns and Practices Group develops Prism, that also helps with composite applications (http://msdn.microsoft.com/en-us/library/dd458809.aspxv2.1)
- Calburn (http://www.codplex.com/calburn) with additional UI patterns
- Silverlight FX (http://projects.nikhil.net/SilverlightFX) also goes beyond MVVM
