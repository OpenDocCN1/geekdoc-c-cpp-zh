
```
LabelJoint(White,xQ,xP,YP,YP',P');
LabelJoint(White,xP,yQ,yQ,Q');
END;
Inc(i);
until (NOT MecOut) AND IsKeyPressed(27);
CloseMMecGraph(FALSE);
END.

program P99_22;
// 模拟一个具有任意数量叶片的机构（第二种变体）
uses Graph, (Red,White);
Libinout, (KeyPressed);
LibMath, ()
LibDXF,(IniDXFfile);
LibInc,(GCrank);
LibAsnur,(RR,T);
MecGraph=(OpenMecGraph NewFrame,Shape,Point,CloseMecDXF)
const DXFile = 'F92.DXF'; (DXF文件名)
vane = 3; (叶片数量)
po3 = 30;
var i,j; Clr; Word;
phi,xO,yO;
xA,yP,yP,xQ,yQ;
BEGIN
OA=6.0;
OP=5.25;
PQ=9.0;
```

21 xO=0.0;

22 yO=0.0;

23 IniDXF(DXFILE);

24 OpenMemGraph(xO,yO,xO-1.3*OA,yO+1.3*A);

25 i=0;

26 if (nvane <= 3) then BEGIN Green else Black;

27 repeat

28 if (i > npos) then BEGIN

29 i=0;

30 CloseMemDXF;

31 NewFrame(500);

32 END;

33 Phi1=pi+6/sin(2*pi/npos);

34 for j=1 to nvane do BEGIN

35 grank(Clr,xO,yO,Phi2-2*pi/nvane);

36 xA=xO+Phi1/4+2*pi/nvane;

37 yA=yO-Phi1/4+2*pi/nvane;

38 T(Clr,xO,yO,xA,yA,Red);

39 PQ(0,1,xA,yA);

40 Shape('VANE.XY',xO,yO,0.0,0.0,'A');

41 if (nvane <= 3) then BEGIN

42 PutGraphPoint(White,xO,yO,'O');

43 LabelJoint(White,xO,yO,xA,yA,'A');

44 LabelJoint(White,xP,yP,xQ,yQ,'Q');

45 END;

46 Inc(i);

47 until (NOT MecOut) AND IsKeyPressed(27);

48 CloseMemGraph(FALSE);

49 END.

# 572 附录 B：选定的源代码

```
program P9_23;
// 显示固定和移动中心的动画
uses CRT,Graph,
4 LibMath,LibGraph,
5 UnitX,
6 LibMath,{InitGr},
7 LibGraph,{WriteX},
8 UnitX,
9 LibDXF,{F923.DXF},
10 {EraseAll,pressed},
11 {GCrank},
12 {RRR},
13 LibAssur,
14 LibNout,
15 LibMech,
16 Libcom,
17 LibGeD;
18 {OpenMechanism,Comocus,Right,Shape,PutPoint};
19 const DXFILE='F923.DXF'; 输出文件名 F923.DXF 或 F923.DXF
20 {左/右机构}
21 {动画帧数}
22 npos=180;
23 var i,j:Test(带有移动中心的ASCII文件);
24 Loop:Integer; OK:Boolean;
25 phi:x,y,xA,YB,OA,BC,xIC,yIC:S:string;
26 BEGIN
27 x=0;y=60;yC=地面位置
28 CA=120;
29 EraseAll('*PCX');
30 EraseAll('*XY');
31 Assign(ICM,Rewrite(ICM));
32 In(Gr); // 设置上述内容的背景
33 if (LR = Left) then S=s;else (LR = Right) then S=s;
34 SetTitle('bar'+S+' - 质心');
35 SetSize(3);
36 i=0; Loop=0;
37 Repeat
38 if (i > npos+1) then BEGIN
39 i=1;
40 Inc(Loop);
41 if (Loop = 2) then BEGIN
42 END;
43 SetTitle('按 <ESC> 退出..');
44 0;
45 Newframe();
46 Phi=pi/npos*i;
47 if (MOD < 5) then SuspendDXF;
48 gcrank(Red,xa,yo,Phi,OA,ya,_);
49 RRR(Rax,xa,ya,_,xYC,yC,_,0.0,AB,BC,LR,xYB,_);
50 IntLS(inc,ya, xYB,xA, yIC,yIC);
51 OK then BEGIN
52 RT2D(xIC,yIC-yA),0.0,xIC,yIC);
53 if (Loop = 0) then (更新形状文件..);
54 Append(IM)(xIC,yIC,yIC);
55 Close(IM);
56 END;
57 END;
58 S;
59 Shape('IC',Green,xa,yB);
60 Comocus(LightBlue,xIC,yIC);
61 Pointroid(Blue,'o',xIC,yIC);
62 if (Loop < 3) AND D_X then WritePCX('ImplicitFileName(PCX'),);
63 Inc(i);
64 until IsKeyPressed(27);
65 CloseMeGraph(TRUE);
66 END.
```

# 574 附录 B：选定的源代码

```
program P9_27;
2 // 在区间 [X.min, X.max] [Y.min, Y.max] 内生成 D2 文件以绘制隐函数
3 use CRT; (Clr);
4 LibMath; (Nmax,Vfd)
5 const File_Name = 'F927A.D2' or 'F927B.D2';
6 var_of: double; vx, vy:Vdn;
7 n nx, iy:integer; X, Y, Xmin, Xmax, Ymin, Ymax:double;
8 function Fx(X:double):double;
9 BEGIN
10 if Pos('A', FileName) > 0
11 Fx=Y*Y-X-10*x+1;
12 {with F927A.D2}
13 if Pos('B', FileName) > 0
14 Fx=X*Cos(X-Y)-1;
15 {with F927B.D2}
16 END;
17;
18 function Fx(X:double):double; BEGIN Fx=Fxy(X, Y);
19 function Fy(Y:double):double; BEGIN Fy=Fxy(X, Y); END;
20 nx:01; Xmin=-7.5; Xmax=7.5;
21 ny:01; Ymin=-7.5; Ymax=7.5;
22 Assign(FD, FileName); Rewrite(FD);
23 for ix=1 to nx do
24 X=Xmin+(Xmax-Xmin)*(ix-1);
25 ZeroGrid(FD); Ymin, Ymax, NX;
26 Nmax=0;
27 for iy=1 to ny do
28 Y=Ymin+(Ymax-Ymin)*(iy-1);
29 if (Loop < 3) then (更新形状文件..);
30 location of ground
31 CA=120;
32 EraseAll('*PCX');
33 EraseAll('*XY');
34 Assign(ICM,Rewrite(ICM));
35 In(Gr); // 设置上述内容的背景
36 if (LR = Left) then S=s;else (LR = Right) then S=s;
37 SetTitle('bar'+S+' - 质心');
38 SetSize(3);
39 i=0; Loop=0;
40 Repeat
41 if (i > npos+1) then BEGIN
42 i=1;
43 Inc(Loop);
44 if (Loop = 2) then BEGIN
45 END;
46 SetTitle('按 <ESC> 退出..');
47 0;
48 Newframe();
49 Phi=pi/npos*i;
50 if (MOD < 5) then SuspendDXF;
51 gcrank(Red,xa,yo,Phi,OA,ya,_);
52 RRR(Rax,xa,ya,_,xYC,yC,_,0.0,AB,BC,LR,xYB,_);
53 IntLS(inc,ya, xYB,xA, yIC,yIC);
54 OK then BEGIN
55 RT2D(xIC,yIC-yA),0.0,xIC,yIC);
56 if (Loop = 0) then (更新形状文件..);
57 Append(IM)(xIC,yIC,yIC);
58 Close(IM);
59 END;
60 END;
61 S;
62 Shape('IC',Green,xa,yB);
63 Comocus(LightBlue,xIC,yIC);
64 Pointroid(Blue,'o',xIC,yIC);
65 if (Loop < 3) AND D_X then WritePCX('ImplicitFileName(PCX'),);
66 Inc(i);
67 until IsKeyPressed(27);
68 CloseMeGraph(TRUE);
69 END.
```

# 附录 B: 选源代码

```pascal
OutJointAngle = 'F9_31.DTA';
OutXF = 'F9_31.STRF';
FTI.Fto.text: Word;
var FTI.Str: AuxString;
Axd, BC, xA1, xA2, xB1, yB1, yB2,
ThaB1, ThaB2, t, vc: double;
xCC, yC, xCp, yCp;
Label Abort
function W(double):string; {MyStr(..) 的简写}
BEGIN
var MyStr(D(10));
END;
BEGIN
Assign(FTI, InPathXY); {.输入路径文件}
Assign(FTI, OutJointAngle); {.输出关节角文件}
InitDllFile(OutDXF); {.输出 DXF 文件}
[in] 点 C 的速度
[in] 地关节 A1 坐标
[in] 地关节 A2 坐标
A1 = 2.25; yA1=-8.0;
A2 = 6.75; yA2=-8.0;
BC = 10.0;
[in] 杆 AB 的长度
[in] 杆 BC 的长度
Rewrite(FTI);
WriteLn(FTI,W(AB),(W(BC)));
WriteLn(FTI,W(xA1),(yA1));
WriteLn(FTI,W(xA2),(yA2));
WriteLn(FTI,W(VC));
theta: double;
FTI.Pto;
OpenMemGraph(-6.15, -12.7),'5R 人的逆运动学');
Repeat
Reset(FTI);
ThaB2=0.0; ThaB1=0.0;
cXC=IFD; ycC=IFD;
t=0.0;
i:=;
repeat
NewFrame(0)
if (i MOD 4 < 0) then SuspendDXF;
PutResumeDXF(3,3,'x', 'y');
xC:=xC;yC:=y;
Readln(Pri;xC,yC);
if (xC < Inf) then t:=t+Dist2F2s(xC,yC,xC,yC);
RBR(Red(YA2,0.0,0.0,xC,yC,AB_BC,+1,xB1,yB1);
RBB(Blue(YA2,0.0,0.0,xC,yC,AB_BC,+1,xB2,yB2);
AGPVA(YA1,0.0,0.0,xC,yC,Thal,+1,xB1,yB1);
AGPVA(YA2,0.0,0.0,xC,yC,Thal,+1,xB2,yB2);
xC,yC,_TB1;
AGPVA(YA2,0.0,0.0,xC,yC,_xB2_);
AGPVA(YA2,0.0,0.0,xC,yC,_xB2_);
xC,yC,_TB2;
Putang(White,2*xC-xA1,yC-yA1,xB1,yB1,6,'<#2333 A1);
Putang(White,2*xC-xA2,yC-yA2,xB2,yB2,6,'<#2333 A2);
Putang(White,2*xC-xA1,yC-yA1,xB2,yB2,6,'<#2333 B1);
PutPoint(White,xA1,yA1,B1);
PutPoint(White,xA2,yA2,B2);
PutPoint(White,xC,yC,B1);
PutPoint(White,xC,yC,B2);
PutPoint(White,0.5*(xA1+xA2),0.5*(yA1+y2));
ResumeDXF;
if i then Writeln(W(t),'W(Th1*DEG)');
'W(Th2*DEG),'W(Th2*DEG));
if IsKeyPressed(27) then GotoAbort;
Inc(i);
until EOF(FTI);
CloseMeDXF;
until FALSE;
Abort;
Close(FTI);
Close(FTI);
CloseMech(FALSE);
```

```cpp
PutGPoint(White, 'xB', 'yB', 'B');
LabelJoint(White, 0.5 * (xA+xB), 0.5 * (yA+yB), 'C');
if (A0 > 0) then LabelJoint(White, xC, xA0, yA0, 'A');
if (B0 > 0) then LabelJoint(White, xC, xB, yB0, 'B');
PutVector(LightBlue, White, xC, xB, vxC, 3, vC);
ResumeEF;
Locus (Cyan, xC, 'C');
if Mecout then
if isKeyPressed(27) then Goto Abort;
WriteLn(FTO, ' ', (ws1), ' ', (wds2));
Inc(1);
until EOP(FTO);
CloseMeCDFX;
Abort;
Close(FTO);
until FALSE;
CloseMeGraph(FALSE);
END;
```

1 程序 P9, 35;

3 = 带有齿轮和耙形状的 RTRTR 机器人正运动学

5 使用 Graph，{蓝, 青, , 红, 品红};

6 LibGe2D, {SI23};

7 LibMath, {DRG};

8 LibInOut, {IsKeyPressed};

9 LibDXF, {InitDXFile};

10 LibMeIn,

11 RRTFR;

12 LibAAsur,

13 LibMe2CD, {OpenGraph, NewFrame, SetJointSize, {AngPawa, 3PVA, CloseMeCDFX, Mecout})

```cpp
14 const InLabCol = White;
15 f99_34.DATA; {..输入 t,s1,ds1,s2,ds2 文件}
16 f99_35.DATA; {..输出 t,Theta1,Theta2,Theta1/dt,Theta2/dt}
17 OutDXF = {..输出 DXF (齿轮)}
18 Out = :integer;
19 rp = 1.57847; (节圆圆输出)
20 var FTI_FTOtext:
21 AuxStr:string;
22 t,xA0,A0,xB,yB,xA0,yA,0,xB,yB,0
23 xC,xC,yC,ds1,ds2,Phil,phi2
24 dheta1,Theta,Fcap,dheta1,dheta2:double;
25 function W(double):string; (MyStr() 的简写)
26 WN=MyStr(D,10);
27 END;
28 label Abort
29 BEGIN
30 Assign(FTI,InData);
31 Assign(FTO,OutData);
32 InidxFFTO.ile(OutDXF)
33 BEGIN
34 Rewrite(FTO);
35 WriteLn(FTO, t,Theta1, Theta2, dheta1/dt, dheta2/dt);
36 OpenGraph(-4,13,-18,7);
37 Setitle('RTRXR 齿轮机器人的正运动学');
38 SetSizeOffset(-2)
39 repeat
40 Reset(FTI);
41 ReadLn(FTI,AuxStr); ReadLn(FTI,AuxStr);
42 ReadLn(FTI,xA,yA,yB,A0,B0);
43 ReadLn(FTI,AuxStr);
44 phi:=0.0; phi2:=0.0;
45 Theta1:=Infd;
46 Theta2:=Infd;
47 dheta2:=Infd;
```
