```
class Widget {
    int value;
    static int quantity;
};
```

Each individual Widget object has its own value variable, but only one quantity variable exists and is shared by all Widget objects.

One unusual thing about static fields is that must be defined outside of the class declaration. For the Widget class above, we must supply the statement

```
int Widget::quantity;
```

somewhere in the source code outside of the class declaration.

Consider a widget factory in which each widget object must have a unique serial number. Serial numbers are sequential, and a new widget object's serial number is one larger than the widget produced immediately before. Important for warranty claims, a client should not be able to alter a serial number of a widget object. The Widget class in Listing 15.10 (serialnumber.cpp) shows how to use a static variable to manage serial numbers for widget objects.

# Listing 15.10: serialnumber.cpp

```
#include <iostream>

class Widget {
    // All Widget objects share serial_number_source
    static int serial_number_source;
    // Each Widget object is supposed to have its own
    // unique serial number
    int serial_number;
public:
    // A Widget object's serial number is initialized from
    // the shared serial_number_source variable which is
    // incremented each time a Widget object is created
    Widget(): serial_number(serial_number_source++) {}
    // Client's can look at the serial number but not touch
    int get_serial_number() const {
        return serial_number;
    }
};

// Initialize the initial serial number; the first
// Widget made will have serial number 1
int Widget::serial_number_source = 1;

// Make some widgets and check their serial numbers
int main() {
    Widget w1, w2, w3, w4;
    std::cout << "w1 serial number = " << w1.get_serial_number() << '\n';
    std::cout << "w2 serial number = " << w2.get_serial_number() << '\n';
    std::cout << "w3 serial number = " << w3.get_serial_number() << '\n';
    std::cout << "w4 serial number = " << w4.get_serial_number() << '\n';
}
```

The output of Listing 15.10 (serialnumber.cpp) is