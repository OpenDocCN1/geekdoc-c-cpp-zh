
The focus of the function module here is to take a certain input and process it to produce a result. OOP shifts the focus to the object. In this example, we define an object that represents a person and then define attributes and methods to store and process the person's BMI.

In this section, we'll look at the defining elements of OOP, including classes, methods, instances and static components, and events.

## 8.1.1 Classes

*Objects* encapsulate data and create functions to manipulate that data. The characteristics (called *attributes*) and functions (called *methods*) of an object are put into one package. The definition of this package is called a *class*. To use objects in a program, classes must be defined, because an object exists as an instance of a class.

A class can be defined as shown in Listing 8.3.

```abap
REPORT ZCA_BMI.
CLASS CL_PERSON DEFINITION.
PUBLIC SECTION.

TYPES ty_packed TYPE p LENGTH 4 DECIMALS 2.
METHODS set_height IMPORTING im_height TYPE ty_packed.
METHODS set_weight IMPORTING im_weight TYPE ty_packed.
METHODS set_bmi.
METHODS get_bmi RETURNING VALUE(r_bmi) TYPE ty_packed.
PRIVATE SECTION.
DATA : bmi TYPE I,
       height TYPE I,
       weight TYPE I.
ENDCLASS.
CLASS CL_PERSON IMPLEMENTATION.
METHOD set_height.
  height = im_height.
ENDMETHOD.
METHOD set_weight.
  weight = im_weight.
ENDMETHOD.
METHOD set_bmi.
  bmi = height / weight.
ENDMETHOD.
METHOD get_bmi.
  r_bmi = bmi.
ENDMETHOD.
ENDCLASS.
```

Components belonging to the protected section can be accessed by the methods of the same class and its subclasses. A *subclass* inherits its components from a parent class. Once a class inherits from a parent class, it can access the public and protected components of the parent class. We'll learn more about encapsulation in Section 8.2.

In Listing 8.3, we defined the CL_PERSON class consisting of HEIGHT, WEIGHT and BMI attributes in the private visibility section. Because these attributes are private, they can't be accessed by external objects or programs directly. To manipulate these attributes, we defined setter and getter methods in the public section of the class. *Setter methods* allow you to set the value of an attribute, and *getter methods* allow you to read the value of an attribute. Defining the attributes in the private section and providing setter and getter methods to manipulate the attributes allows for more control, such as validating the data before changing the state of the object.

For example, we can avoid an invalid value being set for a person's height by validating the input in the SET_HEIGHT method. In the program, we defined two *object reference variables* called JOHN and MARK referring to the CL_PERSON class. An object exists as an instance of a class, and each class can have multiple instances. The object reference variable initially contains an empty value until the object is instantiated using the CREATE OBJECT statement. Once the object is instantiated, the object reference variable contains the reference (pointer) to the object in memory, and the object is accessed using the object reference variable. The object reference variables are also called *reference objects* and are defined using the TYPE REF TO addition.

Unlike in function modules, here each reference object occupies its own memory space and multiple instances of the class can be defined in the program, with each instance working with its own data.

In this section, we'll discuss local and global classes, class parts and components, and the use of visibility in classes.

## Local and Global Classes

As previously discussed, classes can be defined locally in an ABAP program or globally in the system using Class Builder (Transaction SE24). *Local classes* can be used only within the program in which they're defined, whereas *global classes* can be used in any ABAP program. Irrespective of whether the class is defined locally or globally, the syntax to define the class remains the same, as shown in Listing 8.3. Apart from visibility, there is no difference between a local class and a global class. When a class is used in an ABAP program, the system first searches if the class exists locally. If the class isn’t defined locally, then the system looks for a global class.

When defining global classes, we can use the form-based editor of the Class Builder tool to easily define the components of the class and implement the methods without getting into the nitty gritty of the syntax.

Wherever applicable, we will show you the steps to define classes both locally and globally throughout this chapter. Define local classes if the scope of the object is limited to the program and the object may be irrelevant to other programs, but if you plan to use an object in multiple programs, we recommend defining the class globally in Class Builder.

## Class Parts and Components

To break down the code in Listing 8.3 further, a class in ABAP has two sections:

- **Definition section**

  In the definition section, various components of a class, such as attributes, events, and methods, are defined. For example, in Listing 8.3, we defined the attributes and the methods of the class in the definition section of the class. When defining the methods, we also defined the parameter interface for the methods.

  For the sake of simplicity, we haven’t defined any events in Listing 8.3, but if you want to trigger various events to which the methods of the class can respond, you can do so in the definition part of the class. The methods that respond to events are called *event handler methods*. We’ll learn more about defining events and implementing suitable event handler methods in Section 8.1.4.

- **Implementation section**

  The implementation section of the class is where we implement the methods defined in the definition section. The methods are implemented between the `METHOD` and `ENDMETHOD` statements, and each method defined in the definition part must have an implementation in the implementation part of the class.

There are three important types of components available in a class:

- **Methods**

  Methods are used to change the state of an object and manipulate its behavior. For example, in *Listing 8.3*, different methods were implemented in the `CL_PERSON` class to set the height, weight, and BMI of the person. Methods can also be defined as event handler methods that respond to specific events during the runtime of the object. By using setter and getter methods, we can ensure that all attributes of the class are always accessed through its methods, thus guaranteeing data consistency.

- **Attributes**

  Attributes are the internal data fields of a class and store the state of an object. We can change the state of an object by changing the contents of an attribute.

- **Events**

  Events are defined in the definition area of a class and can be raised during the runtime of the object. A suitable event handler method is maintained in the implementation part of the class and is triggered when the corresponding event is raised. Events allow you to call specific methods dynamically during the run-time of the object.

  For example, if you want to perform specific tasks when the user double-clicks an output line, you can maintain a `DOUBLE_CLICK` event, which can be raised on that event. The registered event handler method will be called dynamically when the event is raised.

The components of a class can be categorized as follows:

- **Static components**

  Static components can be accessed directly using the class component selector `=>`. Static components behave similarly to function modules in that only one instance of a static component exists in the program.

- **Instance components**

  Instance components can't be accessed directly using the class name. To access an instance component, you need to define a reference object in the program using `TYPE REF TO` (for example, the objects `JOHN` and `MARK` in *Listing 8.3*) and then access its attributes and methods through the reference object using the object component selector `->`.
