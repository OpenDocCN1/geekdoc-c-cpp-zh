

![](img/91599d88757ed8c75960eb83f4f85a12_209_0.png)

图7.1 混合控制器

模拟计算机系统总线¹³¹的控制线，并具有用于读出的16位ADC。

以下示例概述了混合计算机的一般功能。关于混合计算及其许多应用的更多信息，可参见[BEKEY et al. 1968]、[KORN et al. 1964]、[SCHÖNEFELD 1977]以及其他经典教科书。

### 7.2 基本操作

这些示例中使用的Model-1混合控制器通过模拟串行线的USB接口连接到数字计算机。¹³² 为了方便对数字计算机进行编程，实现了一个Perl¹³³模块（IO::HyCon）；它为混合控制器提供了一个面向对象的接口。¹³⁴

IO::HyCon需要一个YAML格式¹³⁵的配置文件，该文件描述了模拟计算机的实际设置，即各种计算元件的地址、串行线路参数等。下面是一个典型的极简示例：¹³⁶

```yaml
serial:
  port: /dev/cu.usbserial-DN05OL10
  bits: 8
  baud: 115200
  parity: none
  stopbits: 1
  poll_interval: 10
  poll_attempts: 20000
types:
  0: PS
  1: SUM8
  2: INT4
  3: PT8
  4: CU
  5: MLT8
  6: MDS2
  7: CMP4
  8: HC
manual_potentiometers:
elements:
  INT-0: 0x0030
  INT-1: 0x0031
  INT-2: 0x0032
  INT-3: 0x0033
```

它由以下部分组成：

**serial：** 本节描述通信设置。port定义串行设备。其名称取决于操作系统和所使用的USB串行适配器。其余参数为默认值，在大多数情况下可以保持不变。

135 关于YAML的详细描述，参见https://yaml.org/spec/1.2/spec.html （2019年10月3日访问）。

136 还有更多的可选节和设置，将在需要时介绍。

**types：** Analog Paradigm Model-1中的每个计算元件在被选择进行读出时，会在数据总线上返回一个8位值。本节包含这些代码与实际计算元件类型之间的映射。

**manual_potentiometers：** 本节允许定义可由混合控制器读取的手动电位器。如果仿真需要通过系数电位器进行用户输入，并且这些电位器的值在模拟计算机运行期间或之后需要被读取，那么这一节将非常有用。

**elements：** 所有需要由混合控制器读出的元件都必须在本节中定义。应避免使用像INT-0这样的名称，而应使用有意义的变量名，如phi-dot等。

一个典型的混合计算机程序如下所示：

```perl
use strict;
use warnings;
use IO::HyCon;

my $ac = IO::HyCon->new();
```

标量变量`$ac`是一个对象，可以访问`IO::HyCon`中实现的所有方法，以控制模拟计算机的操作和设置。调用`$ac->ic()`会将模拟计算机设置为IC模式，`$ac->op()`将启动OP阶段，等等。

### 7.3 弹丸轨迹

第一个示例基于第6.6节中描述的弹道轨迹仿真，是数字计算机和模拟计算机交替工作的一个例子。此混合计算机设置使用了图6.21所示的模拟计算机设置。这里唯一的区别是，用于以下方程的系数电位器

$\dot{x}_0 = \cos(\varphi)$

$\dot{y}_0 = \sin(\varphi)$

是混合控制器八个数字电位器中的两个。$\dot{x}_0$对应DPT0，$\dot{y}_0$对应DPT1。

该仿真的目的是确定此二维设置中大炮的仰角，以便命中用户自定义$x$坐标处的目标。数字计算机设置一个仰角$\varphi$，从而设置$\dot{x}_0$和$\dot{y}_0$，然后开始一次仿真运行，并读取弹丸着地时的$x$分量。根据δ = x − x_target（目标点与着地点之间的距离），确定新的φ，依此类推，直到δ足够小。

![](img/91599d88757ed8c75960eb83f4f85a12_212_0.png)

图7.2 HALT检测与目标输入

假设大炮位置的y分量满足 y_cannon > 0，而目标的y分量为 y_target = 0。如图7.2所示，使用比较器，当弹丸击中地面时会产生外部停止信号。该信号连接到混合控制器的EXTHALT输入端。x_target可以通过比较器下方所示的电位器手动设置。其输出不连接到任何东西，因为它只在一次运行后由数字计算机读出，以确定脱靶距离δ。

此混合仿真的配置文件如下所示——省略了serial和types节，因为它们与第197页所列的相同。产生混合计算机设置的数字部分所需值的两个计算元件在elements节中定义，并标记为X和TARGET，分别代表x_shell和x_target。

```yaml
elements:
  X:     0x0221
  TARGET: 0x0051
```

相应的此混合仿真的Perl程序如下所示，并且很直观。

```perl
use strict;
use warnings;
use IO::HyCon;

my $ac = IO::HyCon->new();

$ac->set_ro_group('X', 'TARGET');

$ac->set_ic_time(1);

$ac->enable_ext_halt();

my $phi = 3.1415 / 4;  # Start with 45 degrees of elevation
while (1) {
    $ac->set_pt(0, cos($phi));
    $ac->set_pt(1, sin($phi));

    $ac->single_run_sync();
    my $result = $ac->read_ro_group();
    my $delta = $result->{X} - $result->{TARGET};
    $phi -= $delta / 10;
    printf("%0.4f\t%0.4f\t%0.4f\n",
        $result->{X}, $result->{TARGET}, $delta);
}
```

在第6行实例化IO::HyCon对象$ac之后，在第8行定义了读出组。混合控制器可以以最小的时钟偏差读取该读出组的所有元件——在这种特定情况下，这并不是必需的，因为当模拟弹丸击中地面时，模拟计算机已经停止，因此所有变量都是静态的。通过在第19行调用single_run_sync启动单次运行，包括1 ms的IC周期和2 ms的OP阶段。此方法会阻塞，直到达到定义的OP时间或出现外部停止信号。在此仿真中，后一事件总是先于超时发生，因为当k0 = 10³时，弹丸会在不到2 ms的时间内击中地面。

在这样一次单次运行之后，通过调用read_ro_group读取x_shell和x_target。这会返回一个哈希，其中包含为读出组中定义的每个元件提供的一个键值对。基于这些值，在第22行确定δ。然后使用该值在第23行确定新的仰角φ。¹³⁸ 在开始下一次使用此角度的单次运行之前，当前x_shell、x_target和δ的值会打印在屏幕上。

### 7.4 数据采集

使用混合控制器，还可以在较长的计算机运行期间的HALT阶段或OP阶段中连续采集数据，如下例所示。¹³⁹ 目标是求解一维波动方程

$\frac{1}{c}\ddot{u} - \frac{\partial^2 u}{\partial x^2}=0.$

和之前一样，对$x$的导数用差商近似，得到

$\frac{1}{c}\ddot{u} - \frac{u_{i-1}-2u_i+u_{i+1}}{(\Delta x)^2}=0$

其中 $\Delta x = \frac{x}{n}$，$n \in \mathbb{N}$。定义

$\lambda := \frac{c}{(\Delta x)^2} = \frac{c n^2}{x^2}$

得到适合推导模拟计算机设置的形式：

$\ddot{u}_i = \lambda (u_{i-1}-2u_i+u_{i+1})$

为了进一步简化，假设 $n=4$ 且 $\lambda=1$，最终得到以下耦合常微分方程组：

- $\ddot{u}_0 = \delta(t)$
- $\ddot{u}_1 = u_0 -2u_1 + u_2$
- $\ddot{u}_2 = u_1 -2u_2 + u_3$
- $\ddot{u}_3 = u_2 -2u_3 + u_4$
- $\ddot{u}_4 = u_3 -2u_4 + u_5$
- $u_5 = 0$

$\delta(t)$表示仿真运行开始时（即$t=0$时）出现的冲激。图7.3显示了最终的计算设置，由四个基本相同的单元组成，每个单元包含两个积分器、一个反相加法器和一个系数电位器。使用混合控制器作为数据记录器，现在可以在仿真运行期间采集变量$u_1,\dots,u_4$。¹⁴⁰

