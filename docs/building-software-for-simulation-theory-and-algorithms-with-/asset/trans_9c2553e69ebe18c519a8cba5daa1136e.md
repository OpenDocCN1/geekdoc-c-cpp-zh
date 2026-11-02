
```cpp
bool reverse_left, reverse_right; // Motor direction
double last_left_v, last_right_v; // Previous output voltages
double left_v, right_v; // Next output voltages
Phase phase; // The current phase of the model
};

#endif
```

## InterruptHandler 的实现

```cpp
#include "InterruptHandler.h"
#include <iostream>
using namespace std;
using namespace adevs;

InterruptHandler::InterruptHandler(double freq):
    Atomic<SimEvent>(),
    interrupt_period(1.0/(8.0*freq)), // Initialize the model
    motor_voltage(7.2),
    exec_time(0.432E-6),
    ttg(interrupt_period),
    counter(0),
    left_on_time(0),
    right_on_time(0),
    reverse_left(false),
    reverse_right(false),
    last_left_v(0.0),
    last_right_v(0.0),
    left_v(0.0),
    right_v(0.0),
    phase(WAIT)
{
}

void InterruptHandler::delta_int()
{
    // Start an interrupt
    if (phase == WAIT)
    {
        phase = EXEC;
        ttg = exec_time;
    }
    // End an interrupt and send the output
    else if (phase == EXEC)
    {
        // Increment the counter
        counter += 32;
        // Compute the next output voltage
        left_v = motor_voltage*(counter < left_on_time);
        if (reverse_left) left_v = -left_v;
        right_v = motor_voltage*(counter < right_on_time);
        if (reverse_right) right_v = -right_v;
        // Send the voltage and interrupt signal
        phase = OUTPUT;
        ttg = 0.0;
    }
    // Wait for the next interrupt
    else if (phase == OUTPUT)
    {
        // Remember the last output voltages
        last_left_v = left_v;
        last_right_v = right_v;
        // Wait for the next interrupt
        phase = WAIT;
        ttg = interrupt_period;
    }
}

void InterruptHandler::delta_ext(double e, const Bag<SimEvent>& xb)
{
    // Decrement the time to go
    ttg -= e;
    // Look for input
    for (Bag<SimEvent>::iterator iter = xb.begin();
         iter != xb.end(); iter++)
    {
        assert((*iter).getType() == SIM_MOTOR_ON_TIME);
        left_on_time = (*iter).simMotorOnTime().left;
        right_on_time = (*iter).simMotorOnTime().right;
        reverse_left = (*iter).simMotorOnTime().reverse_left;
        reverse_right = (*iter).simMotorOnTime().reverse_right;
    }
}

void InterruptHandler::delta_conf(const Bag<SimEvent>& xb)
{
    delta_int();
    delta_ext(0.0,xb);
}

void InterruptHandler::output_func(Bag<SimEvent>& yb)
{
    // If this is the end of an interrupt
    if (phase == OUTPUT)
    {
        // If the voltage changed, then send the new values
        if (last_left_v != left_v || last_right_v != right_v)
        {
            SimMotorVoltage volts;
            volts.el = left_v;
            volts.er = right_v;
            yb.insert(SimEvent(volts));
        }
        // Send the interrupt indicator
        yb.insert(SimEvent(SIM_INTERRUPT));
    }
    // If this is the start of an interrupt
    else if (phase == WAIT) yb.insert(SimEvent(SIM_INTERRUPT));
}
double InterruptHandler::ta() { return ttg; }
```

仿真程序通过标准输入获得一条输入轨迹，并计算由此得到的状态和输出轨迹。仿真在最后一个输入处结束。中断处理器产生的电压信号频率通过命令行设置。下面列出了该仿真器的实现。这是模型在新环境中被复用的另一个示例：最初作为交互式坦克仿真器的一部分构建的 `InterruptHandler`，现已从该仿真器中提取出来，并被复用于这个新的仿真程序。

## InterruptHandler 的仿真

```cpp
#include "adevs.h"
#include "InterruptHandler.h"
#include <iostream>
using namespace std;
using namespace adevs;

// Listener for recording the state and output of the interrupt handler
class InterruptListener: public EventListener<SimEvent>
{
public:
InterruptListener(){}
void outputEvent(Atomic<SimEvent>* model,
const SimEvent& value, double t)
{
cout << "Output, t = " << t << ", ";
if (value.getType() == SIM_INTERRUPT)
cout << "interrupt" << endl;
else if (value.getType() == SIM_MOTOR_VOLTAGE)
cout << "el = " << value.simMotorVoltage().el <<
" er = " << value.simMotorVoltage().er << endl;
}
void stateChange(Atomic<SimEvent>* model, double t)
{
InterruptHandler* ih = dynamic_cast<InterruptHandler*>(model);
        cout << "State, t = " << t;
        cout << ", el = " << ih->getLeftOutput();
        cout << ", er = " << ih->getRightOutput();
        cout << ", e'l = " << ih->getLastLeftOutput();
        cout << ", e'r = " << ih->getLastRightOutput();
        cout << "\n\tc = " << ih->getCounter();
        cout << ", o'l = " << ih->getLeftOnTime();
        cout << ", o'r = " << ih->getRightOnTime();
        cout << ", r'l = " << ih->getLeftReverse();
        cout << ", r'r = " << ih->getRightReverse();
        cout << ", i = ";
        if (ih->getPhase() == InterruptHandler::WAIT)
            cout << "WAIT" << endl;
        else if (ih->getPhase() == InterruptHandler::EXEC)
            cout << "EXEC" << endl;
        else if (ih->getPhase() == InterruptHandler::OUTPUT)
            cout << "OUTPUT" << endl;
    }
};

int main(int argc, char** argv)
{
    // Make sure that a frequency was given
    if (argc != 2) {
        cout << "Must provide a signal frequency" << endl;
        return 0;
    }
    // Set the output precision to make the small time advances apparent
    cout.precision(12);
    // Create the model, event listener, and simulator
    InterruptHandler* ih = new InterruptHandler(atof(argv[1]));
    InterruptListener* l = new InterruptListener();
    Simulator<SimEvent>* sim = new Simulator<SimEvent>(ih);
    sim->addEventListener(l);
    // Print the initial state of the model
    l->stateChange(ih,0.0);
    // Run the simulation
    while (true) {
        // Bag for injecting the input
        Bag<SimEvent> input;
        // The value to inject
        SimMotorOnTime motor_setting;
        // Time to inject the input
        double t; int c;
        // Read the time and input values
        unsigned int o_l, o_r;
        cin >> t >> c >> o_l >> motor_setting.reverse_left
            >> o_r >> motor_setting.reverse_right;
        motor_setting.left = (unsigned char)o_l;
        motor_setting.right = (unsigned char)o_r;
        // If this is the end of the input, then quit
        if (cin.eof()) break;
        // Simulate until time t and then inject the input
        while (sim->nextEventTime() < t) {
          cout << endl;
          sim->execNextEvent();
        }
        // Simulate the transient events
        for (int i = 0; i < 100 && sim->nextEventTime() == t; i++) {
          cout << endl;
          sim->execNextEvent();
        }
        // Inject the input
        input.insert(SimEvent(motor_setting));
        cout << endl;
        sim->computeNextState(input,t);
    }
    // Clean up
    delete sim; delete l; delete ih;
    return 0;
}
```

在这个示例中，中断处理器以 2000 Hz 运行，因此其周期 t_e 精确等于 6.25 × 10⁻⁴ 秒（式 4.11）。输入轨迹 x((0), (t_e, 0)) 在 x((t_e/2, 0)) = (255, 0, 255, 1) 处有一个事件，它将左电机设为全速前进、右电机设为全速反向；它还在 x((t_e, 0)) = (0, 0, 0, 0) 处有一个事件，在计算机有机会处理前一条命令之前，将电机设置改为完全停止。描述该轨迹的输入文件 `exp1` 包含两行：

~~~text
3.125E-5 0 255 0 255 1
6.25E-5 0 0 0 0 0
~~~

运行仿真会产生：

~~~text
$ ./a.out 2000 < exp1
State, t = 0, el = 0, er = 0, e'l = 0, e'r = 0,
       c = 0,ol = 0,or = 0,rl = 0,rr = 0,i = WAIT

State, t = 3.125e-05, el = 0, er = 0, e'l = 0, e'r = 0,
       c = 0,ol = 255,or = 255,rl = 0,rr = 1,i = WAIT

Output, t = 6.25e-05, interrupt
State, t = 6.25e-05, el = 0, er = 0, e'l = 0, e'r = 0,
       c = 0,ol = 0,or = 0,rl = 0,rr = 0,i = EXEC
$
~~~

仿真器打印时间 (0, 0) 处的初始状态。输入轨迹在时间 (t_e/2, 0) 设置左右电机的计数器。在时间 (t_e, 0)，中断处理器被激活，并产生它的 {interrupt} 输出；与此同时，第二个输入被施加，从而阻断了电机的启动。

让电机以半功率运行，可以很有说服力地说明尽量减少中断处理器产生的电压事件数量有多重要。输入文件

```
0 0 127 0 127 1
1 0 0 0 0 0
```

会让坦克原地旋转一秒钟。中断处理器产生了 35,753 个输出，其中 397 个是 *SimMotorVoltage* 事件。如果每次仿真的中断都产生一个电压事件，问题就立刻显现出来：朴素方案会为 *TankPhysics* 模型产生 10 倍于原来的输入事件，而该模型的状态转换计算非常耗时。这些额外的工作会把仿真器拖慢到无法用于交互的程度。将 *SimMotorVoltage* 事件限制为仅那些真正表示电压变化的事件，是一项必不可少的优化。

## 4.2 网络模型

离散时间模型网络和离散事件模型网络的构造方式相同。一个网络由一组组件模型、这些模型之间的连接，以及网络输入输出与组件输入输出之间的连接组成。离散事件网络在耦合运算下是封闭的，将网络约简为其原子等价模型的步骤，也定义了多组件系统的仿真步骤。从第 3 章对离散时间系统的学习中，这些方面都应该很熟悉。

由于离散事件模型的各原子组件各自按自己的步调运行，由此得到的离散事件网络比对应的离散时间网络更复杂。这些新的组合复杂性几乎完全来自时间推进函数。除去这些细节，本节的内容与第 3 章中的内容相类似。输入和输出事件在模型中递归地路由。算法的基础步骤同样是熟悉的：计算输出、将输出转换为输入，然后计算新状态。仿真器的接口也基本保持不变。

### 4.2.1 网络模型的组成

离散事件网络的结构和组合方式与离散时间网络完全相同。总结第 3.2.1 节，一个网络
