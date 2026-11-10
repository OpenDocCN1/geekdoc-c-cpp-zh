There are three important types of components available in a class:

+   - **Methods**
+     Methods are used to change the state of an object and manipulate its behavior.
+     For example, in *Listing 8.3*, different methods were implemented in the `CL_PERSON` class to set the height, weight, and BMI of the person. Methods can also be defined as event handler methods that respond to specific events during the runtime of the object. By using setter and getter methods, we can ensure that all attributes of the class are always accessed through its methods, thus guaranteeing data consistency.

+   - **Attributes**
+     Attributes are the internal data fields of a class and store the state of an object.
+     We can change the state of an object by changing the contents of an attribute.

+   - **Events**
+     Events are defined in the definition area of a class and can be raised during the runtime of the object. A suitable event handler method is maintained in the implementation part of the class and is triggered when the corresponding event is raised. Events allow you to call specific methods dynamically during the run-time of the object.
+   
+     For example, if you want to perform specific tasks when the user double-clicks an output line, you can maintain a `DOUBLE_CLICK` event, which can be raised on that event. The registered event handler method will be called dynamically when the event is raised.

The components of a class can be categorized as follows:

+   - **Static components**
+     Static components can be accessed directly using the class component selector `=>`. Static components behave similarly to function modules in that only one instance of a static component exists in the program.

+   - **Instance components**
+     Instance components can't be accessed directly using the class name. To access an instance component, you need to define a reference object in the program using `TYPE REF TO` (for example, the objects `John` and `Mark` in *Listing 8.3*) and then access its attributes and methods through the reference object using the object component selector `->`.