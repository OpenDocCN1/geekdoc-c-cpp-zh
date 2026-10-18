```
```cpp
// Uses iostream:
void DayOfYear::output()
{
    cout << "month = " << month
         << ", day = " << day << endl;
}
```
```

The class definition for the example class DayOfYear above is given in Display 10.3, where month and day are defined as the names of member variables for the class DayOfYear. Note that month and day are not preceded by an object name and dot.

# The Dot Operator and the Scope Resolution Operator

Both the dot operator and the scope resolution operator are used with member names to specify what thing they are members of. For example, suppose you have declared a class called DayOfYear and you declare an object called today as follows:

```
```cpp
DayOfYear today;
```
```

You use the **dot operator** to specify a member of the object today. For example, output is a member function for the class DayOfYear (defined in Display 10.3), and the following function call will output the data values stored in the object today:

```
```cpp
today.output();
```
```

You use the **scope resolution operator ::** to specify the class name when giving the function definition for a member function. For example, the heading of the function definition for the member function output would be as follows:

```
```cpp
void DayOfYear::output()
```
```

Remember, the scope resolution operator :: is used with a class name, whereas the dot operator is used with an object of that class.