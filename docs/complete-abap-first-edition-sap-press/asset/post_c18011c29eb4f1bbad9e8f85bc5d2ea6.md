
```
METHODS trigger_event.
METHODS on_double_click FOR EVENT double_click OF cl_events_demo
  IMPORTING
    column
    row
    sender.
METHODS on_right_click FOR EVENT right_click OF cl_events_demo.
ENDCLASS.
CLASS cl_events_demo IMPLEMENTATION.
  METHOD trigger_event.
    RAISE EVENT double_click
      EXPORTING
        column = 4
        row    = 5.
    RAISE EVENT right_click.
  ENDMETHOD.
  METHOD on_double_click.
    WRITE: / 'Double click event triggered at column', column,
             'and row', row.
  ENDMETHOD.
  METHOD on_right_click.
    WRITE: / 'Right click event triggered'.
  ENDMETHOD.
ENDCLASS.
DATA oref TYPE REF TO cl_events_demo.
START-OF-SELECTION.
  CREATE OBJECT oref.
  SET HANDLER oref->on_double_click FOR oref. "Instance event
  SET HANDLER oref->on_right_click. "Handler for Static event
  CALL METHOD oref->trigger_event( ).
```

**Listing 8.12** Defining Events

In the implementation part of the class, the `trigger_event` method uses the RAISE EVENT statement to trigger the `double_click` and `right_click` events. Because the `double_click` event contains defined exporting parameters, this method exports certain values to the event handler method. The `on_double_click` method imports the values that were exported by the trigger method. In the program code, the events are registered using the SET HANDLER statement, and the code in the event handler methods is executed when the `trigger_event` method is called.

In this section, we introduced the basics of OOP, including classes, methods, instance and static components, and event. Working with objects simplifies the implementation of functionality. OOP concepts provide many advantages compared to procedural programming techniques. Programs developed using OOP techniques are easy to maintain and, if designed well, should be easy to enhance.

Now that you've been introduced to the basics of OOP, in the next few sections we'll discuss some of the characteristics of this kind of programming, beginning with the process of encapsulation.

## 8.2 Encapsulation

In procedural programming, developers generally use a technique called *functional decomposition* for application development design. In functional decomposition, the series of steps that the application needs to perform are identified from the functional requirements, and procedures are developed for each step. In other words, complex business requirements are broken down into smaller, easy to understand steps. Once all the procedures are in place, they are composed into the main program, which calls the procedures in a fixed order and passes the relevant data to each procedure.

For example, if you want to develop software for an ATM machine, then the requirements can be broken down into smaller steps, such as reading a card, verifying its PIN, dispensing cash, and so on. Modules can then be developed separately for each of these steps, such as one module to read the card, another module to validate the PIN, another module to verify the account balance and dispense cash, and so on. These modules can then be combined to form the overall application. By breaking down the requirements into smaller steps that are easy to understand and maintain, this approach makes it easy to develop small- to medium-sized applications.

However, because procedures (function modules or subroutines) don't have their own data environment, they're dependent on the main program to supply the data each time a procedure is called, or they must work with the global data of the program. This makes the procedures tightly coupled with the main program. As the application branches out and becomes more and more complex, it may lead to maintenance headaches.

For example, if many procedures are manipulating the global data, we can't be sure if the application will behave in a predictable way if the sequence of procedure calls is changed for any future enhancements. By depending entirely on the main program to supply the required data each time the procedure is called, the interface will soon be cluttered, and it makes the procedure too restrictive to work in other environments. The developer of the procedure depends too much on the external application, over which he has no control. It also becomes difficult to develop loosely coupled procedures that can work seamlessly for future enhancements. In addition, once the procedure is developed, the developer can't change the parameter interface for future enhancements without breaking existing applications that call the procedure.

In OOP, because objects have their own data environment, they can be made smart enough to make their own decisions without too much dependency on external applications.

*Encapsulation* in OOP allows you to define boundaries and hide implementation from the external world. The term *encapsulation* means that the attributes (data) and the methods (functions) that manipulate the data are enclosed in a capsule (object). This means that we can set a boundary between what can be accessed from within the object and from the outside world. This boundary helps to address many of the issues mentioned previously regarding procedures.

In this section, we'll discuss some of the characteristics of encapsulation in OOP. We'll look at component visibility, the different visibility sections, friendship between classes, and implementation hiding.

### 8.2.1 Component Visibility

As shown back in Listing 8.7, the component of an object can be accessed from an *external program* or from a *subclass* or from within the class. The access restriction on a component of a class is what defines its visibility. In other words, we can decide if the component of a class can be accessed only from within the class or its subclasses or from external programs.

Back in Listing 8.10, we defined sections (PUBLIC SECTION, PRIVATE SECTION) under which components are declared. These sections are called *visibility sections*. There are three visibility sections: *public, protected,* and *private*.

The visibility section identifies how the component of a class can be accessed. The following list defines the different visibility sections:

- **Public section**
  The components in the *public section* can be accessed from within the class and outside of the class. These components form the public interface of the class.
- **Protected section**
  The components in the *protected section* can be accessed only from within the class and its subclasses (child classes). These components can’t be accessed from external programs.
- **Private section**
  The components in the *private section* can be accessed only from within the class and its friend classes (we'll discuss friend classes in Section 8.2.2).

Listing 8.13 shows an example of the visibility sections.

```text
CLASS cl_encapsulation_demo DEFINITION.
  PUBLIC SECTION.
    METHODS print.
    METHODS set_copies IMPORTING copies TYPE i.
    METHODS get_counter EXPORTING counter TYPE i.
  PROTECTED SECTION.
    METHODS reset_counter.
  PRIVATE SECTION.
    DATA copies TYPE i.
    DATA counter TYPE i.
    METHODS reset_copies.
ENDCLASS.
CLASS cl_encapsulation_demo IMPLEMENTATION.
  METHOD print.
    "Business logic goes here
  ENDMETHOD.
  METHOD set_copies.
    "Business logic goes here
    me->copies = copies.
  ENDMETHOD.
  METHOD get_counter.
    "Business logic goes here
    counter = me->counter.
  ENDMETHOD.
  METHOD reset_counter.
    "Business logic goes here
    CLEAR counter.
  ENDMETHOD.
  METHOD reset_copies.
    "Business logic goes here
    CLEAR copies.
  ENDMETHOD.
ENDCLASS.
CLASS cl_encapsulation_sub_demo DEFINITION INHERITING FROM cl_encapsulation_demo.
  PROTECTED SECTION.
    METHODS reset_counter REDEFINITION.
ENDCLASS.
CLASS cl_encapsulation_sub_demo IMPLEMENTATION.
  METHOD reset_counter.
    super->reset_counter( ).
*   super->reset_copies( ). "gives syntax error
  ENDMETHOD.
ENDCLASS.
```

**Listing 8.13** Implementing Visibility Sections

The code in Listing 8.13 implements the `cl_encapsulation_demo` class, and the `cl_encapsulation_sub_demo` class is defined as a subclass of `cl_encapsulation_demo`. The code shows the syntax to implement visibility sections. Notice the order of implementation of the visibility sections: First, public components are defined, then protected components, and finally private components. This declaration order can't be changed.

In Listing 8.13, the `cl_encapsulation_sub_demo` subclass can access only the public and protected components of its superclass, `cl_encapsulation_demo`. If the `cl_encapsulation_sub_demo` class tries to access the private components of its superclass, the attempt will result in a syntax error. Note that when redefining a method of the superclass in a subclass, the visibility section of the method can't be changed. For example, if the method is defined in the protected section of the superclass, then the method should be redefined in the protected section of the subclass.

Figure 8.1 shows the visibility set in Class Builder for global classes.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_327_0.png)

**Figure 8.1** Visibility Using Class Builder

With visibility sections, clear boundaries can be defined so that only the required components of an object are exposed to the outside world. This arrangement
