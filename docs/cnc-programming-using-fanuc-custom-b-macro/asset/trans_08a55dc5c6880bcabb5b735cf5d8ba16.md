
## 第8章 复杂运动生成

### 8.1 引言

到目前为止，只讨论了宏编程的基本工具。借助这些工具，除了后续章节中讨论的其他若干应用外，还可以生成复杂的刀具路径。本章给出了一些复杂运动生成的示例。一般来说，在铣床（二维加工）上实现比在车床上更容易，因为在车床上生成的刀具路径必须与合适的固定循环（G71/G72/G73）配合使用，以避免较大的切削深度。因此，先讨论铣削示例。

### 8.2 半径均匀变化的圆弧

考虑图8.1所示的槽，其形状为半径均匀增大的圆弧（AB）。起始半径和终止半径分别为35 mm（CA）和40 mm（CB）。圆弧角为60°，起始角为15°。工件零点（所选WCS的原点或基准点，在G54、G55、...、G59中选择）位于O。圆弧中心（C）位于坐标(30, 20)。假设槽深为3 mm。

由于圆弧半径连续变化，本例不能使用圆弧插补。唯一的方法是在圆弧AB上定位间距很近的点，并用直线插补连接这些点。这些点之间的间距必须仔细选择。较小的值会提高圆弧的平滑度。然而，值太小会增加计算量，可能导致刀具运动迟缓。（刀具运动迟缓的另一个也是主要的原因是每个刀具路径段都涉及加速/减速。因此，有效进给率可能远小于指定进给率。）

![](img/1341ce50369ce8fcfb8dc3539d51c52f_183_0.png)

**图8.1** 半径均匀增大的圆弧。

圆弧上某点P的坐标（X_p, Y_p）作为角度θ的函数，可用以下方程求得，假设半径r随θ均匀（线性）变化：

r = r_A + ((r_B − r_A) θ) / ∠ACB

X_p = X_c + r cos(θ + θ_A)

Y_p = Y_c + r sin(θ + θ_A)

其中

- r_A = CA（起始半径）
- r_B = CB（终止半径）
- ∠ACB = 圆弧的包含角
- θ_A = CA与X轴的夹角（起始角）
- X_c = 圆弧中心C的X坐标
- Y_c = 圆弧中心C的Y坐标

在圆弧起点（A），θ的值为零。此后，它逐渐增大以到达终点（B）。这构成了该问题算法的基础。

开发宏算法的第一步是决定如何使用宏。这里假设调用宏时刀具位于圆弧起点（A）上方2 mm处，宏执行结束时刀具回到圆弧终点（B）的同一Z高度。还假设调用程序使用毫米（G21）、XY平面（G17）、进给率单位为毫米/分钟（G94）、绝对坐标（G90）、无半径补偿（G40），且无活动固定循环（G80）。进一步假设主轴装夹正确刀具（直径6 mm的槽钻），并以正确转速旋转。最后假设工件坐标系选择（G54）和刀具长度补偿（G43 H_）正确。在这些假设下，该宏不能说是很通用，但此处目的是描述生成变半径圆弧的技术。当然，圆弧会通过若干可变参数定义，从而使其相当通用。基本程序准备好后，按需求使其更通用就很容易。实际上，不建议一开始就考虑所有可能性，因为这种方法会使编程困难，并留下足够的逻辑错误空间。

槽的参数、为这些参数选择的字母地址以及相关的局部变量（按照参数规格I，参见表7.4）在表8.1中给出。由于字母地址将用于在G65/G66宏调用中传递数据，选择字母地址时应尽可能反映其实际物理意义。这有助于回忆哪个字母地址对应哪个参数。在本例中，除A和F无法使用外，参数的首字母被选作字母地址。

**表8.1.** 图8.1中槽的参数及所选字母地址

| 槽的参数 | 所选字母地址 | 关联变量 |
|---|---|---|
| 起始角 | A | #1 |
| 圆弧包含角 | I | #4 |
| 起始半径 | S | #19 |
| 终止半径 | E | #8 |
| 槽深 | D | #7 |
| 圆心X坐标 | X | #24 |
| 圆心Y坐标 | Y | #25 |
| 下刀进给率 | F | #9 |
| 铣削进给率 | M | #13 |

现在可以写出适合WHILE...DO END循环的该问题算法（注意，在WHILE语句中，指定条件在循环开始时检查）：

- 1. 以指定下刀进给率下刀进入至指定深度。
- 2. 选择角度增量Δθ，并赋值θ = Δθ。
- 3. 如果θ大于圆弧包含角，转到步骤8。
- 4. 使用给定公式计算 \(r\)、\(X_p\) 和 \(Y_p\)。
- 5. 以指定铣削进给率通过G01移动到计算坐标 \((X_p, Y_p)\)。
- 6. 角度递增 \((\theta = \theta + \Delta\theta)\)。
- 7. 转到步骤3。
- 8. 将刀具退回至工件上方2 mm。
- 9. 返回调用程序。

程序号8014基于该算法。要加工图8.1的槽，需要如下调用该宏：

```
G65 P8014 A15 I60 S35 E40 D3 X30 Y20 F20 M60;
```

其中下刀进给率和铣削进给率分别取20和60 mm/min。

```
O8014 (ARC WITH VARYING RADIUS);
G01 Z-[ABS[#7]] F#9;        (Plunge entry with the specified plunge feedrate at the start point A. Use of ABS function accepts both positive and negative values for the depth of the slot. Step 1 complete)

#100 = 0.1;                (Δθ selected, in degrees)
#101 = #100;               (θ set equal to Δθ. Step 2 complete)
WHILE [#101 LE #4] DO 1;   (Exit from the loop if θ is greater than the included angle of the arc. Step 3 complete)

#102 = #19 + [[#8 − #19] * #101 / #4];  (r calculated)
#103 = #24 + #102 * COS[#101 + #1];      (X_p calculated)
#104 = #25 + #102 * SIN[#101 + #1];      (Y_p calculated. Step 4 complete)

X#103 Y#104 F#13;          (Move to (X_p, Y_p) with the specified milling feedrate. Step 5 complete)
#101 = #101 + #100;        (Angle θ incremented by the chosen step. Step 6 complete)
END 1;                     (End of WHILE loop. Step 7 complete)
G00 Z2;                    (The tool is now at the end point B of the arc. Here, it is retracted 2 mm above the workpiece. Step 8 complete)

M99;                       (Return to the calling program. Step 9 complete)
```

该宏对半径增大和减小都适用（即也适用于 \(r_A > r_B\) 时）。然而，对于顺时针圆弧（即图8.1中A和B位置互换，但仍希望从A到B加工），需要进行以下更改：

- 为Δθ指定负值（例如#100 = −0.1）。
- 在r的公式中，应使用θ的绝对值（当Δθ赋为负值时，θ变为负值）。因此，在计算r的代码块中将#101替换为ABS[#101]。计算X_p和Y_p的代码块无需更改。另一种方法是在宏调用代码块中，如果从CA移动到CB时包含角按顺时针方向度量，则为包含角指定负值。这样就不需要对程序做任何更改。
- WHILE块应比较绝对值。

针对略有不同的需求修改宏并不是好做法，因为经验较少的程序员可能会无意中破坏由某些专家程序员精心开发的宏。此外，机床的其他用户可能不知道宏中所做的更改。事实上，正是因为这一原因，宏通常受编辑保护。

鉴于上述讨论，最好再定义一个局部变量（例如，引用字母地址Q的#17），用于将角度增量（Δθ）的值传递给宏，使得正增量值生成逆时针圆弧，负值生成顺时针圆弧。此外，由于包含角的符号可能存在混淆，宏应接受两种符号。传递Δθ值的一个优点是宏的用户还可以控制圆弧的平滑度。程序号8015就是这样一个宏，可通过以下方式调用：

```
G65 P8015 A15 I60 S35 E40 D3 X30 Y20 F20 M60 Q-0.1;
```

或

```
G65 P8015 A15 I-60 S35 E40 D3 X30 Y20 F20 M60 Q-0.1;
```

对于顺时针圆弧。读者可以尝试使宏更通用，以适应特定应用。一旦程序核心准备好，修改它并不是什么难事，正如本例中O8014被修改为O8015所示。

```
O8015 (ARC WITH VARYING RAD - MODIFIED);
G01 Z-[ABS[#7]] F#9;      (Plunge entry with the specified plunge
                          feedrate at the start point A. Use of ABS
                          function accepts both positive and negative
                          values for the depth of the slot. Step 1
                          complete)
#100 = #17;               (Δθ set to the specified value in the Q-word,
                          which can be both positive and negative,
                          for CCW and CW arcs, respectively)
#101 = #100;              (θ set equal to Δθ. Step 2 complete)
```
