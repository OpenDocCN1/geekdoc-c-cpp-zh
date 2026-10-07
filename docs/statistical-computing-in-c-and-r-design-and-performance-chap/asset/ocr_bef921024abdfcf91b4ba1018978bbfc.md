# 288 NUMERICAL OPTIMIZATION

```
cout << f2(2.5) << endl;
return 0;
}
```

In the main function of Listing Functor constructor an object is created from the Z class address is passed to the address of the func1 method. The resulting Functor object is then used to call func1. this is accomplished with an overloaded version of () in the Functor struct that makes the process resemble evaluation of an ordinary function in main. The syntax that appears in the body of the () operator seems somewhat complicated at first. But, PZ->pF translates to i) dereference the pointer pF to obtain the actual Z and ii use the pointer pZ to access the method with the member access operator ->. The results would be produced using *pF instead of pZ->pF. Both * and -> are called method dereferencing operators. The sole purpose of the functor struct is to evaluate a class method and should not need nor be able to alter the class object that is used to invoke method. The const designation for the () operator ensures that this is the case.

The output from Listing 8.4 is

+   Calling from Z func1
2
Calling from Z func2

Thus, Functor objects have successfully encapsulated both of the member functions of the Z class.
Simple functions like those in Listings 8.2 and 8.4 can be effective and will suffice for many purposes. Nonetheless, the Functor class in Listing 8.4 is still constrained to work only with the particular class Z. The next step is to allow for both Z and the member function to be arbitrary. Template classes provides the means to attain that end.
Proceeding in Section 3.10, a "general purpose" functor might take the form

```
//funcTemp.h
template <class T> class Functor{

int (T::*pF)(double);
T* pT;

public:
Functor(){
Functor(T pT, int (T::*pF)(double))pT = pt; pf = pf;
int operator() (double u) const {
return (pT->*pF)(u);
}
}
```

# Listing 8.5 funcTemp.h

In the essence of the class Z argument in Listing 8.5 is the same as the generic in Listing 8.4. The only difference is that the program has been replaced with the generic "place-holder" T. The following program was written to test our new Functor class.

```
//functorDriver.cpp
#include <iostream>
#include <cmath>
```

# Listing 8.6 functorDriver.cpp