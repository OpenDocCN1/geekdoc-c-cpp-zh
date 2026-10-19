C or C++ or the equivalent in another language. Here’s how you’d set up the type definition in C++:

```
**C++ Example of Creating a Type**
```cpp
typedef float Coordinate;  // for coordinate variables
```
```

This type definition declares a new type, *Coordinate*, that’s functionally the same as the type float. To use the new type, you declare variables with it just as you would with a predefined type such as *float*. Here’s an example:

```
**C++ Example of Using the Type You’ve Created**
```cpp
Routine1( ... ) {
    Coordinate latitude;     // latitude in degrees
    Coordinate longitude;    // longitude in degrees
    Coordinate elevation;    // elevation in meters from earth center
    ...
}
...

Routine2( ... ) {
    Coordinate x;    // x coordinate in meters
    Coordinate y;    // y coordinate in meters
    Coordinate z;    // z coordinate in meters
    ...
}
```
```

In this code, the variables *latitude*, *longitude*, *elevation*, *x*, *y*, and *z* are all declared to be of type *Coordinate*.

Now suppose that the program changes and you find that you need to use double-precision variables for coordinates after all. Because you defined a type specifically for coordinate data, all you have to change is the type definition. And you have to change it in only one place: in the *typedef* statement. Here’s the changed type definition:

```
**C++ Example of Changed Type Definition**
```cpp
typedef double Coordinate;  // for coordinate variables
```
```

![](bbox=[0.058, 0.713, 0.243, 0.748])

Here’s a second example—this one in Pascal. Suppose you’re creating a payroll system in which employee names are a maximum of 30 characters long. Your users have told you that no one ever has a name longer than 30 characters. Do you hard-code the number 30 throughout your program? If you do, you trust your users a lot more than I trust mine! A better approach is to define a type for employee names:

```
**Pascal Example of Creating a Type for Employee Names**
```pascal
Type
    employeeName = array[ 1..30 ] of char;
```
```