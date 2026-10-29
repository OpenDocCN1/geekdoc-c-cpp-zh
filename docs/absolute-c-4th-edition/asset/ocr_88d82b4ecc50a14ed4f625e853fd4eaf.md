Assuming that the value of the pointer variable p has not changed (so it still points to the same dynamic variable), how can you destroy this new dynamic variable and return the memory it uses to the freestore manager so that the memory can be reused to create other new dynamic variables?

7. Write a definition for a type called NumberPtr that will be the type for pointer variables that hold pointers to dynamic variables of type double. Also, write a declaration for a pointer variable called myPoint, which is of type NumberPtr.

8. Describe the action of the new operator. What does the new operator return? What are the indications of errors?

# TYPE DEFINITIONS

You can assign a name to a type definition and then use the type name to declare variables. This is done with the keyword typedef. These type definitions are normally placed outside the body of the main part of your program and outside the body of other functions, typically near the start of a file. That way the typedef is global and available to your entire program. We will use type definitions to define names for pointer types, as shown in the example below.

# SYNTAX

```
typedef Known_Type_Definition New_Type_Name;
```

# EXAMPLE

```
typedef int* IntPtr;
```

The type name IntPtr can then be used to declare pointers to dynamic variables of type int, as in the following example:

```
IntPtr pointer1, pointer2;
```

# POINTERS AS CALL-BY-VALUE PARAMETERS

When a call-by-value parameter is of a pointer type, its behavior can occasionally be subtle and troublesome. Consider the function call shown in Display 10.4. The parameter temp in the function sneaky is a call-by-value parameter, and hence it is a local variable. When the function is called, the value of temp is set to the value of the argument p and the function body is executed. Since temp is a local variable, no changes to temp should go outside the function sneaky. In particular, the value of the pointer variable p should not be changed. Yet the sample dialogue makes it look like the value of the pointer variable p has changed. Before the call to the function sneaky, the value of *p was 77, and after the call to sneaky the value of *p is 99. What has happened?