Using templates does have its cost. You risk template code bloat, where the compiler has to generate specialized code for all different types of callbacks, even when it's not required for performance reasons. It also has its limitations: What if you needed say a vector<> of callback functions—a vector<> that is potentially filled with a mixture of function pointers, function objects, and lambda closures?

To cater to these types of scenarios, the <functional> module defines the std::function<> template. With objects of type std::function<> you can store, copy, move, and invoke any kind of function-like entity—be it a function pointer, function object, or lambda closure. The following example demonstrates precisely that:

```
```cpp
// Ex19_08.cpp
// Using the std::function<> template
import <iostream>;
import <functional>;
#include <cmath>       // for std::abs()

// A global less() function
bool less(int x, int y) { return x < y; }

int main()
{
   int a{ 18 }, b{ 8 };
   std::cout << std::boolalpha;  // Print true/false rather than 1/0

   std::function<bool(int,int)> compare;

   compare = less;               // Store a function pointer into compare
   std::cout << a << " < " << b << ": " << compare(a, b) << std::endl;

   compare = std::greater<>{};   // Store a function object into compare
   std::cout << a << " > " << b << ": " << compare(a, b) << std::endl;

   int n{ 10 };                  // Store a lambda closure into compare
   compare = [n](int x, int y) { return std::abs(x - n) < std::abs(y - n); };
   std::cout << a << " nearer to " << n << " than " << b << ": " << compare(a, b);

   // Check whether a function<> object is tied to an actual function
   std::function<void(const int&)> empty;
   if (empty)                    // Or, equivalently: 'if (empty != nullptr)'
   {
      std::cout << "Calling a default-constructed std::function<>?" << std::endl;
      empty(a);
   }
}
```
```

The output looks as follows:

```
```
18 < 8: false
18 > 8: true
18 nearer to 10 than 8: false
```
```