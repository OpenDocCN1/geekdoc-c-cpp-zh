# 274 Modular Design and Functions

The following prototype shows the specification of dummy variable names:
int funsort(int input_int, float length_in_ft, double height_in_ft, char site_id);

The variable names input_int, length_in_ft, height_in_ft, and site_id are dummy names and are optional. The specification of names in the prototype is one way to document function code.

It is standard practice to declare functions at the beginning of the program and implement them after the main function.

# 5.2.2 Function Definition

Every library function must be implemented. A function implementation starts with a function header followed by the function body. The function consists of statements enclosed between left and right braces. The general form of the function header is as follows:

```
return-data-type function-name(list of parameters with their data types)
```

An example written in C code is as follows:

```
int funsort(int id_num, float cost, double quantity, char order_status)
```

A function header match the function prototype as follows:

+   * The return-data-type must match
* The function-name must match
* The number, data types, and order of the parameters must match

The only difference is that

+   * In a prototype there is no need to specify the names of the parameters, only their data types. Specification of names is optional, and they are dummy names, whereas in a function header, in addition to the specification of data types, the local names of the variables must be specified. This declares and defines the parameter variables.
* A prototype ends with a semicolon, whereas a function header does not end with a semicolon as it is followed by the function body in braces.
* A prototype does not define any variables, whereas a function header declares local names for the parameter variables.