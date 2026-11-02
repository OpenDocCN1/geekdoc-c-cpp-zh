
```cpp
}
private:
    omp_lock_t lock; // Lock to protect qshare and qshare_empty
    std::list<Message> *q1, *q2; // The lists themselves
    std::list<Message> **qsafe, **qshare; // Roles for q1 and q2
    volatile bool qshare_empty; // Is qshare empty?
};

} // end of namespace

#endif
```

### B.2.5 The *ParSimulator*

The *ParSimulator* class hides the parallel simulation algorithm behind an interface that closely resembles the *Simulator* interface. The user can register an *EventListener* to be notified when output is produced by and state changes occur in the component models; the constructor accepts a *Devs* model whose components are assigned to specific logical processes in accordance with the user preferences, and the *execUntil* method runs the parallel algorithm until a specified end time. The implementation of this class is listed below.

The assignment of components to *LogicalProcesses* is one of the main functions of the *ParSimulator*. Each *Devs*, atomic and network, has a *setProc* method that is used by the modeler to assign it to a specific thread. Valid assignments are in the range of 0 to *omp_get_max_threads*-1. By default, a model is unassigned and this is indicated by a thread number of -1. Models are attached to processors depth first. A *Network* with a valid assignment is given to the appropriate *LogicalProcess*, which adopts its and all of its components. If the *Network* does not have a valid assignment, then the *ParSimulator* looks at the assignments of its children. Again, *Networks* with a valid assignment are given to the appropriate *LogicalProcess*; those without a valid assignment are expanded. An *Atomic* model, however, is always assigned to some *LogicalProcess*; if the atomic model has an invalid assignment, then a *LogicalProcess* is selected at random. This assignment process is illustrated in Figure B.8.

![](img/df6085a1b35edf9c9ea818a5c66ccad9_333_0.png)

**FIGURE B.8** An assignment of a network model to a set of logical processes. Each block in the tree is a model; the leaves are atomic and intermediates are networks. The labels are processor assignments; underlining indicates a -1 that was altered during the assignment process.

#### Implementation of the *ParSimulator*

```cpp
#ifndef __adevs_par_simulator_h_
#define __adevs_par_simulator_h_
#include "adevs_abstract_simulator.h"
#include "adevs_msg_manager.h"
#include "adevs_lp.h"
#include "adevs_lp_graph.h"
#include <cassert>
#include <cstdlib>
#include <iostream>
#include <vector>

namespace adevs
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

template <class X>
ParSimulator<X>::ParSimulator(Devs<X>* model, MessageManager<X>* msg_mngr):
    AbstractSimulator<X>(),msg_manager(msg_mngr)
{
    // Create an all to all coupling of logical processes in place of
    // the LpGraph not provided by the user
    lp_count = omp_get_max_threads();
    LpGraph g;
    for (int i = 0; i < lp_count; i++)
    {
        for (int j = 0; j < lp_count; j++)
        {
            if (i != j)
            {
                g.addEdge(i,j);
                g.addEdge(j,i);
            }
        }
    }
    init_sim(model,g); // Initialize the simulator
}

template <class X>
ParSimulator<X>::ParSimulator(Devs<X>* model, LpGraph& g,
    MessageManager<X>* msg_mngr):
    AbstractSimulator<X>(),msg_manager(msg_mngr)
{
    init_sim(model,g); // Initialize the simulator
}

template <class X>
void ParSimulator<X>::init_sim(Devs<X>* model, LpGraph& g)
{
    // Create a default manager if one was not provided
    if (msg_manager == NULL) msg_manager = new NullMessageManager<X>();
    lp_count = omp_get_max_threads(); // One logical process per thread
    lp = new LogicalProcess<X>*[lp_count]; // Allocate the lp array
    // Create the logical processes; IDs are the array positions
    for (int i = 0; i < lp_count; i++)
        lp[i] = new LogicalProcess<X>(i,g.getE(i),g.getE(i),lp,
            this,msg_manager);
    init(model); // Partition the model for simulation by the processes
}

template <class X>
double ParSimulator<X>::nextEventTime()
{
    // Calculate the time of the next event as the smaller of the
    // next event times of the logical processes
    Time tN = Time::Inf();
    for (int i = 0; i < lp_count; i++)
    {
        if (lp[i]->getNextEventTime() < tN)
            tN = lp[i]->getNextEventTime();
    }
    return tN.t;
}

template <class X>
ParSimulator<X>::~ParSimulator()
{
    for (int i = 0; i < lp_count; i++)
        delete lp[i]; // Delete the logical processes
    delete [] lp; // Delete the array that held them
    delete msg_manager; // Delete the message manager
}

template <class X>
void ParSimulator<X>::execUntil(double tstop)
{
    // Create a separate thread for each logical process and execute
    // until the simulation stop time is reached
    #pragma omp parallel
    {
        lp[omp_get_thread_num()]->run(tstop);
    }
}

template <class X>
void ParSimulator<X>::init(Devs<X>* model)
{
    // If the model wants a process that exists, then do the assignment
    if (model->getProc() >= 0 && model->getProc() < lp_count)
    {
        lp[model->getProc()]->addModel(model);
        return;
    }
    // Otherwise, try to place it
    Atomic<X>* a = model->typeIsAtomic();
    if (a != NULL) // Atomic models are assigned at random
    {
        int lp_assgn = a->getProc();
        if (lp_assgn < 0 || lp_assgn >= lp_count)
            lp_assgn = ((long int)a)%lp_count;
        lp[lp_assgn]->addModel(a);
    }
    // The components of a network model are recursively assigned
    else
    {
        Set<Devs<X>*> components;
        model->typeIsNetwork()->getComponents(components);
        typename Set<Devs<X>*>::iterator iter = components.begin();
        for ( ; iter != components.end(); iter++) init(*iter);
    }
}
} // End of namespace
#endif
```

## B.3 DEMONSTRATION OF GUSTAFSON'S AND AMDAHL'S LAWS

The conservative algorithm works best when the model is partitioned such that information flows forward. The connections between processes ideally form a tree with data originating at the root and flowing down to the leaves. With this arrangement, each branch of the tree can be executed as quickly as the upstream process provides input to it. Feedback, by which a process at a lower level in the tree feeds information to its parent, limits the exploitable parallelism in simultaneous state transitions.

For example, consider just two models connected in a feedback arrangement. Beginning at time zero, suppose that the first model has a lookahead ε1 and time advance of Δt1 and the second model of ε2 and Δt2, respectively. The first act of each processor is to send the smaller of its Δt and ε to its neighbor and thereby establish the earliest input times.

Consider first what happens if ε1 < Δt1 and ε2 < Δt2. Neither process can do anything useful; each merely updates its estimate of the earliest input time by the ε of its neighbor. This happens again and again until the accumulated εs reach the smaller of the Δts and the first event finally occurs. Clearly, no useful work is done in parallel and substantial time is wasted while the processors agree on the time of the next executable event. This is the worst-case scenario.

In the best circumstances, Δt1 < ε1 and Δt2 < ε2. In this case, the processes exchange their next event times and if, say, Δt2 < Δt1, the internal event at the second processor and external event at the first processor are executed in parallel. Some small amount of parallelism is exploited, but any benefit is likely overwhelmed by time lost to the exchange of estimates for the earliest output times and the output values themselves.

With this in mind, the benchmark model embodies the ideal case where models feed information forward. With careful attention to how the model is partitioned for parallel simulation, this ideal can often be realized in practice. Manufacturing problems provide a good example. Raw material enters a plant and is processed in stages. Specific stages may send defective parts back for reprocessing, and the stages connected by feedback loops are incorporated into a single logical process. The
