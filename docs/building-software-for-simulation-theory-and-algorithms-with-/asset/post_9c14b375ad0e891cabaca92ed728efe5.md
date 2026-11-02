
```cpp
43            // Input to N2
44            e.model = &n2;
45            e.value.port = N2::m;
46            r.insert(e);
47          }
48        }
49      private:
50        adtss::Resultant<port_value_t> n2;
51        Memory m;
52      };
53
54    #endif
```
## N2 Model
```cpp
1    #ifndef _n2_h_
2    #define _n2_h_
3    #include "adtss.h"
4    #include "xor_memory_models.h"
5
6    class N2: public adtss::Network<port_value_t>
7    {
8      public:
9
10       static const int m, x1, x2; // Labels for the input ports
11
12       N2():adtss::Network<port_value_t>(),
13           xor1(),xor2(){}
14
15       void getComponents(adtss::Set<adtss::Atomic<port_value_t>*>& c)
16       {
17         c.insert(&xor1);
18         c.insert(&xor2);
19       }
20
21       void route(const port_value_t& value,
22           adtss::Atomic<port_value_t>* src,
23           adtss::Bag<adtss::Event<port_value_t> >& r)
24       {
25         adtss::Event<port_value_t> e;
26         e.value = value;
27         // Input to the network
28         if (src == getResultant()) {
29           // Input to the m port
30           if (value.port == m) e.model = &xor2;
31           // Input to one of the bit ports
32           else e.model = &xor1;
33           r.insert(e);
34         }
```
```cpp
// Output from 01
else if (src == &xor1) {
    // Input to 02
    e.model = &xor2;
    r.insert(e);
}
// Output from 02
else if (src == &xor2) {
    // Output from the network
    e.model = getResultant();
    r.insert(e);
}
}
private:
    Xor xor1, xor2;
};

#endif
```
## N1 and N2 Port Definitions
```cpp
#include "n1.h"
#include "n2.h"
// Ports have unique numbers within the scope of their class
const int N2::m = 0;
const int N2::x1 = 1;
const int N2::x2 = 2;
const int N1::x1 = N2::x1;
const int N1::x2 = N2::x2;
```
The main function for the simulator, which is listed below, reads a pair of input bits from standard input, applies these inputs for a complete machine cycle (three clock cycles), and prints the output of the machine at each clock cycle.

## Main Function for the Logical Machine Simulator
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
```
```cpp
{
    cout << x.bit << " ";
}
void stateChange(adtss::Atomic<port_value_t>*,unsigned int){}
};

int main()
{
    // Create the model
    adtss::Resultant<port_value_t>* m =
    new adtss::Resultant<port_value_t>(new N1());
    // Setup the simulator and a listener for reporting outputs
    MachineListener* l = new MachineListener();
    adtss::Simulator<port_value_t>* sim =
    new adtss::Simulator<port_value_t>(m);
    sim->addEventListener(l);
    // Counters for the clock and machine cycle
    int clk = 0, machine_cycle = 0;
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
        input.insert(x2);
        // Print the time and input
        cout << "## M" << machine_cycle << " C" << clk <<
        "\t" << x1.bit << " " << x2.bit << "\t\n";
        // Print the time and output at the next machine cycle
        cout << "## M" << ++machine_cycle <<
        " C" << clk+2 << "\t\n";
        // Advance the simulation by one machine cycle
        for (int t = 0; t < 3; t++) {
            clk++;
            sim->computeNextState(input);
        }
        cout << endl;
    }
    // Clean up and exit
    delete sim; delete l; delete m;
    return 0;
}
```

Now we have a complete simulator for the logical function defined by Equation 3.22. For reference, it is rewritten here:

$$y(n+1)=y(n)\oplus(x_1(n)\oplus x_2(n))$$

The time $n$ in this function counts machine cycles. Three timesteps of the model are needed to complete one machine cycle. Consequently, logical input–logical output is read at every third clock cycle.

The memory possessed by this model gives it an interesting transient behavior. If the inputs $x_1$ and $x_2$ are maintained such that $x_1\oplus x_2$ is 1, then the output will oscillate between 1 and 0. If the input changes to $x_1\oplus x_2=0$, then the output will stick to its previous value. The oscillating behavior can be resumed by setting $x_1\oplus x_2$ back to 1.

We can compute the output trajectory by hand using the definition of $y$ as a function of $x_1$ and $x_2$. Recall that $y(0)=0$. If we apply $x_1[0,3]=111$ and $x_2[0,3]=000$, the output is

$$\begin{aligned}
y(1)&=y(0)\oplus(x_1(0)\oplus x_2(0))=0\oplus(1\oplus0)=1\\
y(2)&=y(1)\oplus(x_1(1)\oplus x_2(1))=1\oplus(1\oplus0)=0\\
y(3)&=y(2)\oplus(x_1(2)\oplus x_2(2))=0\oplus(1\oplus0)=1
\end{aligned}$$

The simulator, of course, agrees with this calculation. Feeding the input

```
1 0
1 0
1 0
```

into the simulator produces the output

```
xx M0 C0        1 0    yy M1 C0–2    0 0 1
xx M1 C3        1 0    yy M2 C3–5    1 1 0
xx M2 C6        1 0    yy M3 C6–8    0 0 1
```

where the columns preceded by xx are the inputs at each machine cycle and the columns preceded by yy are the output produced at and between machine cycles. Because each machine cycle requires three timesteps, there are two transient outputs for every machine output: the last column of the simulator’s report is y.

If the machine is subsequently fed $x_1[3,5]=00$ and $x_2[3,5]=00$, then

$$\begin{aligned}
y(4)&=y(3)\oplus(x_1(3)\oplus x_2(3))=1\oplus(0\oplus0)=1\\
y(5)&=y(4)\oplus(x_1(4)\oplus x_2(4))=1\oplus(0\oplus0)=1
\end{aligned}$$

and the output will remain 1 while the input is constant. The simulator, of course, agrees with this calculation as well: feeding it

```
    1 0
    1 0
    1 0
    0 0
    0 0
```

produces the output

```
    xx M0 C0        1 0      yy M1 C0~2      0 0 1
    xx M1 C3        1 0      yy M2 C3~5      1 1 0
    xx M2 C6        1 0      yy M3 C6~8      0 0 1
    xx M3 C9        0 0      yy M4 C9~11     1 1 1
    xx M4 C12       0 0      yy M5 C12~14    1 1 1
```

where the last column of the simulator's output is y.

If the machine is next fed x₁[5, 10) = 11100 and x₂[5, 10) = 00000, the output will swing from 1 to 0 to 1 and back to 0, where it remains. Putting

```
    1 0
    1 0
    1 0
    0 0
    0 0
    1 0
    1 0
    1 0
    0 0
    0 0
```

into the simulator gives the result

```
    xx M0 C0        1 0      yy M1 C0~2      0 0 1
    xx M1 C3        1 0      yy M2 C3~5      1 1 0
    xx M2 C6        1 0      yy M3 C6~8      0 0 1
    xx M3 C9        0 0      yy M4 C9~11     1 1 1
    xx M4 C12       0 0      yy M5 C12~14    1 1 1
    xx M5 C15       1 0      yy M6 C15~17    1 1 0
    xx M6 C18       1 0      yy M7 C18~20    0 0 1
    xx M7 C21       1 0      yy M8 C21~23    1 1 0
    xx M8 C24       0 0      yy M9 C24~26    0 0 0
    xx M9 C27       0 0      yy M10 C27~29   0 0 0
```

just as expected.

Correct operation of this system depends critically on the proper timing of changes in the input. The input values are permitted to change at every third tick of the clock and must be held constant otherwise. The simulation code enforces this in its main loop. The behavior of the model is much more difficult to anticipate if this restriction is removed. To demonstrate this, the author has changed the main function of the simulation program to apply a new input value at every tick of the clock, rather than holding the input constant between machine cycles. The code is listed below.

## Main Program to Apply Input Immediately
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
