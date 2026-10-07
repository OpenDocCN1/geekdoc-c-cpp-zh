# Identifiers With Special Meaning

The C++ language reserves names declared with external linkage in library header files. For functions, this includes the function signature (name and parameter list). For example, suppose you have this code:

```
#include <cmath>
using namespace std;
```

In this case, the function signature tan(double) is reserved. That means your program should not declare a function that has this prototype:

```
int tan(double); // do not do it
```

This doesn't match the library tan() prototype, which returns type double, but it does match the signature. However, it would be okay to have the following prototype:

```
char *tan(char *); // ok
```

That's even though it matches the tan() identifier, it doesn't match the signature.

# Identifiers With Special Meaning

The C++ community is loath to add new keywords because they could conflict with existing code. That is why the standards committee has, for example, repurposed the auto keyword and used more than one for others, such as virtual and delete. C++11 has implemented another to avoid adding keywords, and that is to use identifiers with special meanings. These identifiers, override and final, are not keywords, but they are used to implement language features. The compiler uses the context to determine whether they are used as ordinary identifiers or as language features:

```
class F {
  int final; // #1
public:
  ...
  virtual void unfold(){} = final; // #2
}
```

The final on line #1 is used as an ordinary identifier, and the final on line #2 is used to invoke a language feature. The two uses do not conflict with one another.
Also C++ has many identifiers that commonly appear in programs but that are not reserved. These include header file names, library function names, and main, the name of the required function with execution begins. As long as you avoid namespace conflicts, you can use these identifiers for other purposes, although there is no reason to do so. That is, nothing except a lack of common sense prevents code like the following:

```
// allowable but silly
#include <iostream>
int iostream(int a);
```