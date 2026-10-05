# 15. SEPARATING METHOD DECLARATIONS AND DEFINITIONS

```
public:
    Point(double x, double y) : x(x), y(y) {}
    double get_x() const { return x; }
    double get_y() const { return y; }
    void set_x(double v) { x = v; }
    void set_y(double v) { y = v; }

```

```
double dist(const Point pt1, const Point pt2) {
    // Compute distance between pt1 and pt2
    // This is a function stub; add the actual code later
    return 0.0; // Just return zero for now
}
```

```
int main() {
    Point p1(2.5, 6), p2(0.0, 0.0);
    std::cout << dist(p1, p2) << std::endl;
}
```

Here the Point class is very simple, and the constructor and methods are obvious. The inline structure makes more sense in this situation.

Listing 15.4(trafficlight.h) contains the interface for a class to create objects that simulate stop-caution traffic signals.

```
Listing 15.4: trafficlight.h
class TrafficLight {
public:
    // Constants available to clients
    enum SignalColor { Red, Green, Yellow };
private:
    SignalColor color; // The light's current color: Red, Green, or Yellow
public:
    TrafficLight(SignalColor initial_color);
    void change();
    SignalColor get_color() const;
}
```

Notice the TrafficLight class defines a public enumerated type (SignalColor) that clients may use. Because the type is defined inside the class, clients must use the fully-qualified name TrafficLight::SignalColor when declaring variables or parameters of the type.

The traffic signal implementation code in Listing 15.5(trafficlight.cpp) defines the TrafficLight methods.

```
Listing 15.5: trafficlight.cpp
#include "trafficlight.h"

// Ensures a traffic light object is in the state of
// red, green, or yellow. A rogue value makes the
// traffic light
TrafficLight::TrafficLight(TrafficLight::SignalColor initial_color) {
    switch (initial_color) {
```