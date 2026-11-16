
```
return color;
}
```

The code within Listing 15.8 (trafficlight.cpp) must #include the trafficlight.h header so the compiler is exposed to the TrafficLight class declaration; otherwise, when compiling trafficlight.cpp the compiler would not know if the method implementations faithfully agreed with declarations. If the method definition of TrafficLight::change in trafficlight.cpp specified parameters but its declaration within trafficlight.h did not, that would be a problem. Furthermore, without including trafficlight.h, the type SignalColor would be an undefined type within trafficlight.cpp.

Notice that outside the class declaration in Listing 15.7 (trafficlight.h) we must prefix the method names with TrafficLight::. Without this prefix the compiler would treat the identifiers as globals. It would interpret them as functions, not methods. SignalColor is declared outside of the TrafficLight class, so it does not need the TrafficLight:: prefix. SignalColor is a global type available to any code that #includes trafficlight.h.

Listing 15.9 (trafficmain.cpp) shows how a client could use the TrafficLight class.

### Listing 15.9: trafficmain.cpp

```
#include <iostream>
#include "trafficlight.h"

void print(TrafficLight lt) {
    SignalColor color = lt.get_color();
    std::cout << "---------\n";
    std::cout << "| " << "\n";
    if (color == SignalColor::Red)
        std::cout << "| (R) |\n";
    else
        std::cout << "|   |\n";
    std::cout << "| " << "\n";
    if (color == SignalColor::Yellow)
        std::cout << "| (Y) |\n";
    else
        std::cout << "|   |\n";
    std::cout << "| " << "\n";
    if (color == SignalColor::Green)
        std::cout << "| (G) |\n";
    else
        std::cout << "|   |\n";
    std::cout << "| " << "\n";
    std::cout << "---------\n";
}

int main() {
    TrafficLight light(SignalColor::Green);
    while (true) {
        print(light);
        light.change();
        std::cin.get();
    }
}
```

Listing 15.9 (trafficmain.cpp) first prints

```
+------+
|      |
| ( )  |
|      |
| ( )  |
|      |
| (G)  |
|      |
+------+
```

When the user presses the `Enter` key the program prints

```
+------+
|      |
| ( )  |
|      |
| (Y)  |
|      |
| ( )  |
|      |
+------+
```

a second `Enter` press prints

```
+------+
|      |
| (R)  |
|      |
| ( )  |
|      |
| ( )  |
|      |
+------+
```

A third `Enter` press completes the cycle:

```
+------+
|      |
| ( )  |
|      |
| ( )  |
|      |
| (G)  |
|      |
+------+
```

The program's execution continues in this manner within its infinite loop until the user presses `Ctrl+C`

Observe that the `color` variable within the `TrafficLight` class is private. That means that once the client creates a traffic light object the only way a client can influence the value of `color` is via the `change` method. This makes it impossible for a client to force a traffic light object to cycle incorrectly, for example, a client cannot make a traffic light change directly from yellow to green (it would have to pass through red on the way from yellow to green).

## 15.6 Preventing Multiple Inclusion

C++ follows the *one definition rule*, or ODR, which means a variable, function, class, instance variable, or method may not have more than one definition in the same context. The code within the following function definition violates the one definition rule:

```
int sum_and_display(const std::vector<int>& list) {
    int s = 0, size = list.size();
    // Add up the values in the list
    int i = 0;
    while (i < size) {
        s += list[i];
        i++;
    }
    // Print the contents of the list
    int i = 0; // Illegal, variable i already defined above
    while (i < size) {
        std::cout << std::setw(5) << list[i] << '\n';
        i++;
    }
    std::cout << "-------\n";
    std::cout << std::setw(5) << s << '\n';
}
```

The line

```
int s = 0, size = list.size();
```

is not a problem even though the identifier size appears twice. The first appearance denotes the local variable named size, and the second use is a call to the size method of the std::vector class. This statement defines (declares) only the variable size; the size method already has been defined in the std::vector class (and the compiler processed its definition from the <vector> header file).

The variable i has two distinct definitions in the same context, so its redefinition right before the display code is an error.

Like a variable, a class may have only one definition. When we build general purpose classes meant to be used widely in our programs we must take care that we do not violate the one definition rule. In fact, we can violate the one definition rule accidentally even if we define a class only once!

To see how we can accidentally violate the one definition rule, consider the following simple example. Suppose we have a simple counter class declared in count.h:

```
class Counter {
    int count;
public:
    // Allow clients to reset the counter to zero
    void clear();
    // Allow clients to increment the counter
    void inc();
    // Return a copy of the counter's current value
    int get() const;
};
```

with its implementation in count.cpp:

```
// Allow clients to reset the counter to zero
void Counter::clear() {
    count = 0;
}

// Allow clients to increment the counter
void Counter::inc() {
    count++;
}

// Return a copy of the counter's current value
int Counter::get() const {
    return count;
}
```

Next, consider the following two header files defining objects that themselves use Counter objects, widget.h:

```
// File widget.h

#include "count.h"

class Widget {
    Counter meter;
public:
    // Other stuff omitted
};
```

and gadget.h:

```
// File gadget.h

#include "count.h"

class Gadget {
    Counter ticker;
public:
    // Other stuff omitted
};
```

The preprocessor directive

```
#include "count.h"
```

is required in the file widget.h, because the compiler must be acquainted with the type Counter to properly handle the instance variable meter. Similarly, the count.h header must be included in gadget.h in order for the compiler to accept Gadget's declaration of its ticker field.

Client code that wishes to use Widget objects must use the appropriate #include statement:

```
#include "widget.h"

int main() {
    Widget myWidget;
    // Use the myWidget object
}
```

Similarly, client code that uses Gadget objects must include at the top of its file:

```
#include "gadget.h"

int main() {
    Gadget myGadget;
    // Use the myGadget object
}
```

Both of these client programs will build without any problems. Sometimes, however, a program may need to use both Widget objects *and* Gadget objects. Since the widget.h header file does not know anything about the Gadget class and the gadget.h header file has no information about Widgets, we must include both header files in code that uses both classes. The appropriate include directives would be

```
#include "widget.h"
#include "gadget.h"

int main() {
    Widget myWidget;
    Gadget myGadget;
    // Use the myWidget and myGadget objects
}
```

Including one of the header files without the other is insufficient since the compiler must be able to check if the client is using both types correctly. This client code, however, will not compile. In this case the problem is with *count.h*. Including both widget.h and gadget.h includes the definition of the Counter class twice, so the compiler sees two definitions of Counter. Even though the two definitions are identical, this violates the one definition rule and so results in a compiler error.

The issue here is known as *multiple inclusion*, and it can arise when header files #include other header files. Multiple inclusion is a problem, but it often is necessary because the programmer may have a legitimate need for both types of objects within the same program. Fortunately, the solution is simple. The standard way to prevent multiple inclusion is to wrap a class definition as follows:

```
#ifndef COUNT_H_
#define COUNT_H_

class Counter {
int count;
public:
    // Allow clients to reset the counter to zero
    void clear();

    // Allow clients to increment the counter
    void inc();
}
```
