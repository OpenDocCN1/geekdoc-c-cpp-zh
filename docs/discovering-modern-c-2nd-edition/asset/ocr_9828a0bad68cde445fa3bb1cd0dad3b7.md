Click here to view code image

```
pi is 3.14159
pi is 3.141592653589793
```

C++20 In Section 4.3.1, we will show how the precision can be adjusted to the type’s representable number of digits. Instead of the macro `M_PI` or a literal value, in C++20 we can use the `double` constant `std::number::pi` from `<numbers>`.

When we write a table, vector, or matrix, we need to align values for readability. Therefore, we next set the width of the output:

Click here to view code image

```
cout << "pi is " << setw(30) << pi << '\n';
```

This results in

Click here to view code image

```
pi is             3.141592653589793
```

setw changes only the next output while setprecision affects all following (numerical) outputs, like the other manipulators. The provided width is understood as a minimum, and if the printed value needs more space, our tables will get ugly.

We can further request that the values be left aligned, and the empty space be filled with a character of our choice, say, - :

Click here to view code image

```
cout << "pi is " << setfill('-') << left
     << setw(30) << pi << '\n';
```

yielding

Click here to view code image

```
pi is 3.141592653589793----------------
```

Another way of formatting is setting the flags directly. Furthermore, we force the “scientific” notation in the normalized exponential representation:

Click here to view code image

```
cout.setf(ios_base::showpos);
cout << "pi is " << scientific << pi << '\n';
```