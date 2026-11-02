
![](img/df6085a1b35edf9c9ea818a5c66ccad9_337_0.png)

FIGURE B.9 The benchmark model with nine servers in three lines and its partitioning for three processors. The box labels indicate the model's class.

remaining stages constitute serial or parallel flows of material. Doing this necessarily restricts the number of processors that can be usefully exploited, and the benchmark reflects this fact. We will consider a small number of processors and a relatively large problem, an ideal circumstance for showing Gustafson's law applied to simulations executing on a multicore workstation.

The benchmark model is a queuing network constructed from atomic models that contain a queue and a server with a first-come, first-served policy. The servers have a processing time of 1 + r seconds, where r is exponentially distributed with a mean of one second. These form N serial arrangements of Q servers each. The lines of servers are fed by a single generator that produces a new job every 2/N seconds and chooses at random one of the N lines of servers to process it. This ensures that, on average, each line of queues receives a job every two seconds. The output from the lines of servers arrive at a collector, which counts the finished jobs as they arrive. The model is illustrated in Figure B.9.

The model is partitioned for P processors in the following way. The generator and ⌊N/P⌋ of the lines of servers are assigned to the first processor. Processors 2,..., P − 1 each get ⌊N/P⌋ lines of servers, and processor P gets the collector and the lines of servers that remain. With this partitioning, processor 1 provides input to 2,..., P, and processors 1,..., P − 1 provide input to P. A partitioning of three lines of servers is illustrated in Figure B.9. The generator, which is input-free, and the collector, which is output-free, each have infinite lookahead. The individual servers have a lookahead of 1, and each line of Q servers therefore has a lookahead of Q. The lines are arranged in parallel, and so each processor can conservatively estimate its lookahead as Q. In fact, the first processor, which has the generator, has infinite lookahead and likewise the last processor, which contains the collector.

![](img/df6085a1b35edf9c9ea818a5c66ccad9_338_0.png)

**FIGURE B.10** Execution time of the benchmark as a function of size and the number of processors used: (a) execution times; (b) closeup view of part (a) illustrating Gustafson's and Amdahl's laws.

The servers with queues, the lines of servers, the generator, and the collector differ only minimally from the discrete-event models that we have seen so far; they are implemented by the *Sq*, *Q1*, *Genr*, and *Collector* classes, respectively. The *Qn* class, which connects these components and assigns them to processors, and the *main* function, which creates and executes the parallel simulator, show how the new elements of the simulation engine are used. The code for this is listed below.

This benchmark can be scaled in three dimensions: the number *N* of lines of servers, the number *Q* of queues and servers in each line, and the simulation ending time *T*. In this instance, the model is set up with N = Q and T = 3N; so a problem of size 100 has N = Q = 100 and T = 300. The choice of N = Q is arbitrary. Using T = 3N ensures that some of the jobs arrive at the collector before the simulation terminates. What is important is that, as Gustafson's law requires, the parallel part of the simulation grows with its size while the serial part remains essentially unchanged.

Therefore, as the size of the model grows, we can maintain a reasonable execution time by using a larger computer.

Figure B.10 confirms our expectations. These results were produced with a four-core Intel processor. A critical feature of this plot is the horizontal line connecting equal execution times using one, two, three, and four cores. The parallel fraction of the program grows with the size of the problem, and the trend predicted by Gustafson's law is unmistakable: the speedup, although not ideal, is steady when the number of processors matches the size of the problem. Amdahl's law can also be seen in this plot: the vertical line connecting the execution times for a fixed-size simulation shows diminishing returns. This experiment reinforces the argument with which the chapter began. Parallel computers are marginally useful for speeding up small problems but are very good for maintaining a reasonable execution time as the simulation grows.

### Main Function for the Benchmark Program

```cpp
#include "Qn.h"
#include "adevs_par_simulator.h"
#include <iostream>

using namespace adevs;
using namespace std;

int main(int argc, char** argv)
{
    if (argc < 4) {
        cerr << "Need # queues, # lines, and end time" << endl;
        return 0;
    }
    if (argc == 5)
        cout << "Using " << omp_get_max_threads() << " threads" << endl;
    int queues = atoi(argv[1]);
    int lines = atoi(argv[2]);
    double tend = atof(argv[3]);
    LpGraph lpg;
    Qn* model = new Qn(queues,lines,lpg);
    AbstractSimulator<int>* sim;
    if (argc == 5) sim = new ParSimulator<int>(model,lpg);
    else sim = new Simulator<int>(model);
    sim->execUntil(tend);
    delete sim; delete model;
    return 0;
}
```

### Qn Class for the Benchmark Program

```cpp
#ifndef _Qn_h_
#define _Qn_h_
#include "adevs.h"
#include "Genr.h"
#include "Sq.h"
#include <iostream>

class Qn: public adevs::Network<int>
{
public:
    // Create a model with s lines of q servers. The arrangement
    // of the logical processes is returned via the supplied LpGraph.
    Qn(int q, int s, adevs::LpGraph& lpg):
        adevs::Network<int>(qcount(s), ql(new Q1*[s]),
                            genr(double(s)/2.0), collect())
    {
        int thrds = omp_get_max_threads(); // Get the number of threads
        genr.setParent(this); // The generator goes to process zero
        genr.setProc(0);
        collect.setParent(this); // Collector goes on the last process
        collect.setProc(thrds-1);
        // The queues are split among all the processes
        for (int i = 0; i < qcount; i++)
        {
            ql[i] = new Q1(q);
            ql[i]->setParent(this);
            ql[i]->setProc(i%thrds);
        }
        // Add 0->[1,thrds) to the LpGraph. This connects the
        // generator to everyone.
        for (int i = 1; i < thrds; i++) lpg.addEdge(0,i);
        // Add [0,thrds-1]->thrds-1 to the LpGraph. This connects
        // everyone to the collector.
        for (int i = 0; i < thrds-1; i++) lpg.addEdge(i,thrds-1);
    }
    void getComponents(adevs::Set<adevs::Devs<int>*>& c)
    {
        for (int i = 0; i < qcount; i++) c.insert(ql[i]);
        c.insert(&genr); c.insert(&collect);
    }
    void route(const int &value, adevs::Devs<int> *model,
               adevs::Bag<adevs::Event<int> > &r)
    {
        if (model == &genr)
            r.insert(adevs::Event<int>(ql[value%qcount],value));
        else r.insert(adevs::Event<int>(&collect,value));
    }
    ~Qn()
    {
        // Delete the components of the model
        for (int i = 0; i < qcount; i++) delete ql[i];
        delete [] ql;
    }
private:
    const int qcount;
    Q1** ql;
    Genr genr;
    Collector collect;
};
#endif
```

## APPENDIX C

## MATHEMATICAL TOPICS

### C.1 SYSTEM HOMOMORPHISMS

A morphism is a mapping from one system to another. When such a mapping exists, one system, the “big” system, is capable of doing all the essential work of another system, the “small” system. If the mapping is reversible, so that the small and big systems can change places, then the two systems are in fact identical except for the renaming and, possibly, a reversible recombination of their input, output, and state variables. A homomorphism is a mapping from big system to a small system that loses some information about the big system. The small system, in this case, does less than the big system, and the mapping is not reversible. If the mapping is reversible, then it is an isomorphism and the systems involved are interchangeable.

A trivial example will introduce the idea in an intuitive way. Consider first a discrete-time system (see Chapter 3) with a single state, single input, and single output; call this system A. Any other discrete-time system, call it B, is capable of mimicking A as follows. Let the entire set of states of B be mapped to the single state of A, and likewise with B’s set of outputs. A’s single input is mapped to any input of B, which in particular does not matter. Now the input for A is fed, via the mapping, into B. In response, B changes state and produces an output, and this action, observed through the lens of the morphism, looks exactly like the response of A: B remains in its single state (as seen through the mapping) and produces its single output (again, as seen through the mapping). This is a trivial example of a homomorphism. If B has only a single state, input, and output to begin with, then A and B are trivially isomorphic.
