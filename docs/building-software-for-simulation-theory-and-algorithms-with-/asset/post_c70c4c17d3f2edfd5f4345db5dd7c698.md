
```cpp
private:
    const Computer* computer;
    ofstream vout;
};

int main(int argc, char** argv)
{
    // Get the parameters for the experiment from the command line
    if (argc != 4) {
        cout << "freq left_throttle right_throttle" << endl;
        return 0;
    }
    // Get the frequency of the voltage signal from the first argument
    double freq = atof(argv[1]);
    // Create a command from the driver that contains the duty ratios and
    // directions.
    SimPacket sim_command;
    sim_command.left_power = atof(argv[2]);
    sim_command.right_power = atof(argv[3]);
    // Create computer, simulator, and event listener.
    Computer* computer = new Computer(freq);
    Simulator<SimEvent>* sim = new Simulator<SimEvent>(computer);
    ComputerListener* l = new ComputerListener(computer);
    // Add an event listener to plot the voltage signals
    sim->addEventListener(l);
    // Inject the driver command into the simulation at time 0
    Bag<Event<SimEvent> > input;
    SimEvent cmd(sim_command);
    Event<SimEvent> event(computer, cmd);
    input.insert(event);
    sim->computeNextState(input, 0.0);
    // Run the simulation
    while (sim->nextEventTime() <= 0.004)
        sim->execNextEvent();
    // Clean up and exit
    delete sim; delete computer; delete l;
    return 0;
}
```

## 4.5 CELLULAR AUTOMATA REVISITED

This chapter began with a statement that discrete-event simulations are a generalization of discrete-time systems. The cellular automata constructed in Section 3.5 will demonstrate this fact. Let T(l, c, r) be the cell's transition rule, which maps its present state c and states of its left l and right r neighbors into a new state.

![](img/df6085a1b35edf9c9ea818a5c66ccad9_188_0.png)

**FIGURE 4.12** Output of the computer in response to a packet that sets a 50% duty ratio for the right motor and 75% for the left motor. The frequency of the computer’s clock is 7.4 kHz.

Consider the discrete-event system

$$S = \{0, 1\}$$

$$X = Y = S \times \mathbb{N}$$

$$\delta_{int}(s) = s$$

$$\delta_{ext}(s, e, \{(b_l, k - 1), (b_r, k + 1)\}) = T(b_l, s, b_r)$$

$$\delta_{con}(s, x^b) = \delta_{ext}(s, 0, x^b)$$

$$\lambda(s) = (s, k)$$

$$ta(s) = 1$$

which models a cell at location $k$. For the moment, assume that each cell begins with its elapsed time equal to 1. If $N$ of these cells are connected to identical neighbors, differing only in $k$, to form a ring, then the output trajectories have nonevents except at $t = (m, 0)$, where $m \in \mathbb{N}$. Likewise, the input trajectories are $\Phi$ except at $t = (m, 0)$, where their values are $\{(b_r, k + 1), (b_l, k - 1)\}$ for $k \in [1, N - 1]$; for the cell at $k = 1$, the input values arrive from $N$ and 2; similarly for the cell at $k = N$. The state trajectories change in the discrete instant following an input, that is, from state $s$ at $t = (m, 0)$ to state $T(b_l, s, b_r)$ at $(m, 1)$.

The discrete-time cell is quite similar in form. It has identical sets of states, inputs, and outputs; an identical output function; and the state transition function is

$$\delta(s, \{(b_l, k - 1), (b_r, k + 1)\}) = T(b_l, s, b_r) \tag{4.21}$$

This is precisely what was rendered in code in Section 3.5.

It is intuitively obvious that the discrete-event cell mimics its discrete-time counterpart; we now proceed to establish this in a formal way. The function $\bar g$ maps a discrete-time trajectory $x_d[m,m+1)$ to an event trajectory $x_e((m,0),(m+1,0))$ by assigning $x_d(m) \to x_e((m,0))$ and $x_d(t) = \Phi$ for all $t \in ((m,1),(m+1,0))$. The function $\bar h$ takes the total state $(s,1)$ of the discrete-event system to the state $s$ of the discrete-time system. Letting $\delta_d$ and $\delta_e$ be the single-step state transition functions for the discrete-time and discrete-event models (i.e., as in Equations 3.8 and 4.7), respectively, and $\lambda$ (from above) and $\Lambda$ (Equation 4.10) be the output functions of the discrete-time and discrete-event systems, respectively, two facts are readily verified:

- 1. $\bar h(\delta_e((s,1), \bar g(x_d))) = \delta_d(\bar h((s,1)), x_d)$
- 2. $\Lambda((s,1)) = \lambda(\bar h((s,1)))$

This establishes a homomorphic mapping of the discrete-event system to the discrete-time system (this is an I/O system homomorphism [157]). Informally, the discrete-event system begun in total state $(s,1)$ has all the capabilities of the discrete-time system started in state $s$. Moreover, because the structure of the discrete-time and discrete-event networks are identical, the discrete-event cellular automaton is a componentwise reproduction of the discrete-time automaton. A discrete-event automaton, however, can do much more than its discrete-time counterpart. The elapsed time need not be uniform across the space of cells, and if some variety is allowed, this produces asynchronous cellular automata, which are a subject of considerable interest in biology and the social sciences (see, e.g., Refs. 13, 28, 55, 129, and 134).

To illustrate, consider trajectories produced by a ring composed of the asynchronous cell listed below. The cells are left-looking (oriented toward the left); the transition rule is $T(b_l, s, b_r) = b_l$. Moreover, each cell is allowed a separate time advance and so they must record the previous output of the left neighbor to have it available when a state transition occurs. Each cell begins, as required by our simulation software, with an elapsed time of zero. The initial state of the cells alternates between 0, colored black, and 1, colored white. Note that in the figures the cells are arranged from top to bottom and time moves from left to right; this is not the visual arrangement used in Section 3.5.

### Left-Looking Event Cell

```cpp
#ifndef LookLeft_h_
#define LookLeft_h_
#include "adevs.h"

#define BLACK 0
#define WHITE 1

// A left looking event automaton. The CellEvent structure
// contains an integer that is the cell's position and
// another integer that has its state.
class LookLeft: public adevs::Atomic<adevs::CellEvent<int> >
{
public:
    // Constructor puts the cell into its initial state of
    // black if the location is even and white otherwise
    LookLeft(int width, int location, double P):
        adevs::Atomic<adevs::CellEvent<int> >(),
        location(location), width(width), P(P)
    {
        s = l = WHITE;
        // We have a state 0
        if (location % 2 == 0) s = BLACK;
        else l = BLACK; // or our neighbor does
        c = 0.0;
    }
    void delta_int() { c = 0.0; s = l; }
    void delta_ext(double e, const adevs::Bag<adevs::CellEvent<int> >& xb)
    {
        c += e;
        l = (*xb.begin()).value;
    }
    void delta_conf(const adevs::Bag<adevs::CellEvent<int> >& xb)
    {
        delta_int();
        delta_ext(0.0, xb);
    }
    double ta() { return P - c; }
    // Output function
    void output_func(adevs::Bag<adevs::CellEvent<int> >& yb)
    {
        adevs::CellEvent<int> y;
        y.x = (location + 1) % width;
        y.value = s;
        yb.insert(y);
    }
    // The gc method is not needed
    void gc_output(adevs::Bag<adevs::CellEvent<int> >&) {}
    // Get the location of the cell
    int getLocation() const { return location; }
    // Get the state of the cell
    int getState() const { return s; }
private:
    int s, l; // Own and left neighbor's discrete state
    double c; // Time spent in own, current discrete state
    const int location, width; // Our position in the space and its size
    const double P; // Time interval between changes of s
};

#endif
```

![](img/df6085a1b35edf9c9ea818a5c66ccad9_191_0.png)

(a) Discrete variable

![](img/df6085a1b35edf9c9ea818a5c66ccad9_191_1.png)

(b) Elapsed time

**FIGURE 4.13** Trajectory of the left-looking automaton with the time advance of each cell selected at random from 1/2, 1/3, and 1: (a) discrete variable; (b) elapsed time.

Figure 4.13 shows 125 units of time for this model with the time advance of each cell selected at random from 1/2, 1/3, and 1. The trajectory initially appears to be irregular, but at the sixth set of bands settles into a recognizable pattern. The elapsed time for each component is periodic as well. Indeed, the individual components return simultaneously to zero every unit of real time. Moreover, the number of discrete states is finite and must also repeat. It follows that the total state trajectory of the resultant of this network is periodic: the observed repetitions in the discrete state persist indefinitely.

If, however, the time advance is fixed at 1 then a discrete-time system emerges once again. The initial chaos (but ultimate order) produced by an irregular time advance vanishes, replaced by a simple arrangement that translates colors to the left at each step. Figure 4.14 shows 125 steps of this arrangement. The periodicity of this cellular automaton is immediately apparent, and the close connection between discrete-event and discrete-time systems is vividly revealed.

## 4.6 SUMMARY

Just as discrete-time systems are derived by application of the semigroup property to sequences, this chapter has derived discrete-event systems by its application to event
