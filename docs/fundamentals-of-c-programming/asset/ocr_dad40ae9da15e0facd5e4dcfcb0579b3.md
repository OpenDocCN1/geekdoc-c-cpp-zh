```
w1 serial number = 1
w2 serial number = 2
w3 serial number = 3
w4 serial number = 4
```

Each Widget object has its own serial_number variable, but all Widget objects have access to the shared serial_number_source variable. The executing program initializes serial_number_source one time at the beginning of the program's execution before it calls the main function. This means serial_number_source is properly initialized to 1 before the program creates any Widget objects. Each time the client creates a new Widget object, the constructor assigns the individual object's serial number from the static variable. The constructor also increments serial_number_source's value, so the next object created will have a serial number one higher than the previous Widget.

C++ programmers often use class static fields to provide public constants available to clients. Consider Listing 15.11 (trafficsignal.h) that models a simple traffic light a little differently from Listing 15.7 (trafficlight.h). It uses symbolic integer constants instead of enumeration types.

# Listing 15.11: trafficsignal.h

```
#ifndef TRAFFICSIGNAL_H_
#define TRAFFICSIGNAL_H_

class TrafficSignal {
  int color; // The light's current color: RED, GREEN, or YELLOW
public:
  // Class constants available to clients
  static const int RED = 0;
  static const int GREEN = 1;
  static const int YELLOW = 2;

  TrafficSignal(int initial_color);
  void change();
  int get_color() const;
};

#endif
```

The state of a traffic light object—which of its lamps is illuminated—is determined by an integer value: 0 represents red, 1 stands for green, and 2 means yellow. It is much more convenient for clients to use the symbolic constants RED, GREEN, and YELLOW than to try to remember which integer values stand for which colors. These constants are public, so clients can freely access them, but since they are constants, clients cannot alter their values. An additional benefit to being const is this: You may initialize a static const field within the class body itself. You do not need to re-define a static const field outside the class body as you do for a non-const static field.

Listing 15.12 (trafficsignal.cpp) provides the implementation of the methods of TrafficSignal class.

# Listing 15.12: trafficsignal.cpp

```
#include "trafficsignal.h"

// Ensures a traffic light object is in the state of
// red, green, or yellow.  A rogue integer value makes the
// traffic light red
```