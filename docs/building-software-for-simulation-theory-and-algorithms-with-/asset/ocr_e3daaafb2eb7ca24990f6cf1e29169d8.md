```
```cpp
// Compute the next state of the model and invoke stateChange
// and outputEvent callbacks as appropriate
void computeNextState(const Bag<X>& input);
// Compute the model's output and make outputEvent callbacks
void computeOutput();
// Get the simulation time.
unsigned int getTime() { return t; }
// Add an event listener
void addEventListener(EventListener<X>* listener)
{
    listeners.push_back(listener);
}
private:
Atomic<X>* model; // The model to simulate
unsigned int t; // Simulation clock
bool output_up_to_date; // Is the model output up to date?
// List of event listeners
typedef std::list<EventListener<X>*> ListenerList;
ListenerList listeners;
};

template <typename X>
void Simulator<X>::computeNextState(const Bag<X>& input)
{
    computeOutput(); // Compute the output at time t
    t++; // Advance the simulation clock
    model->delta(input); // Compute the new state of the model
    // Notify listeners that the state has changed
    for (typename ListenerList::iterator iter = listeners.begin();
         iter != listeners.end(); ++iter)
        (*iter)->stateChange(model);
    // Cleanup
    model->gc_output(model->output_bag);
    model->output_bag.clear();
    output_up_to_date = false;
}

template <typename X>
void Simulator<X>::computeOutput()
{
    // Return if the output function has been evaluated
    if (output_up_to_date) return;
    // Compute the output
    output_up_to_date = true;
    model->output_func(model->output_bag);
    // Tell listeners about the output
    for (typename Bag<X>::iterator iter = model->output_bag.begin();
         iter != model->output_bag.end(); ++iter)
        for (typename ListenerList::iterator iter = listeners.begin();
```
```