# Additional Details About Structures

We should mention that you have some flexibility in defining a structure. First, you can declare a variable to be of a particular structure type at the same time that the structure is defined. You do this simply by including the variable name(s) before the terminating semicolon of the structure definition. For example, the following statement defines the structure date and also declares the variables todaysDate and purchaseDate to be of this type:

```
struct date
{
  int month;
  int day;
  int year;
  todaysDate, purchaseDate;
```

You can also assign initial values to the variables in the normal fashion. Thus, the following defines the structure date and the variable todaysDate with initial values as indicated:

```
struct date
{
  int month;
  int day;
  int year;
} todaysDate = { 9, 25, 2011 };
```

If all the variables of a particular structure type are defined when the structure is defined, you can commit the structure name. So the following statement defines an array dates to consist of 100 elements:

```
struct
{
  int month;
  int day;
  int year;
} dates[100];
```

Each element is a structure containing three integer members: month, day, and year. Because you did not supply a name to the structure, the only way to subsequently declare variables of the same type is to explicitly define the structure again.

# Bit Fields

Two methods in Objective-C can pack information together. One way is to simply represent the data inside an integer and access the desired bits of the integer using the bit operators described in Chapter 4, "Data Types and Expressions."

Another way is to define a structure of packed information using an Objective-C structure known as a bit field. This method uses a special syntax in the structure definition that enables you to define a field of bits and assign a name to that field.