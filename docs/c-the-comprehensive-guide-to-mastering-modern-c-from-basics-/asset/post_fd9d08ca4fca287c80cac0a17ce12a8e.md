
the literals "red", "yellow", and "green". You can avoid typos by defining constants like const string RED = "red";

However, the ubiquitous int and string types are often referred to as type sinks—which roughly means black holes for types." Let's assume you wrote a method that takes a traffic light color:

```
createStoplight(string lightColor, string lightName);
```

Many things can go wrong here:

```
createStoplight("AX-001", YELLOW);               // Arguments swapped
createStoplight("yellowgreen", "AX-002");         // Undefined color used
createStoplight("grren", "AX-003");               // Typo in color
```

These are all errors that the compiler does not notice—and perhaps you don't either, but only the customer does.

The solution is to write a StoplightColor enumeration class that defines the exact valid range—no more and no less.

```cpp
// https://godbot.org/z/xd7s1YhE
#include <string>
using std::string;
enum class StoplightColor {
    RED, YELLOW, REDYELLOW, GREEN
};
struct Stoplight {
    StoplightColor color_;
    Stoplight(StoplightColor color, string name) : color_{color} {}
};
```

```cpp
Stoplight createStoplight(StoplightColor color, string name) {
    return Stoplight(color, name);
}
int main() {
  Stoplight stoplight = createStoplight(StoplightColor::RED, "AX-001");
}
```

# Listing 16.30 With an "enum", you define a type with its own value range.

Now you can implement different behaviors depending on the traffic light color. This is often used in switch statements or if-else chains:

```cpp
string drivingSchool(Stoplight light) {
  switch(light.color_) {
    case StoplightColor::RED:
      return "stop";
    case StoplightColor::YELLOW:
      return "get ready";
    case StoplightColor::REDYELLOW: // Fixed from duplicate YELLOW in context
      return "brake";
    case StoplightColor::GREEN:
      return "go";
  }
  abort(); // exhaustive switch, should not happen
}
```

We've handled all possible cases in the switch, so the abort() should not occur. Alternatively, we could have defined a default: case.

It's good that with enum class, RED and YELLOW no longer enter the surrounding namespace, but having to always write the TrafficLightColor:: prefix is cumbersome, especially in such a switch. Therefore, since C++20, there is the possibility to bring the enumeration class into the current namespace using enum TrafficLightColor:

```cpp
// https://godbolt.org/z/f8on7bs1Y
string drivingSchool(Stoplight light) {
    switch(light.color) {
        using enum StoplightColor; // "StoplightColor::" can now be omitted
        case RED:
            return "stop";
        case REDYELLOW:
            return "get ready";
        case YELLOW:
            return "slow down";
        case GREEN:
            return "go";
    }
    abort(); // exhaustive switch, should not happen
}
```

Individual values using StoplightColor::RED can also be imported. This can be important to avoid name conflicts.

In other applications, the possible enum values are backed by specific numerical values. You can access these with a type conversion. You can specify the numerical values in the enumeration class.

```cpp
// https://godbolt.org/z/Yibzrnob
enum class Weekday {
    MO=1, TU, WE, TH, FR, SA, SU // TU becomes 2, WE becomes 3
};
enum class Level {
    TRACE=1, DEBUG, INFO=10, ERROR, FATAL // gaps are also possible
};
void log(Level level) {
    int intLevel = (int)level; // explicitly cast to an int
    if(intLevel > 10) { /* ... */ }
}
```

# Listing 16.31 In an "enum", you can also specify the desired numerical values.

The C++ compiler assigns values incrementally after each explicitly specified value. Thus, in Level, DEBUG becomes 2, ERROR becomes 11, and FATAL becomes 12. If, as a user, you need the int value of an element when using it, you can obtain the value through explicit type casting like (int)level.

# 17 GOOD CODE, 4TH DAN: SECURITY, QUALITY, AND SUSTAINABILITY

In this chapter, I want to summarize some things that can particularly help you in the development of *good software*. Throughout the book, you will find many tips, and especially in [Chapter 29], a long collection, but each is only briefly touched upon.

The special thing about the tips in this chapter is that they are best applied *from the very beginning*. If you incorporate the ideas *behind* the rules into your daily programming routine, your perspective on C++ and your thinking with C++ will change in such a way that better code will automatically emerge.

# 17.1 The Rule of Zero

A class can be equipped with many functions for special purposes. You can initiate an automatic conversion, you can specify how a class should be copied, and so on.

Read the following paragraphs at ease—because at the end I will tell you that you should not implement any of them.

## 17.1.1 The Big Five

The C++ compiler generates five special functions for you. Pay special attention to the following:

- Destructor `~Type()`: The compiler cleans up member variables.
- Copy constructor `Type(const Type&)`: If you do not write it, the compiler generates one.
- Copy assignment operator `operator=(const Type&)`: If you do not write it, the compiler generates one.
- Move constructor `Type(Type&&)`: If you do not write it, the compiler generates one.
- Move assignment operator `operator=(Type&&)`: If you do not write it, the compiler generates one.

It is said that if you need to implement one of these functions, then you must implement the others as well. This is because all functions need to handle ownership. You may noticed what the compiler can generate was mentioned each time. And each time, raw pointers and C-arrays are problematic.

## 17.1.2 Helper Construct by Prohibition

Instead of tackling the not-simple task of implementing all these functions, you can at least prohibit them. If you disable all copy and move operations, then ownership cannot get mixed up.

```cpp
// https://godbolt.org/z/K1714eWr9
struct Type {
    // raw pointer can cause unclear ownership
    char* data_;
    Explicit Type(int n) : data(new char[n]) {}
    ~Type() { delete data_; } // you need the destructor

    Type(const Type&) = delete; // do not allow copying
    Type& operator=(const Type&) = delete; // no assignment please
    Type(Type&&) = delete; // no moving
    Type& operator=(Type&&) = delete; // no move assignment
};
```

### Listing 17.1 Prohibit four of the big five with `= delete`.

## 17.1.3 The Rule of Zero and Its Application

Am I away from using raw pointers? Good! Because the solution to the puzzle, the philosopher’s stone, the holy grail is this: take advantage of the compiler's ability to generate functions for you. You just need to allow it to do so correctly. First, memorize the
