
```cpp
void stateChange(AtomicModel* model, double t)
{
    // If this is the model of the tank's physics
    if (model == tank->getPhysics()) {
        // Get the current and motor resistance
        double Rm = tank->getPhysics()->getMotorOhms();
        // Update the energy dissipated in the motors
        E += (t-t1)*(il*il*Rm + ir*ir*Rm);
        // Remember the last sample
        il = tank->getPhysics()->leftMotorCurrent();
        ir = tank->getPhysics()->rightMotorCurrent();
        t1 = t;
        fout << t1 << " " << il << " " << ir << std::endl;
    }
}
// Get the power dissipated in the left and right motors
double getPowerLoss() const { return E/t1; }
private:
    const Tank* tank;
    std::ofstream fout;
    double E, t1, il, ir;
};

#endif
```

一个 shell 脚本会反复调用主程序来开展仿真实验。每次调用仿真程序时，都会计算在一个频率和一对占空比下电机中耗散的功率。仿真程序的第一个参数是发送给电机的电压信号频率，第二个参数是左电机的占空比，第三个参数是右电机的占空比。（第零个参数是可执行文件本身的名称。）程序会准备实验、运行实验、将结果打印到控制台、进行清理并退出。主函数的 C++ 代码如下所示。

### 功率耗散实验的主程序

```cpp
#include "Tank.h"
#include "SimEvents.h"
#include "TankEventListener.h"
using namespace std;

int main(int argc, char** argv)
{
    // Get the parameters for the experiment from the command line
    if (argc != 4) {
        cout << "freq left_throttle right_throttle" << endl;
        return 0;
    }
    // Get the frequency of the voltage signal from the first argument
    double freq = atof(argv[1]);
    // Create a command from the driver that contains the duty ratios from
    // the second and third arguments.
    SimPacket sim_command;
    sim_command.left_power = atof(argv[2]);
    sim_command.right_power = atof(argv[3]);
    // Create the tank, simulator, and event listener. The arguments to the
    // tank are its initial position (x = y = 0), heading (theta = 0), and
    // the smallest interval of time that will separate any two reports of
    // the tank's state (0.02 seconds).
    Tank* tank = new Tank(freq,0.0,0.0,0.0,0.0,0.02);
    Simulator* sim = new Simulator(tank);
    TankEventListener* l = new TankEventListener(tank);
    // Add an event listener to compute the power dissipated in the motors
    sim->addEventListener(l);
    // Inject the driver command into the simulation at time zero
    ModelInputBag input;
    SimEvent cmd(sim_command);
    ModelInput event(tank,cmd);
    input.insert(event);
    sim->computeNextState(input,0.0);
    // Run the simulation for 3 seconds
    while (sim->nextEventTime() <= 3.0) sim->execNextEvent();
    // Write the result to the console
    cout << freq << " " << l->getPowerLoss() << endl;
    // Clean up and exit
    delete sim; delete tank; delete l;
    return 0;
}
```

使用以下 shell 脚本对一组频率执行仿真

```bash
for ((i=50;i<=7000;i+=50)); do ./a.out $i 0.5 0.5; done
```

其中 a.out 是仿真程序的名称（这是 GNU C++ 编译器生成的可执行文件的默认名称）。该脚本以 50 Hz 为增量，计算频率范围 [50, 7000] 内电机中耗散的功率。结果绘制在图 2.12 中。该图表明 3000 Hz 是频率的一个合理下限。交互实验将从 3000 Hz 开始，逐步提高到更高频率，直到我们找到仍能实现有效控制的最高频率。²

²这些损耗的功率去了哪里？它变成了热和噪声。图 2.12 中所示的频率处于人耳听觉范围内。因此，电机会发出明显的高频嗡鸣声。伴随而来的是齿轮发出的低沉咕噜声和研磨声；如果电机接近满功率运行，还会闻到淡淡的臭氧味。

![](img/df6085a1b35edf9c9ea818a5c66ccad9_40_0.png)

图 2.13 所示的赛道用于交互实验。坦克从赛道最左侧一段的中心出发，被操纵绕赛道行驶并返回起始位置。如果坦克偏离赛道，则该次运行被丢弃。经过数次练习运行后，实验运行以 2 kHz 为增量进行。在每个频率下，坦克绕赛道行驶，直到完成三圈。作者记录了完成每圈的时间以及每个频率下的失败尝试次数。结果列于表 2.3 中。

比较损耗功率、完成一圈赛道所需时间以及失败运行次数的数据，效率与控制之间的权衡立刻显而易见。在低频下，坦克响应非常灵敏，实验赛道可在大约一分钟内安全通过。在较高频率下，驾驶员必须更加谨慎；在 9 kHz 及以上时，赛道非常难以通过。随着频率提高，电机运行效率更高，但坦克更难控制。

![](img/df6085a1b35edf9c9ea818a5c66ccad9_40_1.png)

表 2.3 交互实验数据

| 频率（kHz） | T₁（s） | T₂（s） | T₃（s） | 平均值 | 失败次数 |
|---|---:|---:|---:|---:|---:|
| 3 | 68.7 | 68.3 | 69.1 | 68.7 | 0 |
| 5 | 68.9 | 68.3 | 70.8 | 69.3 | 0 |
| 7 | 69.8 | 70.0 | 67.9 | 69.2 | 0 |
| 9 | 68.3 | 68.5 | 88.4 | 75.1 | 2 |
| 11 | 67.6 | 84.4 | 113.0 | 88.3 | 0 |
| 12 | 104.0 | 101.7 | 无数据 | 103.2 | 2 |

根据这些数据以及图 2.12 中的数据，我们可以得出结论：7 到 8 kHz 之间的频率是最佳选择。在该范围内，电机运行高效，计算机能及时处理来自驾驶员的命令。实际坦克的工作频率约为 7.4 kHz：中断处理程序的相邻两次调用之间相隔 310 个机器周期。

## 2.5 小结

本示例展示了本书其余部分所开发的仿真引擎的三个主要特性：模块化、自底向上的模型构建；模型与其仿真器的分离；以及离散事件组件和连续组件的纳入。模块化、自底向上的构建方式允许大型仿真器被分块构建和测试。原子模型封装基本行为；如果对大型模型进行合理分解，那么这些最小的部件就可以被独立地构建、测试和维护。当这些部件组合成更大的组件时，这些更大的组件也可以彼此独立地构建、测试和调试。这种封装原则延伸到整个仿真器，最终使整个仿真器可以作为更大软件系统中的一个自包含组件使用。

模型与其仿真器的分离也有类似目的。仿真引擎中包含的算法是为特定类别的系统设计的。因此，它们可以在不涉及任何特定系统的情况下被构建、测试和维护。仿真引擎的测试用例将主要由简单模型组成，这些模型的行为可以通过手工计算或借助另一个已知正确的仿真器推导出来。这对建模者来说也是一个优势；仿真器所假定的系统类别的定义，保证了它将如何运行。因此，仿真引擎的改进对模型是透明的，这大大简化了仿真程序的长期维护。

包含离散事件组件和连续组件对于许多工程系统的建模不可或缺；机器人坦克就是一个例子。这必须准确且精确地完成，但准确性正是最大的挑战。说一个仿真相对于理想化模型是准确的，意味着该模型的行为原则上可以不借助仿真器推导出来：必须存在一个正确结果，用以衡量准确性。因此，将模型与计算其行为的算法分离至关重要。因此，这两个概念是建模与仿真研究的核心。

