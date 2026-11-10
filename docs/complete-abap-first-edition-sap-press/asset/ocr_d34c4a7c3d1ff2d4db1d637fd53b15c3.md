```
```text
*"      REFERENCE(BMI) TYPE I
BMI = WEIGHT / HEIGHT.
ENDFUNCTION.
```
```

# Listing 8.1 Example Function Module to Calculate BMI

Listing 8.2 shows the call to the function module `zcalculate_bmi` that we defined in Listing 8.1.

```
```text
REPORT ZCA_BMI.
DATA : v_bmi TYPE I.
PARAMETERS: p_height TYPE I.
            p_weight TYPE I.

CALL FUNCTION 'ZCALCULATE_BMI'
EXPORTING
    height = p_height
    weight = p_weight
IMPORTING
    bmi = v_bmi.
WRITE: 'Your BMI is', v_bmi.
```
```

# Listing 8.2 Program to Calculate BMI

When the function module is called in the program, the whole function group to which this function module belongs is loaded into the memory (internal session) the main program is assigned to. Each subsequent call to this function module in the program will access the existing instance in the memory as opposed to loading a new instance.

When a function module is called in a program, one instance of it is created in the internal session in which the program runs, and each subsequent call to this function module from the program will point to the existing instance that was previously loaded into the internal session. You can't have multiple instances of the same function module within the same internal session.

If you call the `zcalculate_bmi` function module in the program to calculate the BMI of multiple persons, there's no way for the function module to be aware of the person for which the BMI is calculated. You can define a global variable in the function group to store a person's name so that other function modules of the function group can use this information, but it's easy to lose track of all these variables in the code—and even then, this design can only support one person at a time in the application.