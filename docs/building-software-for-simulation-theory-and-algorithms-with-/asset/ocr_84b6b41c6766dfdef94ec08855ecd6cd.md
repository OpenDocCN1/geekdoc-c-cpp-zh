Correct operation of this system depends critically on the proper timing of changes in the input. The input values are permitted to change at every third tick of the clock and must be held constant otherwise. The simulation code enforces this in its main loop. The behavior of the model is much more difficult to anticipate if this restriction is removed. To demonstrate this, the author has changed the main function of the simulation program to apply a new input value at every tick of the clock, rather than holding the input constant between machine cycles. The code is listed below.

# Main Program to Apply Input Immediately

```
```cpp
#include "adtss.h"
#include "n1.h"
#include <iostream>
using namespace std;

class MachineListener: public adtss::EventListener<port_value_t>
{
public:
    void outputEvent(adtss::Atomic<port_value_t>* model,
        const port_value_t& x, unsigned int t)
    {
        // Print the time and output at the next machine cycle
        cout << "y " << t << "\t" << x.bit << endl;
    }
    void stateChange(adtss::Atomic<port_value_t>*,unsigned int){}
};

int main()
{
    // Create the model
    adtss::Resultant<port_value_t>* m =
        new adtss::Resultant<port_value_t>(new N1());
    // Setup the simulator and output listener
    MachineListener* l = new MachineListener();
    adtss::Simulator<port_value_t>* sim =
        new adtss::Simulator<port_value_t>(m);
    sim->addEventListener(l);
    // Run the simulation
    while (true) {
        // Get the input from stdin
        adtss::Bag<port_value_t> input;
        port_value_t x1, x2;
        x1.port = N1::x1;
        x2.port = N1::x2;
        cin >> x1.bit >> x2.bit;
        // Quit if the input has ended
        if (cin.eof()) break;
        input.insert(x1);
```
```