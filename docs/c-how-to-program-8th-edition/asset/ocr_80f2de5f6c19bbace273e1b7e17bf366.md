# Mechanical Demonstration of a mutable Data Member

Figure 24.2 demonstrates using a mutable member. The program defines class Test-Mutable (lines 7–21), which contains a constructor, function getValue and a private data member value that’s declared mutable. Lines 15–18 define function getValue as a const member function that returns a copy of value. Notice that the function increments mutable data member value in the return statement. Normally, a const member function cannot modify data members unless the object on which the function operates—i.e., the one to which this points—is cast (using const_cast) to a non-const type. Because value is mutable, this const function can modify the data.

```
```cpp
// Fig. 24.2: fig24_02.cpp
// Demonstrating storage-class specifier mutable.
#include <iostream>
using namespace std;

// class TestMutable definition
class TestMutable
{
public:
   TestMutable( int v = 0 )
   {
      value = v;
   } // end TestMutable constructor

   int getValue() const
   {
      return ++value; // increments value
   } // end function getValue
private:
   mutable int value; // mutable member
}; // end class TestMutable

int main()
{
   const TestMutable test( 99 );

   cout << "Initial value: " << test.getValue();
   cout << "\nModified value: " << test.getValue() << endl;
} // end main
```
```

```
```text
Initial value: 99
Modified value: 100
```
```

Fig. 24.2 | Demonstrating a mutable data member.

Line 25 declares const TestMutable object test and initializes it to 99. Line 27 calls the const member function getValue, which adds one to value and returns its previous contents. Notice that the compiler allows the call to member function getValue on the object test because it’s a const object and getValue is a const member function. However, getValue modifies value’s actual value. Thus, when line 28 invokes getValue again, the new value (100) is output to prove that the mutable data member was indeed modified.