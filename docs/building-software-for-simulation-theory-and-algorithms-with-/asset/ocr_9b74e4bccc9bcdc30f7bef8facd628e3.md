time T. In this instance, the model is set up with N = Q and T = 3N; so a problem of size 100 has N = Q = 100 and T = 300. The choice of N = Q is arbitrary. Using T = 3N ensures that some of the jobs arrive at the collector before the simulation terminates. What is important is that, as Gustafson's law requires, the parallel part of the simulation grows with its size while the serial part remains essentially unchanged.

Therefore, as the size of the model grows, we can maintain a reasonable execution time by using a larger computer.

Figure B.10 confirms our expectations. These results were produced with a four-core Intel processor. A critical feature of this plot is the horizontal line connecting equal execution times using one, two, three, and four cores. The parallel fraction of the program grows with the size of the problem, and the trend predicted by Gustafson's law is unmistakable: the speedup, although not ideal, is steady when the number of processors matches the size of the problem. Amdahl's law can also be seen in this plot: the vertical line connecting the execution times for a fixed-size simulation shows diminishing returns. This experiment reinforces the argument with which the chapter began. Parallel computers are marginally useful for speeding up small problems but are very good for maintaining a reasonable execution time as the simulation grows.

# Main Function for the Benchmark Program

```
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
```