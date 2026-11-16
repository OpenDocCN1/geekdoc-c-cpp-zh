# EVENT ELEMENTS

You've probably noticed that routed events are a lot like dependency properties. WPF takes the basic POCO object and adds some additional functionality. It probably won't come as a surprise that the process for creating one is very similar. You need to create the objects involved in a different order, but the components are the same:

| DEPENDENCY PROPERTY | ROUTED EVENT |
| :--- | :--- |
| CLR PROPERTY<br>Accessors must only call GetValue() and SetValue(). | CLR EVENT<br>Accessors must only call AddHandler() and RemoveHandler(). |
| PROPERTY METADATA<br>Describes property to the WPF property system. | EVENTARGS & DELEGATE<br>You can use existing types such as RoutedEventArgs and RoutedEventHandler, or create custom objects if you need to pass additional information to methods that handle your events. |
| CALLBACK METHODS<br>These optional methods are invoked by the property system. | EVENT METHOD<br>This optional method will raise the event. |
| PROPERTY REGISTRATION<br>The call to one of the DependencyProperty.Register...() methods tells the WPF property system to manage the property. | EVENT REGISTRATION<br>The call to one of the EventManager.Register...() methods tells the WPF property system to manage the property. |