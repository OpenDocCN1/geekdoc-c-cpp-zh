```
```
The double value is: 2.1
The int value is: 2
The double value is: 3.8
The int value is: 3
The int value is: 4
```
```

Note that the last two lines show the difference in rounding the value 3.8. In the first case, you see the default `Trunc`, and in the second, you see the effects of `RoundEven`. Discover more about performing numeric conversion using Boost at http://www.boost.org/doc/libs/1_55_0/libs/numeric/conversion/doc/html/index.html.

# Creating Improved Loops Using Foreach

Writing efficient loops is a requirement if you want your application to perform optimally. Interestingly enough, many loops use a certain amount of *boilerplate code* (code that is essentially the same every time you write it, but with small nuances).

![](bbox=[0.135, 0.403, 0.233, 0.465])

Templates and other methodologies described in this book provide a means to overcome the boredom of writing essentially the same code. However, none of the examples to date has shown a tried and true method, *macros*. A *macro* is essentially a substitution technique that replaces a keyword with the boilerplate code you'd normally write. Macros normally appear in uppercase, such as `BOOST_FOREACH`, which is the macro used in this section of the chapter. Instead of typing all the code associated with a macro, you simply type the macro name and the compiler does the rest of the work for you.

![](bbox=[0.135, 0.604, 0.233, 0.668])

The magic behind the `BOOST_FOREACH` macro is that it creates all the iteration code you normally create by hand. In other words, you aren't providing any less code to the compiler; you simply let the macro write it for you. The Boost library still relies on the Standard library `for_each` algorithm; you simply avoid writing all the code you used to write when using the algorithm. You can discover more about the `BOOST_FOREACH` macro at http://www.boost.org/doc/libs/1_55_0/doc/html/foreach.html.

You may recognize the *ForEach* example in Listing 5-4 partially from Listing 6-1 in Book IV, Chapter 6. However, instead of choosing specific items, the example now uses a `BOOST_FOREACH` loop to iterate through the vector.

# **Listing 5-4: Creating a BOOST_FOREACH Loop**

```
```
#include <iostream>
#include <vector>
#include "boost/foreach.hpp"
```
```