![](bbox=[0.18, 0.08, 0.85, 0.55])

FIGURE B.8 An assignment of a network model to a set of logical processes. Each block in the tree is a model; the leaves are atomic and intermediates are networks. The labels are processor assignments; underlining indicates a −1 that was altered during the assignment process.

```
namespace adeva
{
template <class X> class ParSimulator: public AbstractSimulator<X>
{
public:
    // Create a simulator for the model. This constructor assumes that
    // the logical processes are all connected to each other
    ParSimulator(Devs<X>* model, MessageManager<X>* msg_mgr = NULL);
    // This constructor accepts a directed graph whose edges tell the
    // simulator which processes feed input to which other processes.
    ParSimulator(Devs<X>* model, LpGraph& g,
        MessageManager<X>* msg_mgr = NULL);
    // Get the model's next event time
    double nextEventTime();
    // Run the simulator until the next event time is greater
    // than the specified value.
    void execUntil(double stop_time);
    // Delete the simulator, but leave the model intact
    ~ParSimulator();
private:
    LogicalProcess<X>** lp; // Pointers to the logical processes
    int lp_count; // Number of logical processes in lp
    MessageManager<X>* msg_manager; // For managing inter-lp events
    void init(Devs<X>* model);
    void init_sim(Devs<X>* model, LpGraph& g);
};
}
```