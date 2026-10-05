

```cpp
return d.print(os);
}
// codegolf.stackexchange.com/a/1114/1405
Date(Year year) {
    const int y = year.value();
    int a = y/100 - y/400 - 2;
    int b = 365*y + y/4 - a + 154;
    return Date(Year(y), Month((b/31)+1), Day(b%31));
}
int main(int argc, const char *argv[]) {
    /* Input */
    int number;
    if(argc > 1) {
        number = std::stoi(argv[1]);
    } else {
        std::cin >> number;
    }
    /* Calculation */
    Date date = easter(number);
    /* Output */
    std::cout << "Easter: " << date << "\n";
}
```

**Listing 12.2** Custom types can protect against errors. This is the first step toward that.

When executed, the program asks for a year and then outputs the date of Easter for that year. You can also call the program from the command line with your year:

```
Easter: 2024-03-31
```

The function for calculating Easter is a variation of Carl Friedrich Gauss's algorithm. In his time, this was one of the most important calculations. I will not go into the details of this calculation here. One line is particularly interesting upon inspection:

```cpp
Date date = easter(number);
```

Here, the int number is automatically converted into Year for the parameter of easter. Why this happens and how it works is shown in Section 12.11.3, under "Type Conversion." you will also see whether this is a good idea or not.

## 12.11.1 Using Classes as Values

When working with custom data types, you should treat them no differently than the standard library—and actually differently than built-in types. When using classes and structs, first consider whether there is reason not to use them as if they were an int or similar. Only if there is a good reason not to should you handle the individual case differently.

This means that you should also treat variables of your class as simple values, and the following applies:

- You can assign a completely new value to a variable of your type instead of changing its internal state.
- Prefer passing a variable by value (call-by-value). Only when you are sure should you use references (or pointers).
- Do not hesitate to return your type as a result.

# Value Parameters

In the example, the functions receive their data types as value parameters:

```cpp
ostream& operator<<(ostream& os, Date d);
Date easter(Year year);
```

Both functions only read their parameters and do not want to change them. Two ways to pass parameters in this case are by value and by constant reference.

Passing by value is the safest way to protect your program as it grows from getting confused in a mess of references. Pass a reference, and if the original object no longer exists outside the function, then the program may crash as soon as the reference is used.

The disadvantage is that the variable has to be copied for this. This costs time and memory during program execution. However, you should still prefer this option to protect yourself from hard-to-find errors in a larger project.

An alternative to passing by value is the constant reference. It looks like this in case:

```cpp
ostream& operator<<(ostream& os, const Date& d) {
  return d.print(os); // d is const
}
```

But this now results in an error: d must not be changed because that is exactly what you said with const Date&. However, d.print could change d; at least, that’s how it looks to the compiler. To remedy this, you need to tell the compiler that print does not change the object. To do this, add a const after the method declaration:

```cpp
ostream& print(ostream& os) const;
```

Now the d.print(os) call works—and additionally, you are now also const-correct. I go into all these aspects of const in detail in Chapter 13.

# Returns

If you want to return your new type, just do it. Normally, you do not return a reference—and if you do, it is at most one that you received as a parameter, like os in the following:

```cpp
ostream& Date::print(ostream& os) {
    return os << format("{:02}-{:02}",
        year_.value(), month_.value(), day_.value());
}
```

Never—and I mean never!—return a reference to an object created (nonstatically) within the function or method:

```cpp
Date& firstJanuaryOf(int y) { // returning a nonconst reference is a red flag
    Date result{Year{y}, Month{1}, Day{1}};
    return result; // reference to local variable
}
```

This immediately goes wrong: result is created in this function and will be destroyed upon exit. If you pass the reference to the internal object outside the function, then the reference points to the destroyed object. This is simply wrong.

Therefore, just return the newly created object:

```cpp
Date firstJanuaryOf(int y) {
    Date result{Year{y}, Month{1}, Day{1}};
    return result;
}
```

# Performance

If you are worried that there might be extra copying, I can reassure you: the compiler can avoid a copy in return statements. In most cases, the compiler can still avoid a copy (copy elision).

```cpp
#include <vector>
#include <iostream>

std::vector<int> createData(unsigned size) {
    std::vector<int> result;
    for(int idx=0; idx<size; ++idx) {
        result.push_back(idx);
    }
    return result;
}
```

