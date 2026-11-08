You use the `setprecision` manipulator with `cout` and the insertion operator. For example, the statement:

```
    cout << setprecision(2);
```

formats the output of decimal numbers to two decimal places until a similar subsequent statement changes the precision. Notice that the number of decimal places, or the precision value, is passed as an argument to `setprecision`.

To use the manipulator `setprecision`, the program must include the header file `iomanip`. Thus, the following include statement is required:

```
    #include <iomanip>
```

# ### fixed Manipulator

To further control the output of floating-point numbers, you can use other manipulators. To output floating-point numbers in a fixed decimal format, you use the manipulator `fixed`. The following statement sets the output of floating-point numbers in a fixed decimal format on the standard output device:

```
    cout << fixed;
```

After the preceding statement executes, all floating-point numbers are displayed in the fixed decimal format until the manipulator `fixed` is disabled. You can disable the manipulator `fixed` by using the stream member function `unsetf`. For example, to disable the manipulator `fixed` on the standard output device, you use the following statement:

```
    cout.unsetf(ios::fixed);
```

After the manipulator `fixed` is disabled, the output of the floating-point numbers returns to their default settings. The manipulator `scientific` is used to output floating-point numbers in scientific format.

> > **NOTE**
> >
> > On some compilers, the statements `cin>>fixed;` and `cin>>scientific;` might not work. In this case, you can use `cin.setf(ios::fixed);` in place of `cin>>fixed;` and `cin.setf(ios::scientific);` in place of `cin>>scientific;`.

The following example shows how the manipulators `scientific` and `fixed` work without using the manipulator `setprecision`.

# **EXAMPLE 3-10**

```
    //Example: scientific and fixed

    #include <iostream>

    using namespace std;
```