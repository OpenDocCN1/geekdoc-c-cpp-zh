
```
G91 G10 L13 P10 R-0.05;
```

（以增量方式向10号偏置中输入-0.05 mm，作为D代码的磨损补偿值，将其值改为-0.55，从而使刀具半径等于9.45 mm）

```
G90 G10 L10 P10 R-500;
```

（以绝对方式向10号偏置中输入-500 mm，作为H代码的几何补偿值）

```
G91 G10 L10 P10 R5;
```

（以增量方式向10号偏置中输入5 mm，作为H代码的几何补偿值，使其减小5 mm，变为-495 mm。因此，在相同的程序下，如果使用G43进行长度补偿，同一刀具将多切入工件5 mm）

```
G91 G10 L11 P10 R0.5;
```

（以增量方式向10号偏置中输入0.5 mm，作为H代码的磨损补偿值。因此，磨损值将增加0.5 mm，在相同的程序下，如果使用G43进行长度补偿，同一刀具将少切入工件0.5 mm）

当然，系统变量也可用于实现相同的功能。例如，第一个和最后一个示例分别等价于（参见表3.4）

```
#13010 = 5;
#10010 = #10010 + 0.5;
```

## 13.5 车床上补偿值的数据输入

可以指定径向/轴向距离、刀尖半径和刀尖号的几何值以及磨损值。与前面所述格式的一个区别是：在车床上输入补偿值时不使用L字。格式如下：

```
G10 P_ X_ Y_ Z_ R_ Q_;    (Absolute mode)
G10 P_ U_ V_ W_ C_ Q_;    (Incremental mode)
```

其中

- P0 指工件偏移值，
- P1至P64 指与1至64号偏置对应的磨损补偿值（假设有64个偏置号），
- P1001至P10064 指与1至64号偏置对应的几何补偿值，
- X/U、Y/V（如果Y轴可用）和Z/W 在绝对/增量模式下包含各轴所需的数值，
- R/C 在绝对/增量模式下包含刀尖半径，Q 包含刀尖号（两种模式下均如此）。

刀尖号或刀鼻号是由Fanuc针对不同的刀具方位任意定义的。图13.1显示了后置刀架式车床上的Fanuc定义的刀尖号。请注意，为几何偏置号指定的Q值会自动赋予对应的磨损偏置号，反之亦然。换句话说，Q的几何补偿值和磨损补偿值始终相同。这是数控系统的一项内置安全功能，可消除指定刀尖号时出现无意错误的可能性。

并非G10程序段中的所有补偿值都需要指定。未指定的值保持不变。下面给出一些示例：

```
G10 P10010 X-100 W5;   (Corresponding to geometry offset number
                       10, i.e., in the G10 row on the geometry offset
                       screen, the radial compensation value is set
                       to -100 mm, and the axial compensation value
                       is increased by 5 mm. Mixed coordinate mode
                       is allowed in G10)

G10 P10 X0 Z0;         (Corresponding to wear offset number 10,
                       the radial as well as the axial compensation
                       values are set to zero. In other words, the
                       radial and axial wear offsets are made zero,
                       for the W10 row on the wear offset screen)

G10 P10010 R0.8 Q3;    (Corresponding to geometry offset number
                       10, i.e., in the G10 row on the geometry offset
                       screen, the nose radius is set to 0.8 mm. The
                       tip number is set to 3 on both geometry and
                       wear offset screens, corresponding to offset
                       number 10)
```

在这种情况下，也可以使用系统变量来获得相同的结果。上面给出的三个G10程序段可以被以下程序段替换（参见表3.2）：

```
For G10 P10010 X-100 W5; use
#2710 = -100;
#2810 = #2810 + 5;
For G10 P10 X0 Z0; use
#2010 = 0;
#2110 = 0;
For G10 P10010 R0.8 Q3; use
#2910 = 0.8;
#2310 = 3;
```

另一个示例：如果需要清除全部64个偏置，可以在循环中执行G10。如果有99个偏置可用，只需将给定程序中的64改为99即可：

```
O8024 (CLEAR LATHE OFFSETS WITH G10);
#100 = 1;                         (Counter initialized)
WHILE [#100 LE 64] DO 1;          (Start of loop)
G10 P[#100] X0 Z0 R0;             (Clears wear offset)
G10 P[10000 + #100] X0 Z0 R0 Q0;  (Clears geometry offset)
#100 = #100 + 1;                  (Counter incremented)
END 1;                            (End of loop)
M99;                              (Returns to the calling program)
```

使用系统变量也可以完成同样的操作，尽管在这种情况下G10方法更简单：

```
O8025 (CLEAR LATHE OFFSETS WITH SYSVAR);
#100 = 1;                         (Counter initialized)
WHILE [#100 LE 64] DO 1;          (Start of loop)
[#2000 + #100] = 0;               (Clears X-axis wear offset)
[#2100 + #100] = 0;               (Clears Z-axis wear offset)
[#2200 + #100] = 0;               (Clears nose radius wear offset)
[#2300 + #100] = 0;               (Clears tip number)
[#2700 + #100] = 0;               (Clears X-axis geometry offset)
[#2800 + #100] = 0;               (Clears Z-axis geometry offset)
[#2900 + #100] = 0;               (Clears nose radius geometry offset)
#100 = #100 + 1;                  (Counter incremented)
END 1;                            (End of loop)
M99;                              (Returns to the calling program)
```

## 13.6 参数值的数据输入

到目前为止，读者可能会产生这样的印象：如果机床具有宏程序编程功能，就不需要使用G10。然而，系统变量方法仅限于到目前为止所讨论的内容。大多数参数没有关联的系统变量。因此，G10是通过程序更改参数的唯一方法。G10的这种用途通常被称为可编程参数输入。

与之前G10应用的一个区别是：当用于参数输入时，G10表现为模态代码。一旦进入参数模式，就可以在后续程序段中输入任意多个所需参数，直到该模式被G11取消。另一个区别是不允许使用十进制小数值。因此，如果参数与某个轴向距离有关，则必须按最小输入增量来指定该值（即在毫米模式下以微米为单位，在英制模式下以0.0001英寸的步长）。请注意，如果同一参数也定义了系统变量，则在此类变量中使用毫米或英寸（视情况而定）值。

请注意，最适合大多数情况的参数值已由MTB（机床制造厂）设置。不建议对这些值进行任何更改，因为不正确的设置可能导致机床出现不可预测的、可能危险的行为，从而造成操作员受伤或机床损坏，或两者兼有。然而，某些参数可能需要更改以适应特定应用，例如软件超程极限、车床上的G代码系统选择（A、B或C）、使用G00的直线定位、计算器型数据输入（例如，将X10解释为10 mm，而不是10 μm）等。但在这种情况下，在进行任何更改之前，请先记下原始设置，以便在设置不正确时能够恢复到原始值。任何更改都必须由有经验的人员在彻底研究打算更改的参数后完成。所有参数的完整说明可在随机附带的*《参数手册》*中找到。

进一步讨论需要清楚理解参数的类型。大致有四类参数：*位型*（允许的数据为0或1）、*字节型*（允许的数据范围为-128至127，或0至255）、*字型*（允许的数据范围为-32,768至32,767，或0至65,535）和*双字型*（允许的数据范围为-99,999,999至99,999,999）。位型参数有八位的行（最右边是位#0，最左边是位#7）。一些位型参数有多个八位行，每行对应一个机床轴。其他一些参数也有对应不同轴的多个行。在两轴车床上，第一行对应X轴，第二行对应Z轴。在三轴铣床上，三行分别对应X、Y和Z轴。这类参数称为轴型参数。为了有效利用内存，不同类型的参数用于不同的应用。例如，I/O通道是字节型参数，而设置软件超程极限（以微米为单位，机床坐标系）的参数是字型和双字型参数。

可编程参数输入的格式如下：

```
G10 L50;       (Parameter entry mode starts)
N_ R_;         (For parameters other than axis-type)
N_ P_ R_;      (For axis-type parameters)
...
...             (Multiple parameter entry is permitted)
...
G11;            (Parameter-entry mode ends)
```

其中

- L50 选择参数输入模式，
- N 包含参数号，
- P 包含轴号（仅用于轴型参数），
- R 包含该参数的指定值。
