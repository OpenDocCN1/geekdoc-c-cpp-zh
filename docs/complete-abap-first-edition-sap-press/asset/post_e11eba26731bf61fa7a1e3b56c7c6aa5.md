
Before the attributes and methods can be accessed through the reference object, the reference object needs to be instantiated using the `CREATE OBJECT` statement, which creates an instance of the class (an object described by the class) in the program.

We’ll discuss static and instance components further in Section 8.1.3.

### Visibility

The components of a class can have different visibility sections, such as public, protected, and private. The visibility is set in the definition part of the class. Component visibility allows for data encapsulation and hiding the implementation from the external world.

Encapsulation is an important concept in OOP, and we’ll discuss visibility further in Section 8.2.

### 8.1.2 Methods

A method can access other components of the same object. To access the attributes and methods of the same class, a special self-reference variable, `me`, is used. Even though the components of the class can be accessed directly from within the methods of the same class, for better readability it’s recommended to use the self-reference variable `me` when accessing the same class components. You can access both static and instance components from within an instance method, whereas you only can access static components from within a static method.

To call a method of the class, we can either use the `CALL METHOD` statement (e.g., `CALL METHOD John->get_bmi`) or use the object component selector and parentheses directly (e.g., `john->get_bmi( )`).

A method can have importing, exporting, changing, and returning parameters. The importing, exporting, and changing parameters behave similarly to the parameters we define in function modules. For example, data is imported through importing parameters and exported through exporting parameters, while changing parameters can be used for both importing and exporting.

The methods that use returning parameters are called *functional methods*. Prior to SAP NetWeaver 7.4, functional methods could only have one returning parameter and no exporting parameters. However, with SAP NetWeaver 7.4, this restriction is lifted. Functional methods are typically used when a result is returned to the caller program that can be directly assigned to a data object in the program.

For example, with the statement `v_bmi = oref->get_bmi( )`, `v_bmi` is the data object, `oref` is the reference object, and `get_bmi` is a method with a returning parameter, the value of which will be assigned to the `v_bmi` variable.

## Inheritance

Often, many objects are different, but similar enough to be put into a single class. For example, animals and humans have heartbeats, so a class may have a `get_heart_beat` method. However, dogs have tail lengths, so should this class also have a `get_tail_length` method? No, we can define another class as a child class (called a *subclass*) of the parent class. This subclass will have all the features of the parent class plus some additional features. This allows you to extend the functionality of your applications while leveraging the existing code.

Let's look at an example. Objects are designed to closely represent real-life objects—such as a printer. A printer may have an external interface, including a paper tray, keypad, and so on, and the basic functionality of the printer is to create a printout. OOP objects can be designed to represent that setup.

Therefore, let's create a class called `printer` with a method called `print`, as shown in Listing 8.4.

```
CLASS PRINTER DEFINITION.
  PUBLIC SECTION.
    METHODS print.
ENDCLASS.

CLASS PRINTER IMPLEMENTATION.
  METHOD print.
    WRITE 'document printed'.
  ENDMETHOD.
ENDCLASS.
```

**Listing 8.4** Parent Class for Printer

This is a basic printer, but what if we want to extend its functionality? For example, if we have a new printer model that has a counter feature to keep track of the number of copies printed, do we have to build all of the printer logic from scratch? No, we can define a subclass, as shown in Listing 8.5, that inherits all the functionality of the basic printer and extends it.

```
CLASS PRINTER_WITH_COUNTER DEFINITION INHERITING FROM PRINTER.
PUBLIC SECTION.
DATA counter TYPE I.
METHODS print REDEFINITION.
ENDCLASS.
CLASS PRINTER_WITH_COUNTER IMPLEMENTATION.
METHOD print.
counter = counter + 1.
CALL METHOD super->print.
ENDMETHOD.
ENDCLASS.
```

**Listing 8.5** Subclass Implementation

In Listing 8.5, the class `PRINTER_WITH_COUNTER` is inherited from the class `printer`. Here, `printer` is the superclass (parent class) and `PRINTER_WITH_COUNTER` is the subclass (child class). This process of a subclass inheriting the traits of a superclass is called *inheritance* in OOP.

Notice the keyword `INHERITING FROM` used in the definition of the class `PRINTER_WITH_COUNTER`. The subclass inherits all the components of the parent class. It will, by default, have all the attributes and methods defined in the parent class. If required, the methods inherited in the subclass can be redefined to add functionality.

In Listing 8.5, the `print` method in the `PRINTER_WITH_COUNTER` subclass is redefined to increment the counter attribute and calls the `print` method of the parent class. This effectively extends the functionality of the method while leveraging the existing functionality provided by the method of the parent class. Because the same `print` method behaves differently in the superclass and subclass, it leads to some interesting behavior called *polymorphism* (meaning *having many forms*), which we’ll discuss in Section 8.4.

Now we have a printer with a counter, and we know that the counter increments by one every time a document is printed. However, what will its initial value be? How do we ensure that the counter always starts from one or any other initial value? These details are sorted out by defining a constructor for the class.

There are two types of constructors:

- **Instance constructor**：An *instance constructor* is a special method called when the object is *instantiated*. The instance constructor is called for each object when it is instantiated.
- **Class constructor**：The *class constructor* is a special method called just once for the whole class in one internal session. A class can have a maximum of one instance and one static constructor. A static constructor can't have any parameters, whereas the instance constructor can have only importing parameters.

By defining importing parameters for the instance constructor, we can ensure that the object is always initialized before any of its attributes or methods are accessed.

Listing 8.6 shows the implementation of the constructor.

```
CLASS PRINTER_WITH_COUNTER DEFINITION INHERITING FROM PRINTER.
PUBLIC SECTION.
DATA counter TYPE I.
METHODS constructor IMPORTING count TYPE I.
METHODS print REDEFINITION.
ENDCLASS.

CLASS PRINTER_WITH_COUNTER IMPLEMENTATION.
METHOD constructor.
CALL METHOD super->constructor.
counter = count.
ENDMETHOD.
METHOD print.
counter = counter + 1.
CALL METHOD super->print.
ENDMETHOD.
ENDCLASS.

START-OF-SELECTION.
DATA oref TYPE REF TO PRINTER_WITH_COUNTER.
CREATE OBJECT oref
EXPORTING
count = 0.
```

**Listing 8.6** Class with Constructor

In Listing 8.6, the constructor method is defined in the definition part of the PRINTER_WITH_COUNTER class with one importing parameter, count. Because the PRINTER_WITH_COUNTER class is a subclass of the printer class, the superclass constructor must be called first in the implementation of the constructor method, even if there's no constructor defined in the superclass. This ensures that all of the superclass components in the inheritance tree are initialized properly. If a constructor is defined in the superclass, it won't be inherited by the subclass. This allows each class in the inheritance tree to have its own constructor in order to initialize its attributes per requirements.

In the example in Listing 8.6, the `count` parameter of the constructor is assigned a value when instantiating the reference object `oref`. The syntax checker will give an error if the constructor's mandatory parameters aren't passed while instantiating the reference object. This ensures that the object is always instantiated properly.

Now, say we have a more advanced printer model that can print multiple copies along with the basic features provided so far. To create this printer, we'll inherit the `PRINTER_WITH_COUNTER` class and add additional functionality, as shown in Listing 8.7.

```
CLASS MULTI_COPY_PRINTER DEFINITION INHERITING FROM PRINTER_WITH_COUNTER.
PUBLIC SECTION.
DATA copies TYPE I.
METHODS set_copies IMPORTING copies TYPE I.
METHODS print REDEFINITION.
ENDCLASS.

CLASS MULTI_COPY_PRINTER IMPLEMENTATION.
METHOD set_copies.
me->copies = copies.
ENDMETHOD.
METHOD print.
DO copies TIMES.
CALL METHOD super->print.
ENDDO.
ENDMETHOD.
ENDCLASS.

START-OF-SELECTION.
DATA oref TYPE REF TO MULTI_COPY_PRINTER.
CREATE OBJECT oref
EXPORTING
count = 0.
oref->set_copies( 5 ).
oref->print( ).
```

**Listing 8.7** Class Extended to Print Multiple Copies

In Listing 8.7, we defined the `MULTI_COPY_PRINTER` class, inheriting from `PRINTER_WITH_COUNTER`. In the `MULTI_COPY_PRINTER` class, we defined a method called
