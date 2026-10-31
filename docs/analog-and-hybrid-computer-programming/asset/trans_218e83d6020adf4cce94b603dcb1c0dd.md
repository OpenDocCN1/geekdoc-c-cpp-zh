
![](img/91599d88757ed8c75960eb83f4f85a12_215_0.png)

### Fig. 7.3. 求解一维波动方程的计算机程序

对应混合控制器的配置文件基本上与第197页所示的最小示例相同，只是做了以下更改和补充：

```yaml
wave_equation.yml
elements:
  U1: O260
  U2: O261
  U3: O262
  U4: O263
problem:
  times:
    ic: 10
    op: 200
  ro-group:
    - U1
    - U2
    - U3
    - U4
```

问题部分已添加。它包含各种计时设置、读出组（ro-group）的定义以及此处不需要的其他可选子部分。读出组定义了在模拟的 OP 阶段以等间隔读取的计算元素列表。在本例中，读出组由标记为 U1、U2、U3 和 U4 的元素组成。

使用此配置文件的相应 Perl 程序如下所示：

```perl
use strict;
use warnings;
use IO::HyCon;

my $ac = IO::HyCon->new();  # Create a new hybrid controller object.
$ac->setup();               # Setup the analog computer
$ac->single_run_sync();     # Start a single run.
$ac->get_data();            # Get the data gathered
$ac->plot();                # and generate a plot.
```

方法调用 $ac->setup() 执行所有基本设置操作，例如设置初始和运行时间，以及在配置文件中指定时定义读出组。如果定义了这样的组，混合控制器将在每次模拟计算机运行期间自动收集数据。收集到的数据存储在 $ac 对象中，可以通过调用方法 $ac->get_data() 提取，该方法返回一个数组引用。另一个有用的方法是 $ac->plot()，它可以参数化以产生不同的绘图样式，并且要求在数字计算机上安装 gnuplot。

仅调用 $ac->plot() 如上例所示，会得到图 7.4 所示的结果。图中四条线代表四个变量 u1,...,u4。每个变量代表一维波动方程问题中 x 轴上的一个位置。

对于这类问题，更希望对记录的变量有一个更 3d-ish 的显示。plot() 方法也支持这种显示样式。调用 $ac->plot(type => '3d') 会得到图 7.5 所示的图，它比之前显示的叠加 2d 图更直观。

![](img/91599d88757ed8c75960eb83f4f85a12_219_0.png)

### Fig. 7.6. 反向摆的修改设置

![](img/91599d88757ed8c75960eb83f4f85a12_220_0.png)

### Fig. 7.7. 受控倒立摆的控制电路

```python
import serial

from readchar import readchar
from time import sleep

# Hybrid Controller serial setup
HC_PORT = "/dev/cu.usbserial-DN050L10"
HC_BAUD = 250000
HC_BYTE = 8
HC_PARITY = serial.PARITY_NONE
HC_STOP = serial.STOPBITS_ONE
HC_RTSCTS = False
HC_TIMEOUT = 2

# Addresses of the computing elements to be read
HC_SIM_X_POS = "0223" # Position of the cart
HC_SIM_X_VEL = "0222" # Velocity of the cart
HC_SIM_ANGLE = "0161" # Angle of the pendulum
HC_SIM_ANGULAR_VEL = "0160" # Angular velocity of pendulum

HC_SIM_DIRECTION_1 = "D0" # Digital out 0=1: push right
HC_SIM_DIRECTION_0 = "d0" # Digital out 0=0: push left
HC_SIM_IMPULSE_1 = "D1" # Digital out 1=1: apply force
HC_SIM_IMPULSE_0 = "d1" # Digital out 1=0: stop applying force

# Model-1 Hybrid Controller: commands and responses
HC_CMD_RESET = "z" # Reset hybrid controller
HC_CMD_INIT = "i" # Initial condition
HC_CMD_OP = "o" # Start simulation run
HC_CMD_ROGROUP = "f" # Define a readout group

HC_RSP_RESET      = "RESET" # HC response to HC_CMD_RESET

# Send a command to the hybrid controller
def hc_send(cmd):
    global dbg_last_sent
    dbg_last_sent = cmd
    hc_ser.write(cmd.encode("ASCII"))

# Get a response from the hybrid controller
def hc_receive():
    # As the hybrid controller ends each output with
    # "\n", we can conveniently use readline
    return hc_ser.readline().decode("ASCII").split("\n")[0]

# When reading values from the hybrid controller, the result
# is formatted as "<value><space><id/type>\n". The type
# information is ignored in the following.
def hc_res2float(str):
    f = 0
    try:
        f = float(str.split(" ")[0])
        return f
    except:
        print("ERROR #2: FLOAT CONVERSION:", str)
        print("Last command sent:", dbg_last_sent)
        print("Length of received string:", len(str))
        print("Hex output of received string:","".join("{:02x}".format(ord(c)) for c in str))
        sys.exit(2)

# Query the current state of the simulation, which consists of
# the position and the velocity of the cart, and the angle and
# angular velocity of the pendulum
def hc_get_sim_state():
    hc_send(HC_CMD_ROGROUP)
    (res_x_pos, res_x_vel, res_angle, res_angle_vel) =
        hc_receive().split(',')
    return (hc_res2float(res_x_pos), hc_res2float(res_x_vel),
            hc_res2float(res_angle), hc_res2float(res_angle_vel))

# Reset the simulation (pendulum is in its upright position,
# cart is at x = 0)
def hc_reset_sim():
    hc_send(HC_CMD_INIT)
    sleep(0.05)        #time for condensators to recharge
    hc_send(HC_CMD_OP)
    sleep(0.05)        #time for the feedback string to arrive
    hc_ser.flushInput()

# Push the cart to the left or right, depending on the parameter a
def hc_influence_sim(a):
    if (a == 1):
        hc_send(HC_SIM_DIRECTION_1)
    else:
        hc_send(HC_SIM_DIRECTION_0)

    hc_send(HC_SIM_IMPULSE_1)
    sleep(HC_IMPULSE_DURATION / 1000.0)
    hc_send(HC_SIM_IMPULSE_0)

# Initialize the serial line
try:
    hc_ser = serial.Serial(port=HC_PORT,
                           baudrate=HC_BAUD,
                           bytesize=HC_BYTE,
                           parity=HC_PARITY,
                           stopbits=HC_STOP,
                           rtscts=HC_RTSCTS,
                           dsrdtr=False,
                           timeout=HC_TIMEOUT)

    sleep(1.5)
    dbg_last_sent = ""
except:
    print("ERROR #1: SERIAL PORT CANNOT BE OPENED.")
    sys.exit(1)

# Reset the hybrid controller
received = ""
while (received != HC_RSP_RESET):
    print("Hybrid Controller reset attempt...")
    hc_send(HC_CMD_RESET)
    sleep(1)
    received = hc_receive()
    if received != "":
        print("  received:", received)

# Define the readout group for all four parameters
hc_send('G' + HC_SIM_X_POS + ',' + HC_SIM_X_VEL + ',' + HC_SIM_ANGLE + ',' + HC_SIM_ANGLE_VEL + '.')
# Here follows the actual reinforcement learning code...
...
r1.py
```

使用模拟计算机作为陪练，强化学习系统根据值 x、ẋ、φ 和 φ̇ 学习平衡倒立摆。每当 φ 超过约 30 度或小车位置 x 离开区间 [−1,1] 时，当前模拟运行将被终止并开始下一次运行。起初，强化学习系统相当随机地平衡，但随着时间的推移会迅速改进。在训练结束时，摆在很大程度上无限期地保持在稳定位置。¹⁴⁶

## 第 8 章 总结与展望

编程模拟计算机，因此混合计算机，从根本上不同于数字计算机中使用的算法方法，正如前几章所示。乍一看，使用模拟计算机似乎比编程数字计算机更复杂、更麻烦。这是误导的。除了缩放问题之外，编程模拟计算机比编程数字计算机更直接，因为问题的数学描述基本上足以设置模拟计算机——而在数字计算机的情况下，必须考虑大量额外的怪癖和复杂性。

模拟计算机的主要优点，无论是作为独立系统还是作为混合计算机设置的一部分，都是

- 该类机器所表现出的极高的并行度，
- 同样高的能源效率，以及
- 模拟计算机获得的解的稳定性——例如，没有类似数值不稳定的情况。

在数字计算机中，位从 0 变为 1 或反之的每次变化都需要给一个小的寄生电容充电或放电。结合其他效应，例如逻辑门典型输出驱动级结构，这导致时钟频率与数字计算机整体能耗之间存在超线性关系。鉴于今天高达数 GHz 的时钟频率，这导致典型多核
