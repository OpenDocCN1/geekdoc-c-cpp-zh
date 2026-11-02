```
7 {
8 public:
9   // Listen for events from a coffee machine
10 CoffeeMachineListener(CoffeeMachine* m):m(m){}
11   // This is invoked by the simulator when the model produces output
12 void outputEvent(adts::AtomicIO_Type* model, const IO_Type& value, unsigned int t)
13 {
14   std::cout << "output @ t = " << t << ", ";
15   if (value == NICKEL) std::cout << "nickel\n";
16   else if (value == DIME) std::cout << "dime\n";
17   else if (value == QUARTER) std::cout << "quarter\n";
18   else if (value == COFFEE) std::cout << "Coffee\n";
19   else std::cout << "nothing\n";
20 }
21   // This is invoked by the simulator when the model changes state
22 void stateChange(adts::AtomicIO_Type* model, unsigned int t)
23 {
24   std::cout << "You have " <<
25   m->getCustomerValue() << " cents @ t = "
26   << t << std::endl;
27 }
28 private:
29   CoffeeMachine* m;
30 };
31 
32 #endif
```

The program's main function has two parts. The first part creates a CoffeeMachine, a CoffeeMachineListener, and a Simulator. The CoffeeMachine is passed to the Simulator's constructor, and the CoffeeMachineListener is registered to receive output and state change notifications from the Simulator. The second part runs the simulation until the user types "quit." Each line of input to the program is parsed into quarter (q), dime (d), nickel (n), cancel (c), and wait (w) inputs for the model. These are applied to the CoffeeMachine via the Simulator's computeNextState method. When the user types "quit," the profit made by the machine is printed, the program cleans up, and then it exits.

# Main Function for the Coffee Machine Simulation

```
1 #include "CoffeeMachine.h"
2 #include "CoffeeMachineListener.h"
3 #include <iostream>
4 using namespace std;
5 
6 int main()
7 {
8   // Create the model
```