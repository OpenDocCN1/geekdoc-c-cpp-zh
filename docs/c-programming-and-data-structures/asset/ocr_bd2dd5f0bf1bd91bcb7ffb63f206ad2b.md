The enumerated variables v1, v2, ... vn can only have one of the values value1, value2, ... value n. The assignments of the following types are valid:

```
v1 = value3;
v5 = value1;
```

# An example:

```
enum day {Monday, Tuesday, ... Sunday};
enum day week_st, week_end;
week_st = Monday;
week_end = Friday;
if(week_st == Tuesday)
week_end = Saturday;
```

The compiler automatically assigns integer digits beginning with 0 to all the enumeration constants. That is, the enumeration constant value1 is assigned 0, value2 is assigned 1, and so on. However, the automatic assignments can be overridden by assigning values explicitly to the enumeration constants. For example:

```
enum day {Monday = 1, Tuesday, ... Sunday};
```

Here, the constant Monday is assigned the value of 1. The remaining constants are assigned values that increase successively by 1.

The definition and declaration of enumerated variables can be combined in one statement. Example:

```
enum day {Monday, ... Sunday} week_st, week_end;
```

# 1.33 DECLARATION OF STORAGE CLASS

Variables in C can have not only data type but also storage class that provides information about their location and visibility. The storage class decides the portion of the program within which the variables are recognized. Consider the following example:

```
/* Example of storage classes */
int m;
main()
{
  int i;
  float balance;
  ....
  ....
  function1();
}
function1()
{
  int i;
  float sum;
  ....
  ....
}
```

The variable m which has been declared before the main is called global variable. It can be used in all the functions in the program. It need not be declared in other functions. A global variable is also known as an external variable.

The variables i, balance and sum are called local variables because they are declared inside a function. Local variables are visible and meaningful only inside the functions in which they are declared. They are not