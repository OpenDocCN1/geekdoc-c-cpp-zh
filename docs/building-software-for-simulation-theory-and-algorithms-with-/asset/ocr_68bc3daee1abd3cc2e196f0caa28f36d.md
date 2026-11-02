```
```cpp
{
    if (event_exists) // Execute the internal event
        sys->internal_event(q_trial,event);
    // Copy the new state vector to q
    for (int i = 0; i < sys->numVars(); i++) q[i] = q_trial[i];
    tentative_step(); // Take a tentative step
}
void delta_ext(double e, const Bag<X>& xb)
{
    solver->advance(q,e); // Advance the state q by e
    sys->external_event(q_a,xb); // Compute the external event
    // Copy the new state to the tentative solution
    for (int i = 0; i < sys->numVars(); i++) q_trial[i] = q[i];
    tentative_step(); // Take a tentative step
}
void delta_conf(const Bag<X>& xb)
{
    if (event_exists) // Execute the confluent or external event
        sys->confluent_event(q_trial,xb);
    else sys->external_event(q_trial,ta(),xb);
    // Copy the new state vector to q
    for (int i = 0; i < sys->numVars(); i++) q[i] = q_trial[i];
    tentative_step(); // Take a tentative step
}
double ta() { return sigma; }
void output_func(Bag<X>& yb)
{
    if (event_exists) sys->output_func(q_trial,event,yb);
}
void gc_output(Bag<X>& gb) { sys->gc_output(gb); }
virtual ~Hybrid()
{
    delete [] q; delete [] q_trial; delete [] event;
    delete event_finder; delete solver; delete sys;
}
private:
    ode_system<X>* sys; // The ODE system
    ode_solver<X>* solver; // Integrator for the ode set
    event_locator<X>* event_finder; // Event locator
    double sigma; // Time to the next internal event
    double *q, *q_trial; // Current and tentative states
    bool* event; // Flags indicating the encountered event surfaces
    bool event_exists; // True if there is at least one event
    // Execute a tentative step and calculate the time advance function
    void tentative_step()
    {
        // Check for a time event
        double time_event = sys->time_event_func(q);
        // Integrate up to that time at most
```
```