# 17.1. I/O STREAM INHERITANCE

```
return os;
)
```

Can we easily adapt our << operator so that we can use it with ofstream objects?

The answer, perhaps surprisingly, is not that we do not have to adapt our operator<< function; it works as with ofstream objects. How can this be, since the count object has type ofstream is not the same class as ofstream?

C++ allows some automatic conversions in the numeric types; for example, an int is widened to a double, and a double is truncated to an int. bool and ints are freely interconvertible. These types are built into the library, so standards apply. When it comes to programmer-defined types, the compiler is unable to automatically generate code to convert one to another. Most of the time it would make no sense to do so—imaginary attempting to convert an object of type Stopwatch(16) to an object of type Tester(16).

So, how is that an object of type ofstream be automatically converted to an object of type ostream? You might think that is because both are part of the standard library, so the conversion has been programmed into them. The conversion takes place! Any object of type ofstream object is automatically treated as if it were an ostream object because of the ostream and ofstream classes are in a special relation. The ofstream class is derived from the ostream class. We may say that ostream is the base class and ofstream is the derived class. Sometimes the term superclass is used instead of subclass. The base/derived class terminology is used interchangeably with super/subclass, although the C++ community tends to prefer the base/derived over super/subclass. The process is known as inheritance because the derived class inherits the characteristics of its base class. The terms derivation, subclassing and specialization are used sometimes in place of the term inheritance.

As a consequence of the derivation process, an instance of the derived class can be treated as if it were an instance of the base class. Listing 17.1 (printstreams.cpp) shows how a function can process instances of two different classes by inheritance.

Listing 17.1: printstreams.cpp

```
#include <fstream>

using namespace std;

void print(ostream& os, int n) {
    os.width(10); // Right filled in 10 spaces
    os.fill('*'); // Fill character is *
    os << n << endl;
}

int main() {
    // Pretty print to screen
    print(cout, 35);

    // Pretty print to text file
    ofstream out("temp.data");
    if (out.good()) {
        print(out, 36);
    }
    out.close();n}
```