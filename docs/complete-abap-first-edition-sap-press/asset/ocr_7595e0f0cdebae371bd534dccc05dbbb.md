# **TYPE vs. LIKE**

TYPE is used to refer to an elementary data type, local data type in a program, or data type in ABAP Data Dictionary. LIKE is used to refer to another data object in the program.

To support backward compatibility, it's still possible to use LIKE to refer to an ABAP Data Dictionary table or flat structure; however, this usage is obsolete and should be avoided.

# *LIKE (name)*

The LIKE (name) addition allows you to supply the field reference dynamically. name expects a flat character data object containing the name of a component in a flat structure from ABAP Data Dictionary in uppercase. The parameter is created internally with data TYPE c and LENGTH 132, but it's displayed on the selection screen with a length, field label, input help, and field help as per the data type specified in name.

Listing 6.3 shows an example of dynamically assigning the data type for the input field. In this example, we're passing the field name SCO_L_FLIGHT_MEAL-CARRID at runtime. The statement `comp = 'SCO_L_FLIGHT_MEAL-CARRID'` in the example is executed before the selection screen is called because it's maintained under the `AT SELECTION-SCREEN OUTPUT` event. The ABAP runtime environment triggers various selection screen events that we can maintain in the program to process selection screens.

You'll learn about various selection screen events in detail in Chapter 14.

```
```
DATA comp TYPE c LENGTH 30.
PARAMETERS p_dyn LIKE (comp).
AT SELECTION-SCREEN OUTPUT.
  comp = 'SCO_L_FLIGHT_MEAL-CARRID'.
```
```

**Listing 6.3** Dynamically Assigning Data Type for Input Field

In Listing 6.3, the keyword `AT SELECTION-SCREEN OUTPUT` defines an event that ensures the code under it is executed before the selection screen is called. Because this event is triggered before showing the selection screen to the user, we can make use of it to dynamically assign the properties to the selection screen field.

We'll explore all the program events in Chapter 7.