switch the mode if an interrupt indicator is received; and (3) if the model was idle and a packet is now available, then begin to process it. The operation of the external transition function can be inferred without ambiguity because the events S0 through S3 produce the same result regardless of the order in which they are applied.

The confluent transition function must resolve the situation where S4, S0, S3, or all of these are eligible to be active at the same time. The phase graph does not supply a rule for this situation, and so we must create one to complete the state space description of the model. Any ordering of the external events S3 and S0 will produce the same result, and so the question is where S4 should sit in the sequence. The intention of the phase graph is that S4 occur while the model is in the OPERATE phase. Because an interrupt can move the model out of this phase, it seems reasonable to apply S4 prior to engaging any of the external events. This implies that the confluent transition function is calculated by first applying the internal transition function and then the external transition function.

The output function and time advance function are less complicated. The model will produce output only when it is in the OPERATE phase, and the output is a *SimMotorOnTime* event that carries the ON times and directions contained in the packet at the front of the queue. If the model is operating, then the time until the next internal event is σ. If the model is interrupted, then the next internal event is at infinity. The implementation of the *PacketProcessing* model is listed below.

# **Implementation of the PacketProcessing Model**

```
~~~cpp
#include "PacketProcessing.h"
#include <cmath>
using namespace std;
using namespace adevs;

PacketProcessing::PacketProcessing():
    Atomic<SimEvent>(),
    processing_time(0.0016),
    sigma(DBL_MAX),
    interrupt(false)
{
}

void PacketProcessing::delta_int()
{
    q.pop_front();
    if (q.empty()) sigma = DBL_MAX;
    else sigma = processing_time;
}

void PacketProcessing::delta_ext(double e, const Bag<SimEvent>& xb)
{
    // If we are not interrupted and are processing a packet, then
    // reduce the time remaining to finish with that packet
~~~
```