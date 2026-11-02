```
```cpp
const Bag<SimEvent> &xb)
{
    internal_event(q,events);
    external_event(q,0,0,xb);
}

void TankPhysicsEqns::output_func(const double *q, const bool* events,
        Bag<SimEvent> &yb)
{
    // Produce a position event
    SimTankPosition pos;
    pos.x = q[X]; pos.y = q[Y]; pos.theta = q[THETA];
    yb.insert(SimEvent(pos));
}

double TankPhysicsEqns::getLeftCurrent(const double* q) const
{
    if (simple) return (el-alpha*q[WL])/Rm;
    else return q[L];
}

double TankPhysicsEqns::getRightCurrent(const double* q) const
{
    if (simple) return (er-alpha*q[WR])/Rm;
    else return q[R];
}
```
```

# Header File for the Tank Class

```
```cpp
#ifndef Tank_h_
#define Tank_h_
#include "Computer.h"
#include "TankPhysics.h"

// This is the complete model of the tank with the TankPhysics and Computer
class Tank:
    public adevs::Network<SimEvent>
{
public:
    // Tank has an interrupt handler with the specified frequency,
    // starts at the specified position, and generates events for
    // the display at the given interval
    Tank(double freq, double x0, double y0, double theta0, double cint);
    // Get the components of the tank
    void getComponents(adevs::Set<adevs::Devs<SimEvent> > &c);
    // Route events within the tank
    void route(const SimEvent& value, adevs::Devs<SimEvent>* model,
        adevs::Bag<adevs::Event<SimEvent> > &br);
    // Get the physics model
```
```