

```cpp
// Counters for the clock and machine cycle
int clk = 0, machine_cycle = 0;
// Run the simulation
while (true) {
    // Get the input from stdin
    adtss::Bag<adtss::Event<port_value_t> > input;
    port_value_t x1, x2;
    x1.port = N1::x1;
    x2.port = N1::x2;
    cin >> x1.bit >> x2.bit;
    // Quit if the input has ended
    if (cin.eof()) break;
    input.insert(adtss::Event<port_value_t>(m,x1));
    input.insert(adtss::Event<port_value_t>(m,x2));
    // Print the time and input
    cout << " xx M" << machine_cycle << " C" << clk <<
         "\t" << x1.bit << " " << x2.bit << "\t";
    // Print the time and output at the next machine cycle
    cout << " yy M" << ++machine_cycle << " C" << clk << "-" << clk+2 << "\t";
    // Advance the simulation by one machine cycle
    for (int t = 0; t < 3; t++) {
        clk++;
        sim->computeNextState(input);
    }
    cout << endl;
}
// Clean up and exit
delete sim; delete l1; delete m;
return 0;
}
```

## 3.4 米利/摩尔型系统

摩尔型系统的输出是其状态的函数；摩尔输出函数具有如下形式

$$\lambda : S \to Y$$

这些系统我们已经熟悉。米利型系统的输出是其状态和当前输入的函数；米利输出函数具有如下形式

$$\lambda : S \times X \to Y$$

通过丢弃提供给输出函数的输入，我们可以构建一个米利型系统来模仿任何摩尔型系统。在这个意义上，米利型系统是更一般的构造。那么，我们为什么没有为米利型系统构建仿真引擎呢？

当我们构建由米利型组件组成的网络时，麻烦就来了。假设我们有两台米利型机器 M₁ 和 M₂，按图 3.8 所示的反馈配置排列。这两台特定的米利机是一对相同的有限状态自动机，其状态转移与输出函数如图 3.9 所示。圆圈表示状态，弧线表示系统对输入的响应。斜杠前的字母是引起状态转移的输入，斜杠后的字母是对应的输出。

![](img/df6085a1b35edf9c9ea818a5c66ccad9_101_0.png)

**图 3.8** 两个按反馈配置排列的米利型系统。

不知道 M₂ 的输出，就无法知道 M₁ 的输出，因为 M₂ 为 M₁ 提供输入。不知道 M₁ 的输出，就无法知道 M₂ 的输出，但这又需要 M₂ 的输出。只有存在对 M₁ 和 M₂ 输出的一致且唯一的选择时，这个问题才能解决。

假设 M₁ 从状态 p 开始，M₂ 从状态 q 开始。M₁ 的输出可以是 a 或 b。如果它是 a，那么 M₁ 的输入就是 b，因此 M₂ 的输出也是 b。不幸的是，这要求 M₂ 的输入为 b，于是 M₁ 的输出必须是 b，而不是 a。我们得到了一个矛盾：M₁ 的输出不可能是 a。

假设 M₁ 的输出是 b。那么它的输入必须是 a。因此，M₂ 的输出也必须是 a，但这要求它的输入为 a，于是 M₁ 的输出必须是 a，而不是 b。这又是一个矛盾：M₁ 的输出不可能是 b。显然，机器不能从状态 (p, q) 开始，而 (q, p) 同样不可维持。

状态 (p, p) 给了我们一点喘息之机。如果 M₁ 的输出是 a 且 M₂ 的输出是 b，那么机器进入状态 (p, q)，但随后就卡住了。状态 (q, q) 稍微更有吸引力。如果两台机器都产生输出 a，整个系统可以移动到状态 (p, p)，然后卡住；或者，如果两台机器都产生输出 b，它可以移动（更确切地说，停留）在状态 (q, q)。

![](img/df6085a1b35edf9c9ea818a5c66ccad9_101_1.png)

**图 3.9** 米利系统 M₁ 和 M₂ 的状态转移与输出函数。

![](img/df6085a1b35edf9c9ea818a5c66ccad9_102_0.png)

**图 3.10** 一维元胞自动机中五个元胞的排列。当这些元胞构成环时存在虚线连接，构成线时则不存在。

这个特定问题是一种更根本弊病的症状。由离散模型构成的网络如果包含无延迟环路，通常是定义不良的。图 3.9 所示的排列不是一个系统，因为我们无法为该网络定义一个合成结果。在某些特殊情况下，这个问题也许可以避免；例如，我们的例子可以通过消除状态 *p* 及其相连的弧线来简化。经过这种简化后，它行为良好，但并不十分有趣。

这个问题还会在涉及对输入作出瞬时反应的离散事件系统时再次出现。禁止瞬时事件，并由此消除无延迟环路，会严重束缚模型，因而不可行。一个令人满意的解决方案也许出人意料地存在于本章所研究的摩尔型离散时间系统中。

## 3.5 元胞自动机

著名的“生命游戏”因 1970 年一篇*《科学美国人》*文章而流行起来 [48]，它是一类称为元胞自动机的系统的实例。元胞自动机由一组离散时间系统——自动机中的元胞——组成，这些系统排列在网格中。每个元胞与其直接相邻的元胞交互。在一维元胞自动机中，元胞排成一行，并与其左侧和右侧的邻居交互；如图 3.10 所示。为了可视化元胞自动机的整体状态，为其元胞的每个状态分配一种颜色，并将这些状态并排绘制。通过按顺序排列其后续状态，一个叠一个，来描绘自动机的轨迹。这形成了一幅马赛克图，可以揭示原本简单的元胞在集体行为中令人惊讶的模式。

元胞自动机很容易作为离散时间网络来建模和仿真。为便于说明，我们将考虑一维元胞自动机，其元胞有两种状态：白色和黑色，分别缩写为 *w* 和 *b*。元胞由 *Cell* 类实现，该类派生自仿真引擎的 *Atomic* 类。*Cell* 具有一个状态以及在元胞自动机中的位置。其 *delta* 方法接受一个结构，其中包含相邻元胞的状态和位置。来自左右邻居的输入以及 *Cell* 的当前状态被传递给一个名为 *cell_rule* 的虚方法。该方法检查其三个参数，并返回元胞的下一个状态。要实现任何特定元胞，只需实现 *cell_rule* 方法。*Cell* 的 *output_func* 方法仅返回其当前状态。*Cell* 类的源代码如下所示。

### Cell 类

~~~cpp
#ifndef Cell_h_
#define Cell_h_
#include "adtss.h"

typedef enum { BLACK, WHITE } state_t;
// Structure used for input to and output from a cell
struct IO_Type
{
    state_t state; // The cell's discrete state
    int src; // Location of the cell that produced the event
    bool operator<(const IO_Type& other) const // Needed by the STL
    {
        return src < other.src;
    }
};

class Cell: public adtss::Atomic<IO_Type>
{
    public:
        // Constructor puts the cell into its initial state
        Cell(state_t s0, int location):
            adtss::Atomic<IO_Type>(),
            s(s0),location(location) {}
        // State transition function
        void delta(const adtss::Bag<IO_Type>& xb)
        {
            // Edges are WHITE
            state_t left = WHITE, right = WHITE;
            for (adtss::Bag<IO_Type>::iterator iter = xb.begin();
                 iter != xb.end(); iter++) {
                if ((*iter).src == location-1) left = (*iter).state;
                else right = (*iter).state;
            }
            s = cell_rule(left,right,s);
        }
        // Output function
        void output_func(adtss::Bag<IO_Type>& yb)
        {
            IO_Type output;
            output.state = s;
            output.src = location;
            yb.insert(output);
        }
        // The gc_output method is not needed
        void gc_output(adtss::Bag<IO_Type>&){}
        // Get the location of the cell
        int getLocation() const { return location;
