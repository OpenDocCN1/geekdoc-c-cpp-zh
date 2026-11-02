
because the drill does not produce an output. Case 3 of Equation 4.7 now moves the system into the state

$$\delta_{int,r}(((1, 1), 0), ((0, 2), 0)) = ((\delta_{int,m}((1, 1), 0), \delta_{ext,m}((0, 2), 1, 1), 0)) = (((0, 1), 0), ((1, 2), 0))$$

at time (1, 1) and sets e_r = 0. Case 5 finishes x_1.

The trajectory x_2 is applied next. The time advance of the assembly line is now

$$ta_r(((0, 1), 0), ((1, 2), 0)) = \min\{\infty, 2\} = 2$$

and so the input at time (1, 1) triggers an external transition, putting the system into the state

$$\delta_{ext,r}((((0, 1), 0), ((1, 2), 0)), 0, 2) = ((\delta_{ext,m}((0, 1), 0, 2), 0), ((1, 2), 0)) = (((2, 1), 0), ((1, 2), 0))$$

at time (1, 2) and setting e_r = 0. The time advance is now

$$ta_r(((2, 1), 0), ((1, 2), 0)) = \min\{1, 2\} = 1$$

Case 4 advances the time to (2, 0) and sets e_r = 1. The output of the resultant at this time is

$$\lambda_r(((2, 1), 0), ((1, 2), 0)) = \Phi$$

because the drill needs another unit of time before it produces an output. Case 3 is applied at (2, 0), and the next state is

$$\delta_{int,r}(((2, 1), 0), ((1, 2), 0)) = ((\delta_{int,m}((2, 1), 0), \delta_{ext,m}((1, 2), 1, 1), 0)) = (((1, 1), 0), ((2, 1), 0))$$

at time (2, 1) and e_r = 0. The time advance is now

$$ta_r(((1, 1), 0), ((2, 1), 0)) = \min\{1, 1\} = 1$$

and case 4 advances the time to (3, 0) and sets e_r = 1. Now the drill produces its first part, and the output of the resultant is

$$\lambda_r(((1, 1), 0), ((2, 1), 0)) = 1$$

Case 5 ends the simulation.

This recursion amply demonstrates the definition of a network, but a table-driven procedure is more practical when hand calculations are necessary. The table contains a column for time and five columns for each component. As before, proceed row by row calculating input, output, and state transition events as required. In this case, however, the x column of each component will contain contributions from the y columns of its influencers. For this purpose, it is helpful to keep the coupling diagram near at hand. A repetition of the preceding simulation using a table-driven approach is shown in Table 4.2.

**TABLE 4.2 Table-Driven Simulation of a Network of Discrete-Event Systems**

| t | **Press** s | **Press** ta(s) | **Press** y | **Press** x | **Press** type | **Drill** s | **Drill** ta(s) | **Drill** y | **Drill** x | **Drill** type |
|---|---|---|---|---|---|---|---|---|---|---|
| (0, 0) | (0, 1) | ∞ | — | 1 | in,init,0 | (0, 2) | ∞ | — | — | init,0 |
| (0, 1) | (1, 1) | 1 | — | — | ext | — | — | — | — | — |
| (1, 0) | — | — | 1 | — | out | — | — | — | 1 | in |
| (1, 1) | (0, 1) | ∞ | — | 2 | out,in | (1, 2) | 2 | — | — | ext |
| (1, 2) | (2, 1) | 1 | — | — | ext | — | — | — | — | — |
| (2, 0) | — | — | 1 | — | out | — | — | — | 1 | in |
| (2, 1) | (1, 1) | 1 | — | — | int | (2, 1) | 1 | — | — | ext |
| (3, 0) | — | — | — | 1 | out,final,1 | — | — | 1 | 1 | in,out,final,1 |

### 4.2.4 Simulating the Resultant

Just as was done in Section 3.2.4 for discrete-time systems, closure under coupling can be used to transform the simulator described in Section 4.1.8 for a single atomic model into a simulator for network models. For this purpose, four new classes are added to Figure 4.3: the Network, the Resultant, the Event, and the Set. The revised class diagram is shown in Figure 4.5.

![](img/df6085a1b35edf9c9ea818a5c66ccad9_144_0.png)

FIGURE 4.5 Class diagram of the top-down simulator for network models.

The Set, Event, and Network classes are the same ones used in the discrete time simulator; they are described in Section 3.2.4. The Event class holds input to or output from a model, and it carries these events through the Network. The Set has four essential features; elements can be added to and removed from it, it contains at most one copy of each element, and we can iterate through its elements. The Network class has two abstract methods, one for routing input and output events through the network and another for getting its set of components. The Network also has a pointer to its Resultant.

The Resultant is an atomic model that encapsulates the Network and computes the state transition, output, and time advance functions defined for it in Section 4.2.2. As with the discrete-time simulator, the calculation of input for the components proceeds forward using the set E_d of influences, rather than backward using the set I_d of influencers. The Resultant is otherwise an unadorned implementation of the time advance function (Equation 4.13), output function (Equation 4.15), and external (Equation 4.18), internal (Equation 4.17), and confluent (Equation 4.20) transition functions of the network.

The implementation of the *Resultant* is listed below. The similarity of this *Resultant* with the discrete-time resultant extends even to the reuse of code; the *route* method is the same one listed in Section 3.2.4.

### Implementation of the Resultant

```cpp
#ifndef _adevs_resultant_h
#define _adevs_resultant_h
#include "adevs_network.h"
#include <vector>

namespace adevs
{

template <typename X> class Resultant: public Atomic<X>
{
  public:
    Resultant(Network<X>* model);
    void delta_int();
    void delta_ext(double e, const Bag<X>& xb);
    void delta_conf(const Bag<X>& xb);
    void output_func(Bag<X>& yb);
    double ta();
    void gc_output(Bag<X>& gb);
    ~Resultant() { delete model; }
  private:
    Network<X>* model;
    // Structure for the state and elapsed time of the components
    struct total_state_t
    {
        double e; Atomic<X>* m;
        // The STL set needs the less than operator
        bool operator<(const total_state_t& b) const { return m < b.m; }
    };
    std::vector<total_state_t> c;
    std::map<Atomic<X>*,Bag<X> > input, output;
    void route(const X& value, Atomic<X>* source);
};

template <typename X>
Resultant<X>::Resultant(Network<X>* model):
    Atomic<X>(model->model())
{
    model->setResultant(this);
    // Get the atomic components
    Set<Atomic<X>*> ctmp; model->getComponents(ctmp);
    // Set the elapsed time to zero and save the total state
    typename Set<Atomic<X>*>::iterator iter = ctmp.begin();
    for ( ; iter != ctmp.end(); iter++) {
        total_state_t s;
        s.e = 0.0; s.m = *iter;
        c.push_back(s);
    }
}

template <typename X>
void Resultant<X>::delta_int()
{
    // Save the time advance because it will change as the state is updated
    double time_adv = ta();
    // Input for each component was computed in the output_func method and
    // so only the new states are computed here.
    for (typename std::vector<total_state_t>::iterator iter = c.begin();
            iter != c.end(); iter++) {
        // Get the bag of input for the model
        Bag<X>& xb = input[(*iter).m];
        // Is this model in IMM?
        if ((*iter).m->ta()-(*iter).e <= time_adv) {
            // Internal event if no input
            if (xb.empty()) (*iter).m->delta_int();
            // Confluent event otherwise
            else (*iter).m->delta_conf(xb);
            // Reset the elapsed time
            (*iter).e = 0.0;
        }
        // otherwise, does it have input?
        else if (!xb.empty()) {
            (*iter).m->delta_ext((*iter).e + time_adv,xb);
            (*iter).e = 0.0;
        }
        // just update the elapsed time otherwise
        else (*iter).e += time_adv;
    }
}

template <typename X>
void Resultant<X>::delta_ext(double e, const Bag<X>& xb)
{
    // Send the input to the proper components
    for (typename Bag<X>::const_iterator iter = xb.begin();
            iter != xb.end(); iter++)
        route(*iter,this);
    // Compute next state of each component
    for (typename std::vector<total_state_t>::iterator iter = c.begin();
            iter != c.end(); iter++) {
        // Get the bag of input for the model
        Bag<X>& xb = input[(*iter).m];
        // Update the elapsed time
        (*iter).e += e;
        // If it has input, apply the external transition function
        if (!xb.empty()) {
            (*iter).m->delta_ext((*iter).e,xb);
            (*iter).e = 0.0;
        }
    }
}

template <typename X>
void Resultant<X>::delta_conf(const Bag<X>& xb)
{
    // Send the input to the proper components
    for (typename Bag<X>::const_iterator iter = xb.begin();
            iter != xb.end(); iter++)
        route(*iter,this);
    // The confluent transition is the same as the internal transition
    // when the network inputs have been routed to their destinations
    delta_int();
}
```
