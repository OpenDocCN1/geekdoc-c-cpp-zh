by the model is not allocated dynamically, and so it does not need to be freed by the garbage collection method. The implementation of the *InterruptHandler* is listed below.

# Header File for the InterruptHandler

```
#ifndef INTERRUPT_HANDLER_H_
#define INTERRUPT_HANDLER_H_
#include "adevs.h"
#include "SimEvents.h"

// This is the model of the computer’s interrupt handler.
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