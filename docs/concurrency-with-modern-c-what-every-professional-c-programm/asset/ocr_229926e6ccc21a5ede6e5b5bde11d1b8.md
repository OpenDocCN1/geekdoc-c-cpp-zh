+   - has to be declared as default or delete or the function body must be empty (C++11).

The constexpr user-defined type

+   - cannot have virtual base classes.
+   - requires each base object and each non-static member to be initialized in the constructor's initialization list or directly in the class body. Consequently, it holds that each used constructor (e.g. of a base class) has to be constexpr constructor and that the applied initializers have to be constant expressions.

cppreference.com¹ provides additional information to constexpr user-defined types. To add praxis to the theory, I define the class MyInt. MyInt shows the just mentioned points. The class has also constexpr member functions.

# Immutable user-defined types

```
```cpp
// userdefinedTypes.cpp

#include <iostream>
#include <ostream>

class MyInt{
public:
    constexpr MyInt()= default;
    constexpr MyInt(int fir, int sec): myVal1(fir), myVal2(sec){}
    MyInt(int i){
        myVal1= i - 2;
        myVal2= i + 3;
    }

    constexpr int getSum() const { return myVal1 + myVal2; }

    friend std::ostream& operator<< (std::ostream &out, const MyInt& myInt){
        out << "(" << myInt.myVal1 << "," << myInt.myVal2 << ")";
        return out;
    }

private:
    int myVal1= 1998;
    int myVal2= 2003;

};

int main(){
```
```

¹https://en.cppreference.com/w/cpp/language/constexpr