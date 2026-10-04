When passing parameters, remember that the different types are actually different. And that means if a function you call it with a different type, it often needs to perform a conversion in order to match the specific signature. Some of these type conversions can be very tricky.

One way to get around this is to make sure you call with floating-point numbers. Any time you write a floating-point literal, you can append an f to the number to indicate that the number should be treated as a float:

# // Program 13_3_ERROR

// Multiple parameter types; Error when trying to use floats due to double

```
#include <iostream>
```

```
using namespace std;
```

```
float average(float a, float b) {
    return (a + b) / 2.0;
}
```

This is the same program from before, now you're calling it with 10.0 and 35.

```
cout << "The average of 10 and 35 is: " << average(10.0, 35.0) << endl;
```

When you compile this code, you will probably find that you get a compiler error, saying that you're trying to make a call to a function average and giving 2 doubles as parameters.

```
cout << "The average of 10 and 35 is: " << average(10.0f, 35.0f) << endl;
```

The compiler can't figure out if it's better to convert those floats to integers or to convert the int to integers and use the int value of average. It's ambiguous what's wanted, so it won't compile the program.

```
int average(int a, int b) {
    return (a + b) / 2;
}
```

There are similar methods for other types; for example, adding LL after a number ensures that it's treated as a long int int.

Even you thought you had called with floats, floating-point literals are treated as doubles by default.

Now this code will compile and run just fine.