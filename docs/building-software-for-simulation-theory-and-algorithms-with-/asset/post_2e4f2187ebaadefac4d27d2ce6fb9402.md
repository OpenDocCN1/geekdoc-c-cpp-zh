
It has two virtual methods that the `Simulator` invokes to notify the listener that an output was produced or that a state transition has taken place.

The *Atomic* class has six virtual methods. It retains the `gc_output` method that the *Simulator* uses to tell the model to delete objects it produced as output. It also retains the `output_func` method that implements the model's output function. The `delta` function of the discrete time simulator is replaced by three methods, one for each primitive transition function of the discrete event model. The `delta_int` method implements the internal transition function, the `delta_ext` method implements the external transition function, and the `delta_conf` method implements the confluent transition function. Finally, the method `ta` is added to implement the model's time advance function.

The *Simulator* retains the `addEventListener` and `computeOutput` methods of the discrete-time simulator, but where it has three methods for interacting with the simulation, the discrete-event simulator has four. Two of these methods are for obtaining information. The `nextEventTime` method returns the time of the next autonomous action. The `computeOutput` method invokes the `outputEvent` method of registered *EventListeners* to inform them of the model's output at the next event time.

The other two are for advancing the simulation clock. The `execNextEvent` method computes the output and next state of the model at the next event time, invoking the `outputEvent` and `stateChange` methods of all registered *EventListeners* as it proceeds. This method accepts no input; it executes the model's internal transition function. Input is applied with the `computeNextState` method. It accepts a `Bag` of input and the time at which to apply it, which must be less than or equal to the `nextEventTime`. At that time, an external or confluent event, as appropriate, is executed and the method notifies any *EventListeners* of the action by calling their `stateChange` and, for a confluent event, `outputEvent` methods.

Virtual methods, to be implemented by the programmer, constitute most of the simulation engine. The only class with a substantial implementation is the *Simulator*, and its implementation is shown below. Not in this implementation is the time pair (`t`, `c`). The real time `t` appears explicitly, but `c` is incremented implicitly each time `computeNextState` is called with the same argument for time. Nothing is gained by making the `c` explicit, except possibly to allow users of the *Simulator* to record the complete timestamp for each event. If this information is needed, it can be recovered with a counter that is set to zero each time the real part of the simulation clock advances and is incremented after calls to `computeNextState` that do not advance the clock.

## Implementation of the Simulator Class

```cpp
#ifndef _adevs_simulator_h_
#define _adevs_simulator_h_
#include "adevs_atom.h"
#include <cfloat>
#include <cassert>

namespace adevs
{

template <typename X> class Simulator {
    public:
        Simulator(Atomic<X>* model):
            model(model), tL(0.0),
            output_up_to_date(false){}
        void addEventListener(EventListener<X>* l)
        {
            listeners.push_back(l);
        }
        double nextEventTime() { return tN; }
        void computeNextState(const Bag<X>& input, double t);
        // Execute the autonomous event at time nextEventTime()
        void execNextEvent()
        {
            Bag<X> empty;
            computeNextState(empty,nextEventTime());
        }
        void computeNextOutput();
    private:
        Atomic<X>* model; // The model to simulate
        double tN, tL; // Time of the next and previous event
        bool output_up_to_date; // Is the output up to date?
        // List of event listeners
        typedef std::list<EventListener<X>*> ListenerList;
        ListenerList listeners;
};

template <typename X>
void Simulator<X>::computeNextState(const Bag<X>& input, double t)
{
    // If this is an external event
    if (t < tN && !input.empty()) model->delta_ext(t-tL,input);
    // If this coincides with an autonomous action
    else if (t == tN) {
        computeNextOutput();
        if (!input.empty()) model->delta_conf(input);
        else model->delta_int();
    }
    // Find the next event time
    double ta = model->ta();
    if (ta < DBL_MAX) tN = t + ta;
    else tN = DBL_MAX;
    // Set the simulation clock and notify listeners of the change in state
    tL = t;
    for (typename ListenerList::iterator iter = listeners.begin();
         iter != listeners.end(); iter++) {
        (*iter)->stateChange(model,t);
    }
    // Cleanup
    model->gc_output(model->output_bag);
    model->output_bag.clear();
    output_up_to_date = false;
}

template <typename X>
void Simulator<X>::computeNextOutput()
{
    // Return if the output function has been evaluated
    if (output_up_to_date) return;
    // Compute the output
    output_up_to_date = true;
    model->output_func(model->output_bag);
    // Notify registered listeners of the output events
    for (typename Bag<X>::iterator yiter = model->output_bag.begin();
         yiter != model->output_bag.end(); yiter++) {
        for (typename ListenerList::iterator iter = listeners.begin();
             iter != listeners.end(); iter++)
            (*iter)->outputEvent(model,*yiter,tN);
    }
}

} // end of namespace

#endif
```

## 4.1.9 Simulating the Interrupt Handler

An implementation of the interrupt handler developed in Section 4.1.6 demonstrates how the simulation software is used. The class InterruptHandler is derived from Atomic; its virtual methods are implemented to realize the model's transition functions, time advance function, and output function. Input and output to this model (and throughout the implementation of the tank; see Appendix A, Section A.2.2) are instances of the class SimEvent, which has two attributes: a union containing one of five types of specific events and a flag showing which of these types is actually present.

The interrupt handler reacts to events with the type SimMotorOnTime and produces events with the type SimInterrupt and SimMotorVoltage. The SimMotorOnTime event carries information about the ON times for the motors and the direction in which they should turn. The SimInterrupt event has no information other than its type, and the SimMotorVoltage event has the voltages at the left and right motors. Output produced by the model is not allocated dynamically, and so it does not need to be freed by the garbage collection method. The implementation of the *InterruptHandler* is listed below.

### Header File for the InterruptHandler

```cpp
#ifndef INTERRUPT_HANDLER_H_
#define INTERRUPT_HANDLER_H_
#include "adevs.h"
#include "SimEvents.h"

// This is the model of the computer's interrupt handler.
class InterruptHandler: public adevs::Atomic<SimEvent>
{
    public:
        // Phases of the interrupt handler
        typedef enum { OUTPUT, EXEC, WAIT } Phase;
        // Create an interrupt handler that executes with the
        // specified frequency.
        InterruptHandler(double freq);
        // State transition functions
        void delta_int();
        void delta_ext(double e, const adevs::Bag<SimEvent>& xb);
        void delta_conf(const adevs::Bag<SimEvent>& xb);
        // Output function
        void output_func(adevs::Bag<SimEvent>& yb);
        // Time advance function
        double ta();
        void gc_output(adevs::Bag<SimEvent>&){}
        // Methods for getting the values of the state variables
        unsigned int getCounter() const { return counter; }
        unsigned int getLeftOnTime() const { return left_on_time; }
        unsigned int getRightOnTime() const { return right_on_time; }
        bool getLeftReverse() const { return reverse_left; }
        bool getRightReverse() const { return reverse_right; }
        double getLastLeftOutput() const { return last_left_v; }
        double getLastRightOutput() const { return last_right_v; }
        double getLeftOutput() const { return left_v; }
        double getRightOutput() const { return right_v; }
        Phase getPhase() const { return phase; }
        double getInterruptPeriod() const { return interrupt_period; }
    private:
        const double interrupt_period; // Clock period
        // Magnitude of the voltage at the motor when turned on
        const double motor_voltage;
        const double execute_time; // Execution time of the interrupt
        double ttg; // Time to the next internal event
        unsigned char counter, left_on_time,
                      right_on_time; // On/off counters
```
