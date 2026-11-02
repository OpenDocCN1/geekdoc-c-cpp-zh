
```cpp
114 template <typename X>
115 void Resultant<X>::output_func(Bag<X>& yb)
116 {
117   // Compute the output of each component and
118   // send those outputs to their destinations
119   for (typename std::vector<total_state_t>::iterator iter = c.begin();
120        iter != c.end(); iter++) {
121     // If this model is in the set IMM
122     if ((*iter).m->ta()-(*iter).e < ta()) {
123       Bag<X>& y = output[(*iter).m];
124       (*iter).m->output_func(y);
125       for (typename Bag<X>::iterator y_iter = y.begin();
126            y_iter != y.end(); y_iter++)
127         route(*y_iter,(*iter).m);
128     }
129   }
130   // Copy the network output to yb
131   Bag<X>& y = output[this];
132   for (typename Bag<X>::iterator iter = y.begin();
133        iter != y.end(); iter++)
134     yb.insert(*iter);
135 }
136
137 template <typename X>
138 double Resultant<X>::ta()
139 {
140   double min_to_go = DBL_MAX;
141   for (typename std::vector<total_state_t>::iterator iter = c.begin();
142        iter != c.end(); iter++) {
143     min_to_go = std::min((*iter).m->ta()-(*iter).e,min_to_go);
144   }
145   return min_to_go;
146 }
147
148 template <typename X>
149 void Resultant<X>::gc_output(Bag<X>& gb)
150 {
151   // Let the components clean up their output
152   for (typename std::vector<total_state_t>::iterator iter = c.begin();
153        iter != c.end(); iter++) {
154     (*iter).m->gc_output(output[(*iter).m]);
155     // Clear the output bag for the component
156     output[(*iter).m].clear();
157     // Clear the input bag for the component
158     input[(*iter).m].clear();
159   }
160   // Clear the input and output bag for the resultant
161   input[this].clear();
162   output[this].clear();
163 }

template <typename X>
void Resultant<X>::route(const X& value, Atomic<X>* source)
{
    Bag<Event<X> > r;
    model->route(value,source,r);
    for (typename Bag<Event<X> >::const_iterator iter = r.begin();
        iter != r.end(); iter++) {
        // If this is an output from the network
        if ((*iter).model == this) output[this].insert((*iter).value);
        // otherwise it goes to an internal component
        else input[(*iter).model].insert((*iter).value);
    }
} // end of namespace
#endif
```

冲压机和钻床将演示如何使用仿真引擎。机器模型的实现如下所示。这段代码对应第 4.2.3 节给出的定义。构造函数接受用于区分钻床和冲压机的处理时间 t_m，并将初始状态设置为 p = 0 和 σ = t_m。还要注意，delta_conf 方法利用了如下事实：δ_con,m(s, q) = δ_ext,m(δ_int,m(s), 0, q)。

装配线的实现也列在下面，它反映了图 4.4。

### 机器模型的实现

```cpp
#ifndef Machine_h_
#define Machine_h_
#include "adevs.h"

class Machine: public adevs::Atomic<int>
{
public:
    Machine(double tm):
        adevs::Atomic<int>(), tm(tm), sigma(tm), p(0) {}
    void delta_int() { p--; sigma = tm; }
    void delta_ext(double e, const adevs::Bag<int>& xb)
    {
        if (p > 0) sigma -= e;
        else sigma = tm;
        for (adevs::Bag<int>::iterator iter = xb.begin();
             iter != xb.end(); iter++)
            p += (*iter);
    }
    void delta_conf(const adevs::Bag<int>& xb)
    {
        delta_int();
        delta_ext(0.0,xb);
    }
    void output_func(adevs::Bag<int>& yb) { yb.insert(1); }
    double ta()
    {
        if (p > 0) return sigma;
        else return DBL_MAX;
    }
    void gc_output(adevs::Bag<int>&) {}
    double getSigma() const { return sigma; }
    int getParts() const { return p; }
private:
    const double tm; // Machining time
    int p; // Number of parts in the bin
    double sigma; // Time to the next output
};

#endif
```

### 装配线模型的实现

```cpp
#ifndef _AssemblyLine_h_
#define _AssemblyLine_h_
#include "Machine.h"

class AssemblyLine: public adevs::Network<int>
{
  public:
    AssemblyLine():
      adevs::Network<int>(),
      // Create the components
      press(1.0),drill(2.0){}

    void getComponents(adevs::Set<adevs::Atomic<int>*>& c)
    {
      c.insert(&press);
      c.insert(&drill);
    }
    void route(const int& value, adevs::Atomic<int>* model,
      adevs::Bag<adevs::Event<int> >& r)
    {
      adevs::Event<int> x;
```

```cpp
cout << "drill = (" << assembly_line->getDrill()->getParts()
     << ", " << assembly_line->getDrill()->getSigma() << ")"
     << endl;
}
private:
    AssemblyLine* assembly_line;
};

int main()
{
    // Create the model, event listener, and simulator
    AssemblyLine* assembly_line = new AssemblyLine();
    Resultant<int>* r = new Resultant<int>(assembly_line);
    AssemblyLineListener* l = new AssemblyLineListener(assembly_line);
    Simulator<int>* sim = new Simulator<int>(r);
    sim->addEventListener(l);
    // Print the initial state of the model
    l->stateChange(r,0,0);
    // Run the simulation
    while (true) {
        // Bag for injecting the input
        Bag<int> input;
        // The value to inject
        int blanks;
        // Time to inject the input
        double t; int c;
        // Read the time and input values
        cin >> t >> c >> blanks;
        // If this is the end of the input, then quit
        if (cin.eof()) break;
        // Simulate until time t and then inject the input
        while (sim->nextEventTime() < t) {
            cout << endl;
            sim->execNextEvent();
        }
        // Simulate the transient events
        for (int i = 0; i < c && sim->nextEventTime() == t; i++) {
            cout << endl;
            sim->execNextEvent();
        }
        // Inject the input
        input.insert(blanks);
        cout << endl;
        sim->computeNextState(input,t);
    }
    // Run until the simulation completes
    while (sim->nextEventTime() < DBL_MAX) {
        cout << endl;
        sim->execNextEvent();
    72   }
    73   // Clean up
    74   delete sim; delete l; delete r;
    75   return 0;
    76 }
```

### 给出输入文件

```
    0 0 1
    2 1 2
```

将该输入文件提供给仿真器，会重复第 4.2.3 节中手工完成的计算。手工仿真产生了装配线截至时刻 (3, 0) 的响应。计算机仿真在该时刻之前与手工仿真一致，并继续推进，在时刻 (7, 0) 产出最终零件，并在 (7, 1) 终止。该仿真的输出如下所示。阅读输出时请记住：当产生输出或状态改变时，时钟的整数部分会隐式推进：第一行显示时刻 (0, 0)，第二行显示 (0, 1)，第三行显示 (1, 1)，第四行显示 (2, 2)（紧接在 (2, 1) 的输入之后），依此类推。

```
    $ ./a.out < input
    State, t = 0, press = (0,1), drill = (0,2)

    State, t = 0, press = (1,1), drill = (0,2)

    State, t = 1, press = (0,1), drill = (1,2)

    State, t = 2, press = (2,1), drill = (1,2)

    Output, t = 3, y = 1
    State, t = 3, press = (1,1), drill = (1,2)

    State, t = 4, press = (0,1), drill = (2,1)

    Output, t = 5, y = 1
    State, t = 5, press = (0,1), drill = (1,2)

    Output, t = 7, y = 1
    State, t = 7, press = (0,1), drill = (0,2)
    $
```

比较由内容如下的文件 input.a 所产生的结果：

```
    0 0 1
    3 0 1
```

## 4.3 离散事件系统的仿真器

可以像第 3.3 节构建离散时间系统仿真器那样，构建离散事件系统的自底向上仿真器。算法几乎相同，只需作出修改以适应离散事件系统状态转移函数和输出函数的定义。这些修改将与离散时间仿真器和离散事件仿真器的 Resultant 类之间的差异非常相似。

在任意特定时刻，大型离散事件系统中的大多数组件不会产生输出或改变状态。如果我们只关心事件实际发生的那些时刻，那么按照离散时间仿真器的模式构建的简单实现会浪费计算资源。只需稍作努力，就可以消除三项具体负担。

第一项负担在于网络状态转移函数和输出函数的计算。Resultant 的内部、外部和合流转移函数会遍历网络中的每个原子模型，并为其计算新状态或更新其已流逝时间。很可能只有少数组件会真正改变状态；如果我们只处理这些模型，就可以避免为其他模型递增已流逝时间的开销。当一个模型包含许多组件时，这种节省相当可观。

第二项负担在于网络时间推进函数的计算。这需要找到集合中的最小值，而 Resultant 中使用的朴素实现会遍历集合中的每个成员来找到该最小值。然而，如果模型按下次事件时间的顺序保持排序，那么在需要计算输出函数和状态转移函数时，就可以快速识别出即将发生事件的模型。

第三项负担是路由算法所使用的输入包和输出包所需的内存。只有当模型产生输出或接收输入时才需要这些包，而这些操作相对不频繁。原则上，只需为每次迭代中活跃的少量模型分配少量包。当仿真非常大量的组件时，这样做可以节省大量内存。此外，这些包通常只保存少量对象，而且这些对象不需要按任何特定顺序保存。两项优化将利用这些事实，减少仿真引擎管理输入和输出事件所花费的时间和空间开销。

通过考虑这些问题，高效的仿真引擎会比第 4.2.4 节展示的自顶向下仿真器复杂得多。然而请记住，高效仿真器无非就是针对上述系统类的仿真器。构建将从主要数据结构开始：事件调度表和 Bag。有了这些之后，其余部分就很直接，而且其中大部分借鉴自离散时间系统仿真器。算法 3.6 用于将事件从输入转换为输出，反之亦然；仿真器的接口将与离散时间系统的接口非常相似，只是在需要为适应不规则时间推进而作出修改的地方有所不同，如第 4.2.4 节所示。

