# 16.12.2  Enumeration Classes

You have learned that integer types like `int` and the string type `string` are very useful data types. For example, if you wanted to write a `Stoplight` class, you could use it to represent the current light. With an `int`, you would “remember” that 0 stands for red, 1 for yellow, and 2 for green. Or you could use a string and consistently use the literals “red”, “yellow”, and “green”. You can avoid typos by defining constants like `const string RED = "red";`.

However, the ubiquitous `int` and `string` types are often referred to as *type sinks*—which roughly means “black holes for types.” Let’s assume you wrote a method that takes a traffic light color:

```
Stoplight createStoplight(string lightColor, string lightName);
```

Many things can go wrong here:

```
createStoplight("AX-001", YELLOW);       // ⚠ Arguments swapped
createStoplight("yellowgreen", "AX-002"); // ⚠ Undefined color used
createStoplight("green", "AX-003");       // ⚠ Typo in color
```

These are all errors that the compiler does not notice—and perhaps you don’t either, but only the customer does.

The solution is to write a `StoplightColor` *enumeration class* that defines the exact valid range—no more and no less.

```
// https://godbolt.org/z/xhd7s1YhE
#include <string>
using std::string;
enum class StoplightColor {
    RED, YELLOW, REDYELLOW, GREEN
};
struct Stoplight {
    StoplightColor color_;
    Stoplight(StoplightColor color, string name) : color_{color} {}
};

Stoplight createStoplight(StoplightColor color, string name) {
    return Stoplight{color, name};
}

int main() {
    Stoplight st_stoplight = createStoplight(StoplightColor::RED, "AX-001");
}
```

**Listing 16.30** With an “enum”, you define a type with its own value range.