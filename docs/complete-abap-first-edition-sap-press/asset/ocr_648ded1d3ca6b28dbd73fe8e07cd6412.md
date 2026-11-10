# SCREEN_OPTIONS

These options allow you to manipulate screen fields, including declaring the input field as a required field or hiding the input field on the selection screen. Using `SCREEN_OPTIONS`, the input field can be displayed as a checkbox, radio button, or dropdown list box.

The following subsections look at the different additions for `SCREEN_OPTIONS`.

# OBLIGATORY

The `OBLIGATORY` addition defines the input field on the selection screen as a required (obligatory) field. The program can't be executed if the obligatory field is empty. The runtime system automatically performs a validation to check if all obligatory fields are filled with input values when the user selects the EXECUTE function `F8` to exit the selection screen. If the obligatory field isn't filled, the user can only use the functions BACK, EXIT, or CANCEL to leave the selection screen.

An example of this addition is as follows:

```
PARAMETERS p_carrid TYPE s_carr_id OBLIGATORY.
```

# NO-DISPLAY

When the `NO-DISPLAY` addition is used, no screen elements are generated for the parameter on the selection screen. This is useful when you want to use the parameter only as part of the interface defined by the selection screen in an executable program that can be supplied with a value by the calling program with the SUBMIT statement. The SUBMIT statement is used to execute an executable program internally from another program.

An example of this addition is as follows:

```
PARAMETERS p_carrid TYPE s_carr_id NO-DISPLAY.
```

# VISIBLE LENGTH vlen

The `VISIBLE LENGTH vlen` addition controls the visible length of a screen field. Here, vlen is entered directly as a positive number. If vlen is less than the length of the parameter and less than the maximum visible length (45), then the input field is displayed as per the length defined in vlen, with movable content. Otherwise, the addition is ignored.