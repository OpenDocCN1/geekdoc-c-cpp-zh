
## CNC 技巧与技术

因为 Z 轴起始位置为 Z3.0（在固定循环中编程为 R3.0），刀具的总行程长度将为 27.925。所需啄钻次数为三次，*始终*按总行程距离计算，在我们的例子中为 27.925 mm。

27.925/3 的结果是 9.308333，作为最小 Q 深度值。由于公制单位要求四舍五入到三位小数，Q 深度必须向上取整，并且必须在固定循环中编程为 **Q9.309**（或更大）。因为要求的是*最小* Q 深度，所以循环中必须使用 Q9.309。注意舍入！将 9.308333 按数学方法正确舍入到三位小数是 9.308，但这不满足啄钻中*向上*取整的要求。正确的最小 Q 值将是 Q9.309，并在循环中使用。

如果你确实将最小 Q 深度用作 Q9.308，你将得到 9.308 x 3 次啄钻 = 27.924 深度，差一微米（！）——也就是 0.00003937 英寸。我故意使用了一个公制示例，利用微米作为 CNC 加工中心所能接受的最小单位。结果将是三次 9.308 的啄钻，以及第四次恰好一微米的啄钻！通过将 Q 深度改为 9.309，将会有两次 9.309 的啄钻和一次 9.307 的啄钻。因此，最终答案是：最小 Q 深度为 9.309 mm。如你所见，即使一微米也会在 CNC 工作中产生差异。

## 附录

![](img/0023bd5cc50494e6d7799ab76d437c8d_238_0.png)

## 附录 2

*2008年7月*

### 宏中的默认设置

以下程序对应图 A2-1。

```
(MAIN PROGRAM - EXAMPLE OF USAGE)
N1 G21
N2 G90 G00 G54 X0 Y0 S1200 M03
N3 G43 Z10.0 H01 M08
N4 G99 G81 R2.0 Z-15.9 F225.0 L0 (K0)
N5 G65 P8500 X50.0 Y37.5 D49.0 H6 A10.0 S1 (MACRO CALL)
N6 G80 Z10.0 M09
N7 G28 Z10.0 M05
N8 M30
%
```

```
O8500 (=== BOLT HOLE CIRCLE MACRO =========)
(== VARIABLE DEFINITIONS =================)
(X = #24 = X-CENTER LOCATION - DEFAULT=0 )
(Y = #25 = Y-CENTER LOCATION - DEFAULT=0 )
(D = #7 = BOLT CIRCLE DIAMETER          )
(H = #11 = NUMBER OF HOLES - RANGE 2-48  )
(A = #1 = FIRST HOLE ANGLE - DEFAULT=0 )
(S = #19 = FIRST HOLE NUMBER - DEFAULT=1 )
(== ERROR TRAPPING SECTION ==============)
IF[#7 EQ #0] GOTO9101
IF[#7 LE 0] GOTO9102
IF[#11 EQ #0] GOTO9103
IF[#11 NE FUP[#11]] GOTO9104
IF[[ABS[#11] LT 2] OR [[ABS[#11] GT 48]] GOTO9105
(== DEFAULTS ===========================)
IF[#24 NE #0] GOTO10
#24 = 0
N10 IF[#25 NE #0] GOTO20
#25 = 0
N20 IF[#1 NE #0] GOTO30
#1 = 0
N30 IF[#19 NE #0] GOTO40
#19 = 1
N40 IF[#19 NE FUP[#19]] GOTO9104
IF[#19 LT 1] GOTO9106
IF[#19 GT #11] GOTO9107
#10 = #4003
(== MAIN MACRO BODY START =================)
#7 = #7/2
WHILE[#19 LE #11] DO1
#30 = [#19-1]*360/#11+#1
G90 X[COS[#30]*#7+#24] Y[SIN[#30]*#7+#25]
#19 = #19+1
END1
(== MAIN MACRO BODY END ===================)
GOTO9999
(== ERROR MESSAGES ========================)
N9101 #3000=101 (BOLT DIAMETER MISSING)
N9102 #3000=102 (CANNOT BE ZERO OR NEGATIVE)
N9103 #3000=103 (NUMBER OF HOLES MISSING)
N9104 #3000=104 (HOLES DATA MUST BE INTEGER)
N9105 #3000=105 (RANGE OF HOLES IS 2 TO 48)
N9106 #3000=106 (START HOLE IS 1 OR HIGHER)
N9107 #3000=107 (START HOLE NUMBER TOO HIGH)
(== MACRO END =============================)
N9999 G#10
M99
%
```

## 螺栓孔圆周阵列 - 定义

| 变量 | # | 说明 | 默认值 |
|---|---:|---|---|
| X | 24 | X 方向的绝对中心位置 | 0.0 |
| Y | 25 | Y 方向的绝对中心位置 | 0.0 |
| D | 7 | 螺栓圆周直径 | n/a |
| H | 11 | EQSP 孔数 | n/a |
| A | 1 | 从 0° 起的第一个孔角度 | 0.0 |
| S | 19 | 起始孔编号 | 1 |
| R | n/a | 螺栓圆周半径（#72） | |
| B | n/a | 孔间角度（360/#11） | |

任意孔的 X 和 Y 坐标：

`X = cos((n-1) * B + A) * R + #24`

`Y = sin((n-1) * B + A) * R + #25`

`n=1` 对应第 1 个孔，`n=2` 对应第 2 个孔，依此类推。

![](img/0023bd5cc50494e6d7799ab76d437c8d_240_0.png)

```
G65 P8500 [X...] [Y...] D... H... [A...] [S...]
```

![](img/0023bd5cc50494e6d7799ab76d437c8d_241_0.png)

## 附录 3

*2008年8月*

### 创建自己的 G 代码

以下程序对应图 A3-1。

```gcode
O9013 (G13 CIRCULAR MILLING CYCLE — CLIMB MILLING)
#31 = ABS[#3]/2 (POSITIVE RADIUS OF THE CIRCULAR POCKET)
#11 = #4001 (STORE CURRENT G-CODE GROUP 01 — MOTION COMMANDS)
#13 = #4003 (STORE CURRENT G-CODE GROUP 03 — ABSOLUTE/INCREMENTAL)
#32 = #31-#[2000+#7] (TRUE POCKET RADIUS MACHINED)
IF [#32 LE 0] GOTO998 (ERROR IF RADIUS OFFSET VALUE IS TOO LARGE)
#33 = #32/2 (CALCULATED LEAD-IN/LEAD-OUT RADIUS)
G91 G03 X#32 I#33 J0 F[#9/2] (MOTION 1 — LEAD-IN ARC TOOL-PATH)
I-#32 F#9 (MOTION 2 - FULL CIRCULAR POCKET TOOLPATH)
X-#32 I-#33 J0 F[#9/2] (MOTION 3 — LEAD-OUT ARC TOOLPATH)
G#11 G#13 (RESTORE ORIGINAL G-CODES OF GROUPS 1 AND 3)
GOTO999 (BYPASS ERROR MESSAGE)
N998 #3000 = 13 (OFFSET TOO LARGE) (REFERS TO ACTUAL OFFSET SETTING)
N999 M99 (MACRO END)
%
```

## 宏 O8600 / O9013

### 圆弧切削循环 G13

| G65 # | 说明 |
|---|---|
| C 3 | 圆周型腔直径 |
| D 7 | 刀具半径偏置编号 |
| F 9 | 切削进给率 |

## G13 C..D..F..

见正文

![](img/0023bd5cc50494e6d7799ab76d437c8d_242_0.png)

#32

#31

C (#3)

#33

#33

#32

在 XY 中心且位于型腔底部启动宏

D (#7)

![](img/0023bd5cc50494e6d7799ab76d437c8d_242_1.png)

直径

半径偏置编号

## 程序注释与清单

缩放中心是零件中点 X37.5 Y37.5。成功解决方案的关键是将公共刀具路径放入子程序，并具有一个重要特性——在关闭缩放后，刀具必须返回原始起点——见程序段 N115。刀具看起来已经处于该位置——见程序段 N112 中的 X95.0 和程序段 N113 中的 Y37.5。当缩放生效时，情况并非如此。

请仔细查看主程序和子程序——它们的结构非常重要。

```
(SCALING .NC)
(MAIN PROGRAM)

(T01 = 20 MM DIA END MILL)
N1 G21
N2 G50
N3 G17 G40 G80 T01
N4 M06
N5 G90 G54 G00 X95.0 Y37.5 S2500 M03      (CONTOUR START POINT)
N6 G43 Z3.0 H01 M08                      (DEPTH OF THE SMALLEST CONTOUR)
N7 G01 Z-3.0 F300.0                       (SCALING DATA - 0.5 SCALE)
N8 G51 X37.5 Y37.5 P0.5                   (SCALED CONTOUR CUTTING)
N9 M98 P7003                             (DEPTH OF THE MIDDLE CONTOUR)
N10 G01 Z-5.9 F300.0                      (SCALING DATA - 0.7 SCALE)
N11 G51 X37.5 Y37.5 P0.7                  (SCALED CONTOUR CUTTING)
N12 M98 P7003                            (DEPTH OF THE LARGEST CONTOUR)
N13 G01 Z-8.5 F300.0                      (SCALING DATA - 0.9 SCALE)
N14 G51 X37.5 Y37.5 P0.9                  (SCALED CONTOUR CUTTING)
N15 M98 P7003                            (SCALING OFF - INCLUDED FOR SAFETY)
N16 M09
N17 G28 Z3.0 M05
N18 G50
N19 G00 X-50.0 Y250.0                    (PART CHANGE POSITION)
N20 M30
%

O7003 (SUBROGRAM FOR SCALING EXERCISE)
(D51 = CUTTER RADIUS = 10 MM)
N101 G01 G41 Y57.5 D51                   (LEAD-IN LINE WITH G41)
N102 G03 X75.0 Y37.5 I0 J-20.0 F250.0    (LEAD-IN ARC)
N103 G01 X10.0
N104 G02 X65.0 Y0 I-10.0 J0
N105 G01 X10.0
N106 G02 X0 Y10.0 I0 J10.0
N107 G01 Y65.0
N108 G02 X10.0 Y75.0 I10.0 J0
N109 G01 X65.0
N110 G02 X75.0 Y65.0 I0 J-10.0
N111 G01 Y37.5
N112 G03 X95.0 Y17.5 I20.0 J0          (LEAD-OUT ARC)
N113 G00 G40 Y37.5 F500.0               (LEAD-OUT LINE WITH G40)
N114 G50                                 (SCALING OFF)
N115 X95.0 Y37.5                         (RETURN TO ORIGINAL START - NOT SCALED)
N116 M99
%
```

## CNC 与安全

### 概述

加工安全对于任何机械（包括 CNC 设备）的成功运行至关重要。大多数公司遵守——并且在许多情况下超过——其所在辖区的职业安全法律法规。最近的一次海报宣传活动确定了基本安全规则：

**始终遵守所有安全规则**

这句简短的广告语朗朗上口、巧妙——而且非常正确。安全通常与机加工车间环境中零件的实际加工联系在一起。尽管这是事实，但 CNC 程序员负有重大责任，应将安全功能构建到每个 CNC 程序中。

### 编程中的安全

以下是 CNC 程序员应为 CNC 加工中心考虑的一些最常见安全规则（也可适用于大多数 CNC 车床）：

- 在所有工作中都带着安全意识进行程序开发
- 编程时先在 XY 轴方向接近零件，然后再移动 Z 轴
- 编程时先在 Z 轴方向从零件退刀，然后再移动 XY 轴
- 每个程序都以取消指令开始（所谓的状态程序段或安全程序段）
- 提供足够的间隙（零件上方、零件下方、引入和引出等）
- 编程合理的速度、进给、切削深度、切削宽度等
- 选择安全的换刀或换件位置
- 为工作选择合适的刀具
- 编程刀具运动朝向坚固支撑，例如台虎钳的固定钳口
- 从一个工作到另一个工作时保持编程方法一致
- 如果程序失败，应纠正问题的真正原因，而不是主观认为的原因

### 加工中的安全 - 通用

由于工作性质，CNC 操作员有更多与安全相关的问题需要考虑。以下是操作 CNC 机器的人员必须遵循的一些最常见安全规则：

- 穿戴经认可的安全靴
- 佩戴带侧面防护罩的经认可安全眼镜，并在需要时佩戴经认可的安全头盔
- 穿着合适的衣物（衬衫塞好、袖子扣好、不打领带）
- 将长发置于发网下或扎起
- 操作机器前取下手表、戒指、手镯及类似首饰
- 保持地面清洁，无油污或其他危险
- 不要拆除防护罩和保护装置
- 不要在运动或旋转物体周围使用抹布或手套
- 不要在机器顶部放置物品
- 以安全方式安装每个零件

