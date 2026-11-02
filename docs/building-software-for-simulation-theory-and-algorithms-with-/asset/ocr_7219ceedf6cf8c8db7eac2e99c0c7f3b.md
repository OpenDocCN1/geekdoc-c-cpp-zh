```
```cpp
{
    internal_event(q,events);
    external_event(q,0.0,xb);
}
void output_func(const double* q, const bool* events,
        Bag<bool>& yb)
{
    assert(events[0]);
    yb.insert(!d);
}
void go_output(Bag<bool>&){}
bool getDiode() const { return d; }
bool getSwitch() const { return s; }
private:
    bool s, d;
    const double vs, C, Rs, Rl, vop, vcl;
};

class StateListener: public EventListener<bool>
{
    public:
        StateListener(Hybrid<bool>* c1, Circuit* c2): c1(c1),c2(c2){}
        void stateChange(Atomic<bool>*,double t)
        {
            cout << t << " " << c1->getState() << " " <<
                c2->getSwitch() << " " << c2->getDiode() << endl;
        }
        void outputEvent(Event<bool>,double){}
    private:
        Hybrid<bool>* c1; Circuit* c2;
};

int main()
{
    // Create the model
    Circuit* circuit = new Circuit();
    Hybrid<bool>* hybrid_model = new Hybrid<bool>(
        circuit,new coroutine_coupled_error<bool>(circuit,1E-5,0.01),
            new linear_event_locator<bool>(circuit,1E-5));
    // Create the simulator
    Simulator<bool>* sim = new Simulator<bool>(hybrid_model);
    sim->addEventListener(new StateListener(hybrid_model,circuit));
    // Simulate until the switch opens
    while (sim->nextEventTime() <= 1.0) sim->execNextEvent();
    // Open the switch
    Bag<Event<bool> > xb; xb.insert(Event<bool>(hybrid_model,0));
    sim->computeNextState(xb,1.0);
    // Simulate for another three seconds
    while (sim->nextEventTime() <= 4.0) sim->execNextEvent();
```
```