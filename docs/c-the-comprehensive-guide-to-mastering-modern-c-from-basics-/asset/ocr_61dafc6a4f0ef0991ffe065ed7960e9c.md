# 12.6 Defining Methods Inline

Did you notice that when declaring and later defining the method of the class, I used a technique you already know—the forward declaration of the method? First, in the structure, only the method header is mentioned, and then later, outside, the actual definition takes place. (Strictly speaking, it is still an aggregate, but it will soon become a class. Everything is still public, without constructors or virtual methods.)

This is also the way you should usually go forward with structures and classes. However, if a method is very short, for example, then you can treat it the same way as normal functions. You can also define it right on the spot—within the structure.

```
// https://godbolt.org/z/Y3eW1Kh8v
#include <string>
#include <iostream>    // ostream
#include <format>

using std::string; using std::ostream; using std::format;

struct Person {
    string name;
    int age;
    string city;
    ostream& print(ostream& os) {    // method defined inline
        return os << format("{{\{\}}\} from {}", name, age, city);
    }
};
```

Listing 12.11 Methods can also be defined inline.