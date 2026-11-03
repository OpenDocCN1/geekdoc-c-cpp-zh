# Creating a constant type

Once an enumerated sequence is declared it can be considered to be like a new data type in its own right, with properties of its specified constant names and their associated values.

Variables of this enum data type can be declared in the same way that variables are declared of other data types – using this syntax:

```
data-type variable-name ;
```

The example here created an enumerated sequence named SNOOKER, which can be regarded as a data type of enum SNOOKER. So a variable named “pair” of that data type can be created with the declaration enum SNOOKER pair ; and can store values of the enumeration set defined by that type.

To explicitly assign an integer value to a variable of an enumerated data type, the C standard recommends that a cast be used to convert the int data type to the enum data type, like this:

```
pair = ( enum SNOOKER ) 7 ;
```

In practice this is not needed though, as enumerated values are always integers so are equivalent to the int data type.

An enum declaration can optionally also create a variable by specifying a variable name after the final brace. For example, the declaration enum BOOLEAN { FALSE , TRUE } flag ; defines an enum data type and creates a variable named “flag” of that type.

Custom data types can be defined using the typedef keyword and this syntax:

```
typedef definition type-name ;
```

Declaration of custom data types can help make the program code more concise. For example, where a program uses a number of unsigned short int variables it would be useful to first create a custom data type with those modifiers, using this declaration:

```
typedef unsigned short int USINT ;
```