As shown previously, you can also use the `string` type in the function `readCourses` to input a value in a variable of type `courses`. We leave the details as an exercise.

The following function outputs an enumeration type value:

```
```cpp
void printEnum(courses registered)
{
    switch (registered)
    {
    case ALGEBRA:
        cout << "Algebra";
        break;
    case ANALYSIS:
        cout << "Analysis";
        break;
    case BASIC:
        cout << "Basic";
        break;
    case CHEMISTRY:
        cout << "Chemistry";
        break;
    case CPP:
        cout << "CPP";
        break;
    case HISTORY:
        cout << "History";
        break;
    case PYTHON:
        cout << "Python";
        break;
    case PHILOSOPHY:
        cout << "Philosophy";
        break;
    }//end switch
}//end printEnum
```
```

# Declaring Variables When Defining the Enumeration Type

In previous sections, you first defined an enumeration type and then declared variables of that type. C++ allows you to combine these two steps into one. That is, you can declare variables of an enumeration type when you define an enumeration type. For example, the statement:

```
```cpp
enum grades {A, B, C, D, F} courseGrade;
```
```

defines an enumeration type, `grades`, and declares a variable `courseGrade` of type `grades`.

Similarly, the statement:

```
```cpp
enum coins {PENNY, NICKEL, DIME, HALFDOLLAR, DOLLAR} change, usCoins;
```
```

defines an enumeration type, `coins`, and declares two variables, `change` and `usCoins`, of type `coins`.