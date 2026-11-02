```
```cpp
const SimTankPosition& simTankPosition() const { return data.pos; }
// Get the motor settings
const SimMotorOnTime& simMotorOnTime() const { return data.ontime; }
// Get the network packet
const SimPacket& simPacket() const { return data.packet; }
// The STL needs this operator
bool operator<(const SimEvent& b) const { return type < b.type; }
private:
SimEventType type;
union
{
SimMotorVoltage volts;
SimTankPosition pos;
SimMotorOnTime ontime;
SimPacket packet;
} data;
};
#endif
```
```

# A.2.3 Pointers and Hierarchies of Events

When simple data structures and unions are insufficient, the designer almost invariably resorts to pointers. Now the output of a model can be an arbitrarily complex object to which the recipients of the event receive a pointer. In many ways, using pointers for input and output is a necessary evil; all variations on this theme have considerable drawbacks. The need for explicit memory management is most immediately apparent; this issue, along with the gc_output method for addressing it, were discussed in Section 3.1.5.

There are other, more subtle and far-reaching, impacts that pointers have on the design of the simulator. In fact, it is not a problem with using pointers, but a more general difficulty arising from the use of indirection to move events from source to destination. Suppose that we construct a hierarchy of classes, such as the one shown in Figure A.1, for the types of events in the simulation. The base class contains information common to all events: a virtual method for printing the event data to a log, a pointer to the source of the event, and maybe a type code to help with debugging. Each derived class contains information that is pertinent to a specific type(s) of event.

The input-output type of the Atomic, Network, and Simulator classes is a pointer to the base class X. The route method carries this pointer from the output_func of the originating model to the delta_ext and delta_conf methods of the receiving models. The models, however, need the classes EventA and EventB that are derived from X. The simulator cannot provide these because the type information is lost when the event is routed.

Runtime type identification is used at the event’s destination to recover the lost type information and downcast the object accordingly. The downcast is done with the