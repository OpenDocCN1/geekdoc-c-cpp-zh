```
```cpp
cout << "0.1*0.1: " << x << "\\n";
// Output: 0.01000000000000000019428903
if(x == 0.01) {        // never compare double with ==
    cout << "Yes! x == 0.01" << "\\n";
} else {
    cout << "Uh-oh! x != 0.01" << "\\n";        // you see this output
}
// Attention especially when comparing with 0.0
double null = x - 0.01;
cout << "null: " << null << "\\n";
// Output: null: 0.0000000000000017347235
if(std::fabs(null) < 0.00000001) {                  // compare with an "epsilon"
    cout << "Yes! null is close to 0.0" << "\\n";  // you see this output
} else {
    cout << "Uh-oh! null not close to 0.0" << "\\n";
}
// fractions of powers of 2 are less critical
double y = 0.5 * 0.5;
cout << "0.5*0.5: " << y << "\\n";
// Output: 0.5*0.5: 0.250000000000000000000000000
if(y == 0.25) {       // here the dangerous comparison works exceptionally
    cout << "Yes! y == 0.25" << "\\n";              // you see this output
} else {
    cout << "Oh-oh! y != 0.25" << "\\n";
}
//
return 0;
}
```
```

**Listing 4.32** “double” cannot always store numbers exactly. Calculating and comparing with “==” is an error.

> > **Do Not Compare Floating-Point Numbers with ==**
> >
> > Because none of the floating-point types, float, double, and long double, can store all numbers exactly, you should never test for equality by using ==. Instead, calculate the difference and check whether the result is close to zero. For example, if you want to know whether the two double values a and b are “almost equal,” you can check this in this way:
> >
> > ```cpp
> > if( fabs(b-a)<0.0001 )...
> > ```
> >
> > The fabs() function determines the absolute value (it makes it positive) and is located in the <cmath> header. For 0.0001, use an epsilon that suits your application.