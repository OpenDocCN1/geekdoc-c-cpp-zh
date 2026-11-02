
```text
1  procedure route(parent,d,y^b)
2  foreach d' ∈ E_d do
3      d' is an atomic component of parent
4      if d' is atomic then
5          x_{d'}^b ← x_{d'}^b ∪ z_{d,d'}(y^b)
6      d' is a network component of parent
7      else if d' ≠ parent then
8          route(d',d,z_{d,d'}(y^b))
9      else if this is an output from parent
10     else if d' = parent and PARENT(d') exists then
11         route(PARENT(d'),d',z_{d,d'}(y^b))
12     end
13 end
```

**Algorithm 3.6** Procedure to route input and output within a network model. The set E_d of influencees and coupling functions z_{d,d'} belong to the network parent.

The other two parts of the routing problem—putting input into a network model and observing output from a network model—are conveniently solved by Algorithm 3.6. An input x^b is injected into a network N by calling route with N for the first and second arguments (i.e., parent = d = N) and x^b for the third argument. A network model produces an output whenever the third condition is true (i.e., the “output from parent” condition), and EventListeners registered with the Simulator are notified when this occurs.

Algorithm 3.7 describes the complete simulation procedure. It applies an input trajectory x < t_0, t_n > to a network N with a set of atomic components A_N. For each component d ∈ A_N there is a bag x^b_d of input and its state s_d. Notifications for EventListeners have been omitted even though they will appear in the implementation.

```text
1  for t_k ∈ < t_0, t_n > do
2      Clear the bags of input
3      foreach d ∈ A_N do
4          x_{d}^b ← ∅
5      end
6      Route the input to N
7      route(N,N,x(t_k))
8      Compute and route output from the components
9      foreach d ∈ A_N do
10         route(PARENT(d),d,z_{d,d}(s_d))
11     end
12     Change the state of the components
13     foreach d ∈ A_N do
14         s_d ← δ_d(s_d, x_d^b)
15     end
16 end
```

**Algorithm 3.7** Bottom-up simulation algorithm for a discrete-time model.

The classes that implement the bottom-up simulator are nearly the same as those used by the top-down simulator. The *Resultant*, which isn’t necessary, is eliminated. One new class, the *Diss* class, is added, and the *Atomic* and *Network* classes are modified to inherit from it. The *Diss* class holds two pieces of information: the parent of the model and the type of the model. The parent field of the *Diss* class is used to implement the PARENT function. The type information is used by the route procedure and to initialize the simulation engine⁴. The *Network* and *Atomic* classes are otherwise unchanged.

The *Event* class does not require any modification, but we have an opportunity to usefully expand the capability of the *EventListener* class. The simulator, now aware of every event as it moves through the couplings of the network, can inform the listener of every output of every atomic and network model. Likewise, the listener can be informed of changes to the state of every atomic model. This significantly expands the ability of an *EventListener* to observe, report, record, and visualize the operation of a large model. The *outputEvent* method of the new *EventListener* accepts an *Event* that carries the model, network or atomic, that produced the output and the output itself.

There is a similar opportunity to expand the capability of the *Simulator* class by allowing its clients to inject input directly into any component of a multicomponent model. This is an essential capability for building interactive simulations and for integrating the simulator into multisimulator federations. The *computeNextState* method of the new *Simulator* accepts a *Bag* of *Event* objects. Each *Event* in the *Bag* holds a model and an input for that model. If the model is atomic, then the input is put into its bag of inputs. If the target is a network, then Algorithm 3.6 is used to deliver the input to the proper set of atomic models.

The revised class diagram is shown in Figure 3.7, from which the implementations of the *Diss*, *Network*, *Atomic*, *Event*, and *EventListener* classes are easily inferred. The *Event* class has two fields and methods for setting and accessing them. The *EventListener* is a pure virtual class and has no implementation, just a definition. The *Diss* class contains its parent, methods for setting and getting the parent, and the virtual *typeIsNetwork* and *typeIsAtomic* methods; these are implemented by the *Network* and *Atomic* classes. The *Network* class returns itself when *typeIsNetwork* is called and NULL when *typeIsAtomic* is called. The *Atomic* class does the opposite.

The *Simulator* class is the only one with a substantial implementation. It implements Algorithm 3.7 with the small modifications discussed above to permit a client of the simulator to inject input into any component and to notify listeners when a component produces output or changes state. Algorithm 3.6 is used to move events through the model. The source code for the *Simulator* is listed below.

![](img/df6085a1b35edf9c9ea818a5c66ccad9_92_0.png)

**FIGURE 3.7** Class diagram of the bottom-up simulation engine for discrete-time systems.

## General Simulator for a Discrete-Time Model

```cpp
1 #ifndef _dtss_simulator_h_
2 #define _dtss_simulator_h_
3 #include "dtss_models.h"
4 #include <ostream>
5
6 namespace dtss
7 {
8
9 template <typename X> class Simulator {
10 public:
11   // Create a simulator for the supplied model
12   Simulator(Dtss<X>* model);
13   // Compute the next state of the model and invoke callbacks
14   void computeNextState(const Bag<Event<X> >& input);
15   // Compute the model's output and make outputEvent callbacks
16   void computeOutput();
17   // Get the simulation time.
18   unsigned int getTime() { return t; }
19   // Add an event listener
20   void addEventListener(EventListener<X>* listener) {
21     listeners.push_back(listener);
22   }
23 private:
24   Set<Atomic<X>*> atomics; // The complete set of atomic models
25   unsigned int t; // Simulation clock
26     bool output_up_to_date; // Is the model output up to date?
27     // List of event listeners
28     typedef std::list<EventListener<X>*> ListenerList;
29     ListenerList listeners;
30     // Get all of the children belonging to a network
31     void getAllChildren(Network<X>* model, Set<Atomic<X>*>& s);
32     // Move an input or output value to its destination
33     void route(Network<X>* parent, Dtss<X>* src, const X& x);
34     // Tell all EventListeners about an output
35     void notify_output_listeners(Dtss<X>* model,
36                                  const X& value, unsigned int t);
37 };
38
39 template <typename X>
40 Simulator<X>::Simulator(Dtss<X>* model):
41     t(0),output_up_to_date(false)
42 {
43     // If this is an atomic model then it is the only
44     // atomic model to simulate
45     if (model->typeIsAtomic() != NULL)
46         atomics.insert(model->typeIsAtomic());
47     // Otherwise get all of the atomic models by recursion
48     else getAllChildren(model->typeIsNetwork(),atomics);
49 }
50
51 template <typename X>
52 void Simulator<X>::computeNextState(const Bag<Event<X> >& input)
53 {
54     // Compute the output at time t
55     computeOutput();
56     // Deliver the injected input
57     for (typename Bag<Event<X> >::iterator iter = input.begin();
58          iter != input.end(); iter++) {
59         if ((*iter).model->typeIsAtomic()) {
60             (*iter).model->typeIsAtomic()->input_bag.insert((*iter).value);
61         }
62         else {
63             route((*iter).model->typeIsNetwork(),(*iter).model,(*iter).value);
64         }
65     }
66     // Advance the simulation clock
67     t++;
68     // Update the state of every atomic component
69     for (typename Set<Atomic<X>*>::iterator aiter = atomics.begin();
70          aiter != atomics.end(); aiter++) {
71         // Compute the new state of the model
72         (*aiter)->delta((*aiter)->input_bag);
73         // Notify listeners that the state has changed
74         for (typename ListenerList::iterator liter = listeners.begin();
```
