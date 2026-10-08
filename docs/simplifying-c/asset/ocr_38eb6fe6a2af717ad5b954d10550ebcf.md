# ■ Register Variables

The counter-controlled loops require a counter variable now and then to check which iteration of loop is being executed. If the counter variables are stored in the primary memory, the access to these variables becomes slow. To have fast access to variables, we can store the variables in the CPU registers. C language provides us a storage class called register for the said purpose. The following syntax allows us to define a register storage class for a variable:

```
register data type identifier;
```

For example, the definition register int i_ctr; indicates that the variable i_ctr is of type integer and its storage class is register. The register class variables are accessible only in the region of the function they are defined in. They exist as long as the function is active. The register class variables are assigned garbage value by default. One has to be cautious while using register class variables, as at times the compiler may convert them to automatic class variables and store them in the primary memory. The reason for this conversion is the limitation of a number of CPU registers.

# ■ Static Variables

All the three storage classes discussed till now create temporary variables in the memory. The static storage class variables when defined are made permanent within a specified region. A static storage class variable is stored permanently in the primary memory and, by default, is assigned value zero. The following syntax allows us to define a static storage class for a variable:

```
static data type identifier;
```

For example, the definition static int i_result; indicates that the variable i_result is of type integer and its storage class is static. If used as local variable of a function, these variables are usable within the functions and preserve their previous values held by them between function calls. Table 4 list the major properties of the four storage classes discussed in this chapter:

| **Table 4: Properties of Storage Class Variables** |  |  |  |  |  |
|---|---|---|---|---|---|
| Storage Class | Keyword | Accessibility Range | Existence | Storage Location | Default Value |
| Automatic | auto | Accessible within the block it is defined | From the time of function being invoked till completion of function | Primary memory | Garbage |
| External | extern | Accessible within multiple programs | From the time of function being invoked till completion of program | Primary memory | Zero |
| Register | register | Accessible within the | From the time of function being | CPU register | Garbage |