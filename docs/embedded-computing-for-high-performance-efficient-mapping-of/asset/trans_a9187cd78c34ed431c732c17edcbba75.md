
power management (DPM) are techniques related to architectures and hardware to reduce energy/power consumption.

Power consumption is represented in watts (W), which directly affects system heat (temperature) and the possible need for cooling schemes. The total power consumption of a CMOS integrated circuit (IC) is the sum of the static power and the dynamic power as represented by Eq. (2.6).

```
$P = P_{static} + P_{dynamic}$ (2.6)
```

Short circuits and leakage currents are responsible for power consumption even when transistor devices are not switching. The static power consumption ($P_{static}$) can be calculated by Eq. (2.7), where $V_{cc}$ represents the supply voltage (sometimes also represented as $V_{dd}$) and $I_{cc}$ (sometimes represented as $I_{dd}$) represents the overall current flowing through the device which is given by the sum of the leakage currents. The static power depends mainly on the area of the IC and can be decreased by disconnecting some parts of the circuit from the supply voltage and/or by reducing the supply voltage.

```
$P_{static} = V_{cc} \times I_{cc}$ (2.7)
```

The dynamic power ($P_{dynamic}$) consumption can be calculated by Eq. (2.8), where $V_{cc}$ represents the supply voltage, $\beta$ represents the activity factor, $C_L$ represents the load capacitance, and $f$ denotes the clock frequency at which the device is operating. $P_{dynamic}$ is proportional to the switching activity of the transistors in the IC. Thus, one way to reduce the dynamic power is to make regions of the IC non active and/or to reduce $V_{cc}$ and/or $f$.

```
$P_{dynamic} = \beta \times C_L \times V_{cc}^2 \times f$ (2.8)
```

When reducing the dynamic power by reducing the frequency and/or the supply voltage, it is common to attempt to reduce the value of the supply voltage as its value impacts in a quadratic way the dynamic power ($P_{dynamic} \propto V_{cc}^2$). Reducing the clock frequency clearly has a negative impact on execution time as the components will operate at a lower clock frequency thus translating into longer execution times, increased latencies, or lower throughputs. Moreover, reducing supply voltage may also imply a reduction of the clock frequency. Typically, the system provides a table of discrete values of supply voltages that they can operate under along with the corresponding maximum clock frequencies (known as frequency-voltage table). Thus, the supply voltage ($V_{cc}$) can be seen as a linear function of the clock frequency as depicted in Eq. (2.9) and the dynamic power consumption is directly proportional to the cube of the clock frequency ($P_{dynamic} \propto f^3$), as shown in Eq. (2.10).

## 频率-电压对

The operating performance points (OPPs) depend on the components (e.g., CPUs) and the support included in the system implemented in the IC.

For example, the Texas Instruments OMAP-L138 IC includes an ARM9 RISC processor and a VLIW DSP. The following table presents the OPPs for three subsystems of the IC, the ARM processor, the DSP, and the RAM.

| 子系统 | 频率 (MHz) | 电压 (V) |
| :--- | :--- | :--- |
| DSP C674x 和 ARM926EJ-S | 456 | 1.3 |
| | 375 | 1.2 |
| | 200 | 1.1 |
| | 100 | 1.0 |
| DDR2 | 312 | 1.3 |
| | 312 | 1.2 |
| | 300 | 1.1 |
| | 266 | 1.0 |

Intel also has provided control over the processor’s operating frequency and supply voltage with the Enhanced Intel SpeedStep Technology.*

*德州仪器公司，OMAP-L138 6000 DSP+ARM处理器，SPRS586I—2009年6月—2014年9月修订。
†英特尔公司，面向英特尔奔腾M处理器的增强型英特尔SpeedStep技术，白皮书，2004年3月。

The tuple consisting of the voltage and the corresponding maximum clock frequency is known as the operating performance point (OPP). OPP = (f,V).

Table 2.1 presents an example of four OPPs of a hypothetical processor. This example considers the processor can operate with a supply voltage of 1 V at a maximum clock frequency of 300 MHz, or 1.2 V at 600 MHz, or 1.3 V at 800 MHz, or at 1.4 V at 1 GHz. These OPPs can be managed by the operating system (OS) and/or by the application via system library functions.

$V_{cc} = \alpha \times f$ (2.9)

$P_{dynamic} = \beta \times C_L \times \alpha^2 \times f^3$ (2.10)

To reduce dynamic power and static power consumption, two main mechanisms can be used, namely, dynamic voltage and frequency scaling (DVFS) and dynamic power management (DPM), respectively. These two techniques are described in the following subsections.

## 表2.1 频率-电压表示例（表示OPP）

| 频率 (MHz) | 供电电压 (V) |
| :--- | :--- |
| 300 | 1.0 |
| 600 | 1.2 |
| 800 | 1.3 |
| 1,000 | 1.4 |

The energy consumed, represented in Joules (J), during a period of activity is the integral of the total power dissipated (Eq. 2.6 for CMOS ICs) over that period. Eq. 2.11 represents in a simplified way the total energy consumed during a period T (in seconds) as the product of the average power dissipated over that period (P_avg) by T. For a given application, one can save energy if power consumption/dissipation is reduced and the execution time is not increased as much, or conversely if the execution time is reduced without a large increase in power dissipation.

## ACPI：高级配置与电源接口

ACPI is a standard interface specification supported by hardware and software drivers. Usually the operating system uses this API to manage power consumption, but the API can also be used by applications.

ACPI considers four global states (from G0 to G3, with a subdivision in six sleep states S0 to S5), performance states (based on the possible OPPs), known as P-states (and from P0 to P15 at maximum, being P0 the state operating at maximum clock frequency and resulting in the highest power dissipation). Processor states, known as C-states (and usually from C0 to C3, but depending on the processor). The C-states represent operating (C0), Halt (C1), Stop-Clock (C2), and Sleep (C3) states.

*统一EFI公司。高级配置与电源接口（ACPI）概述。修订版5.1，2014年7月。http://www.uefi.org/sites/default/files/resources/ACPI_5_1_Release.pdf.

```
E = P_avg × T (2.11)
```

Energy consumption is not directly associated with heat but affects battery usage. Thus by saving energy one is also extending the battery life or the length of the interval between battery recharges. On the other hand, energy efficiency is a term related to performing the work needed with as less energy as possible, sometimes being quantified by the work done per Joule (e.g., samples/J, Gbit/J, and frames/J). Two common metrics used to represent the trade-off between energy consumption and performance are the energy delay product (EDP) and the energy delay squared product (ED²P). EDP is obtained by multiplying the average energy consumed by the computation time required [31]. Both EDP and ED²P give more importance to the execution time than to the energy consumed. Compared to EDP, by squaring the computation time required, the ED²P metric gives even more importance to execution time than to energy consumption. One can give even more importance to performance by raising the computation time required by values >2.

### 2.6.1 动态电源管理

Dynamic power management (DPM) techniques [32] use the various operating CPU modes such as sleep (idle) and active (running) to dynamically reduce power and possibly energy consumption. These techniques need to take into account the switch cost, in terms of time and energy, between those modes. Fig. 2.23 presents an example of a power state machine representing a microprocessor with three power states (RUN, IDLE, and SLEEP). Each state dissipates a certain level of power. The

![](img/55beb9162c0073b3a3d7b44f1d5873e8_59_0.png)

状态之间的转换显示了电源状态之间转换相关的延迟。The RUN state may also have different levels according to the support of DVFS, DVS, or DFS.

### 2.6.2 动态电压和频率调整

Dynamic voltage and frequency scaling (DVFS) is a technique that aims at reducing the dynamic power consumption by dynamically adjusting voltage and frequency of a CPU [33]. This technique exploits the fact that CPUs have discrete frequency and voltage settings as previously described. These frequency/voltage settings depend on the CPU and it is common to have ten or less clock frequencies available as operating points. Changing the CPU to a frequency-voltage pair (also known as a CPU frequency/voltage state) is accomplished by sequentially stepping up or down through each adjacent pair. It is not common to allow a processor to make transitions between any two nonadjacent frequency/voltage pairs.

## 测量功率和能量

Power dissipation can be monitored by measuring the current drawn from the power supply to the system or to each device. There are specific boards providing this kind of measurements but this scheme requires access to the power rails for the inclusion of a shunt resistor from the Vcc supplied and the device/system under measurement (note that P = V x Icc). This is typically a problem and only useful in certain conditions or environments. Another possibility is to use pass-through power meters as the ones provided for USB interfaces.

Some computing systems provide built-in current sensors and the possibility to acquire from the software side the power dissipated. Examples of this are the support provided by the ODROID-XU3, which allows us to measure the power dissipation of the ARM Cortex big.LITTLE A15 and A7 cores, GPU and DRAM individually, and the NVIDIA Management Library (NVML) which allows to report the current power draw in some of their GPU cards.
