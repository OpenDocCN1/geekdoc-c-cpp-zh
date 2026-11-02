

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

### B.2.5 *ParSimulator* 类

*ParSimulator* 类将并行仿真算法隐藏在一个与 *Simulator* 接口非常相似的接口之后。用户可以注册一个 *EventListener*，以便在组件模型产生输出以及组件模型发生状态变化时收到通知；构造函数接受一个 *Devs* 模型，其组件根据用户偏好被分配到特定的逻辑进程，而 *execUntil* 方法运行并行算法，直到指定的结束时间。该类的实现如下。

将组件分配给 *LogicalProcesses* 是 *ParSimulator* 的主要功能之一。每个 *Devs*（原子模型和网络模型）都有一个 *setProc* 方法，建模者用它将其分配到特定线程。有效分配范围为 0 到 *omp_get_max_threads*-1。默认情况下，模型未分配，这由线程号 -1 表示。模型按深度优先附加到处理器。具有有效分配的 *Network* 会被交给相应的 *LogicalProcess*，后者接纳它及其所有组件。如果 *Network* 没有有效分配，则 *ParSimulator* 查看其子项的分配。同样，具有有效分配的 *Networks* 会被交给相应的 *LogicalProcess*；没有有效分配的 *Networks* 会被展开。然而，*Atomic* 模型总是被分配给某个 *LogicalProcess*；如果原子模型具有无效分配，则随机选择一个 *LogicalProcess*。该分配过程如图 B.8 所示。

![](img/df6085a1b35edf9c9ea818a5c66ccad9_333_0.png)

**图 B.8** 将一个网络模型分配给一组逻辑进程。树中的每个块是一个模型；叶子是原子模型，中间节点是网络。标签是处理器分配；下划线表示在分配过程中被修改的 -1。

#### *ParSimulator* 的实现

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

## B.3 古斯塔夫森定律与阿姆达尔定律的演示

当模型被划分得使信息向前流动时，保守算法效果最好。进程之间的连接理想情况下形成一棵树，数据从根节点产生并向下流向叶子节点。在这种安排下，树的每个分支都能以上游进程向其提供输入的速度执行。反馈（即树中较低层级的进程向其父进程提供信息）限制了在同时状态转换中可利用的并行性。

例如，仅考虑两个以反馈方式连接的模型。从时间零开始，假设第一个模型的前瞻量为 ε1、时间推进量为 Δt1，第二个模型分别为 ε2 和 Δt2。每个处理器的第一个动作是将其 Δt 和 ε 中较小的值发送给邻居，从而确定最早的输入时间。

首先考虑如果 ε1 < Δt1 且 ε2 < Δt2 会发生什么。两个进程都无法做任何有用的事情；每个进程仅用其邻居的 ε 更新对最早输入时间的估计。这种情况反复发生，直到累积的 ε 达到较小的 Δt，并且第一个事件最终发生。显然，没有并行完成任何有用工作，并且在处理器就下一个可执行事件的时间达成一致的过程中浪费了大量时间。这是最坏情况。

在最佳情况下，Δt1 < ε1 且 Δt2 < ε2。在这种情况下，进程交换它们的下一事件时间；如果例如 Δt2 < Δt1，则第二个处理器处的内部事件和第一个处理器处的外部事件并行执行。虽然利用了一定程度的并行性，但任何收益都可能被交换最早输出时间估计值及输出值本身所损失的时间所淹没。

考虑到这一点，基准模型体现了模型向前传递信息的理想情况。通过仔细关注如何为并行仿真划分模型，这种理想情况通常可以在实践中实现。制造问题提供了一个很好的例子。原材料进入工厂并分阶段加工。特定阶段可能会将缺陷零件送回重新加工，而通过反馈回路连接的阶段会被合并到单个逻辑进程中。这

