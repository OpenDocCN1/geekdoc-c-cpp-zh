```
```cpp
T2.displayTime();        // display T2
T2++;                    // increment T2 again
T2.displayTime();        // display T2
return 0;
}
```
```

When the above code is compiled and executed, it produces the following result:

```
```
H: 12 M:0

H: 12 M:1

H: 10 M:41

H: 10 M:42
```
```

# Assignment Operators Overloading

You can overload the assignment operator (=) just as you can other operators and it can be used to create an object just like the copy constructor.

Following example explains how an assignment operator can be overloaded.

```
```cpp
#include <iostream>
using namespace std;

class Distance
{
   private:
      int feet;              // 0 to infinite
      int inches;            // 0 to 12
   public:
      // required constructors
      Distance(){
         feet = 0;
         inches = 0;
      }
      Distance(int f, int i){
         feet = f;
         inches = i;
      }
```
```