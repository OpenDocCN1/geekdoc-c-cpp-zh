
```text
1  procedure route(parent,d,y^b)
2  foreach d' ∈ E_d do
3      d' is an atomic component of parent
4      if d' is atomic then
5          x_{d'}^b ← x_{d'}^b ∪ z_{d,d'}(y^b)
6      d' is a network component of parent
7      else if d' ≠ parent then
8          route(d',d,z_{d,d'}(y^b))
9      else if this is an output from parent
10     else if d' = parent and PARENT(d') exists then
11         route(PARENT(d'),d',z_{d,d'}(y^b))
12     end
13 end
```

**算法 3.6** 用于在网络模型内路由输入和输出的流程。影响集合 E_d 和耦合函数 z_{d,d'} 属于网络父级。

路由问题的另外两个部分——将输入放入网络模型以及从网络模型观察输出——可方便地由算法 3.6 解决。通过调用 route 并将 N 作为第一个和第二个参数（即 parent = d = N），以及将 x^b 作为第三个参数，可将输入 x^b 注入网络 N。当第三个条件为真时（即“来自父级的输出”条件），网络模型会产生输出，并且注册到 Simulator 的 EventListeners 会在此时收到通知。

算法 3.7 描述了完整的仿真流程。它将输入轨迹 x < t_0, t_n > 应用于具有原子组件集合 A_N 的网络 N。对于 A_N 中的每个组件 d，都有一个输入包 x^b_d 和其状态 s_d。EventListeners 的通知已被省略，即使它们将在实现中出现。

```text
1  for t_k ∈ < t_0, t_n > do
2      Clear the bags of input
3      foreach d ∈ A_N do
4          x_{d}^b ← ∅
5      end
6      Route the input to N
7      route(N,N,x(t_k))
8      Compute and route output from the components
9      foreach d ∈ A_N do
10         route(PARENT(d),d,z_{d,d}(s_d))
11     end
12     Change the state of the components
13     foreach d ∈ A_N do
14         s_d ← δ_d(s_d, x_d^b)
15     end
16 end
```

**算法 3.7** 离散时间模型的自底向上仿真算法。

实现自底向上模拟器的类几乎与自顶向下模拟器使用的类相同。*Resultant* 不再必要，已被移除。新增一个 *Diss* 类，并修改 *Atomic* 和 *Network* 类使其继承自它。*Diss* 类保存两条信息：模型的父级和模型的类型。*Diss* 类的父级字段用于实现 PARENT 函数。类型信息用于 route 流程以及初始化仿真引擎⁴。*Network* 和 *Atomic* 类在其他方面保持不变。

*Event* 类不需要任何修改，但我们有机会有用地扩展 *EventListener* 类的功能。模拟器现在能够感知每个事件在网络耦合中的移动，可以通知监听器每个原子和网络模型的每一个输出。同样，监听器也可以被告知每个原子模型状态的变化。这显著扩展了 *EventListener* 观察、报告、记录和可视化大型模型运行的能力。新的 *EventListener* 的 *outputEvent* 方法接受一个 *Event*，该事件携带产生输出的模型、网络或原子，以及输出本身。

类似地，我们可以通过允许其客户端直接向多组件模型的任何组件注入输入来扩展 *Simulator* 类的功能。这是构建交互式仿真以及将模拟器集成到多模拟器联邦中的基本能力。新的 *Simulator* 的 *computeNextState* 方法接受一个 *Event* 对象的 *Bag*。*Bag* 中的每个 *Event* 都包含一个模型及其输入。如果模型是原子的，则输入会被放入其输入包中。如果目标是网络，则使用算法 3.6 将输入传递给适当的原子模型集合。

修订后的类图如图 3.7 所示，由此可以轻松推断出 *Diss*、*Network*、*Atomic*、*Event* 和 *EventListener* 类的实现。*Event* 类有两个字段以及设置和访问它们的方法。*EventListener* 是一个纯虚类，没有实现，只有定义。*Diss* 类包含其父级、设置和获取父级的方法，以及虚方法 *typeIsNetwork* 和 *typeIsAtomic*；这些方法由 *Network* 和 *Atomic* 类实现。*Network* 类在调用 *typeIsNetwork* 时返回自身，在调用 *typeIsAtomic* 时返回 NULL。*Atomic* 类则相反。

*Simulator* 类是唯一具有实质性实现的一个类。它实现了算法 3.7，并进行了上述讨论的小幅修改，以允许模拟器的客户端向任何组件注入输入，并在组件产生输出或状态发生变化时通知监听器。算法 3.6 用于在模型中移动事件。*Simulator* 的源代码如下所示。

![](img/df6085a1b35edf9c9ea818a5c66ccad9_92_0.png)

**图 3.7** 离散时间系统自底向上仿真引擎的类图。

## 离散时间模型的通用模拟器

```cpp
1 #ifndef _dtss_simulator_h_
2 #define _dtss_simulator_h_
3 #include "dtss_models.h"
4 #include <ostream>
5
6 namespace dtss
7 {
8
9 template <typename X> class Simulator {
10 public:
11   // Create a simulator for the supplied model
12   Simulator(Dtss<X>* model);
13   // Compute the next state of the model and invoke callbacks
14   void computeNextState(const Bag<Event<X> >& input);
15   // Compute the model's output and make outputEvent callbacks
16   void computeOutput();
17   // Get the simulation time.
18   unsigned int getTime() { return t; }
19   // Add an event listener
20   void addEventListener(EventListener<X>* listener) {
21     listeners.push_back(listener);
22   }
23 private:
24   Set<Atomic<X>*> atomics; // The complete set of atomic models
25   unsigned int t; // Simulation clock
26     bool output_up_to_date; // Is the model output up to date?
27     // List of event listeners
28     typedef std::list<EventListener<X>*> ListenerList;
29     ListenerList listeners;
30     // Get all of the children belonging to a network
31     void getAllChildren(Network<X>* model, Set<Atomic<X>*>& s);
32     // Move an input or output value to its destination
33     void route(Network<X>* parent, Dtss<X>* src, const X& x);
34     // Tell all EventListeners about an output
35     void notify_output_listeners(Dtss<X>* model,
36                                  const X& value, unsigned int t);
37 };
38
39 template <typename X>
40 Simulator<X>::Simulator(Dtss<X>* model):
41     t(0),output_up_to_date(false)
42 {
43     // If this is an atomic model then it is the only
44     // atomic model to simulate
45     if (model->typeIsAtomic() != NULL)
46         atomics.insert(model->typeIsAtomic());
47     // Otherwise get all of the atomic models by recursion
48     else getAllChildren(model->typeIsNetwork(),atomics);
49 }
50
51 template <typename X>
52 void Simulator<X>::computeNextState(const Bag<Event<X> >& input)
53 {
54     // Compute the output at time t
55     computeOutput();
56     // Deliver the injected input
57     for (typename Bag<Event<X> >::iterator iter = input.begin();
58          iter != input.end(); iter++) {
59         if ((*iter).model->typeIsAtomic()) {
60             (*iter).model->typeIsAtomic()->input_bag.insert((*iter).value);
61         }
62         else {
63             route((*iter).model->typeIsNetwork(),(*iter).model,(*iter).value);
64         }
65     }
66     // Advance the simulation clock
67     t++;
68     // Update the state of every atomic component
69     for (typename Set<Atomic<X>*>::iterator aiter = atomics.begin();
70          aiter != atomics.end(); aiter++) {
71         // Compute the new state of the model
72         (*aiter)->delta((*aiter)->input_bag);
73         // Notify listeners that the state has changed
74         for (typename ListenerList::iterator liter = listeners.begin();
```

