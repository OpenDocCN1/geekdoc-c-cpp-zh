![](Images/cover07406.jpeg)

# A B C

# of

# Ada

# Programming

# Compiled by,

#  Aspen Blake

# Contents

###### 1 [Basic  Ada](#part0005.xhtml__bookmark1)3

[1.1"Hello,  world!"programs](#part0005.xhtml__bookmark2). . . . . . . . . . . . . . . . . . . . . . . . . . . .               3

1.2 [Compiling  the  "Hello,  world!"program](#part0007.xhtml__bookmark7). . . . . . . . . . . . . . . . . . . .               5

[1.3Things  to  look  out  for](#part0008.xhtml__bookmark11) .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .6

[1.4Where  to  ask  for  help](#part0010.xhtml__bookmark13). . . . . . . . . . . . . . . . . . . . . . . . . . . . .               8

[1.5Notes](#part0010.xhtml__bookmark14) . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .               8

###### 2 [Installing](#part0011.xhtml__bookmark21)9

[2.1AdaMagic  from  SofCheck](#part0011.xhtml__bookmark22).  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .               9

2.2 [AdaMULTI  from  Green  Hills  Software](#part0011.xhtml__bookmark23) . . . . . . . . . . . . . . . . . . . .               9

2.3 [DEC  Ada  from  HP](#part0012.xhtml__bookmark30)             10

2.4 [GNAT,  the  GNU  Ada  Compiler  from  AdaCore  and  the  Free  Software](#part0012.xhtml__bookmark31)  [Foundation](#part0012.xhtml__bookmark31)               10

2.5 [ICC  from  Irvine  Compiler  Corporation](#part0027.xhtml__bookmark99)             25

2.6 [Janus/Ada  83  and  95  from  RR  Software](#part0027.xhtml__bookmark100)             25

2.7 [MAXAda from Concurrent](#part0027.xhtml__bookmark101)             25

2.8 [ObjectAda  from  Atego  (formerly  Aonix)](#part0028.xhtml__bookmark107)             26

2.9 [PowerAda from OC  Systems](#part0028.xhtml__bookmark108)             26

26section.2.10

2.11 [SCORE  from  DDC-I](#part0029.xhtml__bookmark122)             27

2.12 [XD  Ada  from  SWEP-EDS](#part0029.xhtml__bookmark123)             27

2.13 [XGC  Ada  from  XGC  Software](#part0029.xhtml__bookmark124)             27

2.14 [References](#part0030.xhtml__bookmark127)             28

###### 3 [Building](#part0031.xhtml__bookmark128)29

3.1 [Building  with  various  compilers](#part0031.xhtml__bookmark129)             29

3.2 [Compiling  our  Demo  Source](#part0035.xhtml__bookmark146)             33

3.3 [External  links](#part0038.xhtml__bookmark156)             36

###### 4 [Control  Statements](#part0039.xhtml__bookmark161)37

4.1 [Conditionals](#part0039.xhtml__bookmark162)             37

4.2 [Unconditionals](#part0041.xhtml__bookmark173)             39

4.3 [Loops](#part0043.xhtml__bookmark175)             41

4.4 [See  also](#part0046.xhtml__bookmark178)             44

###### 5 [Type  System](#part0047.xhtml__bookmark180)45

5.1 [Predefined  types](#part0047.xhtml__bookmark181)             45

5.2 [The  Type  Hierarchy](#part0049.xhtml__bookmark190)             47

5.3 [Concurrency Types](#part0052.xhtml__bookmark209)             50

5.4 [Limited  Types](#part0052.xhtml__bookmark210)             50

5.5 [Defining  new  types  and  subtypes](#part0052.xhtml__bookmark211)             51

5.6 [Subtype  categories](#part0056.xhtml__bookmark214)             54

5.7 [Qualified  expressions](#part0059.xhtml__bookmark223)             57

5.8 [Type  conversions](#part0059.xhtml__bookmark224)             58

5.9 [Elaborated  Discussion  of  Types  for  Signed  Integer  Types](#part0067.xhtml__bookmark231)             65

5.10 [Relations  between  types](#part0069.xhtml__bookmark232)             67

5.11 [See  also](#part0069.xhtml__bookmark233)             67

| [6](#part0071.xhtml__bookmark237) | [Integer  types](#part0071.xhtml__bookmark237) | 69 |
|  | [6.1Working  demo](#part0071.xhtml__bookmark238) .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  . | 69 |
|  | [6.2See  also](#part0072.xhtml__bookmark240)   .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  . | 70 |
| [7](#part0073.xhtml__bookmark245) | [Unsigned  integer  types](#part0073.xhtml__bookmark245) | 71 |
|  | [7.1Description](#part0073.xhtml__bookmark246)   . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . | 71 |
|  | [7.2See  also](#part0073.xhtml__bookmark247)   .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  . | 72 |
| [8](#part0075.xhtml__bookmark251) | [Enumerations](#part0075.xhtml__bookmark251) | 73 |
|  | [8.1Operators  and  attributes](#part0075.xhtml__bookmark252)  .  . . . . . . . . . . . . . . . . . . . . . . . . . . . | 73 |
|  | [8.2Enumeration  literals](#part0075.xhtml__bookmark253)   .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  . | 74 |
|  | [8.3Enumeration  subtypes](#part0077.xhtml__bookmark259)  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  . | 75 |
|  | [8.4See  also](#part0077.xhtml__bookmark260)   .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  . | 76 |
| [9](#part0079.xhtml__bookmark266) | [Floating  point  types](#part0079.xhtml__bookmark266) | 77 |
|  | [9.1Description](#part0079.xhtml__bookmark267)   . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . | 77 |
|  | [9.2See  also](#part0079.xhtml__bookmark268)   .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  . | 77 |
| [10](#part0081.xhtml__bookmark278) | [Fixed  point  types](#part0081.xhtml__bookmark278) | 79 |
|  | [10.1Description](#part0081.xhtml__bookmark279)   . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . | 79 |
|  | [10.2Ordinary  Fixed  Point](#part0081.xhtml__bookmark280) .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  . | 79 |
|  | [10.3Decimal  Fixed  Point](#part0082.xhtml__bookmark282)  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  . | 80 |
|  | [10.4Differences  between  Ordinary  and  Decimal  Fixed  Point  Types](#part0082.xhtml__bookmark283)  .  .  .  .  .  .  . | 80 |
|  | [10.5See  also](#part0084.xhtml__bookmark284)   .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  . | 82 |
| [11](#part0085.xhtml__bookmark293) | [Arrays](#part0085.xhtml__bookmark293) | 83 |
|  | [11.1Declaring  arrays](#part0085.xhtml__bookmark294).  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  . | 83 |
|  | [11.2Using  arrays](#part0088.xhtml__bookmark309)  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  . | 87 |
|  | [11.3See  also](#part0090.xhtml__bookmark311)   .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  . | 88 |
| [12](#part0093.xhtml__bookmark318) | [Records](#part0093.xhtml__bookmark318) | 91 |
| [12.1](#part0093.xhtml__bookmark319) | [Basic  record](#part0093.xhtml__bookmark319) | .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  . | 91 |
| [12.2](#part0093.xhtml__bookmark320) | [Null  record](#part0093.xhtml__bookmark320) | .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  . | 91 |
|  |  |  |  |  |

12.3 [Record  Values](#part0093.xhtml__bookmark321)             91

12.4 [Discriminated  record](#part0095.xhtml__bookmark324)             93

12.5 [Variant  record](#part0095.xhtml__bookmark325)             93

12.6 [Union](#part0097.xhtml__bookmark326)             95

12.7 [Tagged  record](#part0097.xhtml__bookmark327)             95

12.8 [Abstract  tagged  record](#part0098.xhtml__bookmark331)             96

12.9 [With  aliased  elements](#part0098.xhtml__bookmark332)             96

12.10 [Limited  Records](#part0099.xhtml__bookmark335)             97

12.11 [See  also](#part0099.xhtml__bookmark336)             97

13 [Access  types](#part0101.xhtml__bookmark346)99

13.1 [What's  an  Access  Type?](#part0101.xhtml__bookmark347)             99

13.2 [Pool  access](#part0101.xhtml__bookmark348)             99

13.3 [General  access](#part0104.xhtml__bookmark350)             102

13.4 [Anonymous  access](#part0105.xhtml__bookmark354)             103

13.5 [Implicit  Dereference](#part0106.xhtml__bookmark355)             104

13.6 [Null  exclusions](#part0107.xhtml__bookmark356)             105

13.7 [Access  to  Subprogram](#part0108.xhtml__bookmark357)             106

13.8 [Access  FAQ](#part0108.xhtml__bookmark358)             106

13.9 [Thin  and  Fat  Access  Types](#part0111.xhtml__bookmark361)             109

13.10 [See  also](#part0112.xhtml__bookmark362)             110

14 [Limited  types](#part0115.xhtml__bookmark366)113

14.1 [Limited  Types](#part0115.xhtml__bookmark367)             113

14.2 [Initialising  Limited  Types](#part0117.xhtml__bookmark369)             115

14.3 [See  also](#part0118.xhtml__bookmark370)             116

14.4 [References](#part0119.xhtml__bookmark372)             117

15 [Strings](#part0121.xhtml__bookmark373)119

15.1 [Fixed-length  string  handling](#part0121.xhtml__bookmark374)             119

15.2 [Bounded-length  string  handling](#part0122.xhtml__bookmark377)             120

15.3 [Unbounded-length  string  handling](#part0124.xhtml__bookmark378)             122

15.4 [See  also](#part0124.xhtml__bookmark379)             123

16 [Subprograms](#part0127.xhtml__bookmark381)125

16.1 [Procedures](#part0128.xhtml__bookmark384)             126

16.2 [Functions](#part0129.xhtml__bookmark385)             127

16.3 [Named  parameters](#part0131.xhtml__bookmark386)             129

16.4 [Default  parameters](#part0131.xhtml__bookmark387)             129

16.5 [Renaming](#part0132.xhtml__bookmark388)             130

16.6 [See  also](#part0133.xhtml__bookmark389)             131

17 [Packages](#part0135.xhtml__bookmark393)133

17.1 [Separate  compilation](#part0135.xhtml__bookmark394)             133

17.2 [Parts  of  a  package](#part0136.xhtml__bookmark395)             134

17.3 [Using  packages](#part0139.xhtml__bookmark404)             137

17.4 [Package  organisation](#part0143.xhtml__bookmark408)             141

17.5 [Notes](#part0147.xhtml__bookmark410)             145

17.6 [See  also](#part0147.xhtml__bookmark411)             145

18 [Input  Output](#part0149.xhtml__bookmark416)147

18.1 [Overview](#part0149.xhtml__bookmark417)             147

18.2 [Text  I/O](#part0150.xhtml__bookmark418)             148

18.3 [Direct  I/O](#part0150.xhtml__bookmark419)             148

18.4 [Sequential  I/O](#part0151.xhtml__bookmark423)             149

18.5 [Stream  I/O](#part0151.xhtml__bookmark424)             149

18.6 [See  also](#part0151.xhtml__bookmark425)             150

19 [Exceptions](#part0155.xhtml__bookmark478)153

19.1 [Robustness](#part0155.xhtml__bookmark479)             153

19.2 [Modules,  preconditions  and  postconditions](#part0155.xhtml__bookmark480)             153

19.3 [Predefined  exceptions](#part0156.xhtml__bookmark481)             154

19.4 [Input-output  exceptions](#part0157.xhtml__bookmark482)             156

19.5 [Exception  declarations](#part0158.xhtml__bookmark483)             156

19.6 [Raising  exceptions](#part0159.xhtml__bookmark484)             157

19.7 [Exception  handling  and  propagation](#part0159.xhtml__bookmark485)             157

19.8 [Information  about  an  exception  occurrence](#part0160.xhtml__bookmark486)             158

19.9 [See  also](#part0161.xhtml__bookmark487)             159

20 [Generics](#part0163.xhtml__bookmark489)161

20.1 [Parametric  polymorphism  (generic  units)](#part0163.xhtml__bookmark490)             161

20.2 [Generic  parameters](#part0164.xhtml__bookmark491)             162

20.3 [Instantiating  generics](#part0170.xhtml__bookmark492)             168

20.4 [Advanced  generics](#part0170.xhtml__bookmark493)             168

20.5 [See  also](#part0174.xhtml__bookmark494)             172

21 [Tasking](#part0175.xhtml__bookmark499)173

21.1 [Tasks](#part0175.xhtml__bookmark500)             173

21.2 [Protected  types](#part0179.xhtml__bookmark503)             177

21.3 [Entry  families](#part0181.xhtml__bookmark504)             180

21.4 [Termination](#part0182.xhtml__bookmark505)             180

21.5 [Timeout](#part0183.xhtml__bookmark507)             181

21.6 [Conditional  entry  calls](#part0185.xhtml__bookmark508)             183

21.7 [Requeue  statements](#part0185.xhtml__bookmark509)             183

21.8 [Scheduling](#part0185.xhtml__bookmark510)             184

21.9 [Interfaces](#part0186.xhtml__bookmark511)             184

21.10 [See  also](#part0186.xhtml__bookmark512)             184

21.11 [Ada  Quality  and  Style  Guide](#part0187.xhtml__bookmark516)             185

22 [Object  Orientation](#part0189.xhtml__bookmark519)187

22.1 [Object  orientation  in  Ada](#part0189.xhtml__bookmark520)             187

22.2 [Class  names](#part0207.xhtml__bookmark527)             206

22.3 [Object-Oriented  Ada  for  C++  programmers](#part0209.xhtml__bookmark530)             207

22.4 [See  also](#part0219.xhtml__bookmark532)             217

23 [New  in  Ada  2005](#part0221.xhtml__bookmark541)219

23.1 [Language  features](#part0221.xhtml__bookmark542)             219

23.2 [Language  library](#part0224.xhtml__bookmark560)             222

23.3 [Real-Time  and  High  Integrity  Systems](#part0225.xhtml__bookmark564)             223

23.4 [Summary  of  what's  new](#part0226.xhtml__bookmark566)             224

23.5 [See  also](#part0229.xhtml__bookmark567)             227

23.6 [External  links](#part0229.xhtml__bookmark568)             228

24 [Containers](#part0233.xhtml__bookmark596)231

24.1 [See  also](#part0242.xhtml__bookmark597)             240

25 [Interfacing](#part0245.xhtml__bookmark600)243

25.1 [Interfacing](#part0245.xhtml__bookmark601)             243

25.2 [Other  programming  languages](#part0245.xhtml__bookmark602)             243

25.3 [Hardware  devices](#part0245.xhtml__bookmark603)             243

25.4 [See  also](#part0246.xhtml__bookmark614)             244

26 [Coding  Standards](#part0247.xhtml__bookmark617)245

26.1 [Introduction](#part0247.xhtml__bookmark618)             245

26.2 [Tools](#part0247.xhtml__bookmark619)             245

26.3 [Coding  guidelines](#part0247.xhtml__bookmark620)             246

26.4 [See  also](#part0248.xhtml__bookmark632)             246

26.5 [External  links](#part0249.xhtml__bookmark642)             247

27 [Tips](#part0251.xhtml__bookmark645)249

27.1 [Full  declaration  of  a  type  can  be  deferred  to  the  unit's  body](#part0251.xhtml__bookmark646)             249

27.2 [Lambda  calculus  through  generics](#part0252.xhtml__bookmark651)             250

27.3 [Compiler  Messages](#part0252.xhtml__bookmark652)             250

27.4 [Universal  integers](#part0253.xhtml__bookmark657)             251

[27.5I/O](#part0254.xhtml__bookmark658)             253

27.6 [Quirks](#part0255.xhtml__bookmark660)             253

27.7 [References](#part0256.xhtml__bookmark663)             254

27.8 [See  also](#part0256.xhtml__bookmark664)             254

28 [Common  Errors](#part0257.xhtml__bookmark667)255

28.1 [pragma  Atomic  &  Volatile](#part0257.xhtml__bookmark668)             255

28.2 [References](#part0258.xhtml__bookmark675)             256

28.3 [pragma  Pack](#part0258.xhtml__bookmark676)             256

28.4 ['Bit_Order  attribute](#part0259.xhtml__bookmark685)             257

28.5 ['Size  attribute](#part0259.xhtml__bookmark686)             257

28.6 [See  also](#part0259.xhtml__bookmark687)             258

28.7 [References](#part0260.xhtml__bookmark696)             258

29 [Algorithms](#part0261.xhtml__bookmark699)259

29.1 [Introduction](#part0261.xhtml__bookmark700)             259

29.2 [Chapter  1:  Introduction](#part0261.xhtml__bookmark701)             259

29.3 [Chapter  6:  Dynamic  Programming](#part0262.xhtml__bookmark706)             261

30 [Function  overloading](#part0269.xhtml__bookmark710)267

30.1 [Function  overloading  in  Ada](#part0269.xhtml__bookmark711)             267

30.2 [See  also](#part0270.xhtml__bookmark712)             268

31 [Mathematical  calculations](#part0271.xhtml__bookmark715)269

31.1 [Simple  calculations](#part0271.xhtml__bookmark716)             269

31.2 [Exponential  calculations](#part0274.xhtml__bookmark720)             272

31.3 [Higher  math](#part0277.xhtml__bookmark722)             275

31.4 [See  also](#part0282.xhtml__bookmark725)             280

32 [Statements](#part0285.xhtml__bookmark732)283

33 [Variables](#part0287.xhtml__bookmark733)285

33.1 [Assignment  statements](#part0287.xhtml__bookmark734)             285

33.2 [Uses](#part0287.xhtml__bookmark735)             285

33.3 [See  also](#part0287.xhtml__bookmark736)             286

34 [Lexical  elements](#part0289.xhtml__bookmark740)287

34.1 [Character  set](#part0289.xhtml__bookmark741)             287

34.2 [Lexical  elements](#part0289.xhtml__bookmark742)             287

34.3 [See  also](#part0292.xhtml__bookmark755)             291

35 [Keywords](#part0295.xhtml__bookmark761)293

35.1 [Language  summary  keywords](#part0295.xhtml__bookmark762)             293

35.2 [List  of  keywords](#part0295.xhtml__bookmark763)             293

35.3 [See  also](#part0296.xhtml__bookmark766)             294

36 [Delimiters](#part0299.xhtml__bookmark777)297

36.1 [Single  character  delimiters](#part0299.xhtml__bookmark778)             297

36.2 [Compound  character  delimiters](#part0300.xhtml__bookmark796)             298

36.3 [Others](#part0301.xhtml__bookmark813)             299

36.4 [See  also](#part0301.xhtml__bookmark814)             299

37 [Operators](#part0303.xhtml__bookmark820)301

37.1 [Standard  operators](#part0303.xhtml__bookmark821)             301

37.2 [Short-circuit  control  forms](#part0305.xhtml__bookmark858)             303

37.3 [Membership  tests](#part0305.xhtml__bookmark859)             303

37.4 [See  also](#part0306.xhtml__bookmark876)             304

38 [Attributes](#part0307.xhtml__bookmark878)305

38.1 [Language  summary  attributes](#part0307.xhtml__bookmark879)             305

38.2 [List  of  language  defined  attributes](#part0307.xhtml__bookmark880)             305

38.3 [List  of  implementation  defined  attributes](#part0312.xhtml__bookmark975)             310

38.4 [See  also](#part0316.xhtml__bookmark1063)             314

38.5 [References](#part0317.xhtml__bookmark1082)             315

39 [Pragmas](#part0319.xhtml__bookmark1089)317

39.1 [Description](#part0319.xhtml__bookmark1090)             317

39.2 [List  of  language  defined  pragmas](#part0319.xhtml__bookmark1091)             317

39.3 [List  of  implementation  defined  pragmas](#part0322.xhtml__bookmark1149)             320

39.4 [See  also](#part0330.xhtml__bookmark1337)             328

39.5 [References](#part0331.xhtml__bookmark1354)             329

40 [Libraries](#part0333.xhtml__bookmark1359)331

40.1 [Predefined  Language  Libraries](#part0333.xhtml__bookmark1360)             331

40.2 [Other  Language  Libraries](#part0333.xhtml__bookmark1361)             331

40.3 [See  also](#part0333.xhtml__bookmark1362)             332

41 [Libraries:  Standard](#part0335.xhtml__bookmark1379)333

41.1 [Implementation](#part0335.xhtml__bookmark1380)             333

41.2 [Portability](#part0335.xhtml__bookmark1381)             333

41.3 [See  also](#part0336.xhtml__bookmark1392)             334

42 [Libraries:  Ada](#part0339.xhtml__bookmark1395)337

42.1 [List  of  language  defined  child  units](#part0339.xhtml__bookmark1396)             337

42.2 [List  of  implementation  defined  child  units](#part0346.xhtml__bookmark1534)             344

42.3 [See  also](#part0349.xhtml__bookmark1583)             347

43 [Libraries:  Interfaces](#part0351.xhtml__bookmark1593)349

43.1 [Child  Packages](#part0351.xhtml__bookmark1594)             349

43.2 [See  also](#part0352.xhtml__bookmark1613)             350

44 [Libraries:  System](#part0353.xhtml__bookmark1621)351

45 [Libraries:  GNAT](#part0355.xhtml__bookmark1622)353

45.1 [Child  packages](#part0355.xhtml__bookmark1623)             353

45.2 [See  also](#part0358.xhtml__bookmark1690)             356

46 [Libraries:  Multi-Purpose](#part0359.xhtml__bookmark1696)357

46.1 [See  also](#part0359.xhtml__bookmark1697)             357

47 [Libraries:  Container](#part0361.xhtml__bookmark1704)359

47.1 [See  also](#part0361.xhtml__bookmark1705)             359

48 [Libraries:  GUI](#part0363.xhtml__bookmark1717)361

48.1 [See  also](#part0363.xhtml__bookmark1718)             361

49 [Libraries:  Distributed  Systems](#part0365.xhtml__bookmark1734)363

49.1 [See  also](#part0365.xhtml__bookmark1735)             363

50 [Libraries:  Databases](#part0367.xhtml__bookmark1744)365

51 [Libraries:  Web](#part0373.xhtml__bookmark1745)371

51.1 [See  also](#part0373.xhtml__bookmark1746)             371

52 [Libraries:  Input  Output](#part0375.xhtml__bookmark1753)373

52.1 [See  also](#part0375.xhtml__bookmark1754)             373

53 [Platform  Support](#part0377.xhtml__bookmark1761)375

53.1 [See  also](#part0377.xhtml__bookmark1762)             375

54 [Platform:  Linux](#part0379.xhtml__bookmark1770)377

54.1 [See  also](#part0379.xhtml__bookmark1771)             377

55 [Platform:  Windows](#part0381.xhtml__bookmark1781)379

55.1 [See  also](#part0381.xhtml__bookmark1782)             379

56 [Platform:  Virtual  Machines](#part0383.xhtml__bookmark1793)381

56.1 [See  also](#part0383.xhtml__bookmark1794)             381

57 [Portals](#part0385.xhtml__bookmark1799)383

57.1 [Forges  of  open-source  projects](#part0385.xhtml__bookmark1800)             383

![](Images/image06571.jpeg)Contents

57.2 [Directories  of  freely  available  tools  and  libraries](#part0385.xhtml__bookmark1801)             383

57.3 [Collections  of  Ada  source  code](#part0385.xhtml__bookmark1802)             384

57.4 [See  also](#part0386.xhtml__bookmark1812)             384

58 [Tutorials](#part0389.xhtml__bookmark1820)387

[59 Web  2.0](#part0391.xhtml__bookmark1832)389

# 1 Basic  Ada

## 1.1 "Hello, world!"  programs

#### 1.1.1  "Hello,  world!"

A common example of a language's syntax[1](#part0005.xhtml__bookmark3)   is the Hello world program[2](#part0005.xhtml__bookmark4).              Here  is  a  straightforward  Ada  Implementation:

![](Images/image06572.jpeg)

The with statement adds the package Ada.Text_IO to the program. This package comes  with every Ada compiler and contains all functionality needed for textual Input/Output.  The with statement makes the declarations of Ada.Text_IO available to procedure Hello.  This includes the types declared in Ada.Text_IO, the subprograms of Ada.Text_IO and  everything else that is declared in Ada.Text_IO for public use. In Ada, packages can be  used as toolboxes. Text_IO provides a collection of tools for textual input and output in  one  easy-to-access  module.  Here  is  a  partial  glimpse  at  package  Ada.Text_IO

![](Images/image06573.jpeg)![](Images/image06574.jpeg)

1 [http://en.wikipedia.org/wiki/Syntax_%28programming_languages%29](http://en.wikipedia.org/wiki/Syntax_%28programming_languages%29)

2 [http://en.wikipedia.org/wiki/Hello_world_program](http://en.wikipedia.org/wiki/Hello_world_program)

![](Images/image06575.jpeg)

Next in the program we declare a main procedure.  An Ada main procedure does not need  to be called "main".  Any simple name is fine so here it is Hello.  Compilers might allow  procedures  or  functions  to  be  used  as  main  subprograms.  [3](#part0006.xhtml__bookmark5)

The  call  on  Ada.Text_IO.Put_Line  writes  the  text  "Hello  World"  to  the  current  output  file.

A with clause makes the content of a package visible by selection:  we need to prefix the  procedure name Put_Line from the Text_IO package with its full package name Ada.Text_-  IO. If you need procedures from a package more often some form of shortcut is needed.  There  are  two  options  open:

#### 1.1.2  "Hello,  world!"  with  renames

By renaming a package it is possible to give a shorter alias to any package name.[4](#part0006.xhtml__bookmark6) This  reduces  the  typing  involved  while  still  keeping  some  of  the  readability.

![](Images/image06576.jpeg)

#### 1.1.3  "Hello,  world!"  with  use

The use clause makes all the content of a package directly visible. It allows even less typing  but removes some of the readability. One suggested "rule of thumb": use for the most used  package and renames for all other packages.  You might have another rule (for example,  always  use  Ada.Text_IO.  never  use  anything  else).

![](Images/image06577.jpeg)

3 Main  subprograms  may  even  have  parameters;  it  is  implementation-defined  what  kinds  of  subprograms  can be used as main subprograms.  The reference manual explains the details in 10.2 LRM 10.2(29)  ˆ{[http://www.adaic.org/resources/add_content/standards/05rm/html/RM-10-2.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-10-2.html)  :  “. . . ,  an  implementation is required to support all main subprograms that are public parameterless library  procedures.” Library means not nested in another subprogram, for example, and other things that  needn't  concern  us  now.

4 renames  can  also  be  used  for  procedures,  functions,  variables,  array  elements.  It  can  not  be  used  for  types  -  a  type  rename  can  be  accomplished  with  subtype.

![](Images/image06578.jpeg)

use  can  be  used  for  packages  and  in  the  form  of  use  type  for  types.  use  type  makes  only  the  operators[5](#part0007.xhtml__bookmark8)  of  the  given  type  directly  visible  but  not  any  other  operations  on  the  type.

## 1.2 Compiling  the  "Hello,  world!"  program

For information on how to build the "Hello, world!" program on various compilers, see the  Building[6](#part0007.xhtml__bookmark9)  chapter.

#### 1.2.1  FAQ:  Why  is  "Hello,  world!"  so  big?

Ada beginners frequently ask how it can be that such a simple program as "Hello, world!"  results  in  such  a  large  executable.  The  reason  has  nothing  to  do  with  Ada  but  can  usually  be  found  in  the  compiler  and  linker  options  used  —  or  better,  not  used.

Standard  behavior  for  Ada  compilers  —  or  good  compilers  in  general  —  is  not  to  create  the  best code possible but to be optimized for ease of use.  This is done to ensure a system that  works "out of the box" and thus does not frighten away potential new users with unneeded  complexity.

The GNAT project files, which you can  download[7](#part0007.xhtml__bookmark10) alongside the example programs, use  better tuned compiler, binder and linker options. If you use those your "Hello, world!" will  be  a  lot  smaller:

![](Images/image06579.jpeg)

![](Images/image06580.jpeg)

5 Chapter  [37](#part0303.xhtml__bookmark820)  on  page  [301](#part0303.xhtml__bookmark820)

6 Chapter  [3](#part0031.xhtml__bookmark128)  on  page  [29](#part0031.xhtml__bookmark128)

7 [https://sourceforge.net/project/showfiles.php?group_id=124904](https://sourceforge.net/project/showfiles.php?group_id=124904)

For  comparison  the  sizes  for  a  plain  gnat  make  compile:

![](Images/image06581.jpeg)

Worth  mentioning  is  that  hello_world  (Ada,C,C++)  compiled  with  GNAT/MSVC  7.1/GCC(C)  all  produces  executables  with  approximately  the  same  size  given  comparable  optimisation  and  linker  methods.

## 1.3 Things  to  look  out  for

It  will  help  to  be  prepared  to  spot  a  number  of  significant  features  of  Ada  that  are  important  for  learning  its  syntax  and  semantics.

#### 1.3.1  Comb  Format

There is a comb format in all the control structures and module structures. See the following  examples for the comb format. You don't have to understand what the examples do yet -  just  look  for  the  similarities  in  layout.

![](Images/image06582.jpeg)

![](Images/image06583.jpeg)

![](Images/image06584.jpeg)

![](Images/image06585.jpeg)

![](Images/image06586.jpeg)

![](Images/image06587.jpeg)

![](Images/image06588.jpeg)

![](Images/image06589.jpeg)

![](Images/image06590.jpeg)

![](Images/image06591.jpeg)

Note  that  semicolons  consistently  terminate  statements  and  declarations;  the  empty  line  (or  a  semicolon  alone)  is  not  a  valid  statement:  the  null  statement  is

![](Images/image06592.jpeg)

#### 1.3.2  Type  and  subtype

There is an important distinction between type and subtype:  a type is given by a set of  values  and  their  operations.  A  subtype  is  given  by  a  type,  and  a  constraint  that  limits  the  set of values. Values are always of a type. Objects (constants and variables) are of a subtype.  This generalizes, clarifies and systematizes a relationship, e.g. between Integer and 1..100,  that  is  handled  ad  hoc  in  the  semantics  of  Pascal[8](#part0009.xhtml__bookmark12).

#### 1.3.3  Constrained  types  and  unconstrained  types

There is an important distinction between constrained types and unconstrained types. An  unconstrained  type  has  one  or  more  free  parameters  that  affect  its  size  or  shape.  A  constrained  type  fixes  the  values  of  these  parameters  and  so  determines  its  size  and  shape.

![](Images/image06593.jpeg)

8 [http://en.wikipedia.org/wiki/Pascal%20programming%20language](http://en.wikipedia.org/wiki/Pascal%20programming%20language)

Loosely  speaking,  objects  must  be  of  a  constrained  type,  but  formal  parameters  may  be  of  an unconstrained type (they adopt the constraint of any corresponding actual parameter).  This  solves  the  problem  of  array  parameters  in  Pascal  (among  other  things).

#### 1.3.4  Dynamic  types

Where values in Pascal[9](#part0010.xhtml__bookmark15) or C[10](#part0010.xhtml__bookmark16) must be static (e.g. the subscript bounds of an array) they  may be dynamic in Ada.  However, static expressions are required in certain cases where  dynamic evaluation would not permit a reasonable implementation (e.g.  in setting the  number  of  digits  of  precision  of  a  floating  point  type).

#### 1.3.5  Separation  of  concerns

Ada consistently supports a separation of interface and mechanism.  You can see this in the  format  of  a  package[11](#part0010.xhtml__bookmark17),  which  separates  its  declaration  from  its  body;  and  in  the  concept  of  a  private  type,  whose  representation  in  terms  of  Ada  data  structures  is  inaccessible  outside  the  scope  containing  its  definition.

## 1.4 Where  to  ask  for  help

Most  Ada  experts  lurk  on  the  Usenet  newsgroups[12](#part0010.xhtml__bookmark18)  comp.lang.ada  (English)  and  fr.comp.lang.ada (French); they are accessible either with a newsreader[13](#part0010.xhtml__bookmark19) or through one of  the  many  web  interfaces.  This  is  the  place  for  all  questions  related  to  Ada.

People on these newsgroups are willing to help but will not do students' homework for them;  they will not post complete answers to assignments.  Instead, they will provide guidance for  students  to  find  their  own  answers.

For  more  online  resources,  see  the  External  links[14](#part0010.xhtml__bookmark20)  section  in  this  wikibook's  introduction.

## 1.5 Notes

![](Images/image06594.jpeg)

9 [http://en.wikipedia.org/wiki/Pascal%20programming%20language](http://en.wikipedia.org/wiki/Pascal%20programming%20language)

10 [http://en.wikipedia.org/wiki/C%20programming%20language](http://en.wikipedia.org/wiki/C%20programming%20language)

11 Chapter  [17](#part0135.xhtml__bookmark393)  on  page  [133](#part0135.xhtml__bookmark393)

12 [http://en.wikipedia.org/wiki/Newsgroup](http://en.wikipedia.org/wiki/Newsgroup)

13 [http://en.wikipedia.org/wiki/News_client](http://en.wikipedia.org/wiki/News_client)

14 [http://en.wikibooks.org/wiki/Ada%20Programming%23External%20links](http://en.wikibooks.org/wiki/Ada%20Programming%23External%20links)

# 2 Installing

Ada compilers[1](#part0011.xhtml__bookmark24)  are available  from several  vendors, on  a variety of  host and  target platforms.  The  Ada  Resource  Association[2](#part0011.xhtml__bookmark25)  maintains  a  list  of  available  compilers[3](#part0011.xhtml__bookmark26).

Below  is  an  alphabetical  list  of  available  compilers  with  additional  comments.

## 2.1 AdaMagic  from  SofCheck

SofCheck[4](#part0011.xhtml__bookmark27) produces  an  Ada  95  front-end  that  can  be  plugged  into  a  code  generating  back-end  to  produce  a  full  compiler.  This  front-end  is  offered  for  licensing  to  compiler  vendors.

Based  on  this  front-end,  SofCheck  offers:

• AdaMagic,  an  Ada-to-C  translator

• AppletMagic,  an  Ada-to-Java[5](#part0011.xhtml__bookmark28)  bytecode  compiler  Commercial;  proprietary.

## 2.2 AdaMULTI  from  Green  Hills  Software

Green  Hills  Software  sells  development  environments  for  multiple  languages  and  multiple  targets  (including  DSP[6](#part0011.xhtml__bookmark29)s),  primarily  to  embedded  software  developers.

| Languages  supported | Ada  83,  Ada  95,  C,  C++,  Fortran |
| License  for  the  run-timelibrary | proprietary |
| Native  platforms | GNU/Linux  on  i386,  Microsoft  Windows  on  i386,and Solaris  on SPARC |
| Cross  platforms | INTEGRITY, INTEGRITY-178B and velOSityfrom  Green  Hills;  VxWorks  from  Wind  River;  sev-  eral bare board targets. Safety-critical GMART  and  GSTART  run-time  libraries  certified  to  DO-  178B  level  A. |
| Available  from | [http://www.ghs.com/](http://www.ghs.com/) |

![](Images/image06595.jpeg)

1 [http://en.wikipedia.org/wiki/Compiler](http://en.wikipedia.org/wiki/Compiler)

2 [http://www.adaic.com](http://www.adaic.com/)

3 [http://www.adaic.com/compilers/comp-tool.html](http://www.adaic.com/compilers/comp-tool.html)

4 [http://www.sofcheck.com/](http://www.sofcheck.com/)

5 [http://en.wikibooks.org/wiki/Ada_Programming%2FPlatform%2FVM%2FJava](http://en.wikibooks.org/wiki/Ada_Programming%2FPlatform%2FVM%2FJava)

6 [http://en.wikipedia.org/wiki/Digital%20signal%20processor](http://en.wikipedia.org/wiki/Digital%20signal%20processor)

| Support | Commercial |
| Add-ons  included | IDE,  debugger,  TimeMachine,  integration  withvarious  version  control  systems,  source  browsers,  other  utilities |

GHS claims to make great efforts to ensure that their compilers produce the most efficient  code and often cites the  EEMBC[7](#part0012.xhtml__bookmark32) benchmark results as evidence, since many of the results  published by chip manufacturers use GHS compilers to show their silicon in the best light,  although  these  benchmarks  are  not  Ada  specific.

GHS has no publicly announced plans to support the new Ada standard published in 2007  but  they  do  continue  to  actively  market  and  develop  their  existing  Ada  products.

## 2.3 DEC  Ada  from  HP

DEC Ada is an Ada 83 compiler for OpenVMS[8](#part0012.xhtml__bookmark33). While “DEC Ada” is probably the name  most users know, the compiler is now called “ HP Ada[9](#part0012.xhtml__bookmark34)”. It had previously been known also  by  names  of  "VAX  Ada"  and  "Compaq  Ada".

• Ada  for  OpenVMS  Alpha  Installation  Guide[10](#part0012.xhtml__bookmark35)  (PDF)

• Ada  for  OpenVMS  VAX  Installation  Guide[11](#part0012.xhtml__bookmark36)  (PDF)

## 2.4 GNAT,  the  GNU  Ada  Compiler  from  AdaCore  and  the  Free  Software  Foundation

GNAT[12](#part0012.xhtml__bookmark37)  is  the  free  GNU  Ada  compiler,  which  is  part  of  the  GNU  Compiler  Collection[13](#part0012.xhtml__bookmark38).  It  is  the  only  Ada  compiler  that  supports  all  of  the  optional  annexes  of  the  language  standard. The original authors formed the company AdaCore[14](#part0012.xhtml__bookmark39) to offer professional support,  consulting, training and custom development services.  It is thus possible to obtain GNAT  from  many  different  sources,  detailed  below.

GNAT  is  always  licensed  under  the  terms  of  the  GNU  General  Public  License[15](#part0012.xhtml__bookmark40).

However,  the  run-time  library  uses  either  the  GPL[16](#part0012.xhtml__bookmark41),  or  the  GNAT  Modified  GPL[17](#part0012.xhtml__bookmark42),  depending  on  where  you  obtain  it.

![](Images/image06596.jpeg)

7 [http://www.eembc.com](http://www.eembc.com/)

8 [http://en.wikipedia.org/wiki/OpenVMS](http://en.wikipedia.org/wiki/OpenVMS)

9 [http://h71000.www7.hp.com/commercial/ada/ada_index.html](http://h71000.www7.hp.com/commercial/ada/ada_index.html)

10 [http://h71000.www7.hp.com/commercial/ada/ada_avms_ig.pdf](http://h71000.www7.hp.com/commercial/ada/ada_avms_ig.pdf)

11 [http://h71000.www7.hp.com/commercial/ada/ada_vvms_ig.pdf](http://h71000.www7.hp.com/commercial/ada/ada_vvms_ig.pdf)

12 [http://en.wikipedia.org/wiki/GNAT](http://en.wikipedia.org/wiki/GNAT)

13 [http://en.wikipedia.org/wiki/GNU_Compiler_Collection](http://en.wikipedia.org/wiki/GNU_Compiler_Collection)

14 [http://www.adacore.com](http://www.adacore.com/)

15 [http://en.wikipedia.org/wiki/GNU%20General%20Public%20License](http://en.wikipedia.org/wiki/GNU%20General%20Public%20License)

16 [http://en.wikipedia.org/wiki/GNU%20General%20Public%20License](http://en.wikipedia.org/wiki/GNU%20General%20Public%20License)

17 [http://en.wikipedia.org/wiki/GNAT%20Modified%20General%20Public%20License](http://en.wikipedia.org/wiki/GNAT%20Modified%20General%20Public%20License)

Several  optional  add-ons  are  available  from  various  places:

• ASIS,  the  Ada  Semantic  Interface  Specification[18](#part0013.xhtml__bookmark44),  is  a  library  that  allows  Ada  programs  to  examine  and  manipulate  other  Ada  programs.

• FLORIST[19](#part0013.xhtml__bookmark45)  is  a  library  that  provides  a  POSIX  programming  interface  to  the  operating  system.

• GDB,  the  GNU  Debugger,  with  Ada  extensions.

• GLADE implements Annex E, the Distributed Systems Annex. With it, one can write  distributed programs in Ada, where partitions of the program running on different  computers  communicate  over  the  network  with  one  another  and  with  shared  objects.

• GPS, the GNAT Programming Studio, is a full-featured integrated development environ-  ment,  written  in  Ada.  It  allows  you  to  code  in  Ada,  C  and  C++.

Many  Free  Software  libraries  are  also  available.

#### 2.4.1  GNAT  GPL  Edition

This is a source and binary release from AdaCore, intended for use by Free Software  developers only. If you want to distribute your binary programs linked with the GPL  run-time library, then you must do so under terms compatible with the GNU General Public  License.

As  of  GNAT  GPL  Edition  2011:

| Languages  supported | Ada  83,  Ada  95,  Ada  2005,  Ada  2012,  C,  C++ |
| License  for  the  run-timelibrary | pure  GPL |
| Native  platforms | GNU/Linux  on  i386  and  x86_64;  Microsoft  Win-dows  on  i386;  Microsoft  .NET  on  i386;  Mac  OS  X  (Darwin,  x86_64);  Solaris  on  SPARC. |
| Cross  platforms | AVR,  hosted  on  Windows;  Java  VM,  hosted  onWindows;  Mindstorms  NXT,  hosted  on  Windows |
| Compiler  back-end | GCC  4.5.3 |
| Available  from | [http://libre.adacore.com/](http://libre.adacore.com/) (requires free regis-tration) |
| Support | None |
| Add-ons  included | GDB,  GNATbench  (Eclipse  plug-in),  GPS  insource  and  binary  form;  many  more  in  source-only  form. |

#### 2.4.2  GNAT  Modified  GPL  releases

With these releases of GNAT, you can distribute your programs in binary form under  licensing  terms  of  your  own  choosing;  you  are  not  bound  by  the  GPL.

![](Images/image06597.jpeg)

18 [http://en.wikipedia.org/wiki/Ada%20Semantic%20Interface%20Specification](http://en.wikipedia.org/wiki/Ada%20Semantic%20Interface%20Specification)

19 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FPOSIX](http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FPOSIX)

###### GNAT  3.15p

This is the last public release of GNAT from AdaCore that uses the GNAT Modified General  Public  License[20](#part0014.xhtml__bookmark47).

GNAT 3.15p has passed the Ada Conformity Assessment Test Suite[21](#part0014.xhtml__bookmark48) (ACATS[22](#part0014.xhtml__bookmark49)). It was  released  in  October  2002.

The binary distribution from AdaCore also contains an Ada-aware version of the GNU  Debugger (GDB[23](#part0014.xhtml__bookmark50)), and a graphical front-end to GDB called the GNU Visual Debugger  (GVD).

| Languages  supported | Ada  83,  Ada  95,  C |
| License  for  the  run-timelibrary | GNAT-modified  GPL |
| Native  platforms | GNU/Linux  on  i386  (with  glibc  2.1  or  later),Microsoft  Windows  on  i386,  OS/2  2.0  or  later  on  i386,  Solaris  2.5  or  later  on  SPARC |
| Cross  platforms | none |
| Compiler  back-end | GCC  2.8.1 |
| Available  from | ftp://ftp.cs.kuleuven.ac.be/pub/Ada-Belgium/mirrors/gnu-ada/3.15p/ |
| Support | None |
| Add-ons  included | ASIS,  Florist,  GLADE,  GDB,  Gnatwin  (on  Win-dows  only),  GtkAda  1.2,  GVD |

###### GNAT  Pro

GNAT  Pro  is  the  professional  version  of  GNAT,  offered  as  a  subscription  package  by  AdaCore.  The  package  also  includes  professional  consulting,  training  and  maintenance  services. AdaCore can provide custom versions of the compiler for native or cross development.  For  more  information,  see  [http://www.adacore.com/.](http://www.adacore.com/)

| Languages  supported | Ada  83,  Ada  95,  Ada  2005,  Ada  2012,  C,  andoptionally  C++ |
| License  for  the  run-timelibrary | GNAT-modified  GPL |
| Native  platforms | many,  see  [http://www.adacore.com/home/](http://www.adacore.com/home/products/gnatpro/supported_platforms/)[products/gnatpro/supported_platforms/](http://www.adacore.com/home/products/gnatpro/supported_platforms/) |
| Cross  platforms | many,  see  [http://www.adacore.com/home/](http://www.adacore.com/home/products/gnatpro/supported_platforms/%3B)[products/gnatpro/supported_platforms/;](http://www.adacore.com/home/products/gnatpro/supported_platforms/%3B)even  more  on  request |

![](Images/image06598.jpeg)

20 [http://en.wikipedia.org/wiki/GNAT%20Modified%20General%20Public%20License](http://en.wikipedia.org/wiki/GNAT%20Modified%20General%20Public%20License)

21 [http://en.wikipedia.org/wiki/ISO%2018009](http://en.wikipedia.org/wiki/ISO%2018009)

22 [http://en.wiktionary.org/wiki/ACATS](http://en.wiktionary.org/wiki/ACATS)

23 [http://en.wikipedia.org/wiki/GDB](http://en.wikipedia.org/wiki/GDB)

| Compiler  back-end | GCC  4.3 |
| Available  from | [http://www.adacore.com/](http://www.adacore.com/) by  subscription  (com-mercial) |
| Support | Commercial;  customer-only  bug  database |
| Add-ons  included | ASIS,  Florist,  GDB,  GLADE,  GPS, GtkAda,XML/Ada,  and  many  more  in  source  and,  on  request,  binary  form. |

###### GCC

GNAT has been part of the Free Software Foundation[24](#part0015.xhtml__bookmark51)'s   GCC[25](#part0015.xhtml__bookmark52) since October 2001.  The Free Software Foundation does not distribute binaries, only sources. Its licensing of  the  run-time  library  for  Ada  (and  other  languages)  allows  the  development  of  proprietary  software  without  necessarily  imposing  the  terms  of  the  GPL[26](#part0015.xhtml__bookmark53).

Most GNU/Linux distributions and several distributions for other platforms include prebuilt  binaries;  see  below.

For technical reasons, we recommend against using the Ada compilers included in GCC 3.1,  3.2, 3.3 and 4.0\. Instead, we recommend using GCC 3.4, 4.1 or later, or one of the releases  from  AdaCore[27](#part0015.xhtml__bookmark54)  (3.15p,  GPL  Edition  or  Pro).

Since October 2003, AdaCore merge most of their changes from GNAT Pro into GCC during  Stage 1[28](#part0015.xhtml__bookmark55); this happens once for each major release. Since GCC 3.4, AdaCore has gradually  added  support  for  revised  language  standards,  first  Ada  2005  and  now  Ada  2012.

GCC  version  4.4  switched  to  version  3  of  the  GNU  General  Public  License[29](#part0015.xhtml__bookmark56)  and  grants  a  Runtime Library Exception[30](#part0015.xhtml__bookmark57) similar in spirit to the GNAT Modified General Public  License[31](#part0015.xhtml__bookmark58)  used  in  all  previous  versions.  This  Runtime  Library  Exception  applies  to  run-time  libraries  for  all  languages,  not  just  Ada.

As  of  GCC  4.7,  released  on  2012-03-22:

| Languages  supported | Ada  83,  Ada  95,  Ada  2005,  parts  of  Ada  2012,  C,C++,  Fortran  95,  Java,  Objective-C,  Objective-  C++  (and  others) |
| License  for  the  run-timelibrary | GPL  version  3[32](#part0000.xhtml__bookmark0)  with  Runtime  Library  Excep-tion[33](#part0000.xhtml__bookmark0) |
| Native  platforms | none  (source  only) |

![](Images/image06599.jpeg)

24 [http://www.fsf.org/](http://www.fsf.org/)

25 [http://gcc.gnu.org/](http://gcc.gnu.org/)

26 [http://en.wikipedia.org/wiki/GNU%20General%20Public%20License](http://en.wikipedia.org/wiki/GNU%20General%20Public%20License)

27 [http://www.adacore.com](http://www.adacore.com/)

28 [http://gcc.gnu.org/develop.html#stage1](http://gcc.gnu.org/develop.html#stage1)

29 [http://www.gnu.org/licenses/gpl.html](http://www.gnu.org/licenses/gpl.html)

30 [http://www.gnu.org/licenses/gcc-exception.html](http://www.gnu.org/licenses/gcc-exception.html)

31 [http://en.wikipedia.org/wiki/GNAT%20Modified%20General%20Public%20License](http://en.wikipedia.org/wiki/GNAT%20Modified%20General%20Public%20License)

32 [http://www.gnu.org/licenses/gpl.html](http://www.gnu.org/licenses/gpl.html)

33 [http://www.gnu.org/licenses/gcc-exception.html](http://www.gnu.org/licenses/gcc-exception.html)

| Cross  platforms | none  (source  only) |
| Compiler  back-end | GCC  4.7 |
| Available  from | [http://gcc.gnu.org/](http://gcc.gnu.org/) in  source  only  form. |
| Support | Volunteer;  public  bug  database |
| Add-ons  included | none |

#### 2.4.3  The  GNU  Ada  Project

The  GNU Ada Project[34](#part0016.xhtml__bookmark60) provides source and binary packages of various GNAT versions for  several operating systems, and, importantly, the scripts used to create the packages. This  may  be  helpful  if  you  plan  to  port  the  compiler  to  another  platform  or  create  a  cross-compiler;  there  are  instructions  for  building  your  own  GNAT  compiler  for  GNU/Linux[35](#part0016.xhtml__bookmark61)  and Mac  OS  X[36](#part0016.xhtml__bookmark62)  users.

Both GPL[37](#part0016.xhtml__bookmark63) and GMGPL[38](#part0016.xhtml__bookmark64) or  GCC Runtime Library Exception[39](#part0016.xhtml__bookmark65) versions of GNAT are  available.

| Languages  supported | Ada  83,  Ada  95,  Ada  2005,  C.  (Some  distributionsalso  support  Ada  2012,  Fortran  90,  Java,  Objective  Cand  Objective  C++) |
| License  for  the  run-timelibrary | pure,  GNAT-modified  GPL,  or  GCC  RuntimeLibrary  Exception |
| Native  platforms | Fedora  Core  4  and  5,  MS-DOS,  OS/2,  Solaris  10,SuSE  10,  MacOS  X,  (more?) |
| Cross  platforms | none |
| Compiler  back-end | GCC  2.8.1,  3.4,  4.0,  4.1,  4.2,  4.3,  4.4,  4.5,  4.6(various  binary  packages) |
| Available  from | Sourceforge[40](#part0000.xhtml__bookmark0) |
| Support | Volunteer;  public  bug  database |
| Add-ons  included | AdaBrowse,  ASIS,  Booch  Components,  Charles,GPS,  GtkAda  (more?) |

#### 2.4.4  A#  (A-Sharp,  a.k.a.  Ada  for  .NET)

This compiler is historical as it has now been merged into GNAT GPL Edition[41](#part0016.xhtml__bookmark66) and GNAT  Pro[42](#part0016.xhtml__bookmark67).

![](Images/image06600.jpeg)

34 [http://gnuada.sourceforge.net](http://gnuada.sourceforge.net/)

35 [http://ada.krischik.com/index.php/Articles/CompileGNAT](http://ada.krischik.com/index.php/Articles/CompileGNAT)

36 [http://forward-in-code.blogspot.com/2011/11/building-gcc-again.html](http://forward-in-code.blogspot.com/2011/11/building-gcc-again.html)

37 [http://en.wikipedia.org/wiki/GNU%20General%20Public%20License](http://en.wikipedia.org/wiki/GNU%20General%20Public%20License)

38 [http://en.wikipedia.org/wiki/GNAT%20Modified%20General%20Public%20License](http://en.wikipedia.org/wiki/GNAT%20Modified%20General%20Public%20License)

39 [http://www.gnu.org/licenses/gcc-exception.html](http://www.gnu.org/licenses/gcc-exception.html)

40 [http://sourceforge.net/projects/gnuada/files/](http://sourceforge.net/projects/gnuada/files/)

41 Chapter  [2.4.1](#part0013.xhtml__bookmark43)  on  page  [11](#part0013.xhtml__bookmark43)

42 Chapter  [2.4.2](#part0014.xhtml__bookmark46)  on  page  [12](#part0014.xhtml__bookmark46)

A#  is  a  port  of  Ada  to  the  .NET  Platform[43](#part0017.xhtml__bookmark68).  A#  was  originally  developed  at  the  Department  of Computer Science at the United States Air Force Academy which distribute A# as a  service to the Ada community under the terms of the GNU general public license.  A#  integrates well with Microsoft Visual Studio 2005, AdaGIDE and the RAPID open-source  GUI  Design  tool.  As  of  2006-06-06:

| Languages  supported | Ada  83,  Ada  95,  C |
| License  for  the  run-timelibrary | pure  GPL |
| Native  platforms | Microsoft  .NET |
| Cross  platforms | none |
| Compiler  back-end | GCC  3.4  (GNAT  GPL  2006  Edition?) |
| Available  from | [http://sourceforge.net/projects/asharp/](http://sourceforge.net/projects/asharp/) |
| Support | None  (but  see  GNAT  Pro) |
| Add-ons  included | none. |

#### 2.4.5  GNAT  for  AVR  microcontrollers

Rolf Ebert and others provide a version of GNAT configured as a cross-compiler to various  AVR microcontrollers[44](#part0017.xhtml__bookmark69), as well as an experimental Ada run-time library suitable for use on  the  microcontrollers.  As  of  Version  1.1.0  (2010-02-25):

| Languages  supported | Ada  83,  Ada  95,  Ada  2005,  C |
| License  for  the  run-timelibrary | GNAT-Modified  GPL |
| Host  platforms | GNU/Linux  and  Microsoft  Windows  on  i386 |
| Target  platforms | Various  AVR  8-bit  microcontrollers |
| Compiler  back-end | GCC  4.3 |
| Available  from | [http://avr-ada.sourceforge.net/](http://avr-ada.sourceforge.net/) |
| Support | Volunteer;  public  bug  database |
| Add-ons  included | partial  Ada  run  time  system,  AVR  peripheralssupport  library |

#### 2.4.6  GNAT  for  LEON

The Real-Time Research Group of the Technical University of Madrid (UPM, Universidad  Politécnica de Madrid) wrote a Ravenscar[45](#part0017.xhtml__bookmark70)-compliant real-time kernel for execution on  LEON processors[46](#part0017.xhtml__bookmark71) and a modified run-time library.  They also provide a GNAT cross-  compiler.  As  of  version  2.0.1:

![](Images/image06601.jpeg)

43 [http://www.microsoft.com/net/](http://www.microsoft.com/net/)

44 [http://en.wikipedia.org/wiki/Atmel_AVR](http://en.wikipedia.org/wiki/Atmel_AVR)

45 [http://en.wikipedia.org/wiki/Ravenscar%20profile](http://en.wikipedia.org/wiki/Ravenscar%20profile)

46 [http://en.wikipedia.org/wiki/LEON](http://en.wikipedia.org/wiki/LEON)

| Languages  supported | Ada  83,  Ada  95,  Ada  2005,  C |
| License  for  the  run-timelibrary | pure  GPL |
| Native  platforms | none |
| Cross  platforms | GNU/Linux  on  i686  to  LEON2  bare  boards |
| Compiler  back-end | GCC  4.1  (GNAT  GPL  2007  Edition) |
| Available  from | [http://www.dit.upm.es/ork/](http://www.dit.upm.es/ork/) |
| Support | ? |
| Add-ons  included | OpenRavenscar  real-time  kernel;  minimal  run-time  library |

#### 2.4.7  GNAT  for  Macintosh  (Mac  OS  X)

GNAT for Macintosh[47](#part0018.xhtml__bookmark72) provides both FSF (GMGPL) and AdaCore (GPL) versions of  GNAT[48](#part0018.xhtml__bookmark73)  with  Xcode[49](#part0018.xhtml__bookmark74)  and  Carbon[50](#part0018.xhtml__bookmark75)  integration  and  bindings.

Note  that  this  site  was  last  updated  for  GCC  4.3  and  Mac  OS  X  Leopard  (both  PowerPC  and  Intel-based).  Aside  from  the  work  on  integration  with  Apple’s  Carbon  graphical  user  interface and  with  Xcode 3.1  it  may be  preferable  to see above[51](#part0018.xhtml__bookmark76).

There  is  also  support  at  MacPorts[52](#part0018.xhtml__bookmark77);  the  last  update  (at  25  Nov  2011)  was  for  GCC  4.4.2.

#### 2.4.8  Prebuilt  packages  as  part  of  larger  distributions

Many distributions contain prebuilt binaries of GCC or various public releases of GNAT  from  AdaCore.  Quality  varies  widely  between  distributions.  The  list  of  distributions  below  is  in  alphabetical  oder.  (Please  keep  it  that  way.)

###### AIDE  (for  Microsoft  Windows)

AIDE — Ada Instant Development Environment[53](#part0018.xhtml__bookmark78) is a complete one-click, just-works Ada  distribution for Windows, consisting of GNAT, comprehensive documentation, tools and  libraries.  All are precompiled, and source code is also available.  The installation procedure  is  particularly  easy.  AIDE  is  intended  for  beginners  and  teachers,  but  can  also  be  used  by  advanced  users.

| Languages  supported | Ada  83,  Ada  95,  C |
| License  for  the  run-timelibrary | GNAT-modified  GPL |

![](Images/image06602.jpeg)

47 [http://www.macada.org/](http://www.macada.org/)

48 [http://en.wikipedia.org/wiki/GNAT](http://en.wikipedia.org/wiki/GNAT)

49 [http://en.wikipedia.org/wiki/Xcode](http://en.wikipedia.org/wiki/Xcode)

50 [http://en.wikipedia.org/wiki/Carbon%20%28API%29](http://en.wikipedia.org/wiki/Carbon%20%28API%29)

51 Chapter  [2.4.3](#part0016.xhtml__bookmark59)  on  page  [14](#part0016.xhtml__bookmark59)

52 [https://trac.macports.org/browser/trunk/dports/lang/gnat-gcc](https://trac.macports.org/browser/trunk/dports/lang/gnat-gcc)

53 [http://sr.sriviere.info/aide/aide.html](http://sr.sriviere.info/aide/aide.html)

| Native  platforms | Microsoft  Windows  on  i386 |
| Cross  platforms | none |
| Compiler  back-end | GCC  2.8.1 |
| Available  from | [http://www.ada-france.org/](http://www.ada-france.org/AIDE/)[AIDE/](http://www.ada-france.org/AIDE/)ftp://ftp.cs.kuleuven.ac.be/pub/Ada-  Belgium/mirrors/aide/ |
| Support | ? |
| Add-ons  included | ASIS,  GDB,  GPS,  GtkAda  (more?) |

###### Blastwave  (for  Solaris  on  SPARC  and  x86)

Blastwave[54](#part0019.xhtml__bookmark79)  has  binary  packages  of  GCC  3.4.5  and  4.0.2  with  Ada  support.  The  package  names  are  gcc3ada  and  gcc4ada  respectively.

| Languages  supported | Ada  83,  Ada  95,  parts  of  Ada  2005,  C,  C++,Fortran  95,  Java,  Objective-C,  Objective-C++ |
| License  for  the  run-timelibrary | GNAT-modified  GPL |
| Native  platforms | Solaris  and  OpenSolaris  on  SPARC |
| Cross  platforms | none |
| Compiler  back-end | GCC  3.4.5  and  4.0.2  (both  available) |
| Support | ? |
| Available  from | [http://www.blastwave.org/](http://www.blastwave.org/) |
| Add-ons  included | none  (?) |

###### OpenCSW  (for  Solaris  on  SPARC  and  x86)

OpenCSW[55](#part0019.xhtml__bookmark80)  has  binary  packages  of  GCC  3.4.6  and  4.6.2  with  Ada  support.  The  package  names  are  gcc3ada  and  gcc4ada  respectively.

| Languages  supported | Ada  83,  Ada  95,  parts  of  Ada  2005,  C,  C++,Fortran  95,  Java,  Objective-C,  Objective-C++ |
| License  for  the  run-timelibrary | GNAT-modified  GPL |
| Native  platforms | Oracle  Solaris  and  OpenSolaris  on  SPARC  andx86 |
| Cross  platforms | none |
| Compiler  back-end | GCC  3.4.6  and  4.6.2  (both  available) |
| Support | ? |
| Available  from | [http://www.opencsw.org/](http://www.opencsw.org/) |
| Add-ons  included | none  (?) |

![](Images/image06603.jpeg)

54 [http://www.blastwave.org](http://www.blastwave.org/)

55 [http://www.opencsw.org](http://www.opencsw.org/)

###### Cygwin  (for  Microsoft  Windows)

Cygwin[56](#part0020.xhtml__bookmark82),  the  Linux-like  environment  for  Windows,  also  contains  a  version  of  the  GNAT[57](#part0020.xhtml__bookmark83)  compiler. The Cygwin[58](#part0020.xhtml__bookmark84) version of GNAT[59](#part0020.xhtml__bookmark85) is older than the MinGW[60](#part0020.xhtml__bookmark86) version and does  not  support  DLLs  and  Multi-Threading  (as  of  11.2004).

###### Debian  (GNU/Linux and GNU/kFreeBSD)

There is a Debian Policy for Ada[61](#part0020.xhtml__bookmark87) which tries to make Debian the best Ada development and  deployment platform. The development platform includes the compiler and many libraries,  pre-packaged  and  integrated  so  as  to  be  easy  to  use  in  any  program.  The  deployment  platform  is the renowned  stable[62](#part0020.xhtml__bookmark88) distribution, which is suitable for mission-critical workloads and  enjoys long life cycles, typically 3 to 4 years. Because Debian is a binary distribution, it is  possible to deploy non-free, binary-only programs on it while enjoying all the benefits of a  stable platform. Compiler choices are conservative for this reason, and the Policy mandates  that all Ada programs and libraries be compiled with the same version of GNAT. This makes  it possible to use all libraries in the same program. Debian separates run-time libraries from  development  packages,  so  that  end  users  do  not  have  to  install  the  development  system  just  to  run  a  program.

The  GNU  Ada  compiler  can  be  installed  on  a  Debian  system  with  this  command:

![](Images/image06604.jpeg)

This  will  also  give  you  a  list  of  related  packages,  which  are  likely  to  be  useful  for  an  Ada  programmer.

Debian  is  unique  in  that  it  also  allows  programmers  to  use  some  of  GNAT's  internal  components  by  means  of  two  libraries:

• libgnatvsn  (licensed  under  GNAT-Modified  GPL)  and

• libgnatprj  (the  project  manager,  licensed  under  pure  GPL).  Debian  packages  make  use  of  these  libraries.

In  the  table  below,  the  information  about  the  future  Debian  7.0  Wheezy  is  accurate  as  of  July  2012  but  may  change.

56 [http://www.cygwin.com](http://www.cygwin.com/)

57 Chapter  [2.4](#part0012.xhtml__bookmark31)  on  page  [10](#part0012.xhtml__bookmark31)

58 [http://en.wikipedia.org/wiki/Cygwin](http://en.wikipedia.org/wiki/Cygwin)

59 [http://en.wikipedia.org/wiki/GNAT](http://en.wikipedia.org/wiki/GNAT)

60 [http://en.wikipedia.org/wiki/MinGW](http://en.wikipedia.org/wiki/MinGW)

61 [http://people.debian.org/~lbrenta/debian-ada-policy.html](http://people.debian.org/~lbrenta/debian-ada-policy.html)

62 [http://www.debian.org/releases/stable/](http://www.debian.org/releases/stable/)

![](Images/image06605.jpeg)![](Images/image06606.jpeg)![](Images/image06607.jpeg)

|  | 3.1  Sarge | 4.0  Etch | 5.0  Lenny | 6.0  Squeeze | 7.0  Wheezy |
| Release  date | June  2005 | April  2007 | February  2009 | February  2011 | 2013? |
| Languagessupported | Ada  83,  Ada  95,C | Ada  83,  Ada  95,  Ada  2005,  parts  of  Ada  2012,  C,  C++,  Fortran  95,  Java,Objective-C,  Objective-C++ |
| License  forthe run-time  library | GNAT-modified  GPL  (both  ZCX  and  SJLJ  versionsstarting  from  5.0  Lenny) | GPL  version  3  with  Run-timelibrary  exception |
| Native  plat-forms: | 3.1  Sarge | 4.0  Etch | 5.0  Lenny | 6.0  Squeeze | 7.0  Wheezy |
| alpha |  | yes | yes |  |  |
| amd64 |  | yes | yes | yes | yes |
| armel |  |  |  | preliminary | yes |
| armhf |  |  |  |  | yes |
| hppa |  | yes | yes | yes |  |
| hurd-i386 |  |  |  |  | preliminary |
| i386 | yes | yes | yes | yes | yes |
| ia64 |  | yes | yes | yes | yes |
| kfreebsd-amd64 |  |  |  | yes | yes |
| kfreebsd-i386 |  | yes | yes | yes | yes |
| mips |  | yes | yes | yes | yes |
| mipsel |  | yes | yes | yes | yes |
| powerpc | yes | yes | yes | yes | yes |
| ppc64 |  |  | yes | yes | yes |
| s390 |  | yes | yes | yes | yes |
| sparc | yes | yes | yes | yes | yes |
| Cross  plat-forms | none |
| Compilerback-end | GCC  2.8.1 | GCC  4.1 | GCC  4.3 | GCC  4.4 | GCC  4.6 |
| Available  from | [http://www.debian.org/](http://www.debian.org/) |
|  |  |  |  |  |  |

![](Images/image06608.jpeg)![](Images/image06609.jpeg)![](Images/image06610.jpeg)

|  | 3.1  Sarge | 4.0  Etch | 5.0  Lenny | 6.0  Squeeze | 7.0  Wheezy |
| Release  date | June  2005 | April  2007 | February  2009 | February  2011 | 2013? |
| Languagessupported | Ada  83,  Ada  95,C | Ada  83,  Ada  95,  Ada  2005,  parts  of  Ada  2012,  C,  C++,  Fortran  95,  Java,Objective-C,  Objective-C++ |
| License  forthe run-time  library | GNAT-modified  GPL  (both  ZCX  and  SJLJ  versionsstarting  from  5.0  Lenny) | GPL  version  3  with  Run-timelibrary  exception |
| Native  plat-forms: | 3.1  Sarge | 4.0  Etch | 5.0  Lenny | 6.0  Squeeze | 7.0  Wheezy |
| Support | Volunteer;  public  bug  database;  paid  support  available  from  third  parties;  public  mailing  list[63](#part0000.xhtml__bookmark0) |
| Add-ons  in-cluded | 3.1  Sarge | 4.0  Etch | 5.0  Lenny | 6.0  Squeeze | 7.0  Wheezy |
| ada-reference-manual | 1995 | 1995 | 1995 | 2005 | 2012 |
| AdaBindX | 0.7.2 |  |  |  |  |
| AdaBrowse | 4.0.2 | 4.0.2 | 4.0.2 | 4.0.3 | 4.0.3 |
| AdaCGI | 1.6 | 1.6 | 1.6 | 1.6 | 1.6 |
| AdaControl |  | 1.6r8 | 1.9r4 | 1.12r3 | 1.12r3 |
| APQ  (with  Post-greSQL) |  |  |  | 3.0 | 3.2 |
| AdaSockets | 1.8.4.7 | 1.8.4.7 | 1.8.4.7 | 1.8.8 | 1.8.10 |
| Ahven |  |  | 1.2 | 1.7 | 2.1 |
| Alog |  |  | 0.1 | 0.3 | 0.4.1 |
| anet |  |  |  |  | 0.1 |
| ASIS | 3.15p | 2005 | 2007 | 2008 | 2010 |
| AUnit | 1.01 | 1.03 | 1.03 | 1.03 | 1.03 |
| AWS | 2.0 | 2.2 | 2.5  prerelease | 2.7 | 2.10.2 |
| Charles | 2005-02-17 | (superseded  by  Ada.Containers  in  gnat) |
| Florist | 3.15p | 2006 | 2006 | 2009 | 2011 |
|  |  |  |  |  |  |

![](Images/image06611.jpeg)

63 [http://lists.debian.org/debian-ada](http://lists.debian.org/debian-ada)

![](Images/image06612.jpeg)![](Images/image06613.jpeg)![](Images/image06614.jpeg)

|  | 3.1  Sarge | 4.0  Etch | 5.0  Lenny | 6.0  Squeeze | 7.0  Wheezy |
| Release  date | June  2005 | April  2007 | February  2009 | February  2011 | 2013? |
| Languagessupported | Ada  83,  Ada  95,C | Ada  83,  Ada  95,  Ada  2005,  parts  of  Ada  2012,  C,  C++,  Fortran  95,  Java,Objective-C,  Objective-C++ |
| License  forthe run-time  library | GNAT-modified  GPL  (both  ZCX  and  SJLJ  versionsstarting  from  5.0  Lenny) | GPL  version  3  with  Run-timelibrary  exception |
| Native  plat-forms: | 3.1  Sarge | 4.0  Etch | 5.0  Lenny | 6.0  Squeeze | 7.0  Wheezy |
| GDB | 5.3 | 6.4 | 6.8 | 7.0.1 | 7.4.1 |
| GLADE | 3.15p | 2006 |  | (see  PolyORB) |
| GMPAda |  |  |  | 0.0.20091124 | 0.0.20120331 |
| GNADE | 1.5.1 | 1.6.1 | 1.6.1 | 1.6.2 | 1.6.2 |
| GNAT  Checker | 1999-05-19 | (superseded  by  AdaControl) |
| GPRBuild |  |  |  | 1.3.0w | 2011 |
| GPS | 2.1 | 4.0.1 | 4.0.1 | 4.3 | 5.0 |
| GtkAda | 2.4 | 2.8.1 | 2.8.1 | 2.14.2 | 2.24.0 |
| Log4Ada |  |  |  | 1.0 | 1.2 |
| Narval |  |  |  | 1.10.2 |  |
| OpenToken | 3.0b | 3.0b | 3.0b | 4.0b | 4.0b |
| PC/SC  Ada |  |  |  | 0.6 | 0.7.1 |
| PolyORB |  |  |  | 2.6  prerelease | 2.8  prerelease |
| PLPlot |  |  | 5.9.0 | 5.9.5 | 5.9.5 |
| TemplatesParser |  | 10.0+20060522 | 11.1 | 11.5 | 11.6 |
| TextTools | 2.0.3 | 2.0.3 | 2.0.5 | 2.0.6 |  |
| XML/Ada | 1.0 | 2.2 | 3.0 | 3.2 | 4.1 |
| XML-EZ-out |  |  |  | 1.06 | 1.06.1 |
|  |  |  |  |  |  |

The ADT plugin for Eclipse (see section ObjectAda from Aonix[64](#part0024.xhtml__bookmark89)) can be used with GNAT  as  packaged  for  Debian  Etch.  Specify  "/usr"  as  the  toolchain  path.

###### DJGPP  (for  MS-DOS)

DJGPP  has  GNAT[65](#part0024.xhtml__bookmark90)  as  part  of  their  GCC[66](#part0024.xhtml__bookmark91)  distribution.

DJGPP[67](#part0024.xhtml__bookmark92)  is a port of a comprehensive collection of GNU utilities to MS-DOS with 32-bit  extensions, and is actively supported (as of 1.2005). It includes the whole GCC[68](#part0024.xhtml__bookmark93) compiler  collection,  that  now  includes  Ada.  See  the  DJGPP[69](#part0024.xhtml__bookmark94)  website  for  installation  instructions.

DJGPP  programs  run  also  in  a  DOS  command  box  in  Windows,  as  well  as  in  native  MS-DOS  systems.

###### FreeBSD

FreeBSD[70](#part0024.xhtml__bookmark95)'s  ports  collection[71](#part0024.xhtml__bookmark96)  contains  GNAT  GPL  2006  Edition  (package  gnat-2006),  GNAT 3.15p, GCC 4.1, 4.2 and 4.3 with support for Ada. The usual way to install a package  on FreeBSD is to compile it from source; not all add-ons are compatible with all versions of  GNAT  provided.

You  can  also  use  the  Debian  packages  described  above  in  a  jail,  thanks  to  Debian  GNU/k-  FreeBSD.

As  of  2008-11-10:

| Languages  supported | Ada  83,  Ada  95,  parts  of  Ada  2005,  C |
| License  for  the  run-timelibrary | both  pure  and  modified  GPL  available |
| Native  platforms | FreeBSD  on  i386  (more?) |
| Cross  platforms | none |
| Compiler  back-end | GCC  2.8.1,  3.4,  4.1,  4.2,  4.3 |
| Available  from | [http://www.freebsd.org](http://www.freebsd.org/) |
| Support | Volunteer;  public  bug  database |
| Add-ons  included | AdaBindX,  AdaCurses,  AdaSDL,  AdaSockets,AFlex+AYACC, ASIS, AUnit, Booch Compo-  nents, CBind, Florist, GLADE, GtkAda, SGL,  XML/Ada  (more?) |

![](Images/image06615.jpeg)

64 Chapter  [2.4.8](#part0026.xhtml__bookmark98)  on  page  [24](#part0026.xhtml__bookmark98)

65 [http://en.wikipedia.org/wiki/GNAT](http://en.wikipedia.org/wiki/GNAT)

66 [http://en.wikipedia.org/wiki/GCC](http://en.wikipedia.org/wiki/GCC)

67 [http://www.delorie.com/djgpp/](http://www.delorie.com/djgpp/)

68 [http://en.wikipedia.org/wiki/GCC](http://en.wikipedia.org/wiki/GCC)

69 [http://www.delorie.com/djgpp/](http://www.delorie.com/djgpp/)

70 [http://www.freebsd.org](http://www.freebsd.org/)

71 [http://www.freebsd.org/ports](http://www.freebsd.org/ports)

###### Gentoo  GNU/Linux

The  GNU  Ada  compiler  can  be  installed  on  a  Gentoo  system  using  emerge:

![](Images/image06616.jpeg)

In contrast to Debian,  Gentoo is primarily a source distribution,  so many packages are  available  only  in  source  form,  and  require  the  user  to  recompile  them  (using  emerge).

Also in contrast to Debian, Gentoo supports several versions of GNAT in parallel on the  same system. Be careful, because not all add-ons and libraries are available with all versions  of  GNAT.

| Languages  supported | Ada  83,  Ada  95,  Ada  2005,  C  (more?) |
| License  for  the  run-timelibrary | pure  or  GNAT-modified  GPL  (both  available) |
| Native  platforms | Gentoo  GNU/Linux  on  amd64,  powerpc  and  i386 |
| Cross  platforms | none |
| Compiler  back-end | GCC  3.4,  4.1  (various  binary  packages) |
| Available  from | [http://www.gentoo.org/](http://www.gentoo.org/) (see other Gentoodev-ada[72](#part0000.xhtml__bookmark0)  packages) |
| Support | Volunteer;  public  bug  database |
| Add-ons  included | AdaBindX,  AdaBroker,  AdaDoc,  AdaOpenGL,AdaSockets, ASIS, AUnit, Booch Components,  CBind,  Charles,  Florist,  GLADE,  GPS,  GtkAda,  XML/Ada |

###### Mandriva  Linux

The  GNU  Ada  compiler  can  be  installed  on  a  Mandriva  system  with  this  command:

![](Images/image06617.jpeg)

###### MinGW  (for  Microsoft  Windows)

MinGW  —  Minimalist  GNU  for  Windows[73](#part0025.xhtml__bookmark97)  contains  a  version  of  the  GNAT  compiler.

The current version of MinGW (5.1.6) contains gcc-4.5.0\. This includes a fully functional  GNAT  compiler.  If  the  automatic  downloader  does  not  work  correctly  you  can  download  the  compiler  directly:  pick  gcc-4.5.0-1  from  MinGW/BaseSystem/GCC/Version4/

![](Images/image06618.jpeg)

72 [http://es.znurt.org/dev-ada](http://es.znurt.org/dev-ada)

73 [http://mingw.sourceforge.net](http://mingw.sourceforge.net/)

###### old instructions

The  following  list  should  help  you  with  the  installation.  (I  may  have  forgotten  something  —  but  this  is  wiki,  just  add  to  the  list)

1. Install  MinGW-3.1.0-1.exe

a) extract  binutils-2.15.91-20040904-1.tar.gz

b) extract  mingw-runtime-3.5.tar.gz

c) extract  gcc-core-3.4.2-20040916-1.tar.gz

d) extract  gcc-ada-3.4.2-20040916-1.tar.gz

e) extract  gcc-g++-3.4.2-20040916-1.tar.gz  (Optional)

f) extract  gcc-g77-3.4.2-20040916-1.tar.gz  (Optional)

g) extract  gcc-java-3.4.2-20040916-1.tar.gz  (Optional)

h) extract  gcc-objc-3.4.2-20040916-1.tar.gz  (Optional)

i) extract  w32api-3.1.tar.gz

2. Install  mingw32-make-3.80.0-3.exe  (Optional)

3. Install  gdb-5.2.1-1.exe  (Optional)

4. Install  MSYS-1.0.10.exe  (Optional)

5. Install  msysDTK-1.0.1.exe  (Optional)

a) extract  msys-automake-1.8.2.tar.bz2  (Optional)

b) extract  msys-autoconf-2.59.tar.bz2  (Optional)

c) extract  msys-libtool-1.5.tar.bz2  (Optional)

I  have  made  good  experience  in  using  D:\MinGW  as  target  directory  for  all  installations  and  extractions.

Also  noteworthy  is  that  the  Windows  version  for  GNAT  from  Libre  is  also  based  on  MinGW.  In  gcc-3.4.2-release_notes.txt  from  MinGW  site  reads:  please  check  that  the  files  in  the

/lib/gcc/mingw32/3.4.2/adainclude and  adalib  directories  are  flagged  as  read-only.  This

attribute  is  necessary  to  prevent  them  from  being  deleted  when  using  gnatclean  to  clean  a  project.

So  be  sure  to  do  this.

###### SuSE  Linux

All  versions  of  SuSE  Linux  have  a  GNAT  compiler  included.  SuSE  versions  9.2  and  higher  also  contains  ASIS,  Florist  and  GLADE  libraries.  The  following  two  packages  are  needed:

![](Images/image06619.jpeg)

For  SuSE  version  12.1,  the  compiler  is  in  the  package

![](Images/image06620.jpeg)

For  64  bit  system  you  will  need  the  32  bit  compatibility  packages  as  well:

![](Images/image06621.jpeg)

###### Ubuntu

Ubuntu  (and  derivatives  like  Kubuntu,  Xubuntu...)  is  a  Debian-based  Linux  distribution,  thus the installation process described above[74](#part0027.xhtml__bookmark102) can be used. Graphical package managers  like  Synaptic  or  Adept  can  also  be  employed  to  select  the  Ada  packages.

## 2.5 ICC  from  Irvine  Compiler  Corporation

Irvine  Compiler  Corporation[75](#part0027.xhtml__bookmark103) provides  native  and  cross  compilers  for  various  platforms.[http:](http://www.irvine.com/products.html)

[//www.irvine.com/products.html](http://www.irvine.com/products.html) The  compiler  and  run-time  system  support  development  of  certified,  safety-critical  software.

Commercial, proprietary.  No-cost evaluation is possible on request.  Royalty-free redistribu-  tion  of  the  run-time  system  is  allowed.

## 2.6 Janus/Ada  83  and  95  from  RR  Software

RR Software[76](#part0027.xhtml__bookmark104) offers native compilers for MS-DOS, Microsoft Windows and various Unix  and Unix-like systems, and a library for Windows GUI programming called CLAW. There  are  academic,  personal  and  professional  editions,  as  well  as  support  options.

Commercial  but  relatively  cheap;  proprietary.

## 2.7 MAXAda  from  Concurrent

Concurrent[77](#part0027.xhtml__bookmark105) offers  MAXAda[78](#part0027.xhtml__bookmark106),  an  Ada  95  compiler  for  Linux/Xeon  and  PowerPC  platforms,  and  Ada  bindings  to  POSIX  and  X/Motif.[http://www.ccur.com/pdf/cpb-sw-maxada.pdf](http://www.ccur.com/pdf/cpb-sw-maxada.pdf)

Commercial,  proprietary.

![](Images/image06622.jpeg)

74 Chapter  [2.4.8](#part0020.xhtml__bookmark81)  on  page  [18](#part0020.xhtml__bookmark81)

75 [http://www.irvine.com/](http://www.irvine.com/)

76 [http://www.rrsoftware.com](http://www.rrsoftware.com/)

77 [http://www.ccur.com/](http://www.ccur.com/)

78 [http://www.ccur.com/products_rt_maxada.aspx](http://www.ccur.com/products_rt_maxada.aspx)

## 2.8 ObjectAda  from  Atego  (formerly  Aonix)

Atego[79](#part0028.xhtml__bookmark109) offers native and cross compilers for various platforms.  They come with an IDE,  a debugger,  a plug-in for Eclipse and a POSIX binding[80](#part0028.xhtml__bookmark110)  [http://www.aonix.com/pdf/](http://www.aonix.com/pdf/oa-linux.pdf)  [oa-linux.pdf](http://www.aonix.com/pdf/oa-linux.pdf).

On Microsoft Windows and GNU/Linux on i386, Aonix offers two pricing models, at the  customer's option: either a perpetual license fee with optional support, or just the yearly  support fee:  For Linux, that's $3000 for a single user or $12,000 for a 5-user service pack.  See  the  full  press  release[81](#part0028.xhtml__bookmark111).

In  addition,  they  offer  "ObjectAda  Special  Edition":  a  no-cost  evaluation  version  of  ObjectAda  that  limits  the  size  of  programs  that  can  be  compiled  with  it,  but  is  otherwise  fully  functional,  with  IDE  and  debugger.  Free  registration  required[82](#part0028.xhtml__bookmark112).

A recent contribution by Atego is  ADT[83](#part0028.xhtml__bookmark113) for  Eclipse[84](#part0028.xhtml__bookmark114). The Ada Development Tools add  Ada language support to the Eclipse open source development platform. ADT can be used  with Aonix compilers, and with GNAT. An open source vendor supported project is outlined  for  ADT  at  Eclipse[85](#part0028.xhtml__bookmark115).  Codenamed  Hibachi  and  showcased  at  the  Ada  Conference  UK  2007  and  during  Ada-Europe  2007,  the  project  has  now  been  officially  created[86](#part0028.xhtml__bookmark116).

Commercial,  proprietary.

## 2.9 PowerAda  from  OC  Systems

OC  Systems[87](#part0028.xhtml__bookmark117)  offers  Ada  compilers  and  bindings  to  POSIX  and  X-11:

• PowerAda[88](#part0028.xhtml__bookmark118),  an  Ada  95  compiler  for  Linux  and  AIX,

• LegacyAda/390[89](#part0028.xhtml__bookmark119),  an  Ada  83  compiler  for  IBM  System  370  and  390  mainframes  Commercial,  proprietary.

## 2.10 Rational  Apex  from  Atego  (formerly  IBM  Rational[90](#part0028.xhtml__bookmark120))

Rational  Apex[91](#part0028.xhtml__bookmark121)  for  native  and  embedded  development.

![](Images/image06623.jpeg)

79 [http://www.atego.com/](http://www.atego.com/)

80 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FPOSIX](http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FPOSIX)

81 [http://www.atego.com/pressreleases/pressitem/aonix-shatters-ada-price-barrier-for-linux](http://www.atego.com/pressreleases/pressitem/aonix-shatters-ada-price-barrier-for-linux)

82 [http://www.atego.com/support/eval-aonix-objectada/](http://www.atego.com/support/eval-aonix-objectada/)

83 [http://www.aonix.com/adt.html](http://www.aonix.com/adt.html)

84 [http://www.eclipse.org](http://www.eclipse.org/)

85 [http://www.eclipse.org/proposals/adt/](http://www.eclipse.org/proposals/adt/)

86 [http://www.eclipse.org/hibachi/](http://www.eclipse.org/hibachi/)

87 [http://www.ocsystems.com/](http://www.ocsystems.com/)

88 [http://www.ocsystems.com/prod_powerada.html](http://www.ocsystems.com/prod_powerada.html)

89 [http://www.ocsystems.com/prod_legacyada.html](http://www.ocsystems.com/prod_legacyada.html)

90 Atego  acquires  IBM  Rational  Apex  Ada  Developer  product  family

91 [http://www-306.ibm.com/software/awdtools/developer/ada/](http://www-306.ibm.com/software/awdtools/developer/ada/)

![](Images/image06624.jpeg)

Commercial,  proprietary.

## 2.11 SCORE  from  DDC-I

SCORE  from  DDC-I

DDC-I[92](#part0029.xhtml__bookmark125) offers its SCORE cross-compilers for embedded development. SCORE stands for  Safety-Critical,  Object-oriented,  Real-time  Embedded.

Commercial,  proprietary.

## 2.12 XD  Ada  from  SWEP-EDS

XD Ada from  SWEP-EDS

XD Ada[93](#part0029.xhtml__bookmark126) is an Ada 83 cross-compiler for embedded development.  Hosts include VAX,  Alpha  and  Integrity  Servers  running  OpenVMS.  Targets  include  Motorola  68000  and  MIL-  STD-1750A  processors.

Commercial,  proprietary.

## 2.13 XGC  Ada  from  XGC  Software

XGC  Ada  from  XGC  Software

XGC compilers are GCC with custom run-time libraries suitable for avionics and space  applications. The run-time kernels are very small and do not support exception propagation  (i.e.  you  can  handle  an  exception  only  in  the  subprogram  that  raised  it).

Commercial  but  some  versions  are  also  offered  as  free  downloads.  Free  Software.

| Languages  supported | Ada  83,  Ada  95,  C |
| License  for  the  run-timelibrary | GNAT-Modified  GPL |
| Native  platforms | none |

![](Images/image06625.jpeg)

92 [http://www.ddci.com/](http://www.ddci.com/)

93 [http://www.swep-eds.com/XD%20Ada/Xd%20ada.htm](http://www.swep-eds.com/XD%20Ada/Xd%20ada.htm)

| Cross  platforms | Hosts:  sun-sparc-solaris,  pc-linux2.*;  targets  arebare  boards  with  ERC32[94](#part0000.xhtml__bookmark0),  MIL-STD-1750A[95](#part0000.xhtml__bookmark0),  Motorola  68000[96](#part0000.xhtml__bookmark0)  family  or  Intel  32-bit[97](#part0000.xhtml__bookmark0)  proces-  sors.  PowerPC[98](#part0000.xhtml__bookmark0)  and Intel 80186[99](#part0000.xhtml__bookmark0)  targets on  request. |
| Compiler  back-end | GCC  2.8.1 |
| Available  from | [http://www.xgc.com/](http://www.xgc.com/) |
| Support | Commercial |
| Add-ons  included | Ravenscar-compliant  run-time  kernels,  certifiedfor  avionics  and  space  applications;  gdb  cross-  debugger;  target  simulator. |

## 2.14 References

References

![](Images/image06626.jpeg)

94 [http://en.wikipedia.org/wiki/ERC32](http://en.wikipedia.org/wiki/ERC32)

95 [http://en.wikipedia.org/wiki/MIL-STD-1750A](http://en.wikipedia.org/wiki/MIL-STD-1750A)

96 [http://en.wikipedia.org/wiki/Motorola_68000](http://en.wikipedia.org/wiki/Motorola_68000)

97 [http://en.wikipedia.org/wiki/IA_32](http://en.wikipedia.org/wiki/IA_32)

98 [http://en.wikipedia.org/wiki/PowerPC](http://en.wikipedia.org/wiki/PowerPC)

99 [http://en.wikipedia.org/wiki/Intel_80186](http://en.wikipedia.org/wiki/Intel_80186)

# 3 Building

Ada  programs  are  usually  easier  to  build  than  programs  written  in  other  languages  like  C  or C++, which frequently require a makefile.  This is because an Ada source file already  specifies  the  dependencies  of  its  source  unit.  See  the  with  keyword[1](#part0031.xhtml__bookmark130)  for  further  details.

Building an Ada program is not defined by the Reference Manual, so this process is absolutely  dependent  on  the  compiler.  Usually  the  compiler  kit  includes  a  make  tool  which  compiles  a  main  program  and  all  its  dependencies,  and  links  an  executable  file.

## 3.1 Building  with  various  compilers

Building  with  various  compilers

This  list  is  incomplete.  You  can  help  Wikibooks  by  adding  the  build  information[2](#part0031.xhtml__bookmark131) for  other  compilers.

#### 3.1.1  GNAT

With  GNAT[3](#part0031.xhtml__bookmark132),  you  can  run  this  command:

![](Images/image06627.jpeg)

If  the  file  contains  a  procedure,  gnatmake  will  generate  an  executable  file  with  the  procedure  as  main  program.  Otherwise,  e.g.  a  package,  gnatmake  will  compile  the  unit  and  all  its  dependencies.

###### GNAT  command  line

gnatmake  can  be  written  as  one  word  gnatmake  or  two  words  gnat  make.  For  a  full  list  of gnat commands just type gnat without any command options.  The output will look  something  like  this:

![](Images/image06628.jpeg)

1 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fwith](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fwith)

2 http://en.wikibooks.org/w/index.php?title=Ada_Programming/Building&action=edit

3 [http://en.wikipedia.org/wiki/GNAT](http://en.wikipedia.org/wiki/GNAT)

![](Images/image06629.jpeg)

For  further  help  on  the  option  just  type  the  command  (one  word  or  two  words  —  as  you  like)  without  any  command  options.

###### GNAT  IDE

The GNAT toolchain comes with an IDE[4](#part0032.xhtml__bookmark133) called GPS[5](#part0032.xhtml__bookmark134). You need to download and install it  separately.  The  GPS  features  a  graphical  user  interface[6](#part0032.xhtml__bookmark135).

There  are  also  GNAT  plugins  for  Emacs[7](#part0032.xhtml__bookmark136)  (  Ada  Mode[8](#part0032.xhtml__bookmark137)),  KDevelop[9](#part0032.xhtml__bookmark138)  and  Vim[10](#part0032.xhtml__bookmark139)  (  Ada  Mode[11](#part0032.xhtml__bookmark140))  available.

Both  Emacs  and  Vim  Ada-Mode  are  maintained  by  The  GNU  Ada  project[12](#part0032.xhtml__bookmark141).

###### GNAT  with  Xcode

Apple's  free  (gratis)  IDE,  Xcode,  is  included  with  every  Macintosh  but  requires  an  explicit  installation  step  from  DVD-ROM  or  CD-ROM.  It  is  also  downloadable  from  [http://](http://developer.apple.com/)  [developer.apple.com/.](http://developer.apple.com/) Xcode uses the GNU Compiler Collection[13](#part0032.xhtml__bookmark142) and thus supports  Ada,  GDB[14](#part0032.xhtml__bookmark143),  etc...  and  also  includes  myriad  tools  for  optimizing  code  which  are  unique  to

![](Images/image06630.jpeg)

4 [http://en.wikipedia.org/wiki/Integrated%20development%20environment](http://en.wikipedia.org/wiki/Integrated%20development%20environment)

5 [http://en.wikipedia.org/wiki/GNAT%20Programming%20Studio](http://en.wikipedia.org/wiki/GNAT%20Programming%20Studio)

6 [http://en.wikipedia.org/wiki/Graphical%20user%20interface](http://en.wikipedia.org/wiki/Graphical%20user%20interface)

7 [http://en.wikipedia.org/wiki/Emacs](http://en.wikipedia.org/wiki/Emacs)

8 [http://stephe-leake.org/emacs/ada-mode/emacs-ada-mode.html](http://stephe-leake.org/emacs/ada-mode/emacs-ada-mode.html)

9 [http://en.wikipedia.org/wiki/KDevelop](http://en.wikipedia.org/wiki/KDevelop)

10 [http://en.wikipedia.org/wiki/Vim%20%28text%20editor%29](http://en.wikipedia.org/wiki/Vim%20%28text%20editor%29)

11 [http://www.vim.org/scripts/script.php?script_id=1609](http://www.vim.org/scripts/script.php?script_id=1609)

12 [http://gnuada.sourceforge.net](http://gnuada.sourceforge.net/)

13 [http://en.wikipedia.org/wiki/GNU%20Compiler%20Collection](http://en.wikipedia.org/wiki/GNU%20Compiler%20Collection)

14 [http://en.wikipedia.org/wiki/GNU%20Debugger](http://en.wikipedia.org/wiki/GNU%20Debugger)

the Macintosh platform. However, GNAT must be installed separately as it is (as of 2008) not  distributed as part of Xcode.  Get the binary and/or sources at [http://www.macada.org/,](http://www.macada.org/)  along with numerous tools and bindings including bindings to Apple's Carbon frameworks  which  allow  the  development  of  complete,  "real"  Mac  programs,  all  in  Ada.

#### 3.1.2  Rational  APEX

Rational APEX is a complete development environment comprising a language sensitive  editor, compiler, debugger, coverage analyser, configuration management and much more.  You  normally  work  with  APEX  running  a  GUI.

APEX  has  been  built  for  the  development  of  big  programs.  Therefore  the  basic  entity  of APEX is a subsystem, a directory with certain traits recognized by APEX. All Ada  compilation  units  have  to  reside  in  subsystems.

You  can  define  an  export  set,  i.e.  the  set  of  Ada  units  visible  to  other  subsystems.  However  for  a  subsystem  A  to  gain  visibility  to  another  subsystem  B,  A  has  to  import  B.  After  importing,  A  sees  all  units  in  B's  export  set.  (This  is  much  like  the  with-clauses,  but  here  visibility  means  only  potential  visibility  for  Ada: units  to  be  actually  visible  must  be  mentioned  in  a with-clause of course; units not in the export set cannot be used in with-clauses of Ada  units  in  external  subsystems.)

Normally  subsystems  should  be  hierarchically  ordered,  i.e.  form  a  directed  graph.  But  for  special  uses,  subsystems  can  also  mutually  import  one  another.

For configuration management, a subsystem is decomposed in views, subdirectories of the  subsystem. Views hold different development versions of the Ada units. So actually it's not  subsystems which import other subsystems, rather subsystem views import views of other  subsystems. (Of course, the closure of all imports must be consistent — it cannot be the  case  that  e.g.  subsystem  (A,  view  A1)  imports  subsystems  (B,  B1)  and  (C,  C1),  whereas  (B,  B1)  imports  (C,  C2)).

A view can be defined to be the development view.  Other views then hold releases at  different  stages.

Each  Ada  compilation  unit  has  to  reside  in  a  file  of  its  own.  When  compiling  an  Ada  unit,  the compiler follows the with-clauses.  If a unit is not found within the subsystem holding  the compile, the compiler searches the import list (only the direct imports are considered,  not  the  closure).

Units can be taken under version control.  In each subsystem, a set of histories can be  defined. An Ada unit can be taken under control in a history. If you want to edit it, you first  have to check it out — it gets a new version number. After the changes, you can check it in  again, i.e. make the changes permanent (or you abandon your changes, i.e. go back to the  previous  version).  You  normally  check  out  units  in  the  development  view  only;  check-outs  in  release  views  can  be  forbidden.

You can select which version shall be the active one; normally it is the one latest checked in.  You  can  even  switch  histories  to  get  different  development  paths.  e.g.  different  bodies  of  the  same  specification  for  different  targets.

#### 3.1.3  ObjectAda

ObjectAda  is  a  set  of  tools  for  editing,  compiling,  navigating  and  debugging  programs  written in Ada. There are various editions of ObjectAda. With some editions you compile  programs for the same platform and operating systems on which you run the tools. These  are called native. With others, you can produce programs for different operating systems  and  platforms.  One  possible  platform  is  the  Java  virtual  machine.

These remarks apply to the native Microsoft Windows edition. You can run the translation  tools  either  from  the  IDE  or  from  the  command  line.

Whether you prefer to work from the IDE, or from the command line, a little bookkeeping is  required.  This  is  done  by  creating  a  project.  Each  project  consists  of  a  number  of  source  files,  and  a  number  of  settings  like  search  paths  for  additional  Ada  libraries  and  other  dependences.  Each project also has at least one target. Typically, there is a debug target, and a release  target.  The names of the targets indicate their purpose.  At one time you compile for  debugging, typically during development, at other times you compile with different settings,  for example when the program is ready for release.  Some (all commercial?)  editions of  ObjectAda  permit  a  Java  (VM)  target.

#### 3.1.4  DEC  Ada  for  VMS

DEC Ada is an Ada 83 compiler for VMS[15](#part0034.xhtml__bookmark144). While “DEC Ada” is probably the name most  users  know,  the  compiler  is  now  called  “  HP  Ada[16](#part0034.xhtml__bookmark145)”.  It  had  previously  been  known  also  by  names  of  "VAX  Ada"  and  "Compaq  Ada".

DEC Ada uses a true library management system — so the first thing you need to do is  create  and  activate  a  library:

![](Images/image06631.jpeg)

When  creating  a  library  you  already  set  some  constraints  like  support  for  Long_Float  or  the  available  memory  size.  So  carefully  read

![](Images/image06632.jpeg)

Then  next  step  is  to  load  your  Ada  sources  into  the  library:

![](Images/image06633.jpeg)

The sources don't need to be perfect at this stage but syntactically correct enough for the  compiler to determine the packages declared and analyze the with statements.  Dec Ada  allows  you  to  have  more  than  one  package  in  one  source  file  and  you  have  any  filename

![](Images/image06634.jpeg)

15 [http://en.wikipedia.org/wiki/OpenVMS](http://en.wikipedia.org/wiki/OpenVMS)

16 [http://h71000.www7.hp.com/commercial/ada/ada_index.html](http://h71000.www7.hp.com/commercial/ada/ada_index.html)

convention  you  like.  The  purpose  of  ACS  Load  is  the  creation  of  the  dependency  tree  between  the  source  files.

Next  you  compile  them:

![](Images/image06635.jpeg)

Note that compile take the package name and not the filename. The wildcard * means all  packages  loaded.  The  compiler  automatically  determines  the  right  order  for  the  compilation  so  a  make[17](#part0035.xhtml__bookmark147)  tool  is  not  strictly  needed.

Last  but  not  least  you  link  your  file  into  an

![](Images/image06636.jpeg)

On  large  systems  you  might  want  to  break  sources  down  into  several  libraries  —  in  which  case  you  also  need

![](Images/image06637.jpeg)

to  merge  the  content of  the  current library  with  the library  higher  up  the hierarchy.  The  larger  libraries  should  then  be  created  with:

![](Images/image06638.jpeg)

This  uses  a  different  directory  layout  more  suitable  for  large  libraries.

###### DEC  Ada  IDE

Dec  Ada  comes  without  an  IDE,  however  the  DEC  LSE[18](#part0035.xhtml__bookmark148)  as  well  as  the  Ada  Mode[19](#part0035.xhtml__bookmark149)  of  the  Vim  text  editor[20](#part0035.xhtml__bookmark150)  support  DEC  Ada.

## 3.2 Compiling  our  Demo  Source

Compiling  our  Demo  Source

Once  you  have  downloaded[21](#part0035.xhtml__bookmark151)  our  example  programs  you  might  wonder  how  to  compile  them.

![](Images/image06639.jpeg)

17 [http://en.wikipedia.org/wiki/make%20%28software%29](http://en.wikipedia.org/wiki/make%20%28software%29)

18 [http://en.wikipedia.org/wiki/Language-Sensitive_Editor](http://en.wikipedia.org/wiki/Language-Sensitive_Editor)

19 [http://www.vim.org/scripts/script.php?script_id=1609](http://www.vim.org/scripts/script.php?script_id=1609)

20 [http://en.wikipedia.org/wiki/Vim%20%28text%20editor%29](http://en.wikipedia.org/wiki/Vim%20%28text%20editor%29)

21 [https://sourceforge.net/project/showfiles.php?group_id=124904](https://sourceforge.net/project/showfiles.php?group_id=124904)

First you need to extract the sources.  Use your favorite zip tool[22](#part0036.xhtml__bookmark152)  to achieve that.  On  extraction a directory with the same name as the filename is created. Beware: WinZip might  also create a directory equaling the filename so Windows users need to be careful using the  right  option  otherwise  they  end  up  with  wikibook-ada-1_2_0.src\wikibook-ada-1_2_0.

Once you extracted the files you will find all sources in wikibook-ada-1_2_0/Source. You  could compile them right there. For your convenience we also provide ready made project  files  for  the  following  IDEs  (If  you  find  a  directory  for  an  IDEs  not  named  it  might  be  in  the  making  and  not  actually  work).

#### 3.2.1  GNAT

You will find multi-target GNAT Project files and a multi-make Makefile file in wikibook-  ada-2_0_0/GNAT.  For  i686  Linux  and  Windows  you  can  compile  any  demo  using:

![](Images/image06640.jpeg)

You can also open them inside  the GPS with

![](Images/image06641.jpeg)

For  other  target  platform  it  is  a  bit  more  difficult  since  you  need  to  tell  the  project  files  which  target  you  want  to  create.  The  following  options  can  be  used:

###### style  ("Debug",  "Release")

you  can  define  if  you  like  a  debug  or  release  version  so  you  can  compare  how  the  options  affect  size  and  speed.

###### os  ("Linux",  "OS2",  "Windows_NT",  "VMS")

choose  your  operating  system.  Since  there  is  no  Ada  2005  available  for  OS/2  don't  expect  all  examples  to  compile.

###### target  ("i686",  "x86_64",  "AXP")

choose  your  CPU  —  "i686[23](#part0036.xhtml__bookmark153)"  is  any  form  of  32bit  Intel  or  AMD  CPU,  "x86_64[24](#part0036.xhtml__bookmark154)"  is  an  64  bit  Intel  or  AMD  CPU  and  if  you  have  an  "AXP[25](#part0036.xhtml__bookmark155)"  then  you  know  it.

Remember  to  type  all  options  as  they  are  shown.  To  compile  a  debug  version  on  x86-64  Linux  you  type:

![](Images/image06642.jpeg)

![](Images/image06643.jpeg)

22 [http://en.wikipedia.org/wiki/ZIP%20%28file%20format%29](http://en.wikipedia.org/wiki/ZIP%20%28file%20format%29)

23 [http://en.wikipedia.org/wiki/x86](http://en.wikipedia.org/wiki/x86)

24 [http://en.wikipedia.org/wiki/x86-64](http://en.wikipedia.org/wiki/x86-64)

25 [http://en.wikipedia.org/wiki/DEC%20Alpha](http://en.wikipedia.org/wiki/DEC%20Alpha)

As  said  in  the  beginning  there  is  also  a  makefile  available  that  will  automatically  determine  the  target  used.  So  if  you  have  a  GNU  make  you  can  save  yourself  a  lot  of  typing  by  using:

![](Images/image06644.jpeg)

or  even  use

![](Images/image06645.jpeg)

to  make  all  examples  in  debug  and  release  in  one  go.

Each compile is stored inside its own directory which is created in the form of wikibook-ada-  2_0_0/GNAT/OS-Target-Style.  Empty  directories  are  provided  inside  the  archive.

#### 3.2.2  Rational  APEX

APEX uses the subsystem and view directory structure, so you will have to create those first  and copy the source files into the view.  After creating a view using the architecture model  of your choice, use the menu option "Compile -> Maintenance -> Import Text Files". In the  Import Text Files dialog, add "wikibook-ada-2_0_0/Source/*.ad?" to select the Ada source  files from the directory you originally extracted to. Apex uses the file extensions .1.ada for  specs and .2.ada for bodies — don't worry, the import text files command will change these  automatically.

To link an example, select its main subprogram in the directory viewer and click the link  button in the toolbar, or "Compile -> Link" from the menu. Double-click the executable to  run  it.  You  can  use  the  shift-key  modifier  to  bypass  the  link  or  run  dialog.

#### 3.2.3  ObjectAda

###### ObjectAda  command-line

The  following  describes  using  the  ObjectAda  tools  for  Windows  in  a  console  window.  Before  you  can  use  the  ObjectAda  tools  from  the  command  line,  make  sure  the  PATH

environment  variable  lists  the  directory  containing  the  ObjectAda  tools.  Something  like

![](Images/image06646.jpeg)

AminimalObjectAdaprojectcanhavejustonesource  file.              like              the                            Hello              World                            program              provided                            in

![](Images/image06647.jpeg)

To  build  an  executable  from  this  source  file,  follow  these  steps  (assuming  the  current  directory  is  a  fresh  one  and  contains  the  above  mentioned  source  file):

• Register  your  source  files:

![](Images/image06648.jpeg)

This makes your sources known to the ObjectAda tools. Have a look at the file UNIT.MAP  created by adareg in the current directory if you like seeing what is happening under the  hood.

• Compile  the  source  file:

![](Images/image06649.jpeg)

• Build  the  executable  program:

![](Images/image06650.jpeg)

Notice  that  you  specify  the  name  of  the  main  unit  as  argument  to  adabuild,  not  the  name  of  the  source  file.  In  this  case,  it  is  Hello_World_1  as  in

![](Images/image06651.jpeg)

More  information  about  the  tools  can  be  found  in  the  user  guide  Using  the  command  line  interface,  installed  with  the  ObjectAda  tools.

## 3.3 External  links

External  links

• GNAT  Online  Documentation:

• GNAT User's Guide[26](#part0038.xhtml__bookmark157)

• DEC  Ada:

• Developing  Ada  Products  on  OpenVMS[27](#part0038.xhtml__bookmark158)  (PDF)

• DEC  Ada  —  Language  Reference  Manual[28](#part0038.xhtml__bookmark159) (PDF)

• DEC  Ada  —  Run-Time  Reference[29](#part0038.xhtml__bookmark160)  (PDF)

26 [http://gcc.gnu.org/onlinedocs/gcc-4.0.1/gnat_ugn_unw/](http://gcc.gnu.org/onlinedocs/gcc-4.0.1/gnat_ugn_unw/)

27 [http://h71000.www7.hp.com/commercial/ada/ada_dap.pdf](http://h71000.www7.hp.com/commercial/ada/ada_dap.pdf)

28 [http://h71000.www7.hp.com/commercial/ada/ada_lrm.pdf](http://h71000.www7.hp.com/commercial/ada/ada_lrm.pdf)

29 [http://h71000.www7.hp.com/commercial/ada/ada_rtr.pdf](http://h71000.www7.hp.com/commercial/ada/ada_rtr.pdf)

# 4 Control  Statements

## 4.1 Conditionals

Conditionals

Conditional clauses are blocks of code that will only execute if a particular expression (the  condition)  is  true[1](#part0039.xhtml__bookmark163).

##### 4.1.1  if-else

The if-else statement is the simplest of the conditional statements.  They are also called  branches, as when the program arrives at an if statement during its execution, control will  "branch" off into one of two or more "directions".  An if-else statement is generally in the  following  form:

![](Images/image06652.jpeg)

If  the  original  condition  is  met,  then  all  the  code  within  the  first  statement  is  executed.  The optional else section specifies an alternative statement that will be executed if the  condition is false. Exact syntax will vary between programming languages, but the majority  of  programming  languages  (especially  procedural[2](#part0039.xhtml__bookmark164) and  structured[3](#part0039.xhtml__bookmark165) languages)  will  have  some  form of if-else conditional statement built-in. The if-else statement can usually be extended  to  the  following  form:

![](Images/image06653.jpeg)

![](Images/image06654.jpeg)

1 [http://en.wikipedia.org/wiki/Truth%20function](http://en.wikipedia.org/wiki/Truth%20function)

2 [http://en.wikibooks.org/wiki/Computer%20Programming%2FProcedural%20programming](http://en.wikibooks.org/wiki/Computer%20Programming%2FProcedural%20programming)

3 [http://en.wikibooks.org/wiki/Computer%20Programming%2FStructured%20programming](http://en.wikibooks.org/wiki/Computer%20Programming%2FStructured%20programming)

Only one statement in the entire block will be executed. This statement will be the first one  with  a  condition  which  evaluates  to  be  true.  The  concept  of  an  if-else-if  structure  is  easier  to  understand  with  the  aid  of  an  example:

![](Images/image06655.jpeg)

4.1.2  Optimizing  hints

When this program executes, the computer will check all conditions in order until one of  them matches its concept of truth. As soon as this occurs, the program will execute the  statement immediately following the condition and continue on, without checking any other  condition for truth. For this reason, when you are trying to optimize[4](#part0040.xhtml__bookmark166) a program, it is a  good idea to sort your if-else conditions in descending probability[5](#part0040.xhtml__bookmark167). This will ensure that in  the most common scenarios, the computer has to do less work, as it will most likely only  have to check one or two "branches" before it finds the statement which it should execute.  However, when writing programs for the first time, try not to think about this too much  lest  you  find  yourself  undertaking  premature  optimization[6](#part0040.xhtml__bookmark168).

Having  said  all  that,  you  should  be  aware  that  an  optimizing  compiler[7](#part0040.xhtml__bookmark169)  might  rearrange  your if statement at will when the statement in question is free from side effects[8](#part0040.xhtml__bookmark170). Among  other  techniques  optimizing  compilers  might  even  apply  jump  tables[9](#part0040.xhtml__bookmark171)  and  binary  searches[10](#part0040.xhtml__bookmark172).

In Ada, conditional statements with more than one conditional do not use short-circuit  evaluation by default. In order to mimic C/C++'s short-circuit evaluation, use and then  or  or  else  between  the  conditions.

![](Images/image06656.jpeg)

4 [http://en.wikipedia.org/wiki/Optimization_%2528computer_science%2529](http://en.wikipedia.org/wiki/Optimization_%2528computer_science%2529)

5 [http://en.wikibooks.org/wiki/Probability%2FIntroduction](http://en.wikibooks.org/wiki/Probability%2FIntroduction)

6 [http://en.wikipedia.org/wiki/Premature_optimization%23When_to_optimize](http://en.wikipedia.org/wiki/Premature_optimization%23When_to_optimize)

7 [http://en.wikipedia.org/wiki/Optimizing_compiler](http://en.wikipedia.org/wiki/Optimizing_compiler)

8 [http://en.wikipedia.org/wiki/Side-effect_%28computer_science%29](http://en.wikipedia.org/wiki/Side-effect_%28computer_science%29)

9 [http://en.wikipedia.org/wiki/Jump_table](http://en.wikipedia.org/wiki/Jump_table)

10 [http://en.wikipedia.org/wiki/Binary_search](http://en.wikipedia.org/wiki/Binary_search)

##### 4.1.3  case

Often  it  is  necessary  to  compare  one  specific  variable  against  several  constant  expressions.  For  this  kind  of  conditional  expression  the  case  statement  exists.  For  example:

![](Images/image06657.jpeg)

The  subtype  of  X  must  be  a  discrete  type,  i.e.  an  enumeration  or  integer  type.

In Ada, one advantage of the case statement is that the compiler will check the coverage of  the choices, that is, all the values of the subtype of variable X must be present or a default  branch  when  others  must  specify  what  to  do  in  the  remaining  cases.

## 4.2 Unconditionals

Unconditionals

Unconditionals let you change the flow of your program without a condition. You should be  careful when using unconditionals. Often they make programs difficult to understand. Read  Isn't  goto  evil?[11](#part0041.xhtml__bookmark174)  for  more  information.

##### 4.2.1  return

End  a  function  and  return  to  the  calling  procedure  or  function.  For  procedures:

![](Images/image06658.jpeg)

For  functions:

![](Images/image06659.jpeg)

11 Chapter  [4.2](#part0041.xhtml__bookmark173)  on  page  [39](#part0041.xhtml__bookmark173)

![](Images/image06660.jpeg)

##### 4.2.2  goto

Goto  transfers  control  to  the  statement  after  the  label.

![](Images/image06661.jpeg)

Isn't  goto  evil?

One often hears that goto is evil and one should avoid using goto. But it is often overlooked  that any return which is not the last statement inside a procedure or function is also an  unconditional statement — a goto in disguise. There is an important difference though: a  return is a forward only use of goto. Exceptions are also a type of goto statement; worse,  they  need  not  specify  where  they  are  going  to!

Therefore if you have functions and procedures with more than one return statement you  can just as well use goto. When it comes down to readability the following two samples are  almost  the  same:

![](Images/image06662.jpeg)

![](Images/image06663.jpeg)

Because  the  use  of  a  goto  needs  the  declaration  of  a  label,  the  goto  is  in  fact  twice  as  readable  than  the  use  of  return.  So  if  readability  is  your  concern  and  not  a  strict  "don't  use  goto"

programming  rule  then  you  should  rather  use  goto  than  multiple  returns.  Best,  of  course,  is  the  structured  approach  where  neither  goto  nor  multiple  returns  are  needed:

![](Images/image06664.jpeg)

## 4.3 Loops

Loops

Loops  allow  you  to  have  a  set  of  statements  repeated  over  and  over  again.

#### 4.3.1  Endless  Loop

The endless loop is a loop which never ends and the statements inside are repeated forever.  Never  is  meant  as  a  relative  term  here  —  if  the  computer  is  switched  off  then  even  endless  loops  will  end  very  abruptly.

![](Images/image06665.jpeg)

The  loop  name  (in  this  case,  "Endless_Loop")  is  an  optional  feature  of  Ada.  Naming  loops  is nice for readability but not strictly needed. Loop names are useful though if the program  should  jump  out  of  an  inner  loop,  see  below.

#### 4.3.2  Loop  with  condition  at  the  beginning

This loop has a condition at the beginning.  The statements are repeated as long as the  condition is met.  If the condition is not met at the very beginning then the statements  inside  the  loop  are  never  executed.

![](Images/image06666.jpeg)

#### 4.3.3  Loop  with  condition  at  the  end

This  loop  has  a  condition  at  the  end  and  the  statements  are  repeated  until  the  condition  is  met.  Since  the  check  is  at  the  end  the  statements  are  at  least  executed  once.

![](Images/image06667.jpeg)

#### 4.3.4  Loop  with  condition  in  the  middle

Sometimes you need to first make a calculation and exit the loop when a certain criterion is  met. However when the criterion is not met there is something else to be done. Hence you  need  a  loop  where  the  exit  condition  is  in  the  middle.

![](Images/image06668.jpeg)

In Ada the exit condition can be combined with any other loop statement as well. You can  also have more than one exit statement. You can also exit a named outer loop if you have  several  loops  inside  each  other.

4.3.5  for  loop

Quite  often  one  needs  a  loop  where  a  specific  variable  is  counted  from  a  given  start  value  up  or down to a specific end value. You could use the while[12](#part0044.xhtml__bookmark177) loop here — but since this is a  very  common  loop  there  is  an  easier  syntax  available.

![](Images/image06669.jpeg)

You don't have to declare both type and range as seen in the example. If you leave out the  type then the compiler will determine the type by context and leave out the range then the  loop  will  iterate  over  every  valid  value  for  the  type  given.

![](Images/image06670.jpeg)

12 Chapter  [4.3.5](#part0044.xhtml__bookmark176)  on  page  [42](#part0044.xhtml__bookmark176)

As  always  with  Ada:  when  "determine  by  context"  gives  two  or  more  possible  options  then  an error will be displayed and then you have to name the type to be used.  Ada will only do  "guess-works"  when  it  is  safe  to  do  so.

for  loop  on  arrays

Another very common situation is the need for a loop which iterates over every element of  an  array.  The  following  sample  code  shows  you  how  to  achieve  this:

![](Images/image06671.jpeg)

With  X  being  an  array.  Note:  This  syntax  is  mostly  used  on  arrays  —  hence  the  name  —  but  will  also  work  with  other  types  when  a  full  iteration  is  needed.

Unlike  other  loop  counters,  the  loop  counter  i,  in  the  for  loop  statement  the  value  cannot  be  changed.  The  following  is  illegal.

for  i  in  1  ..  10  loop

i  :=  i  +  1;

end  loop;

Also  the  declaration  of  the  loop  counter  ceases  after  the  body  of  the  loop.

###### Working  Demo

The  following  Demo  shows  how  to  iterate  over  every  element  of  an  integer  type.

![](Images/image06672.jpeg)

![](Images/image06673.jpeg)

## 4.4 See  also

See  also

#### 4.4.1  Wikibook

• Ada  Programming[13](#part0046.xhtml__bookmark179)

#### 4.4.2  Ada  Reference  Manual

• 5.3  If  Statements  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-5-3.html)  [05rm/html/RM-5-3.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-5-3.html)

• 5.4  Case  Statements  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-5-4.html)  [05rm/html/RM-5-4.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-5-4.html)

• 5.5  Loop  Statements  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-5-5.html)  [05rm/html/RM-5-5.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-5-5.html)

• 5.6 Block  Statements ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-5-6.html)  [05rm/html/RM-5-6.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-5-6.html)

• 5.7  Exit  Statements  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-5-7.html)  [05rm/html/RM-5-7.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-5-7.html)

• 5.8  Goto  Statements  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-5-8.html)  [05rm/html/RM-5-8.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-5-8.html)

• 6.5ReturnStatementsˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-6-5.html)  [standards/05rm/html/RM-6-5.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-6-5.html)

![](Images/image06674.jpeg)

13 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

# 5 Type  System

Ada's type system allows the programmer to construct powerful abstractions that represent  the  real  world,  and  to  provide  valuable  information  to  the  compiler,  so  that  the  compiler  can  find many logic or design errors before they become bugs. It is at the heart of the language,  and good Ada programmers learn to use it to great advantage. Four principles govern the  type  system:

• Strong  typing:  types are incompatible with one another, so it is not possible to mix  apples  and  oranges.  There  are,  however,  ways  to  convert  between  types.

• Static  typing:  type  checked  while  compiling,  this  allows  type  errors  to  be  found  earlier.

• Abstraction:  types  represent  the  real  world  or  the  problem  at  hand;  not  how  the  computer represents the data internally. There are ways to specify exactly how a type  must  be  represented  at  the  bit  level,  but  we  will  defer  that  discussion  to  another  chapter.

• Name  equivalence,  as  opposed  to  structural  equivalence  used  in  most  other  languages.  Two  types  are  compatible  if  and  only  if  they  have  the  same  name;  not  if  they  just  happen  to  have  the  same  size  or  bit  representation.  You  can  thus  declare  two  integer  types  with  the same ranges that are totally incompatible, or two record types with exactly the same  components,  but  which  are  incompatible.

Types  are  incompatible  with  one  another.  However,  each  type  can  have  any  number  of

subtypes,  which  are  compatible  with  one  another,  and  with  their  base  type.

## 5.1 Predefined types

Predefined  types

There are several predefined types,  but most programmers prefer to define their own,  application-specific types. Nevertheless, these predefined types are very useful as interfaces  between libraries developed independently.  The predefined library, obviously, uses these  types  too.

These  types  are  predefined  in  the  Standard  package:

###### Integer

This  type  covers  at  least  the  range  −215  +1  ..  +215  −  1  (RM  3.5.4  (21)  ˆ{[http://www.adaic.](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-5-4.html)  [org/resources/add_content/standards/05rm/html/RM-3-5-4.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-5-4.html) ). The Standard  also  defines  Natural  and  Positive  subtypes  of  this  type.

###### Float

There  is  only  a  very  weak  implementation  requirement  on  this  type  (RM  3.5.7  (14)  ˆ{[http:](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-5-7.html)

[//www.adaic.org/resources/add_content/standards/05rm/html/RM-3-5-7.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-5-7.html)   );

most  of  the  time  you  would  define  your  own  floating-point  types,  and  specify  your  precision  and  range  requirements.

###### Duration

A  fixed  point  type[1](#part0048.xhtml__bookmark182)  used for timing. It represents a period of time in sec-  onds  (RM  A.1  (43)  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-1.html)  [05rm/html/RM-A-1.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-1.html) ).

###### Character

A special form of Enumerations[2](#part0048.xhtml__bookmark183). There are three predefined kinds of character types:  8-bit  characters  (called  Character),  16-bit  characters  (called  Wide_Character),  and  32-bit  characters (Wide_Wide_Character). Character has been present since the first version of  the language (Ada 83[3](#part0048.xhtml__bookmark184)), Wide_Character was added in Ada 95[4](#part0048.xhtml__bookmark185), while the type Wide_-  Wide_Character  is  available  with  Ada  2005[5](#part0048.xhtml__bookmark186).

###### String[6](#part0048.xhtml__bookmark187)

Three  indefinite  array  types[7](#part0048.xhtml__bookmark188),  of  Character,  Wide_Character,  and  Wide_Wide_Character  respectively. The standard library contains packages for handling strings in three variants:  fixed  length  (Ada  ),  with  varying  length  below  a  certain  upper  bound  (Ada  ),  and  unbounded  length  (Ada  ).  Each  of  these  packages  has  a  Wide_and  a  Wide_Wide_variant.

###### Boolean

A  Boolean  in  Ada  is  an  Enumeration[8](#part0048.xhtml__bookmark189)  of  False  and  True  with  special  semantics.

Packages System  and System  predefine some types which are primarily useful for low-level  programming  and  interfacing  to  hardware.

###### System.Address

An  address  in  memory.

###### System.Storage_Elements.Storage_Offset

An offset,  which can be added to an address to obtain a new address.  You can also  subtract one address from another to get the offset between them.  Together, Address,  Storage_Offset  and  their  associated  subprograms  provide  for  address  arithmetic.

###### System.Storage_Elements.Storage_Count

A  subtype  of  Storage_Offset  which  cannot  be  negative,  and  represents  the  memory  size  of  a  data  structure  (similar  to  C's  size_t).

###### System.Storage_Elements.Storage_Element

![](Images/image06675.jpeg)

1 Chapter  [10](#part0081.xhtml__bookmark278)  on  page  [79](#part0081.xhtml__bookmark278)

2 Chapter  [8](#part0075.xhtml__bookmark251)  on  page  [73](#part0075.xhtml__bookmark251)

3 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAda%2083](http://en.wikibooks.org/wiki/Ada%20Programming%2FAda%2083)

4 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAda%2095](http://en.wikibooks.org/wiki/Ada%20Programming%2FAda%2095)

5 Chapter  [23](#part0221.xhtml__bookmark541)  on  page  [219](#part0221.xhtml__bookmark541)

6 Chapter  [15](#part0121.xhtml__bookmark373)  on  page  [119](#part0121.xhtml__bookmark373)

7 Chapter  [11](#part0085.xhtml__bookmark293)  on  page  [83](#part0085.xhtml__bookmark293)

8 Chapter  [8](#part0075.xhtml__bookmark251)  on  page  [73](#part0075.xhtml__bookmark251)

In  most  computers,  this  is  a  byte.  Formally,  it  is  the  smallest  unit  of  memory  that  has  an  address.

###### System.Storage_Elements.Storage_Array

An  array  of  Storage_Elements  without  any  meaning,  useful  when  doing  raw  memory  access.

## 5.2 The  Type  Hierarchy

The  Type  Hierarchy

![](Images/image06676.jpeg)Types are organized hierarchically. A type inherits properties from types above it in the  hierarchy. For example, all scalar types (integer, enumeration, modular, fixed-point and  floating-point  types)  have  operators[9](#part0049.xhtml__bookmark191)  "<",  ">"  and  arithmetic  operators  defined  for  them,  and  all  discrete  types  can  serve  as  array  indexes.

Figure 1Ada  type  hierarchy

![](Images/image06677.jpeg)

9Chapter  [37](#part0303.xhtml__bookmark820)  on  page  [301](#part0303.xhtml__bookmark820)

Here is a broad overview of each category of types; please follow the links for detailed  explanations. Inside parenthesis there are equivalences in C and Pascal for readers familiar  with  those  languages.

###### Signed  Integers[10](#part0050.xhtml__bookmark192) (int,  INTEGER)

Signed  Integers  are  defined  via  the  range[11](#part0050.xhtml__bookmark193)  of  values  needed.

###### Unsigned  Integers[12](#part0050.xhtml__bookmark194) (unsigned,  CARDINAL)

Unsigned  Integers  are  called  Modular  Types[13](#part0050.xhtml__bookmark195).  Apart  from  being  unsigned  they  also  have  wrap-around  functionality.

Enumerations[14](#part0050.xhtml__bookmark196) (enum,  char,  bool,  BOOLEAN)  Ada Enumeration[15](#part0050.xhtml__bookmark197) types are a separate type family.  Floating  point[16](#part0050.xhtml__bookmark198) (float,  double,  REAL)

Floating  point  types  are  defined  by  the  digits[17](#part0050.xhtml__bookmark199)  needed,  the  relative  error  bound.

###### Ordinary  and  Decimal  Fixed  Point[18](#part0050.xhtml__bookmark200) (DECIMAL)

Fixed  point  types  are  defined  by  their  delta[19](#part0050.xhtml__bookmark201),  the  absolute  error  bound.

###### Arrays[20](#part0050.xhtml__bookmark202) (  [  ],  ARRAY  [  ]  OF,  STRING  )

Arrays  with  both  compile-time  and  run-time  determined  size  are  supported.

###### Record[21](#part0050.xhtml__bookmark203) (struct,  class,  RECORD  OF)

A  record  is  a  composite  type[22](#part0050.xhtml__bookmark204)  that  groups  one  or  more  fields.

###### Access[23](#part0050.xhtml__bookmark205) (*,  ˆ,  POINTER  TO)

Ada's  Access[24](#part0050.xhtml__bookmark206)  types  may  be  more  than  just  a  simple  memory  address.

Task & Protected[25](#part0050.xhtml__bookmark207) (no equivalence in C or Pascal)  Task and Protected types allow the control of concurrency  Interfaces[26](#part0050.xhtml__bookmark208) (no  equivalence  in  C  or  Pascal)

![](Images/image06678.jpeg)

10 Chapter  [6](#part0071.xhtml__bookmark237)  on  page  [69](#part0071.xhtml__bookmark237)

11 Chapter  [6](#part0071.xhtml__bookmark237)  on  page  [69](#part0071.xhtml__bookmark237)

12 Chapter  [7](#part0073.xhtml__bookmark245)  on  page  [71](#part0073.xhtml__bookmark245)

13 Chapter  [7](#part0073.xhtml__bookmark245)  on  page  [71](#part0073.xhtml__bookmark245)

14 Chapter  [8](#part0075.xhtml__bookmark251)  on  page  [73](#part0075.xhtml__bookmark251)

15 Chapter  [8](#part0075.xhtml__bookmark251)  on  page  [73](#part0075.xhtml__bookmark251)

16 Chapter  [9](#part0079.xhtml__bookmark266)  on  page  [77](#part0079.xhtml__bookmark266)

17 Chapter  [9](#part0079.xhtml__bookmark266)  on  page  [77](#part0079.xhtml__bookmark266)

18 Chapter  [10](#part0081.xhtml__bookmark278)  on  page  [79](#part0081.xhtml__bookmark278)

19 Chapter  [10](#part0081.xhtml__bookmark278)  on  page  [79](#part0081.xhtml__bookmark278)

20 Chapter  [11](#part0085.xhtml__bookmark293)  on  page  [83](#part0085.xhtml__bookmark293)

21 Chapter  [12](#part0093.xhtml__bookmark318)  on  page  [91](#part0093.xhtml__bookmark318)

22 [http://en.wikibooks.org/wiki/Ada%20Programming%2FTypes%23List%20of%20types](http://en.wikibooks.org/wiki/Ada%20Programming%2FTypes%23List%20of%20types)

23 Chapter  [13](#part0101.xhtml__bookmark346)  on  page  [99](#part0101.xhtml__bookmark346)

24 Chapter  [13](#part0101.xhtml__bookmark346)  on  page  [99](#part0101.xhtml__bookmark346)

25 Chapter  [21](#part0175.xhtml__bookmark499)  on  page  [173](#part0175.xhtml__bookmark499)

26 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Finterface](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Finterface)

New  in  Ada  2005,  these  types  are  similar  to  the  Java  interfaces.

5.2.1  Classification  of  Types

The  types  of  this  hierarchy  can  be  classified  as  follows.

###### Specific  vs.  Class-wide

![](Images/image06679.jpeg)

Operations  of  specific  types  are  non-dispatching,  those  on  class-wide  types  are  dispatching.

New  types  can  be  declared  by  deriving  from  specific  types;  primitive  operations  are  inherited

by  derivation.  You  cannot  derive  from  class-wide  types.

###### Constrained  vs.  Unconstrained

![](Images/image06680.jpeg)

By  giving  a  constraint  to  an  unconstrained  subtype,  a  subtype  or  object  becomes  constrained:

![](Images/image06681.jpeg)

Declaring an unconstrained object is only possible if a default value is given in the type  declaration above. The language does not specify how such objects are allocated. GNAT  allocates  the  maximum  size,  so  that  size  changes  that  might  occur  with  discriminant  changes  present no problem. Another possibility is implicit dynamic allocation on the heap and  deallocation  followed  be  a  re-allocation  when  the  size  changes.

###### Definite  vs.  Indefinite

![](Images/image06682.jpeg)

![](Images/image06683.jpeg)

Definite subtypes allow the declaration of objects without initial value, since objects of  definite subtypes have constraints that are known at creation-time. Object declarations of  indefinite  subtypes need  an initial  value to  supply  a constraint; they are  then constrained  by

the  constraint  delivered  by  the  initial  value.

![](Images/image06684.jpeg)

###### Unconstrained  vs.  Indefinite

Note that unconstrained subtypes are not necessarily indefinite as can be seen above with  RD:  it  is  a  definite  unconstrained  subtype.

## 5.3 Concurrency  Types

Concurrency  Types

The Ada language uses types for one more purpose in addition to classifying data + operations.  The type system integrates concurrency (threading,  parallelism).  Programmers will use  types  for  expressing  the  concurrent  threads  of  control  of  their  programs.

The  core  pieces  of  this  part  of  the  type  system,  the  task  types  and  the  protected  types  are  explained  in  greater  depth  in  a  section  on  tasking[27](#part0052.xhtml__bookmark212).

## 5.4 Limited  Types

Limited  Types

Limiting a type means disallowing assignment.  The “concurrency types” described above  are  always  limited.  Programmers  can  define  their  own  types  to  be  limited,  too,  like  this:

![](Images/image06685.jpeg)

(The ellipsis stands for private, or for a record definition, see the corresponding subsection  on this page.) A limited type also doesn't have an equality operator unless the programmer  defines  one.

You  can  learn  more  in  the  limited  types[28](#part0052.xhtml__bookmark213)  chapter.

## 5.5 Defining  new  types  and  subtypes

![](Images/image06686.jpeg)

27 Chapter  [21](#part0175.xhtml__bookmark499)  on  page  [173](#part0175.xhtml__bookmark499)

28 Chapter  [14](#part0115.xhtml__bookmark366)  on  page  [113](#part0115.xhtml__bookmark366)

Defining  new  types  and  subtypes

You  can  define  a  new  type  with  the  following  syntax:

![](Images/image06687.jpeg)

followed  by  the  description  of  the  type,  as  explained  in  detail  in  each  category  of  type.

Formally, the above declaration creates a type and its first subtype named T. The type itself,  correctly called the "type of T", is anonymous; the RM refers to it as T (in italics), but often  speaks  sloppily  about  the  type  T.  But  this  is  an  academic  consideration;  for  most  purposes,  it  is  sufficient  to  think  of  T  as  a  type.  For  scalar  types,  there  is  also  a  base  type  called  T'Base,  which  encompasses  all  values  of  T.

For  signed  integer  types,  the  type  of  T  comprises  the  (complete)  set  of  mathematical  integers.  The base type is a certain hardware type, symmetric around zero (except for possibly one  extra  negative  value),  encompassing  all  values  of  T.

As  explained  above,  all  types  are  incompatible;  thus:

![](Images/image06688.jpeg)

is illegal, because Integer_1 and Integer_2 are different and incompatible types.  It is this  feature  which  allows  the  compiler  to  detect  logic  errors  at  compile  time,  such  as  adding  a  file descriptor to a number of bytes, or a length to a weight.  The fact that the two types  have the same range does not make them compatible:  this is name  equivalence in action,  as opposed to structural equivalence.  (Below, we will see how you can convert between  incompatible  types;  there  are  strict  rules  for  this.)

#### 5.5.1  Creating  subtypes

You  can  also  create  new  subtypes  of  a  given  type,  which  will  be  compatible  with  each  other,  like  this:

![](Images/image06689.jpeg)

The  declaration  of  Integer_2  is  bad  because  the  constraint  7  ..11 is not compatible  with  Integer_1;  it  raises  Contraint_Error  at  subtype  elaboration  time.

Integer_1  and  Integer_3  are  compatible  because  they  are  both  subtypes  of  the  same  type,  namely  Integer_1'Base.

It is not necessary that the subtype ranges overlap, or be included in one another. The  compiler inserts a run-time range check when you assign A to B; if the value of A, at that  point,  happens  to  be  outside  the  range  of  Integer_3,  the  program  raises  Constraint_Error.

There  are  a  few  predefined  subtypes  which  are  very  useful:

![](Images/image06690.jpeg)

#### 5.5.2  Derived  types

A  derived  type  is  a  new,  full-blown  type  created  from  an  existing  one.  Like  any  other  type,  it is incompatible with its parent; however, it inherits the primitive operations defined for  the  parent  type.

![](Images/image06691.jpeg)

Here both types are discrete; it is mandatory that the range of the derived type be included  in the range of its parent. Contrast this with subtypes. The reason is that the derived type  inherits the primitive operations defined for its parent, and these operations assume the  range  of  the  parent  type.  Here  is  an  illustration  of  this  feature:

![](Images/image06692.jpeg)

When we call P  (B), the parameter B is converted to Integer_1; this conversion of course  passes  since  the  set  of  acceptable  values  for  the  derived  type  (here,  8  ..  10)  must  be  included  in  that  of  the  parent  type  (1  ..  10).  Then  P  is  called  with  the  converted  parameter.

Consider  however  a  variant  of  the  example  above:

![](Images/image06693.jpeg)

When P (B, Y) is called, both parameters are converted to Integer_1.  Thus the range  check  on  J  (7)  in  the  body  of  P  will  pass.  However  on  return  parameter  Y  is  converted  back  to  Integer_2  and  the  range  check  on  Y  will  of  course  fail.

With  the  above  in  mind,  you  will  see  why  in  the  following  program  Constraint_Error  will  be  called  at  run  time.

![](Images/image06694.jpeg)

## 5.6 Subtype  categories

Subtype  categories

Ada  supports  various  categories  of  subtypes  which  have  different  abilities.  Here  is  an  overview  in  alphabetical  order.

#### 5.6.1  Anonymous  subtype

A  subtype  which  does  not  have  a  name  assigned  to  it.  Such  a  subtype  is  created  with  a  variable  declaration:

![](Images/image06695.jpeg)

Here,  (1  ..  10)  is  the  constraint.  This  variable  declaration  is  equivalent  to:

![](Images/image06696.jpeg)

#### 5.6.2  Base  type

In Ada, all types are anonymous[29](#part0056.xhtml__bookmark215) and only subtypes may be named[30](#part0056.xhtml__bookmark216).  For scalar types,  there is a special subtype of the anonymous type, called the base type, which is nameable  with the 'Base attribute.  The base type comprises all values of the first subtype.  Some  examples:

![](Images/image06697.jpeg)

The  base  type  Int'Base  is  a  hardware  type  selected  by  the  compiler  that  comprises  the  values  of  Int.  Thus  it  may  have  the  range  -27  ..  27-1  or  -215  ..  215-1  or  any  other  such  type.

![](Images/image06698.jpeg)

Enum'Base  is  the  same  as  Enum,  but  Short'Base  also  holds  the  literal  D.

![](Images/image06699.jpeg)

29 Chapter  [5.11.1](#part0069.xhtml__bookmark234)  on  page  [67](#part0069.xhtml__bookmark234)

30 Chapter  [5.6.6](#part0058.xhtml__bookmark222)  on  page  [56](#part0058.xhtml__bookmark222)

#### 5.6.3  Constrained  subtype

A  subtype  of  an  indefinite  subtype[31](#part0057.xhtml__bookmark217)  that  adds  constraints.  The  following  example  defines  a  10  character  string  sub-type.

![](Images/image06700.jpeg)

You  cannot  partially  constrain  an  unconstrained  subtype:

![](Images/image06701.jpeg)

Constraints  for  all  indices  must  be  given,  the  result  is  necessarily  a  definite  subtype[32](#part0057.xhtml__bookmark218).

#### 5.6.4  Definite  subtype

A definite subtype[33](#part0057.xhtml__bookmark219) is a subtype whose size is known at compile-time. All subtypes which  are  not  indefinite  subtypes[34](#part0057.xhtml__bookmark220)  are,  by  definition,  definite  subtypes[35](#part0057.xhtml__bookmark221).

Objects  of  definite  subtypes  may  be  declared  without  additional  constraints.

#### 5.6.5  Indefinite  subtype

An  indefinite  subtype  is  a  subtype  whose  size  is  not  known  at  compile-time  but  is  dynamically calculated at run-time. An indefinite subtype does not by itself provide enough  information to create an object; an additional constraint or explicit initialization expression  is  necessary  in  order  to  calculate  the  actual  size  and  therefore  create  the  object.

![](Images/image06702.jpeg)

X  is  an  object  of  the  indefinite  (sub)type  String.  Its  constraint  is  derived  implicitly  from  its  initial  value.  X  may  change  its  value,  but  not  its  bounds.

It  should  be  noted  that  it  is  not  necessary  to  initialize  the  object  from  a  literal.  You  can  also  use  a  function.  For  example:

![](Images/image06703.jpeg)

31 [http://en.wikibooks.org/wiki/ada%20Programming%2FSubtypes%23indefinite_subtype](http://en.wikibooks.org/wiki/ada%20Programming%2FSubtypes%23indefinite_subtype)

32 [http://en.wikibooks.org/wiki/ada%20Programming%2FSubtypes%23definite_subtype](http://en.wikibooks.org/wiki/ada%20Programming%2FSubtypes%23definite_subtype)

33 [http://en.wikibooks.org/wiki/ada%20Programming%2FSubtypes%23definite_subtype](http://en.wikibooks.org/wiki/ada%20Programming%2FSubtypes%23definite_subtype)

34 [http://en.wikibooks.org/wiki/ada%20Programming%2FSubtypes%23indefinite_subtype](http://en.wikibooks.org/wiki/ada%20Programming%2FSubtypes%23indefinite_subtype)

35 [http://en.wikibooks.org/wiki/ada%20Programming%2FSubtypes%23definite_subtype](http://en.wikibooks.org/wiki/ada%20Programming%2FSubtypes%23definite_subtype)

![](Images/image06704.jpeg)

This  statement  reads  the  first  command-line  argument  and  assigns  it  to  X.

#### 5.6.6  Named  subtype

A  subtype which has a name assigned to it. “First subtypes” are created with  the  keyword  type  (remember  that  types  are  always  anonymous,  the  name  in  a  type  declaration  is  the  name  of  the  first  subtype),  others  with  the  keyword  subtype.  For  example:

![](Images/image06705.jpeg)

Count_to_Ten  is  the  first  subtype  of  a  suitable  integer  base  type.  However,  if  you  would  like  to  use  this  as  an  index  constraint  on  String,  the  following  declaration  is  illegal:

![](Images/image06706.jpeg)

This is because String has  Positive as index,  which is a subtype  of Integer (these declarations  are  taken  from  package  Standard):

![](Images/image06707.jpeg)

So  you  have  to  use  the  following  declarations:

![](Images/image06708.jpeg)

Now Ten_Characters is the name of that subtype of String which is constrained to Count_-  To_Ten.  You  see  that  posing  constraints  on  types  versus  subtypes  has  very  different  effects.

#### 5.6.7  Unconstrained  subtype

A subtype of an indefinite subtype that does not add a constraint only introduces a new  name  for  the  original  subtype.

![](Images/image06709.jpeg)

My_String  and  String  are  interchangeable.

## 5.7 Qualified expressions

Qualified  expressions

In  most  cases,  the  compiler  is  able  to  infer  the  type  of  an  expression;  for  example:

![](Images/image06710.jpeg)

Here  the  compiler  knows  that  A  is  a  value  of  the  type  Enum.  But  consider:

![](Images/image06711.jpeg)

The compiler  cannot  choose between the two  versions of P; both  would be equally valid.  To  remove  the  ambiguity,  you  use  a  qualified  expression:

![](Images/image06712.jpeg)

As seen in the following example, this syntax is often used when creating new objects.  If  you try to compile the example, it will fail with a compilation error since the compiler will  determine  that  256  is  not  in  range  of  Byte.

![](Images/image06713.jpeg)

## 5.8 Type  conversions

Type  conversions

Data do not always come in the format you need them. You must, then, face the task of  converting them.  As a true multi-purpose language with a special emphasis on "mission  critical", "system programming" and "safety", Ada has several conversion techniques. The  most difficult part is choosing the right one, so the following list is sorted in order of utility.  You  should  try  the  first  one  first;  the  last  technique  is  a  last  resort,  to  be  used  if  all  others  fail.  There are also a few related techniques that you might choose instead of actually  converting  the  data.

Since the most important aspect is not the result of a successful conversion, but how the  system  will  react  to an  invalid conversion,  all  examples  also  demonstrate  faulty  conversions.

#### 5.8.1  Explicit  type  conversion

An  explicit type conversion looks much like a function call; it does not use the tick

(apostrophe,  ')  like  the  qualified  expression  does.

![](Images/image06714.jpeg)

The  compiler  first  checks  that  the  conversion  is  legal,  and  if  it  is,  it  inserts  a  run-time  check at the point of the conversion; hence the name checked conversion. If the conversion  fails, the program raises Constraint_Error.  Most compilers are very smart and optimise  away the constraint checks; so, you need not worry about any performance penalty. Some  compilers can also warn that a constraint check will always fail (and optimise the check with  an  unconditional  raise).

Explicit  type  conversions  are  legal:

• between  any  two  numeric  types

• between  any two  subtypes of  the same  type

• between  any  two  types  derived  from  the  same  type  (note  special  rules  for  tagged  types)

• between  array  types  under  certain  conditions  (see  RM  4.6(24.2/2..24.7/2))

• and  nowhere  else

(The  rules  become  more  complex  with  class-wide  and  anonymous  access  types.)

![](Images/image06715.jpeg)

This  example  illustrates  explicit  type  conversions:

![](Images/image06716.jpeg)

![](Images/image06717.jpeg)

Explicit conversions are possible between any two numeric types: integers, fixed-point and  floating-point  types.  If  one  of  the  types  involved  is  a  fixed-point  or  floating-point  type,  the compiler not only checks for the range constraints (thus the code above will raise  Constraint_Error),  but  also  performs  any  loss  of  precision  necessary.

Example 1: the loss of precision causes the procedure to only ever print "0" or "1", since P /  100  is  an  integer  and  is  always  zero  or  one.

![](Images/image06718.jpeg)

Example  2:  we  use  an  intermediate  floating-point  type  to  guarantee  the  precision.

![](Images/image06719.jpeg)

You  might  ask  why  you  should  convert  between  two  subtypes  of  the  same  type.  An  example  will  illustrate  this.

![](Images/image06720.jpeg)

Here,  Slice has  bounds  1  and  10,  whereas  X  (11  ..20)  has  bounds  11  and  20.

#### 5.8.2  Change  of  Representation

Type  conversions  can  be  used  for  packing  and  unpacking  of  records  or  arrays.

![](Images/image06721.jpeg)

![](Images/image06722.jpeg)

#### 5.8.3  Checked  conversion  for  non-numeric  types

The examples above all revolved around conversions between numeric types; it is possible to  convert between any two numeric types in this way. But what happens between non-numeric  types,  e.g.  between  array  types  or  record  types?  The  answer  is  two-fold:

• you can convert explicitly between a type and types derived from it, or between types  derived  from  the  same  type,

• and  that's  all.  No  other  conversions  are  possible.

Why  would  you  want  to  derive  a  record  type  from  another  record  type?  Because  of  representation  clauses.  Here  we  enter  the  realm  of  low-level  systems  programming,  which  is  not  for  the  faint  of  heart,  nor  is  it  useful  for  desktop  applications.  So  hold  on  tight,  and  let's  dive  in.

Suppose you have a record type which uses the default, efficient representation. Now you  want to write this record to a device, which uses a special record format.  This special  representation is more compact (uses fewer bits), but is grossly inefficient.  You want to  have  a  layered  programming  interface:  the  upper  layer,  intended  for  applications,  uses  the efficient representation. The lower layer is a device driver that accesses the hardware  directly  and  uses  the  inefficient  representation.

![](Images/image06723.jpeg)

The  compiler  chooses  a  default,  efficient  representation  for  Register.  For  example,  on  a  32-bit  machine,  it  would  probably  use  three  32-bit  words,  one  for  A,  one  for  B  and  one  for  Size.  This  efficient  representation  is  good  for  applications,  but  at  one  point  we  want  to  convert  the  entire  record  to  just  8  bits,  because  that's  what  our  hardware  requires.

![](Images/image06724.jpeg)

In the above example, the package body declares a derived type with the inefficient, but  compact  representation,  and  converts  to  and  from  it.

This  illustrates  that  type  conversions  can  result  in  a  change  of  representation.

#### 5.8.4  View  conversion,  in  object-oriented  programming

Within object-oriented programming[36](#part0063.xhtml__bookmark225) you have to distinguish between specific types and  class-wide  types.

With specific types, only conversions to ancestors are possible and, of course, are checked.  During the conversion, you do not "drop" any components that are present in the derived  type and not in the parent type; these components are still present, you just don't see them  anymore.  This  is  called  a  view  conversion.

![](Images/image06725.jpeg)

36 Chapter  [22](#part0189.xhtml__bookmark519)  on  page  [187](#part0189.xhtml__bookmark519)

There  are  no  conversions  to  derived  types  (where  would  you  get  the  further  components  from?);

extension  aggregates  have  to  be  used  instead.

![](Images/image06726.jpeg)

Since,  in  object-oriented  programming,  an  object  of  child  type  is  an  object  of  the  parent  type,  no  run-time  check  is  necessary.

With  class-wide  types,  conversions  to  ancestor  and  child  types  are  possible  and  are  checked  as  well.  These  conversions  are  also  view  conversions,  no  data  is  created  or  lost.

![](Images/image06727.jpeg)

This view conversion involves a run-time check to see if Parent_View is indeed a view of an  object of type Child_Type. In the second case, the run-time check accepts objects of type  Child_Type  but  also  any  type  derived  from  Child_Type.

###### View  renaming

A  renaming  declaration  does  not  create  any  new  object  and  performs  no  conversion;  it  only gives a new name to something that already exists. Performance is optimal since the  renaming is completely done at compile time. We mention it here because it is a common  idiom  in  object  oriented  programming[37](#part0064.xhtml__bookmark226)  to  rename  the  result  of  a  view  conversion.

![](Images/image06728.jpeg)

Now, Parent_View is not a new object, but another name for Child_Instance viewed as  the  parent,  i.e.  only  the  parent  components  are  visible,  the  further  child  components  are  hidden.

![](Images/image06729.jpeg)

37 Chapter  [22](#part0189.xhtml__bookmark519)  on  page  [187](#part0189.xhtml__bookmark519)

#### 5.8.5  Address  conversion

Ada's access type[38](#part0065.xhtml__bookmark227) is not just a memory location (a thin pointer).  Depending on imple-  mentation and the access type[39](#part0065.xhtml__bookmark228) used, the access[40](#part0065.xhtml__bookmark229) might keep additional information (a fat  pointer). For example GNAT keeps two memory addresses for each access[41](#part0065.xhtml__bookmark230) to an indefinite  object  —  one  for  the  data  and  one  for  the  constraint  informations  (Size,  First,  Last).

If you want to convert an access to a simple memory location you can use the package  System  .  Note  however  that  an  address  and  a  fat  pointer  cannot  be  converted  reversibly  into  one  another.

The address of an array object is the address of its first component.  Thus the bounds get  lost  in  such  a  conversion.

![](Images/image06730.jpeg)

#### 5.8.6  Unchecked  conversion

One of the great criticisms of Pascal was "there is no escape".  The reason was that  sometimes you have to convert the incompatible. For this purpose, Ada has the generic  function  Unchecked_Conversion:

![](Images/image06731.jpeg)

Unchecked_Conversion will bit-copy the source data and reinterprete them under the target  type without any checks. It is your chore to make sure that the requirements on unchecked  conversion  as  stated  in  RM  13.9  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-13-9.html)  [standards/05rm/html/RM-13-9.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-13-9.html)  are  fulfilled;  if  not,  the  result  is  implementation  dependent  and  may  even  lead  to  abnormal  data.  Use  the  'Valid  attribute  after  the  conversion  to  check  the  validity  of  the  data  in  problematic  cases.

A function call to (an instance of) Unchecked_Conversion will copy the source to the  destination.  The compiler may also do a conversion in place (every instance has the  convention  Intrinsic).

To  use  Unchecked_Conversion  you  need  to  instantiate  the  generic.

![](Images/image06732.jpeg)

38 Chapter  [13](#part0101.xhtml__bookmark346)  on  page  [99](#part0101.xhtml__bookmark346)

39 Chapter  [13](#part0101.xhtml__bookmark346)  on  page  [99](#part0101.xhtml__bookmark346)

40 Chapter  [13](#part0101.xhtml__bookmark346)  on  page  [99](#part0101.xhtml__bookmark346)

41 Chapter  [13](#part0101.xhtml__bookmark346)  on  page  [99](#part0101.xhtml__bookmark346)

In  the  example  below,  you  can  see  how  this  is  done.  When  run,  the  example  will  output  "A

=  -1,  B  =  255".  No  error  will  be  reported,  but  is  this  the  result  you  expect?

![](Images/image06733.jpeg)

There is of course a range check in the assignment B := Convert (A);. Thus if B were  defined  as  B:  Byte  range  0  ..  10;,  Constraint_Error  would  be  raised.

#### 5.8.7  Overlays

If the copying of the result of Unchecked_Conversion is too much waste in terms of  performance, then you can try overlays, i.e. address mappings. By using overlays, both  objects share the same memory location. If you assign a value to one, the other changes as  well.  The  syntax  is:

![](Images/image06734.jpeg)

where  expression  defines  the  address  of  the  source  object.

While  overlays  might  look  more  elegant  than  Unchecked_Conversion,  you  should  be  aware  that  they  are  even  more  dangerous  and  have  even  greater  potential  for  doing  something  very

wrong. For example if Source'Size  <  Target'Size and you assign a value to Target, you  might  inadvertently  write  into  memory  allocated  to  a  different  object.

You have to take care also of implicit initializations of objects of the target type, since they  would overwrite the actual value of the source object. The Import pragma with convention  Ada  can  be  used  to  prevent  this,  since  it  avoids  the  implicit  initialization,  RM  B.1  ˆ{[http:](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-B-1.html)

[//www.adaic.org/resources/add_content/standards/05rm/html/RM-B-1.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-B-1.html) .  The  example  below  does  the  same  as  the  example  from  "Unchecked  Conversion".

![](Images/image06735.jpeg)

#### 5.8.8  Export  /  Import

Just for the record: There is still another method using the pragma  and pragma  pragmas.  However, since this method completely undermines Ada's visibility and type concepts even  more  than  overlays,  it  has  no  place  here  in  this  language  introduction  and  is  left  to  experts.

## 5.9 Elaborated  Discussion  of  Types  for  Signed  Integer  Types

Elaborated  Discussion  of  Types  for  Signed  Integer  Types  As  explained  before,  a  type  declaration

![](Images/image06736.jpeg)

declares an anonymous type T and its first subtype T (please note the italicization).  T  encompasses the complete set of mathematical integers.  Static expressions and named  numbers  make  use  of  this  fact.

All numeric integer literals are of type Universal_Integer.  They are converted to the  appropriate  specific  type  where  needed.  Universal_Integer  itself  has  no  operators.

Some  examples  with  static  named  numbers:

![](Images/image06737.jpeg)

Static expressions are evaluated at compile-time on the appropriate types with no overflow  checks,  i.e.  mathematically exact (only limited by computer store).  The result is then  implicitly  converted  to  Universal_Integer.

The  literal  1  in  S2  is  of  type  Universal_Integer  and  implicitly  converted  to  Long_Integer.

S3 implicitly converts the summands to root_integer, performs the calculation and converts  back  to  Universal_Integer.

S4  is  illegal  because  it  mixes  two  different  types.  You  can  however  write  this  as

![](Images/image06738.jpeg)

where the Pos attributes convert the values to Universal_Integer, which are then further  implicitly converted to root_integer, added and the result converted back to Universal_-  Integer.

root_integer is the anonymous greatest integer type representable by the hardware. It has  the range System.Min_Integer ..  System.Max_Integer.  All integer types are rooted  at root_integer,  i.e.  derived from  it.  Universal_Integer can be  viewed  as  root_-  integer'Class.

During run-time, computations of course are performed with range checks and overflow  checks on the appropriate subtype. Intermediate results may however exceed the range  limits.  Thus  with  I,  J,  K  of  the  subtype  T  above,  the  following  code  will  return  the  correct  result:

![](Images/image06739.jpeg)

Real literals are of type Universal_Real, and similar rules as the ones above apply accord-  ingly.

## 5.10 Relations  between  types

Relations  between  types

Types  can  be  made  from  other  types.  Array  types,  for  example,  are  made  from  two  types,  one for the arrays' index and one for the arrays' components.  An array, then, expresses an as-  sociation,  namely  that  between  one  value  of  the  index  type  and  a  value  of  the  component  type.

![](Images/image06740.jpeg)

The  type  Color  is  the  index  type  and  the  type  Intensity  is  the  component  type  of  the  array  type  Colored_Point.  See  array[42](#part0069.xhtml__bookmark235).

## 5.11 See  also

See  also

#### 5.11.1 Wikibook

• Ada  Programming[43](#part0069.xhtml__bookmark236)

#### 5.11.2 Ada  Reference  Manual

• 3.2.1TypeDeclarationsˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-2-1.html)  [standards/05rm/html/RM-3-2-1.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-2-1.html)

• 3.3  Objects  and  Named  Numbers  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-3.html)  [standards/05rm/html/RM-3-3.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-3.html)

• 3.7Discriminantsˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-7.html)  [05rm/html/RM-3-7.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-7.html)

• 3.10  Access  Types  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-10.html)  [05rm/html/RM-3-10.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-10.html)

• 4.9  Static  Expressions  and  Static  Subtypes  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-9.html)  [content/standards/05rm/html/RM-4-9.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-9.html)

• 13.9  Unchecked  Type  Conversions  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-13-9.html)  [standards/05rm/html/RM-13-9.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-13-9.html)

![](Images/image06741.jpeg)

42 Chapter  [11](#part0085.xhtml__bookmark293)  on  page  [83](#part0085.xhtml__bookmark293)

43 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

• 13.3  Operational  and  Representation  Attributes  ˆ{[http://www.adaic.org/resources/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-13-3.html)  [add_content/standards/05rm/html/RM-13-3.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-13-3.html)

• Annex  K  (informative)  Language-Defined  Attributes  ˆ{[http://www.adaic.org/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-K.html)  [resources/add_content/standards/05rm/html/RM-K.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-K.html)

# 6 Integer  types

A  range  is  a  signed  integer  value  which  ranges  from  a  First  to  a  last  Last.  It  is  defined  as

![](Images/image06742.jpeg)

When a value is assigned to an object with such a range constraint, the value is checked for  validity  and  Constraint_Error  exception[1](#part0071.xhtml__bookmark239)  is  raised  when  the  value  is  not  within  First  to  Last.

When  declaring  a  range  type,  the  corresponding  mathematical  operators  are  implicitly  declared  by  the  language  at  the  same  place.

The  compiler  is  free  to  choose  a  suitable  underlaying  hardware  type  for  this  user  defined  type.

## 6.1 Working  demo

Working  demo

The  following  Demo  defines  a  new  range  from  -5  to  10  and  then  prints  the  whole  range  out.

![](Images/image06743.jpeg)![](Images/image06744.jpeg)

1Chapter  [19](#part0155.xhtml__bookmark478)  on  page  [153](#part0155.xhtml__bookmark478)

![](Images/image06745.jpeg)

## 6.2 See  also

See  also

#### 6.2.1  Wikibook

• Ada  Programming[2](#part0072.xhtml__bookmark241)

• Ada  Programming/Types[3](#part0072.xhtml__bookmark242)

• Ada Programming/Keywords/range[4](#part0072.xhtml__bookmark243)

#### 6.2.2  Ada  Reference  Manual

• 4.4  Expressions  ˆ{[http://www.adaic.org/resources/add_content/standards/05rm/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-4.html)  [html/RM-4-4.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-4.html)

• 3.5.4  Integer  Types  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-5-4.html)  [05rm/html/RM-3-5-4.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-5-4.html)

es:Programación  en  Ada/Tipos/Enteros[5](#part0072.xhtml__bookmark244)

![](Images/image06746.jpeg)

2 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

3 [http://en.wikibooks.org/wiki/Ada%20Programming%2FTypes](http://en.wikibooks.org/wiki/Ada%20Programming%2FTypes)

4 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Frange](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Frange)

5 [http://es.wikibooks.org/wiki/Programaci%F3n%20en%20Ada%2FTipos%2FEnteros](http://es.wikibooks.org/wiki/Programaci%F3n%20en%20Ada%2FTipos%2FEnteros)

# 7 Unsigned  integer  types

## 7.1 Description

Description

Unsigned  integers  in  Ada  have  a  value  range  from  0  to  some  positive  number  (not  necessarily  1 subtracted from some power of 2). They are defined using the mod keyword because they  implement  a  wrap-around  arithmetic.

![](Images/image06747.jpeg)

where  'First  is  0  and  'Last  is  Modulus  -  1.

Wrap-around arithmetic means that 'Last + 1 = 0 = 'First, and 'First - 1 = 'Last. Addi-  tionally to the normal arithmetic operators, bitwise and, or and xor are defined for the  type.

The predefined package Interfaces  (RM B.2  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-B-2.html)  [content/standards/05rm/html/RM-B-2.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-B-2.html)  )  presents  unsigned  integers  based  on  powers  of  2

![](Images/image06748.jpeg)

for  which  also  shift  and  rotate  operations  are  defined.  The  values  of  n  depend  on  compiler  and  target  architecture.

You  can  use  range  to  sub-range  a  modular  type:

![](Images/image06749.jpeg)

But beware:  the  Modulus of  Half_Byte is  still  256!  Arithmetic  with  such a  type  is interesting  to  say  the  least.

## 7.2 See  also

See  also

#### 7.2.1  Wikibook

• Ada  Programming[1](#part0074.xhtml__bookmark248)

• Ada  Programming/Types[2](#part0074.xhtml__bookmark249)

• Ada  Programming/Keywords/mod[3](#part0074.xhtml__bookmark250)

#### 7.2.2  Ada  Reference  Manual

• 4.4  Expressions  ˆ{[http://www.adaic.org/resources/add_content/standards/05rm/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-4.html)  [html/RM-4-4.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-4.html)

• 3.5.4  Integer  Types  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-5-4.html)  [05rm/html/RM-3-5-4.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-5-4.html)

![](Images/image06750.jpeg)

1 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

2 [http://en.wikibooks.org/wiki/Ada%20Programming%2FTypes](http://en.wikibooks.org/wiki/Ada%20Programming%2FTypes)

3 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fmod](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fmod)

# 8 Enumerations

An  enumeration  type  is  defined  as  a  list  of  possible  values:

![](Images/image06751.jpeg)

Like for numeric types, where e.g. 1 is an integer literal, Red, Green and Blue are called the  literals  of  this  type.  There  are  no  other  values  assignable  to  objects  of  this  type.

## 8.1 Operators  and  attributes

Operators  and  attributes

Apart  from  equality  ("="),  the  only  operators  on  enumeration  types  are  the  ordering  operators[1](#part0075.xhtml__bookmark254):  "<",  "<=",  "=",  "/=",  ">=",  ">",  where  the  order  relation  is  given  implicitly  by  the sequence of literals: Each literal has a position, starting with 0 for the first, incremented  by  one  for  each  successor.  This  position  can  be  queried  via  the  'Pos  attribute[2](#part0075.xhtml__bookmark255);  the  inverse  is  'Val,  which  returns  the  corresponding  literal.  In  our  example:

![](Images/image06752.jpeg)

There  are  two  other  important  attributes:  Image  and  Value  (don't  confuse  Val  with  Value).  Image  returns  the  string  representation  of  the  value  (in  capital  letters),  Value  is  the  inverse:

![](Images/image06753.jpeg)

These attributes are important for simple IO[3](#part0075.xhtml__bookmark256) (there are more elaborate IO facilities in Ada  for enumeration types). Note that, since Ada is case-insensitive, the string given to 'Value  can  be  in  any  case.

## 8.2 Enumeration  literals

![](Images/image06754.jpeg)

1 Chapter  [37](#part0303.xhtml__bookmark820)  on  page  [301](#part0303.xhtml__bookmark820)

2 Chapter  [38](#part0307.xhtml__bookmark878)  on  page  [305](#part0307.xhtml__bookmark878)

3 Chapter  [18](#part0149.xhtml__bookmark416)  on  page  [147](#part0149.xhtml__bookmark416)

Enumeration  literals

Literals  are  overloadable,  i.e.  you  can  have  another  type  with  the  same  literals.

![](Images/image06755.jpeg)

Overload resolution within the context of use of a literal normally resolves which Red is  meant. Only if you have an unresolvable overloading conflict, you can qualify with special  syntax  which  Red  is  meant:

![](Images/image06756.jpeg)

Like  many  other  declarative  items,  enumeration  literals  can  be  renamed.  In  fact,  such  a  literal  is  a  actually  function[4](#part0076.xhtml__bookmark257),  so  it  has  to  be  renamed  as  such:

![](Images/image06757.jpeg)

Here, Primary_Color is assumed to be defined in package P, which is visible at the place of  the renaming declaration. Renaming makes Red directly visible without necessity to resort  the  use-clause.

Note  that  redeclaration  as  a  function  does  not  affect  the  staticness  of  the  literal.

#### 8.2.1  Characters  as  enumeration  literals

Rather  unique  to  Ada  is  the  use  of  character  literals  as  enumeration  literals:

![](Images/image06758.jpeg)

This  literal  'A'  has  nothing  in  common  with  the  literal  'A'  of  the  predefined  type  Character  (or  Wide_Character).

Every  type  that  has  at  least  one  character  literal  is  a  character  type.  For  every  character  type,  string  literals  and  the  concatenation  operator  "&"[5](#part0076.xhtml__bookmark258)  are  also  implicitly  defined.

![](Images/image06759.jpeg)

In  this  example,  S  and  T  have  the  same  value.

![](Images/image06760.jpeg)

4 Chapter  [16.2](#part0129.xhtml__bookmark385)  on  page  [127](#part0129.xhtml__bookmark385)

5 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%26](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%26)

![](Images/image06761.jpeg)

Ada's  Character  type  is  defined  that  way.  See  Ada  Programming/Libraries/Standard[6](#part0077.xhtml__bookmark261).

#### 8.2.2  Booleans  as  enumeration  literals

Also  Booleans  are  defined  as  enumeration  types:

![](Images/image06762.jpeg)

There  is  special  semantics  implied  with  this  declaration  in  that  objects  and  expressions  of this type can be used as conditions.  Note that the literals False and True are not Ada  keywords.

Thus it is not sufficient to declare a type with these literals and then hope objects of this  type  can  be  used  like  so:

![](Images/image06763.jpeg)

If  you  need  your  own  Booleans  (perhaps  with  special  size  requirements),  you  have  to  derive  from  the  predefined  Boolean:

![](Images/image06764.jpeg)

## 8.3 Enumeration  subtypes

Enumeration  subtypes

You  can  use  range  to  subtype  an  enumeration  type:

![](Images/image06765.jpeg)

![](Images/image06766.jpeg)

## 8.4 See  also

![](Images/image06767.jpeg)

6 Chapter  [41](#part0335.xhtml__bookmark1379)  on  page  [333](#part0335.xhtml__bookmark1379)

See  also

#### 8.4.1  Wikibook

• Ada  Programming[7](#part0078.xhtml__bookmark262)

• Ada  Programming/Types[8](#part0078.xhtml__bookmark263)

• Ada  Programming/Libraries/Standard[9](#part0078.xhtml__bookmark264)

#### 8.4.2  Ada  Reference  Manual

• 3.5.1EnumerationTypesˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-5-1.html)  [standards/05rm/html/RM-3-5-1.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-5-1.html)

es:Programación  en  Ada/Tipos/Enumeraciones[10](#part0078.xhtml__bookmark265)

![](Images/image06768.jpeg)

7 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

8 [http://en.wikibooks.org/wiki/Ada%20Programming%2FTypes](http://en.wikibooks.org/wiki/Ada%20Programming%2FTypes)

9 Chapter  [41](#part0335.xhtml__bookmark1379)  on  page  [333](#part0335.xhtml__bookmark1379)

10 [http://es.wikibooks.org/wiki/Programaci%F3n%20en%20Ada%2FTipos%2FEnumeraciones](http://es.wikibooks.org/wiki/Programaci%F3n%20en%20Ada%2FTipos%2FEnumeraciones)

# 9 Floating  point  types

## 9.1 Description

Description

w:Floating  point[1](#part0079.xhtml__bookmark269)

To  define  a  floating  point  type,  you  only  have  to  say  how  many  digits[2](#part0079.xhtml__bookmark270) are  needed,  i.e.  you  define  the  relative  precision:

![](Images/image06769.jpeg)

If  you  like,  you  can  declare  the  minimum  range  needed  as  well:

![](Images/image06770.jpeg)<map name="awmap1"><area shape="rect" href="_bookmark0" coords="193, 11, 201, 24"></map>

This  facility  is  a  great  benefit  of  Ada  over  (most)  other  programming  languages.  In  other  languages,  you  just  choose  between  "float"  and  "long  float",  and  what  most  people  do  is:

• choose  float  if  they  don't  care  about  accuracy

• otherwise,  choose  long  float,  because  it  is  the  best  you  can  get  In  either  case,  you  don't  know  what  accuracy  you  get.

In  Ada,  you  specify  the  accuracy  you  need,  and  the  compiler  will  choose  an  appropriate  floating point type with at least the accuracy you asked for.  This way, your requirement is  guaranteed.  Moreover, if the computer has more than two floating point types available, the  compiler  can  make  use  of  all  of  them.

## 9.2 See  also

See  also

#### 9.2.1  Wikibook

• Ada  Programming[4](#part0079.xhtml__bookmark271)

![](Images/image06771.jpeg)

1 [http://en.wikipedia.org/wiki/Floating%20point](http://en.wikipedia.org/wiki/Floating%20point)

2 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fdigits](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fdigits)

4[http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

• Ada  Programming/Types[5](#part0080.xhtml__bookmark272)

• Ada  Programming/Types/range[6](#part0080.xhtml__bookmark273)

• Ada  Programming/Types/delta[7](#part0080.xhtml__bookmark274)

• Ada  Programming/Types/mod[8](#part0080.xhtml__bookmark275)

• Ada  Programming/Keywords/digits[9](#part0080.xhtml__bookmark276)

#### 9.2.2  Ada  Reference  Manual

• 3.5.7FloatingPointTypesˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-5-7.html)  [standards/05rm/html/RM-3-5-7.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-5-7.html)

es:Programación  en  Ada/Tipos/Coma  flotante[10](#part0080.xhtml__bookmark277)

![](Images/image06772.jpeg)

5 [http://en.wikibooks.org/wiki/Ada%20Programming%2FTypes](http://en.wikibooks.org/wiki/Ada%20Programming%2FTypes)

6 Chapter  [6](#part0071.xhtml__bookmark237)  on  page  [69](#part0071.xhtml__bookmark237)

7 Chapter  [10](#part0081.xhtml__bookmark278)  on  page  [79](#part0081.xhtml__bookmark278)

8 Chapter  [7](#part0073.xhtml__bookmark245)  on  page  [71](#part0073.xhtml__bookmark245)

9 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fdigits](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fdigits)

10 [http://es.wikibooks.org/wiki/Programaci%F3n%20en%20Ada%2FTipos%2FComa%20flotante](http://es.wikibooks.org/wiki/Programaci%F3n%20en%20Ada%2FTipos%2FComa%20flotante)

# 10 Fixed  point  types

## 10.1 Description

Description

w:Fixed-point  arithmetic[1](#part0081.xhtml__bookmark281)  A  fixed  point  type  defines  a  set  of  values  that  are  evenly  spaced  with a given absolute precision. In contrast, floating point values are all spaced according to  a  relative  precision.

The absolute precision is given as the delta of the type. There are two kinds of fixed point  types,  ordinary  and  decimal.

For Ordinary Fixed Point types, the delta gives a hint to the compiler how to choose the  small value if it is not specified: It can be any integer power of two not greater than delta.  You may specify the small via an attribute clause to be any value not greater than delta. (If  the  compiler  cannot  conform  to  this  small  value,  it  has  to  reject  the  declaration.)

For Decimal Fixed Point types, the small is defined to be the delta, which in turn must  be  an  integer  power  of  ten.  (Thus  you  cannot  specify  the  small  by  an  attribute  clause.)

For example, if you define a decimal fixed point type with a delta of 0.1, you will be able to  accurately  store  the  values  0.1,  1.0,  2.2,  5.7,  etc.  You  will  not  be  able  to  accurately  store  the  value  0.01.  Instead,  the  value  will  be  rounded  down  to  0.0.

If  the  compiler  accepts  your  fixed  point  type  definition,  it  guarantees  that  values  represented  by  that  type  will  have  at  least the degree  of  accuracy  specified  (or  better).  If  the  compiler  cannot  support  the  type  definition  (e.g.  due  to  limited  hardware)  then  a  compile-time  error  will  result.

## 10.2 Ordinary  Fixed  Point

Ordinary  Fixed  Point

For  an  ordinary  fixed  point,  you  just  define  the  delta  and  a  range:

![](Images/image06773.jpeg)

The  delta  can  be  any  real  value  —  for  example  you  may  define  a  circle  with  one  arcsecond  resolution  with:

![](Images/image06774.jpeg)

1[http://en.wikipedia.org/wiki/Fixed-point%20arithmetic](http://en.wikipedia.org/wiki/Fixed-point%20arithmetic)

![](Images/image06775.jpeg)

[There is one rather strange rule about fixed point types:  Because of the way they are  internally represented, the range might only go up to 'Last  -  Delta.  This is a bit like a  circle  —  the  0°  and  360°  mark  is  also  the  same.]

It  should  be  noted  that  in  the  example  above  the  smallest  possible  value  used  is  not  12  =   1   .

![](Images/image06776.jpeg)

603600

The  compiler  will  choose  a  smaller  value  which,  by  default,  is  an  integer  power  of  2  not

![](Images/image06777.jpeg)greater  than  the  delta.  In  our  example  this  could  be  2−12  =     1   .  In  most  cases  this  should

render  better  performance  but  sacrifices  precision  for  it.

If  this  is  not  what  you  wish  and  precision  is  indeed  more  important,  you  can  choose  your  own  small  value  via  the  attribute  clause  'Small.

![](Images/image06778.jpeg)

As  internal  representation,  you  will  get  a  32  bit  signed  integer  type.

## 10.3 Decimal  Fixed  Point

Decimal  Fixed  Point

You  define  a  decimal  fixed  point  by  defining  the  delta  and  the  number  of  digits  needed:

![](Images/image06779.jpeg)

Delta  must  be  a  positive  or  negative  integer  power  of  10  —  otherwise  the  declaration  is  illegal.

![](Images/image06780.jpeg)

If  you  like,  you  can  also  define  the  range  needed:

![](Images/image06781.jpeg)

## 10.4  Differences  between  Ordinary  and  Decimal  Fixed  Point  Types

Differences  between  Ordinary  and  Decimal  Fixed  Point  Types

There  is  an  alternative  way  of  declaring  a  "decimal"  fixed  point:  You  declare  an  ordinary  fixed  point  and  use  an  integer  power  of  10  as  'Small.  The  following  two  declarations  are

![](Images/image06782.jpeg)

equivalent  with  respect  to  the  internal  representation:

![](Images/image06783.jpeg)

![](Images/image06784.jpeg)

You might wonder what the difference then is between these two declarations. The answer  is:

None  with  respect  to  precision,  addition,  subtraction,  multiplication  with  integer  values.

The following is an incomplete list of differences between ordinary and decimal fixed point  types.

• Decimal fixed point types are intended to reflect typical COBOL declarations with a  given  number  of  digits.

• Truncation is required for decimal, not for ordinary, fixed point in multiplication and di-  vision  (RM  4.5.5  (21)  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-4-5-5.html)  [95lrm/ARM_HTML/RM-4-5-5.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-4-5-5.html) ) and type conversions. Operations on decimal fixed  point  are  fully  specified,  which  is  not  true  for  ordinary  fixed  point.

• The following attributes are only defined for decimal fixed point: T'Digits (RM

3.5.10  (10)  ˆ{[http://www.adaic.org/resources/add_content/standards/95lrm/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-5-10.html)  [ARM_HTML/RM-3-5-10.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-5-10.html)  )  corresponds  to  the  number  of  decimal  digits  that  are  representable;  T'Scale  (RM  3.5.10  (11)  ˆ{[http://www.adaic.org/resources/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-5-10.html)  [add_content/standards/95lrm/ARM_HTML/RM-3-5-10.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-5-10.html)  ,  taken  from  COBOL)  indicates  the  position  of  the point relative to the rightmost significant dig-  its;  T'Round  (RM  3.5.10  (12)  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-5-10.html)  [standards/95lrm/ARM_HTML/RM-3-5-10.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-5-10.html) ) can be used to specify rounding on  conversion.

• Package  Decimal  (RM  F.2  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-F-2.html)  [standards/95lrm/ARM_HTML/RM-F-2.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-F-2.html) ),  which  of  course  applies  only  to  decimal  fixed point, defines the decimal Divide generic procedure. If annex F is supported (GNAT  does),  at least  18 digits must be supported  (there is no  such rule  for  fixed point).

• Decimal_IO  (RM  A.10.1  (73)  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-A-10-1.html)  [standards/95lrm/ARM_HTML/RM-A-10-1.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-A-10-1.html) ) has semantics different from Fixed_-  IO  (RM  A.10.1  (68)  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-A-10-1.html)  [95lrm/ARM_HTML/RM-A-10-1.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-A-10-1.html) ).

• Static  expressions  must  be  a  multiple  of  the  Small  for  decimal  fixed  point.

Conclusion:  For  normal  numeric  use,  an  ordinary  fixed  point  (probably  with  'Small  defined) should be defined. Only if you are interested in COBOL like use, i.e. well defined  deterministic decimal semantics (especially for financial computations, but that might apply  to  cases  other  than  money)  should  you  take  decimal  fixed  point.

## 10.5 See  also

See  also

#### 10.5.1 Wikibook

• Ada  Programming[2](#part0084.xhtml__bookmark285)

• Ada  Programming/Types[3](#part0084.xhtml__bookmark286)

• Ada  Programming/Types/range[4](#part0084.xhtml__bookmark287)

• Ada  Programming/Types/digits[5](#part0084.xhtml__bookmark288)

• Ada  Programming/Types/mod[6](#part0084.xhtml__bookmark289)

• Ada  Programming/Keywords/delta[7](#part0084.xhtml__bookmark290)

• Ada  Programming/Attributes/'Small[8](#part0084.xhtml__bookmark291)

#### 10.5.2 Ada  95  Reference  Manual

• 3.5.9FixedPointTypesˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-5-9.html)  [standards/95lrm/ARM_HTML/RM-3-5-9.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-5-9.html)

#### 10.5.3 Ada  2005  Reference  Manual

• 3.5.9FixedPointTypesˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-5-9.html)  [standards/05rm/html/RM-3-5-9.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-5-9.html)

es:Programación  en Ada/Tipos/Coma  fija[9](#part0084.xhtml__bookmark292)

![](Images/image06785.jpeg)

2 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

3 [http://en.wikibooks.org/wiki/Ada%20Programming%2FTypes](http://en.wikibooks.org/wiki/Ada%20Programming%2FTypes)

4 Chapter  [6](#part0071.xhtml__bookmark237)  on  page  [69](#part0071.xhtml__bookmark237)

5 Chapter  [9](#part0079.xhtml__bookmark266)  on  page  [77](#part0079.xhtml__bookmark266)

6 Chapter  [7](#part0073.xhtml__bookmark245)  on  page  [71](#part0073.xhtml__bookmark245)

7 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fdelta](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fdelta)

8 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Small](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Small)

9 [http://es.wikibooks.org/wiki/Programaci%F3n%20en%20Ada%2FTipos%2FComa%20fija](http://es.wikibooks.org/wiki/Programaci%F3n%20en%20Ada%2FTipos%2FComa%20fija)

# 11 Arrays

An array[1](#part0085.xhtml__bookmark295) is a collection of elements which can be accessed by one or more index values. In  Ada any definite type is allowed as element and any discrete type, i.e. Range[2](#part0085.xhtml__bookmark296), Modular[3](#part0085.xhtml__bookmark297) or  Enumeration[4](#part0085.xhtml__bookmark298),  can  be  used  as  an  index.

## 11.1 Declaring  arrays

Declaring  arrays

Ada's  arrays  are  quite  powerful  and  so  there  are  quite  a  few  syntax  variations,  which  are  presented  below.

#### 11.1.1 Basic  syntax

The  basic  form  of  an  Ada  array  is:

![](Images/image06786.jpeg)

where  Index_Range  is  a  range  of  values  within  a  discrete  index  type,  and  Element_Type  is  a definite subtype. The array consists of one element of "Element_Type" for each possible  value in the given range.  If you for example want to count how often a specific letter  appears  inside  a  text,  you  could  use:

![](Images/image06787.jpeg)

As a general advice, do not use Integer as the index range, since most of the time negative  indices do not make sense. It is also a good style when using numeric indices, to define them  starting  in  1  instead  of  0,  since  it  is  more  intuitive  for  humans  and  avoids  off-by-one  error[5](#part0085.xhtml__bookmark299)s.

![](Images/image06788.jpeg)

1 [http://en.wikipedia.org/wiki/array](http://en.wikipedia.org/wiki/array)

2 Chapter  [6](#part0071.xhtml__bookmark237)  on  page  [69](#part0071.xhtml__bookmark237)

3 Chapter  [7](#part0073.xhtml__bookmark245)  on  page  [71](#part0073.xhtml__bookmark245)

4 Chapter  [8](#part0075.xhtml__bookmark251)  on  page  [73](#part0075.xhtml__bookmark251)

5 [http://en.wikipedia.org/wiki/off-by-one%20error](http://en.wikipedia.org/wiki/off-by-one%20error)

#### 11.1.2 With  known  subrange

Often  you  don't  need  an  array  of  all  possible  values  of  the  index  type.  In  this  case  you  can

subtype  your  index  type  to  the  actually  needed  range.

![](Images/image06789.jpeg)

Since  this  may  involve  a  lot  of  typing  and  you  may  also  run  out  of  useful  names  for  new  subtypes[6](#part0086.xhtml__bookmark300),  the  array  declaration  allows  for  a  shortcut:

![](Images/image06790.jpeg)

Since  First  and  Last  are  expressions  of  Index_Type,  a  simpler  form  of  the  above  is:

![](Images/image06791.jpeg)

Note  that  if  First  and  Last  are  numeric  literals,  this  implies  the  index  type  Integer.

If  in  the  example  above  the  character  counter  should  only  count  upper  case  characters  and  discard  all  other  characters,  you  can  use  the  following  array  type:

![](Images/image06792.jpeg)

#### 11.1.3 With  unknown  subrange

Sometimes  the  range  actually  needed  is  not  known  until  runtime  or  you  need  ob-  jects of different lengths.  In some languages you would resort to pointers to element  types.  Not  with  Ada.  Here  we  have  the  box  '<>',  which  allows  us  to  declare  indefinite  arrays:

![](Images/image06793.jpeg)

When  you  declare  objects  of  such  a  type,  the  bounds  must  of  course  be  given  and  the  object  is  constrained  to  them.

The  predefined  type  String[7](#part0086.xhtml__bookmark301)  is  such  a  type.  It  is  defined  as

![](Images/image06794.jpeg)

![](Images/image06795.jpeg)

6 [http://en.wikibooks.org/wiki/ada%20Programming%2FSubtypes](http://en.wikibooks.org/wiki/ada%20Programming%2FSubtypes)

7 Chapter  [15](#part0121.xhtml__bookmark373)  on  page  [119](#part0121.xhtml__bookmark373)

You  define  objects  of  such  an  unconstrained  type  in  several  ways  (the  extrapolation  to  other  arrays  than  String  should  be  obvious):

![](Images/image06796.jpeg)

(These  declarations  additionally  define  anonymous  subtypes  of  String.)  In  the  first  example,  the  range  of  indices  is  explicitly  given.  In  the  second  example,  the  range  is  implicitly  defined  from  the  initial  expression,  which  here  could  be  via  a  function  reading  data  from  some  file.  Both  objects  are  constrained  to  their  ranges,  i.e.  they  cannot  grow  nor  shrink.

#### 11.1.4 With  aliased  elements

If you come from C[8](#part0087.xhtml__bookmark302)/C++[9](#part0087.xhtml__bookmark303), you are probably used to the fact that every element of an  array  has  an  address.  The  C[10](#part0087.xhtml__bookmark304)/C++[11](#part0087.xhtml__bookmark305)  standards  actually  demand  that.

In  Ada,  this  is  not  true.  Consider  the  following  array:

![](Images/image06797.jpeg)

Since we have packed the array, the compiler will use as little storage as possible. And in  most  cases  this  will  mean  that  8  boolean  values  will  fit  into  one  byte.

So  Ada  knows  about  arrays  where  more  than  one  element  shares  one  address.  So  what  if  you  need  to  address  each  single  element.  Just  not  using pragma[12](#part0087.xhtml__bookmark306) Pack[13](#part0087.xhtml__bookmark307)   is  not  enough.  If the CPU[14](#part0087.xhtml__bookmark308) has very fast bit access, the compiler might pack the array without  being  told.  You  need  to  tell  the  compiler  that  you  need  to  address  each  element  via  an  access.

![](Images/image06798.jpeg)

#### 11.1.5 Arrays  with  more  than  one  dimension

Arrays  can  have  more  than  one  index.  Consider  the  following  2-dimensional  array:

![](Images/image06799.jpeg)

8 [http://en.wikibooks.org/wiki/Programming%3AC](http://en.wikibooks.org/wiki/Programming%3AC)

9 [http://en.wikibooks.org/wiki/Programming%3AC_plus_plus](http://en.wikibooks.org/wiki/Programming%3AC_plus_plus)

10 [http://en.wikibooks.org/wiki/Programming%3AC](http://en.wikibooks.org/wiki/Programming%3AC)

11 [http://en.wikibooks.org/wiki/Programming%3AC_plus_plus](http://en.wikibooks.org/wiki/Programming%3AC_plus_plus)

12 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fpragma](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fpragma)

13 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPack](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPack)

14 [http://en.wikipedia.org/wiki/CPU](http://en.wikipedia.org/wiki/CPU)

![](Images/image06800.jpeg)

This  type  permits  declaring  rectangular  arrays  of  characters.  Example:

| (  ’  A’  , | ’  R’  , | ’  E’  , | ’  P’  , | ’  O’  )  , |
| (  ’  T’  , | ’  E’  , | ’  N’  , | ’  E’  , | ’  T’  )  , |
| (  ’  O’  , | ’  P’  , | ’  E’  , | ’  R’  , | ’  A’  )  , |
| (  ’  R’  , | ’  O’  , | ’  T’  , | ’  A’  , | ’  S’  )  )  ; |

![](Images/image06801.jpeg)Or,  stating  some  index  values  explicitly,

| 2  => | (  ’  A’  , | ’  R’  , | ’  E’  , | ’  P’  , | ’  O’  )  , |
| 3  => | (  ’  T’  , | ’  E’  , | ’  N’  , | ’  E’  , | ’  T’  )  , |
| 4  => | (  ’  O’  , | ’  P’  , | ’  E’  , | ’  R’  , | ’  A’  )  , |
| 5  => | (  ’  R’  , | ’  O’  , | ’  T’  , | ’  A’  , | ’  S’  )  )  ; |

![](Images/image06802.jpeg)The  index  values  of  the  second  dimension,  those  indexing  the  characters  in  each  row,  are  in  1  ..  5  here.  By  choosing  a  different  second  range,  we  could  change  these  to  be  in  11  ..  15:

![](Images/image06803.jpeg)

By  adding  more  dimensions  to  an  array  type,  we  could  have  squares,  cubes  (or  «  bricks  »),  etc.,  of  homogenous  data  items.

Finally,  an  array  of  characters  is  a  string  (see  Ada  Programming/Strings[15](#part0088.xhtml__bookmark310)).  Therefore,

Magic_Square  may  simply  be  declared  like  this:

![](Images/image06804.jpeg)

## 11.2 Using  arrays

![](Images/image06805.jpeg)

15 Chapter  [15](#part0121.xhtml__bookmark373)  on  page  [119](#part0121.xhtml__bookmark373)

Using  arrays

#### 11.2.1 Assignment

When  accessing  elements,  the  index  is  specified  in  parentheses.  It  is  also  possible  to  access  slices  in  this  way:

![](Images/image06806.jpeg)

Note  that  the  index  range  slides  in  this  example:  After  the  assignment,  Vector_A  (1)  =  Vector_B  (3)  and  similarly  for  the  other  indices.

Also  note that the  ranges  overlap,  nevertheless Vector_A (3)  /= Vector_B  (3); a  compiler  delivering  such  a  result  would  be  severely  broken.

#### 11.2.2 Concatenate

The  operator  "&"  can  be  used  to  concatenate  arrays:

![](Images/image06807.jpeg)

In  both  cases,  if  the  resulting  array  does  not  fit  in  the  destination  array,  Constraint_Error  is  raised.

If  you  try  to  access  an  existing  element  by  indexing  outside  the  array  bounds,  Constraint_-  Error  is  raised  (unless  checks  are  suppressed).

#### 11.2.3 Array  Attributes

There  are  four  Attributes  which  are  important  for  arrays:  'First,  'Last,  'Length  and  'Range.  Lets  look  at  them  with  an  example.  Say  we  have  the  following  three  strings:

![](Images/image06808.jpeg)

Then  the  four  attributes  will  have  the  following  values:

| Array | 'First | 'Last | 'Length | 'Range |
| Hello_World | 1 | 12 | 12 | 1  ..  12 |
| World | 7 | 11 | 5 | 7  ..  11 |
| Empty_String | 1 | 0 | 0 | 1  ..  0 |

The  example  was  chosen  to  show  a  few  common  beginner's  mistakes:

1. The  assumption  that  strings  begin  with  the  index  value  1  is  wrong.

2. The  assumption  (which  follows  from  the  first  one)  that  X'Length  =  X'Last  is  wrong.

3. And  last  the  assumption  that  X'Last  >=  X'First;  this  is  not  true  for  empty  strings.

The attribute 'Range is a little special as it does not return a discrete value but an abstract  description of the array. One might wonder what it is good for. The most common use is in  the  for  loop  on  arrays[16](#part0090.xhtml__bookmark312) but  'Range  can  also  be  used  in  declaring  a  name  for  the  index  subtype:

![](Images/image06809.jpeg)

The  Range  attribute  can  be  convenient  when  programming  index  checks:

![](Images/image06810.jpeg)

#### 11.2.4 Empty  or  Null  Arrays

As  you  have  seen  in  the  section  above,  Ada  allows  for  empty  arrays.  And  —  of  course  —  you  can  have  empty  arrays  of  all  sorts,  not  just  String:

![](Images/image06811.jpeg)

Note:  If  you  give  an  initial  expression  to  an  empty  array  (which  is  a  must  for  a  constant),  the expression in the aggregate will of course not be evaluated since there are no elements  actually  stored.

## 11.3 See  also

See  also

#### 11.3.1 Wikibook

• Ada  Programming[17](#part0090.xhtml__bookmark313)

• Ada  Programming/Types[18](#part0090.xhtml__bookmark314)

• Data  Structures[19](#part0090.xhtml__bookmark315)

• Data  Structures/Arrays[20](#part0090.xhtml__bookmark316)

![](Images/image06812.jpeg)

16 Chapter  [4](#part0039.xhtml__bookmark161)  on  page  [37](#part0039.xhtml__bookmark161)

17 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

18 [http://en.wikibooks.org/wiki/Ada%20Programming%2FTypes](http://en.wikibooks.org/wiki/Ada%20Programming%2FTypes)

19 [http://en.wikibooks.org/wiki/Data%20Structures](http://en.wikibooks.org/wiki/Data%20Structures)

20 [http://en.wikibooks.org/wiki/Data%20Structures%2FArrays](http://en.wikibooks.org/wiki/Data%20Structures%2FArrays)

#### 11.3.2 Ada  95  Reference  Manual

• 3.6ArrayTypesˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-6.html)  [95lrm/ARM_HTML/RM-3-6.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-6.html)

#### 11.3.3 Ada  2005  Reference  Manual

• 3.6ArrayTypesˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-6.html)  [05rm/html/RM-3-6.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-6.html)

#### 11.3.4 Ada  Quality  and  Style  Guide

• 10.5.7  Packed  Boolean  Array  Shifts  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/docs/95style/html/sec_10/10-5-7.html)  [content/docs/95style/html/sec_10/10-5-7.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_10/10-5-7.html)

es:Programación en Ada/Tipos/Arrays[21](#part0091.xhtml__bookmark317)

![](Images/image06813.jpeg)

21 [http://es.wikibooks.org/wiki/Programaci%F3n%20en%20Ada%2FTipos%2FArrays](http://es.wikibooks.org/wiki/Programaci%F3n%20en%20Ada%2FTipos%2FArrays)

# 12 Records

A  record  is  a  composite  type[1](#part0093.xhtml__bookmark322)  that  groups  one  or  more  fields.  A  field  can  be  of  any  type,  even  a  record.

## 12.1 Basic  record

Basic  record

![](Images/image06814.jpeg)

## 12.2 Null  record

Null  record

The  null  record  is  when  a  type  without  data  is  needed.  There  are  two  ways  to  declare  a  null  record:

![](Images/image06815.jpeg)

![](Images/image06816.jpeg)

For the compiler they are the same. However, programmers often use the first variant if the  type is not finished yet to show that they are planning to expand the type later, or they  usually  use  the  second  if  the  (tagged)  record  is  a  base  class  in  object  oriented  programming.

## 12.3 Record  Values

Record  Values

Values of a record type can be specified using a record aggregate, giving a list of named  components  thus

![](Images/image06817.jpeg)

1[http://en.wikibooks.org/wiki/ada%20Programming%2FTypes%23List%20of%20types](http://en.wikibooks.org/wiki/ada%20Programming%2FTypes%23List%20of%20types)

![](Images/image06818.jpeg)

Given  a  somewhat  larger  record  type,

![](Images/image06819.jpeg)

a  value  may  be  specified  using  positional  notation,  that  is,  specifying  a  value  for  each  record  component  in  declaration  order

![](Images/image06820.jpeg)

However,  naming  the  components  of  a  Car  aggregate  offers  a  number  of  advantages.

1. Easy  identification  of  which  value  is  used  for  which  component.  (After  all,  named  components  are  the  raison  d'être  of  records.)

2. Reordering  the  components  is  allowed—you  only  have  to  remember  the  component  names,  not  their  position.

3. Improved  compiler diagnostic  messages.

Reordering  components  is  possible  because  component  names  will  inform  the  compiler  (and the human reader!) of the intended value associations. Improved compiler messages  are  also  in  consequence  of  this  additional  information  passed  to  the  compiler.  While  an  omitted  component  will  always  be  reported  due  to  Ada's  coverage  rules[2](#part0094.xhtml__bookmark323),  messages  can  be  much  more  specific  when  there  are  named  associations.  Considering  the  Car  type  from  above,  suppose  a  programmer  by  mistake  specifies  only  one  of  the  two  floating point values for BMW in positional notation.  The compiler, in search of another  component  value,  will  then  not  be  able  to  decide  whether  the  specified  value  is  intended  for Horse_Power_kW or for Consumption.  If the programmer instead uses named asso-  ciation,  say Horse_Power_kW  =>  190.  0,  it  will be clear  which other component is  missing.

![](Images/image06821.jpeg)

In  order  to  access  a  component  of  a  record  instance,  use  the  dot  delimiter  (.  ),  as  in  BMW.  Number_Wheels.

![](Images/image06822.jpeg)

2[http://www.adacore.com/2007/05/14/gem-1/](http://www.adacore.com/2007/05/14/gem-1/)

## 12.4 Discriminated  record

Discriminated  record

![](Images/image06823.jpeg)

## 12.5 Variant  record

Variant  record

The  variant  record  is  a  special  type  of  discriminated  record  where  the  presence  of  some  components  depend  on  the  value  of  the  discriminant.

![](Images/image06824.jpeg)

#### 12.5.1 Mutable  and  immutable  variant  records

You  can  declare  variant  record  types  such  that  its  discriminant,  and  thus  its  variant  structure,  can be changed during the lifetime of the variable.  Such a record is said to be mutable.  When "mutating" a record, you must assign all components of the variant structure which  you  are  mutating  at  once,  replacing  the  record  with  a  complete  variant  structure.  Although  a variant record declaration may allow objects of its type to be mutable, there are certain  restrictions  on  whether  the  objects  will  be  mutable.  Reasons  restricting  an  object  from  being  mutable  include:

• the  object  is  declared  with  a  discriminant  (see  Immutable_Traffic_Light  below)

• the  object  is  aliased  (either  by  use  of  aliased  in  the  object  declaration,  or  by  allocation  on  the  heap  using  new)

![](Images/image06825.jpeg)

![](Images/image06826.jpeg)

Conversely,  you  can  declare  record  types  so  that  the  discriminant  along  with  the  structure  of the variant record may not be changed.  To make a record type declaration immutable,  the  discriminant  must  not  have  a  default  value.

![](Images/image06827.jpeg)

![](Images/image06828.jpeg)

## 12.6 Union

Union

This  language  feature  is  only  available  in  Ada  2005

![](Images/image06829.jpeg)

The  difference  to  a  variant  record  is  such  that  Option  is  not  actually  stored  inside  the  record  and  never  checked  for  correctness  -  it's  just  a  dummy.

This kind of record is usually used for interfacing with C but can be used for other purposes  as  well  (then  without  pragma  (C,  Union);).

## 12.7 Tagged  record

Tagged  record

The tagged record is one part of what in other languages is called a class.  It is the basic  foundation of object orientated programming in Ada[3](#part0097.xhtml__bookmark328). The other two parts a class in Ada  needs  is  a  package[4](#part0097.xhtml__bookmark329)  and  primitive  operations[5](#part0097.xhtml__bookmark330).

![](Images/image06830.jpeg)

3 Chapter  [22](#part0189.xhtml__bookmark519)  on  page  [187](#part0189.xhtml__bookmark519)

4 Chapter  [22.4.2](#part0219.xhtml__bookmark533)  on  page  [217](#part0219.xhtml__bookmark533)

5 Chapter  [22.1.2](#part0190.xhtml__bookmark521)  on  page  [188](#part0190.xhtml__bookmark521)

![](Images/image06831.jpeg)

![](Images/image06832.jpeg)

Ada  2005  only:

![](Images/image06833.jpeg)

## 12.8 Abstract  tagged  record

Abstract  tagged  record

An  abstract  type  has  at  least  an  abstract  primitive  operation,  i.e.  one  of  its  operations  is  not  defined  and  then  its  derivative  types  has  to  provide  an  implementation.

## 12.9 With  aliased  elements

With  aliased  elements

If you come from C[6](#part0098.xhtml__bookmark333)/C++[7](#part0098.xhtml__bookmark334), you are probably used to the fact that every element of a  record - which is not part of a bitset - has an address.  In Ada, this is not true because  records,  just  like  arrays,  can  be  packed.  And  just  like  arrays  you  can  use  aliased  to  ensure  that  an  element  can  be  accessed  via  an  access  type.

![](Images/image06834.jpeg)

Please  note:  each  element  needs  its  own  aliased.

![](Images/image06835.jpeg)

6 [http://en.wikibooks.org/wiki/C%20Programming](http://en.wikibooks.org/wiki/C%20Programming)

7 [http://en.wikibooks.org/wiki/C%2B%2B%20Programming](http://en.wikibooks.org/wiki/C%2B%2B%20Programming)

## 12.10  Limited  Records

Limited  Records

In  addition  to  being  variant,  tagged,  and  abstract,  records  may  also  be  limited  (no  assignment,  and no predefined equality operation for Limited Types[8](#part0099.xhtml__bookmark337)). In object oriented programming,  when tagged objects are handled by references instead of copying them, this blends well  with  making  objects  limited.

## 12.11  See  also

See  also

#### 12.11.1 Wikibook

• Ada  Programming[9](#part0099.xhtml__bookmark338)

• Ada  Programming/Types[10](#part0099.xhtml__bookmark339)

• Ada Programming/Keywords/record[11](#part0099.xhtml__bookmark340)

• Ada  Programming/Keywords/null[12](#part0099.xhtml__bookmark341)

• Ada  Programming/Keywords/abstract[13](#part0099.xhtml__bookmark342)

• Ada  Programming/Keywords/case[14](#part0099.xhtml__bookmark343)

• Ada  Programming/Keywords/when[15](#part0099.xhtml__bookmark344)

• Ada  Programming/Pragmas/Unchecked_Union[16](#part0099.xhtml__bookmark345)

#### 12.11.2 Ada  Reference  Manual

###### Ada  95

• 3.8  Record  Types  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-8.html)  [95lrm/ARM_HTML/RM-3-8.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-8.html)

###### Ada  2005

• 3.8  Record  Types  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-8.html)  [05rm/html/RM-3-8.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-8.html)

• Annex  B.3.3  Pragma  Unchecked_Union  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-B-3-3.html)  [content/standards/05rm/html/RM-B-3-3.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-B-3-3.html)

![](Images/image06836.jpeg)

8 Chapter  [14](#part0115.xhtml__bookmark366)  on  page  [113](#part0115.xhtml__bookmark366)

9 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

10 [http://en.wikibooks.org/wiki/Ada%20Programming%2FTypes](http://en.wikibooks.org/wiki/Ada%20Programming%2FTypes)

11 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Frecord](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Frecord)

12 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fnull](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fnull)

13 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fabstract](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fabstract)

14 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fcase](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fcase)

15 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fwhen](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fwhen)

16 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FUnchecked_Union](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FUnchecked_Union)

###### Ada  Issues

• AI95-00216-01  Unchecked  unions  —  variant  records  with  no  run-time  discriminant  ˆ{[http:](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00216.TXT)

[//www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00216.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00216.TXT)

# 13 Access  types

## 13.1 What's  an  Access  Type?

What's  an  Access  Type?

Access  types  in  Ada  are  what  other  languages  call  pointers.  They  point  to  objects  located  at certain addresses. So normally one can think of access types as simple addresses (there  are exceptions from this simplified view). Ada instead of saying points to talks of granting  access  to  or  designating  an  object.

Objects  of  access  types  are  implicitly  initialized  with  null,  i.e.  they  point  to  nothing  when  not  explicitly  initialized.

Access types should be used rarely in Ada. In a lot of circumstances where pointers are  used in other languages, there are other ways without pointers.  If you need dynamic  data structures,  first check whether you can use the Ada Container library.  Especially  for  indefinite  record  or  array  components,  the  Ada  2012  package  Indefinite_Holders  (RM  A.18.18)  can  be  used  instead  of  pointers.

There are four kinds of access types in Ada:  Pool access types - General access types -  Anonymous  access  types  -  Access  to  subprogram  types.

## 13.2 Pool  access

Pool  access

A  pool  access  type  handles  accesses  to  objects  which  were  created  on  some  specific  heap  (or  storage  pool  as  it  is  called  in  Ada).  A  pointer  of  these  types  cannot  point  to  a  stack  or  library level (static) object or an object in a different storage pool.  Therefore, conversion  between pool access types is illegal.  (Unchecked_Conversion may be used, but note that  deallocation via an access object with a storage pool different from the one it was allocated  with  is  erroneous.)

![](Images/image06837.jpeg)

A  size  clause  may  be  used  to  limit  the  corresponding  (implementation  defined  anonymous)  storage  pool.  A  size  clause  of  0  disables  calls  of  an  allocator.

![](Images/image06838.jpeg)

The  storage  pool  is  implementation  defined  if  not  specified.  Ada  supports  user  defined  storage  pools,  so  you  can  define  the  storage  pool  with

![](Images/image06839.jpeg)

Objects  in  a  storage  pool  are  created  with  the  keyword  new:

![](Images/image06840.jpeg)

You access the object in the storage pool by appending .all. Mother.all is the complete  record; components are denoted as usual with the dot notation: Mother.all.First_Name.  When accessing components, implicit dereferencing (i.e.  omitting all) can serve as a  convenient  shorthand:

![](Images/image06841.jpeg)

Implicit  dereferencing  also  applies  to  arrays:

![](Images/image06842.jpeg)

Be  careful  to  discriminate  between  deep  and  shallow  copies  when  copying  with  access  objects:

![](Images/image06843.jpeg)

#### 13.2.1 Deleting  objects  from  a  storage  pool

Although  the  Ada  standard  mentions  a  garbage  collector,  which  would  automatically  remove  all unneeded objects that have been created on the heap (when no storage pool has been  defined), only Ada compilers targeting a virtual machine like Java or .NET actually have  garbage collectors.  There is also a pragma  Controlled, which, when applied to such an  access type, prevents automatic garbage collection of objects created with it.  Note that  pragma  Controlled  will  be  dropped  from  Ada  2012,  see  RM  2012  13.11.3.

Therefore in order to delete an object from the heap, you need the generic unit Ada .  Apply  utmost  care  to  not  create  dangling  pointers  when  deallocating  objects  as  is  shown  in  the  example below.  (And note that deallocating objects with a different access type than the one  with  which  they  were  created  is  erroneous  when  the  corresponding  storage  pools  are  different.)

![](Images/image06844.jpeg)

It  is  exactly  because  of  this  problem  with  dangling  pointers  that  the  deallocation  operation  is called unchecked.  It is the chore of the programmer to take care that this does not  happen.

Since Ada allows for user defined storage pools, you could also try a garbage collector  library[1](#part0103.xhtml__bookmark349).

![](Images/image06845.jpeg)

1[http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FMultiPurpose%2FAdaCL%](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FMultiPurpose%2FAdaCL%23Garbage_Collector)  [23Garbage_Collector](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FMultiPurpose%2FAdaCL%23Garbage_Collector)

#### 13.2.2 Constructing  Reference  Counting  Pointers

You  can  find  some  implementations  of  reference  counting  pointers,  called  Safe  or  Smart  Pointers,  on  the  net.  Using  such  a  type  prevents  caring  about  deallocation,  since  this  will  automatically be done when there are no more pointers to an object.  But be careful - most of  those implementations do not prevent deliberate deallocation, thus undermining the alledged  safety  attained  with  their  use.

A  nice  tutorial  how  to  construct  such  a  type  can  be  found  in  a  series  of  Gems  on  the  AdaCore  web  site.

Gem #97: Reference Counting in Ada – Part 1[2](#part0104.xhtml__bookmark351) This little gem constructs a simple reference  counted  pointer  that  does  not  prevent  deallocation,  i.e.  is  inherently  unsafe.

Gem #107:  Preventing Deallocation for Reference-counted Types[3](#part0104.xhtml__bookmark352) This further gem describes  how  to  arrive  at  a  pointer  type  whose  safety  cannot  be  compromised  (tasking  issues  aside).  The  cost  of  this  improved  safety  is  awkward  syntax.

Gem #123: Implicit Dereferencing in Ada 2012[4](#part0104.xhtml__bookmark353) This gem shows how to simplify the syntax  with the new Ada 2012 generation.  (Admittedly, this gem is a bit unrelated to reference  counting  since  the  new  language  feature  can  be  applied  to  any  kind  of  container.)

## 13.3 General access

General  access

General  access  types  grant  access  to  objects  created  on  any  storage  pool,  on  the  stack  or  at library level (static).  They come in two versions, granting either read-write access or  read-only access.  Conversions between general access types are allowed, but subject to  certain  access  level  checks.

Dereferencing  is  like  for  pool  access  types.  Objects  (other  than  pool  objects)  to  be  referenced  have to be declared aliased, and references to them are created with the attribute 'Access.  Access level restrictions prevent accesses to objects from outliving the accessed object,  which  would  make  the  program  erroneous.  The  attribute  'Unchecked_Access  omits  the corresponding  checks.

#### 13.3.1 Access  to  Variable

When  the  keyword  all  is  used  in  their  definition,  they  grant  read-write  access.

![](Images/image06846.jpeg)

![](Images/image06847.jpeg)

2 [http://www.adacore.com/2011/01/17/gem-97-reference-counting-in-ada-part-1/](http://www.adacore.com/2011/01/17/gem-97-reference-counting-in-ada-part-1/)

3 [http://www.adacore.com/2011/06/06/gem-107-preventing-deallocation-for-reference-counted-types/](http://www.adacore.com/2011/06/06/gem-107-preventing-deallocation-for-reference-counted-types/)

4 [http://www.adacore.com/adaanswers/gems/gem-123-implicit-dereferencing-in-ada-2012/](http://www.adacore.com/adaanswers/gems/gem-123-implicit-dereferencing-in-ada-2012/)

#### 13.3.2 Access  to  Constant

General  access  types  granting  read-only  access  to  the  referenced  object  use  the  keyword

constant  in  their  definition.  The  referenced  object  may  be  a  constant  or  a  variable.

![](Images/image06848.jpeg)

13.3.3 Some  examples

![](Images/image06849.jpeg)

## 13.4 Anonymous access

Anonymous  access

Also  Anonymous  access  types  come  in  two  versions  like  general  access  types,  granting  either  read-write  access  or  read-only  access  depending  on  whether  the  keyword  constant  appears.

An  anonymous  access  can  be  used  as  a  parameter  to  a  subprogram  or  as  a  discriminant.  Here  are  some  examples:

![](Images/image06850.jpeg)

![](Images/image06851.jpeg)

![](Images/image06852.jpeg)

Before  using  an  anonymous  access,  you  should  consider  a  named  access  type  or,  even  better,  consider  if  the  "out"  or  "in  out"  modifier  is  not  more  appropriate.

This  language  feature  is  only  available  in  Ada  2005

In  Ada  2005,  anonymous  accesses  are  allowed  in  more  circumstances:

![](Images/image06853.jpeg)

## 13.5 Implicit  Dereference

Implicit  Dereference

Ada  2012  will  simplify  accesses  to  objects  via  pointers  with  new  syntax.  Imagine  you  have  a  container  holding  some  kind  of  elements.

![](Images/image06854.jpeg)

Now  how  do  you  access  elements  stored  in  the  container.  Of  course  you  can  retrieve  them  by

![](Images/image06855.jpeg)

This  will  however  copy  the  element,  which  is  unfortunate  if  the  element  is  big.  You  get  direct  access  with

![](Images/image06856.jpeg)

Now  pointers  are  dangerous  since  you  might  easily  create  dangling  pointers  like  so:

![](Images/image06857.jpeg)

Use  of  an  accessor  object  instead  of  an  access  type  can  prevent  inadvertant  deallocation  (this  is  still  Ada  2005):

![](Images/image06858.jpeg)

(For  the  null  exclusion  not  null  in  the  declaration  of  the  discriminant,  see  below).  Access  via such an accessor is safe: The discriminant can only be used for dereferencing, it cannot  be  copied  to  an  object  of  type  Element_Ptr  because  its  accessibility  level  is  deeper.  In  the

form  above,  the  accessor  provides  read  and  write  access.  If  the  keyword  constant  is  added,  only  read  access  is  possible.

![](Images/image06859.jpeg)

Access  to  the  container  object  now  looks  like  so:

![](Images/image06860.jpeg)

Here  the  new  Ada  2012  feature  of  aspects  comes  along  handy;  for  the  case  at  hand,  the  aspect  Implicit_Dereference  is  the  one  we  need:

![](Images/image06861.jpeg)

Now  rather  than  writing  the  long  and  ugly  function  call  of  above,  we  can  just  omit  the  discriminant  and  its  dereference  like  so:

![](Images/image06862.jpeg)

Note  that  the  call  Get  (Cont)  is  overloaded  —  it  can  denote  the  accessor  object  or  the  element,  the  compiler  will  select  the  correct  interpretation  depending  on  context.

## 13.6 Null  exclusions

Null  exclusions

This  language  feature  is  only  available  in  Ada  2005

All  access  subtypes  can  be  modified  with  not  null,  objects  of  such  a  subtype  can  then  never  have  the  value  null,  so  initializations  are  compulsory.

![](Images/image06863.jpeg)

The  language  also  allows  to  declare  the  first  subtype  directly  with  a  null  exclusion:

![](Images/image06864.jpeg)

However, in nearly all cases this is not a good idea because it renders objects of this type nearly  unusable  (for  example,  you  are  unable  to  free  the  allocated  memory).  Not  null  accesses  are  intended  for  access  subtypes,  object  declarations,  and  subprogram  parameters.[http:](http://groups.google.com/group/comp.lang.ada/msg/13a41ced7af75192)

[//groups.google.com/group/comp.lang.ada/msg/13a41ced7af75192](http://groups.google.com/group/comp.lang.ada/msg/13a41ced7af75192)

## 13.7 Access  to  Subprogram

Access  to  Subprogram

An  access  to  subprogram  allows  to  call  a  subprogram[5](#part0108.xhtml__bookmark359)  without  knowing  its  name  nor  its  declaration  location.  One  of  the  uses  of  this  kind  of  access  is  the  well  known  callbacks.

![](Images/image06865.jpeg)

For  getting  an  access  to  a  subprogram,  the  attribute  Access  is  applied  to  a  subprogram  name  with  the  proper  parameter  and  result  profile.

![](Images/image06866.jpeg)

#### 13.7.1 Anonymous  access  to  Subprogram

This  language  feature  is  only  available  in  Ada  2005

![](Images/image06867.jpeg)

There  is  now  no  limit  on  the  number  of  keyword  in  a  sequence:

![](Images/image06868.jpeg)

This  is  a  function  that  returns  the  access  to  a  function  that  in  turn  returns  an  access  to  a  function  returning  an  access  to  some  type.

## 13.8 Access  FAQ

Access  FAQ

A  few  "Frequently  Asked  Question"  and  "Frequently  Encountered  Problems"  (mostly  from  C[6](#part0108.xhtml__bookmark360)  users)  regarding  Ada's  access  types.

![](Images/image06869.jpeg)

5 Chapter  [16](#part0127.xhtml__bookmark381)  on  page  [125](#part0127.xhtml__bookmark381)

6 [http://en.wikibooks.org/wiki/Programming%3AC](http://en.wikibooks.org/wiki/Programming%3AC)

#### 13.8.1 Access  vs.  access  all

An  access  all  can  do  anything  a  simple  access  can  do.  So  one  might  ask:  "Why  use  simple

access  at  all?"  -  And  indeed  some  programmers  never  use  simple  access.

Unchecked_Deallocation  is  always  dangerous  if  misused.  It  is  just  as  easy  to  deallocate  a pool-specific object twice,  and just as dangerous as deallocating a stack object.  The  advantage  of  "access  all"  is  that  you  may  not  need  to  use  Unchecked_Deallocation  at  all.

Moral: if you have (or may have) a valid reason to store an 'Access or 'Unchecked_Access  into an access object, then use "access all" and don't worry about it. If not, the mantra of  "least privilege" suggests that the "all" should be left out (don't enable capabilities that you  are  not  going  to  use).

The  following  (perhaps  disastrous)  example  will  try  to  deallocate  a  stack  object:

![](Images/image06870.jpeg)

With  a  simple  access  you  know  at  least  that  you  won't  try  to  deallocate  a  stack  object.

#### 13.8.2 Access  vs.  System.Address

An access can be something different from a mere memory address, it may be something  more.  For  example,  an  "access  to  String"  often  needs  some  way  of  storing  the  string  size  as well. If you need a simple address and are not concerned about strong typing, use the  System.Address  type.

#### 13.8.3 C  compatible  pointer

The  correct  way  to  create  a  C  compatible  access  is  to  use  pragma  :

![](Images/image06871.jpeg)

![](Images/image06872.jpeg)

pragma  should  be  used  on  any  type  you  want  to  use  in  C.  The  compiler  will  warn  you  if  the  type  cannot  be  made  C  compatible.

You  may  also  consider  the  following  -  shorter  -  alternative  when  declaring  Day_Of_Month:

![](Images/image06873.jpeg)

Before  you  use  access  types  in  C,  you  should  consider  using  the  normal  "in",  "out"  and  "in  out" modifiers. pragma  and pragma  know how parameters are usually passed in C and  will use a pointer to pass a parameter automatically where C would have used them as  well. Of course the RM contains precise rules on when to use a pointer for "in", "out", and  "in out" - see "B.3 Interfacing with C ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-B-3.html)  [standards/05rm/html/RM-B-3.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-B-3.html) ".

#### 13.8.4 Where  is  void*?

While  actually  a  problem  for  "interfacing  with  C",  here  are  some  possible  solutions:

![](Images/image06874.jpeg)

Less  portable  but  perhaps  more  usable  (for  32  bit  CPUs):

![](Images/image06875.jpeg)

With  GNAT  you  can  get  32/64  bit  portability  by  using:

![](Images/image06876.jpeg)

Closer  to  the  true  nature  of  void  -  pointing  to  an  element  of  zero  size  is  a  pointer  to  a  null  record.  This  also  has  the  advantage  of  having  a  representation  for  void  and  void*:

![](Images/image06877.jpeg)

## 13.9 Thin  and  Fat  Access  Types

Thin  and  Fat  Access  Types

The difference between an access type and an address will be detailed in the following. The  term  pointer  is  used  because  this  is  usual  terminology.

There  is  a  predefined  unit  System.Address_to_Access_Conversion  converting  back  and  forth  between  access  values  and  addresses.  Use  these  conversions  with  care,  as  is  explained  below.

#### 13.9.1 Thin  Pointers

Thin  pointers  grant  access  to  constrained  subtypes.

![](Images/image06878.jpeg)

Objects  of  subtypes  like  these  have  a  static  size,  so  a  simple  address  suffices  to  access  them.  In  the  case  of  arrays,  this  is  generally  the  address  of  the  first  element.

For  pointers  of  this  kind,  use  of  System.Address_to_Access_Conversion  is  safe.

#### 13.9.2 Fat  Pointers

![](Images/image06879.jpeg)

Objects of subtype Unc need a constraint,  i.e.  a start and a stop index, thus pointers to  them need also to include those. So a simple address like the one of the first component is  not  sufficient.  Note  that  A'Address  is  the  same  as  A(A'First)'Address  for  any  array  object.

For pointers of this kind, System.Address_to_Access_Conversion will probably not work  satisfactorily.

#### 13.9.3 Example

![](Images/image06880.jpeg)

Here,  CO  is  a  nominally  constrained  object,  a  pointer  to  it  need  not  store  the  constraint,  i.e.  a  thin  pointer  suffices.  In  contrast,  UO  is  an  object  of  a  nominally  unconstrained  subtype,  its  actual  subtype  is  constrained  by  the  initial  value.

![](Images/image06881.jpeg)

The  relevant  paragraphs  in  the  RM  are  difficult  to  understand.  In  short  words:

An access type's target type is called the designated subtype, in our example Unc.  RM  3.10.2(27.1/2) requires that Unc_Acc's designated subtype statically match the nominal  subtype  of  the  object.

Now the nominal subtype of CO is the constrained anonymous subtype Unc  (-1  ..  +1), the  nominal subtype of UO is the unconstrained subtype Unc.  In the illegal cases, the designated  and  nominal  subtypes  do  not  statically  match.

## 13.10  See  also

See  also

#### 13.10.1 Wikibook

• Ada  Programming[7](#part0112.xhtml__bookmark364)

• Ada  Programming/Types[8](#part0112.xhtml__bookmark365)

![](Images/image06882.jpeg)

7 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

8 [http://en.wikibooks.org/wiki/Ada%20Programming%2FTypes](http://en.wikibooks.org/wiki/Ada%20Programming%2FTypes)

#### 13.10.2 Ada  Reference  Manual

###### Ada  95

• 4.8  Allocators  ˆ{[http://www.adaic.org/resources/add_content/standards/95lrm/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-4-8.html)  [ARM_HTML/RM-4-8.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-4-8.html)

• 13.11StorageManagementˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-13-11.html)  [standards/95lrm/ARM_HTML/RM-13-11.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-13-11.html)

• 13.11.2  Unchecked  Storage  Deallocation  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-13-11-2.html)  [content/standards/95lrm/ARM_HTML/RM-13-11-2.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-13-11-2.html)

• 3.7Discriminantsˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-7.html)  [95lrm/ARM_HTML/RM-3-7.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-7.html)

• 3.10  Access  Types  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-10.html)  [95lrm/ARM_HTML/RM-3-10.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-10.html)

• 6.1  Subprogram  Declarations  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-6-1.html)  [standards/95lrm/ARM_HTML/RM-6-1.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-6-1.html)

• B.3  Interfacing  with  C  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-B-3.html)  [95lrm/ARM_HTML/RM-B-3.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-B-3.html)

###### Ada  2005

• 4.8  Allocators  ˆ{[http://www.adaic.org/resources/add_content/standards/05rm/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-8.html)  [html/RM-4-8.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-8.html)

• 13.11StorageManagementˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-13-11.html)  [standards/05rm/html/RM-13-11.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-13-11.html)

• 13.11.2  Unchecked  Storage  Deallocation  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-13-11-2.html)  [content/standards/05rm/html/RM-13-11-2.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-13-11-2.html)

• 3.7Discriminantsˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-7.html)  [05rm/html/RM-3-7.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-7.html)

• 3.10  Access  Types  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-10.html)  [05rm/html/RM-3-10.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-10.html)

• 6.1  Subprogram  Declarations  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-6-1.html)  [standards/05rm/html/RM-6-1.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-6-1.html)

• B.3  Interfacing  with  C  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-B-3.html)  [05rm/html/RM-B-3.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-B-3.html)

#### 13.10.3 Ada  Quality  and  Style  Guide

• 5.4.5DynamicDataˆ{[http://www.adaic.org/resources/add_content/docs/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_5/5-4-5.html)  [95style/html/sec_5/5-4-5.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_5/5-4-5.html)

• 5.9.2  Unchecked  Deallocation  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_5/5-9-2.html)  [docs/95style/html/sec_5/5-9-2.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_5/5-9-2.html)

# 14 Limited  types

## 14.1 Limited  Types

Limited  Types

When a type is declared limited this means that objects of the type cannot be assigned  values  of  the  same  type.  An  Object  b  of  limited  type  LT  cannot  be  copied  into  an  object  a  of  same  type  LT.

Additionally,  there  is  no  predefined  equality  operation  for  objects  of  a  limited  type.

The desired effects of declaring a type limited include prevention of shallow copying. Also,  the (unique) identity of an object is retained: once declared, a name of a variable of type LT  will  continue  to  refer  to  the  same  object.

The  following  example  will  use  a  rather  simplifying  type  Boat.

![](Images/image06883.jpeg)

When  we  declare  a  variable  to  be  of  type  Boat,  its  name  will  denote  one  boat  from  then  on.  Boats  will  not  be  copied  into  one  another.

The  full  view  of  a  boat  might  be  implemented  as  a  record  such  as

![](Images/image06884.jpeg)

The  Choose  function  returns  a  Boat  object  depending  on  the  parameters  Load  and  Speed.  If we now declare a variable of type Boat we will be better off Choosing an initial Boat (or  else we might be dropping into uninitialized waters!). But when we do so, the initialization  looks  suspiciously  like  assignment  which  is  not  available  with  limited  types:

![](Images/image06885.jpeg)

Fortunately, current Ada distinguishes initialization from copying. Objects of a limited type  may  be  initialized  by  an  initialization  expression  on  the  right  of  the  delimiter  :=  .

(Just to prevent confusion: The Ada Reference Manual discriminates between assignment  and assignment statement, where assignment is part of the assignment statement.  An  initialisation is of course an assignment which,  for limited types,  is done in  place.  An  assignment  statement  involves  copying,  which  is  forbidden  for  limited  types.)

Related  to  this  feature  are  aggregates  of  limited  types[1](#part0116.xhtml__bookmark368)  and  “constructor  functions”  for  limited  types. Internally,  the  implementation  of  the  Choose  function  will  return  a limited record.  However, since the return type Boat is limited, there must be no  copying anywhere. Will this work? A first attempt might be to declare a result variable  local  to  Choose,  manipulate  result,  and  return  it.  The  result  object  needs  to  be  “transported” into the calling environment. But result is a variable local to Choose.  When Choose returns, result will no longer be in scope.  Therefore it looks like result  must be copied but this is not permitted for limited types.  There are two solutions  provided  by  the  language:  extended  return  statements  (see  6.5  Return  Statements  ˆ{[http:](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-6-5.html)

[//www.adaic.org/resources/add_content/standards/05rm/html/RM-6-5.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-6-5.html)  )  and  aggregates of limited types. The following body of Choose returns an aggregate of limited  type  Boat,  after  finding  the  initial  values  for  its  components.

![](Images/image06886.jpeg)

The  object  that  is  returned  is  at  the  same  time  the  object  that  is  to  have  the  returned  value.  The  function  therefore  initializes  Henrietta  in  place.

In  parallel  to  the  predefined  type  Ada  .Controlled,  Ada  provides  the  type  Limited_-  Controlled  in  the  same  package.  It  is  a  limited  version  of  the  former.

![](Images/image06887.jpeg)

1[http://www.adacore.com/2007/05/14/gem-1/](http://www.adacore.com/2007/05/14/gem-1/)

## 14.2 Initialising  Limited  Types

Initialising  Limited  Types

A  few  methods  to  initialise  such  types  are  presented.

![](Images/image06888.jpeg)

![](Images/image06889.jpeg)

![](Images/image06890.jpeg)

Note  that  D3  is  a  constant,  whereas  all  others  are  variables.

Also note that the initial value that is defined for the component of Preinitialised is  evaluated  at  the  time  of  object  creation,  i.e.  if  an  expression  is  used  instead  of  the  literal,  the  value  can  be  run-time  dependent.

![](Images/image06891.jpeg)

In  this  declaration  of  two  objects,  the  initial  expression  will  be  evaluated  twice  and  can  deliver  different  values,  because  it  is  equivalent  to  the  sequence[2](#part0118.xhtml__bookmark371):

![](Images/image06892.jpeg)

So  X  is  initialised  before  Y.

## 14.3 See  also

See  also

#### 14.3.1 Ada  95  Reference  Manual

• 7.5  Limited  Types  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-7-5.html)  [95lrm/ARM_HTML/RM-7-5.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-7-5.html)

![](Images/image06893.jpeg)

2 ISO/IEC  8652:2007.  3.3.1  Object  Declarations  (7).  Ada  2005  Reference  Manual.  Any  declaration  [...]  with  more  than  one  defining_identifier  is  equivalent  to  a  series  of  declarations  each  containing  one defining_identifier from the list, [...] in the same order as the list.  ˆ{[http://www.adaic.org/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-3-1.html)  [resources/add_content/standards/05rm/html/RM-3-3-1.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-3-1.html)

#### 14.3.2 Ada  2005  Reference  Manual

• 7.5  Limited  Types  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-7-5.html)  [05rm/html/RM-7-5.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-7-5.html)

#### 14.3.3 Ada  Quality  and  Style  Guide

• 5.3.3PrivateTypesˆ{[http://www.adaic.org/resources/add_content/docs/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_5/5-3-3.html)  [95style/html/sec_5/5-3-3.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_5/5-3-3.html)

• 8.3.3  Formal  Private  and  Limited  Private  Types  ˆ{[http://www.adaic.org/resources/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_8/8-3-3.html)  [add_content/docs/95style/html/sec_8/8-3-3.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_8/8-3-3.html)

## 14.4 References

References

# 15 Strings

Ada supports three different types of strings.  Each string type is designed to solve a different  problem.

In addition, every string type is implemented for each available Characters type (Character,  Wide_Character,  Wide_Wide_Character)  giving  a  complement  of  nine  combinations.

## 15.1 Fixed-length  string  handling

Fixed-length  string  handling

Fixed-Length  Strings  are  arrays[1](#part0121.xhtml__bookmark375)  of  Character,  and  consequently  of  a  fixed  length.  Since  a fixed length string is an indefinite subtype[2](#part0121.xhtml__bookmark376) the length does not need to be known at  compile  time  —  the  length  may  well  be  calculated  at  run  time.  In  the  following  example  the  length  is  calculated  from  command-line  argument  1:

![](Images/image06894.jpeg)

However  once  the  length  has  been  calculated  and  the  strings  have  been  created  the  length  stays  constant.  Try  the  following  program  which  shows  a  typical  mistake:

![](Images/image06895.jpeg)![](Images/image06896.jpeg)

1 Chapter  [11](#part0085.xhtml__bookmark293)  on  page  [83](#part0085.xhtml__bookmark293)

2 [http://en.wikibooks.org/wiki/ada%20Programming%2FSubtypes%23indefinite%20subtype](http://en.wikibooks.org/wiki/ada%20Programming%2FSubtypes%23indefinite%20subtype)

![](Images/image06897.jpeg)

The  program  will  only  work  when  the  1st  and  2nd  parameter  have  the  same  length.  This  is even true when the 2nd parameter is shorter. There is neither an automatic padding of  shorter  strings  nor  an  automatic  truncation  of  longer  strings.

Having said that, the package Ada  contains a set of procedures and functions for Fixed-  Length String Handling which allows padding of shorter strings and truncation of longer  strings.

Try  the  following  example  to  see  how  it  works:

![](Images/image06898.jpeg)

![](Images/image06899.jpeg)

## 15.2 Bounded-length  string  handling

Bounded-length  string  handling

Bounded-Length Strings can be used when the maximum length of a string is known and/or  restricted. This is often the case in database applications where only a limited number of  characters  can  be  stored.

Like  Fixed-Length  Strings  the  maximum  length  does  not  need  to  be  known  at  compile  time

—  it  can  also  be  calculated  at  runtime  —  as  the  example  below  shows:

![](Images/image06900.jpeg)

You should know that Bounded-Length Strings have some distinct disadvantages.  Most  noticeable is that each Bounded-Length String is a different type which makes converting  them rather cumbersome. Also a Bounded-Length String type always allocates memory for  the maximum permitted string length for the type. The memory allocation for a Bounded-  Length  String  is  equal  to  the  maximum  number  of  string  "characters"  plus  an  implementation  dependent number containing the string length (each character can require allocation of  more  than  one  byte  per  character,  depending  on  the  underlying  character  type  of  the  string,

and the length number is 4 bytes long for the Windows GNAT Ada compiler v3.15p, for  example).

## 15.3 Unbounded-length  string  handling

Unbounded-length  string  handling

Last but not least there is the Unbounded-Length String.  In fact:  If you are not doing  embedded or database programming this will be the string type you are going to use most  often  as  it  gives  you  the  maximum  amount  of  flexibility.

As the name suggest the Unbounded-Length String can hold strings of almost any length —  limited only to the value of Integer'Last or your available heap memory.  This is because  Unbounded_String  type  is  implemented  using  dynamic  memory  allocation  behind  the  scenes,  providing  lower  efficiency  but  maximum  flexibility.

![](Images/image06901.jpeg)

![](Images/image06902.jpeg)

As  you  can  see  the  Unbounded-Length  String  example  is  also  the  shortest  (discarding  the  first  example,  which  is  buggy)  —  this  makes  using  Unbounded-Length  Strings  very  appealing.

## 15.4 See  also

See  also

#### 15.4.1 Wikibook

• Ada  Programming[3](#part0125.xhtml__bookmark380)

#### 15.4.2 Ada  95  Reference  Manual

• 2.6  String  Literals  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-2-6.html)  [95lrm/ARM_HTML/RM-2-6.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-2-6.html)

• 3.6.3  String  Types  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-6-3.html)  [95lrm/ARM_HTML/RM-3-6-3.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-6-3.html)

• A.4.3Fixed-LengthStringHandlingˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-A-4-3.html)  [content/standards/95lrm/ARM_HTML/RM-A-4-3.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-A-4-3.html)

• A.4.4  Bounded-Length  String  Handling  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-A-4-4.html)  [content/standards/95lrm/ARM_HTML/RM-A-4-4.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-A-4-4.html)

• A.4.5  Unbounded-Length  String  Handling  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-A-4-5.html)  [content/standards/95lrm/ARM_HTML/RM-A-4-5.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-A-4-5.html)

#### 15.4.3 Ada  2005  Reference  Manual

• 2.6  String  Literals  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-6.html)  [05rm/html/RM-2-6.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-6.html)

• 3.6.3  String  Types  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-6-3.html)  [05rm/html/RM-3-6-3.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-6-3.html)

• A.4.3Fixed-LengthStringHandlingˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-4-3.html)  [content/standards/05rm/html/RM-A-4-3.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-4-3.html)

• A.4.4  Bounded-Length  String  Handling  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-4-4.html)  [content/standards/05rm/html/RM-A-4-4.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-4-4.html)

• A.4.5  Unbounded-Length  String  Handling  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-4-5.html)  [content/standards/05rm/html/RM-A-4-5.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-4-5.html)

![](Images/image06903.jpeg)

3 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

# 16 Subprograms

In Ada the subprograms are classified into two categories: procedures[1](#part0127.xhtml__bookmark382) and functions[2](#part0127.xhtml__bookmark383). A  procedures call is a statement and does not return any value, whereas a function returns a  value  and  must  therefore  be  a  part  of  an  expression.

Subprogram  parameters  may  have  three  modes.

###### in

The  actual  parameter  value  goes  into  the  call  and  is  not  changed  there.  The  formal  parameter is a constant and allows only reading. This is the default when no mode is given.  The  actual  parameter  is  an  expression.

###### in  out

The  actual  parameter  goes  into  the  call  and  may  be  redefined.  The  formal  parameter  is  a  variable  and  can  be  read  and  written.

###### out

The actual parameter's value before the call is irrelevant, it will get a value in the call. The  formal  parameter  can  be  read  and  written.  (In  Ada  83  out  parameters  were  write-only.)

A  parameter  of  any  mode  may  also  be  explicitly  aliased.  access

The formal parameter is an access (a pointer) to some variable. (This is not a parameter  mode  from  the  reference  manual  point  of  view.)

Note  that  parameter  modes  do  not  specify  the  parameter  passing  method.  Their  purpose  is  to  document  the  data  flow.

The parameter passing method depends on the type of the parameter. A rule of thumb is  that parameters fitting into a register are passed by copy, others are passed by reference.  For certain types, there are special rules, for others the parameter passing mode is left to  the compiler (which you can assume to do what is most sensible). Tagged types are always  passed  by  reference.

Explicitly  aliased  parameters  and  access  parameters  specify  pass  by  reference.

Unlike  in  the  C  class  of  programming  languages,  Ada  subprogram  calls  cannot  have  empty  parameters  parentheses  (  )  when  there  are  no  parameters.

![](Images/image06904.jpeg)

1 Chapter  [16.1](#part0128.xhtml__bookmark384)  on  page  [126](#part0128.xhtml__bookmark384)

2 Chapter  [16.2](#part0129.xhtml__bookmark385)  on  page  [127](#part0129.xhtml__bookmark385)

## 16.1 Procedures

Procedures

A  procedure  call  in  Ada  constitutes  a  statement  by  itself.  For  example:

![](Images/image06905.jpeg)

When  the  procedure  is  called  with  the  statement

![](Images/image06906.jpeg)

the expressions 5 + P and 48 are evaluated (expressions are only allowed for in parameters),  and  then  assigned  to  the  formal  parameters  A  and  B,  which  behave  like  constants.  Then,  the  value  A  +  B  is  assigned  to  formal  variable  C,  whose  value  will  be  assigned  to  the  actual  parameter  Q  when  the  procedure  finishes.

C,  being  an  out  parameter,  is  an  uninitialized  variable  before  the  first  assignment.  (Therefore  in Ada 83, there existed the restriction that out parameters are write-only. If you wanted to  read  the  value  written,  you  had  to  declare  a  local  variable,  do  all  calculations  with  it,  and  finally assign it to C before return. This was awkward and error prone so the restriction  was  removed  in  Ada  95.)

Within  a  procedure,  the  return  statement  can  be  used  without  arguments  to  exit  the  procedure  and  return  the  control  to  the  caller.

For  example,  to  solve  an  equation  of  the  kind  ax2  +  bx  +  c  =  0:

![](Images/image06907.jpeg)

The function SQRT calculates the square root of non-negative values. If the roots are real,  they  are  given  back  in  R1  and  R2,  but  if  they  are  complex  or  the  equation  degenerates  (A

= 0), the execution of the procedure finishes after assigning to the Valid variable the False  value, so that it is controlled after the call to the procedure. Notice that the out parameters  should  be  modified  at  least  once,  and  that  if  a  mode  is  not  specified,  it  is  implied  in.

## 16.2 Functions

Functions

A function is a subprogram that can be invoked as part of an expression. Until Ada 2005,  functions can only take in (the default) or access parameters; the latter can be used as a  work-around for the restriction that functions may not have out parameters. Ada 2012 has  removed  this  restriction.

Here  is  an  example  of  a  function  body:

![](Images/image06908.jpeg)

Or  in  Ada2012:

![](Images/image06909.jpeg)

or  even  shorter  as  an  expression  function

![](Images/image06910.jpeg)

The  formal  parameters  with  mode  in  behave  as  local  constants  whose  values  are  provided  by  the corresponding actual parameters.  The statement return is used to indicate the value  returned  by  the  function  call  and  to  give  back  the  control  to  the  expression  that  called  the function. The expression of the return statement may be of arbitrary complexity and  must be of the same type declared in the specification. If an incompatible type is used, the  compiler gives an error.  If the restrictions of a subtype are not fulfilled, e.g.  a range, it  raises  a  Constraint_Error  exception.

The  body  of  the  function  can  contain  several  return  statements  and  the  execution  of  any  of them will finish the function, returning control to the caller. If the flow of control within  the function branches in several ways, it is necessary to make sure that each one of them is  finished  with  a  return  statement.  If  at  run  time  the  end  of  a  function  is  reached  without

encountering a return statement, the exception Program_Error is raised.  Therefore, the  body  of  a  function  must  have  at  least  one  such  return  statement.

Every call  to  a  function produces a  new  copy of any  object  declared within  it.   When  the function finalizes, its objects disappear.  Therefore, it is possible to call the function  recursively.  For  example,  consider  this  implementation  of  the  factorial  function:

![](Images/image06911.jpeg)

When evaluating the expression Factorial  (4); the function will be called with parameter  4 and within the function it will try to evaluate the expression Factorial  (3), calling itself  as  a  function,  but  in  this  case  parameter  N  would  be  3  (each  call  copies  the  parameters)  and so on until N = 1 is evaluated which will finalize the recursion and then the expression  will  begin  to  be  completed  in  the  reverse  order.

A formal parameter of a function can be of any type, including vectors or records. Never-  theless,  it  cannot  be  an  anonymous  type,  that  is,  its  type  must  be  declared  before,  for  example:

![](Images/image06912.jpeg)

In this example, the function can be used on a vector of arbitrary dimension.  Therefore,  there are no static bounds in the parameters passed to the functions.  For example, it is  possible  to  be  used  in  the  following  way:

![](Images/image06913.jpeg)

In  the  same  way,  a  function  can  also  return  a  type  whose  bounds  are  not  known  a  priori.  For  example:

![](Images/image06914.jpeg)

![](Images/image06915.jpeg)

The variable Result has the same bounds as V, so the returned vector will always have the  same  dimension  as  the  one  passed  as  parameter.

A value returned by a function can be used without assigning it to a variable, it can be  referenced as an expression. For example, Invert_Components (V4) (1), where the first  element of the vector returned by the function would be obtained (in this case, the last  element  of  V4,  i.e.  7.8).

## 16.3 Named parameters

Named parameters

In subprogram calls, named parameter notation (i.e.  the name of the formal parameter  followed of the symbol => and then the actual parameter) allows the rearrangement of the  parameters  in  the  call.  For  example:

![](Images/image06916.jpeg)

This  is  especially  useful  to  make  clear  which  parameter  is  which.

![](Images/image06917.jpeg)

The  first  call  (from  Ada.Numerics.Elementary_Functions)  is  not  very  clear.  One  might  easily  confuse  the  parameters.  The  second  call  makes  the  meaning  clear  without  any  ambiguity.

Another  use  is  for  calls  with  numeric  literals:

![](Images/image06918.jpeg)

## 16.4 Default  parameters

Default  parameters

On  the  other  hand,  formal  parameters  may  have  default  values.  They  can,  therefore,  be  omitted  in  the  subprogram  call.  For  example:

![](Images/image06919.jpeg)

can  be  called  in  these  ways:

![](Images/image06920.jpeg)

In  the  first  statement,  a  "regular  call"  is  used  (with  positional  association);  the  second  also uses positional association but omits the second parameter to use the default; in the  third  statement,  all  parameters  are  by  default;  the  fourth  statement  uses  named  association  to omit the first parameter; finally, the fifth statement uses mixed association, here the  positional  parameters  have  to  precede  the  named  ones.

Note that the default expression is evaluated once for each formal parameter that has no  actual parameter. Thus, if in the above example a function would be used as defaults for A  and B, the function would be evaluated once in case 2 and 4; twice in case 3, so A and B  could  have  different  values;  in  the  others  cases,  it  would  not  be  evaluated.

## 16.5 Renaming

Renaming

Subprograms  may  be  renamed.  The  parameter  and  result  profile  for  a  renaming-as-  declaration  must  be  mode  conformant.

![](Images/image06921.jpeg)

This  may  be  especially  comfortable  for  tagged  types.

![](Images/image06922.jpeg)

![](Images/image06923.jpeg)

![](Images/image06924.jpeg)

But  note  that  Message.Print'Access;  is  illegal,  you  have  to  use  a  renaming  declaration as  above.

Since  only  mode  conformance  is  required  (and  not  full  conformance  as  between  specification  and  body),  parameter  names  and  default  values  may  be  changed  with  renamings:

![](Images/image06925.jpeg)

## 16.6 See  also

See  also

#### 16.6.1 Wikibook

• Ada  Programming[3](#part0133.xhtml__bookmark390)

• Ada  Programming/Operators[4](#part0133.xhtml__bookmark391)

#### 16.6.2 Ada  95  Reference  Manual

• Section6:Subprogramsˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-6.html)  [standards/05rm/html/RM-6.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-6.html)

• 4.4  Expressions  ˆ{[http://www.adaic.org/resources/add_content/standards/05rm/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-4.html)  [html/RM-4-4.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-4.html)

#### 16.6.3 Ada  2005  Reference  Manual

• Section6:Subprogramsˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-6.html)  [standards/05rm/html/RM-6.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-6.html)

• 4.4  Expressions  ˆ{[http://www.adaic.org/resources/add_content/standards/05rm/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-4.html)  [html/RM-4-4.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-4.html)

![](Images/image06926.jpeg)

3 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

4 Chapter  [37](#part0303.xhtml__bookmark820)  on  page  [301](#part0303.xhtml__bookmark820)

#### 16.6.4 Ada  Quality  and  Style  Guide

• 4.1.3Subprogramsˆ{[http://www.adaic.org/resources/add_content/docs/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_4/4-1-3.html)  [95style/html/sec_4/4-1-3.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_4/4-1-3.html)

es:Programación  en  Ada/Subprogramas[5](#part0134.xhtml__bookmark392)

![](Images/image06927.jpeg)

5 [http://es.wikibooks.org/wiki/Programaci%F3n%20en%20Ada%2FSubprogramas](http://es.wikibooks.org/wiki/Programaci%F3n%20en%20Ada%2FSubprogramas)

# 17 Packages

Ada  encourages  the  division  of  code  into  separate  modules  called  packages.  Each  package  can  contain  any  combination  of  items.

Some  of  the  benefits  of  using  packages  are:

• package  contents  are  placed  in  a  separate  namespace,  preventing  naming  collisions,

• implementation details of the package can be hidden from the programmer (information  hiding),

• object  orientation  requires  defining  a  type  and  its  primitive  subprograms  within  a  package,  and

• packages  can  be  separately  compiled.

Some  of  the  more  common  package  usages  are:

• a  group  of  related  subprograms  along  with  their  shared  data,  with  the  data  not  visible  outside  the  package,

• one  or  more  data  types  along  with  subprograms  for  manipulating  those  data  types,  and

• a  generic  package  that  can  be  instantiated  under  varying  conditions.

![](Images/image06928.jpeg)The  following  is  a  quote  from  the  current  Ada  Reference  Manual  7.Packages.RM  7(1)  ˆ{[http://www.adaic.org/resources/add_content/standards/05rm/html/RM-7-](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-7-.html).  [html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-7-.html)

## 17.1 Separate  compilation

Separate  compilation

It is very common for package declarations and package bodies to be coded into separate  files and separately compiled.  Doing so places the package at the library level where it will  be accessible to all other code via the with statement—if a more restricted scope is desired,  simply  declare  the  package  (and  package  body,  if  needed)  within  the  appropriate  scope.  The package body can itself be divided into multiple files by specifying that one or more  subprogram  implementations  are  separate.

One  of  the  biggest  advantages  of  Ada  over  most  other  programming  languages  is  its  well  defined system of modularization and separate compilation.  Even though Ada allows  separate compilation, it maintains the strong type checking among the various compilations  by enforcing rules of compilation order and compatibility checking.  Ada uses separate  compilation (like Modula-2[1](#part0136.xhtml__bookmark396), Java[2](#part0136.xhtml__bookmark397) and C#[3](#part0136.xhtml__bookmark398)), and not independent compilation (as C[4](#part0136.xhtml__bookmark399)/C++[5](#part0136.xhtml__bookmark400)  does), in which the various parts are compiled with no knowledge of the other compilation  units  with  which  they  will  be  combined.

A  note  to  C/C++  users:  Yes,  you  can  use  the  preprocessor  to  emulate  separate  compilation

—  but  it  is  only  an  emulation  and  the  smallest  mistake  leads  to  very  hard  to  find  bugs.  It  is  telling  that  all  C/C++ successor  languages  including  D[6](#part0136.xhtml__bookmark401)  have  turned  away  from  the  independent  compilation  and  the  use  of  the  preprocessor.

So it's good to know that Ada has had separate compilation ever since Ada-83 and is  probably  the  most  sophisticated  implementation  around.

## 17.2 Parts  of  a  package

Parts  of  a  package

A  package  generally  consists  of  two  parts,  the  specification  and  the  body.  A  package  specification  can  be  further  divided  in  two  logical  parts,  the  visible  part  and  the  private  part.  Only  the  visible  part  of  the  specification  is  mandatory.  The  private  part  of  the  specification is optional, and a package specification might not have a package body—the  package  body  only  exists  to  complete  any  incomplete  items  in  the  specification.  Subprogram  declarations are the most common incomplete items. There must not be a package body if  there  is  no  incomplete  declarations  and  there  has  to  be  a  package  body  if  there  is  incomplete  declarations  in  the  specification.

To understand the value of the three-way division, consider the case of a package that has  already been released and is in use.  A change to the visible part of the specification will  require  that  the  programmers  of  all  using  software  verify  that  the  change  does  not  affect  the  using code. A change to the private part of the declaration will require that all using code be  recompiled but no review is normally needed. Some changes to the private part can change  the  meaning  of  the  client  code  however.  An  example  is  changing  a  private  record  type  into  a private access type. This change can be done with changes in the private part, but change  the  semantic  meaning  of  assignment  in  the  clients  code.  A  change  to  the  package  body  will only require that the file containing the package body be recompiled, because nothing  outside of the package body can ever access anything within the package body (beyond the  declarations  in  the  specification  part).

A common usage of the three parts is to declare the existence of a record type and some  subprograms  that  operate  on  that  type  in  the  visible  part,  define  the  actual  structure  of  the

![](Images/image06929.jpeg)

1 [http://en.wikipedia.org/wiki/Modula-2](http://en.wikipedia.org/wiki/Modula-2)

2 [http://en.wikipedia.org/wiki/Java_programming_language](http://en.wikipedia.org/wiki/Java_programming_language)

3 [http://en.wikipedia.org/wiki/C%20Sharp%20programming%20language](http://en.wikipedia.org/wiki/C%20Sharp%20programming%20language)

4 [http://en.wikipedia.org/wiki/C%20programming%20language](http://en.wikipedia.org/wiki/C%20programming%20language)

5 [http://en.wikipedia.org/wiki/C%2B%2B](http://en.wikipedia.org/wiki/C%2B%2B)

6 [http://en.wikipedia.org/wiki/D_programming_language](http://en.wikipedia.org/wiki/D_programming_language)

record  type  in  the  private  part,  and  provide  the  code  to  implement  the  subprograms  in  the  package  body.

#### 17.2.1 The  package  specification  —  the  visible  part

The  visible  part  of  a  package  specification  describes  all  the  subprogram  specifications,  variables,  types,  constants  etc.  that  are  visible  to  anyone  who  wishes  to  use  the  package.

![](Images/image06930.jpeg)

#### 17.2.2 The  private  part

The  private  part  of  a  package  serves  two  purposes:

• To  complete  the  deferred  definition  of  private  types  and  constants.

• To  export  entities  only  visible  to  the  children  of  the  package

![](Images/image06931.jpeg)

#### 17.2.3 The  package  body

The package body defines the implementation of the package. All the subprograms defined  in the specification have to be implemented in the body.  New subprograms, types and  objects  can  be  defined  in  the  body  that  are  not  visible  to  the  users  of  the  package.

![](Images/image06932.jpeg)

![](Images/image06933.jpeg)

![](Images/image06934.jpeg)

###### pragma

Only  available  when  using  GNAT[7](#part0138.xhtml__bookmark402).

#### 17.2.4 Two  Flavors  of  Package

The packages above each define a type together with operations of the type.  When the  type's composition is placed in the private part of a package, the package then exports what  is known to be an Abstract Data Type[8](#part0138.xhtml__bookmark403)  or ADT for short.  Objects of the type are then  constructed  by  calling  one  of  the  subprograms  associated  with  the  respective  type.

A different kind of package is the Abstract State Machine.  A package will be modeling a  single  item  of  the  problem  domain,  such  as  the  motor  of  a  car.  If  a  program  controls  one  car,  there is typically just one motor, or the motor. The public part of the package specification  only  declares  the  operations  of  the  module  (of  the  motor,  say),  but  no  type.  All  data  of  the module are hidden in the body of the package where they act as state variables to be  queried, or manipulated by the subprograms of the package. The initialization part sets the  state  variables  to  their  initial  values.

![](Images/image06935.jpeg)

![](Images/image06936.jpeg)

7 [http://en.wikipedia.org/wiki/GNAT](http://en.wikipedia.org/wiki/GNAT)

8 [http://en.wikipedia.org/wiki/Abstract_data_type](http://en.wikipedia.org/wiki/Abstract_data_type)

![](Images/image06937.jpeg)

![](Images/image06938.jpeg)

(A note on construction:  The package initialization part after begin corresponds to a  construction subprogram of an ADT package. However, as a state machine is an “object”  already, “construction” is happening during package initialization. (Here it sets the state  variable  The_A  to  its  initial  value.)  An  ASM  package  can  be  viewed  as  a  singleton[9](#part0139.xhtml__bookmark405).)

## 17.3 Using  packages

Using  packages

To utilize a package it's needed to name it in a with clause, whereas to have direct visibility  of  that  package  it's  needed  to  name  it  in  a  use  clause.

For  C++  programmers,  Ada's  with  clause  is  analogous  to  the  C++  preprocessor's  #include  and Ada's use is similar to the using namespace statement in C++. In particular, use  leads to the same namespace pollution problems as using namespace and thus should be  used sparingly. Renaming can shorten long compound names to a manageable length, while  the  use  type  clause  makes  a  type's  operators  visible.  These  features  reduce  the  need  for  plain  use.

#### 17.3.1 Standard  with

The standard with clause provides visibility for the public part of a unit to the following  defined unit. The imported package can be used in any part of the defined unit, including  the  body  when  the  clause  is  used  in  the  specification.

![](Images/image06939.jpeg)

9 [http://en.wikipedia.org/wiki/Singleton_pattern](http://en.wikipedia.org/wiki/Singleton_pattern)

#### 17.3.2 Private  with

This  language  feature  is  only  available  in  Ada  2005

![](Images/image06940.jpeg)

![](Images/image06941.jpeg)

#### 17.3.3 Limited  with

This  language  feature  is  only  available  in  Ada  2005

![](Images/image06942.jpeg)

![](Images/image06943.jpeg)

![](Images/image06944.jpeg)

#### 17.3.4 Making  operators  visible

Suppose  you  have  a  package  Universe  that  defines  some  numeric  type  T.

![](Images/image06945.jpeg)

This  program  fragment  is  illegal  since  the  operators  implicitly  defined  in  Universe  are  not  directly  visible.

You  have  four  choices  to  make  the  program  legal.

Use  a  use_package_clause.  This  makes  all  declarations  in  Universe  directly  visible  (provided  they  are  not  hidden  because  of  other  homographs).

![](Images/image06946.jpeg)

Use  renaming.  This  is  error  prone  since  if  you  rename  many  operators,  cut  and  paste  errors  are  probable.

![](Images/image06947.jpeg)

Use  qualification.  This  is  extremely  ugly  and  unreadable.

![](Images/image06948.jpeg)

Use  the  use_type_clause.  This  makes  only  the  operators  in  Universe  directly  visible.

![](Images/image06949.jpeg)

There  is  a  special  beauty  in  the  use_type_clause.  Suppose  you  have  a  set  of  packages  like  so:

![](Images/image06950.jpeg)

![](Images/image06951.jpeg)

Now you've got into trouble. Since Universe is not made visible, you cannot use a use_-  package_clause for Universe to make the operator directly visible, nor can you use qualifi-  cation for the same reason. Also a use_package_clause for Pack does not help, since the  operator  is  not  defined  in  Pack.  The  effect  of  the  above  construct  means  that  the  operator  is  not  nameable,  i.e.  it  cannot  be  renamed  in  a  renaming  statement.

Of course you can add Universe to the context clause, but this may be impossible due to  some other reasons (e.g.  coding standards); also adding the operators to Pack may be  forbidden  or  not  feasible.  So  what  to  do?

The  solution  is  simple.  Use  the  use_type_clause  for  Pack.T  and  all  is  well!

![](Images/image06952.jpeg)

## 17.4 Package  organisation

Package  organisation

#### 17.4.1 Nested  packages

A nested package is a package declared inside a package. Like a normal package, it has a  public  part  and  a  private  part.  From  outside,  items  declared  in  a  nested  package  N  will  have visibility as usual; the programmer may refer to these items using a full dotted name  like  P.N.X.  (But  not  P.M.Y.)

![](Images/image06953.jpeg)

Inside a package, declarations become visible as they are introduced, in textual order. That  is, a nested package N that is declared after some other declaration D can refer to this  declaration D. A declaration E following N can refer to items of N[10](#part0143.xhtml__bookmark409). But neither can “look  ahead”  and  refer  to  any  declaration  that  goes  after  them.  For  example,  spec  N  above  cannot  refer  to  M  in  any  way.

In  the  following  example,  a  type  is  derived  in  both  of  the  two  nested  packages  Disks  and

Books.  Notice  that  the  full  declaration  of  parent  type  Item  appears  before  the  two  nested

![](Images/image06954.jpeg)

10 For  example,  E:  Integer := D + N.X;

packages.

![](Images/image06955.jpeg)

![](Images/image06956.jpeg)

A package may also be nested inside a subprogram.  In fact, packages can be declared in any  declarative  part,  including  those  of  a  block.

#### 17.4.2 Child  packages

Ada allows one to extend the functionality of a unit (package) with so-called children (child  packages). With certain exceptions, all the functionality of the parent is available to a child.  This means that all public and private declarations of the parent package are visible to all  child  packages.

The above example, reworked as a hierarchy of packages, looks like this.  Notice that the  package Ada  is not needed by the top level package Shelf, hence its with clause doesn't  appear  here.  (We  have  added  a  match  function  for  searching  a  shelf,  though):

![](Images/image06957.jpeg)

The  name  of  a  child  package  consists  of  the  parent  unit's  name  followed  by  the  child  package's  identifier,  separated  by  a  period  (dot)  ‘.  '.

![](Images/image06958.jpeg)

![](Images/image06959.jpeg)

Book has two components of type Unbounded_String, so Ada  appears in a with clause of  the child package.  This is unlike the nested packages case which requires that all units  needed by any one of the nested packages be listed in the context clause of the enclosing  package  (see  10.1.2  Context  Clauses  -  With  Clauses  ˆ{[http://www.adaic.org/resources/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-10-1-2.html)  [add_content/standards/05rm/html/RM-10-1-2.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-10-1-2.html) ).  Child  packages  thus  give  better  control  over  package  dependences.  With  clauses  are  more  local.

The new child package Shelf.Disks looks similar. The Boxes package which was a nested  package in the private part of the original Shelf package is moved to a private child  package:

![](Images/image06960.jpeg)

The privacy of the package means that it can only be used by equally private client units.  These clients include private siblings and also the bodies of siblings (as bodies are never  public).

Child packages may be listed in context clauses just like normal packages. A with of a child  also  'withs'  the  parent.

#### 17.4.3 Subunits

A subunit is just a feature to move a body into a place of its own when otherwise the  enclosing body will become too large. It can also be used for limiting the scope of context  clauses.

The subunits allow to physically divide a package into different compilation units without  breaking the logical unity of the package. Usually each separated subunit goes to a different  file allowing separate compilation of each subunit and independent version control history  for  each  one.

![](Images/image06961.jpeg)

## 17.5 Notes

Notes

## 17.6 See  also

See  also

#### 17.6.1 Wikibook

• Ada  Programming[11](#part0147.xhtml__bookmark412)

#### 17.6.2 Wikipedia

• Module[12](#part0147.xhtml__bookmark413)

#### 17.6.3 Ada  95  Reference  Manual

• Annex  7:  Packages[13](#part0147.xhtml__bookmark414)

#### 17.6.4 Ada  2005  Reference  Manual

• Annex  7:  Packages[14](#part0147.xhtml__bookmark415)

![](Images/image06962.jpeg)

11 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

12 [http://en.wikipedia.org/wiki/Module%20%28programming%29](http://en.wikipedia.org/wiki/Module%20%28programming%29)

13 [http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-7.html](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-7.html)

14 [http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-7.html](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-7.html)

# 18 Input  Output

## 18.1 Overview

Overview

The standard Ada libraries provide several Input/Output facilities, each one adapted to  specific  needs.  Namely,  the  language  defines  the  following  dedicated  packages:

• Text_IO

• Sequential_IO

• Direct_IO

• Stream_IO

The programmer must choose the adequate package depending on the application needs.  For example, the following properties of the data handled by the application should be  considered:

• Data  contents:  plain  text,  or  binary  data?

• Accessing  the  data:  random  access, or sequential access?

• Medium:  data  file,  console,  network/data-bus?

• Data  structure:  homogeneous  file  (sequence  of  the  same  data  field),  heterogeneous  file  (different  data  fields)?

• Data  format:  adherence  to  an  existing  data  format,  or  the  application  can  freely  choose  a  new  one?

For  example,  Stream_IO  is  very  powerful  and  can  handle  complex  data  structures  but  can  be  heavier  than  other  packages;  Sequential_IO  is  lean  and  easy  to  use  but  cannot  be  used  by  applications  requiring  random  data  access;  Text_IO  can  handle  just  textual  data,  but  it  is  enough  for  handling  the  command-line  console.

The  following  table  gives  some  advices  for  choosing  the  more  adequate  one:

| Simple  heuristics  for  choosing  an  I/O  package |
| Data  access | Plain  text | Binary  data |
| Homogeneous | Heterogeneous |
| Sequential | Text_IO | Sequential_IO | Stream_IO |
| Random | Text_IO | Direct_IO | Stream_IO |
|  |  |  |  |

So  the  most  important lesson  to  learn  is choosing  the  right one.  This  chapter will  describe  more  in  detail  these  standard  packages,  explaining  how  to  use  them  effectively.  Besides  these  Ada-defined  packages  for  general  I/O  operations  each  Ada  compiler  usually  has  other

implementation-defined Input-Output facilities, and there are also other external libraries  for  specialized  I/O  needs[1](#part0150.xhtml__bookmark420)  like  XML  processing  or  interfacing  with  databases.

## 18.2 Text  I/O

Text  I/O

Text I/O[2](#part0150.xhtml__bookmark421) is probably the most used Input/Output package.  All data inside the file are  represented by human readable text. Text I/O provides support for line and page layout  but  the  standard  is  free  form  text.

![](Images/image06963.jpeg)

It also contains several generic packages for converting numeric and enumeration types to  character strings, or for handling Bounded and Unbounded strings, allowing the program-  mer to read and write different data types in the same file easily (there are ready-to-use  instantiations of these generic packages for the Integer, Float, and Complex types). Finally,  the same family of Ada.Text_IO packages (including the several children and instantiation  packages)  for  the  type  Wide_Character  and  Wide_Wide_Character.

It  is  worth  noting  that  the  family  of  Text_IO  packages  provide  some  automatic  text  processing.  For example, the Get_Line ignores white spaces at the beginning of a line  (Get_Immediate  does  not  present  this  behavior),  or  adding  a  newline  character  when  closing  the file.  This is thus adequate for applications handling simple textual data,  but users  requiring direct management of text (e.g.  raw access to the character encoding) must  consider  other  packages  like  Sequential_IO.

## 18.3 Direct  I/O

Direct  I/O

Direct I/O is used for random access files which contain only elements of one specific type.  With Direct_IO you can position the file pointer to any element of that type (random access),  however you can't freely choose the element type, the element type needs to be a definite  subtype[3](#part0150.xhtml__bookmark422).

![](Images/image06964.jpeg)

1 [http://en.wikibooks.org/wiki/Ada%20Programming%23Other%20Language%20Libraries](http://en.wikibooks.org/wiki/Ada%20Programming%23Other%20Language%20Libraries)

2 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO)

3 [http://en.wikibooks.org/wiki/ada%20Programming%2FSubtypes%23definite_subtype](http://en.wikibooks.org/wiki/ada%20Programming%2FSubtypes%23definite_subtype)

## 18.4 Sequential  I/O

Sequential  I/O

Direct  I/O  is  used  for  random  access  files  which  contain  only  elements  of  one  specific  type. With Sequential_IO it is the other way round: you can choose between definite[4](#part0151.xhtml__bookmark426) and  indefinite[5](#part0151.xhtml__bookmark427)  element  types  but  you  have  to  read  and  write  the  elements  one  after  the  other.

## 18.5 Stream  I/O

Stream  I/O

Stream I/O is the most powerful input/output package which Ada provides. Stream I/O  allows  you  to  mix  objects  from  different  element  types  in  one  sequential  file.  In  order  to  read/write  from/to  a  stream  each  type  provides  a  'Read[6](#part0151.xhtml__bookmark428)  and  'Write[7](#part0151.xhtml__bookmark429)  attribute  as  well  as  an 'Input[8](#part0151.xhtml__bookmark430) and 'Output[9](#part0151.xhtml__bookmark431) attribute. These attributes are automatically generated for each  type  you  declare.

The 'Read[10](#part0151.xhtml__bookmark432)  and 'Write[11](#part0151.xhtml__bookmark433)  attributes treat the elements as raw data.  They are suitable for  low  level  input/output  as  well  as  interfacing  with  other  programming  languages.

The 'Input[12](#part0151.xhtml__bookmark434) and 'Output[13](#part0151.xhtml__bookmark435) attribute add additional control informations to the file, like for  example  the  'First[14](#part0151.xhtml__bookmark436)  and  'Last[15](#part0151.xhtml__bookmark437)  attributes  from  an  array.

In object orientated programming you can also use the 'Class[16](#part0151.xhtml__bookmark438)'Input[17](#part0151.xhtml__bookmark439) and 'Class[18](#part0151.xhtml__bookmark440)'Output[19](#part0151.xhtml__bookmark441)  attributes  -  they  will  store  and  recover  the  actual  object  type  as  well.

Stream  I/O  is  also  the  most  flexible  input/output  package.  All  I/O  attributes  can  be  replaced  with  user  defined  functions  or  procedures  using  representation  clauses  and  you  can  provide  your  own  Stream  I/O  types  using  flexible  object  oriented  techniques.

## 18.6 See  also

![](Images/image06965.jpeg)

4 [http://en.wikibooks.org/wiki/ada%20Programming%2FSubtypes%23definite_subtype](http://en.wikibooks.org/wiki/ada%20Programming%2FSubtypes%23definite_subtype)

5 [http://en.wikibooks.org/wiki/ada%20Programming%2FSubtypes%23Ada%20Programming%](http://en.wikibooks.org/wiki/ada%20Programming%2FSubtypes%23Ada%20Programming%2FSubtypes%23indefinite_subtype)  [2FSubtypes%23indefinite_subtype](http://en.wikibooks.org/wiki/ada%20Programming%2FSubtypes%23Ada%20Programming%2FSubtypes%23indefinite_subtype)

6 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Read](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Read)

7 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Write](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Write)

8 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Input](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Input)

9 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Output](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Output)

10 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Read](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Read)

11 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Write](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Write)

12 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Input](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Input)

13 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Output](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Output)

14 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27First](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27First)

15 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Last](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Last)

16 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Class](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Class)

17 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Input](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Input)

18 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Class](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Class)

19 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Output](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Output)

See  also

#### 18.6.1 Wikibook

• Ada  Programming[20](#part0152.xhtml__bookmark442)

• Ada Programming/Libraries/Ada.Direct_IO[21](#part0152.xhtml__bookmark443)

• Ada  Programming/Libraries/Ada.Sequential_IO[22](#part0152.xhtml__bookmark444)

• Ada  Programming/Libraries/Ada.Streams[23](#part0152.xhtml__bookmark445)

• Ada  Programming/Libraries/Ada.Streams.Stream_IO[24](#part0152.xhtml__bookmark446)

• Ada  Programming/Libraries/Ada.Text_IO.Text_Streams[25](#part0152.xhtml__bookmark447)

• Ada  Programming/Libraries/Ada.Text_IO[26](#part0152.xhtml__bookmark448)

• Ada  Programming/Libraries/Ada.Text_IO.Enumeration_IO[27](#part0152.xhtml__bookmark449)  (nested  package)

• Ada  Programming/Libraries/Ada.Text_IO.Integer_IO[28](#part0152.xhtml__bookmark450)  (nested  package)

• Ada  Programming/Libraries/Ada.Text_IO.Modular_IO[29](#part0152.xhtml__bookmark451)  (nested  package)

• Ada  Programming/Libraries/Ada.Text_IO.Float_IO[30](#part0152.xhtml__bookmark452)   (nested  package)

• Ada  Programming/Libraries/Ada.Text_IO.Fixed_IO[31](#part0152.xhtml__bookmark453)   (nested  package)

• Ada  Programming/Libraries/Ada.Text_IO.Decimal_IO[32](#part0152.xhtml__bookmark454)  (nested  package)

• Ada Programming/Libraries/Ada.Text_IO.Bounded_IO[33](#part0152.xhtml__bookmark455)

• Ada Programming/Libraries/Ada.Text_IO.Unbounded_IO[34](#part0152.xhtml__bookmark456)

• Ada  Programming/Libraries/Ada.Text_IO.Complex_IO[35](#part0152.xhtml__bookmark457)  (specialized  needs  annex)

• Ada  Programming/Libraries/Ada.Text_IO.Editing[36](#part0152.xhtml__bookmark458)  (specialized  needs  annex)

• Ada Programming/Libraries/Ada.Integer_Text_IO[37](#part0152.xhtml__bookmark459)

• Ada  Programming/Libraries/Ada.Float_Text_IO[38](#part0152.xhtml__bookmark460)

• Ada  Programming/Libraries/Ada.Complex_Text_IO[39](#part0152.xhtml__bookmark461)  (specialized  needs  annex)

• Ada  Programming/Libraries/Ada.Storage_IO[40](#part0152.xhtml__bookmark462)  (not  a  general-purpose  I/O  package)

• Ada  Programming/Libraries/Ada.IO_Exceptions[41](#part0152.xhtml__bookmark463)

• Ada  Programming/Libraries/Ada.Command_Line[42](#part0152.xhtml__bookmark464)

![](Images/image06966.jpeg)

20 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

21 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Direct_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Direct_IO)

22 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Sequential_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Sequential_IO)

23 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Streams](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Streams)

24 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Streams.Stream_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Streams.Stream_IO)

25 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Text_Streams](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Text_Streams)

26 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO)

27 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Enumeration_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Enumeration_IO) [IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Enumeration_IO)

28 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Integer_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Integer_IO)

29 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Modular_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Modular_IO)

30 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Float_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Float_IO)

31 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Fixed_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Fixed_IO)

32 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Decimal_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Decimal_IO)

33 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Bounded_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Bounded_IO)

34 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Unbounded_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Unbounded_IO)

35 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Complex_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Complex_IO)

36 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Editing](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Editing)

37 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Integer_Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Integer_Text_IO)

38 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Float_Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Float_Text_IO)

39 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Complex_Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Complex_Text_IO)

40 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Storage_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Storage_IO)

41 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.IO_Exceptions](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.IO_Exceptions)

42 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Command_Line](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Command_Line)

• Ada  Programming/Libraries/Ada.Directories[43](#part0153.xhtml__bookmark465)

• Ada  Programming/Libraries/Ada.Environment_Variables[44](#part0153.xhtml__bookmark466)

• Ada  Programming/Libraries/GNAT.IO[45](#part0153.xhtml__bookmark467)  (implementation  defined)

• Ada  Programming/Libraries/GNAT.IO_Aux[46](#part0153.xhtml__bookmark468)  (implementation  defined)

• Ada  Programming/Libraries/GNAT.Calendar.Time_IO[47](#part0153.xhtml__bookmark469)  (implementation  defined)

• Ada  Programming/Libraries/System.IO[48](#part0153.xhtml__bookmark470) (implementation  defined)

• Ada  Programming/Libraries[49](#part0153.xhtml__bookmark471)

• Ada Programming/Libraries/GUI[50](#part0153.xhtml__bookmark472)

• Ada  Programming/Libraries/Web[51](#part0153.xhtml__bookmark473)

• Ada  Programming/Libraries/Database[52](#part0153.xhtml__bookmark474)

• Ada  Programming/Platform[53](#part0153.xhtml__bookmark475)

• Ada  Programming/Platform/Linux[54](#part0153.xhtml__bookmark476)

• Ada  Programming/Platform/Windows[55](#part0153.xhtml__bookmark477)

#### 18.6.2 Ada  Reference  Manual

• A.6Input-Outputˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-6.html)  [05rm/html/RM-A-6.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-6.html)

• A.7  External  Files  and  File  Objects  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-7.html)  [content/standards/05rm/html/RM-A-7.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-7.html)

• A.8  Sequential  and  Direct  Files  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-8.html)  [standards/05rm/html/RM-A-8.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-8.html)

• A.10TextInput-Outputˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-10.html)  [standards/05rm/html/RM-A-10.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-10.html)

• A.11  Wide  Text  Input-Output  and  Wide  Wide  Text  Input-Output  ˆ{[http://www.adaic.](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-11.html)  [org/resources/add_content/standards/05rm/html/RM-A-11.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-11.html)

• A.12StreamInput-Outputˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-12.html)  [standards/05rm/html/RM-A-12.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-12.html)

• A.13  Exceptions  in  Input-Output  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-13.html)  [standards/05rm/html/RM-A-13.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-13.html)

• A.14  File  Sharing  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-14.html)  [05rm/html/RM-A-14.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-14.html)

![](Images/image06967.jpeg)

43 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Directories](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Directories)

44 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Environment_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Environment_Variables)  [Variables](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Environment_Variables)

45 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.IO)

46 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.IO_Aux](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.IO_Aux)

47 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Calendar.Time_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Calendar.Time_IO)

48 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FSystem.IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FSystem.IO)

49 Chapter  [40](#part0333.xhtml__bookmark1359)  on  page  [331](#part0333.xhtml__bookmark1359)

50 Chapter  [48](#part0363.xhtml__bookmark1717)  on  page  [361](#part0363.xhtml__bookmark1717)

51 Chapter  [51](#part0373.xhtml__bookmark1745)  on  page  [371](#part0373.xhtml__bookmark1745)

52 Chapter  [50](#part0367.xhtml__bookmark1744)  on  page  [365](#part0367.xhtml__bookmark1744)

53 Chapter  [53](#part0377.xhtml__bookmark1761)  on  page  [375](#part0377.xhtml__bookmark1761)

54 Chapter  [54](#part0379.xhtml__bookmark1770)  on  page  [377](#part0379.xhtml__bookmark1770)

55 Chapter  [55](#part0381.xhtml__bookmark1781)  on  page  [379](#part0381.xhtml__bookmark1781)

#### 18.6.3 Ada  95  Quality  and  Style  Guide

• 7.7  Input/Output  ˆ{[http://www.adaic.org/resources/add_content/docs/95style/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/7-7.html)  [html/sec_7/7-7.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/7-7.html)

• 7.7.1  Name  and  Form  Parameters  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/7-7-1.html)  [content/docs/95style/html/sec_7/7-7-1.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/7-7-1.html)

• 7.7.2FileClosingˆ{[http://www.adaic.org/resources/add_content/docs/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/7-7-2.html)  [95style/html/sec_7/7-7-2.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/7-7-2.html)

• 7.7.3  Input/Output  on  Access  Types  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/7-7-3.html)  [content/docs/95style/html/sec_7/7-7-3.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/7-7-3.html)

• 7.7.4  Package  Ada.Streams.Stream_IO  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/7-7-4.html)  [content/docs/95style/html/sec_7/7-7-4.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/7-7-4.html)

• 7.7.5  Current  Error  Files  ˆ{[http://www.adaic.org/resources/add_content/docs/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/7-7-5.html)  [95style/html/sec_7/7-7-5.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/7-7-5.html)

# 19 Exceptions

## 19.1 Robustness

Robustness

Robustness  is  the  ability  of  a  system  or  system  component  to  behave  “reasonably”  when  it  detects  an  anomaly,  e.g.:

• It  receives  invalid  inputs.

• Another  system  component  (hardware  or  software)  malfunctions.

Take as example a telephone exchange control program. What should the control program  do when a line fails? It is unacceptable simply to halt — all calls will then fail. Better would  be to abandon the current call (only), record that the line is out of service, and continue.  Better  still  would  be  to  try  to  reuse  the  line  —  the  fault  might  be  transient.  Robustness  is desirable in all systems, but it is essential in systems on which human safety or welfare  depends,  e.g.,  hospital  patient  monitoring,  aircraft  fly-by-wire,  nuclear  power  station  control,  etc.

## 19.2 Modules, preconditions and  postconditions

Modules,  preconditions  and  postconditions

A module may be specified in terms of its preconditions and postconditions.  A precondition  is a condition that the module’s inputs are supposed to satisfy. A postcondition is a condition  that the module’s outputs are required to satisfy, provided that the precondition is satisfied.  What  should  a  module  do  if  its  precondition  is  not  satisfied?

• Halt?  Even  with  diagnostic  information,  this  is  generally  unacceptable.

• Use  a  global  result  code?  The  result  code  can  be  set  to  indicate  an  anomaly.  Subsequently  it may be tested by a module that can effect error recovery. Problem: this induces tight  coupling  among  the  modules  concerned.

• Each  module  has  its  own  result  code?  This  is  a  parameter  (or  function  result)  that  may  be set to indicate an anomaly, and is tested by calling modules.  Problems:  (1) setting  and testing result codes tends to swamp the normal-case logic and (2) the result codes  are  normally  ignored.

• Exception  handling  —  Ada’s  solution.  A  module  detecting  an  anomaly  raises  an  exception.  The  same,  or  another,  module  may  handle  that  exception.

The  exception  mechanism  permits  clean,  modular  handling  of  anomalous  situations:

• A unit (e.g., block or subprogram body) may raise an exception, to signal that an anomaly  has been detected.  The computation that raised the exception is abandoned (and can  never  be  resumed,  although  it  can  be  restarted).

• A unit may propagate an exception that has been raised by itself (or propagated out of  another  unit  it  has  called).

• A unit may alternatively handle such an exception, allowing programmer-defined recovery  from  an  anomalous  situation.  Exception  handlers  are  segregated  from  normal-case  code.

## 19.3 Predefined exceptions

Predefined  exceptions

The  predefined  exceptions  are  those  defined  in  package  Standard  .  Every  language-defined  run-time  error  causes  a  predefined  exception  to  be  raised.  Some  examples  are:

• Constraint_Error,  raised  when  a  subtype’s  constraint  is  not  satisfied

• Program_Error,  when  a  protected  operation  is  called  inside  a  protected  object,  e.g.

• Storage_Error,  raised  by  running  out  of  storage

• Tasking_Error,  when  a  task  cannot  be  activated  because  the  operating  system  has  not  enough  resources,  e.g.

Ex.1

![](Images/image06968.jpeg)

Ex.2

![](Images/image06969.jpeg)

Ex.3  Compare  the  following  approaches:

![](Images/image06970.jpeg)

![](Images/image06971.jpeg)

A  negative  argument  to  Compute_Sqrt  causes  OK  to  be  set  to  False.  Triangle  uses  it  to  determine  its  own  status  parameter  value,  and  so  on  up  the  calling  tree,  ad  nauseam.

versus

![](Images/image06972.jpeg)

A  negative  argument  to  Sqrt  causes  Constraint_Error  to  be  explicitly  raised  inside  Sqrt,  and  propagated  out.  Triangle  simply  propagates  the  exception  (by  not  handling  it).

Alternatively,  we  can  catch  the  error  by  using  the  type  system:

![](Images/image06973.jpeg)

A  negative  argument  to  Sqrt  now  raises  Constraint_Error  at  the  point  of  call.  Sqrt  is  never  even  entered.

## 19.4 Input-output  exceptions

Input-output  exceptions

Some  examples  of  exceptions  raised  by  subprograms  of  the  predefined  package  Ada.Text_-  IO  are:

• End_Error,  raised  by Get, Skip_Line,  etc., if end-of-file already reached.

• Data_Error,  raised  by  Get  in  Integer_IO,  etc.,  if  the  input  is  not  a  literal  of  the  expected  type.

• Mode_Error,  raised  by  trying  to  read  from  an  output  file,  or  write  to  an  input  file,  etc.

• Layout_Error,  raised  by  specifying  an  invalid  data  format  in  a  text  I/O  operation  Ex.  1

![](Images/image06974.jpeg)

## 19.5 Exception  declarations

Exception  declarations

Exceptions are declared rather like objects, but they are not objects. For example, recursive  re-entry to a scope where an exception is declared does not create a new exception of the  same  name;  instead  the  exception  declared  in  the  outer  invocation  is  reused.

Ex.1

![](Images/image06975.jpeg)

Ex.2

![](Images/image06976.jpeg)

![](Images/image06977.jpeg)

## 19.6 Raising  exceptions

Raising  exceptions

The  raise  statement  explicitly  raises  a  specified  exception.  Ex.  1

![](Images/image06978.jpeg)

## 19.7 Exception  handling  and  propagation

Exception  handling  and  propagation

Exception  handlers  may  be  grouped  at  the  end  of  a  block,  subprogram  body,  etc.  A  handler  is  any  sequence  of  statements  that  may  end:

• by  completing;

• by  executing  a  return  statement;

• by  raising  a  different  exception  (raise  e;);

• by  re-raising  the  same  exception  (raise;).

Suppose  that  an  exception  e  is  raised  in  a  sequence  of  statements  U  (a  block,  subprogram  body,  etc.).

• If  U  contains  a  handler  for  e:  that  handler  is  executed,  then  control  leaves  U.

• If  U  contains  no  handler  for  e:  e  is  propagated  out  of  U;  in  effect,  e  is  raised  at  the  "point  of  call”  of  U.

So  the  raising  of  an  exception  causes  the  sequence  of  statements  responsible  to  be  abandoned  at  the  point  of  occurrence  of  the  exception.  It  is  not,  and  cannot  be,  resumed.

Ex.  1

![](Images/image06979.jpeg)

## 19.8 Information  about  an  exception  occurrence

Information  about  an  exception  occurrence

Ada  provides  information  about  an  exception  in  an  object  of  type  Exception_Occurrence,  defined  in  Ada.Exceptions  along  with  subprograms  taking  this  type  as  parameter:

• Exception_Name:  return  the  full  exception  name  using  the  dot  notation  and  in  uppercase  letters.  For  example,  Queue.Overflow.

• Exception_Message:  return  the  exception  message  associated  with  the  occurrence.

• Exception_Information:  return  a  string  including  the  exception  name  and  the  associated  exception  message.

For  getting  an  exception  occurrence  object  the  following  syntax  is  used:

![](Images/image06980.jpeg)

![](Images/image06981.jpeg)

The  exception  message  content  is  implementation  defined  when  it  is  not  set  by  the  user  who  raises  the  exception.  It  usually  contains  a  reason  for  the  exception  and  the  raising  location.

The  user  can  specify  a  message  using  the  procedure  Raise_Exception.

![](Images/image06982.jpeg)

Starting  with  Ada  2005,  a  simpler  syntax  can  be  used  to  associate  a  string  message  with  exception  occurrence.

![](Images/image06983.jpeg)

The  Ada.Exceptions  package  also  provides  subprograms  for  saving  exception  occurrences  and  re-raising  them.

## 19.9 See  also

See  also

#### 19.9.1 Wikibook

• Ada  Programming[1](#part0161.xhtml__bookmark488)

![](Images/image06984.jpeg)

1[http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

#### 19.9.2 Ada  95  Reference  Manual

• Section11:Exceptionsˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-11.html)  [standards/95lrm/ARM_HTML/RM-11.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-11.html)

• 11.4.1  The  Package  Exceptions  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-11-4-1.html)  [standards/95lrm/ARM_HTML/RM-11-4-1.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-11-4-1.html)

#### 19.9.3 Ada  2005  Reference  Manual

• Section11:Exceptionsˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-11.html)  [standards/05rm/html/RM-11.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-11.html)

• 11.4.1  The  Package  Exceptions  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-11-4-1.html)  [standards/05rm/html/RM-11-4-1.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-11-4-1.html)

#### 19.9.4 Ada  Quality  and  Style  Guide

###### • Chapter  4:  Program  Structure

• 4.3  Exceptions  ˆ{[http://www.adaic.org/resources/add_content/docs/95style/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_4/4-3.html)  [html/sec_4/4-3.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_4/4-3.html)

• 4.3.1  Using  Exceptions  to  Help  Define  an  Abstraction  ˆ{[http://www.adaic.org/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_4/4-3-1.html)  [resources/add_content/docs/95style/html/sec_4/4-3-1.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_4/4-3-1.html)

###### • Chapter  5:  Programming  Practices

• 5.8  Using  Exceptions  ˆ{[http://www.adaic.org/resources/add_content/docs/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_5/5-8.html)  [95style/html/sec_5/5-8.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_5/5-8.html)

• 5.8.1  Handling  Versus  Avoiding  Exceptions  ˆ{[http://www.adaic.org/resources/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_5/5-8-1.html)  [add_content/docs/95style/html/sec_5/5-8-1.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_5/5-8-1.html)

• 5.8.2  Handling  for  Others  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_5/5-8-2.html)  [docs/95style/html/sec_5/5-8-2.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_5/5-8-2.html)

• 5.8.3Propagationˆ{[http://www.adaic.org/resources/add_content/docs/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_5/5-8-3.html)  [95style/html/sec_5/5-8-3.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_5/5-8-3.html)

• 5.8.4  Localizing  the  Cause  of  an  Exception  ˆ{[http://www.adaic.org/resources/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_5/5-8-4.html)  [add_content/docs/95style/html/sec_5/5-8-4.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_5/5-8-4.html)

###### • Chapter  7:  Portability

• 7.5  Exceptions  ˆ{[http://www.adaic.org/resources/add_content/docs/95style/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/7-5.html)  [html/sec_7/7-5.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/7-5.html)

• 7.5.1PredefinedandUser-DefinedExceptionsˆ{[http://www.adaic.org/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/7-5-1.html)  [resources/add_content/docs/95style/html/sec_7/7-5-1.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/7-5-1.html)

• 7.5.2  Implementation-Specific  Exceptions  ˆ{[http://www.adaic.org/resources/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/7-5-2.html)  [add_content/docs/95style/html/sec_7/7-5-2.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/7-5-2.html)

# 20 Generics

## 20.1 Parametric  polymorphism  (generic  units)

Parametric  polymorphism  (generic  units)

The  idea  of  code  reuse  arises  from  the  necessity  for  constructing  large  software  systems  combining well-established building blocks.  The reusability of code improves the productivity  and the quality of software.  The generic units are one of the ways in which the Ada language  supports  this  characteristic.  A  generic  unit  is  a  subprogram  or  package  that  defines  algorithms  in  terms  of  types  and  operations  that  are  not  defined  until  the  user  instantiates  them.

Note  to  C++  programmers:  generic  units  are  similar  to  C++  templates.

For  example,  to  define  a  procedure  for  swapping  variables  of  any  (non-limited)  type:

![](Images/image06985.jpeg)

![](Images/image06986.jpeg)

The Swap subprogram is said to be generic.  The subprogram specification is preceded by  the generic formal part consisting of the reserved word generic followed by a list of generic  formal parameters which may be empty. The entities declared as generic are not directly  usable,  it  is  necessary  to  instantiate  them.

To  be  able  to  use  Swap,  it  is  necessary  to  create  an  instance  for  the  wanted  type.  For  example:

![](Images/image06987.jpeg)

Now  the  Swap_Integers  procedure  can  be  used  for  variables  of  type  Integer.

The generic procedure can be instantiated for all the needed types. It can be instantiated  with different names or, if the same identifier is used in the instantiation, each declaration  overloads  the  procedure:

![](Images/image06988.jpeg)

Similarly,  generic  packages  can  be  used,  for  example,  to  implement  a  stack  of  any  kind  of  elements:

![](Images/image06989.jpeg)

![](Images/image06990.jpeg)

A  stack  of  a  given  size  and  type  could  be  defined  in  this  way:

![](Images/image06991.jpeg)

## 20.2 Generic  parameters

Generic  parameters

The  generic  unit  declares  generic  formal  parameters,  which  can  be:

• objects  (of  mode  in  or  in  out  but  never  out)

• types

• subprograms

• instances  of  another,  designated,  generic  unit.

When instantiating the generic, the programmer passes one actual parameter for each formal.  Formal  values  and  subprograms  can  have  defaults,  so  passing  an  actual  for  them  is  optional.

#### 20.2.1 Generic  formal  objects

Formal parameters of mode in accept any value, constant, or variable of the designated  type. The actual is copied into the generic instance, and behaves as a constant inside the  generic;  this  implies  that  the  designated  type  cannot  be  limited.  It  is  possible  to  specify  a

default  value,  like  this:

![](Images/image06992.jpeg)

For  mode  in  out,  the  actual  must  be  a  variable.

One limitation with generic formal objects is that they are never considered static, even if  the actual happens to be static. If the object is a number, it cannot be used to create a new  type.  It  can  however  be  used  to  create  a  new  derived  type,  or  a  subtype:

![](Images/image06993.jpeg)

The reason why formal objects are nonstatic is to allow the compiler to emit the object code  for the generic only once, and to have all instances share it, passing it the address of their  actual object as a parameter.  This bit of compiler technology is called shared generics.  If  formal objects were static, the compiler would have to emit one copy of the object code,  with the object embedded in it, for each instance, potentially leading to an explosion in  object  code  size  (code  bloat).

(Note to C++ programmers:  in C++, since formal objects can be static, the compiler cannot  implement  shared  generics  in  the  general  case;  it  would  have  to  examine  the  entire  body  of  the generic before deciding whether or not to share its object code.  In contrast, Ada generics  are  designed  so  that  the  compiler  can  instantiate  a  generic  without  looking  at  its  body.)

#### 20.2.2 Generic  formal  types

The  syntax  allows  the  programmer  to  specify  which  type  categories  are  acceptable  as  actuals.  As a rule of thumb:  The syntax expresses how the generic sees the type, i.e.  it assumes the  worst,  not  how  the  creator  of  the  instance  sees  the  type.

This  is  the  syntax  of  RM  12.5:

![](Images/image06994.jpeg)

![](Images/image06995.jpeg)

This  is  quite  complex,  so  some  examples  are  given  below.  A  type  declared  with  the  syntax  type T (<>) denotes a type with unknown discriminants. This is the Ada vernacular for  indefinite types, i.e. types for which objects cannot be declared without giving an initial  expression. An example of such a type is one with a discriminant without default, another  example  is  an  unconstrained  array  type.

| Generic  formal  type | Acceptable  actual  types |
| type  T  (<>)  is  limited  private; | Any  type  at  all.  The  actual  type  canbe  limited[1](#part0000.xhtml__bookmark0)  or  not,  indefinite  or  definite,  but  the  generic  treats  it  as  limited  and  indefinite,  i.e.  does  not  assume  that  as-  signment  is  available  for  the  type. |
| type  T  (<>)  is  private; | Any  nonlimited  type:  the  generic  knowsthat  it  is possible  to assign  to  variables  of  this  type,  but  it  is  not  possible  to  de-  clare  objects  of  this  type  without  initial  value. |
| type  T  is  private; | Any  nonlimited definite  type:  thegeneric  knows  that  it  is  possible  to  assign  to  variables  of  this  type  and  to  declare  objects  without  initial  value. |
| type  T  (<>)  is  abstract  taggedlimited  private; | Any  tagged  type[2](#part0000.xhtml__bookmark0),  abstract  or  concrete,limited  or  not. |
| type  T  (<>)  is  tagged  limitedprivate; | Any  concrete  tagged  type,  limited  ornot. |
| type  T  (<>)  is  abstract  taggedprivate; | Any  nonlimited  tagged  type,  abstract  orconcrete. |
| type  T  (<>)  is  tagged  private; | Any  nonlimited,  concrete  tagged  type. |
| type  T  (<>)  is  new  Parent; | Any  type  derived  from  Parent.  Thegeneric  knows  about  Parent's  operations,  so  can  call  them.  Neither  T  nor  Parent  can  be  abstract. |
| type  T  (<>)  is  abstract  new  Parentwith  private; | Any  type,  abstract or  concrete,  derivedfrom Parent, where Parent is a tagged  type, so calls to T's operations can dis-  patch  dynamically. |
| type  T  (<>)  is  new  Parent  withprivate; | Any  concrete  type,  derived  from  thetagged  type  Parent. |

![](Images/image06996.jpeg)

1 Chapter  [14](#part0115.xhtml__bookmark366)  on  page  [113](#part0115.xhtml__bookmark366)

2 Chapter  [22](#part0189.xhtml__bookmark519)  on  page  [187](#part0189.xhtml__bookmark519)

| Generic  formal  type | Acceptable  actual  types |
| type  T  is  (<>); | Any  discrete  type:  integer[3](#part0000.xhtml__bookmark0),  modular[4](#part0000.xhtml__bookmark0),or  enumeration[5](#part0000.xhtml__bookmark0). |
| type  T  is  range  <>; | Any  signed  integer  type |
| type  T  is  mod  <>; | Any  modular  type |
| type  T  is  delta  <>; | Any  (non-decimal)  fixed  point  type[6](#part0000.xhtml__bookmark0) |
| type  T  is  delta  <>  digits  <>; | Any  decimal  fixed  point  type |
| type  T  is  digits  <>; | Any  floating  point  type[7](#part0000.xhtml__bookmark0) |
| type  T  is  array  (I)  of  E; | Any array  type[8](#part0000.xhtml__bookmark0)  with  index  of  type  Iand  elements  of  type  E  (I  and  E  could  be  formal  parameters  as  well) |
| type  T  is  access  O; | Any  access  type[9](#part0000.xhtml__bookmark0)  pointing  to  objects  oftype  O  (O  could  be  a  formal  parameter  as  well) |

In the body we can only use the operations predefined for the type category of the formal  parameter. That is, the generic specification is a contract between the generic implementor  and the client instantiating the generic unit. This is different to the parametric features of  other  languages,  such  as  C++.

It  is  possible  to  further  restrict  the  set  of  acceptable  actual  types  like  so:

| Generic  formal  type | Acceptable  actual  types |
| type  T (<>) is... | Definite  or  indefinite  types  (loosely  speaking:  typeswith  or  without  discriminants,  but  other  forms  of  indef-  initeness  exist) |
| type  T  (D  :  DT)  is... | Types  with  a  discriminant  of  type  DT  (it  is  possibleto  specify  several  discriminants,  too) |
| type  T  is... | Definite  types  (loosely  speaking  types  without  a  dis-criminant  or  with  a  discriminant  with  default  value) |

#### 20.2.3 Generic  formal  subprograms

It is possible to pass a subprogram as a parameter to a generic.  The generic specifies a  generic  formal  subprogram,  complete  with  parameter  list  and  return  type  (if  the  subprogram  is a function).  The actual must match this parameter profile.  It is not necessary that the  names  of  parameters  match,  though.

![](Images/image06997.jpeg)

3 Chapter  [6](#part0071.xhtml__bookmark237)  on  page  [69](#part0071.xhtml__bookmark237)

4 Chapter  [7](#part0073.xhtml__bookmark245)  on  page  [71](#part0073.xhtml__bookmark245)

5 Chapter  [8](#part0075.xhtml__bookmark251)  on  page  [73](#part0075.xhtml__bookmark251)

6 Chapter  [10](#part0081.xhtml__bookmark278)  on  page  [79](#part0081.xhtml__bookmark278)

7 Chapter  [9](#part0079.xhtml__bookmark266)  on  page  [77](#part0079.xhtml__bookmark266)

8 Chapter  [11](#part0085.xhtml__bookmark293)  on  page  [83](#part0085.xhtml__bookmark293)

9 Chapter  [13](#part0101.xhtml__bookmark346)  on  page  [99](#part0101.xhtml__bookmark346)

Here  is  the  specification  of  a  generic  subprogram  that  takes  another  subprogram  as  its  parameter:

![](Images/image06998.jpeg)

And  here  is  the  body  of  the  generic  subprogram;  it  calls  parameter  as  it  would  any  other  subprogram.

![](Images/image06999.jpeg)

This  generic  function  could  be  used,  for  example,  with  matrices,  having  defined  the  matrix  product.

![](Images/image07000.jpeg)

It  is  possible  to  specify  a  default  with  "the  box"  (is  <>  ),  like  this:

![](Images/image07001.jpeg)

This  means  that  if,  at  the  point  of  instantiation,  a  function  "*"  exists  for  the  actual  type,  and  if  it  is  directly  visible,  then  it  will  be  used  by  default  as  the  actual  subprogram.

One  of  the  main  uses  is  passing  needed  operators.  The  following  example  shows  this  (follow  download  links  for  full  example):

![](Images/image07002.jpeg)

![](Images/image07003.jpeg)

![](Images/image07004.jpeg)

#### 20.2.4 Generic  instances  of  other  generic  packages

A  generic  formal  can  be  a  package;  it  must  be  an  instance  of  a  generic  package,  so  that  the  generic  knows  the  interface  exported  by  the  package:

![](Images/image07005.jpeg)

This means that the actual must be an instance of the generic package Q. The box after Q  means that we do not care which actual generic parameters were used to create the actual  for P. It is possible to specify the exact parameters, or to specify that the defaults must be  used,  like  this:

![](Images/image07006.jpeg)

It is all or nothing:  if you specify the generic parameters, you must specify all of them.  Similarly, if you specify no parameters and no box, then all the generic formal parameters of  Q  must  have  defaults.  The  actual  package  must,  of  course,  match  these  constraints.

The generic sees both the public part and the generic parameters of the actual package  (Param1  and  Param2  in  the  above  example).

This feature allows the programmer to pass arbitrarily complex types as parameters to a  generic  unit,  while  retaining  complete  type  safety  and  encapsulation.  (example  needed)

It is not possible for a package to list itself as a generic formal, so no generic recursion is  possible.  The  following  is  illegal:

![](Images/image07007.jpeg)

In  fact,  this  is  only  a  particular  case  of:

![](Images/image07008.jpeg)

which  is  also  illegal,  despite  the  fact  that  A  is  no  longer  generic.

## 20.3 Instantiating  generics

Instantiating  generics

To  instantiate  a  generic  unit,  use  the  keyword  new:

![](Images/image07009.jpeg)

Notes  of  special  interest  to  C++  programmers:

• The generic formal types define completely which types are acceptable as actuals; therefore,  the  compiler  can  instantiate  generics  without  looking  at  the  body  of  the  generic.

• Each instance has a name and is different from all other instances.  In particular, if a  generic package declares a type, and you create two instances of the package, then you  will  get  two  different,  incompatible  types,  even  if  the  actual  parameters  are  the  same.

• Ada  requires  that  all  instantiations  be  explicit.

• It is not possible to create special-case instances of a generic (known as "template  specialisation"  in  C++).

As a consequence of the above, Ada does not permit template metaprogramming. However,  this  design  has  significant  advantages:

• the object code can be shared by all instances of a generic, unless of course the programmer  has  requested  that  subprograms  be  inlined;  there  is  no  danger  of  code  bloat.

• when reading programs written by other people, there are no hidden instantiations, and  no  special  cases  to  worry  about.  Ada  follows  the  Law  of  Least  Astonishment.

## 20.4 Advanced  generics

Advanced  generics

#### 20.4.1 Generics  and  nesting

A generic unit can be nested inside another unit, which itself may be generic. Even though  no special rules apply (just the normal rules about generics and the rules about nested  units), novices may be confused.  It is important to understand the difference between a  generic  unit  and  instances  of  a  generic  unit.

Example  1.  A  generic  subprogram  nested  in  a  nongeneric  package.

![](Images/image07010.jpeg)

To  use  Apply_To_All,  you  first  define  the  procedure  to  be  applied  to  each  String  in  the  Bag.  Then,  you  instantiate  Apply_To_All,  and  finally  you  call  the  instance.

![](Images/image07011.jpeg)

Example  2.  A  generic  subprogram  nested  in  a  generic  package  This  is  the  same  as  above,  except  that  now  the  Bag  itself  is  generic:

![](Images/image07012.jpeg)

As you can see, the generic formal subprogram Operator takes a parameter of the generic  formal type Element_Type. This is okay: the nested generic sees everything that is in its  enclosing  unit.

You  cannot  instantiate  Generic_Bag.Apply_To_All  directly, so  you  must  first  create  an  instance  of  Generic_Bag,  say  Bag_Of_Strings,  and  then  instantiate  Bag_Of_Strings.Apply_To_All.

![](Images/image07013.jpeg)

![](Images/image07014.jpeg)

#### 20.4.2 Generics  and  child  units

Example  3.  A  generic  unit  that  is  a  child  of  a  nongeneric  unit.

Each  instance  of  the  generic  child  is  a  child  of  the  parent  unit,  and  so  it  can  see  the  parent's  public  and  private  parts.

![](Images/image07015.jpeg)

The  differences  between  this  and  Example  1  are:

• Bag_Of_Strings.Apply_To_All  is  compiled  separately.  In  particular,  Bag_Of_-  Strings.Apply_To_All might have been written by a different person who did not  have  access  to  the  source  text  of  Bag_Of_Strings.

• Before  you  can  use  Bag_Of_Strings.Apply_To_All,  you  must  with  it  explicitly;

withing  the  parent,  Bag_Of_Strings,  is  not  sufficient.

• If you do not use Bag_Of_Strings.Apply_To_All, your program does not contain  its  object  code.

• Because Bag_Of_Strings.Apply_To_All is at the library level, it can declare con-  trolled types; the nested package could not do that in Ada 95\. In Ada 2005, one can  declare  controlled  types  at  any  level.

![](Images/image07016.jpeg)

Example  4.  A  generic  unit  that  is  a  child  of  a  generic  unit

This  is  the  same  as  Example  3,  except  that  now  the  Bag  is  generic,  too.

![](Images/image07017.jpeg)

![](Images/image07018.jpeg)

Example  5.  A  parameterless  generic  child  unit

Children of a generic unit must be generic, no matter what.  If you think about it, it is  quite logical:  a child unit sees the public and private parts of its parent, including the  variables declared in the parent. If the parent is generic, which instance should the child  see?  The answer is that the child must be the child of only one instance of the parent,  therefore  the  child  must  also  be  generic.

![](Images/image07019.jpeg)

Suppose  we  want  a  child  of  a  Generic_Hash_Map  that  can  serialise  the  map  to  disk;  for this it needs to sort the map by hash value. This is easy to do, because we know that  Hash_Type is a discrete type, and so has a less-than operator. The child unit that does  the  serialisation  does  not  need  any  additional  generic  parameters,  but  it  must  be  generic  nevertheless,  so  it  can  see  its  parent's  generic  parameters,  public  and  private  part.

![](Images/image07020.jpeg)

To read and write a map to disk, you first create an instance of Generic_Hash_Map,  for  example  Map_Of_Unbounded_Strings,  and  then  an  instance  of  Map_Of_-  Unbounded_Strings.Serializer:

![](Images/image07021.jpeg)

## 20.5 See  also

See  also

#### 20.5.1 Wikibook

• Ada  Programming[10](#part0174.xhtml__bookmark495)

• Ada  Programming/Object  Orientation[11](#part0174.xhtml__bookmark496):  tagged  types  provides  other  mean  of  polymor-  phism  in  Ada.

#### 20.5.2 Wikipedia

• Generic  programming[12](#part0174.xhtml__bookmark497)

#### 20.5.3 Ada  Reference  Manual

• Section12:GenericUnitsˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-12.html)  [standards/05rm/html/RM-12.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-12.html)

es:Programación  en  Ada/Unidades  genéricas[13](#part0174.xhtml__bookmark498)

![](Images/image07022.jpeg)

10 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

11 Chapter  [22](#part0189.xhtml__bookmark519)  on  page  [187](#part0189.xhtml__bookmark519)

12 [http://en.wikipedia.org/wiki/Generic%20programming](http://en.wikipedia.org/wiki/Generic%20programming)

13 [http://es.wikibooks.org/wiki/Programaci%F3n%20en%20Ada%2FUnidades%20gen%E9ricas](http://es.wikibooks.org/wiki/Programaci%F3n%20en%20Ada%2FUnidades%20gen%E9ricas)

# 21 Tasking

## 21.1 Tasks

Tasks

A  task  unit  is  a  program  unit  that  is  obeyed  concurrently  with  the  rest  of  an  Ada  program.  The  corresponding  activity,  a  new  locus  of  control,  is  called  a  task  in  Ada  terminology,  and  is  similar  to  a  thread,  for  example  in  Java  Threads[1](#part0175.xhtml__bookmark501).  The  execution  of  the  main  program  is  also  a  task,  the  anonymous  environment  task.  A  task  unit  has  both  a  declaration  and  a  body,  which  is  mandatory.  A  task  body  may  be  compiled  separately  as  a  subunit,  but  a  task  may  not  be  a  library  unit,  nor  may  it  be  generic.  Every  task  depends  on  a  master,  which  is  the immediately surrounding declarative region - a block, a subprogram, another task, or a  package.  The  execution  of  a  master  does  not  complete  until  all  its  dependent  tasks  have  terminated.  The  environment  task  is  the  master  of  all  other  tasks;  it  terminates  only  when  all  other  tasks  have  terminated.

Task units are similar to packages in that a task declaration defines entities exported from  the  task,  whereas  its  body  contains  local  declarations  and  statements  of  the  task.

A  single  task  is  declared  as  follows:

![](Images/image07023.jpeg)

A  task  declaration  can  be  simplified,  if  nothing  is  exported,  thus:

![](Images/image07024.jpeg)

Ex.  1

![](Images/image07025.jpeg)

![](Images/image07026.jpeg)

1[http://en.wikibooks.org/wiki/Java%3AThreads](http://en.wikibooks.org/wiki/Java%3AThreads)

![](Images/image07027.jpeg)

It  is  possible  to  declare  task  types,  thus  allowing  task  units  to  be  created  dynamically,  and  incorporated  in  data  structures:

![](Images/image07028.jpeg)

Task types are limited, i.e. they are restricted in the same way as limited private types, so  assignment  and  comparison  are  not  allowed.

#### 21.1.1 Rendezvous

The  only  entities  that  a  task  may  export  are  entries.  An  entry  looks  much  like  a  procedure.  It has an identifier and may have in, out or in out parameters. Ada supports communication  from task to task by means of the entry call. Information passes between tasks through  the actual parameters of the entry call. We can encapsulate data structures within tasks  and operate on them by means of entry calls, in a way analogous to the use of packages for  encapsulating variables. The main difference is that an entry is executed by the called task,  not the calling task, which is suspended until the call completes. If the called task is not  ready  to  service  a  call  on  an  entry,  the  calling  task  waits  in  a  (FIFO)  queue  associated  with  the  entry.  This  interaction  between  calling  task  and  called  task  is  known  as  a  rendezvous.  The  calling  task  requests  rendezvous  with  a  specific  named  task  by  calling  one  of  its  entries.  A  task accepts rendezvous with any caller of a specific entry by executing an accept statement  for the entry. If no caller is waiting, it is held up. Thus entry call and accept statement  behave symmetrically. (To be honest, optimized object code may reduce the number of  context  switches  below  the  number  implied  by  this  naive  description.)

Ex. 2 The following task type implements a single-slot buffer, i.e. an encapsulated variable  that  can  have  values  inserted  and  removed  in  strict  alternation.  Note  that  the  buffer  task has no need of state variables to implement the buffer protocol:  the alternation of  insertion and removal operations is directly enforced by the control structure in the body of  Encapsulated_Buffer_Task_Type  which  is,  as  is  typical,  a  loop.

![](Images/image07029.jpeg)

#### 21.1.2 Selective  Wait

To avoid being held up when it could be doing productive work, a server task often needs  the freedom to accept a call on any one of a number of alternative entries. It does this by  means  of  the  selective  wait  statement,  which  allows  a  task  to  wait  for  a  call  on  any  of  two  or  more  entries.

If only one of the alternatives in a selective wait statement has a pending entry call, then  that one is accepted. If two or more alternatives have calls pending, the implementation is  free  to  accept  any  one  of  them.  For  example,  it  could  choose  one  at  random.  This  introduces  bounded non-determinism into the program. A sound Ada program should not depend on a  particular method being used to choose between pending entry calls. (However, there are  facilities  to  influence  the  method  used,  when  that  is  necessary.)

Ex.  3

![](Images/image07030.jpeg)

![](Images/image07031.jpeg)

![](Images/image07032.jpeg)

creates  two  variables  of  type  Encapsulated_Variable_Task_Type.  They  can  be  used  thus:

![](Images/image07033.jpeg)

Again, note that the control structure of the body ensures that an Encapsulated_Variable_-  Task_Type must be given an initial value by a first Store operation before any Fetch  operation  can  be  accepted.

#### 21.1.3 Guards

Depending  on  circumstances,  a  server  task  may  not  be  able  to  accept  calls  for  some  of  the entries that have accept alternatives in a selective wait statement. The acceptance of  any alternative can be made conditional by using a guard, which is Boolean[2](#part0178.xhtml__bookmark502) precondition  for acceptance. This makes it easy to write monitor-like server tasks, with no need for an  explicit signaling mechanism, nor for mutual exclusion. An alternative with a True guard is  said to be open. It is an error if no alternative is open when the selective wait statement is  executed,  and  this  raises  the  Program_Error  exception.

Ex.  4

![](Images/image07034.jpeg)

![](Images/image07035.jpeg)

2 [http://en.wikibooks.org/wiki/Ada%20Programming%2FTypes%23Boolean](http://en.wikibooks.org/wiki/Ada%20Programming%2FTypes%23Boolean)

![](Images/image07036.jpeg)

## 21.2 Protected  types

Protected  types

Tasks allow for encapsulation and safe usage of variable data without the need for any  explicit mutual exclusion and signaling mechanisms.  Ex.  4 shows how easy it is to write  server tasks that safely manage locally-declared data on behalf of multiple clients. There is  no need for mutual exclusion of access to the managed data, because it is never accessed  concurrently.  However,  the  overhead  of  creating  a  task  merely  to  serve  up  some  data  may  be  excessive. For such applications, Ada 95 provides protected modules. A protected module  encapsulates a data structure and exports subprograms that operate on it under automatic  mutual exclusion. It also provides automatic, implicit signaling of conditions between client  tasks. Again, a protected module can be either a single protected object or a protected type,  allowing  many  protected  objects  to  be  created.

A protected module can export only procedures, functions and entries, and its body may  contain only the bodies of procedures, functions and entries. The protected data is declared  after  private  in  its  specification,  but  is  accessible  only  within  the  protected  module's  body. Protected procedures and entries may read and/or write its encapsulated data, and  automatically exclude each other. Protected functions may only read the encapsulated data,  so  that  multiple  protected  function  calls  can  be  concurrently  executed  in  the  same  protected  object,  with  complete  safety;  but  protected  procedure  calls  and  entry  calls  exclude  protected  function calls, and vice versa. Exported entries and subprograms of a protected object are  executed by its calling task, as a protected object has no independent locus of control. (To  be honest, optimized object code may reduce the number of context switches below the  number  implied  by  this  naive  description.)

Like a task entry, a protected entry can employ a guard to control admission. This provides  automatic signaling, and ensures that when a protected entry call is accepted, its guard  condition  is  True,  so  that  a  guard  provides  a  reliable  precondition  for  the  entry  body.

Ex.  5  The  following  is  a  simple  protected  type  analogous  to  the  Encapsulated_Buffer  task  in  Ex.  2.

![](Images/image07037.jpeg)

Note how the guards, using the state variable Empty, ensure that messages are alternately  inserted and removed, and that no attempt can be made to take data from an empty buffer.  All this is achieved without explicit signaling or mutual exclusion constructs, whether in the  calling  task  or  in  the  protected  type  itself.

The notation for calling a protected entry or procedure is exactly the same as that for calling  a task entry. This makes it easy to replace one implementation of the abstract type by the  other,  the  calling  code  being  unaffected.

Ex.  6  The  following  task  type  implements  Dijkstra's  semaphore  ADT,  with  FIFO  scheduling  of  resumed  processes.  The  algorithm  will  accept  calls  to  both  Wait  and  Signal,  so  long  as  the semaphore invariant would not be violated. When that circumstance approaches, calls  to  Wait  are  ignored  for  the  time  being.

![](Images/image07038.jpeg)

![](Images/image07039.jpeg)

This  task  could  be  used  as  follows:

![](Images/image07040.jpeg)

Alternatively,  semaphore  functionality  can  be  provided  by  a  protected  object,  with  major  efficiency  gains.

Ex.  7 The Initialize and Signal operations of this protected type are unconditional, so they  are implemented as protected procedures, but the Wait operation must be guarded and is  therefore  implemented  as  an  entry.

![](Images/image07041.jpeg)

Unlike the task type above,  this does not ensure that Initialize is called before Wait or  Signal, and Count is given a default initial value instead. Restoring this defensive feature of  the  task  version  is  left  as  an  exercise  for  the  reader.

## 21.3 Entry  families

Entry  families

Sometimes  we  need  a  group  of  related  entries.  Entry  families,  indexed  by  a  discrete  type[3](#part0182.xhtml__bookmark506),  meet  this  need.

Ex.  8  This  task  provides  a  pool  of  several  buffers.

![](Images/image07042.jpeg)

Note  that  the  busy  wait  else  null  is  necessary  here  to  prevent  the  task  from  being  suspended  on some buffer when there was no call pending for it, because such suspension would delay  serving  requests  for  all  the  other  buffers  (perhaps  indefinitely).

## 21.4 Termination

Termination

Server  tasks  often  contain  infinite  loops  to  allow  them  to  service  an  arbitrary  number  of  calls  in  succession.  But  control  cannot  leave  a  task's  master  until  the  task  terminates,  so  we need a way for a server to know when it should terminate. This is done by a terminate  alternative  in  a  selective  wait.

![](Images/image07043.jpeg)

3 [http://en.wikibooks.org/wiki/ada%20Programming%2FTypes%23List%20of%20Types](http://en.wikibooks.org/wiki/ada%20Programming%2FTypes%23List%20of%20Types)

Ex.  9

![](Images/image07044.jpeg)

The  task  terminates  when:

1. at  least  one  terminate  alternative  is  open,  and

2. there  are  no  pending  calls  to  its  entries,  and

3. all  other  tasks  of  the  same  master  are  in  the  same  state  (or  already  terminated),  and

4. the  task's  master  has  completed  (i.e.  has  run  out  of  statements  to  execute).

Conditions (1) and (2) ensure that the task is in a fit state to stop.  Conditions (3) and (4)  ensure that stopping cannot have an adverse effect on the rest of the program, because no  further  calls  that  might  change  its  state  are  possible.

## 21.5 Timeout

Timeout

A task may need to avoid being held up by calling to a slow server. A timed entry call lets a  client specify a maximum delay before achieving rendezvous, failing which the attempted  entry  call  is  withdrawn  and  an  alternative  sequence  of  statements  is  executed.

Ex.  10

![](Images/image07045.jpeg)

![](Images/image07046.jpeg)

To time out the functionality provided by a task, two distinct entries are needed: one to  pass in arguments, and one to collect the result. Timing out on rendezvous with the latter  achieves  the  desired  effect.

Ex.  11

![](Images/image07047.jpeg)

Symmetrically,  a delay alternative in a selective wait statement allows a server task to  withdraw an offer to accept calls after a maximum delay in achieving rendezvous with any  client.

Ex.  12

![](Images/image07048.jpeg)

![](Images/image07049.jpeg)

## 21.6 Conditional  entry  calls

Conditional  entry calls

An  entry  call  can  be  made  conditional,  so  that  it  is  withdrawn  if  the  rendezvous  is  not  immedi-  ately  achieved.  This  uses  the  select  statement  notation  with  an  else  part.  Thus  the  constructs

![](Images/image07050.jpeg)

and

![](Images/image07051.jpeg)

seem to be conceptually equivalent.  However, the attempt to start the rendezvous may  take some time, especially if the callee is on another processor, so the delay 0.0; may expire  although the callee would be able to accept the rendezvous, whereas the else construct is  safe.

## 21.7 Requeue  statements

Requeue  statements

A requeue statement allows an accept statement or entry body to be completed while  redirecting to a different or the same entry queue. The called entry has to share the same  parameter  list  or  be  parameter-less.

## 21.8 Scheduling

Scheduling

FIFO,  priority,  priority  inversion  avoidance,  ...  to  be  completed

## 21.9 Interfaces

Interfaces

This  language  feature  is  only  available  in  Ada  2005

Task  and  Protected  types  can  also  implement  interfaces[4](#part0186.xhtml__bookmark513).

![](Images/image07052.jpeg)

## 21.10  See  also

See  also

#### 21.10.1 Wikibook

• Ada  Programming[5](#part0186.xhtml__bookmark514)

• Ada  Programming/Libraries/Ada.Storage_IO[6](#part0186.xhtml__bookmark515)

#### 21.10.2 Ada  Reference  Manual

###### Ada  95

• Section 9:Tasks  and  Synchronization  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-9.html)  [content/standards/95lrm/ARM_HTML/RM-9.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-9.html)

###### Ada  2005

• 3.9.4  Interface  Types  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-9-4.html)  [05rm/html/RM-3-9-4.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-9-4.html)

![](Images/image07053.jpeg)

4 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Finterface](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Finterface)

5 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

6 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Storage_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Storage_IO)

• Section 9:Tasks  and  Synchronization  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-9.html)  [content/standards/05rm/html/RM-9.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-9.html)

## 21.11  Ada  Quality  and  Style  Guide

Ada  Quality  and  Style  Guide

###### • Chapter  4:  Program  Structure

• 4.1.9Tasksˆ{[http://www.adaic.org/resources/add_content/docs/95style/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_4/4-1-9.html)  [html/sec_4/4-1-9.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_4/4-1-9.html)

• 4.1.10  Protected  Types  ˆ{[http://www.adaic.org/resources/add_content/docs/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_4/4-1-10.html)  [95style/html/sec_4/4-1-10.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_4/4-1-10.html)

• Chapter  6:  Concurrency[7](#part0187.xhtml__bookmark517)  es:Programación  en  Ada/Tareas[8](#part0187.xhtml__bookmark518)

![](Images/image07054.jpeg)

7 [http://www.adaic.org/docs/95style/html/sec_6/toc.html](http://www.adaic.org/docs/95style/html/sec_6/toc.html)

8 [http://es.wikibooks.org/wiki/Programaci%F3n%20en%20Ada%2FTareas](http://es.wikibooks.org/wiki/Programaci%F3n%20en%20Ada%2FTareas)

# 22 Object  Orientation

## 22.1 Object  orientation  in  Ada

Object  orientation  in  Ada

Object oriented programming consists in building the software in terms of "objects".  An  "object" contains data and has a behavior.  The data, normally, consists in constants and  variables as seen in the rest of this book but could also, conceivably, reside outside the  program  entirely,  i.e.  on  disk  or  on  the  network.  The  behavior  consists  in  subprograms  that operate on the data. What makes Object Orientation unique, compared to procedural  programming,  is  not  a  single  feature  but  the  combination  of  several  features:

• encapsulation,  i.e.  the ability to separate the implementation of an object from its  interface; this in turn separates "clients" of the object, who can only use the object in  certain  predefined  ways,  from  the  internals  of  the  object,  which  have  no  knowledge  of  the  outside  clients.

• inheritance, the ability for one type of objects to inherit the data and behavior (subpro-  grams)  of  another,  without  necessarily  needing  to  break  encapsulation;

• type extension, the ability for an object to add new data components and new subprograms  on  top  of  the  inherited  ones  and  to  replace  some  inherited  subprograms  with  its  own  versions;  this  is  called  overriding.

• polymorphism, the ability for a "client" to use the services of an object without knowing  the exact type of the object, i.e. in an abstract way. The actual type of the object can  indeed  change  at  run  time  from  one  invocation  to  the  next.

It  is  possible  to  do  object-oriented  programming  in  any  language,  even  assembly.  However,  type  extension  and  polymorphism  are  very  difficult  to  get  right  without  language  support.

In  Ada,  each  of  these  concepts  has  a  matching  construct;  this  is  why  Ada  supports  object-  oriented  programming  directly.

• Packages  provide  encapsulation;

• Derived  types  provide  inheritance;

• Record  extensions,  described  below,  provide  for  type  extension;

• Class-wide  types,  also  described  below,  provide  for  polymorphism.

Ada has had encapsulation and derived types since the first version (MIL-STD-1815 in 1980),  which led some to qualify the language as "object-oriented" in a very narrow sense.  Record  extensions  and  class-wide  types  were  added  in  Ada  95.  Ada  2005  further  adds  interfaces.  The  rest  of  this  chapter  covers  these  aspects.

#### 22.1.1 The  simplest  object:  the  Singleton

![](Images/image07055.jpeg)

The  Directory  is  an  object  consisting  of  data  (the  telephone  numbers  and  addresses,  presum-  ably held in an external file or database) and behavior (it can look an entry up and traverse  all  the  entries  matching  a  Name_Pattern,  calling  Visit  on  each).

A  simple  package  provides  for  encapsulation  (the  inner  workings  of  the  directory  are  hidden)  and  a  pair  of  subprograms  provide  the  behavior.

This pattern is appropriate when only one object of a certain type must exist; there is,  therefore,  no  need  for  type  extension  or  polymorphism.

#### 22.1.2 Primitive operations

For  the  following,  we  need  the  definition  of  primitive  operations:

The  set  of  primitive  operations  of  a  type  T  consists  of  those  subprograms  that:

• are  declared  immediately  within  the  same  package  as  the  type  (not  within  a  nested  package  nor  a  child  package);

• take  a  parameter  of  the  type  or,  for  functions,  return  an  object  of  the  type;

• take an  access  parameter  of  the  type  or,  for  functions, return  an  access  value  of  the type.  (Also  predefined  operators  like  equality  "="  are  primitive  operations.)

An  operation  can  be  primitive  on  two  or  more  types,  but  only  on  one  tagged  type.  The  following  example  would  be  illegal  if  also  B  were  tagged.

![](Images/image07056.jpeg)

#### 22.1.3 Derived  types

Type  derivation  has  been  part  of  Ada  since  the  very  start.

![](Images/image07057.jpeg)

![](Images/image07058.jpeg)

The above example creates a type T that contains data (here just a Boolean but it could be  anything)  and  behavior  consisting  of  some  subprograms.  It  also  demonstrates  encapsulation  by  placing  the  details  of  the  type  T  in  the  private  part  of  the  package.

The  primitive  operations  of  T are  the  function  Create,  the  overloaded  procedures  Work,  and  the  predefined  "="  operator;  Proc  is  not  primitive,  since  it  has  an ac-  cess  type  on  T  as  parameter  —  don't  confuse  this  with  an  access  parameter,  as  used  in  the  second  procedure  Work.  When  deriving  from  T,  the  primitive  operations  are  inherited.

![](Images/image07059.jpeg)

The  type  Q.Derived  has  the  same  data  and  the  same  behavior  as  P.T;  it  inherits  both  the  data  and  the  subprograms.  Thus  it  is  possible  to  write:

![](Images/image07060.jpeg)

Admittedly,  the  reasons for  writing this  may seem  obscure.  The  purpose of  this kind  of code  is  to  have  objects  of  types  P.T  and  Q.Derived,  which  are  not  compatible:

![](Images/image07061.jpeg)

This  feature  is  not  used  very  often  (it's  used  e.g.  for  declaring  types  reflecting  physical  dimensions)  but  I  present  it  here  to  introduce  the  next  step:  type  extension.

#### 22.1.4 Type  extensions

Type  extensions  are  an  Ada  95  amendment.

A  tagged  type  provides  support  for  dynamic  polymorphism  and  type  extension.  A  tagged  type  bears  a  hidden  tag  that  identifies  the  type  at  run-time.  Apart  from  the  tag,  a  tagged

record  is  like  any  other  record,  so  it  can  contain  arbitrary  data.

![](Images/image07062.jpeg)

As  you  can  see,  a  Person.Object  is  an  object  in  the  sense  that  it  has  data  and  behavior  (the  procedure  Put).  However,  this  object  does  not  hide  its  data;  any  program  unit  that  has  a  with  Person  clause  can  read  and  write  the  data  in  a  Person.Object  directly.  This  breaks  encapsulation  and  also  illustrates  that  Ada  completely  separates  the  con-  cepts  of  encapsulation  and  type.  Here  is  a  version  of  Person.Object  that  encapsulates  its  data:

![](Images/image07063.jpeg)

Because  the  type  Person.Object  is  tagged,  it  is  possible  to  create  a  record  extension,  which  is  a  derived  type  with  additional  data.

![](Images/image07064.jpeg)

The  type  Programmer.Object  inherits  the  data  and  behavior,  i.e.  the  type's  primitive  operations,  from  Person.Object;  it  is  thus  possible  to  write:

![](Images/image07065.jpeg)

So  the  declaration  of  the  type  Programmer.Object,  as  a  record  extension  of  Person.Object,  implicitly  declares  a  procedure  Put  that  applies  to  a  Programmer.Object.

Like in the case of untagged types, objects of type Person and Programmer are convertible.  However, where untagged objects are convertible in either direction, conversion of tagged  types  only  works  in  the  direction  to  the  root.  (Conversion  away  from  the  root  would  have  to add components out of the blue.) Such a conversion is called a view conversion, because  components  are  not  lost,  they  only  become  invisible.

Extension  aggregates  have  to  be  used  if  you  go  away  from  the  root.

#### 22.1.5 Overriding

Now  that  we  have  introduced  tagged  types,  record  extensions  and  primitive  operations,  it  becomes  possible  to  understand  overriding.   In  the  examples  above,  we  introduced  a type  Person.Object  with  a  primitive operation  called Put.  Here is  the  body  of  the package:

![](Images/image07066.jpeg)

As  you  can  see,  this  simple  operation  prints  both  data  components  of  the  record  type  to  standard output. Now, remember that the record extension Programmer.Object has an  additional  data  member.  If  we  write:

![](Images/image07067.jpeg)

then the program will call the inherited primitive operation Put, which will print the name  and gender but not the additional data.  In order to provide this extra behavior, we must  override  the  inherited  procedure  Put  like  this:

![](Images/image07068.jpeg)

![](Images/image07069.jpeg)

Programmer.Put overrides Person.Put; in other words it replaces it completely.  Since  the  intent  is  to  extend  the  behavior  rather  than  replace  it,  Programmer.Put  calls  Person.Put as part of its behavior.  It does this by converting its parameter from the  type Programmer.Object to its ancestor type Person.Object.  This construct is a view  conversion; contrary to a normal type conversion, it does not create a new object and does  not incur any run-time cost. Of course, it is optional that an overriding operation call its  ancestor;  there  are  cases  where  the  intent  is  indeed  to  replace,  not  extend,  the  inherited  behavior.

(Note  that  also  for  untagged  types,  overriding  of  inherited  operations  is  possible.  The  reason  why  it's  discussed  here  is  that  derivation  of  untagged  types  is  done  rather  seldom.)

#### 22.1.6 Polymorphism,  class-wide  programming  and  dynamic  dispatching

The full power of object orientation is realized by polymorphism, class-wide programming  and dynamic dispatching, which are different words for the same, single concept. To explain  this  concept,  let  us  extend  the  example  from  the  previous  sections,  where  we  declared  a  base tagged type Person.Object with a primitive operation Put and a record extension  Programmer.Object  with  additional  data  and  an  overriding  primitive  operation  Put.

Now, let us imagine a collection of persons.  In the collection, some of the persons are  programmers. We want to traverse the collection and call Put on each person. When the  person under consideration is a programmer, we want to call Programmer.Put; when the  person is not a programmer, we want to call Person.Put. This, in essence, is polymorphism,  class-wide  programming  and  dynamic  dispatching.

Ada  implements  this  concept  by  means  of  class-wide  types.

Each  tagged  type,  such  as  Person.Object,  has  a  corresponding  class  of  types  which  is  the  set  of  types  comprising  the  type  Person.Object  itself  and  all  types  that  extend  Person.Object.  In  our  example,  this  class  consists  of  two  types:

• Person.Object

• Programmer.Object

Ada  95  defines  the  Person.Object'Class  attribute  to  denote  the  corresponding  class-wide type.  In  other  words:

![](Images/image07070.jpeg)

The  declaration  of  Someone  denotes  an  object  that  may  be  of  either  type,  Person.Object  or Programmer.Object. Consequently, the call to the primitive operation Put dispatches  dynamically  to  either  Person.Put  or  Programmer.Put.

The  only  problem  is  that,  since  we  don't  know  whether  Someone  is  a  programmer  or  not,  we don't know how many data components Someone has, either, and therefore we don't  know how many bytes Someone takes in memory.  For this reason, the class-wide type  Person.Object'Class  is  indefinite[1](#part0195.xhtml__bookmark523).  It  is  impossible  to  declare  an  object  of  this  type  without  giving  some  constraint.  It  is,  however,  possible  to:

• declare  an  object  of  a  class-wide  with  an  initial  value  (as  above).  The  object  is  then  constrained  by  its  initial  value.

• declare  an  access  value  to  such  an  object  (because  the  access  value  has  a  known  size);

• pass  objects  of  a  class-wide  type  as  parameters  to  subprograms

• assign  an  object  of  a  specific  type  (in  particular,  the  result  of  a  function  call)  to  a  variable  of  a  class-wide  type.

With  this  knowledge,  we  can  now  build  a  polymorphic  collection  of  persons;  in  this  example  we  will  quite  simply  create  an  array  of  access  values  to  persons:

![](Images/image07071.jpeg)

The above procedure achieves our desired goal: it traverses the array of Persons and calls  the  procedure  Put  that  is  appropriate  for  each  person.

###### Advanced  topic:  How  dynamic  dispatching  works

You don't need to know how dynamic dispatching works in order to use it effectively but, in  case  you  are  curious,  here  is  an  explanation.

The first component of each object in memory is the tag; this is why objects are of a tagged  type rather than plain records. The tag really is an access value to a table; there is one table  for each specific type. The table contains access values to each primitive operation of the  type.  In our example, since there are two types Person.Object and Programmer.Object,  there are two tables, each containing a single access value.  The table for Person.Object  contains an access value to Person.Put and the table for Programmer.Object contains an  access value to Programmer.Put. When you compile your program, the compiler constructs  both  tables  and  places  them  in  the  program  executable  code.

![](Images/image07072.jpeg)

1 [http://en.wikibooks.org/wiki/ada%20Programming%2FSubtypes%23Indefinite_subtype](http://en.wikibooks.org/wiki/ada%20Programming%2FSubtypes%23Indefinite_subtype)

Each  time  the  program  creates  a  new  object  of  a  specific  type,  it  automatically  sets  its  tag  to  point  to  the  appropriate  table.

Each  time  the  program  calls  a  primitive  operation,  the  compiler  inserts  object  code  that:

• dereferences  the  tag  to  find  the  table  of  primitive  operations  for  the  specific  type  of  the  object  at  hand

• dereferences  the  access  value to  the  primitive  operation

• calls  the  primitive  operation.

When you perform a view conversion to an ancestor type, the compiler performs these two  dereferences at compile time rather than run time: this is static dispatching; the compiler  emits code that directly calls the primitive operation of the ancestor type specified in the  view  conversion.

###### Redispatching

Dispatching works on the (hidden) tag of the object.  So what happens when a primitive  operation Op1 calls another primitive operation Op2? Which operation will be called when  Op1  is  called  by  dispatching?

![](Images/image07073.jpeg)

In this fragment, Op1 is not overridden, whereas Op2 is overridden. The body of Op1 calls  Op2,  thus  which  Op2  will  be  called  for  a  call  of  Op1  with  a  parameter  of  type  Derived?

The answer is: Ada gives complete control over dispatching and redispatching. If you want  redispatching, it has to be required explicitly by converting the parameter to the class-wide  type again. (Remember: View conversions never lose components, they just hide them. A  conversion  to  the  class-wide  type  makes  them  visible  again.)

Thus  the  first  call  of  Op1  (statically  linked,  i.e.  not  dispatching)  calls  the  inherited  Op1

— and within Op1, the first call to Op2 is therefore also a static call to the inherited Op2  (there is no redispatching). However the second call, since the parameter R is converted to  the  class-wide  type,  dispatches  to  the  overriding  Op2.

The  second  call  of  Op1  is  a  dispatching  call  to  the  inherited  Op1  and  behaves  exactly  as  the  first.

To  understand  what  happens  here,  the  implicitly  defined  inherited  Op1  is  just  the  parent  operation  called  with  a  view  conversion  of  the  parameter:

![](Images/image07074.jpeg)

###### Run-time  type  identification

Run-time  type  identification  allows  the  program  to  (indirectly  or  directly)  query  the  tag  of  an object at run time to determine which type the object belongs to. This feature, obviously,  makes  sense  only  in  the  context  of  polymorphism  and  dynamic  dispatching,  so  works  only  on  tagged  types.

You can determine whether an object belongs to a certain class of types, or to a specific  type,  by  means  of  the  membership  test  in,  like  this:

![](Images/image07075.jpeg)

Thanks  to  the  strong  typing  rules  of  Ada,  run-time  type  identification  is  in  fact  rarely  needed;  the  distinction  between  class-wide  and  specific  types  usually  allows  the  programmer  to  ensure  objects  are  of  the  appropriate  type  without  resorting  to  this  feature.

Additionally, the reference manual defines package Ada.Tags (RM 3.9(6/2)), attribute  'Tag  (RM  3.9(16,18)),  and  function  Ada.Tags.Generic_Dispatching_Constructor  (RM  3.9(18.2/2)),  which  enable  direct  manipulation  with  tags.

#### 22.1.7 Creating  Objects

The  Language  Reference  Manual's  section  on  3.3  Objects  and  Named  Numbers  ˆ{[http://www.](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-3.html)  [adaic.org/resources/add_content/standards/05rm/html/RM-3-3.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-3.html)          states     when  an  object  is  created,  and  destroyed  again.  This  subsection  illustrates  how  objects  are  created.

![](Images/image07076.jpeg)Objects  are  created  at  run  time  and  contain  a  value  of  a  given  type.  An  object

The  LRM  section  starts,be  created  and  initialized  as  part  of  elaborating  a  declaration,  evaluating  an  alloc

aggregate,  or  function_call.

For example, assume a typical hierarchy of object oriented types: a top-level type Person, a  Programmer  type  derived  from  Person,  and  possibly  more  kinds  of  persons.  Each  person  has a name; assume Person objects to have a Name component.  Likewise, each Person has  a  Gender  component.  The  Programmer  type  inherits  the  components  and  the  operations  of the Person type, so Programmer objects have a Name and a Gender component, too.  Programmer  objects  may  have  additional  components  specific  to  programmers.

Objects of a tagged type are created the same way as objects of any type. The second LRM  sentence says, for example, that an object will be created when you declare a variable or a  constant  of  a  type.  For  the  tagged  type  Person,

![](Images/image07077.jpeg)

Nothing special so far. Just like any ordinary variable declaration this O-O one is elaborated.  The result of elaboration is an object named P of type Person. However, P has only default  name and gender value components.  These are likely not useful ones.  One way of giving  initial  values  to  the  object's  components  is  to  assign  an  aggregate.

![](Images/image07078.jpeg)

The parenthesized expression after := is called an aggregate (4.3 Aggregates ˆ{[http://www.](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-3.html)  [adaic.org/resources/add_content/standards/05rm/html/RM-4-3.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-3.html) ).

Another  way  to  create  an  object  that  is  mentioned  in  the  LRM  paragraph  is  to  call  a  function.  An  object  will  be  created  as  the  return  value  of  a  function  call.  Therefore,  instead  of  using  an  aggregate  of  initial  values,  we  might  call  a  function  returning  an  object.

Introducing  proper  O-O  information  hiding,  we  change  the  package  containing  the  Person  type  so  that  Person  becomes  a  private  type.  To  enable  clients  of  the  package  to  construct  Person  objects  we  declare  a  function  that  returns  them.  (The  function  may do some interesting construction work on the objects.  For instance, the aggregate  above  will  most  probably  raise  the  exception  Constraint_Error  depending   on   the  name  string  supplied;  the  function  can  mangle  the  name  so  that  it  matches  the  decla-  ration  of  the  component.)  We  also  declare  a  function  that  returns  the  name  of  Person  objects.

![](Images/image07079.jpeg)

![](Images/image07080.jpeg)

Calling the Make function results in an object which can be used for initialization. Since the  Person  type  is  private  we  can  no  longer  refer  to  the  Name  component  of  P.  But  there  is  a corresponding function Name declared with type Person making it a socalled primitive  operation.  (The  component  and  the  function  in  this  example  are  both  named  Name  However,  we  can  choose  a  different  name  for  either  if  we  want.)

![](Images/image07081.jpeg)

Objects  can  be  copied  into  another.  The  target  object  is  first  destroyed.  Then  the  component values of the source object are assigned to the corresponding components of the  target  object.  In  the  following  example,  the  default  initialized P  gets  a  copy  of  one  of  the  objects  created  by  the  Make  calls.

![](Images/image07082.jpeg)

So far there is no mention of the Programmer type derived from Person.  There is no  polymorphism yet,  and likewise initialization does not yet mention inheritance.  Before  dealing with Programmer objects and their initialization a few words about class-wide types  are  in  order.

#### 22.1.8 More  details  on  primitive  operations

Remember  what  we  said  before  about  "Primitive  Operations"[2](#part0199.xhtml__bookmark524).  Primitive  operations  are:

• subprograms  taking  a  parameter  of  the  tagged  type;

• functions  returning  an  object  of  the  tagged  type;

• subprograms  taking  a  parameter  of  an  anonymous  access  type  to  the  tagged  type;

![](Images/image07083.jpeg)

2 Chapter  [22.1.2](#part0190.xhtml__bookmark521)  on  page  [188](#part0190.xhtml__bookmark521)

• In  Ada  2005  only,  functions  returning  an  anonymous  access  type  to  the  tagged  type;

Additionally,  primitive  operations  must  be  declared  before  the  type  is  frozen  (the  concept  of  freezing  will  be  explained  later):

Examples:

![](Images/image07084.jpeg)

All  of  these  subprograms  are  primitive  operations.

A  primitive  operation  can  also  take  parameters  of  the  same  or  other  types;  also,  the  controlling  operand  does  not  have  to  be  the  first  parameter:

![](Images/image07085.jpeg)

The  definition  of  primitive  operations  specifically  excludes  named  access  types  and  class-wide types as well as operations not defined immediately in the same declarative  region.  Counter-examples:

![](Images/image07086.jpeg)

###### Advanced  topic:  Freezing  rules

Freezing rules ([http://www.adaic.com/standards/05rm/html/RM-13-14.html](http://www.adaic.com/standards/05rm/html/RM-13-14.html)   ARM  13.14[3](#part0201.xhtml__bookmark525))  are  perhaps  the  most  complex  part  of  the  Ada  language  definition;  this  is  be-  cause  the  standard  tries  to  describe  freezing  as  unambiguously  as  possible.  Also,  that  part of the language definition deals with freezing of all entities, including complicated  situations like generics and objects reached by dereferencing access values. You can, however,  get an intuitive understanding of freezing of tagged types if you understand how dynamic  dispatching works[4](#part0201.xhtml__bookmark526).  In that section, we saw that the compiler emits a table of primitive  operations for each tagged type. The point in the program text where this happens is the  point where the tagged type is frozen, i.e.  the point where the table becomes complete.  After  the  type  is  frozen,  no  more  primitive  operations  can  be  added  to  it.

This  point  is  the  earliest  of:

• the  end  of  the  package  spec  where  the  tagged  type  is  declared

• the  appearance  of  the  first  type  derived  from  the  tagged  type  Example:

![](Images/image07087.jpeg)

Intuitively:  at the point where Derived is declared,  the compiler starts a new table of  primitive operations for the derived type.  This new table, initially, is equal to the table of  the  primitive  operations  of  the  parent  type,  Object.  Hence,  Object  must  freeze.

• the declaration of a variable of the tagged type  Example:

![](Images/image07088.jpeg)![](Images/image07089.jpeg)

3 [http://en.wikibooks.org/wiki/%20ARM%2013.14](http://en.wikibooks.org/wiki/%20ARM%2013.14)

4 Chapter  [22.1.6](#part0195.xhtml__bookmark522)  on  page  [193](#part0195.xhtml__bookmark522)

Intuitively: after the declaration of V, it is possible to call any of the primitive operations of  the type on V. Therefore, the list of primitive operations must be known and complete, i.e.  frozen.

• The  completion  (not  the  declaration,  if  any)  of  a  constant  of  the  tagged  type:

![](Images/image07090.jpeg)

#### 22.1.9 New  features  of  Ada  2005

This  language  feature  is  only  available  in  Ada  2005

Ada  2005  adds  overriding  indicators,  allows  anonymous  access  types  in  more  places  and  offers  the  object.method  notation.

###### Overriding  indicators

The  new  keyword  overriding  can  be  used  to  indicate  whether  an  operation  overrides  an  inherited  subprogram  or  not.  Its  use  is  optional  because  of  upward-compatibility  with  Ada

95.  For  example:

![](Images/image07091.jpeg)

The  compiler  will  check  the  desired  behaviour.

This is a good programming practice because it avoids some nasty bugs like not overriding  an  inherited  subprogram  because  the  programmer  spelt  the  identifier  incorrectly,  or  because  a  new  parameter  is  added  later  in  the  parent  type.

It can also be used with abstract operations, with renamings, or when instantiating a  generic  subprogram:

![](Images/image07092.jpeg)

###### Object.Method notation

We  have  already  seen  this  notation:

![](Images/image07093.jpeg)

![](Images/image07094.jpeg)

This  notation  is  only  available  for  primitive  operations  where  the  controlling  parameter  is  the  first  parameter.

#### 22.1.10 Abstract  types

A  tagged  type  can  also  be  abstract  (and  thus  can  have  abstract  operations):

![](Images/image07095.jpeg)

An abstract operation cannot have any body, so derived types are forced to override it  (unless those derived types are also abstract).  See next section about interfaces for more  information  about  this.

The difference with a non-abstract tagged type is that you cannot declare any variable of  this type. However, you can declare an access to it, and use it as a parameter of a class-wide  operation.

#### 22.1.11 Multiple  Inheritance  via  Interfaces

This  language  feature  is  only  available  in  Ada  2005

Interfaces allow for a limited form of multiple inheritance (taken from Java). On a semantic  level they are similar to an "abstract tagged null record" as they may have primitive operations  but cannot hold any data and thus these operations cannot have a body, they are either  declared abstract or null. Abstract means the operation has to be overridden, null means  the  default  implementation  is  a  null  body,  i.e.  one  that  does  nothing.

An  interface  is  declared  with:

![](Images/image07096.jpeg)

You  implement an  interface by adding  it  to a  concrete class:

![](Images/image07097.jpeg)

As  usual,  all  inherited  abstract  operations  must  be  overridden  although  null  subprograms

ones  need  not.

Such  a  type  may  implement  a  list  of  interfaces  (called  the  progenitors),  but  can  have  only  one  parent.  The  parent  may  be  a  concrete  type  or  also  an  interface.

![](Images/image07098.jpeg)

#### 22.1.12 Multiple  Inheritance  via  Mix-in

Ada supports multiple inheritance of interfaces (see above), but only single inheritance of  implementation. This means that a tagged type can implement multiple interfaces but can  only  extend  a  single  ancestor  tagged  type.

This  can  be  problematic  if  you  want  to  add  behavior  to  a  type  that  already  extends  another  type;  for  example,  suppose  you  have

![](Images/image07099.jpeg)

and  you  want  to  make  Derived  controlled,  i.e.  add  the  behavior  that  Derived  controls  its  initialization,  assignment  and  finalization.  Alas  you  cannot  write:

![](Images/image07100.jpeg)

since  Ada.Finalization  for  historical  reasons  does  not  define  interfaces  Controlled  and

Limited_Controlled,  but  abstract  types.

If  your  base  type  is  not  limited,  there  is  no  good  solution  for  this;  you  have  to  go  back  to  the  root  of  the  class  and  make  it  controlled.  (The  reason  will  become  obvious  presently.)

For  limited  types  however,  another  solutions  is  the  use  of  a  mix-in:

![](Images/image07101.jpeg)

This special kind of mix-in is an object with an access discriminant that references its  enclosing object (also known as Rosen trick). In the declaration of the Derived type, we  initialize this discriminant with a special syntax:  Derived'Access really refers to an a  access  value  to  the  current  instance  of  type  Derived.  Thus  the  access  discriminant  allows  the  mix-in  to  see  its  enclosing  object  and  all  its  components;  therefore  it  can  initialize  and

finalize  its  enclosing  object:

![](Images/image07102.jpeg)

and  similarly  for  Finalize.

The reason why this does not work for non-limited types is the self-referentiality via the  discriminant. Imagine you have two variables of such a non-limited type and assign one to  the  other:

![](Images/image07103.jpeg)

In an assignment statement,  Adjust is called only after Finalize of the target X and  so cannot provide the new value of the discriminant. Thus X.Mixin_In.Enclosing will  inevitably  reference  Y.

Now  let's  further  extend  our  hierarchy:

![](Images/image07104.jpeg)

Oops,  this  does  not  work  because  there  are  no  corresponding  procedures  for  Derived,  yet  -  so  let's  quickly  add  them.

![](Images/image07105.jpeg)

We  have  of  course  to  write  not  overriding  for  the  procedures  on  Derived  because  there  is  indeed  nothing  they  could  override.  The  bodies  are

![](Images/image07106.jpeg)

To  our  dismay,  we  have  to  learn  that  Initialize/Finalize  for  objects  of  type  Further

will  not  be  called,  instead  those  for  the  parent  Derived.  Why?

![](Images/image07107.jpeg)

The  reason  is  that  the  mix-in  defines  the  local  object  Enclosing  to  be  of  type  Derived  in the renames-statement above.  To cure this, we have necessarily to use the dreaded  redispatch  (shown  in  different  but  equivalent  notations):

![](Images/image07108.jpeg)

Alternatively  (and  presumably better  still)  is to  write

![](Images/image07109.jpeg)

Then  we  automatically  get  redispatch  and  can  omit  the  type  conversions  on  Enclosing.

## 22.2 Class  names

Class  names

Both  the  class  package  and  the  class  record  need  a  name.  In  theory  they  may  have  the  same name, but in practice this leads to nasty (because of unintutive error messages) name  clashes when you use the use clause. So over time three de facto naming standards have  been  commonly  used.

#### 22.2.1 Classes/Class

The package is named by a plural noun and the record is named by the corresponding  singular  form.

![](Images/image07110.jpeg)

This  convention  is the usually used  in Ada's  built-in libraries.

Disadvantage:  Some  "multiples"  are  tricky  to  spell,  especially  for  those  of  us  who  aren't  native  English  speakers.

#### 22.2.2 Class/Object

The  package  is  named  after  the  class,  the  record  is  just  named  Object.

![](Images/image07111.jpeg)

Most  UML[5](#part0208.xhtml__bookmark528)  and  IDL[6](#part0208.xhtml__bookmark529)  code  generators  use  this  technique.

Disadvantage:  You  can't  use  the  use  clause  on  more  than  one  such  class  packages  at  any  one  time.  However  you  can  always  use  the  "type"  instead  of  the  package.

![](Images/image07112.jpeg)

5 [http://en.wikipedia.org/wiki/Unified%20Modeling%20Language](http://en.wikipedia.org/wiki/Unified%20Modeling%20Language)

6 [http://en.wikipedia.org/wiki/Interface%20description%20language](http://en.wikipedia.org/wiki/Interface%20description%20language)

#### 22.2.3 Class/Class_Type

The  package  is  named  after  the  class,  the  record  is  postfixed  with  _Type.

![](Images/image07113.jpeg)

Disadvantage:  lots  of  ugly  "_Type"  postfixes.

## 22.3 Object-Oriented  Ada  for  C++  programmers

Object-Oriented  Ada  for  C++  programmers

In  C++,  the  construct

![](Images/image07114.jpeg)

is  strictly  equivalent  to  the  following  in  Ada:

![](Images/image07115.jpeg)

In C++, member functions implicitly take a parameter this which is of type C*. In Ada,  all  parameters  are  explicit.  As  a  consequence,  the  fact  that  u()  does  not  take  a  parameter  is  implicit  in  C++  but  explicit  in  Ada.

In C++, this is a pointer.  In Ada, the explicit This parameter does not have to be a  pointer;  all  parameters  of  a  tagged  type  are  implicitly  passed  by  reference  anyway.

#### 22.3.1 Static  dispatching

In  C++,  function  calls  dispatch  statically  in  the  following  cases:

• the  target  of  the  call  is  an  object  type

• the  member  function  is  non-virtual

For  example:

![](Images/image07116.jpeg)

both dispatch statically.  In particular, the static dispatch for v() may be confusing; this is  because object is neither a pointer nor a reference. Ada behaves exactly the same in this  respect,  except  that  Ada  calls  this  static  binding  rather  than  dispatching:

![](Images/image07117.jpeg)

#### 22.3.2 Dynamic  dispatching

In  C++,  a  function  call  dispatches  dynamically  if  the  two  following  conditions  are  met  simultaneously:

• the  target  of  the  call  is  a  pointer  or  a  reference

• the  member  function  is  virtual.  For  example:

![](Images/image07118.jpeg)

In  Ada,  a  primitive  subprogram  call  dispatches  (dynamically)  if  and  only  if:

• the  target  object  is  of  a  class-wide  type;

Note:  In  Ada  vernacular,  the  term  dispatching  always  means  dynamic.  For  example:

![](Images/image07119.jpeg)

As can be seen there  is  no  need  for  access  types  or  pointers to do dispatching in Ada.  In  Ada, tagged types are always passed by-reference to subprograms without the need for explicit  access  values.

Also  note  that  in  C++,  the  class  serves  as:

• the  unit  of  encapsulation  (Ada  uses  packages  and  visibility  for  this)

• the  type,  like  in  Ada.

As  a  consequence,  you  call  C::u()  in  C++  because  u()  is  encapsulated  in  C,  but  P.U  in  Ada  since  U  is  encapsulated  in  the  package  P,  not  the  type  C.

#### 22.3.3 Class-wide  and  specific  types

The most confusing part for C++ programmers is the concept of a "class-wide type".  To  help  you  understand:

• pointers  and  references  in  C++  are  really,  implicitly,  class-wide;

• object  types  in  C++  are  really  specific;

• C++  provides  no  way  to  declare  the  equivalent  of:

![](Images/image07120.jpeg)

• C++  provides  no  way  to  declare  the  equivalent  of:

![](Images/image07121.jpeg)

which,  in  Ada,  are  two  different,  incompatible  types,  possibly  allocating  their  memory  from  different  storage  pools!

• In  Ada,  you  do  not  need  access  values  for  dynamic  dispatching.

• In  Ada,  you  use  access  values  for  dynamic  memory  management  (only)  and  class-wide  types  for  dynamic  dispatching  (only).

• In  C++,  you  use  pointers  and  references  both  for  dynamic  memory  management  and  for  dynamic  dispatching.

• In  Ada,  class-wide  types  are  explicit  (with  'Class).

• In  C++,  class-wide  types  are  implicit  (with  *  or  &).

#### 22.3.4 Constructors

in  C++, a  special  syntax  declares  a  constructor:

![](Images/image07122.jpeg)

A constructor cannot be virtual.  A class can have as many constructors, differentiated by  their  parameters,  as  necessary.

Ada  does  not  have  such  constructors.  Perhaps  they  were  not  deemed  necessary  since  in  Ada,  any  function  that  returns  an  object  of  the  tagged  type  can  serve  as  a  kind  of  constructor.  This  is  however  not  the  same  as  a  real  constructor  like  the  C++  one;  this  difference  is  most  striking  in  cases  of  derivation  trees  (see  Finalization  below).  The  Ada  constructor

subprograms  do  not  have  to  have  a  special  name  and  there  can  be  as  many  constructors  as  necessary;  each  function  can  take  parameters  as  appropriate.

![](Images/image07123.jpeg)

If an Ada constructor function is also a primitive operation (as in the example above), it  becomes abstract upon derivation and has to be overridden if the derived type is not itself  abstract.  If  you  do  not  want  this,  declare  such  functions  in  a  nested  scope.

In  C++,  one  idiom  is  the  copy  constructor  and  its  cousin  the  assignment  operator:

![](Images/image07124.jpeg)

This  copy  constructor  is  invoked  implicitly  on  initialization,  e.g.

![](Images/image07125.jpeg)

Ada  provides  a  similar  functionality  by  means  of  controlled  types.  A  controlled  type  is  one  that  extends  the  predefined  type  Ada.Finalization.Controlled:

![](Images/image07126.jpeg)

Note  that  Initialize  is  not  a  constructor;  it  resembles  the  C++  constructor  in  some  way,  but  is also very different.  Suppose you have a type T1 derived from T with an appropriate  overriding of Initialize.  A real constructor (like the C++ one) would automatically first  construct the parent components (T), then the child components.  In Ada, this is not  automatic.  In  order  to  mimic  this  in  Ada,  we  have  to  write:

![](Images/image07127.jpeg)

![](Images/image07128.jpeg)

The compiler inserts a call to Initialize after each object of type T is allocated when no  initial value is given. It also inserts a call to Adjust after each assignment to the object.  Thus,  the  declarations:

![](Images/image07129.jpeg)

will:

• allocate  memory  for  A

• call  Initialize  (A)

• allocate  memory  for  B

• copy  the  contents  of  X  to  B

• call  Adjust  (B)

Initialize  (B)  will  not  be  called  because  of  the  explicit  initialization.  So,  the  equivalent  of  a  copy  constructor  is  an  overriding  of  Adjust.

If  you  would  like  to  provide  this  functionality  to  a  type  that  extends  another,  non-controlled  type,  see  "Multiple  Inheritance"[7](#part0213.xhtml__bookmark531).

#### 22.3.5 Destructors

In  C++,  a  destructor  is  a  member  function  with  only  the  implicit  this  parameter:

![](Images/image07130.jpeg)

While a constructor cannot be virtual, a destructor must be virtual. Unfortunately, the rules  of the C++ language do not enforce this, so it is quite easy for a programmer to wreak  havoc  in  their  programs  by  simply  forgetting  the  keyword  virtual.

In Ada, the equivalent functionality is again provided by controlled types, by overriding the  procedure  Finalize:

![](Images/image07131.jpeg)

![](Images/image07132.jpeg)

7 Chapter  [22.4.2](#part0219.xhtml__bookmark533)  on  page  [217](#part0219.xhtml__bookmark533)

![](Images/image07133.jpeg)

Because  Finalize  is  a  primitive  operation,  it  is  automatically  "virtual";  you  cannot,  in  Ada,  forget  to  make  a  destructor  virtual.

#### 22.3.6 Encapsulation:  public,  private  and  protected  members

In C++, the unit of encapsulation is the class;  in Ada, the unit of encapsulation is the  package.  This  has  consequences  on  how  an  Ada  programmer  places  the  various  components  of  an  object  type.

![](Images/image07134.jpeg)

A  way  to  mimic  this  C++  class  in  Ada  is  to  define  a  hierarchy  of  types,  where  the  base  type  is the public part, which must be abstract so that no stand-alone objects of this base type  can  be  defined.  It  looks  like  so:

![](Images/image07135.jpeg)

![](Images/image07136.jpeg)

The  private  part  is  defined  as  a  stub  only,  its  completion  is  hidden  in  the  body.  In  order  to  make  it  a  component  of  the  complete  type,  we  have  to  use  a  pointer  since  the  size  of  the component is still unknown (the size of a pointer is known to the compiler).  With  pointers,  unfortunately,  we  incur  the  danger  of  memory  leaks,  so  we  have  to  make  the  private  component  controlled.

For a little test, this is the body, where the subprogram bodies are provided with identifying  prints:

![](Images/image07137.jpeg)

![](Images/image07138.jpeg)

We  see  that,  due  to  the  construction,  the  private  procedure  is  not  a  primitive  operation.  Let's  define  a  child  class  so  that  the  protected  operation  can  be  reached:

![](Images/image07139.jpeg)

A  child  can  look  inside  the  private  part  of  the  parent  and  thus  can  see  the  protected  procedure:

![](Images/image07140.jpeg)

This  is  a  simple  test  program,  its  output  is  shown  below.

![](Images/image07141.jpeg)

This  is  the  commented  output  of  the  test  program:

![](Images/image07142.jpeg)

You  see  that  a  direct  translation  of  the  C++  behaviour  into  Ada  is  difficult,  if  feasible  at  all.  Methinks,  the  primitive  Ada  subprograms  corresponds  more  to  virtual  C++  methods  (in the example, they are not). Each language has its own idiosyncrasies which have to be  taken into account, so that attempts to directly translate code from one into the other may  not  be  the  best  approach.

#### 22.3.7 De-encapsulation:  friends  and  stream  input-output

In C++, a friend function or class can see all members of the class it is a friend of. Friends  break encapsulation and are therefore to be discouraged. In Ada, since packages and not  classes are the unit of encapsulation, a "friend" subprogram is simply one that is declared in  the  same  package  as  the  tagged  type.

In  C++,  stream  input  and  output  are  the  particular  case  where  friends  are  usually  necessary:

![](Images/image07143.jpeg)

![](Images/image07144.jpeg)

Ada  does  not  need  this  construct  because  it  defines  stream  input  and  output  operations  by  default:

![](Images/image07145.jpeg)

![](Images/image07146.jpeg)

By default, the Output attribute sends the tag of the object to the stream then calls the  more  basic  Write  attribute,  which  sends  the  components  to  the  stream  in  the  same  order  as  the declaration, i.e. A, B then C. It is possible to override the default implementation of the  Input,  Output,  Read  and  Write  attributes  like  this:

![](Images/image07147.jpeg)

In  the  above  example,  P.C'output  calls  P.C'Write  which  is  overridden  in  the  body  of  the package. Since the specification of package P does not define any subprograms, it does not  normally need a body, so a package body is forbidden.  The pragma  Elaborate_Body tells  the  compiler  that  this  package  does  have  a  body  that  is  needed  for  other  reasons.

Note that the stream IO attributes are not primitive operations of the tagged type; this is  also the case in C++ where the friend operators are not, in fact, member functions of the  type.

22.3.8 Terminology

| Ada | C++ |
| Package | class  (as  a  unit  of  encapsulation) |
| Tagged  type | class  (of  objects)  (as  a  type)  (not  pointer  orreference,  which  are  class-wide) |
| Primitive  operation | virtual  member  function |
| Tag | pointer  to  the  virtual  table |
| Class  (of  types) | - |
| Class-wide  type | - |
| Class-wide  operation | static  member  function |
| Access  value  to  a  specific  taggedtype | - |
| Access  value  to  a  class-wide  type | Pointer  or  reference  to  a  class |

## 22.4 See  also

See  also

#### 22.4.1 Wikibook

• Ada  Programming[8](#part0219.xhtml__bookmark534)

• Ada  Programming/Types/record[9](#part0219.xhtml__bookmark535)

• record[10](#part0219.xhtml__bookmark536)

• interface[11](#part0219.xhtml__bookmark537)

• tagged[12](#part0219.xhtml__bookmark538)

#### 22.4.2 Wikipedia

• Object-oriented  programming[13](#part0219.xhtml__bookmark539)

![](Images/image07148.jpeg)

8 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

9 Chapter  [12](#part0093.xhtml__bookmark318)  on  page  [91](#part0093.xhtml__bookmark318)

10 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Frecord](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Frecord)

11 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Finterface](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Finterface)

12 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Ftagged](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Ftagged)

13 [http://en.wikipedia.org/wiki/Object-oriented%20programming](http://en.wikipedia.org/wiki/Object-oriented%20programming)

#### 22.4.3 Ada  Reference  Manual

###### Ada  95

• 3.8  Record  Types  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-8.html)  [95lrm/ARM_HTML/RM-3-8.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-8.html)

• 3.9  Tagged  Types  and  Type  Extensions  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-9.html)  [content/standards/95lrm/ARM_HTML/RM-3-9.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-9.html)

• 3.9.1  Type  Extensions  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-9-1.html)  [95lrm/ARM_HTML/RM-3-9-1.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-9-1.html)

• 3.9.2  Dispatching  Operations  of  Tagged  Types  ˆ{[http://www.adaic.org/resources/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-9-2.html)  [add_content/standards/95lrm/ARM_HTML/RM-3-9-2.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-9-2.html)

• 3.9.3  Abstract  Types  and  Subprograms  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-9-3.html)  [content/standards/95lrm/ARM_HTML/RM-3-9-3.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-9-3.html)

• 3.10  Access  Types  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-10.html)  [95lrm/ARM_HTML/RM-3-10.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-3-10.html)

###### Ada  2005

• 3.8  Record  Types  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-8.html)  [05rm/html/RM-3-8.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-8.html)

• 3.9  Tagged  Types  and  Type  Extensions  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-9.html)  [content/standards/05rm/html/RM-3-9.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-9.html)

• 3.9.1  Type  Extensions  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-9-1.html)  [05rm/html/RM-3-9-1.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-9-1.html)

• 3.9.2 Dispatching Operations of Tagged Types  ˆ{[http://www.adaic.org/resources/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-9-2.html)  [add_content/standards/05rm/html/RM-3-9-2.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-9-2.html)

• 3.9.3  Abstract  Types  and  Subprograms  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-9-3.html)  [content/standards/05rm/html/RM-3-9-3.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-9-3.html)

• 3.9.4  Interface  Types  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-9-4.html)  [05rm/html/RM-3-9-4.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-9-4.html)

• 3.10  Access  Types  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-10.html)  [05rm/html/RM-3-10.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-10.html)

#### 22.4.4 Ada  Quality  and  Style  Guide

• Chapter 9:Object-Oriented  Features  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/docs/95style/html/sec_9/)  [content/docs/95style/html/sec_9/}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_9/)

es:Programación  en  Ada/Tipos  etiquetados[14](#part0220.xhtml__bookmark540)

![](Images/image07149.jpeg)

14 [http://es.wikibooks.org/wiki/Programaci%F3n%20en%20Ada%2FTipos%20etiquetados](http://es.wikibooks.org/wiki/Programaci%F3n%20en%20Ada%2FTipos%20etiquetados)

# 23 New  in  Ada  2005

This is an overview of the major features that are available in Ada 2005, the version of  the Ada standard that was accepted by ISO in January 2007 (to differentiate it from its  predecessors Ada 83[1](#part0221.xhtml__bookmark544) and Ada 95[2](#part0221.xhtml__bookmark545), the informal name Ada 2005 is generally agreed on). For  the  rationale  and  a  more  detailed  (and  very  technical)  description,  see  the  Amendment[3](#part0221.xhtml__bookmark546)  to the Ada Reference Manual following the links to the last version of every Ada Issue  document  (AI).

Although  the  standard  is  now  published,  not  all  compilers  will  be  able  to  handle  it.  Many  of  these  additions  are  already  implemented  by  the  following  Free  Software[4](#part0221.xhtml__bookmark547)  compilers:

• GNAT  GPL  Edition[5](#part0221.xhtml__bookmark548)

• GCC  4.1[6](#part0221.xhtml__bookmark549)

• GNAT  Pro  6.0.2[7](#part0221.xhtml__bookmark550)  (the  AdaCore  supported  version)  is  a  complete  implementation.

After  downloading  and  installing  any  of  them,  remember  to  use  the  -gnat05  switch  when  compiling  Ada  2005  code.  Note  that  Ada  2005  is  the  default  mode  in  GNAT  GPL  2007  Edition.

## 23.1 Language  features

Language  features

#### 23.1.1 Character  set

Not only does Ada 2005 now support a new 32-bit character type — called Wide_Wide_-  Character — but the source code itself may be of this extended character set as well. Thus  Russians  and  Indians,  for  example,  will  be  able  to  use  their  native  language  in  identifiers  and comments.  And mathematicians will rejoice:  The whole Greek and fractur character  sets are available for identifiers. For example, Ada.Numerics[8](#part0221.xhtml__bookmark551) will be extended with a new  constant:

![](Images/image07150.jpeg)

1 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAda%2083](http://en.wikibooks.org/wiki/Ada%20Programming%2FAda%2083)

2 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAda%2095](http://en.wikibooks.org/wiki/Ada%20Programming%2FAda%2095)

3 [http://www.ada-auth.org/AI-XREF.HTML#Amend_Doc](http://www.ada-auth.org/AI-XREF.HTML#Amend_Doc)

4 [http://en.wikipedia.org/wiki/Free%20Software](http://en.wikipedia.org/wiki/Free%20Software)

5 [http://libre.adacore.com/](http://libre.adacore.com/)

6 [http://gcc.gnu.org/](http://gcc.gnu.org/)

7 [http://www.adacore.com/home/gnatpro/](http://www.adacore.com/home/gnatpro/)

8 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics)

![](Images/image07151.jpeg)

This  is  not  a  new  idea  —  GNAT[9](#part0222.xhtml__bookmark552)  always  had  the  -gnatic  compiler  option  to  specify  the  character  set [http://gcc.gnu.org/onlinedocs/gnat_ugn_unw/Character-Set-Control.](http://gcc.gnu.org/onlinedocs/gnat_ugn_unw/Character-Set-Control.html)  [html](http://gcc.gnu.org/onlinedocs/gnat_ugn_unw/Character-Set-Control.html).  But  now  this  idea  has  become  standard,  so  all  Ada  compilers  will  need  to  support  Unicode  4.0[10](#part0222.xhtml__bookmark553)  for  identifiers  —  as  the  new  standard  requires.

See  also:

• AI95-00285-01  Support  for  16-bit  and  32-bit  characters  ˆ{[http://www.ada-auth.org/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00285.TXT)  [cgi-bin/cvsweb.cgi/AIs/AI-00285.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00285.TXT)

• AI95-00388-01  Add  Greek  pi  to  Ada.Numerics  ˆ{[http://www.ada-auth.org/cgi-bin/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00388.TXT)  [cvsweb.cgi/AIs/AI-00388.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00388.TXT)

#### 23.1.2 Interfaces

Interfaces  allow  for  a  limited  form  of  multiple  inheritance  similar  to  Java  and  C#.  You  find  a  full  description  here:  Ada  Programming/OO[11](#part0222.xhtml__bookmark554).

See  also:

• AI95-00251-01  Abstract  Interfaces  to  provide  multiple  inheritance  ˆ{[http://www.](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00251.TXT)  [ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00251.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00251.TXT)

• AI95-00345-01  Protected  and  task  interfaces  ˆ{[http://www.ada-auth.org/cgi-bin/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00345.TXT)  [cvsweb.cgi/AIs/AI-00345.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00345.TXT)

#### 23.1.3 Union

In  addition  to  Ada's  safe  variant  record  an  unchecked  C  style  union  is  now  available.  You  can  find  a  full  description  here:  Ada  Programming/Types/record#Union[12](#part0222.xhtml__bookmark555).

See  also:

• AI95-00216-01  Unchecked  unions  --  variant  records  with  no  run-time  discriminant  ˆ{[http:](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00216.TXT)

[//www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00216.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00216.TXT)

• Annex  B.3.3  Pragma  Unchecked_Union  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-B-3-3.html)  [content/standards/05rm/html/RM-B-3-3.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-B-3-3.html)

![](Images/image07152.jpeg)

9 [http://en.wikipedia.org/wiki/GNAT](http://en.wikipedia.org/wiki/GNAT)

10 [http://en.wikipedia.org/wiki/Unicode](http://en.wikipedia.org/wiki/Unicode)

11 Chapter  [22.4.2](#part0219.xhtml__bookmark533)  on  page  [217](#part0219.xhtml__bookmark533)

12 Chapter  [12.6](#part0097.xhtml__bookmark326)  on  page  [95](#part0097.xhtml__bookmark326)

#### 23.1.4 With

The with statement got a massive upgrade.  First there is the new limited with[13](#part0223.xhtml__bookmark556)  which  allows two packages to with each other. Then there is private with[14](#part0223.xhtml__bookmark557) to make a package only  visible  inside  the  private  part  of  the  specification.

See  also:

• AI95-00217-01  Limited  With  Clauses  ˆ{[http://www.ada-auth.org/cgi-bin/cvsweb.](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00217.TXT)  [cgi/AIs/AI-00217.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00217.TXT)

• AI95-00262-01  Access  to  private  units  in  the  private  part  ˆ{[http://www.ada-auth.org/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00262.TXT)  [cgi-bin/cvsweb.cgi/AIs/AI-00262.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00262.TXT)

#### 23.1.5 Access  types

###### Not  null  access

An  access  type  definition  can  specify  that  the  access  type  can  never  be  null.  See  Ada  Programming/Types/access#Not  null  access[15](#part0223.xhtml__bookmark558).

See  also:  AI95-00231-01  Access-to-constant  parameters  and  null-excluding  access  subtypes  ˆ{[http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00231.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00231.TXT)

###### Anonymous  access

The possible uses of anonymous access types are extended.  They are allowed virtually in  every type or object definition, including access to subprogram parameters.  Anonymous  access types may point to constant objects as well. Also, they could be declared to be not  null.

With the addition of the following operations in package Standard , it is possible to test the  equality  of  anonymous  access  types.

![](Images/image07153.jpeg)

See  Ada  Programming/Types/access#Anonymous  access[16](#part0223.xhtml__bookmark559).  See  also:

• AI95-00230-01  Generalized  use  of  anonymous  access  types  ˆ{[http://www.ada-auth.org/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00230.TXT)  [cgi-bin/cvsweb.cgi/AIs/AI-00230.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00230.TXT)

• AI95-00385-01  Stand-alone  objects  of  anonymous  access  types  ˆ{[http://www.ada-auth.](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00385.TXT)  [org/cgi-bin/cvsweb.cgi/AIs/AI-00385.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00385.TXT)

![](Images/image07154.jpeg)

13 Chapter  [17.3.3](#part0140.xhtml__bookmark407)  on  page  [138](#part0140.xhtml__bookmark407)

14 Chapter  [17.3.2](#part0140.xhtml__bookmark406)  on  page  [138](#part0140.xhtml__bookmark406)

15 Chapter  [13.10.1](#part0112.xhtml__bookmark363)  on  page  [110](#part0112.xhtml__bookmark363)

16 Chapter  [13.4](#part0105.xhtml__bookmark354)  on  page  [103](#part0105.xhtml__bookmark354)

• AI95-00318-01  Limited  and  anonymous  access  return  types  ˆ{[http://www.ada-auth.](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00318.TXT)  [org/cgi-bin/cvsweb.cgi/AIs/AI-00318.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00318.TXT)

## 23.2 Language  library

Language  library

#### 23.2.1 Containers

A  major  addition  to  the  language  library  is  the  generic  packages  for  containers.  If  you  are  familiar with the C++ STL, you will likely feel very much at home using Ada . One thing,  though: Ada is a block structured language. Many ideas of how to use the STL employ  this  feature  of  the  language.  For  example,  local  subprograms  can  be  supplied  to  iteration  schemes.

The original Ada Issue text AI95-00302-01 Container library ˆ{[http://www.ada-auth.org/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00302.TXT)  [cgi-bin/cvsweb.cgi/AIs/AI-00302.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00302.TXT)  has  now  been  transformed  into  A.18  Contain-  ers  ˆ{[http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-18.](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-18.html)  [html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-18.html) .

If you know how to write Ada programs, and have a need for vectors, lists, sets, or maps  (tables), please have a look at the AI95-00302-01 AI Text ˆ{[http://www.ada-auth.org/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00302.TXT)  [cgi-bin/cvsweb.cgi/AIs/AI-00302.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00302.TXT)mentioned above.  There is an !example section  in  the  text  explaining  the  use  of  the  containers  in  some  detail.  Matthew  Heaney  provides  a  number  of  demonstration  programs  with  his  reference  implementation  of  AI-302  (Ada  )  which  you  can  find  at  tigris[17](#part0224.xhtml__bookmark561).

In  Ada  Programming/Containers[18](#part0224.xhtml__bookmark562)  you  will  find  a  demo  using  containers.

Historical  side  note:  The  C++ STL draws  upon  the  work  of  David  R. Musser  and  Alexander  A.  Stepanov.  For  some  of  their  studies  of  generic  programming,  they  had  been  using  Ada  83.  The  Stepanov  Papers  Collection[19](#part0224.xhtml__bookmark563)  has  a  few  publications  available.

#### 23.2.2 Scan  Filesystem  Directories  and  Environment  Variables

See  also:

• AI95-00248-01  Directory  Operations  ˆ{[http://www.ada-auth.org/cgi-bin/cvsweb.](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00248.TXT)  [cgi/AIs/AI-00248.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00248.TXT)

• AI95-00370-01  Environment  variables  ˆ{[http://www.ada-auth.org/cgi-bin/cvsweb.](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00370.TXT)  [cgi/AIs/AI-00370.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00370.TXT)

![](Images/image07155.jpeg)

17 [http://charles.tigris.org](http://charles.tigris.org/)

18 Chapter  [24](#part0233.xhtml__bookmark596)  on  page  [231](#part0233.xhtml__bookmark596)

19 [http://www.stepanovpapers.com/](http://www.stepanovpapers.com/)

#### 23.2.3 Numerics

Besides the new constant of package Ada.Numerics  (see Character Set[20](#part0225.xhtml__bookmark565) above), the most  important  addition  are  the  packages  to  operate  with  vectors  and  matrices.

See  also:

• AI95-00388-01 Add Greek pi (π) to Ada.Numerics ˆ{[http://www.ada-auth.org/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00388.TXT)  [cgi-bin/cvsweb.cgi/AIs/AI-00388.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00388.TXT)

• AI95-00296-01 Vector and matrix operations ˆ{[http://www.ada-auth.org/cgi-bin/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00296.TXT)  [cvsweb.cgi/AIs/AI-00296.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00296.TXT)

(Related note on Ada programming tools: AI-388 contains an interesting assessment of how  compiler writers are bound to perpetuate the lack of handling of international characters in  programming support tools for now.  As an author of Ada programs, be aware that your  tools provider or Ada consultant could recommend that the program text be 7bit ASCII  only.)

## 23.3 Real-Time  and  High  Integrity  Systems

Real-Time  and  High  Integrity  Systems

See  also:

• AI95-00297-01 Timing events ˆ{[http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00297.TXT)  [AI-00297.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00297.TXT)

• AI95-00307-01  Execution-Time  Clocks  ˆ{[http://www.ada-auth.org/cgi-bin/cvsweb.](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00307.TXT)  [cgi/AIs/AI-00307.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00307.TXT)

• AI95-00354-01  Group  execution-time  budgets  ˆ{[http://www.ada-auth.org/cgi-bin/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00354.TXT)  [cvsweb.cgi/AIs/AI-00354.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00354.TXT)

• AI95-00266-01  Task  termination  procedure  ˆ{[http://www.ada-auth.org/cgi-bin/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00266.TXT)  [cvsweb.cgi/AIs/AI-00266.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00266.TXT)

• AI95-00386-01 Further functions returning Time_Span values ˆ{[http://www.ada-auth.](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00386.TXT)  [org/cgi-bin/cvsweb.cgi/AIs/AI-00386.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00386.TXT)

#### 23.3.1 Ravenscar  profile

See  also:

• AI95-00249-01  Ravenscar  profile  for  high-integrity  systems  ˆ{[http://www.ada-auth.](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00249.TXT)  [org/cgi-bin/cvsweb.cgi/AIs/AI-00249.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00249.TXT)

• AI95-00305-01  New  pragma  and  additional  restriction  identifiers  for  real-time  systems  ˆ{[http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00305.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00305.TXT)

• AI95-00347-01  Title  of  Annex  H  ˆ{[http://www.ada-auth.org/cgi-bin/cvsweb.cgi/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00347.TXT)  [AIs/AI-00347.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00347.TXT)

![](Images/image07156.jpeg)

20 Chapter  [23.1.1](#part0221.xhtml__bookmark543)  on  page  [219](#part0221.xhtml__bookmark543)

• AI95-00265-01  Partition  Elaboration  Policy  for  High-Integrity  Systems  ˆ{[http://www.](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00265.TXT)  [ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00265.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00265.TXT)

#### 23.3.2 New  scheduling  policies

See  also:

• AI95-00355-01  Priority  Specific  Dispatching  including  Round  Robin  ˆ{[http://www.](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00355.TXT)  [ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00355.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00355.TXT)

• AI95-00357-01  Support  for  Deadlines  and  Earliest  Deadline  First  Scheduling  ˆ{[http:](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00357.TXT)

[//www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00357.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00357.TXT)

• AI95-00298-01  Non-Preemptive  Dispatching  ˆ{[http://www.ada-auth.org/cgi-bin/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00298.TXT)  [cvsweb.cgi/AIs/AI-00298.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00298.TXT)

#### 23.3.3 Dynamic  priorities  for  protected  objects

See also:  AI95-00327-01  Dynamic ceiling priorities  ˆ{[http://www.ada-auth.org/cgi-bin/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00327.TXT)  [cvsweb.cgi/AIs/AI-00327.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00327.TXT)

## 23.4 Summary  of  what's  new

Summary  of  what's  new

#### 23.4.1 New  keywords

Added  3  keywords  (72  total)

###### • interface

• overriding

• synchronized

#### 23.4.2 New  pragmas

Added  11  pragmas:

###### • pragma

• pragma

###### • pragma

• pragma

###### • pragma

• pragma

###### • pragma

• pragma

###### • pragma

• pragma

• pragma

#### 23.4.3 New  attributes

Added  7  attributes:

• Machine_Rounding

• Mod

• Priority

• Stream_Size

• Wide_Wide_Image

• Wide_Wide_Value

• Wide_Wide_Width

#### 23.4.4 New  packages

• Assertions:

• Ada.Assertions

• Container library:

• Ada.Containers

• Ada.Containers.Vectors

• Ada.Containers.Doubly_Linked_Lists

• Ada.Containers.Generic_Array_Sort  (generic  procedure)

• Ada.Containers.Generic_Constrained_Array_Sort  (generic  procedure)

• Ada.Containers.Hashed_Maps

• Ada.Containers.Ordered_Maps

• Ada.Containers.Hashed_Sets

• Ada.Containers.Ordered_Sets

• Ada.Containers.Indefinite_Vectors

• Ada.Containers.Indefinite_Doubly_Linked_Lists

• Ada.Containers.Indefinite_Hashed_Maps

• Ada.Containers.Indefinite_Ordered_Maps

• Ada.Containers.Indefinite_Hashed_Sets

• Ada.Containers.Indefinite_Ordered_Sets

• Vector  and  matrix  manipulation:

• Ada.Numerics.Real_Arrays

• Ada.Numerics.Complex_Arrays

• Ada.Numerics.Generic_Real_Arrays

• Ada.Numerics.Generic_Complex_Arrays

• General  OS  facilities:

• Ada.Directories

• Ada.Directories.Information

• Ada.Environment_Variables

• String  hashing:

• Ada.Strings.Hash (generic  function)

• Ada.Strings.Fixed.Hash  (generic  function)

• Ada.Strings.Bounded.Hash (generic  function)

• Ada.Strings.Unbounded.Hash (generic  function)

• Ada.Strings.Wide_Hash  (generic  function)

• Ada.Strings.Wide_Fixed.Wide_Hash  (generic  function)

• Ada.Strings.Wide_Bounded.Wide_Hash (generic function)

• Ada.Strings.Wide_Unbounded.Wide_Hash (generic function)

• Ada.Strings.Wide_Wide_Hash  (generic  function)

• Ada.Strings.Wide_Wide_Fixed.Wide_Wide_Hash  (generic  function)

• Ada.Strings.Wide_Wide_Bounded.Wide_Wide_Hash  (generic  function)

• Ada.Strings.Wide_Wide_Unbounded.Wide_Wide_Hash (generic function)

• Time  operations:

• Ada.Calendar.Time_Zones

• Ada.Calendar.Arithmetic

• Ada.Calendar.Formatting

• Tagged  types:

• Ada.Tags.Generic_Dispatching_Constructor  (generic  function)

• Text  packages:

• Ada.Complex_Text_IO

• Ada.Text_IO.Bounded_IO

• Ada.Text_IO.Unbounded_IO

• Ada.Wide_Text_IO.Bounded_IO

• Ada.Wide_Text_IO.Unbounded_IO

• Ada.Wide_Characters

• Ada.Wide_Wide_Characters

• Wide_Wide_Character  packages:

• Ada.Strings.Wide_Wide_Bounded

• Ada.Strings.Wide_Wide_Fixed

• Ada.Strings.Wide_Wide_Maps

• Ada.Strings.Wide_Wide_Maps.Wide_Wide_Constants

• Ada.Strings.Wide_Wide_Unbounded

• Ada.Wide_Wide_Text_IO

• Ada.Wide_Wide_Text_IO.Complex_IO

• Ada.Wide_Wide_Text_IO.Editing

• Ada.Wide_Wide_Text_IO.Text_Streams

• Ada.Wide_Wide_Text_IO.Unbounded_IO

• Execution-time  clocks:

• Ada.Execution_Time

• Ada.Execution_Time.Timers

• Ada.Execution_Time.Group_Budgets

• Dispatching:

• Ada.Dispatching

• Ada.Dispatching.EDF

• Ada.Dispatching.Round_Robin

• Timing  events:

• Ada.Real_Time.Timing_Events

• Task  termination  procedures:

• Ada.Task_Termination

## 23.5 See  also

See  also

#### 23.5.1 Wikibook

• Ada  Programming/Ada  83[21](#part0229.xhtml__bookmark569)

• Ada  Programming/Ada  95[22](#part0229.xhtml__bookmark570)

• Ada  Programming/Ada  2012[23](#part0229.xhtml__bookmark571)

• Ada Programming/Object  Orientation[24](#part0229.xhtml__bookmark572)

• Ada  Programming/Types/access[25](#part0229.xhtml__bookmark573)

• Ada  Programming/Keywords[26](#part0229.xhtml__bookmark574)

• Ada  Programming/Keywords/and[27](#part0229.xhtml__bookmark575)

• Ada  Programming/Keywords/interface[28](#part0229.xhtml__bookmark576)

• Ada  Programming/Attributes[29](#part0229.xhtml__bookmark577)

• Ada  Programming/Pragmas[30](#part0229.xhtml__bookmark578)

• Ada  Programming/Pragmas/Restrictions[31](#part0229.xhtml__bookmark579)

• Ada  Programming/Libraries/Ada.Containers[32](#part0229.xhtml__bookmark580)

• Ada  Programming/Libraries/Ada.Directories[33](#part0229.xhtml__bookmark581)

#### 23.5.2 Pages  in  the  category  Ada  2005

• Category:Ada  Programming/Ada  2005  feature[34](#part0229.xhtml__bookmark582)

## 23.6 External  links

![](Images/image07157.jpeg)

21 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAda%2083](http://en.wikibooks.org/wiki/Ada%20Programming%2FAda%2083)

22 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAda%2095](http://en.wikibooks.org/wiki/Ada%20Programming%2FAda%2095)

23 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAda%202012](http://en.wikibooks.org/wiki/Ada%20Programming%2FAda%202012)

24 Chapter  [22](#part0189.xhtml__bookmark519)  on  page  [187](#part0189.xhtml__bookmark519)

25 Chapter  [13](#part0101.xhtml__bookmark346)  on  page  [99](#part0101.xhtml__bookmark346)

26 Chapter  [35](#part0295.xhtml__bookmark761)  on  page  [293](#part0295.xhtml__bookmark761)

27 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fand](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fand)

28 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Finterface](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Finterface)

29 Chapter  [38](#part0307.xhtml__bookmark878)  on  page  [305](#part0307.xhtml__bookmark878)

30 Chapter  [39](#part0319.xhtml__bookmark1089)  on  page  [317](#part0319.xhtml__bookmark1089)

31 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FRestrictions](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FRestrictions)

32 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers)

33 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Directories](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Directories)

34 [http://en.wikibooks.org/wiki/%3ACategory%3AAda%20Programming%2FAda%202005%20feature](http://en.wikibooks.org/wiki/%3ACategory%3AAda%20Programming%2FAda%202005%20feature)

External  links

#### 23.6.1 Papers  and  presentations

• Ada  2005:  Putting  it  all together[35](#part0230.xhtml__bookmark583)  (SIGAda  2004  presentation)

• GNAT  and  Ada  2005[36](#part0230.xhtml__bookmark584)  (SIGAda  2004  paper)

• An  invitation  to  Ada  2005[37](#part0230.xhtml__bookmark585),  and  the  presentation  of  this  paper[38](#part0230.xhtml__bookmark586)  at  Ada-Europe  2004

#### 23.6.2 Rationale

• Rationale  for  Ada  2005[39](#part0230.xhtml__bookmark587) by  John  Barnes[40](#part0230.xhtml__bookmark588):

1. Introduction

2. Object  Oriented  Model

3. Access  Types

4. Structure  and  Visibility

5. Tasking  and  Real-Time

6. Exceptions,  Generics,  Etc.

7. Predefined  Library

8. Containers

9. Epilogue  References  Index

Available  as  a  single  document  for  printing[41](#part0230.xhtml__bookmark589).

#### 23.6.3 Language  Requirements

• Instructions to the Ada Rapporteur Group from SC22/WG9 for Preparation of the  Amendment to ISO/IEC 8652[42](#part0230.xhtml__bookmark590) (10 October 2002), and a  presentation of this document[43](#part0230.xhtml__bookmark591)  at  SIGAda  2002

#### 23.6.4 Ada  Reference  Manual

• Ada  Reference  Manual,  ISO/IEC  8652:1995(E)  with  COR.1:2001  and  AMD.1:2007[44](#part0230.xhtml__bookmark592)

![](Images/image07158.jpeg)

35 [http://www.sigada.org/conf/sigada2004/SIGAda2004-CDROM/SIGAda2004-Proceedings/](http://www.sigada.org/conf/sigada2004/SIGAda2004-CDROM/SIGAda2004-Proceedings/Ada2005Panel.pdf)  [Ada2005Panel.pdf](http://www.sigada.org/conf/sigada2004/SIGAda2004-CDROM/SIGAda2004-Proceedings/Ada2005Panel.pdf)

36 [http://www.adacore.com/wp-content/files/attachments/Ada_2005_and_GNAT.pdf](http://www.adacore.com/wp-content/files/attachments/Ada_2005_and_GNAT.pdf)

37 [http://sigada.org/ada_letters/sept2003/Invitation_to_Ada_2005.pdf](http://sigada.org/ada_letters/sept2003/Invitation_to_Ada_2005.pdf)

38 [http://www.cs.kuleuven.ac.be/~dirk/ada-belgium/events/04/040616-aec-ada2005.pdf](http://www.cs.kuleuven.ac.be/~dirk/ada-belgium/events/04/040616-aec-ada2005.pdf)

39 [http://www.adaic.com/standards/05rat/html/Rat-TTL.html](http://www.adaic.com/standards/05rat/html/Rat-TTL.html)

40 [http://en.wikipedia.org/wiki/John%20Barnes%20%28computer%20scientist%29](http://en.wikipedia.org/wiki/John%20Barnes%20%28computer%20scientist%29)

41 [http://www.adaic.com/standards/05rat/Rationale05.pdf](http://www.adaic.com/standards/05rat/Rationale05.pdf)

42 [http://www.open-std.org/jtc1/sc22/WG9/n412.pdf](http://www.open-std.org/jtc1/sc22/WG9/n412.pdf)

43 [http://std.dkuug.dk/JTC1/sc22/wg9/n423.pdf](http://std.dkuug.dk/JTC1/sc22/wg9/n423.pdf)

44 [http://www.adaic.com/standards/05rm/html/RM-TTL.html](http://www.adaic.com/standards/05rm/html/RM-TTL.html)

• Annotated  Ada  Reference  Manual,  ISO/IEC 8652:1995(E) with COR.1:2001 and  AMD.1:2007[45](#part0231.xhtml__bookmark593)  (colored  diffs)

• List  of Ada Amendment drafts[46](#part0231.xhtml__bookmark594)

#### 23.6.5 Ada  Issues

• Amendment  200Y[47](#part0231.xhtml__bookmark595)

• AI95-00387-01  Introduction  to  Amendment  ˆ{[http://www.ada-auth.org/cgi-bin/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00387.TXT)  [cvsweb.cgi/AIs/AI-00387.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00387.TXT)

• AI95-00284-01  New  reserved  words  ˆ{[http://www.ada-auth.org/cgi-bin/cvsweb.](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00284.TXT)  [cgi/AIs/AI-00284.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00284.TXT)

• AI95-00252-01  Object.Operation  notation  ˆ{[http://www.ada-auth.org/cgi-bin/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00252.TXT)  [cvsweb.cgi/AIs/AI-00252.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00252.TXT)

• AI95-00218-01  Accidental  overloading  when  overriding  ˆ{[http://www.ada-auth.org/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00218.TXT)  [cgi-bin/cvsweb.cgi/AIs/AI-00218.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00218.TXT)

• AI95-00348-01  Null  procedures  ˆ{[http://www.ada-auth.org/cgi-bin/cvsweb.cgi/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00348.TXT)  [AIs/AI-00348.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00348.TXT)

• AI95-00287-01  Limited  aggregates  allowed  ˆ{[http://www.ada-auth.org/cgi-bin/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00287.TXT)  [cvsweb.cgi/AIs/AI-00287.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00287.TXT)

• AI95-00326-01  Incomplete  types  ˆ{[http://www.ada-auth.org/cgi-bin/cvsweb.](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00326.TXT)  [cgi/AIs/AI-00326.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00326.TXT)

• AI95-00317-01  Partial  parameter  lists  for  formal  packages  ˆ{[http://www.ada-auth.](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00317.TXT)  [org/cgi-bin/cvsweb.cgi/AIs/AI-00317.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00317.TXT)

• AI95-00376-01  Interfaces.C  works  for  C++  as  well  ˆ{[http://www.ada-auth.org/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00376.TXT)  [cgi-bin/cvsweb.cgi/AIs/AI-00376.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00376.TXT)

• AI95-00368-01  Restrictions  for  obsolescent  features  ˆ{[http://www.ada-auth.org/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00368.TXT)  [cgi-bin/cvsweb.cgi/AIs/AI-00368.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00368.TXT)

• AI95-00381-01  New  Restrictions  identifier  No_Dependence  ˆ{[http://www.ada-auth.](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00381.TXT)  [org/cgi-bin/cvsweb.cgi/AIs/AI-00381.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00381.TXT)

• AI95-00224-01  pragma  Unsuppress  ˆ{[http://www.ada-auth.org/cgi-bin/cvsweb.](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00224.TXT)  [cgi/AIs/AI-00224.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00224.TXT)

• AI95-00161-01  Default-initialized  objects  ˆ{[http://www.ada-auth.org/cgi-bin/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00161.TXT)  [cvsweb.cgi/AIs/AI-00161.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00161.TXT)

• AI95-00361-01 Raise with message ˆ{[http://www.ada-auth.org/cgi-bin/cvsweb.](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00361.TXT)  [cgi/AIs/AI-00361.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00361.TXT)

• AI95-00286-01  Assert  pragma  ˆ{[http://www.ada-auth.org/cgi-bin/cvsweb.cgi/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00286.TXT)  [AIs/AI-00286.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00286.TXT)

• AI95-00328-01  Preinstantiations  of  Complex_IO  ˆ{[http://www.ada-auth.org/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00328.TXT)  [cgi-bin/cvsweb.cgi/AIs/AI-00328.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00328.TXT)

• AI95-00301-01  Operations  on  language-defined  string  types  ˆ{[http://www.ada-auth.](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00301.TXT)  [org/cgi-bin/cvsweb.cgi/AIs/AI-00301.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00301.TXT)

• AI95-00340-01  Mod  attribute  ˆ{[http://www.ada-auth.org/cgi-bin/cvsweb.cgi/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00340.TXT)  [AIs/AI-00340.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00340.TXT)

![](Images/image07159.jpeg)

45 [http://www.adaic.com/standards/05aarm/html/AA-TTL.html](http://www.adaic.com/standards/05aarm/html/AA-TTL.html)

46 [http://www.ada-auth.org/amendment.html](http://www.ada-auth.org/amendment.html)

47 [http://www.ada-auth.org/AI-XREF.HTML#Amend_Doc](http://www.ada-auth.org/AI-XREF.HTML#Amend_Doc)

• AI95-00364-01  Fixed-point  multiply/divide  ˆ{[http://www.ada-auth.org/cgi-bin/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00364.TXT)  [cvsweb.cgi/AIs/AI-00364.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00364.TXT)

• AI95-00267-01  Fast  float-to-integer  conversions  ˆ{[http://www.ada-auth.org/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00267.TXT)  [cgi-bin/cvsweb.cgi/AIs/AI-00267.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00267.TXT)

• AI95-00321-01  Definition  of  dispatching  policies  ˆ{[http://www.ada-auth.org/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00321.TXT)  [cgi-bin/cvsweb.cgi/AIs/AI-00321.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00321.TXT)

• AI95-00329-01  pragma  No_Return  --  procedures  that  never  return  ˆ{[http://www.](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00329.TXT)  [ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00329.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00329.TXT)

• AI95-00362-01  Some  predefined  packages  should  be  recategorized  ˆ{[http://www.](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00362.TXT)  [ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00362.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00362.TXT)

• AI95-00351-01  Time  operations  ˆ{[http://www.ada-auth.org/cgi-bin/cvsweb.](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00351.TXT)  [cgi/AIs/AI-00351.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00351.TXT)

• AI95-00427-01  Default  parameters  and  Calendar  operations  ˆ{[http://www.ada-auth.](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00427.TXT)  [org/cgi-bin/cvsweb.cgi/AIs/AI-00427.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00427.TXT)

• AI95-00270-01  Stream  item  size  control  ˆ{[http://www.ada-auth.org/cgi-bin/](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00270.TXT)  [cvsweb.cgi/AIs/AI-00270.TXT}](http://www.ada-auth.org/cgi-bin/cvsweb.cgi/AIs/AI-00270.TXT)

# 24 Containers

What follows is a simple demo of some of the container types. It does not cover everything,  but  should  get  you  started.

This  language  feature  is  only  available  in  Ada  2005

###### First  Example:  Maps

The program below prints greetings to the world in a number of human languages.  The  greetings are stored in a table, or hashed map. The map associates every greeting (a value)  with a language code (a key). That is, you can use language codes as keys to find greeting  values  in  the  table.

The elements in the map are constant strings of international characters, or really, pointers  to  such  constant  strings.  A  package  Regional  is  used  to  set  up  both  the  language  IDs  and  an  instance  of  Ada  .

![](Images/image07160.jpeg)

![](Images/image07161.jpeg)

Here  is  the  program,  details  will  be  explained  later.

![](Images/image07162.jpeg)

![](Images/image07163.jpeg)

The  first  of  the  Insert  statements  is  written  in  an  Ada  95  style:

![](Images/image07164.jpeg)

The next insertions use so called distinguished receiver notation which you can use in  Ada 2005.  (It's O-O parlance.  While the Insert call involves all of:  a Container object  (greetings),  a  Key  object  (EN),  and  a  New_Item  object  (new  Wide_String'("Hello,  World!")),  the  Container  object  is  distinguished  from  the  others  in  that  the  Insert  call  provides  it  (and  only  it)  with  the  other  objects.  In  this  case  the  Container  object  will  be  modified  by  the  call,  using  arguments  named  Key  and  New_Item  for  the  modification.)

![](Images/image07165.jpeg)

After the table is set up, the program goes on to print all the greetings contained in the  table. It does so employing a cursor that runs along the elements in the table in some order.  The typical scheme is to obtain a cursor, here using First, and then to iterate the following  calls:

1. Has_Element,  for  checking  whether  the  cursor  is  at  an  element

2. Element,  to  get  the  element  and

3. Next,  to  move  the  cursor  to  another  element

When there is no more element left, the cursor will have the special value No_Element.  Actually,  this  is  an  iteration  scheme  that  can  be  used  with  all  containers  in  child  packages  of  Ada  .

###### A  slight  variation:  picking  an  element

The next program shows how to pick a value from the map, given a key. Actually, you will  provide  the  key.  The  program  is  like  the  previous  one,  except  that  it  doesn't  just  print  all  the elements in the map, but picks one based on a Language_ID value that it reads from  standard  input.

![](Images/image07166.jpeg)

![](Images/image07167.jpeg)

This  time  the  Element  function  consumes  a  Key  (lang)  not  a  Cursor.  Actually,  it  consumes  two  values,  the  other  value  being  greetings,  in  distinguished  receiver  notation.

###### Second  Example:  Vectors  and  Maps

Let's take bean counting literally.  Red beans, green beans, and white beans.  (Yes, white  beans  really  do  exist.)  Your  job  will  be  to  collect  a  number  of  beans,  weigh  them,  and  then  determine  the  average  weight  of  red,  green,  and  white  beans,  respectively.  Here  is  one  approach.

Again, we need a package, this time for storing vegetable related information. Introducing  the Beans package (the Grams type doesn't belong in a vegetable package, but it's there to  keep  things  simple):

![](Images/image07168.jpeg)

![](Images/image07169.jpeg)

The  Vectors  instance  offers  a  data  structure  similar  to  an  array  that  can  change  its  size  at  run  time.  It is called Vector.  Each bean that is read will be appended to a Bean_Vecs.Vector  object.

The following program first calls read_input to fill a buffer with beans.  Next, it calls a  function  that  computes  the  average  weight  of  beans  having  the  same  color.  This  function:

![](Images/image07170.jpeg)

Then  the  average  value  is  printed  for  beans  of  each  color  and  the  program  stops.

![](Images/image07171.jpeg)

![](Images/image07172.jpeg)

All  container  operations  take  place  in  function  average_weight.  To  find  the  mean  weight  of beans of the same color, the function is looking at all beans in order. If a bean has the  right  color,  average_weight  adds  its  weight  to  the  total  weight,  and  increases  the  number  of  beans  counted  by  1.

The computation visits all beans. The iteration that is necessary for going from one bean to  the next and then performing the above steps is best left to the Iterate procedure which is  part of all container packages. To do so, wrap the above steps inside some procedure and  pass this procedure to Iterate. The effect is that Iterate calls your procedure for each  element  in  the  vector,  passing  a  cursor  value  to  your  procedure,  one  for  each  element.

Having the container machinery do the iteration can also be faster than moving and  checking the cursor yourself, as was  done in  the Hello_World_Extended example.

![](Images/image07173.jpeg)

![](Images/image07174.jpeg)

![](Images/image07175.jpeg)

This approach is straightforward. However, imagine larger vectors. average_weight will  visit all elements repeatedly for each color. If there are M colors and N beans, average_-  weight  will  be  called  M  *  N  times,  and  with  each  new  color,  N  more  calls  are  necessary.  A  possible alternative is to collect all information about a bean once it is visited. However,  this will likely need more variables, and you will have to find a way to return more than one  result  (one  average  for  each  color),  etc.  Try  it!

A  different  approach  might  be  better.  One  is  to  copy  beans  of  different  colors  to  separate  vec-  tor objects. (Remembering Cinderella.) Then average_weight must visit each element only  one  time.  The  following  procedure  does  this,  using  a  new  type  from  Beans,  called  Bean_Pots.

![](Images/image07176.jpeg)

Note  how  this  plain  array  associates  colors  with  Vectors.  The  procedure  for  getting  the  beans  into  the  right  bowls  uses  the  bean  color  as  array  index  for  finding  the  right  bowl  (vector).

![](Images/image07177.jpeg)

![](Images/image07178.jpeg)

![](Images/image07179.jpeg)

Everything is  in place now.

![](Images/image07180.jpeg)

![](Images/image07181.jpeg)

As  a  side  effect  of  having  chosen  one  vector  per  color,  we  can  determine  the  number  of  beans  in each vector by calling the Length function.  But average_weight,  too,  computes the  number  of  elements  in  the  vector.  Hence,  a  summing  function  might  replace  average_weight  here.

###### All  In  Just  One  Map!

The following program first calls read_input to fill a buffer with beans. Then, information  about  these  beans  is  stored  in  a  table,  mapping  bean  properties  to  numbers  of  occurrence.

The processing that starts at Iterate uses chained procedure calls typical of the Ada  iteration  mechanism.

The  Beans  package  in  this  example  instantiates  another  generic  library  unit,  Ada  .  Where  the Ada  require a hashing function, Ada  require a comparison function. We provide one,  "<",  which  sorts  beans  first  by  color,  then  by  weight.  It  will  automatically  be  associated  with the corresponding generic formal function,  as its name,  "<",  matches that of the  generic  formal  function,  "<".

![](Images/image07182.jpeg)

Where  the  previous  examples  have  withed  subprograms,  this  variation  on  bean_counting

packs  them  all  as  local  subprograms.

![](Images/image07183.jpeg)

![](Images/image07184.jpeg)

![](Images/image07185.jpeg)

end  add_bean_info;

begin --bean_counting

read_input(  buffer)  ;

--next,  for  all  beans  in  the  vector  ‘buffer‘  just  filled,  store

--information  about each bean in the ‘stats_cw‘ table.

declare

use  Bean_Vecs;

procedure  count_bean(  c:Cursor) is  begin

add_bean_info(  Element(  c)  )  ;

end  count_bean;

begin

Iterate( buffer, count_bean’  Access)  ;

end;

--now  everything  is  set  up  for  computing  some  statistical  data. The

--keys of the map, i.e. beans,  are  ordered  by  color  and  then  weight.

--The  ‘First‘,  and  ‘Ceiling‘  functions  will  find  cursors

--denoting  the ends of a group.

declare

use Bean_Statistics;

--statistics  is  computed  groupwise:

q_sum:Grams;  q_count:Natural;

procedure  q_stats(  lo, hi:Cursor) ;

--‘q_stats‘  will  update  the  ‘q_sum‘  and  ‘q_count‘  globals  with

--the  sum  of  the  key  weights  and  their  number,  respectively. ‘lo‘

--(included)  and  ‘hi‘  (excluded)  mark the  interval  of  keys

--to  use  from  the  map.

procedure  q_stats(  lo, hi:Cursor) is

k:Cursor  :=  lo;

begin

q_count :=  0; q_sum  :=  0. 0;

loop

exit  when  k  =  hi;

q_count  :=  q_count  + Element(  k) ;

q_sum  :=  q_sum  + Key(  k)  . weight  * Element(  k)  ;  Next(  k)  ;

end  loop;  end  q_stats;

--precondition

pragma  assert(  not  Is_Empty(  stats_cw)  , "container  is  empty")  ;

lower, upper:Cursor  :=  First(  stats_cw)  ;

--denoting  the  first  key  of  a  group,  and  the  first  key  of  a

--following  group,  respectively

begin

--start  reporting  and  trigger  the  computations

Wide_Text_IO.  Put_Line(  "Summary:")  ;

![](Images/image07186.jpeg)

Like in the greetings example, you can pick values from the table. This time the values tell  the number of occurrences of beans with certain properties. The stats_cw table is ordered  by  key,  that  is  by  bean  properties.  Given  particular  properties,  you  can  use  the  Floor  and Ceiling functions to approximate the bean in the table that most closely matches the  desired  properties.

It is now easy to print a histogram showing the frequency with which each kind of bean has  occurred.  If  N  is  the  number  of  beans  of  a  kind,  then  print  N  characters  on  a  line,  or  draw  a  graphical  bar  of  length  N,  etc.  A  histogram  showing  the  number  of  beans  per  color  can  be drawn after computing the sum of beans of this color, using groups like in the previous  example.  You  can  delete  beans  of  a  color  from  the  table  using  the  same  technique.

Finally, think of marshalling the beans in order starting at the least frequently occurring  kind.  That  is,  construct  a  vector  appending  first  beans  that  have  occurred  just  once,  followed  by beans that have occurred twice, if any, and so on. Starting from the table is possible, but  be  sure  to  have  a  look  at  the  sorting  functions  of  Ada  .

## 24.1 See  also

See  also

#### 24.1.1 Wikibook

• Ada  Programming[1](#part0242.xhtml__bookmark598)

• Ada  Programming/Libraries/Ada.Containers[2](#part0242.xhtml__bookmark599)

![](Images/image07187.jpeg)

1 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

2 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers)

#### 24.1.2 Ada  2005  Reference  Manual

• A.18.1  The  Package  Containers  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-18-1.html)  [standards/05rm/html/RM-A-18-1.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-18-1.html)

# 25 Interfacing

## 25.1 Interfacing

Interfacing

Ada is one of the few languages where interfacing is part of the language standard.  The  programmer  can  interface  with  other  programming  languages,  or  with  the  hardware.

## 25.2 Other  programming  languages

Other  programming  languages

The language standard defines the interfaces for C[1](#part0245.xhtml__bookmark604), Cobol[2](#part0245.xhtml__bookmark605) and Fortran[3](#part0245.xhtml__bookmark606). Of course any  implementation might define further interfaces — GNAT[4](#part0245.xhtml__bookmark607) for example defines an interface  to  C++[5](#part0245.xhtml__bookmark608).

Interfacing with other languages is actually provided by pragma Export[6](#part0245.xhtml__bookmark609), Import[7](#part0245.xhtml__bookmark610) and  Convention[8](#part0245.xhtml__bookmark611).

## 25.3 Hardware devices

Hardware  devices

Embedded  programmers  usually  have  to  write  device  drivers.  Ada  provides  extensive  support  for  interfacing  with  hardware,  like  using  representation  clauses[9](#part0245.xhtml__bookmark612)  to  specify  the  exact  representation of types used by the hardware, or standard interrupt handling for writing  Interrupt  service  routine[10](#part0245.xhtml__bookmark613)s.

![](Images/image07188.jpeg)

1 [http://en.wikibooks.org/wiki/C%20Programming](http://en.wikibooks.org/wiki/C%20Programming)

2 [http://en.wikibooks.org/wiki/COBOL](http://en.wikibooks.org/wiki/COBOL)

3 [http://en.wikibooks.org/wiki/Programming%3AFortran](http://en.wikibooks.org/wiki/Programming%3AFortran)

4 [http://en.wikibooks.org/wiki/Ada%20Programming%2FGNAT](http://en.wikibooks.org/wiki/Ada%20Programming%2FGNAT)

5 [http://en.wikibooks.org/wiki/C%2B%2B%20Programming](http://en.wikibooks.org/wiki/C%2B%2B%20Programming)

6 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExport](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExport)

7 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FImport](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FImport)

8 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FConvention](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FConvention)

9 [http://en.wikibooks.org/wiki/Ada%20Programming%2FRepresentation%20clauses](http://en.wikibooks.org/wiki/Ada%20Programming%2FRepresentation%20clauses)

10 [http://en.wikipedia.org/wiki/Interrupt%20service%20routine](http://en.wikipedia.org/wiki/Interrupt%20service%20routine)

## 25.4 See  also

See  also

#### 25.4.1 Wikibook

• Ada  Programming[11](#part0246.xhtml__bookmark615)

• Ada  Programming/Libraries/Interfaces[12](#part0246.xhtml__bookmark616)

#### 25.4.2 Ada  Reference  Manual

• Annex  B  Interface  to  Other  Languages  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-B.html)  [content/standards/05rm/html/RM-B.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-B.html)

• Annex  C  Systems  Programming  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-C.html)  [standards/05rm/html/RM-C.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-C.html)

#### 25.4.3 Ada  95  Rationale

• bInterface  to  Other  Languages3

#### 25.4.4 Ada  Quality  and  Style  Guide

• 7.6.4  Interfacing  to  Foreign  Languages  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/7-6-4.html)  [content/docs/95style/html/sec_7/7-6-4.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/7-6-4.html)

11 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

12 Chapter  [43](#part0351.xhtml__bookmark1593)  on  page  [349](#part0351.xhtml__bookmark1593)

# 26 Coding  Standards

## 26.1 Introduction

Introduction

Each  project  should  follow  a  specific  coding  standard[1](#part0247.xhtml__bookmark621)  to  ease  readability  and  maintenance  of the source code, and reduce the insertion of errors. Depending on the requirements of the  project, a  set  of guidelines  can help to achieve  the  desired level  of performance, portability,  code  complexity...

There are many ASIS[2](#part0247.xhtml__bookmark622) tools that can be used to check automatically the adherence of Ada  source  code  to  the  guidelines.

## 26.2 Tools

Tools

• AdaControl[3](#part0247.xhtml__bookmark623)  (  Rules[4](#part0247.xhtml__bookmark624))

• gnatcheck[5](#part0247.xhtml__bookmark625)  (  Rules[6](#part0247.xhtml__bookmark626))

• GNAT  Pretty-Printer[7](#part0247.xhtml__bookmark627)

• The  GNAT  Metric  Tool  gnatmetric[8](#part0247.xhtml__bookmark628)

• RainCode  Engine[9](#part0247.xhtml__bookmark629)

• RainCode  Checker[10](#part0247.xhtml__bookmark630)

• AdaSTAT[11](#part0247.xhtml__bookmark631)

## 26.3 Coding  guidelines

![](Images/image07189.jpeg)

1 [http://en.wikipedia.org/wiki/coding%20standard](http://en.wikipedia.org/wiki/coding%20standard)

2 [http://en.wikipedia.org/wiki/Ada%20Semantic%20Interface%20Specification](http://en.wikipedia.org/wiki/Ada%20Semantic%20Interface%20Specification)

3 [http://www.adalog.fr/adacontrol2.htm](http://www.adalog.fr/adacontrol2.htm)

4 [http://www.adalog.fr/compo/adacontrol_ug.html#Rules-reference](http://www.adalog.fr/compo/adacontrol_ug.html#Rules-reference)

5 [http://gcc.gnu.org/onlinedocs/gnat_ugn_unw/Verifying-Properties-Using-gnatcheck.html](http://gcc.gnu.org/onlinedocs/gnat_ugn_unw/Verifying-Properties-Using-gnatcheck.html)

6 [http://gcc.gnu.org/onlinedocs/gnat_ugn_unw/Predefined-Rules.html](http://gcc.gnu.org/onlinedocs/gnat_ugn_unw/Predefined-Rules.html)

7 [http://gcc.gnu.org/onlinedocs/gnat_ugn_unw/The-GNAT-Pretty_002dPrinter-gnatpp.html](http://gcc.gnu.org/onlinedocs/gnat_ugn_unw/The-GNAT-Pretty_002dPrinter-gnatpp.html)

8 [http://gcc.gnu.org/onlinedocs/gnat_ugn_unw/The-GNAT-Metric-Tool-gnatmetric.html](http://gcc.gnu.org/onlinedocs/gnat_ugn_unw/The-GNAT-Metric-Tool-gnatmetric.html)

9 [http://www.raincode.com/adaengine.html](http://www.raincode.com/adaengine.html)

10 [http://www.raincode.com/adachecker.html](http://www.raincode.com/adachecker.html)

11 [http://www.adastat.com/](http://www.adastat.com/)

Coding  guidelines

• Ada  Quality  &  Style  Guide[12](#part0248.xhtml__bookmark633):  Guidelines  for  Professional  Programmers

• ISO/IEC  TR  15942:2000,  Guide  for  the  use  of  the  Ada  programming  language  in  high  integrity  systems[13](#part0248.xhtml__bookmark634),  First  edition  (2000-03-01).  ISO  Freely  Available  Standards[14](#part0248.xhtml__bookmark635)

• Stephen  Leake,  NASA  Flight Software Branch — Ada  Coding Standard[15](#part0248.xhtml__bookmark636) (2004-01-30)

• ESA[16](#part0248.xhtml__bookmark637)  BSSC

![](Images/image07190.jpeg)

.  ,  ,

![](Images/image07191.jpeg)

.  ,  ,

• GNAT  Coding  Style:  A  Guide  for  GNAT  Developers

![](Images/image07192.jpeg)

17. .  Retrieved

![](Images/image07193.jpeg)<map name="awmap2"><area shape="rect" href="http://gcc.gnu.org/onlinedocs/gnat-style/" coords="115, 27, 459, 40"></map>

18. .  Retrieved  (  PDF[19](#part0248.xhtml__bookmark640))

## 26.4 See  also

See  also

#### 26.4.1 Other  wikibooks

• Ada  Style  Guide[20](#part0248.xhtml__bookmark641)

![](Images/image07194.jpeg)

12 [http://en.wikibooks.org/wiki/Ada%20Style%20Guide](http://en.wikibooks.org/wiki/Ada%20Style%20Guide)

13 [http://www.dit.upm.es/ork/documents/adahis.pdf](http://www.dit.upm.es/ork/documents/adahis.pdf)

14 [http://standards.iso.org/ittf/PubliclyAvailableStandards/](http://standards.iso.org/ittf/PubliclyAvailableStandards/)

15 [http://software.gsfc.nasa.gov/AssetsApproved/PA2.4.1.1.1.pdf](http://software.gsfc.nasa.gov/AssetsApproved/PA2.4.1.1.1.pdf)

16 [http://en.wikipedia.org/wiki/European%20Space%20Agency](http://en.wikipedia.org/wiki/European%20Space%20Agency)

17

18

19 [http://gcc.gnu.org/onlinedocs/gnat-style.pdf](http://gcc.gnu.org/onlinedocs/gnat-style.pdf)

20 [http://en.wikibooks.org/wiki/Ada%20Style%20Guide](http://en.wikibooks.org/wiki/Ada%20Style%20Guide)

![](Images/image07195.jpeg)

#### 26.4.2 Wikibook

• Ada  Programming[21](#part0249.xhtml__bookmark643)

#### 26.4.3 Ada  Quality  and  Style  Guide

• Chapter  1:Introduction  ˆ{[http://www.adaic.org/resources/add_content/docs/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_1/)  [95style/html/sec_1/}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_1/)

## 26.5 External  links

External  links

• Introduction  to  Coding  Standards[22](#part0249.xhtml__bookmark644)

![](Images/image07196.jpeg)

21 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

22 [http://geekswithblogs.net/sdorman/archive/2007/06/13/Introduction-to-Coding-Standards.](http://geekswithblogs.net/sdorman/archive/2007/06/13/Introduction-to-Coding-Standards.aspx)  [aspx](http://geekswithblogs.net/sdorman/archive/2007/06/13/Introduction-to-Coding-Standards.aspx)

# 27 Tips

## 27.1 Full  declaration  of  a  type  can  be  deferred  to  the  unit's  body

Full  declaration  of  a  type  can  be  deferred  to  the  unit's  body

Often, you'll want to make changes to the internals of a private type.  This, in turn, will  require the algorithms that act on it to be modified.  If the type is completed in the unit  specification,  it  is  a  pain  to  edit  and  recompile  both  files,  even  with  an  IDE[1](#part0251.xhtml__bookmark647),  but  it's  something  some  programmers  learn  to  live  with.

It turns out you don't have to. Nonchalantly mentioned in the  ARM[2](#part0251.xhtml__bookmark648), and generally skipped  over in tutorials, is the fact that private types can be completed in the unit's body itself,  making them much closer to the relevant code, and saving a recompile of the specification,  as well as every unit depending on it.  This may seem like a small thing, and, for small  projects,  it  is.  However,  if  you  have  one  of  those  uncooperative  types  that  requires  dozens  of  tweaks,  or  if  your  dependence  graph  has  much  depth,  the  time  and  annoyance  saved  add  up  quickly.

Also, this construction is very useful when coding a shared library, because it permits to  change  the  implementation  of  the  type  while  still  providing  a  compatible  ABI[3](#part0251.xhtml__bookmark649).

Code  sample:

![](Images/image07197.jpeg)

The  type  in  the  public  part  is  an  access[4](#part0251.xhtml__bookmark650)  to  the  hidden  type.  This  has  the  drawback  that  memory management has to be provided by the package implementation.  That is the reason  why  Private_Type  is  a  limited  type,  the  client  will  not  be  allowed  to  copy  the  access  values,  in  order  to  prevent  dangling  references.

![](Images/image07198.jpeg)

1 [http://en.wikipedia.org/wiki/Integrated%20development%20environment](http://en.wikipedia.org/wiki/Integrated%20development%20environment)

2 [http://www.adaic.org/standards/95lrm/html/RM-TTL.html](http://www.adaic.org/standards/95lrm/html/RM-TTL.html)

3 [http://en.wikipedia.org/wiki/Application_binary_interface](http://en.wikipedia.org/wiki/Application_binary_interface)

4 Chapter  [13](#part0101.xhtml__bookmark346)  on  page  [99](#part0101.xhtml__bookmark346)

These  types  are  sometimes  called  "Taft  types"  —named  after  Tucker  Taft,  the  main  designer  of Ada 95— because were introduced in the so-called Taft Amendment to Ada 83\. In other  programming  languages,  this  technique  is  called  "opaque  pointer[5](#part0252.xhtml__bookmark653)s".

## 27.2 Lambda  calculus  through  generics

Lambda  calculus  through  generics

Suppose you've decided to roll your own set[6](#part0252.xhtml__bookmark654) type. You can add things to it, remove things  from it, and you want to let a user apply some arbitrary function to all of its members. But  the  scoping  rules  seem  to  conspire  against  you,  forcing  nearly  everything  to  be  global.

The  mental  stumbling  block  is  that  most  examples  given  of  generics[7](#part0252.xhtml__bookmark655)  are  packages,  and  the  Set  package  is  already  generic.  In  this  case,  the  solution  is  to  make  the  Apply_To_All procedure generic as well;  that is,  to nest the generics.  Generic pro-  cedures  inside  packages  exist  in  a  strange  scoping  limbo,  where  anything  in  scope  at  the  instantiation  can  be  used  by  the  instantiation,  and  anything  normally  in  scope  at  the formal can be accessed by the formal.  The end result is that the relevant scoping  roadblocks  no  longer  apply.  It  isn't  the  full  lambda  calculus,  just  one  of  the  most  useful  parts.

![](Images/image07199.jpeg)

For  a  view  of  Functional  Programming  in  Ada  see  [8](#part0252.xhtml__bookmark656).

## 27.3 Compiler  Messages

Compiler  Messages

Different  compilers  can  diagnose  different  things  differently,  or  the  same  thing  using  different  messages,  etc..  Having  two  compilers  at  hand  can  be  useful.

###### selected  component

When a source program contains a construct such as Foo.Bar, you may see messages  saying something like «selected component "Bar"» or maybe like «selected component  "Foo"».  The  phrases  may  seem  confusing,  because  one  refers  to  Foo,  while  the  other  refers

![](Images/image07200.jpeg)

5 [http://en.wikipedia.org/wiki/opaque%20pointer](http://en.wikipedia.org/wiki/opaque%20pointer)

6 [http://en.wikipedia.org/wiki/Set%20%28computer%20science%29](http://en.wikipedia.org/wiki/Set%20%28computer%20science%29)

7 Chapter  [20](#part0163.xhtml__bookmark489)  on  page  [161](#part0163.xhtml__bookmark489)

8 FunctionalProgrammingin...Ada?ˆ{[http://okasaki.blogspot.com/2008/07/](http://okasaki.blogspot.com/2008/07/functional-programming-inada.html)  [functional-programming-inada.html}](http://okasaki.blogspot.com/2008/07/functional-programming-inada.html)  ,  by  Chris  Okasaki

to Bar. But they are both right. The reason is that selected_component is an item from  Ada's grammar (4.1.3 Selected Components ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-1-3.html)  [content/standards/05rm/html/RM-4-1-3.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-1-3.html) ).  It denotes all of:  a prefix, a dot, and  a  selector_name.  In  the  Foo.Bar  example  these  correspond  to  Foo,  '.',  and  Bar.  Look  for  more grammar words in the compiler messages, e.g. «prefix», and associate them with  identifiers  quoted  in  the  messages.

For  example,  if  you  submit  the  following  code  to  the  compiler,

![](Images/image07201.jpeg)

the compiler may print a diagnostic message about a prefixed component:  Foo's author  thought that Pak denotes a package, but actually it is the name of a generic package.  (Which  needs  to  be  instantiated  first;  and  then  the  instance  name  is  a  suitable  prefix.)

## 27.4 Universal  integers

Universal  integers

All integer literals and also some attributes like 'Length are of the anonymous type  universal_integer, which comprises the infinite set of mathematical integers.  Named  numbers are of this type and are evaluated exactly (no overlow except for machine storage  limitations),  e.g.

![](Images/image07202.jpeg)

Since universal_integer has no operators, its values are converted in this example to root_-  integer,  another  anonymous  type,  the  calcuation  is  performed  and  the  result  again  converted  back  in  universal_integer.

Generally values of universal_integer are implicitly converted to the appropriate type when  used  in  some  expression.  So  the  expression  not  A'  Length  is  fine;  the  value  of  A' Length  is interpreted as a modular integer since not can only be applied to modular integers (of  course a context is needed to decide which modular integer type is meant). This feature can  lead  to  pitfalls.  Consider

![](Images/image07203.jpeg)

and  then

![](Images/image07204.jpeg)

![](Images/image07205.jpeg)

The second conditional cannot be compiled because the expressions to the left of in is  incompatible  to  the  type  at  the  right.  Note  that  not  has  precedence  over  in.  It  does  not  negate  the  entire  membership  test  but  only  A'  Length.

The  fourth  conditional  fails  in  various  ways.

The sixth conditional might be fine because not turns A' Length into a modular value  which  is  OK  if  the  value  is  covered  by  modular  type  Mod_6.

GNAT  GPL  2009  gives  these  diagnoses  respectively:

![](Images/image07206.jpeg)

A  way  to  avoid  these  problems  is  to  use  not  in  for  the  membership  test,

![](Images/image07207.jpeg)

See

• 2.4 Numeric  Literals ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-4.html)  [05rm/html/RM-2-4.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-4.html) ,

• 3.6.2  Operations  of  Array  Types  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-6-2.html)  [standards/05rm/html/RM-3-6-2.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-6-2.html) ),  and

• 4.5  Operators  and  Expression  Evaluation  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-5.html)  [content/standards/05rm/html/RM-4-5.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-5.html) ,

• 4.5.2  Relational  Operators  and  Membership  Tests  ˆ{[http://www.adaic.org/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-5-2.html)  [resources/add_content/standards/05rm/html/RM-4-5-2.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-5-2.html) ,

• Membership  Tests[9](#part0254.xhtml__bookmark659)

## 27.5 I/O

![](Images/image07208.jpeg)

9 Chapter  [37.3](#part0305.xhtml__bookmark859)  on  page  [303](#part0305.xhtml__bookmark859)

I/O

#### 27.5.1  Text_IO  Issues

A canonical method of reading a sequence of lines from a text file uses the standard procedure  Ada .Get_Line.  When the end of input is reached, Get_Line will fail, and exception End_-  Error is raised. Some programs will use another function from Ada  to prevent this and test  for End_of_Input.  However, this isn't always the best choice, as has been explained for  example  in  a  Get_Line  news  group  discussion  on  comp.lang.ada[10](#part0255.xhtml__bookmark661).

A  working  solution  uses  an  exception  handler  instead:

![](Images/image07209.jpeg)

## 27.6 Quirks

Quirks

Using  GNAT  on  Windows,  calls  to  subprograms  from  Ada  might  need  special  attention.  (For  example,  the  Real_Time.Clock  function  might  seem  to  return  values  indicating  that  no time has passed between two invocations when certainly some time has passed.)  The  cause is reported to be a missing initialization of the run-time support when no other  real-time  features  are  present  in  the  program.[11](#part0255.xhtml__bookmark662)  As  a  provisional  fix,  it  is  suggested  to  insert

![](Images/image07210.jpeg)

before  any  use  of  Real_Time  services.

#### 27.6.1 Stack  Size

With  some  implementations,  notably  GNAT,  knowledge  of  stack  size  manipulation  will  be  to  your  advantage.  Executables  produced  with  GNAT  tools  and  standard  settings  can  hit  the  stack  size  limit.  If  so,  the  operating  system  might  allow  setting  higher  limits.  Using

![](Images/image07211.jpeg)

10 [http://groups.google.com/group/comp.lang.ada/browse_thread/thread/5afe598156615c8b#](http://groups.google.com/group/comp.lang.ada/browse_thread/thread/5afe598156615c8b)

11 Vincent  Celier  .  Timing  code  blocks  Timing  code  blocks  ˆ{groups.google.es/group/comp.lang.ada/  browse_thread/thread/c8acfc87fbb1813d}  .  ,  Usenet  article  forwards  this  information  from  AdaCore.

GNU/Linux  and  the  Bash  command  shell,  try

![](Images/image07212.jpeg)

The  current  value  is  printed  when  only  -s  is  given  to  ulimit.

## 27.7 References

References

## 27.8 See  also

See  also

#### 27.8.1 Wikibook

• Ada  Programming[12](#part0256.xhtml__bookmark665)

• Ada  Programming/Errors[13](#part0256.xhtml__bookmark666)

#### 27.8.2 Ada  Reference  Manual

• 3.10.1  Incomplete  Type  Declarations  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-10-1.html)  [content/standards/05rm/html/RM-3-10-1.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-10-1.html)

![](Images/image07213.jpeg)

12 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

13 Chapter  [28](#part0257.xhtml__bookmark667)  on  page  [255](#part0257.xhtml__bookmark667)

# 28 Common  Errors

Some  language  features  are  often  misunderstood,  resulting  in  common  programming  errors,  performance degradation and portability problems. The following incorrect usages of the  Ada  language  are  often  seen  in  code  written  by  Ada  beginners.

## 28.1 pragma  Atomic  &  Volatile

pragma  Atomic  &  Volatile

It is  almost  always  incorrect  to  use  atomic[1](#part0257.xhtml__bookmark669) or  volatile[2](#part0257.xhtml__bookmark670) variables  for  tasking[3](#part0257.xhtml__bookmark671).[4](#part0257.xhtml__bookmark672)  When an object is atomic it just means that it will be read from or written to memory  atomically. The compiler will not generate atomic instructions or memory barriers when  accessing  to  that  object,  it  will  just:

• check  that  the  architecture  guarantees  atomic  memory  loads  and  stores,

• disallow some compiler optimizations, like reordering or suppressing redundant accesses  to  the  object.

For  example,  the  following  code,  where  A  is  an  atomic  object  can  be  misunderstood:

![](Images/image07214.jpeg)

The compiler will not (and is not allowed by the Standard to) generate an atomic increment  instruction to directly increment and update from memory the variable A.[6](#part0257.xhtml__bookmark673) This is the code  generated  by  the  compiler:

| 804969f: | a1  04 95 05 08 | mov | 0x8059504,%eax |
| 80496a4: | 40 | inc | %eax |
| 80496a5: | a3  04 95 05 08 | mov | %eax,0x8059504 |

![](Images/image07215.jpeg)As can be seen, no atomic increment instruction or test-and-set opcode will be generated.  Like  in  other  programming  languages,  if  these  specific  instructions  are  required  in  the  program  they  must  be  written  explicitly  using  machine  code  insertions.[8](#part0257.xhtml__bookmark674)

![](Images/image07216.jpeg)

1 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAtomic](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAtomic)

2 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FVolatile](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FVolatile)

3 Chapter  [21](#part0175.xhtml__bookmark499)  on  page  [173](#part0175.xhtml__bookmark499)

4 Volatile:  Almost  Useless  for  Multi-Threaded  Programming  2008-05-30

![](Images/image07217.jpeg)![](Images/image07218.jpeg)6[7](#part0000.xhtml__bookmark0)

5. Intel  Software  Network  .  Retrieved

8Laurent  Guerby  Ada  95  Rationale  .  Intermetrics  ,  ,  1995

The above  code snippet  is equivalent  to the following code (both  code sequences generates  exactly  the  same  object  code),  where  T  is  a  (non-atomic)  temporary  variable:

![](Images/image07219.jpeg)

Thus  it  is  incorrect  to  modify  an  atomic  variable  at  the  same  time  from  multiple  tasks.  For example, two tasks incrementing a counter in parallel. Even in an uniprocessor, other  Ada tasking features like a protected object should be used instead.  In multiprocessors,  depending on the memory consistency model[9](#part0258.xhtml__bookmark677), using various atomic or volatile variables for  task communication can have surprising consequences.[10](#part0258.xhtml__bookmark678)[12](#part0258.xhtml__bookmark679) Therefore, extreme care should  be taken when using atomic objects for task data sharing or synchronization, specially in a  multiprocessor.

## 28.2 References

References

## 28.3 pragma  Pack

pragma  Pack

#### 28.3.1 Exact  data  representation

It is important to realize that pragma Pack[13](#part0258.xhtml__bookmark680) must not be used to specify the exact  representation  of  a  data  type, but to help the compiler to improve the efficiency of  the generated code.[14](#part0258.xhtml__bookmark681)  The compiler is free to ignore the pragma, therefore if a specific  representation  of  a  type  is  required,  representation  clauses[15](#part0258.xhtml__bookmark682)  should  be  used  instead  (record  representation  clauses,  and/or  attributes  'Size[16](#part0258.xhtml__bookmark683)  or  'Component_Size[17](#part0258.xhtml__bookmark684)).

![](Images/image07220.jpeg)

9 [http://en.wikipedia.org/wiki/Memory%20model%20%28programming%29](http://en.wikipedia.org/wiki/Memory%20model%20%28programming%29)

10 Volatile  [11](#part0000.xhtml__bookmark0).  .  Retrieved  2008-05-28

12 Sarita V. Adve, Kourosh Gharachorloo . Shared Memory Consistency Models: A Tutorial  Shared Mem-  ory Consistency Models: A Tutorial  ˆ{[www.hpl.hp.com/techreports/Compaq-](http://www.hpl.hp.com/techreports/Compaq-){}DEC/WRL-{}95-{}7.  pdf}  .  IEEE  Computer  ,  29  :  66−76  December  1996

13 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPack](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPack)

14 Adam  Beneschan  .  Pragma  Pack  vs.  Convention  C,  portability  issue?  Pragma  Pack  vs.  Convention  C,  portability  issue?  ˆ{groups.google.es/group/comp.lang.ada/msg/6698960624779ec7}  .  ,

15 [http://en.wikibooks.org/wiki/Ada%20Programming%2FRepresentation%20clauses](http://en.wikibooks.org/wiki/Ada%20Programming%2FRepresentation%20clauses)

16 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Size](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Size)

17 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Component_Size](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Component_Size)

![](Images/image07221.jpeg)

#### 28.3.2 Bit-wise  operations

Although in Ada 83 packed boolean arrays were used for bit-wise operations,[18](#part0259.xhtml__bookmark688) since Ada 95  modular types[19](#part0259.xhtml__bookmark689) are more adequate for these operations.[20](#part0259.xhtml__bookmark690) The argument may be weighed  against  the  advantages  of  named  Boolean  array  indexes  such  as  Traffic_Lights'  (  Red

=> True, others => False) ,  depending  on  use  case.

## 28.4 'Bit_Order attribute

'Bit_Order  attribute

The 'Bit_Order[21](#part0259.xhtml__bookmark691) attribute  is  not  intended  to  convert  data  between  a  big-endian  and a little-endian machine (it affects bit numbering, not byte order). The compiler will  not generate  code to  reorder multi-byte  fields  when a  non-native  bit  order  is  specified.[22](#part0259.xhtml__bookmark692)[23](#part0259.xhtml__bookmark693)[24](#part0259.xhtml__bookmark694)

## 28.5 'Size  attribute

'Size  attribute

A  common  Ada  programming  mistake  is  to  assume  that  specifying  'Size  for  a  type  T  forces  the compiler to allocate exactly this number of bits for objects of this type. This is not true.  The specified T'Size[26](#part0259.xhtml__bookmark695) will force the compiler to use this size for components in  packed arrays and records and in Unchecked_Conversion, but the compiler is still  free  to  allocate  more  bits  for  stand-alone  objects.

Use  'Size  on  the  object  itself  to  force  the  object  to  the  specified  value.

## 28.6 See  also

![](Images/image07222.jpeg)

18 Software Productivity Consortium (October 1995).  Ada 95 Quality and Style Guide, "10.5.7 Packed  Boolean  Array  Shifts  ˆ{[http://www.adaic.org/resources/add_content/docs/95style/html/sec_10/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_10/10-5-7.html)  [10-5-7.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_10/10-5-7.html)  "

19 Chapter  [7](#part0073.xhtml__bookmark245)  on  page  [71](#part0073.xhtml__bookmark245)

20 Software Productivity Consortium (October 1995). Ada 95 Quality and Style Guide, "10.6.3 Bit Op-  erations  on  Modular  Types  ˆ{[http://www.adaic.org/resources/add_content/docs/95style/html/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_10/10-6-3.html)  [sec_10/10-6-3.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_10/10-6-3.html)  "

21 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Bit%20Order](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Bit%20Order)

22 .  .  ,

23 ISO/IEC  8652:2007.  13.5.3  Bit  Ordering  (9/2). Ada  2005  Reference  Manual. Bit_Order  clauses  make it possible to write record_representation_clauses that can be ported between machines having  different bit ordering. They do not guarantee transparent exchange of data between such machines.  ˆ{[http://www.adaic.org/resources/add_content/standards/05rm/html/RM-13-5-3.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-13-5-3.html)

24 [25](#part0000.xhtml__bookmark0).  .  Retrieved

26 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Size](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Size)

See  also

#### 28.6.1 Wikibook

• Ada  Programming[27](#part0260.xhtml__bookmark697)

• Ada  Programming/Tips[28](#part0260.xhtml__bookmark698)

## 28.7 References

References

![](Images/image07223.jpeg)

27 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

28 Chapter  [27](#part0251.xhtml__bookmark645)  on  page  [249](#part0251.xhtml__bookmark645)

# 29 Algorithms

## 29.1 Introduction

Introduction

Welcome  to  the  Ada  implementations  of  the  Algorithms[1](#part0261.xhtml__bookmark702)  Wikibook.  For  those  who  are  new  to  Ada  Programming[2](#part0261.xhtml__bookmark703)  a  few  notes:

• All  examples  are  fully  functional  with  all  the  needed  input  and  output  operations.  However, only the code needed to outline the algorithms at hand is copied into the text -  the full samples are available via the download links. (Note: It can take up to 48 hours  until  the  cvs  is  updated).

• We seldom use predefined types in the sample code but define special types suitable for  the  algorithms  at  hand.

• Ada allows for default function parameters; however, we always fill in and name all  parameters,  so  the  reader  can  see  which  options  are  available.

• We seldom use shortcuts - like using the attributes Image or Value for String <=> Integer  conversions.

All these rules make the code more elaborate than perhaps needed. However, we also hope  it  makes  the  code  easier  to  understand

Category:Ada  Programming[3](#part0261.xhtml__bookmark704)

## 29.2 Chapter  1: Introduction

Chapter  1:  Introduction

The  following  subprograms  are  implementations  of  the  Inventing  an  Algorithm  examples[4](#part0261.xhtml__bookmark705).

#### 29.2.1 To  Lower

The Ada example code does not append to the array as the algorithms.  Instead we create  an  empty  array  of  the  desired  length  and  then  replace  the  characters  inside.

![](Images/image07224.jpeg)

1 [http://en.wikibooks.org/wiki/Algorithms](http://en.wikibooks.org/wiki/Algorithms)

2 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

3 [http://en.wikibooks.org/wiki/Category%3AAda%20Programming](http://en.wikibooks.org/wiki/Category%3AAda%20Programming)

4 [http://en.wikibooks.org/wiki/Algorithms%2FIntroduction%23Inventing%20an%20Algorithm](http://en.wikibooks.org/wiki/Algorithms%2FIntroduction%23Inventing%20an%20Algorithm)

![](Images/image07225.jpeg)

Would the append approach be  impossible with Ada?  No,  but it  would be significantly more  complex  and  slower.

29.2.2 Equal  Ignore  Case

![](Images/image07226.jpeg)![](Images/image07227.jpeg)

## 29.3 Chapter  6: Dynamic  Programming

![](Images/image07228.jpeg)

Chapter  6:  Dynamic  Programming

#### 29.3.1  Fibonacci  numbers

The  following  codes  are  implementations  of  the  Fibonacci-Numbers  examples[5](#part0263.xhtml__bookmark707).

###### Simple  Implementation

![](Images/image07229.jpeg)![](Images/image07230.jpeg)

To  calculate  Fibonacci  numbers  negative  values  are  not  needed  so  we  define  an  integer  type  which  starts  at  0.  With  the  integer  type  defined  you  can  calculate  up  until  Fib  (87).  Fib

(88)  will  result  in  an  Constraint_Error.

![](Images/image07231.jpeg)

You  might  notice  that  there  is  not  equivalence  for  the  assert  (n  >=  0)  from  the  original  example.  Ada  will  test  the  correctness  of  the  parameter  before  the  function  is  called.

![](Images/image07232.jpeg)

###### Cached  Implementation

![](Images/image07233.jpeg)![](Images/image07234.jpeg)

For  this  implementation  we  need  a  special  cache  type  can  also  store  a  -1  as  "not  calculated"  marker

![](Images/image07235.jpeg)

5 [http://en.wikibooks.org/wiki/Algorithms%2FDynamic%20Programming%23Fibonacci_Numbers](http://en.wikibooks.org/wiki/Algorithms%2FDynamic%20Programming%23Fibonacci_Numbers)

![](Images/image07236.jpeg)

The actual type for calculating the fibonacci numbers continues to start at 0.  As it is a  subtype  of  the  cache  type  Ada  will  automatically  convert  between  the  two.  (the  conversion  is  -  of  course  -  checked  for  validity)

![](Images/image07237.jpeg)

In  order  to  know  how  large  the  cache  need  to  be  we  first  read  the  actual  value  from  the  command  line.

![](Images/image07238.jpeg)

The  Cache  array  starts  with  element  2  since  Fib  (0)  and  Fib  (1)  are  constants  and  ends  with  the  value  we  want  to  calculate.

![](Images/image07239.jpeg)

The  Cache  is  initialized  to  the  first  valid  value  of  the  cache  type  —  this  is  -1.

![](Images/image07240.jpeg)

What  follows  is  the  actual  algorithm.

![](Images/image07241.jpeg)

This  implementation  is  faithful  to  the  original  from  the  Algorithms[6](#part0264.xhtml__bookmark708)  book.  However,  in  Ada  you  would  normally  do  it  a  little  different:

![](Images/image07242.jpeg)

![](Images/image07243.jpeg)

6 [http://en.wikibooks.org/wiki/Algorithms](http://en.wikibooks.org/wiki/Algorithms)

when  you  use  a  slightly  larger  array  which  also  stores  the  elements  0  and  1  and  initializes  them  to  the  correct  values

![](Images/image07244.jpeg)

and  then  you  can  remove  the  first  if  path.

![](Images/image07245.jpeg)

![](Images/image07246.jpeg)![](Images/image07247.jpeg).  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .  .

This  will  save  about  45%  of  the  execution-time  (measured  on  Linux  i686)  while  needing  only  two  more  elements  in  the  cache  array.

###### Memory  Optimized  Implementation

This  version  looks  just  like  the  original  in  WikiCode.

![](Images/image07248.jpeg)![](Images/image07249.jpeg)

###### No  64  bit  integers

Your Ada compiler does not support 64 bit integer numbers?  Then you could try to use  decimal numbers[7](#part0267.xhtml__bookmark709) instead. Using decimal numbers results in a slower program (takes about  three  times  as  long)  but  the  result  will  be  the  same.

The following example shows you how to define a suitable decimal type.  Do experiment  with  the  digits  and  range  parameters  until  you  get  the  optimum  out  of  your  Ada  compiler.

|  |
|  | File: fibonacci_5.adb |
|  |
|  |  |

![](Images/image07250.jpeg)

You should know that floating point numbers are unsuitable for the calculation of fibonacci  numbers. They will not report an error condition when the number calculated becomes too  large  —  instead  they  will  lose  in  precision  which  makes  the  result  meaningless.

![](Images/image07251.jpeg)

7 Chapter  [10](#part0081.xhtml__bookmark278)  on  page  [79](#part0081.xhtml__bookmark278)

# 30 Function  overloading

![](Images/image07252.jpeg)

![](Images/image07253.jpeg)

![](Images/image07254.jpeg)

## 30.1 Function  overloading  in  Ada

Function  overloading  in  Ada

Ada  supports  all  six  signature  options  but  if  you  use  the  arguments'  name  as  option  you  will  always  have  to  name  the  parameter  when  calling  the  function.  i.e.:

![](Images/image07255.jpeg)

Note  that  you  cannot  overload  a  generic  procedure  or  generic  function  within  the  same  package.  The  following  example  will  fail  to  compile:

![](Images/image07256.jpeg)

## 30.2 See  also

See  also

#### 30.2.1 Wikibook

• Ada  Programming[1](#part0270.xhtml__bookmark713)

• Ada  Programming/Subprograms[2](#part0270.xhtml__bookmark714)

#### 30.2.2 Ada  95  Reference  Manual

• 6.6  Overloading  of  Operators  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-6-6.html)  [standards/95lrm/ARM_HTML/RM-6-6.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-6-6.html)

• 8.6  The  Context  of  Overload  Resolution  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-8-6.html)  [content/standards/95lrm/ARM_HTML/RM-8-6.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-8-6.html)

#### 30.2.3 Ada  2005  Reference  Manual

• 6.6  Overloading  of  Operators  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-6-6.html)  [standards/05rm/html/RM-6-6.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-6-6.html)

• 8.6  The  Context  of  Overload  Resolution  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-8-6.html)  [content/standards/05rm/html/RM-8-6.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-8-6.html)

![](Images/image07257.jpeg)

1 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

2 Chapter  [16](#part0127.xhtml__bookmark381)  on  page  [125](#part0127.xhtml__bookmark381)

# 31 Mathematical calculations

Ada  is  very  well  suited  for  all  kind  of  calculations.  You  can  define  you  own  fixed  point  and floating point types and — with the aid of generic packages call all the mathematical  functions you need. In that respect Ada is on par with Fortran[1](#part0271.xhtml__bookmark717). This module will show you  how  to  use  them  and  while  we  progress  we  create  a  simple  RPN[2](#part0271.xhtml__bookmark718)  calculator.

## 31.1 Simple  calculations

Simple  calculations

#### 31.1.1 Addition

Additions can be done using the predefined operator + . The operator is predefined for all  numeric  types  and  the  following,  working  code,  demonstrates  its  use:

![](Images/image07258.jpeg)<map name="awmap3"><area shape="rect" href="_bookmark0" coords="173, 59, 180, 72"></map>![](Images/image07259.jpeg)

1 [http://en.wikibooks.org/wiki/Programming%3AFortran](http://en.wikibooks.org/wiki/Programming%3AFortran)

2 [http://en.wikipedia.org/wiki/Reverse%20Polish%20notation](http://en.wikipedia.org/wiki/Reverse%20Polish%20notation)

#### 31.1.2 Subtraction

Subtractions  can  be  done  using  the  predefined  operator  -  .  The  following  extended  demo  shows  the  use  of  +  and  -  operator  together:

![](Images/image07260.jpeg)<map name="awmap4"><area shape="rect" href="_bookmark0" coords="173, 59, 180, 72"></map>

Purists  might  be  surprised  about  the  use  of  goto  —  but  some  people  prefer  the  use  of  goto  over  the  use  of  multiple  return  statements  if  inside  functions  —  given  that,  the  opinions  on  this  topic  vary  strongly.  See  the  isn't  goto  evil[5](#part0273.xhtml__bookmark719)  article.

#### 31.1.3 Multiplication

Multiplication can be done using the predefined operator * .  For a demo see the next chapter  about  Division.

#### 31.1.4 Division

Divisions can be done using the predefined operators / ,  mod ,  rem .  The operator /  performs a normal division, mod returns a modulus division and rem returns the remainder  of  the  modulus  division.

The following extended demo shows the use of the + , - , *  and /   operators together as  well  as  the  use  of  a  four  number  wide  stack  to  store  intermediate  results:

The operators mod  and rem  are not part of the demonstration as they are only defined for  integer  types.

![](Images/image07261.jpeg)![](Images/image07262.jpeg)

5Chapter  [4](#part0039.xhtml__bookmark161)  on  page  [37](#part0039.xhtml__bookmark161)

![](Images/image07263.jpeg)

## 31.2 Exponential  calculations

Exponential  calculations

All  exponential  functions  are  defined  inside  the  generic  package  Ada  .

#### 31.2.1 Power  of

Calculation of the form xy  are performed by the operator ** .  Beware:  There are two  versions of this operator. The predefined operator ** allows only for Standard.Integer to be  used  as  exponent.  If  you  need  to  use  a  floating  point  type  as  exponent  you  need  to  use  the

**  defined  in  Ada  .

#### 31.2.2 Root

![](Images/image07264.jpeg)The  square  root  √x  is  calculated  with  the  function  Sqrt().  There  is  no  function  defined  to

![](Images/image07265.jpeg)calculate  an  arbitrary  root  √n  x.  However  you  can  use  logarithms  to  calculate  an  arbitrary

![](Images/image07266.jpeg)root  using  the  mathematical  identity:   √b  a  =  eloge(a)/b  which  will  become  root  :=  Exp  (Log

![](Images/image07267.jpeg)![](Images/image07268.jpeg)(a)  /  b)  in  Ada.  Alternatively,  use  √b  a  =  a  1  which,  in  Ada,  is  root  :=  a**(1.0/b).

b

#### 31.2.3 Logarithm

Ada  defines  a  function  for  both  the  arbitrary  logarithm  logn(x)  and  the  natural  logarithm

loge(x),  both  of  which  have  the  same  name  Log()  distinguished  by  the  number  of  parameters.

#### 31.2.4 Demonstration

The following extended demo shows the how to use the exponential functions in Ada. The  new demo also uses Unbounded_String[6](#part0275.xhtml__bookmark721) instead of Strings which make the comparisons  easier.

Please note that from now on we won't copy the full sources any more.  Do follow the  download  links  to  see  the  full  program.

![](Images/image07269.jpeg)

function  Get_Line  return  Str.Unbounded_String  is

BufferSize  :  constant  :=  2000;

Retval:  Str.Unbounded_String  :=  Str.Null_Unbounded_String;  Item:  String  (1  ..  BufferSize);

Last:  Natural;

begin

Get_Whole_Line  :

loop

T_IO.Get_Line  (Item  =>  Item,  Last  =>  Last);

Str.Append  (Source  =>  Retval,  New_Item  =>  Item  (1  ..

Last));

exit  Get_Whole_Line  when  Last  <  Item’Last;

end  loop Get_Whole_Line;

return  Retval;

end  Get_Line;

...

begin

Main_Loop  :

loop

T_IO.Put  (">");

Operation  :=  Get_Line;

...

elsif  Operation  =  "e"  then

--    insert  e  Push_Value;

Values  (1)  :=  Ada.Numerics.e;

elsif  Operation  =  "**"  or  else  Operation  =  "ˆ"  then

-- power  of  xˆy

Values  (1)  :=  Values  (1)  **  Values  (2);  Pop_Value;

elsif  Operation  =  "sqr"  then

-- square  root

Values  (1)  :=  Sqrt  (Values  (1));

elsif  Operation  =  "root" then

-- arbritary root  Values  (1)  :=

Exp  (Log  (Values  (2))  /  Values  (1));  Pop_Value;

elsif  Operation  =  "ln"  then

-- natural  logarithm

Values  (1)  :=  Log  (Values  (1));

elsif  Operation  =  "log"  then

-- based  logarithm  Values  (1)  :=

Log  (Base  =>  Values  (1),  X  =>  Values  (2));  Pop_Value;

elsif  Operation  =  "exit"  then  exit  Main_Loop;

else

Push_Value;

F_IO.Get

(From  =>  Str.To_String  (Operation),  Item  =>  Values  (1),

Last  =>  Dummy);

end  if;

![](Images/image07270.jpeg)

...

end  loop  Main_Loop;

![](Images/image07271.jpeg)

## 31.3 Higher  math

Higher  math

#### 31.3.1 Trigonometric  calculations

The  full  set  of  trigonometric[7](#part0277.xhtml__bookmark723)  functions  are  defined  inside  the  generic  package  Ada  .  All  functions  are  defined  for  2  and  an  arbitrary  cycle  value  (a  full  cycle  of  revolution).

Please  note  the  difference  of  calling  the  Arctan  ()  function.

![](Images/image07272.jpeg)![](Images/image07273.jpeg)![](Images/image07274.jpeg)

7[http://en.wikibooks.org/wiki/%2FTrigonometry](http://en.wikibooks.org/wiki/%2FTrigonometry)

![](Images/image07275.jpeg)

The  Demo  also  contains  an  improved  numeric  output  which  behaves  more  like  a  normal  calculator.

#### 31.3.2 Hyperbolic calculations

You  guessed  it:  The  full  set  of  hyperbolic  functions  is  defined  inside  the  generic  package  Ada  .

![](Images/image07276.jpeg)

![](Images/image07277.jpeg)

As added bonus this version supports error handling and therefore won't just crash when an  illegal  calculation  is  performed.

#### 31.3.3 Complex  arithmethic

For complex arithmetic[8](#part0280.xhtml__bookmark724) Ada provides the package Ada . This package is part of the "special  need Annexes" which means it is optional. The open source Ada compiler GNAT implements  all  "special  need  Annexes"  and  therefore  has  complex  arithmetic  available.

Since Ada supports user defined operators, all (+ , - , * ) operators have their usual meaning  as soon as the package Ada  has been instantiated (package ... is new ...)  and the type has  been  made  visible  (use  type  ...)

Ada also provides the packages Ada  and Ada  which provide similar functionality to their  normal  counterparts.  But  there  are  some  differences:

• Ada  supports only the exponential and trigonometric functions which make sense in  complex  arithmetic.

• Ada  is a child package of Ada  and therefore needs its own with. Note: the Ada  Get  ()  function is pretty fault tolerant - if you forget the "," or the "()" pair it will still parse the  input  correctly.

So,  with only a very few modifications you can convert your "normals" calculator to a  calculator  for  complex  arithmetic:

![](Images/image07278.jpeg)![](Images/image07279.jpeg)![](Images/image07280.jpeg)

8 [http://en.wikibooks.org/wiki/Algebra%2FComplex%20Numbers](http://en.wikibooks.org/wiki/Algebra%2FComplex%20Numbers)

use  Complex_Functions;

Values:  Value_Array  :=

(others  =>  Complex_Types.Complex’(Re  =>  0.0,  Im =>  0.0));

...

procedure  Put_Line  (Value  :  in  Complex_Types.Complex)  is  begin

if  (abs  Value_Type’Exponent  (Value.Re)  >=

abs  Value_Type’Exponent  (10.0  **  C_IO.Default_Aft))

or  else  (abs  Value_Type’Exponent  (Value.Im)  >=

abs  Value_Type’Exponent  (10.0  **  C_IO.Default_Aft))

then

C_IO.Put

(Item  =>  Value,

Fore  =>  C_IO.Default_Aft,  Aft  =>  C_IO.Default_Aft,  Exp  =>  4);

else

C_IO.Put

(Item  =>  Value,

Fore  =>  C_IO.Default_Aft,  Aft  =>  C_IO.Default_Aft,  Exp  =>  0);

end if;  T_IO.New_Line;

return;  end  Put_Line;

begin

...

=>  0.0);

...

elsif  Operation  =  "e"  then

--    insert  e  Push_Value;  Values  (1)  :=

Complex_Types.Complex’(Re  =>  Ada.Numerics.e,  Im

![](Images/image07281.jpeg)

=>  0.0);

elsif  Operation  =  "pi"  or  else  Operation  =  ""  then

--    insert  pi  Push_Value;  Values  (1)  :=

Complex_Types.Complex’(Re  =>  Ada.Numerics.Pi,  Im

elsif  Operation  =  "sin"  then

-- sinus

Values  (1)  :=  Sin  (Values  (1));

elsif  Operation  =  "cos"  then

-- cosinus

Values  (1)  :=  Cot  (Values  (1));

elsif  Operation  =  "tan"  then

-- tangents

Values  (1)  :=  Tan  (Values  (1));

elsif  Operation  =  "cot"  then

-- cotanents

Values  (1)  :=  Cot  (Values  (1));

elsif  Operation  =  "asin"  then

-- arc-sinus

Values  (1)  :=  Arcsin  (Values  (1));

elsif  Operation  =  "acos"  then

-- arc-cosinus

![](Images/image07282.jpeg)

#### 31.3.4 Vector  and  Matrix  Arithmetic

Ada  supports  vector[9](#part0282.xhtml__bookmark726)  and  matrix[10](#part0282.xhtml__bookmark727)  Arithmetic  for  both  normal  real  types  and  com-  plex  types.  For  those,  the  generic  packages  Ada.Numerics.Generic_Real_Arrays  and  Ada.Numerics.Generic_Complex_Arrays  are  used.  Both  packages  offer  the  usual  set  of  operations,  however  there  is  no  I/O  package  and  understandably,  no  package  for  elementary  functions.

Since there is no I/O package for vector and matrix I/O creating a demo is by far more  complex — and hence not ready yet. You can have a look at the current progress which will  be  a  universal  calculator  merging  all  feature.

Status: Stalled - for a Vector and Matrix stack we need Indefinite_Vectors — which are  currently  not  part  of  GNAT/Pro.  Well  I  could  use  the  booch  components  ...

| File:  numeric_8-complex_calculator.ada |
| File:  numeric_8-get_line.ada |
| File:  numeric_8-real_calculator.ada |
| File:  numeric_8-real_vector_calculator.ada |

## 31.4 See  also

See  also

#### 31.4.1 Wikibook

• Ada  Programming[11](#part0282.xhtml__bookmark728)

![](Images/image07283.jpeg)

9 [http://en.wikibooks.org/wiki/Linear%20Algebra%2FVectors%20in%20Space](http://en.wikibooks.org/wiki/Linear%20Algebra%2FVectors%20in%20Space)

10 [http://en.wikibooks.org/wiki/Linear_Algebra%2FDescribing_the_Solution_Set%23matrix](http://en.wikibooks.org/wiki/Linear_Algebra%2FDescribing_the_Solution_Set%23matrix)

11 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

• Ada  Programming/Delimiters/-[12](#part0283.xhtml__bookmark729)

• Ada  Programming/Libraries/Ada.Numerics.Generic_Complex_Types[13](#part0283.xhtml__bookmark730)

• Ada  Programming/Libraries/Ada.Numerics.Generic_Elementary_Functions[14](#part0283.xhtml__bookmark731)

#### 31.4.2 Ada  95  Reference  Manual

• 4.4  Expressions  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-4-4.html)  [95lrm/ARM_HTML/RM-4-4.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-4-4.html)

• Annex  A.5-1  Elementary  Functions  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-A-5-1.html)  [content/standards/95lrm/ARM_HTML/RM-A-5-1.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-A-5-1.html)

• Annex  A.10-1  The  Package  Text_IO  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-A-10-1.html)  [content/standards/95lrm/ARM_HTML/RM-A-10-1.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-A-10-1.html)

• Annex G.1 Complex Arithmetic ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-G-1.html)  [standards/95lrm/ARM_HTML/RM-G-1.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-G-1.html)  Annex G.3 Vector and Matrix Manip-  ulation  ˆ{[http://www.adaic.org/resources/add_content/standards/95lrm/ARM_](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-G-3.html)  [HTML/RM-G-3.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-G-3.html) myitemize

#### 31.4.3 Ada  2005  Reference  Manual

• 4.4  Expressions  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-4.html)  [05rm/html/RM-4-4.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-4.html)

• Annex  A.5.1  Elementary  Functions  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-5-1.html)  [content/standards/05rm/html/RM-A-5-1.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-5-1.html)

• Annex  A.10.1  The  Package  Text_IO  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-10-1.html)  [content/standards/05rm/html/RM-A-10-1.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-10-1.html)

• G1Complex  Arithmetic

• G3Vector  and  Matrix  Manipulation

![](Images/image07284.jpeg)

12 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F-](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F-)

13 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Generic_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Generic_Complex_Types)  [Complex_Types](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Generic_Complex_Types)

14 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Generic_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Generic_Elementary_Functions)

[Elementary_Functions](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Generic_Elementary_Functions)

# 32 Statements

Note:  there  are  some  simplifications  in  the  explanations  below.  Don‘t  take  anything  too  literally.

Most  programming  languages  have  the  concept  of  a  statement.  A  statement  is  a  command  that  the  programmer  gives  to  the  computer.  For  example:

![](Images/image07285.jpeg)

This command has a verb ("") and other details (what to print). In this case, the command  "" means "show on the screen," not "print on the printer." The programmer either gives  the  statement  directly  to  the  computer  (by  typing  it  while  running  a  special  program),  or creates a text file with the command in it.  You could create a file called "hi.txt", put  the  above  command  in  it,  and  give  the  file  to  the  computer.

If you have more than one command in the file, each will be performed in order, top to  bottom.  So  the  file  could  contain:

![](Images/image07286.jpeg)

This  does  seem  like  a  lot  of  typing  but  don't  worry:  Ada  allows  you  to  declare  shorter  aliasnames  if  you  need  a  long  statement  very  often.

# 33 Variables

Variables are references that stand in for a value that is contained at a certain memory  address.

Variables are said to have a value and may have a data type[1](#part0287.xhtml__bookmark737).  If a variable has a type,  then  only  values  of  this  type  may  be  assigned  to  it.  Variables  do  not  always  have  a  type.  A value can have many values of many different types: integers (7), ratios (1/2), (approx-  imations  of)  reals  (10.234), complex  numbers  (4+2i), characters  ('a'),  strings  ("hello"),  and  much  more.

Different languages use different names for their types and may not include any of the  above.

## 33.1 Assignment  statements

Assignment  statements

An  assignment  statement  is  used  to  set  a  variable  to  a  new  value.  Assignment  statements  are  written  as  name  =[2](#part0287.xhtml__bookmark738)  value.

![](Images/image07287.jpeg)<map name="awmap5"><area shape="rect" href="_bookmark0" coords="71, 11, 77, 24"></map>

1. REDIRECT  Template:Computer  Programming/Variables/2[4](#part0287.xhtml__bookmark739)  Ada  is  the  same.  The  declaration  is  as  follows:

![](Images/image07288.jpeg)<map name="awmap6"><area shape="rect" href="_bookmark0" coords="145, 22, 152, 35"></map>

## 33.2 Uses

Uses

Variables  store  everything  in  your  program.  The  purpose  of  any  useful  program  is  to  modify  variables.

## 33.3 See  also

![](Images/image07289.jpeg)

1 [http://en.wikibooks.org/wiki/Computer%20Programming%2FTypes](http://en.wikibooks.org/wiki/Computer%20Programming%2FTypes)

2 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%3A%3D](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%3A%3D)

4[http://en.wikibooks.org/wiki/Template%3AComputer%20Programming%2FVariables%2F2](http://en.wikibooks.org/wiki/Template%3AComputer%20Programming%2FVariables%2F2)

Variables

See  also

#### 33.3.1  Ada  Reference  Manual

• 3.3  Objects  and  Named  Numbers  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-3.html)  [content/standards/05rm/html/RM-3-3.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-3.html)

# 34 Lexical  elements

## 34.1 Character  set

Character  set

The  character  set  used  in  Ada  programs  is  composed  of:

• Upper-case  letters:  A,  ...,  Z  and  lower-case  letters:  a,  ...,  z.

• Digits:  0,  ...,  9.

• Special  characters.

Take into account that in Ada 95 the letter range includes accented characters and other  letters  used  in  Western Europe languages,  those  belonging  to  the ISO  Latin-1[1](#part0289.xhtml__bookmark743) character  set,  as  ç,  ñ,  ð,  etc.

In Ada 2005[2](#part0289.xhtml__bookmark744) the character set has been extended to the full Unicode[3](#part0289.xhtml__bookmark745) set, so the identifiers  and  comments  can  be  written  in  almost  any  language  in  the  world.

Ada is a case-insensitive language, i. e. the upper-case set is equivalent to the lower-case  set  except  in  character  string  literals  and  character  literals.

## 34.2 Lexical  elements

Lexical  elements

In  Ada  we  can  find  the  following  lexical  elements:

• Identifiers

• Numeric  Literals

• Character  Literals

• String  Literals

• Delimiters[4](#part0289.xhtml__bookmark746)

• Comments

• Reserved Words[5](#part0289.xhtml__bookmark747)  Example:

![](Images/image07290.jpeg)

This  line  contains  5  lexical  elements:

• The  identifier  Temperature_In_Room.

• The compound  delimiter  :=.

• The  number  25.

• The  single  delimiter  ;.

![](Images/image07291.jpeg)

1 [http://en.wikipedia.org/wiki/ISO%208859-1](http://en.wikipedia.org/wiki/ISO%208859-1)

2 Chapter  [23](#part0221.xhtml__bookmark541)  on  page  [219](#part0221.xhtml__bookmark541)

3 [http://en.wikipedia.org/wiki/Unicode](http://en.wikipedia.org/wiki/Unicode)

4 Chapter  [36](#part0299.xhtml__bookmark777)  on  page  [297](#part0299.xhtml__bookmark777)

5 Chapter  [35](#part0295.xhtml__bookmark761)  on  page  [293](#part0295.xhtml__bookmark761)

• The  comment  --Temperature  to  be  preserved  in  the  room..

#### 34.2.1  Identifiers

Definition  in  BNF[6](#part0290.xhtml__bookmark749):

![](Images/image07292.jpeg)

From  this  definition  we  must  exclude  the  keywords  that  are  reserved  words  in  the  language  and  cannot  be  used  as  identifiers.

Examples:

The  following  words  are  legal  Ada  identifiers:

![](Images/image07293.jpeg)

The  following  ones  are  NOT  legal  Ada  identifiers:

![](Images/image07294.jpeg)

Exercise:  could  you  give  the  reason  for  not  being  legal  for  each  one  of  them?

#### 34.2.2  Numbers

The  numeric  literals  are  composed  of  the  following  characters:

• digits 0  ..9

• the  decimal  separator  .,

• the  exponentiation  sign  e  or  E,

• the  negative  sign  - (in  exponents only)  and

• the underscore  _.

The  underscore  is  used  as  separator  for  improving  legibility  for  humans,  but  it  is  ignored  by  the  compiler.  You  can  separate  numbers  following  any  rationale,  e.g.  decimal  integers  in  groups  of  three  digits,  or  binary  integers  in  groups  of  eight  digits.

For  example,  the real  number such  as  98.4 can  be  represented as:  9.84E1,  98.4e0,  984.0e-1  or  0.984E+2,  but  not  as  984e-1.

For  integer  numbers,  for  example  1900,  it  could  be  written  as  1900,  19E2,  190e+1  or

1_900E+0.

A  numeric  literal  could  also  be  expressed  in  a  base  different  to  10,  by  enclosing  the  number  between # characters, and preceding it by the base, which can be a number between 2  and  16.  For  example,  2#101#  is  1012,  that  is  510;  a  hexadecimal  number  with  exponent  is  16#B#E2,  that  is  11  ×  162  =  2,816.

Note  that  there  are  no  negative  literals;  e.g.  -1  is  not  a  literal,  rather  it  is  the  literal  1

preceded  by  the  unary  minus  operator.

![](Images/image07295.jpeg)

6 [http://en.wikipedia.org/wiki/Backus-Naur%20form](http://en.wikipedia.org/wiki/Backus-Naur%20form)

#### 34.2.3 Character  literals

Their  type  is  Standard  .Character,  Wide_Character  or  Wide_Wide_Character.  They  are  delimited  by  an  apostrophe  (')[7](#part0291.xhtml__bookmark751).

Examples:

![](Images/image07296.jpeg)

#### 34.2.4 String  literals

String[8](#part0291.xhtml__bookmark752)  literals  are  of  type  Standard  .String,  Wide_String  or  Wide_Wide_String.  They  are  delimited  by  the  quotation  mark  (")[9](#part0291.xhtml__bookmark753).

Example:

![](Images/image07297.jpeg)

#### 34.2.5 Delimiters

Single  delimiters  are  one  of  the  following  special  characters:

![](Images/image07298.jpeg)

Compound  delimiters  are  composed  of  two  special  characters,  and  they  are  the  following  ones:

![](Images/image07299.jpeg)

You  can  see  a  full  reference  of  the  delimiters  in  Ada  Programming/Delimiters[10](#part0291.xhtml__bookmark754).

#### 34.2.6 Comments

Comments  in  Ada  start  with  two  consecutive  hyphens  (--)  and  end  in  the  end  of  line.

![](Images/image07300.jpeg)

A  comment  can  appear  where  an  end  of  line  can  be  inserted.

![](Images/image07301.jpeg)

7 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%27](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%27)

8 Chapter  [15](#part0121.xhtml__bookmark373)  on  page  [119](#part0121.xhtml__bookmark373)

9 [http://en.wikibooks.org/wiki/Ada%20Programming%2FSpecial%2F%22](http://en.wikibooks.org/wiki/Ada%20Programming%2FSpecial%2F%22)

10 Chapter  [36](#part0299.xhtml__bookmark777)  on  page  [297](#part0299.xhtml__bookmark777)

#### 34.2.7  Reserved  words

Reserved words are equivalent in upper-case and lower-case letters, although the typical  style is the one from the Reference Manual, that is to write them in all lower-case letters.  In Ada some keywords have a different meaning depending on context. You can refer to  Ada  Programming/Keywords[11](#part0292.xhtml__bookmark756)  and  the  following  pages  for  each  keyword.

Ada  Keywords[12](#part0000.xhtml__bookmark0)

| abort | else | new | return |
| abs | elsif | not | reverse |
| abstract  (Ada  95) | end | null |  |
| accept | entry |  | select |
| access | exception | of | separate |
| aliased  (Ada  95) | exit | or | some |
|  |  |  | (Ada  2012) |
| all |  | others | subtype |
| and | for | out | synchronized |
|  |  |  | (Ada  2005) |
| array | function | overriding |  |
|  |  | (Ada  2005) |  |
| at |  |  | tagged |
|  |  |  | (Ada  95) |
|  | generic | package | task |
| begin | goto | pragma | terminate |
| body |  | private | then |
|  | if | procedure | type |
| case | in | protected |  |
|  |  | (Ada  95) |  |
| constant | interface |  | until |
|  | (Ada  2005) |  | (Ada  95) |
|  | is | raise | use |
| declare |  | range |  |
| delay | limited | record | when |
| delta | loop | rem | while |
| digits |  | renames | with |
| do | mod | requeue | xor |
|  |  | (Ada  95) |  |

## 34.3 See  also

![](Images/image07302.jpeg)

11 Chapter  [35](#part0295.xhtml__bookmark761)  on  page  [293](#part0295.xhtml__bookmark761)

12 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAll%20Keywords](http://en.wikibooks.org/wiki/Ada%20Programming%2FAll%20Keywords)

See  also

#### 34.3.1 Wikibook

• Ada  Programming[13](#part0293.xhtml__bookmark757)

• Ada Programming/Delimiters[14](#part0293.xhtml__bookmark758)

• Ada  Programming/Keywords[15](#part0293.xhtml__bookmark759)

#### 34.3.2 Ada  Reference  Manual

• Section  2:  Lexical  Elements  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2.html)  [standards/05rm/html/RM-2.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2.html)

• 2.1  Character  Set ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-1.html)  [05rm/html/RM-2-1.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-1.html)

• 2.2 Lexical Elements,Separators, and  Delimiters  ˆ{[http://www.adaic.org/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-2.html)  [resources/add_content/standards/05rm/html/RM-2-2.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-2.html)

es:Programación  en  Ada/Elementos  del  lenguaje[16](#part0293.xhtml__bookmark760)

13 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

14 Chapter  [36](#part0299.xhtml__bookmark777)  on  page  [297](#part0299.xhtml__bookmark777)

15 Chapter  [35](#part0295.xhtml__bookmark761)  on  page  [293](#part0295.xhtml__bookmark761)

16 [http://es.wikibooks.org/wiki/Programaci%F3n%20en%20Ada%2FElementos%20del%20lenguaje](http://es.wikibooks.org/wiki/Programaci%F3n%20en%20Ada%2FElementos%20del%20lenguaje)

# 35 Keywords

## 35.1 Language  summary  keywords

Language  summary  keywords

Most  Ada  “keywords”  have  different  functions  depending  on  where  they  are  used.  A  good  example  is  for[1](#part0295.xhtml__bookmark764) which  controls  the  representation  clause  when  used  within  a  declaration  part  and  controls  a  loop  when  used  within  an  implementation.

In Ada, a keyword is a reserved word, so it cannot be used as an identifier. Some of  them  are  used  as  attribute[2](#part0295.xhtml__bookmark765)  names.

## 35.2 List  of  keywords

List  of  keywords

###### Ada  Keywords[3](#part0000.xhtml__bookmark0)

![](Images/image07303.jpeg)

1 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Ffor](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Ffor)

2 Chapter  [38](#part0307.xhtml__bookmark878)  on  page  [305](#part0307.xhtml__bookmark878)

3 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAll%20Keywords](http://en.wikibooks.org/wiki/Ada%20Programming%2FAll%20Keywords)

Keywords

| abort | else | new | return |
| abs | elsif | not | reverse |
| abstract  (Ada  95) | end | null |  |
| accept | entry |  | select |
| access | exception | of | separate |
| aliased  (Ada  95) | exit | or | some |
|  |  |  | (Ada  2012) |
| all |  | others | subtype |
| and | for | out | synchronized |
|  |  |  | (Ada  2005) |
| array | function | overriding |  |
|  |  | (Ada  2005) |  |
| at |  |  | tagged |
|  |  |  | (Ada  95) |
|  | generic | package | task |
| begin | goto | pragma | terminate |
| body |  | private | then |
|  | if | procedure | type |
| case | in | protected |  |
|  |  | (Ada  95) |  |
| constant | interface |  | until |
|  | (Ada  2005) |  | (Ada  95) |
|  | is | raise | use |
| declare |  | range |  |
| delay | limited | record | when |
| delta | loop | rem | while |
| digits |  | renames | with |
| do | mod | requeue | xor |
|  |  | (Ada  95) |  |

## 35.3 See  also

See  also

#### 35.3.1  Wikibook

• Ada  Programming[4](#part0296.xhtml__bookmark767)

• Ada  Programming/Aspects[5](#part0296.xhtml__bookmark768)

• Ada  Programming/Attributes[6](#part0296.xhtml__bookmark769)

• Ada  Programming/Pragmas[7](#part0296.xhtml__bookmark770)

![](Images/image07304.jpeg)

4 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

5 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAspects](http://en.wikibooks.org/wiki/Ada%20Programming%2FAspects)

6 Chapter  [38](#part0307.xhtml__bookmark878)  on  page  [305](#part0307.xhtml__bookmark878)

7 Chapter  [39](#part0319.xhtml__bookmark1089)  on  page  [317](#part0319.xhtml__bookmark1089)

#### 35.3.2 Ada  Reference  Manual

###### Ada  83

• Annex  2:  Reserved  Words  ˆ{[http://archive.adaic.com/standards/83lrm/html/](http://archive.adaic.com/standards/83lrm/html/lrm-2.html)  [lrm-2.html}](http://archive.adaic.com/standards/83lrm/html/lrm-2.html)

• Annex  E:  Syntax  Summary  ˆ{[http://archive.adaic.com/standards/83lrm/html/](http://archive.adaic.com/standards/83lrm/html/lrm-E.html)  [lrm-E.html}](http://archive.adaic.com/standards/83lrm/html/lrm-E.html)

###### Ada  95

• 2.9  Reserved  Words[8](#part0297.xhtml__bookmark771)

• Annex  P:  (informative)  Syntax  Summary[9](#part0297.xhtml__bookmark772)

###### Ada  2005

• 2.9  Reserved  Words[10](#part0297.xhtml__bookmark773)

• Annex  P:  (informative)  Syntax  Summary[11](#part0297.xhtml__bookmark774)

###### Ada  2012

• 2.9  Reserved  Words[12](#part0297.xhtml__bookmark775)

• Annex  P:  (informative)  Syntax  Summary[13](#part0297.xhtml__bookmark776)

#### 35.3.3 Ada  Quality  and  Style  Guide

• 3.1.3Capitalizationˆ{[http://www.adaic.org/resources/add_content/docs/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_3/3-1-3.html)  [95style/html/sec_3/3-1-3.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_3/3-1-3.html)

![](Images/image07305.jpeg)

8 [http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-2-9.html](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-2-9.html)

9 [http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-P.html](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-P.html)

10 [http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-2-9.html](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-2-9.html)

11 [http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-P.html](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-P.html)

12 [http://www.ada-auth.org/standards/12rm/html/RM-2-9.html](http://www.ada-auth.org/standards/12rm/html/RM-2-9.html)

13 [http://www.ada-auth.org/standards/12rm/html/RM-P.html](http://www.ada-auth.org/standards/12rm/html/RM-P.html)

# 36 Delimiters

## 36.1 Single  character  delimiters

Single  character  delimiters

&[1](#part0299.xhtml__bookmark779)

ampersand  (also  operator  &[2](#part0299.xhtml__bookmark780))

'[3](#part0299.xhtml__bookmark781)

apostrophe,  tick

([4](#part0299.xhtml__bookmark782)

left  parenthesis

)[5](#part0299.xhtml__bookmark783)

right  parenthesis

*[6](#part0299.xhtml__bookmark784)

asterisk,  multiply  (also  operator  *[7](#part0299.xhtml__bookmark785))

+[8](#part0299.xhtml__bookmark786)

plus  sign  (also  operator  +[9](#part0299.xhtml__bookmark787))

,[10](#part0299.xhtml__bookmark788)

comma

-[11](#part0299.xhtml__bookmark789)

hyphen,  minus  (also  operator  -[12](#part0299.xhtml__bookmark790))

.[13](#part0299.xhtml__bookmark791)

full  stop,  point,  dot

/[14](#part0299.xhtml__bookmark792)

solidus,  divide (also  operator  /[15](#part0299.xhtml__bookmark793))

[16](#part0299.xhtml__bookmark794)

colon

;[17](#part0299.xhtml__bookmark795)

![](Images/image07306.jpeg)

1 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%26](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%26)

2 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%26](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%26)

3 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%27](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%27)

4 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%28](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%28)

5 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%29](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%29)

6 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2A](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2A)

7 [http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2F%2A](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2F%2A)

8 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2B](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2B)

9 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2B](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2B)

10 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2C](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2C)

11 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F-](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F-)

12 [http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2F-](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2F-)

13 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fdot](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fdot)

14 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2F](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2F)

15 [http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2F%2F](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2F%2F)

16 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%3A](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%3A)

17 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%3B](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%3B)

Delimiters

semicolon

<[18](#part0300.xhtml__bookmark797)

less  than  sign  (also  operator)

=[19](#part0300.xhtml__bookmark798)

equal  sign  (also  operator  =[20](#part0300.xhtml__bookmark799))

>[21](#part0300.xhtml__bookmark800)

greater  than  sign  (also  operator)

[22](#part0300.xhtml__bookmark801)

vertical  line

## 36.2 Compound  character  delimiters

Compound  character  delimiters

=>[23](#part0300.xhtml__bookmark802)

arrow

..[24](#part0300.xhtml__bookmark803)

double  dot

**[25](#part0300.xhtml__bookmark804)

double  star,  exponentiate  (also  operator  **[26](#part0300.xhtml__bookmark805))

=[27](#part0300.xhtml__bookmark806)

assignment

/=[28](#part0300.xhtml__bookmark807)

inequality  (also  operator)

>=[29](#part0300.xhtml__bookmark808)

greater  than  or  equal  to  (also  operator)

<=[30](#part0300.xhtml__bookmark809)

less  than  or  equal  to  (also  operator)

<<[31](#part0300.xhtml__bookmark810)

left  label  bracket

>>[32](#part0300.xhtml__bookmark811)

right  label  bracket

<>[33](#part0300.xhtml__bookmark812)

![](Images/image07307.jpeg)

18 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fless%20than](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fless%20than)

19 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%3D](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%3D)

20 [http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2F%3D](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2F%3D)

21 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fgreater%20than](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fgreater%20than)

22 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fvertical%20line](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fvertical%20line)

23 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Farrow](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Farrow)

24 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fdouble%20dot](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fdouble%20dot)

25 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2A%2A](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2A%2A)

26 [http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2F%2A%2A](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2F%2A%2A)

27 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%3A%3D](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%3A%3D)

28 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2F%3D](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2F%3D)

29 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fgreater%20than%20or%](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fgreater%20than%20or%20equal%20to)  [20equal%20to](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fgreater%20than%20or%20equal%20to)

30 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fless%20than%20or%](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fless%20than%20or%20equal%20to)

[20equal%20to](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fless%20than%20or%20equal%20to)

31 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fleft%20label](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fleft%20label)

32 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fright%20label](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fright%20label)

33 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fbox](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fbox)

box

## 36.3 Others

Others

The  following  ones  are  special  characters  but  not  delimiters.

"[34](#part0301.xhtml__bookmark815)

quotation  mark,  used  for  string  literals[35](#part0301.xhtml__bookmark816).

#[36](#part0301.xhtml__bookmark817)

number  sign,  used  in  based  numeric  literals[37](#part0301.xhtml__bookmark818).

The following special characters are unused in Ada code - they are illegal except within  string literals and comments (they are used in the Reference Manual Backus-Naur syntax  definition  of  Ada):

###### [

left  square  bracket

###### ]

right  square  bracket

###### {

left  curly  bracket

###### }

right  curly bracket

## 36.4 See  also

See  also

#### 36.4.1 Wikibook

• Ada  Programming[38](#part0301.xhtml__bookmark819)

#### 36.4.2 Ada  95  Reference  Manual

• 2.1  Character  Set ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-2-1.html)  [95lrm/ARM_HTML/RM-2-1.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-2-1.html)

• 2.2 Lexical Elements,Separators,  and  Delimiters  ˆ{[http://www.adaic.org/](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-2-2.html)  [resources/add_content/standards/95lrm/ARM_HTML/RM-2-2.html}](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-2-2.html)

#### 36.4.3 Ada  2005  Reference  Manual

• 2.1  Character  Set ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-1.html)  [05rm/html/RM-2-1.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-1.html)

• 2.2 Lexical Elements,Separators, and  Delimiters  ˆ{[http://www.adaic.org/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-2.html)  [resources/add_content/standards/05rm/html/RM-2-2.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-2.html)

![](Images/image07308.jpeg)

34 [http://en.wikibooks.org/wiki/Ada%20Programming%2FSpecial%2F%22](http://en.wikibooks.org/wiki/Ada%20Programming%2FSpecial%2F%22)

35 Chapter  [34.2.4](#part0291.xhtml__bookmark750)  on  page  [289](#part0291.xhtml__bookmark750)

36 [http://en.wikibooks.org/wiki/Ada%20Programming%2FSpecial%2Fnumber%20sign](http://en.wikibooks.org/wiki/Ada%20Programming%2FSpecial%2Fnumber%20sign)

37 Chapter  [34.2.2](#part0290.xhtml__bookmark748)  on  page  [288](#part0290.xhtml__bookmark748)

38 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

# 37 Operators

## 37.1 Standard  operators

Standard  operators

Ada[1](#part0303.xhtml__bookmark822) allows operator overloading[2](#part0303.xhtml__bookmark823) for all standard operators and so the following sum-  maries can only describe the suggested standard operations for each operator. It is quite  possible  to  misuse  any  standard  operator  to  perform  something  unusual.

Each  operator  is  either  a  keyword[3](#part0303.xhtml__bookmark824) or  a  delimiter[4](#part0303.xhtml__bookmark825) --  hence  all  operator  pages  are  redirects  to  the  appropriate  keyword[5](#part0303.xhtml__bookmark826)  or  delimiter[6](#part0303.xhtml__bookmark827).

Operators  have  arguments  which  in  the  RM  are  called  Left  and  Right  for  binary  operators,  Right for unary operators (indicating the position with respect to the operator symbol).  The  list  is  sorted  from  lowest  precedence  to  highest  precedence.

#### 37.1.1 Logical  operators

###### and[7](#part0303.xhtml__bookmark828)

![](Images/image07309.jpeg)and  xy,  (also  keyword and[8](#part0303.xhtml__bookmark829))

###### or[9](#part0303.xhtml__bookmark830)

![](Images/image07310.jpeg)or  xy,  (also  keyword  or[10](#part0303.xhtml__bookmark831))

###### xor[11](#part0303.xhtml__bookmark832)

exclusive  or  (x  ∧  y¯)  ∨  (x¯  ∧  y),  (also  keyword  xor[12](#part0303.xhtml__bookmark833))

#### 37.1.2 Relational  operators

/=[13](#part0303.xhtml__bookmark834)

![](Images/image07311.jpeg)Not  Equal  x  =  y,  (also  special  character  /=[14](#part0303.xhtml__bookmark835))

=[15](#part0303.xhtml__bookmark836)

Equal  x  =  y,  (also  special  character  =[16](#part0303.xhtml__bookmark837))

![](Images/image07312.jpeg)

1 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

2 [http://en.wikipedia.org/wiki/operator%20overloading](http://en.wikipedia.org/wiki/operator%20overloading)

3 Chapter  [35](#part0295.xhtml__bookmark761)  on  page  [293](#part0295.xhtml__bookmark761)

4 Chapter  [36](#part0299.xhtml__bookmark777)  on  page  [297](#part0299.xhtml__bookmark777)

5 Chapter  [35](#part0295.xhtml__bookmark761)  on  page  [293](#part0295.xhtml__bookmark761)

6 Chapter  [36](#part0299.xhtml__bookmark777)  on  page  [297](#part0299.xhtml__bookmark777)

7 [http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fand](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fand)

8 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fand](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fand)

9 [http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2For](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2For)

10 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2For](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2For)

11 [http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fxor](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fxor)

12 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fxor](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fxor)

13 [http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2F%2F%3D](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2F%2F%3D)

14 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2F%3D](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2F%3D)

15 [http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2F%3D](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2F%3D)

16 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%3D](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%3D)

<[17](#part0304.xhtml__bookmark838)

Less  than  x  <  y,  (also  special  character  <[18](#part0304.xhtml__bookmark839))

<=[19](#part0304.xhtml__bookmark840)

![](Images/image07313.jpeg)Less  than  or  equal  to  (xy),  (also  special  character  <=[20](#part0304.xhtml__bookmark841))

>[21](#part0304.xhtml__bookmark842)

Greater  than  (x  >  y),  (also  special  character  >[22](#part0304.xhtml__bookmark843))

>=[23](#part0304.xhtml__bookmark844)

Greater  than  or  equal  to  (x  ≥  y),  (also  special  character  >=[24](#part0304.xhtml__bookmark845))

#### 37.1.3  Binary  adding  operators

+[25](#part0304.xhtml__bookmark846)

Add  x  +  y,  (also  special  character  +[26](#part0304.xhtml__bookmark847))

-[27](#part0304.xhtml__bookmark848)

![](Images/image07314.jpeg)Subtract  xy,  (also  special  character  -[28](#part0304.xhtml__bookmark849))

&[29](#part0304.xhtml__bookmark850)

Concatenate  ,  x  &  y,  (also  special  character  &[30](#part0304.xhtml__bookmark851))

#### 37.1.4  Unary  adding  operators

+[31](#part0304.xhtml__bookmark852)

Plus  sign  +x,  (also  special  character  +[32](#part0304.xhtml__bookmark853))

-[33](#part0304.xhtml__bookmark854)

Minus  sign  −x,  (also  special  character  -[34](#part0304.xhtml__bookmark855))

#### 37.1.5  Multiplying  operator

*[35](#part0304.xhtml__bookmark856)

Multiply,  x  ×  y,  (also  special  character  *[36](#part0304.xhtml__bookmark857))

![](Images/image07315.jpeg)

17 [http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fless%20than](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fless%20than)

18 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fless%20than](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fless%20than)

19 [http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fless%20than%20or%](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fless%20than%20or%20equal%20to)  [20equal%20to](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fless%20than%20or%20equal%20to)

20 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fless%20than%20or%](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fless%20than%20or%20equal%20to)

[20equal%20to](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fless%20than%20or%20equal%20to)

21 [http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fgreater%20than](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fgreater%20than)

22 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fgreater%20than](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fgreater%20than)

23 [http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fgreater%20than%20or%](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fgreater%20than%20or%20equal%20to)  [20equal%20to](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fgreater%20than%20or%20equal%20to)

24 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fgreater%20than%20or%](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fgreater%20than%20or%20equal%20to)

[20equal%20to](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2Fgreater%20than%20or%20equal%20to)

25 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2B](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2B)

26 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2B](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2B)

27 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F-](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F-)

28 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F-](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F-)

29 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%26](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%26)

30 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%26](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%26)

31 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2B](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2B)

32 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2B](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2B)

33 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F-](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F-)

34 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F-](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F-)

35 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2A](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2A)

36 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2A](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2A)

/[37](#part0305.xhtml__bookmark860)

Divide  x/y,  (also  special  character  /[38](#part0305.xhtml__bookmark861))

###### mod[39](#part0305.xhtml__bookmark862)

modulus  (also  keyword  mod[40](#part0305.xhtml__bookmark863))

###### rem[41](#part0305.xhtml__bookmark864)

remainder  (also  keyword  rem[42](#part0305.xhtml__bookmark865))

#### 37.1.6 Highest  precedence  operator

**[43](#part0305.xhtml__bookmark866)

Power xy, (also  special  character  **[44](#part0305.xhtml__bookmark867))

###### not[45](#part0305.xhtml__bookmark868)

![](Images/image07316.jpeg)logical  notx,  (also  keyword  not[46](#part0305.xhtml__bookmark869))

###### abs[47](#part0305.xhtml__bookmark870)

absolute  value  |x|  (also  keyword  abs[48](#part0305.xhtml__bookmark871))

## 37.2 Short-circuit  control  forms

Short-circuit  control  forms

These  are  not  operators  and  thus  cannot  be  overloaded.

###### and  then[49](#part0305.xhtml__bookmark872)

e.g.  if  Y  /=  0  and  then  X/Y  >  Limit  then  ...

###### or  else[50](#part0305.xhtml__bookmark873)

e.g.  if  Ptr  =  null  or  else  Ptr.I  =  0  then  ...

## 37.3 Membership tests

Membership  tests

The  Membership  Tests  also  cannot  be  overloaded  because  they  are  not  operators.

in[51](#part0305.xhtml__bookmark874)

![](Images/image07317.jpeg)element  of,  vartype, e.g.  if I in  Positive  then, (also keyword in)  not  in[52](#part0305.xhtml__bookmark875)

![](Images/image07318.jpeg)

37 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2F](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2F)

38 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2F](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2F)

39 [http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fmod](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fmod)

40 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fmod](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fmod)

41 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Frem](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Frem)

42 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Frem](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Frem)

43 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2A%2A](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2A%2A)

44 [http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2A%2A](http://en.wikibooks.org/wiki/Ada%20Programming%2FDelimiters%2F%2A%2A)

45 [http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fnot](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fnot)

46 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fnot](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fnot)

47 [http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fabs](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fabs)

48 [http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fabs](http://en.wikibooks.org/wiki/Ada%20Programming%2FKeywords%2Fabs)

49 [http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fand%23Boolean_shortcut_](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fand%23Boolean_shortcut_operator)  [operator](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fand%23Boolean_shortcut_operator)

50 [http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2For%23Boolean_shortcut_](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2For%23Boolean_shortcut_operator)

[operator](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2For%23Boolean_shortcut_operator)

51 [http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fin](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fin)

52 [http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fin](http://en.wikibooks.org/wiki/Ada%20Programming%2FOperators%2Fin)

not  element  of,  var  ∈/  type,  e.g.  if  I  not  in  Positive  then,  (also  keywords  not  in)

#### 37.3.1  Range  membership  test

![](Images/image07319.jpeg)

37.3.2  Subtype  membership  test

![](Images/image07320.jpeg)

37.3.3  Class  membership  test

![](Images/image07321.jpeg)

## 37.4 See  also

See  also

#### 37.4.1  Wikibook

• Ada  Programming[53](#part0306.xhtml__bookmark877)

#### 37.4.2  Ada  95  Reference  Manual

• 4.5  Operators  and  Expression  Evaluation  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-5.html)  [content/standards/05rm/html/RM-4-5.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-5.html)

#### 37.4.3  Ada  2005  Reference  Manual

• 4.5  Operators  and  Expression  Evaluation  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-5.html)  [content/standards/05rm/html/RM-4-5.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-4-5.html)

#### 37.4.4  Ada  Quality  and  Style  Guide

• 2.1.3 Alignment of  Operators ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_2/2-1-3.html)  [docs/95style/html/sec_2/2-1-3.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_2/2-1-3.html)

• 5.7.4  Overloaded  Operators  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_5/5-7-4.html)  [docs/95style/html/sec_5/5-7-4.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_5/5-7-4.html)

• 5.7.5  Overloading  the  Equality  Operator  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/docs/95style/html/sec_5/5-7-5.html)  [content/docs/95style/html/sec_5/5-7-5.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_5/5-7-5.html)

###### Ada  Operators[54](#part0000.xhtml__bookmark0)

and[55](#part0000.xhtml__bookmark0)and  then[56](#part0000.xhtml__bookmark0)>[57](#part0000.xhtml__bookmark0)+[58](#part0000.xhtml__bookmark0)abs[59](#part0000.xhtml__bookmark0)&[60](#part0000.xhtml__bookmark0)  or[61](#part0000.xhtml__bookmark0)or else[62](#part0000.xhtml__bookmark0)>=[63](#part0000.xhtml__bookmark0)-[64](#part0000.xhtml__bookmark0)              mod[65](#part0000.xhtml__bookmark0)

xor[66](#part0000.xhtml__bookmark0)=[67](#part0000.xhtml__bookmark0)<[68](#part0000.xhtml__bookmark0)*[69](#part0000.xhtml__bookmark0)rem[70](#part0000.xhtml__bookmark0)in[71](#part0000.xhtml__bookmark0)

###### not[72](#part0000.xhtml__bookmark0)/=[73](#part0000.xhtml__bookmark0)<=[74](#part0000.xhtml__bookmark0)**[75](#part0000.xhtml__bookmark0)/[76](#part0000.xhtml__bookmark0)not  in[77](#part0000.xhtml__bookmark0)

![](Images/image07322.jpeg)

53 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

54 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAll%20Operators](http://en.wikibooks.org/wiki/Ada%20Programming%2FAll%20Operators)

# 38 Attributes

## 38.1 Language  summary  attributes

Language  summary  attributes

The concept of attributes is pretty unique to Ada[1](#part0307.xhtml__bookmark881). Attributes allow you to get —and  sometimes set— information about objects or other language entities such as types. A  good  example  is  the  Size  attribute.  It  describes  the  size  of  an  object  or  a  type  in  bits.

![](Images/image07323.jpeg)<map name="awmap7"><area shape="rect" href="_bookmark0" coords="444, 11, 450, 24"></map>

However,  unlike  the  sizeof  operator  from  C[3](#part0307.xhtml__bookmark882)/C++[4](#part0307.xhtml__bookmark883)  the  Size  attribute  can  also  be  set:

![](Images/image07324.jpeg)

Of  course  not  all  attributes  can  be  set.  An  attribute  starts  with  a  tick  '  and  is  followed  by its name.  The compiler determines by context if the tick is the beginning of an  attribute  or  of  a  character  literal.

![](Images/image07325.jpeg)

## 38.2 List  of  language  defined  attributes

List  of  language  defined  attributes

###### Ada  2005

This  is  a  new  Ada  2005[5](#part0307.xhtml__bookmark884)  attribute.

###### Ada  2012

This  is  a  new  Ada  2012[6](#part0307.xhtml__bookmark885)  attribute.

###### Obsolescent

This  is  a  deprecated  attribute  and  should  not  be  used  in  new  code.

![](Images/image07326.jpeg)

1[http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

3 [http://en.wikibooks.org/wiki/C%20Programming](http://en.wikibooks.org/wiki/C%20Programming)

4 [http://en.wikibooks.org/wiki/C%2B%2B%20Programming](http://en.wikibooks.org/wiki/C%2B%2B%20Programming)

5 Chapter  [23](#part0221.xhtml__bookmark541)  on  page  [219](#part0221.xhtml__bookmark541)

6 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAda%202012](http://en.wikibooks.org/wiki/Ada%20Programming%2FAda%202012)

38.2.1  A  −  B

• 'Access[7](#part0308.xhtml__bookmark886)

• 'Address[8](#part0308.xhtml__bookmark887)

• 'Adjacent[9](#part0308.xhtml__bookmark888)

• 'Aft[10](#part0308.xhtml__bookmark889)

• 'Alignment[11](#part0308.xhtml__bookmark890)

• 'Base[12](#part0308.xhtml__bookmark891)

• 'Bit_Order[13](#part0308.xhtml__bookmark892)

• 'Body_Version[14](#part0308.xhtml__bookmark893)

38.2.2  C

• 'Callable[15](#part0308.xhtml__bookmark894)

• 'Caller[16](#part0308.xhtml__bookmark895)

• 'Ceiling[17](#part0308.xhtml__bookmark896)

• 'Class[18](#part0308.xhtml__bookmark897)

• 'Component_Size[19](#part0308.xhtml__bookmark898)

• 'Compose[20](#part0308.xhtml__bookmark899)

• 'Constrained[21](#part0308.xhtml__bookmark900)

• 'Copy_Sign[22](#part0308.xhtml__bookmark901)

• 'Count[23](#part0308.xhtml__bookmark902)

38.2.3  D  −  F

• 'Definite[24](#part0308.xhtml__bookmark903)

• 'Delta[25](#part0308.xhtml__bookmark904)

• 'Denorm[26](#part0308.xhtml__bookmark905)

• 'Digits[27](#part0308.xhtml__bookmark906)

• 'Emax[28](#part0308.xhtml__bookmark907)  (Obsolescent)

![](Images/image07327.jpeg)

7 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Access](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Access)

8 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Address](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Address)

9 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Adjacent](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Adjacent)

10 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Aft](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Aft)

11 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Alignment](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Alignment)

12 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Base](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Base)

13 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Bit_Order](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Bit_Order)

14 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Body_Version](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Body_Version)

15 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Callable](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Callable)

16 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Caller](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Caller)

17 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Ceiling](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Ceiling)

18 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Class](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Class)

19 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Component_Size](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Component_Size)

20 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Compose](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Compose)

21 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Constrained](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Constrained)

22 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Copy_Sign](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Copy_Sign)

23 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Count](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Count)

24 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Definite](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Definite)

25 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Delta](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Delta)

26 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Denorm](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Denorm)

27 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Digits](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Digits)

28 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Emax](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Emax)

• 'Exponent[29](#part0309.xhtml__bookmark908)

• 'External_Tag[30](#part0309.xhtml__bookmark909)

• 'Epsilon[31](#part0309.xhtml__bookmark910)  (Obsolescent)

• 'First[32](#part0309.xhtml__bookmark911)

• 'First_Bit[33](#part0309.xhtml__bookmark912)

• 'Floor[34](#part0309.xhtml__bookmark913)

• 'Fore[35](#part0309.xhtml__bookmark914)

• 'Fraction[36](#part0309.xhtml__bookmark915)

38.2.4 G  −  L

• 'Has_Same_Storage[37](#part0309.xhtml__bookmark916)  (Ada  2012)

• 'Identity[38](#part0309.xhtml__bookmark917)

• 'Image[39](#part0309.xhtml__bookmark918)

• 'Input[40](#part0309.xhtml__bookmark919)

• 'Large[41](#part0309.xhtml__bookmark920)  (Obsolescent)

• 'Last[42](#part0309.xhtml__bookmark921)

• 'Last_Bit[43](#part0309.xhtml__bookmark922)

• 'Leading_Part[44](#part0309.xhtml__bookmark923)

• 'Length[45](#part0309.xhtml__bookmark924)

#### 38.2.5 M

• 'Machine[46](#part0309.xhtml__bookmark925)

• 'Machine_Emax[47](#part0309.xhtml__bookmark926)

• 'Machine_Emin[48](#part0309.xhtml__bookmark927)

• 'Machine_Mantissa[49](#part0309.xhtml__bookmark928)

• 'Machine_Overflows[50](#part0309.xhtml__bookmark929)

![](Images/image07328.jpeg)

29 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Exponent](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Exponent)

30 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27External_Tag](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27External_Tag)

31 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Epsilon](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Epsilon)

32 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27First](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27First)

33 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27First_Bit](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27First_Bit)

34 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Floor](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Floor)

35 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Fore](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Fore)

36 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Fraction](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Fraction)

37 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Has_Same_Storage](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Has_Same_Storage)

38 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Identity](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Identity)

39 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Image](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Image)

40 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Input](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Input)

41 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Large](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Large)

42 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Last](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Last)

43 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Last_Bit](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Last_Bit)

44 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Leading_Part](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Leading_Part)

45 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Length](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Length)

46 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Machine](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Machine)

47 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Machine_Emax](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Machine_Emax)

48 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Machine_Emin](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Machine_Emin)

49 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Machine_Mantissa](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Machine_Mantissa)

50 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Machine_Overflows](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Machine_Overflows)

• 'Machine_Radix[51](#part0310.xhtml__bookmark930)

• 'Machine_Rounding[52](#part0310.xhtml__bookmark931)  (Ada  2005)

• 'Machine_Rounds[53](#part0310.xhtml__bookmark932)

• 'Mantissa[54](#part0310.xhtml__bookmark933)  (Obsolescent)

• 'Max[55](#part0310.xhtml__bookmark934)

• 'Max_Aligment_For_Allocation[56](#part0310.xhtml__bookmark935)  (Ada  2012)

• 'Max_Size_In_Storage_Elements[57](#part0310.xhtml__bookmark936)

• 'Min[58](#part0310.xhtml__bookmark937)

• 'Mod[59](#part0310.xhtml__bookmark938)  (Ada  2005)

• 'Model[60](#part0310.xhtml__bookmark939)

• 'Model_Emin[61](#part0310.xhtml__bookmark940)

• 'Model_Epsilon[62](#part0310.xhtml__bookmark941)

• 'Model_Mantissa[63](#part0310.xhtml__bookmark942)

• 'Model_Small[64](#part0310.xhtml__bookmark943)

• 'Modulus[65](#part0310.xhtml__bookmark944)

38.2.6  O  −  R

• 'Old[66](#part0310.xhtml__bookmark945)  (Ada  2012)

• 'Output[67](#part0310.xhtml__bookmark946)

• 'Overlaps_Storage[68](#part0310.xhtml__bookmark947)  (Ada  2012)

• 'Partition_ID[69](#part0310.xhtml__bookmark948)

• 'Pos[70](#part0310.xhtml__bookmark949)

• 'Position[71](#part0310.xhtml__bookmark950)

• 'Pred[72](#part0310.xhtml__bookmark951)

• 'Priority[73](#part0310.xhtml__bookmark952)  (Ada  2005)

![](Images/image07329.jpeg)

51 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Machine_Radix](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Machine_Radix)

52 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Machine_Rounding](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Machine_Rounding)

53 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Machine_Rounds](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Machine_Rounds)

54 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Mantissa](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Mantissa)

55 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Max](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Max)

56 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Max_Aligment_For_](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Max_Aligment_For_Allocation)  [Allocation](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Max_Aligment_For_Allocation)

57 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Max_Size_In_Storage_](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Max_Size_In_Storage_Elements)

[Elements](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Max_Size_In_Storage_Elements)

58 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Min](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Min)

59 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Mod](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Mod)

60 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Model](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Model)

61 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Model_Emin](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Model_Emin)

62 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Model_Epsilon](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Model_Epsilon)

63 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Model_Mantissa](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Model_Mantissa)

64 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Model_Small](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Model_Small)

65 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Modulus](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Modulus)

66 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Old](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Old)

67 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Output](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Output)

68 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Overlaps_Storage](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Overlaps_Storage)

69 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Partition_ID](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Partition_ID)

70 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Pos](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Pos)

71 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Position](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Position)

72 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Pred](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Pred)

73 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Priority](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Priority)

• 'Range[74](#part0311.xhtml__bookmark953)

• 'Read[75](#part0311.xhtml__bookmark954)

• 'Remainder[76](#part0311.xhtml__bookmark955)

• 'Result[77](#part0311.xhtml__bookmark956)  (Ada  2012)

• 'Round[78](#part0311.xhtml__bookmark957)

• 'Rounding[79](#part0311.xhtml__bookmark958)

#### 38.2.7 S

• 'Safe_Emax[80](#part0311.xhtml__bookmark959)  (Obsolescent)

• 'Safe_First[81](#part0311.xhtml__bookmark960)

• 'Safe_Large[82](#part0311.xhtml__bookmark961)  (Obsolescent)

• 'Safe_Last[83](#part0311.xhtml__bookmark962)

• 'Safe_Small[84](#part0311.xhtml__bookmark963)  (Obsolescent)

• 'Scale[85](#part0311.xhtml__bookmark964)

• 'Scaling[86](#part0311.xhtml__bookmark965)

• 'Signed_Zeros[87](#part0311.xhtml__bookmark966)

• 'Size[88](#part0311.xhtml__bookmark967)

• 'Small[89](#part0311.xhtml__bookmark968)

• 'Storage_Pool[90](#part0311.xhtml__bookmark969)

• 'Storage_Size[91](#part0311.xhtml__bookmark970)

• 'Stream_Size[92](#part0311.xhtml__bookmark971)  (Ada  2005)

• 'Succ[93](#part0311.xhtml__bookmark972)

38.2.8 T  −  V

• 'Tag[94](#part0311.xhtml__bookmark973)

• 'Terminated[95](#part0311.xhtml__bookmark974)

![](Images/image07330.jpeg)

74 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Range](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Range)

75 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Read](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Read)

76 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Remainder](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Remainder)

77 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Result](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Result)

78 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Round](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Round)

79 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Rounding](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Rounding)

80 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Safe_Emax](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Safe_Emax)

81 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Safe_First](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Safe_First)

82 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Safe_Large](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Safe_Large)

83 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Safe_Last](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Safe_Last)

84 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Safe_Small](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Safe_Small)

85 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Scale](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Scale)

86 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Scaling](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Scaling)

87 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Signed_Zeros](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Signed_Zeros)

88 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Size](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Size)

89 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Small](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Small)

90 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Storage_Pool](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Storage_Pool)

91 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Storage_Size](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Storage_Size)

92 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Stream_Size](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Stream_Size)

93 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Succ](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Succ)

94 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Tag](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Tag)

95 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Terminated](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Terminated)

• 'Truncation[96](#part0312.xhtml__bookmark976)

• 'Unbiased_Rounding[97](#part0312.xhtml__bookmark977)

• 'Unchecked_Access[98](#part0312.xhtml__bookmark978)

• 'Val[99](#part0312.xhtml__bookmark979)

• 'Valid[100](#part0312.xhtml__bookmark980)

• 'Value[101](#part0312.xhtml__bookmark981)

• 'Version[102](#part0312.xhtml__bookmark982)

38.2.9  W  −  Z

• 'Wide_Image[103](#part0312.xhtml__bookmark983)

• 'Wide_Value[104](#part0312.xhtml__bookmark984)

• 'Wide_Wide_Image[105](#part0312.xhtml__bookmark985)  (Ada  2005)

• 'Wide_Wide_Value[106](#part0312.xhtml__bookmark986) (Ada  2005)

• 'Wide_Wide_Width[107](#part0312.xhtml__bookmark987)  (Ada  2005)

• 'Wide_Width[108](#part0312.xhtml__bookmark988)

• 'Width[109](#part0312.xhtml__bookmark989)

• 'Write[110](#part0312.xhtml__bookmark990)

## 38.3 List  of  implementation  defined  attributes

List  of  implementation  defined  attributes

The  following  attributes  are  not  available  in  all  Ada  compilers,  only  in  those  that  had  implemented  them.

Currently,  there  are  only  listed  the  implementation-defined  attributes  of  a  few  compilers.  You  can  help  Wikibooks  adding[111](#part0312.xhtml__bookmark991)  specific  attributes  of  other  compilers:

###### GNAT

Implementation-defined  attribute[112](#part0312.xhtml__bookmark992)  of  the GNAT[113](#part0312.xhtml__bookmark993)  compiler  from AdaCore/FSF.

###### HP  Ada

![](Images/image07331.jpeg)

96 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Truncation](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Truncation)

97 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Unbiased_Rounding](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Unbiased_Rounding)

98 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Unchecked_Access](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Unchecked_Access)

99 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Val](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Val)

100 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Valid](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Valid)

101 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Value](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Value)

102 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Version](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Version)

103 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Wide_Image](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Wide_Image)

104 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Wide_Value](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Wide_Value)

105 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Wide_Wide_Image](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Wide_Wide_Image)

106 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Wide_Wide_Value](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Wide_Wide_Value)

107 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Wide_Wide_Width](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Wide_Wide_Width)

108 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Wide_Width](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Wide_Width)

109 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Width](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Width)

110 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Write](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Write)

111 [http://en.wikibooks.org/w/index.php?title=Programming:Ada:Attributes&action=edit](http://en.wikibooks.org/w/index.php?title=Programming%3AAda%3AAttributes&action=edit)

112 [http://www.adacore.com/wp-content/files/auto_update/gnat-unw-docs/html/gnat_rm_3.html](http://www.adacore.com/wp-content/files/auto_update/gnat-unw-docs/html/gnat_rm_3.html)

113 [http://en.wikibooks.org/wiki/Ada%20Programming%2FGNAT](http://en.wikibooks.org/wiki/Ada%20Programming%2FGNAT)

Implementation-defined  attribute[114](#part0313.xhtml__bookmark994)  of  the  HP  Ada[115](#part0313.xhtml__bookmark995)  compiler  (formerly  known  as  "DEC  Ada").

###### ICC

Implementation-defined  attribute[116](#part0313.xhtml__bookmark996)  of  the  Irvine  ICC[117](#part0313.xhtml__bookmark997)  compiler.

###### PowerAda

Implementation-defined  attribute[118](#part0313.xhtml__bookmark998) of  OC  Systems'  PowerAda[119](#part0313.xhtml__bookmark999).

###### SPARCompiler

Implementation-defined  attribute[120](#part0313.xhtml__bookmark1000)  of  Sun's  SPARCompiler  Ada[121](#part0313.xhtml__bookmark1001).

38.3.1 A  −  D

• 'Abort_Signal[122](#part0313.xhtml__bookmark1002)  (GNAT)

• 'Address_Size[123](#part0313.xhtml__bookmark1003)  (GNAT)

• 'Architecture[124](#part0313.xhtml__bookmark1004)  (ICC)

• 'Asm_Input[125](#part0313.xhtml__bookmark1005)  (GNAT)

• 'Asm_Output[126](#part0313.xhtml__bookmark1006)  (GNAT)

• 'AST_Entry[127](#part0313.xhtml__bookmark1007) (GNAT,  HP  Ada)

• 'Bit[128](#part0313.xhtml__bookmark1008)  (GNAT,  HP  Ada)

• 'Bit_Position[129](#part0313.xhtml__bookmark1009)  (GNAT)

• 'CG_Mode[130](#part0313.xhtml__bookmark1010)  (ICC)

• 'Code_Address[131](#part0313.xhtml__bookmark1011)  (GNAT)

• 'Compiler_Key[132](#part0313.xhtml__bookmark1012)  (SPARCompiler)

• 'Compiler_Version[133](#part0313.xhtml__bookmark1013)  (SPARCompiler)

• 'Declared[134](#part0313.xhtml__bookmark1014)  (ICC)

• 'Default_Bit_Order[135](#part0313.xhtml__bookmark1015)  (GNAT)

• 'Dope_Address[136](#part0313.xhtml__bookmark1016) (SPARCompiler)

![](Images/image07332.jpeg)

114 [http://h71000.www7.hp.com/commercial/ada/ada_lrm.pdf](http://h71000.www7.hp.com/commercial/ada/ada_lrm.pdf)

115 [http://h71000.www7.hp.com/commercial/ada/ada_index.html](http://h71000.www7.hp.com/commercial/ada/ada_index.html)

116 "4.2  ICC-Defined  Attributes",  ICC  Ada  Implementation  Reference  —  ICC  Ada  Version  8.2.5  for  i960MC  Targets,  document  version  2.11.4[http://www.irvine.com/support/general/](http://www.irvine.com/support/general/)

117 [http://www.irvine.com/products.html](http://www.irvine.com/products.html)

118 [http://www.ocsystems.com/user_guide/powerada/html/powerada-117.html#HEADING117-0](http://www.ocsystems.com/user_guide/powerada/html/powerada-117.html#HEADING117-0)

119 [http://www.ocsystems.com/prod_powerada.html](http://www.ocsystems.com/prod_powerada.html)

120 [http://docs.sun.com/app/docs/doc/802-3641/6i7h8si5i?a=view#F.](http://docs.sun.com/app/docs/doc/802-3641/6i7h8si5i?a=view&F.Implementation-Dependent_Characteristi-30)  [Implementation-Dependent_Characteristi-30](http://docs.sun.com/app/docs/doc/802-3641/6i7h8si5i?a=view&F.Implementation-Dependent_Characteristi-30)

121 [http://docs.sun.com/app/docs/coll/15.4](http://docs.sun.com/app/docs/coll/15.4)

122 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Abort_Signal](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Abort_Signal)

123 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Address_Size](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Address_Size)

124 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Architecture](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Architecture)

125 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Asm_Input](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Asm_Input)

126 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Asm_Output](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Asm_Output)

127 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27AST_Entry](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27AST_Entry)

128 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Bit](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Bit)

129 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Bit_Position](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Bit_Position)

130 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27CG_Mode](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27CG_Mode)

131 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Code_Address](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Code_Address)

132 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Compiler_Key](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Compiler_Key)

133 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Compiler_Version](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Compiler_Version)

134 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Declared](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Declared)

135 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Default_Bit_Order](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Default_Bit_Order)

136 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Dope_Address](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Dope_Address)

• 'Dope_Size[137](#part0314.xhtml__bookmark1017)  (SPARCompiler)

38.3.2  E  −  H

• 'Elaborated[138](#part0314.xhtml__bookmark1018)  (GNAT)

• 'Elab_Body[139](#part0314.xhtml__bookmark1019)  (GNAT)

• 'Elab_Spec[140](#part0314.xhtml__bookmark1020)  (GNAT)

• 'Emax[141](#part0314.xhtml__bookmark1021)  (GNAT)

• 'Enabled[142](#part0314.xhtml__bookmark1022)  (GNAT)

• 'Entry_Number[143](#part0314.xhtml__bookmark1023)  (SPARCompiler)

• 'Enum_Rep[144](#part0314.xhtml__bookmark1024)  (GNAT)

• 'Enum_Val[145](#part0314.xhtml__bookmark1025)  (GNAT)

• 'Epsilon[146](#part0314.xhtml__bookmark1026)  (GNAT)

• 'Exception_Address[147](#part0314.xhtml__bookmark1027)  (ICC)

• 'Extended_Aft[148](#part0314.xhtml__bookmark1028) (PowerAda)

• 'Extended_Base[149](#part0314.xhtml__bookmark1029)  (PowerAda)

• 'Extended_Digits[150](#part0314.xhtml__bookmark1030)  (PowerAda)

• 'Extended_Fore[151](#part0314.xhtml__bookmark1031)  (PowerAda)

• 'Extended_Image[152](#part0314.xhtml__bookmark1032)  (PowerAda)

• 'Extended_Value[153](#part0314.xhtml__bookmark1033)  (PowerAda)

• 'Extended_Width[154](#part0314.xhtml__bookmark1034)  (PowerAda)

• 'Extended_Wide_Image[155](#part0314.xhtml__bookmark1035)  (PowerAda)

• 'Extended_Wide_Value[156](#part0314.xhtml__bookmark1036)  (PowerAda)

• 'Extended_Wide_Width[157](#part0314.xhtml__bookmark1037)  (PowerAda)

• 'Fixed_Value[158](#part0314.xhtml__bookmark1038)  (GNAT)

• 'Has_Access_Values[159](#part0314.xhtml__bookmark1039)  (GNAT)

• 'Has_Discriminants[160](#part0314.xhtml__bookmark1040)  (GNAT)

![](Images/image07333.jpeg)

137 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Dope_Size](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Dope_Size)

138 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Elaborated](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Elaborated)

139 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Elab_Body](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Elab_Body)

140 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Elab_Spec](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Elab_Spec)

141 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Emax](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Emax)

142 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Enabled](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Enabled)

143 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Entry_Number](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Entry_Number)

144 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Enum_Rep](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Enum_Rep)

145 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Enum_Val](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Enum_Val)

146 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Epsilon](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Epsilon)

147 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Exception_Address](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Exception_Address)

148 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Extended_Aft](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Extended_Aft)

149 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Extended_Base](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Extended_Base)

150 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Extended_Digits](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Extended_Digits)

151 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Extended_Fore](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Extended_Fore)

152 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Extended_Image](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Extended_Image)

153 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Extended_Value](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Extended_Value)

154 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Extended_Width](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Extended_Width)

155 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Extended_Wide_Image](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Extended_Wide_Image)

156 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Extended_Wide_Value](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Extended_Wide_Value)

157 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Extended_Wide_Width](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Extended_Wide_Width)

158 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Fixed_Value](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Fixed_Value)

159 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Has_Access_Values](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Has_Access_Values)

160 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Has_Discriminants](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Has_Discriminants)

• 'High_Word[161](#part0315.xhtml__bookmark1041)  (ICC)

• 'Homogeneous[162](#part0315.xhtml__bookmark1042)  (SPARCompiler)

38.3.3 I  −  N

• 'Img[163](#part0315.xhtml__bookmark1043)  (GNAT)

• 'Integer_Value[164](#part0315.xhtml__bookmark1044)  (GNAT)

• 'Invalid_Value[165](#part0315.xhtml__bookmark1045)  (GNAT)

• 'Linear_Address[166](#part0315.xhtml__bookmark1046)  (ICC)

• 'Low_Word[167](#part0315.xhtml__bookmark1047)  (ICC)

• 'Machine_Size[168](#part0315.xhtml__bookmark1048)  (GNAT,  HP  Ada)

• 'Max_Interrupt_Priority[169](#part0315.xhtml__bookmark1049)  (GNAT)

• 'Max_Priority[170](#part0315.xhtml__bookmark1050)  (GNAT)

• 'Maximum_Alignment[171](#part0315.xhtml__bookmark1051)  (GNAT)

• 'Mechanism_Code[172](#part0315.xhtml__bookmark1052)  (GNAT)

• 'Null_Parameter[173](#part0315.xhtml__bookmark1053)  (GNAT,  HP  Ada)

38.3.4 O  −  T

• 'Object_Size[174](#part0315.xhtml__bookmark1054)  (GNAT)

• 'Old[175](#part0315.xhtml__bookmark1055)  (GNAT)

• 'Passed_By_Reference[176](#part0315.xhtml__bookmark1056)  (GNAT)

• 'Pool_Address[177](#part0315.xhtml__bookmark1057)  (GNAT)

• 'Range_Length[178](#part0315.xhtml__bookmark1058)  (GNAT)

• 'Ref[179](#part0315.xhtml__bookmark1059)  (SPARCompiler)

• 'Storage_Unit[180](#part0315.xhtml__bookmark1060)  (GNAT)

• 'Stub_Type[181](#part0315.xhtml__bookmark1061)  (GNAT)

• 'Target[182](#part0315.xhtml__bookmark1062)  (ICC)

![](Images/image07334.jpeg)

161 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27High_Word](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27High_Word)

162 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Homogeneous](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Homogeneous)

163 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Img](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Img)

164 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Integer_Value](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Integer_Value)

165 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Invalid_Value](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Invalid_Value)

166 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Linear_Address](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Linear_Address)

167 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Low_Word](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Low_Word)

168 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Machine_Size](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Machine_Size)

169 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Max_Interrupt_](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Max_Interrupt_Priority)  [Priority](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Max_Interrupt_Priority)

170 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Max_Priority](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Max_Priority)

171 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Maximum_Alignment](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Maximum_Alignment)

172 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Mechanism_Code](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Mechanism_Code)

173 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Null_Parameter](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Null_Parameter)

174 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Object_Size](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Object_Size)

175 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Old](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Old)

176 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Passed_By_Reference](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Passed_By_Reference)

177 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Pool_Address](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Pool_Address)

178 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Range_Length](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Range_Length)

179 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Ref](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Ref)

180 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Storage_Unit](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Storage_Unit)

181 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Stub_Type](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Stub_Type)

182 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Target](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Target)

• 'Target_Name[183](#part0316.xhtml__bookmark1064)  (GNAT)

• 'Task_ID[184](#part0316.xhtml__bookmark1065)  (SPARCompiler)

• 'Tick[185](#part0316.xhtml__bookmark1066)  (GNAT)

• 'To_Address[186](#part0316.xhtml__bookmark1067)  (GNAT)

• 'Type_Class[187](#part0316.xhtml__bookmark1068)  (GNAT,  HP  Ada)

• 'Type_Key[188](#part0316.xhtml__bookmark1069) (SPARCompiler)

38.3.5  U  −  Z

• 'UET_Address[189](#part0316.xhtml__bookmark1070)  (GNAT)

• 'Unconstrained_Array[190](#part0316.xhtml__bookmark1071)  (GNAT)

• 'Universal_Literal_String[191](#part0316.xhtml__bookmark1072)  (GNAT)

• 'Unrestricted_Access[192](#part0316.xhtml__bookmark1073)  (GNAT,  ICC)

• 'VADS_Size[193](#part0316.xhtml__bookmark1074)  (GNAT)

• 'Value_Size[194](#part0316.xhtml__bookmark1075)  (GNAT)

• 'Wchar_T_Size[195](#part0316.xhtml__bookmark1076)  (GNAT)

• 'Word_Size[196](#part0316.xhtml__bookmark1077)  (GNAT)

## 38.4 See  also

See  also

#### 38.4.1  Wikibook

• Ada  Programming[197](#part0316.xhtml__bookmark1078)

• Ada  Programming/Aspects[198](#part0316.xhtml__bookmark1079)

• Ada  Programming/Pragmas[199](#part0316.xhtml__bookmark1080)

• Ada  Programming/Keywords[200](#part0316.xhtml__bookmark1081)

![](Images/image07335.jpeg)

183 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Target_Name](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Target_Name)

184 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Task_ID](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Task_ID)

185 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Tick](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Tick)

186 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27To_Address](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27To_Address)

187 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Type_Class](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Type_Class)

188 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Type_Key](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Type_Key)

189 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27UET_Address](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27UET_Address)

190 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Unconstrained_Array](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Unconstrained_Array)

191 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Universal_Literal_](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Universal_Literal_String)  [String](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Universal_Literal_String)

192 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Unrestricted_Access](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Unrestricted_Access)

193 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27VADS_Size](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27VADS_Size)

194 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Value_Size](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Value_Size)

195 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Wchar_T_Size](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Wchar_T_Size)

196 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Word_Size](http://en.wikibooks.org/wiki/Ada%20Programming%2FAttributes%2F%27Word_Size)

197 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

198 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAspects](http://en.wikibooks.org/wiki/Ada%20Programming%2FAspects)

199 Chapter  [39](#part0319.xhtml__bookmark1089)  on  page  [317](#part0319.xhtml__bookmark1089)

200 Chapter  [35](#part0295.xhtml__bookmark761)  on  page  [293](#part0295.xhtml__bookmark761)

#### 38.4.2 Ada  Reference  Manual

###### Ada  83

• Annex  4:  Attributes  ˆ{[http://archive.adaic.com/standards/83lrm/html/lrm-](http://archive.adaic.com/standards/83lrm/html/lrm-4.html)4.  [html}](http://archive.adaic.com/standards/83lrm/html/lrm-4.html)

• AnnexA:PredefinedLanguageAttributesˆ{[http://archive.adaic.com/](http://archive.adaic.com/standards/83lrm/html/lrm-A.html)  [standards/83lrm/html/lrm-A.html}](http://archive.adaic.com/standards/83lrm/html/lrm-A.html)

###### Ada  95

• 4.1  Attributes[201](#part0317.xhtml__bookmark1083)

• Annex  K:  (informative)  Language-Defined  Attributes[202](#part0317.xhtml__bookmark1084)

###### Ada  2005

• 4.1  Attributes[203](#part0317.xhtml__bookmark1085)

• Annex  K:  (informative)  Language-Defined  Attributes[204](#part0317.xhtml__bookmark1086)

###### Ada  2012

• 4.1  Attributes[205](#part0317.xhtml__bookmark1087)

• Annex  K:  (informative)  Language-Defined  Attributes[206](#part0317.xhtml__bookmark1088)

## 38.5 References

References

![](Images/image07336.jpeg)

201 [http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-4-1.html](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-4-1.html)

202 [http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-K.html](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-K.html)

203 [http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-4-1.html](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-4-1.html)

204 [http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-K.html](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-K.html)

205 [http://www.ada-auth.org/standards/12rm/html/RM-4-1.html](http://www.ada-auth.org/standards/12rm/html/RM-4-1.html)

206 [http://www.ada-auth.org/standards/12rm/html/RM-K.html](http://www.ada-auth.org/standards/12rm/html/RM-K.html)

# 39 Pragmas

## 39.1 Description

Description

Pragmas[1](#part0319.xhtml__bookmark1092) control  the  compiler, i.e.  they  are  compiler  directives[2](#part0319.xhtml__bookmark1093).  They  have  the  standard  form  of

![](Images/image07337.jpeg)

where  the  parameter  list  is  optional.

## 39.2 List  of  language  defined  pragmas

List  of  language  defined  pragmas

Some  pragmas  are  specially  marked:

###### Ada  2005

This  is  a  new  Ada  2005[3](#part0319.xhtml__bookmark1094)  pragma.

###### Ada  2012

This  is  a  new  Ada  2012[4](#part0319.xhtml__bookmark1095)  pragma.

###### Obsolescent

This  is  a  deprecated  pragma  and  it  should  not  be  used  in  new  code.

39.2.1 A  −  H

• All_Calls_Remote[5](#part0319.xhtml__bookmark1096)

• Assert[6](#part0319.xhtml__bookmark1097)  (Ada  2005)

• Assertion_Policy[7](#part0319.xhtml__bookmark1098)  (Ada  2005)

• Asynchronous[8](#part0319.xhtml__bookmark1099)  (Obsolescent  since  Ada  2012)

• Atomic[9](#part0319.xhtml__bookmark1100)  (Obsolescent  since  Ada  2012)

• Atomic_Components[10](#part0319.xhtml__bookmark1101)  (Obsolescent  since  Ada  2012)

• Attach_Handler[11](#part0319.xhtml__bookmark1102)  (Obsolescent  since  Ada  2012)

![](Images/image07338.jpeg)

1 Chapter  [39](#part0319.xhtml__bookmark1089)  on  page  [317](#part0319.xhtml__bookmark1089)

2 [http://en.wikipedia.org/wiki/Compiler%20directive](http://en.wikipedia.org/wiki/Compiler%20directive)

3 Chapter  [23](#part0221.xhtml__bookmark541)  on  page  [219](#part0221.xhtml__bookmark541)

4 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAda%202012](http://en.wikibooks.org/wiki/Ada%20Programming%2FAda%202012)

5 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAll_Calls_Remote](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAll_Calls_Remote)

6 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAssert](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAssert)

7 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAssertion_Policy](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAssertion_Policy)

8 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAsynchronous](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAsynchronous)

9 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAtomic](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAtomic)

10 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAtomic_Components](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAtomic_Components)

11 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAttach_Handler](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAttach_Handler)

• Controlled[12](#part0320.xhtml__bookmark1103)

• Convention[13](#part0320.xhtml__bookmark1104)  (Obsolescent  since  Ada  2012)

• CPU[14](#part0320.xhtml__bookmark1105)  (Ada  2012)

• Default_Storage_Pool[15](#part0320.xhtml__bookmark1106)  (Ada  2012)

• Detect_Blocking[16](#part0320.xhtml__bookmark1107)  (Ada  2005)

• Discard_Names[17](#part0320.xhtml__bookmark1108)

• Dispatching_Domain[18](#part0320.xhtml__bookmark1109)  (Ada  2012)

• Elaborate[19](#part0320.xhtml__bookmark1110)

• Elaborate_All[20](#part0320.xhtml__bookmark1111)

• Elaborate_Body[21](#part0320.xhtml__bookmark1112)

• Export[22](#part0320.xhtml__bookmark1113)  (Obsolescent  since  Ada  2012)

39.2.2  I  −  O

• Import[23](#part0320.xhtml__bookmark1114)  (Obsolescent  since  Ada  2012)

• Independent[24](#part0320.xhtml__bookmark1115)  (Ada  2012)

• Independent_Component[25](#part0320.xhtml__bookmark1116)  (Ada  2012)

• Inline[26](#part0320.xhtml__bookmark1117)  (Obsolescent  since  Ada  2012)

• Inspection_Point[27](#part0320.xhtml__bookmark1118)

• Interface[28](#part0320.xhtml__bookmark1119)  (Obsolescent)

• Interrupt_Handler[29](#part0320.xhtml__bookmark1120)  (Obsolescent  since  Ada  2012)

• Interrupt_Priority[30](#part0320.xhtml__bookmark1121)   (Obsolescent  since  Ada  2012)

• Linker_Options[31](#part0320.xhtml__bookmark1122)

• List[32](#part0320.xhtml__bookmark1123)

• Locking_Policy[33](#part0320.xhtml__bookmark1124)

• Memory_Size[34](#part0320.xhtml__bookmark1125)  (Obsolescent)

• No_Return[35](#part0320.xhtml__bookmark1126)  (Ada  2005)  (Obsolescent  since  Ada  2012)

![](Images/image07339.jpeg)

12 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FControlled](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FControlled)

13 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FConvention](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FConvention)

14 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCPU](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCPU)

15 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FDefault_Storage_Pool](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FDefault_Storage_Pool)

16 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FDetect_Blocking](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FDetect_Blocking)

17 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FDiscard_Names](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FDiscard_Names)

18 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FDispatching_Domain](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FDispatching_Domain)

19 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FElaborate](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FElaborate)

20 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FElaborate_All](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FElaborate_All)

21 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FElaborate_Body](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FElaborate_Body)

22 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExport](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExport)

23 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FImport](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FImport)

24 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FIndependent](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FIndependent)

25 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FIndependent_Component](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FIndependent_Component)

26 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInline](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInline)

27 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInspection_Point](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInspection_Point)

28 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInterface](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInterface)

29 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInterrupt_Handler](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInterrupt_Handler)

30 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInterrupt_Priority](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInterrupt_Priority)

31 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FLinker_Options](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FLinker_Options)

32 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FList](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FList)

33 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FLocking_Policy](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FLocking_Policy)

34 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FMemory_Size](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FMemory_Size)

35 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FNo_Return](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FNo_Return)

• Normalize_Scalars[36](#part0321.xhtml__bookmark1127)

• Optimize[37](#part0321.xhtml__bookmark1128)

39.2.3 P  −  R

• Pack[38](#part0321.xhtml__bookmark1129)  (Obsolescent  since  Ada  2012)

• Page[39](#part0321.xhtml__bookmark1130)

• Partition_Elaboration_Policy[40](#part0321.xhtml__bookmark1131)  (Ada  2005)

• Preelaborable_Initialization[41](#part0321.xhtml__bookmark1132)  (Ada  2005)

• Preelaborate[42](#part0321.xhtml__bookmark1133)

• Priority[43](#part0321.xhtml__bookmark1134)  (Obsolescent  since  Ada  2012)

• Priority_Specific_Dispatching[44](#part0321.xhtml__bookmark1135)  (Ada  2005)

• Profile[45](#part0321.xhtml__bookmark1136)  (Ada  2005)

• Pure[46](#part0321.xhtml__bookmark1137)

• Queueing_Policy[47](#part0321.xhtml__bookmark1138)

• Relative_Deadline[48](#part0321.xhtml__bookmark1139)  (Ada  2005)

• Remote_Call_Interface[49](#part0321.xhtml__bookmark1140)

• Remote_Types[50](#part0321.xhtml__bookmark1141)

• Restrictions[51](#part0321.xhtml__bookmark1142)

• Reviewable[52](#part0321.xhtml__bookmark1143)

39.2.4 S  −  Z

• Shared[53](#part0321.xhtml__bookmark1144)  (Obsolescent)

• Shared_Passive[54](#part0321.xhtml__bookmark1145)

• Storage_Size[55](#part0321.xhtml__bookmark1146)

• Storage_Unit[56](#part0321.xhtml__bookmark1147)  (Obsolescent)

• Suppress[57](#part0321.xhtml__bookmark1148)

![](Images/image07340.jpeg)

36 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FNormalize_Scalars](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FNormalize_Scalars)

37 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FOptimize](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FOptimize)

38 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPack](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPack)

39 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPage](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPage)

40 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPartition_Elaboration_](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPartition_Elaboration_Policy)  [Policy](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPartition_Elaboration_Policy)

41 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPreelaborable_](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPreelaborable_Initialization)

[Initialization](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPreelaborable_Initialization)

42 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPreelaborate](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPreelaborate)

43 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPriority](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPriority)

44 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPriority_Specific_](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPriority_Specific_Dispatching)  [Dispatching](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPriority_Specific_Dispatching)

45 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FProfile](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FProfile)

46 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPure](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPure)

47 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FQueueing_Policy](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FQueueing_Policy)

48 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FRelative_Deadline](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FRelative_Deadline)

49 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FRemote_Call_Interface](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FRemote_Call_Interface)

50 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FRemote_Types](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FRemote_Types)

51 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FRestrictions](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FRestrictions)

52 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FReviewable](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FReviewable)

53 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FShared](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FShared)

54 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FShared_Passive](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FShared_Passive)

55 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FStorage_Size](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FStorage_Size)

56 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FStorage_Unit](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FStorage_Unit)

57 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSuppress](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSuppress)

• System_Name[58](#part0322.xhtml__bookmark1150)  (Obsolescent)

• Task_Dispatching_Policy[59](#part0322.xhtml__bookmark1151)

• Unchecked_Union[60](#part0322.xhtml__bookmark1152) (Ada  2005)

• Unsuppress[61](#part0322.xhtml__bookmark1153)  (Ada  2005)

• Volatile[62](#part0322.xhtml__bookmark1154)

• Volatile_Components[63](#part0322.xhtml__bookmark1155)

## 39.3 List  of  implementation  defined  pragmas

List  of  implementation  defined  pragmas

The  following  pragmas  are  not  available  in  all  Ada  compilers,  only  in  those  that  had  implemented  them.

Currently,  there  are  only  listed  the  implementation-defined  pragmas  of  a  few  compilers.  You  can  help  Wikibooks  adding[64](#part0322.xhtml__bookmark1156)  specific  aspects  of  other  compilers:

###### GNAT

Implementation  defined pragma[65](#part0322.xhtml__bookmark1157)  of  the GNAT[66](#part0322.xhtml__bookmark1158)  compiler from  AdaCore and  FSF.

###### HP  Ada

Implementation  defined  pragma[67](#part0322.xhtml__bookmark1159)  of  the  HP  Ada[68](#part0322.xhtml__bookmark1160)  compiler  (formerly  known  as  "DEC  Ada").

###### ICC

Implementation-defined  pragma[69](#part0322.xhtml__bookmark1161) of  the  Irvine  ICC[70](#part0322.xhtml__bookmark1162)  compiler.

###### PowerAda

Implementation  defined  pragma[71](#part0322.xhtml__bookmark1163)  of  OC  Systems'  PowerAda[72](#part0322.xhtml__bookmark1164).

###### SPARCompiler

Implementationdefinedpragma[73](#part0322.xhtml__bookmark1165)ofSun'sSPARCompiler              Ada[74](#part0322.xhtml__bookmark1166).[http://](http://findarticles.com/p/articles/mi_m0EIN/is_1994_Nov_2/ai_15882197)  [findarticles.com/p/articles/mi_m0EIN/is_1994_Nov_2/ai_15882197](http://findarticles.com/p/articles/mi_m0EIN/is_1994_Nov_2/ai_15882197)

39.3.1  A  −  C

• Abort_Defer[75](#part0322.xhtml__bookmark1167)  (GNAT)

![](Images/image07341.jpeg)

58 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSystem_Name](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSystem_Name)

59 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FTask_Dispatching_Policy](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FTask_Dispatching_Policy)

60 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FUnchecked_Union](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FUnchecked_Union)

61 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FUnsuppress](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FUnsuppress)

62 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FVolatile](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FVolatile)

63 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FVolatile_Components](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FVolatile_Components)

64 http://en.wikibooks.org/w/index.php?title=Ada_Programming/Pragmas&action=edit

65 [http://www.adacore.com/wp-content/files/auto_update/gnat-unw-docs/html/gnat_rm_2.html](http://www.adacore.com/wp-content/files/auto_update/gnat-unw-docs/html/gnat_rm_2.html)

66 [http://en.wikibooks.org/wiki/Ada%20Programming%2FGNAT](http://en.wikibooks.org/wiki/Ada%20Programming%2FGNAT)

67 [http://h71000.www7.hp.com/commercial/ada/ada_lrm.pdf](http://h71000.www7.hp.com/commercial/ada/ada_lrm.pdf)

68 [http://h71000.www7.hp.com/commercial/ada/ada_index.html](http://h71000.www7.hp.com/commercial/ada/ada_index.html)

69 "2.2  ICC-Defined  Pragmas",  ICC  Ada  Implementation  Reference  —  ICC  Ada  Version  8.2.5  for  i960MC  Targets,  document  version  2.11.4.[http://www.irvine.com/support/general/](http://www.irvine.com/support/general/)

70 [http://www.irvine.com/products.html](http://www.irvine.com/products.html)

71 [http://www.ocsystems.com/user_guide/powerada/html/powerada-106.html#HEADING106-0](http://www.ocsystems.com/user_guide/powerada/html/powerada-106.html#HEADING106-0)

72 [http://www.ocsystems.com/prod_powerada.html](http://www.ocsystems.com/prod_powerada.html)

73 [http://docs.sun.com/app/docs/doc/802-3641/6i7h8si5i?a=view#F.](http://docs.sun.com/app/docs/doc/802-3641/6i7h8si5i?a=view&F.Implementation-Dependent_Characteristi-2)  [Implementation-Dependent_Characteristi-2](http://docs.sun.com/app/docs/doc/802-3641/6i7h8si5i?a=view&F.Implementation-Dependent_Characteristi-2)

74 [http://docs.sun.com/app/docs/coll/15.4](http://docs.sun.com/app/docs/coll/15.4)

75 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAbort_Defer](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAbort_Defer)

• Ada_83[76](#part0323.xhtml__bookmark1168)  (GNAT)

• Ada_95[77](#part0323.xhtml__bookmark1169)  (GNAT)

• Ada_05[78](#part0323.xhtml__bookmark1170)  (GNAT)

• Ada_2005[79](#part0323.xhtml__bookmark1171)  (GNAT)

• Ada_12[80](#part0323.xhtml__bookmark1172)  (GNAT)

• Ada_2012[81](#part0323.xhtml__bookmark1173)  (GNAT)

• Annotate[82](#part0323.xhtml__bookmark1174)  (GNAT)

• Assume_No_Invalid_Values[83](#part0323.xhtml__bookmark1175)  (GNAT)

• Ast_Entry[84](#part0323.xhtml__bookmark1176)  (GNAT,  HP  Ada)

• Bit_Pack[85](#part0323.xhtml__bookmark1177)  (SPARCompiler)

• Built_In[86](#part0323.xhtml__bookmark1178)  (SPARCompiler)

• Byte_Pack[87](#part0323.xhtml__bookmark1179)  (SPARCompiler)

• C_Pass_By_Copy[88](#part0323.xhtml__bookmark1180)  (GNAT)

• Call_Mechanism[89](#part0323.xhtml__bookmark1181)  (ICC)

• Canonical_Streams[90](#part0323.xhtml__bookmark1182)  (GNAT)

• Check[91](#part0323.xhtml__bookmark1183)  (GNAT)

• Check_Name[92](#part0323.xhtml__bookmark1184)  (GNAT)

• Check_Policy[93](#part0323.xhtml__bookmark1185)  (GNAT)

• CM_Info[94](#part0323.xhtml__bookmark1186)  (PowerAda)

• Comment[95](#part0323.xhtml__bookmark1187)  (GNAT)

• Common_Object[96](#part0323.xhtml__bookmark1188)  (GNAT,  HP  Ada)

• Compatible_Calls[97](#part0323.xhtml__bookmark1189)  (ICC)

• Compile_Time_Error[98](#part0323.xhtml__bookmark1190)  (GNAT)

• Compile_Time_Warning[99](#part0323.xhtml__bookmark1191)  (GNAT)

• Complete_Representation[100](#part0323.xhtml__bookmark1192)  (GNAT)

![](Images/image07342.jpeg)

76 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAda_83](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAda_83)

77 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAda_95](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAda_95)

78 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAda_05](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAda_05)

79 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAda_2005](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAda_2005)

80 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAda_12](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAda_12)

81 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAda_2012](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAda_2012)

82 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAnnotate](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAnnotate)

83 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAssume_No_Invalid_Values](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAssume_No_Invalid_Values)

84 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAst_Entry](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FAst_Entry)

85 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FBit_Pack](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FBit_Pack)

86 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FBuilt_In](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FBuilt_In)

87 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FByte_Pack](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FByte_Pack)

88 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FC_Pass_By_Copy](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FC_Pass_By_Copy)

89 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCall_Mechanism](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCall_Mechanism)

90 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCanonical_Streams](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCanonical_Streams)

91 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCheck](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCheck)

92 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCheck_Name](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCheck_Name)

93 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCheck_Policy](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCheck_Policy)

94 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCM_Info](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCM_Info)

95 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FComment](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FComment)

96 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCommon_Object](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCommon_Object)

97 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCompatible_Calls](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCompatible_Calls)

98 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCompile_Time_Error](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCompile_Time_Error)

99 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCompile_Time_Warning](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCompile_Time_Warning)

100 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FComplete_Representation](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FComplete_Representation)

• Complex_Representation[101](#part0324.xhtml__bookmark1193)  (GNAT)

• Component_Alignment[102](#part0324.xhtml__bookmark1194)  (GNAT,  HP  Ada)

• Compress[103](#part0324.xhtml__bookmark1195)  (ICC)

• Constrain_Private[104](#part0324.xhtml__bookmark1196)  (ICC)

• Convention_Identifier[105](#part0324.xhtml__bookmark1197)  (GNAT)

• CPP_Class[106](#part0324.xhtml__bookmark1198)  (GNAT)

• CPP_Constructor[107](#part0324.xhtml__bookmark1199)  (GNAT)

• CPP_Virtual[108](#part0324.xhtml__bookmark1200)  (GNAT)

• CPP_Vtable[109](#part0324.xhtml__bookmark1201)  (GNAT)

39.3.2  D  −  H

• Data_Mechanism[110](#part0324.xhtml__bookmark1202)  (ICC)

• Debug[111](#part0324.xhtml__bookmark1203)  (GNAT)

• Debug_Policy[112](#part0324.xhtml__bookmark1204)  (GNAT)

• Delete_Subprogram_Entry[113](#part0324.xhtml__bookmark1205)  (ICC)

• Elaboration_Checks[114](#part0324.xhtml__bookmark1206)  (GNAT)

• Eliminate[115](#part0324.xhtml__bookmark1207)  (GNAT)

• Error[116](#part0324.xhtml__bookmark1208)  (SPARCompiler)

• Export_Exception[117](#part0324.xhtml__bookmark1209)  (GNAT,  HP  Ada)

• Export_Function[118](#part0324.xhtml__bookmark1210)  (GNAT,  HP  Ada,  SPARCompiler)

• Export_Mechanism[119](#part0324.xhtml__bookmark1211)  (ICC)

• Export_Object[120](#part0324.xhtml__bookmark1212)  (GNAT,  HP  Ada,  SPARCompiler)

• Export_Procedure[121](#part0324.xhtml__bookmark1213)  (GNAT,  HP  Ada,  SPARCompiler)

• Export_Value[122](#part0324.xhtml__bookmark1214)  (GNAT)

• Export_Valued_Procedure[123](#part0324.xhtml__bookmark1215)  (GNAT,  HP  Ada)

• Extend_System[124](#part0324.xhtml__bookmark1216)  (GNAT)

![](Images/image07343.jpeg)

101 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FComplex_Representation](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FComplex_Representation)

102 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FComponent_Alignment](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FComponent_Alignment)

103 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCompress](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCompress)

104 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FConstrain_Private](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FConstrain_Private)

105 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FConvention_Identifier](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FConvention_Identifier)

106 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCPP_Class](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCPP_Class)

107 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCPP_Constructor](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCPP_Constructor)

108 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCPP_Virtual](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCPP_Virtual)

109 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCPP_Vtable](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FCPP_Vtable)

110 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FData_Mechanism](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FData_Mechanism)

111 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FDebug](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FDebug)

112 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FDebug_Policy](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FDebug_Policy)

113 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FDelete_Subprogram_Entry](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FDelete_Subprogram_Entry)

114 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FElaboration_Checks](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FElaboration_Checks)

115 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FEliminate](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FEliminate)

116 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FError](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FError)

117 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExport_Exception](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExport_Exception)

118 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExport_Function](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExport_Function)

119 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExport_Mechanism](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExport_Mechanism)

120 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExport_Object](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExport_Object)

121 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExport_Procedure](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExport_Procedure)

122 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExport_Value](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExport_Value)

123 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExport_Valued_Procedure](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExport_Valued_Procedure)

124 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExtend_System](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExtend_System)

• Extensions_Allowed[125](#part0325.xhtml__bookmark1217) (GNAT)

• External[126](#part0325.xhtml__bookmark1218)  (GNAT,  SPARCompiler)

• External_Name[127](#part0325.xhtml__bookmark1219)  (ICC,  SPARCompiler)

• External_Name_Casing[128](#part0325.xhtml__bookmark1220)  (GNAT)

• Fast_Math[129](#part0325.xhtml__bookmark1221) (GNAT)

• Favor_Top_Level[130](#part0325.xhtml__bookmark1222)  (GNAT)

• Finalize_Storage_Only[131](#part0325.xhtml__bookmark1223)  (GNAT)

• Float_Representation[132](#part0325.xhtml__bookmark1224)  (GNAT,  HP  Ada)

• Foreign[133](#part0325.xhtml__bookmark1225)  (ICC)

• Generic_Mechanism[134](#part0325.xhtml__bookmark1226)  (ICC)

• Generic_Policy[135](#part0325.xhtml__bookmark1227)  (SPARCompiler)

39.3.3 I  −  L

• i960_Intrinsic[136](#part0325.xhtml__bookmark1228)  (ICC)

• Ident[137](#part0325.xhtml__bookmark1229)  (GNAT,  HP  Ada)

• Images[138](#part0325.xhtml__bookmark1230)  (PowerAda)

• Implemented[139](#part0325.xhtml__bookmark1231),  previously  named  'Implemented_By_Entry'  (GNAT)

• Implicit_Code[140](#part0325.xhtml__bookmark1232)  (SPARCompiler)

• Implicit_Packing[141](#part0325.xhtml__bookmark1233)  (GNAT)

• Import_Exception[142](#part0325.xhtml__bookmark1234)  (GNAT,  HP  Ada)

• Import_Function[143](#part0325.xhtml__bookmark1235)  (GNAT,  HP  Ada,  SPARCompiler)

• Import_Mechanism[144](#part0325.xhtml__bookmark1236) (ICC)

• Import_Object[145](#part0325.xhtml__bookmark1237)  (GNAT,  HP  Ada,  SPARCompiler)

• Import_Procedure[146](#part0325.xhtml__bookmark1238)  (GNAT,  HP  Ada,  SPARCompiler)

• Import_Valued_Procedure[147](#part0325.xhtml__bookmark1239)  (GNAT,  HP  Ada)

• Include[148](#part0325.xhtml__bookmark1240)  (SPARCompiler)

![](Images/image07344.jpeg)

125 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExtensions_Allowed](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExtensions_Allowed)

126 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExternal](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExternal)

127 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExternal_Name](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExternal_Name)

128 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExternal_Name_Casing](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FExternal_Name_Casing)

129 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FFast_Math](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FFast_Math)

130 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FFavor_Top_Level](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FFavor_Top_Level)

131 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FFinalize_Storage_Only](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FFinalize_Storage_Only)

132 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FFloat_Representation](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FFloat_Representation)

133 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FForeign](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FForeign)

134 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FGeneric_Mechanism](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FGeneric_Mechanism)

135 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FGeneric_Policy](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FGeneric_Policy)

136 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2Fi960_Intrinsic](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2Fi960_Intrinsic)

137 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FIdent](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FIdent)

138 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FImages](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FImages)

139 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FImplemented](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FImplemented)

140 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FImplicit_Code](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FImplicit_Code)

141 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FImplicit_Packing](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FImplicit_Packing)

142 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FImport_Exception](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FImport_Exception)

143 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FImport_Function](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FImport_Function)

144 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FImport_Mechanism](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FImport_Mechanism)

145 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FImport_Object](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FImport_Object)

146 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FImport_Procedure](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FImport_Procedure)

147 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FImport_Valued_Procedure](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FImport_Valued_Procedure)

148 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInclude](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInclude)

• Initialize[149](#part0326.xhtml__bookmark1241)  (SPARCompiler)

• Initialize_Scalars[150](#part0326.xhtml__bookmark1242)  (GNAT)

• Inline_Always[151](#part0326.xhtml__bookmark1243)  (GNAT)

• Inline_Generic[152](#part0326.xhtml__bookmark1244)  (GNAT,  HP  Ada)

• Inline_Only[153](#part0326.xhtml__bookmark1245)  (SPARCompiler)

• Instance_Policy[154](#part0326.xhtml__bookmark1246)  (SPARCompiler)

• Interface_Constant[155](#part0326.xhtml__bookmark1247)  (ICC)

• Interface_Information[156](#part0326.xhtml__bookmark1248)  (PowerAda)

• Interface_Mechanism[157](#part0326.xhtml__bookmark1249)  (ICC)

• Interface_Name[158](#part0326.xhtml__bookmark1250)  (GNAT,  HP  Ada,  ICC,  SPARCompiler)

• Interrupt_State[159](#part0326.xhtml__bookmark1251)  (GNAT)

• Invariant[160](#part0326.xhtml__bookmark1252)  (GNAT)

• Keep_Names[161](#part0326.xhtml__bookmark1253)  (GNAT)

• Label[162](#part0326.xhtml__bookmark1254)  (ICC)

• License[163](#part0326.xhtml__bookmark1255)  (GNAT)

• Link_With[164](#part0326.xhtml__bookmark1256)  (GNAT,  ICC,  SPARCompiler)

• Linker_Alias[165](#part0326.xhtml__bookmark1257)  (GNAT)

• Linker_Constructor[166](#part0326.xhtml__bookmark1258)  (GNAT)

• Linker_Destructor[167](#part0326.xhtml__bookmark1259)  (GNAT)

• Linker_Section[168](#part0326.xhtml__bookmark1260)  (GNAT)

• Long_Float[169](#part0326.xhtml__bookmark1261)  (GNAT:  OpenVMS,  HP  Ada)

39.3.4  M  −  P

• Machine_Attribute[170](#part0326.xhtml__bookmark1262)  (GNAT)

• Main[171](#part0326.xhtml__bookmark1263)  (GNAT)

• Main_Storage[172](#part0326.xhtml__bookmark1264)  (GNAT,  HP  Ada)

![](Images/image07345.jpeg)

149 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInitialize](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInitialize)

150 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInitialize_Scalars](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInitialize_Scalars)

151 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInline_Always](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInline_Always)

152 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInline_Generic](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInline_Generic)

153 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInline_Only](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInline_Only)

154 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInstance_Policy](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInstance_Policy)

155 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInterface_Constant](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInterface_Constant)

156 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInterface_Information](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInterface_Information)

157 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInterface_Mechanism](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInterface_Mechanism)

158 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInterface_Name](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInterface_Name)

159 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInterrupt_State](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInterrupt_State)

160 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInvariant](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FInvariant)

161 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FKeep_Names](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FKeep_Names)

162 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FLabel](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FLabel)

163 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FLicense](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FLicense)

164 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FLink_With](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FLink_With)

165 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FLinker_Alias](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FLinker_Alias)

166 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FLinker_Constructor](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FLinker_Constructor)

167 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FLinker_Destructor](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FLinker_Destructor)

168 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FLinker_Section](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FLinker_Section)

169 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FLong_Float](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FLong_Float)

170 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FMachine_Attribute](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FMachine_Attribute)

171 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FMain](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FMain)

172 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FMain_Storage](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FMain_Storage)

• No_Body[173](#part0327.xhtml__bookmark1265)  (GNAT)

• No_Image[174](#part0327.xhtml__bookmark1266)  (SPARCompiler)

• No_Strict_Aliasing[175](#part0327.xhtml__bookmark1267)  (GNAT)

• No_Suppress[176](#part0327.xhtml__bookmark1268)  (PowerAda)

• No_Reorder[177](#part0327.xhtml__bookmark1269)  (ICC)

• No_Zero[178](#part0327.xhtml__bookmark1270)  (ICC)

• Noinline[179](#part0327.xhtml__bookmark1271)  (ICC)

• Non_Reentrant[180](#part0327.xhtml__bookmark1272)  (SPARCompiler)

• Not_Elaborated[181](#part0327.xhtml__bookmark1273)  (SPARCompiler)

• Not_Null[182](#part0327.xhtml__bookmark1274)  (ICC)

• Obsolescent[183](#part0327.xhtml__bookmark1275)  (GNAT)

• Optimize_Alignment[184](#part0327.xhtml__bookmark1276)  (GNAT)

• Optimize_Code[185](#part0327.xhtml__bookmark1277)  (SPARCompiler)

• Optimize_Options[186](#part0327.xhtml__bookmark1278)  (ICC)

• Ordered[187](#part0327.xhtml__bookmark1279)  (GNAT)

• Parameter_Mechanism[188](#part0327.xhtml__bookmark1280)  (ICC)

• Passive[189](#part0327.xhtml__bookmark1281)  (GNAT,  HP  Ada,  SPARCompiler)

• Persistent_BSS[190](#part0327.xhtml__bookmark1282)  (GNAT)

• Physical_Address[191](#part0327.xhtml__bookmark1283)  (ICC)

• Polling[192](#part0327.xhtml__bookmark1284)  (GNAT)

• Postcondition[193](#part0327.xhtml__bookmark1285)  (GNAT)

• Precondition[194](#part0327.xhtml__bookmark1286)  (GNAT)

• Preserve_Layout[195](#part0327.xhtml__bookmark1287)  (PowerAda)

• Profile_Warnings[196](#part0327.xhtml__bookmark1288)  (GNAT)

• Propagate_Exceptions[197](#part0327.xhtml__bookmark1289)  (GNAT)

![](Images/image07346.jpeg)

173 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FNo_Body](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FNo_Body)

174 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FNo_Image](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FNo_Image)

175 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FNo_Strict_Aliasing](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FNo_Strict_Aliasing)

176 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FNo_Suppress](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FNo_Suppress)

177 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FNo_Reorder](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FNo_Reorder)

178 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FNo_Zero](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FNo_Zero)

179 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FNoinline](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FNoinline)

180 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FNon_Reentrant](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FNon_Reentrant)

181 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FNot_Elaborated](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FNot_Elaborated)

182 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FNot_Null](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FNot_Null)

183 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FObsolescent](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FObsolescent)

184 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FOptimize_Alignment](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FOptimize_Alignment)

185 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FOptimize_Code](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FOptimize_Code)

186 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FOptimize_Options](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FOptimize_Options)

187 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FOrdered](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FOrdered)

188 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FParameter_Mechanism](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FParameter_Mechanism)

189 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPassive](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPassive)

190 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPersistent_BSS](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPersistent_BSS)

191 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPhysical_Address](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPhysical_Address)

192 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPolling](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPolling)

193 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPostcondition](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPostcondition)

194 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPrecondition](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPrecondition)

195 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPreserve_Layout](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPreserve_Layout)

196 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FProfile_Warnings](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FProfile_Warnings)

197 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPropagate_Exceptions](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPropagate_Exceptions)

• Protect_Registers[198](#part0328.xhtml__bookmark1290)  (ICC)

• Protected_Call[199](#part0328.xhtml__bookmark1291)  (ICC)

• Protected_Return[200](#part0328.xhtml__bookmark1292)  (ICC)

• Psect_Object[201](#part0328.xhtml__bookmark1293)  (GNAT,  HP  Ada)

• Pure_Function[202](#part0328.xhtml__bookmark1294)  (GNAT)

• Put[203](#part0328.xhtml__bookmark1295)  (ICC)

• Put_Line[204](#part0328.xhtml__bookmark1296)  (ICC)

39.3.5  R  −  S

• Reserve_Registers[205](#part0328.xhtml__bookmark1297)  (ICC)

• Restriction_Warnings[206](#part0328.xhtml__bookmark1298)  (GNAT)

• RTS_Interface[207](#part0328.xhtml__bookmark1299)  (SPARCompiler)

• SCCS_ID[208](#part0328.xhtml__bookmark1300)  (PowerAda)

• Share_Body[209](#part0328.xhtml__bookmark1301)  (SPARCompiler)

• Share_Code[210](#part0328.xhtml__bookmark1302) (SPARCompiler)

• Share_Generic[211](#part0328.xhtml__bookmark1303)  (GNAT,  HP  Ada)

• Shareable[212](#part0328.xhtml__bookmark1304)  (ICC)

• Short_Circuit_And_Or[213](#part0328.xhtml__bookmark1305)  (GNAT)

• Short_Descriptors[214](#part0328.xhtml__bookmark1306)  (GNAT)

• Simple_Storage_Pool_Type[215](#part0328.xhtml__bookmark1307)  (GNAT)

• Simple_Task[216](#part0328.xhtml__bookmark1308)  (ICC)

• Source_File_Name[217](#part0328.xhtml__bookmark1309)  (GNAT)

• Source_File_Name_Project[218](#part0328.xhtml__bookmark1310)  (GNAT)

• Source_Reference[219](#part0328.xhtml__bookmark1311)  (GNAT)

• Stack_Size[220](#part0328.xhtml__bookmark1312)  (ICC)

• Static_Elaboration[221](#part0328.xhtml__bookmark1313)  (ICC)

![](Images/image07347.jpeg)

198 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FProtect_Registers](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FProtect_Registers)

199 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FProtected_Call](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FProtected_Call)

200 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FProtected_Return](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FProtected_Return)

201 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPsect_Object](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPsect_Object)

202 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPure_Function](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPure_Function)

203 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPut](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPut)

204 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPut_Line](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FPut_Line)

205 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FReserve_Registers](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FReserve_Registers)

206 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FRestriction_Warnings](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FRestriction_Warnings)

207 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FRTS_Interface](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FRTS_Interface)

208 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSCCS_ID](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSCCS_ID)

209 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FShare_Body](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FShare_Body)

210 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FShare_Code](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FShare_Code)

211 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FShare_Generic](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FShare_Generic)

212 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FShareable](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FShareable)

213 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FShort_Circuit_And_Or](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FShort_Circuit_And_Or)

214 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FShort_Descriptors](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FShort_Descriptors)

215 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSimple_Storage_Pool_Type](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSimple_Storage_Pool_Type)

216 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSimple_Task](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSimple_Task)

217 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSource_File_Name](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSource_File_Name)

218 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSource_File_Name_Project](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSource_File_Name_Project)

219 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSource_Reference](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSource_Reference)

220 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FStack_Size](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FStack_Size)

221 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FStatic_Elaboration](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FStatic_Elaboration)

• Static_Elaboration_Desired[222](#part0329.xhtml__bookmark1314)  (GNAT)

• Stream_Convert[223](#part0329.xhtml__bookmark1315)  (GNAT)

• Style_Checks[224](#part0329.xhtml__bookmark1316)  (GNAT)

• Subtitle[225](#part0329.xhtml__bookmark1317)  (GNAT)

• Suppress_All[226](#part0329.xhtml__bookmark1318)  (GNAT,  HP  Ada,  PowerAda,  SPARCompiler)

• Suppress_Elaboration_Checks[227](#part0329.xhtml__bookmark1319)   (SPARCompiler)

• Suppress_Exception_Locations[228](#part0329.xhtml__bookmark1320)  (GNAT)

• Suppress_Initialization[229](#part0329.xhtml__bookmark1321)  (GNAT)

• System_Table[230](#part0329.xhtml__bookmark1322)  (ICC)

39.3.6 T  −  Z

• Task_Attributes[231](#part0329.xhtml__bookmark1323)  (SPARCompiler)

• Task_Info[232](#part0329.xhtml__bookmark1324)  (GNAT)

• Task_Name[233](#part0329.xhtml__bookmark1325)  (GNAT)

• Task_Storage[234](#part0329.xhtml__bookmark1326)  (GNAT,  HP  Ada)

• Test_Case[235](#part0329.xhtml__bookmark1327)  (GNAT)

• Thread_Body[236](#part0329.xhtml__bookmark1328)  (GNAT)

• Thread_Local_Storage[237](#part0329.xhtml__bookmark1329)  (GNAT)

• Time_Slice[238](#part0329.xhtml__bookmark1330)  (GNAT,  HP  Ada,  ICC)

• Time_Slice_Attributes[239](#part0329.xhtml__bookmark1331)  (ICC)

• Title[240](#part0329.xhtml__bookmark1332)  (GNAT,  HP  Ada)

• Unimplemented_Unit[241](#part0329.xhtml__bookmark1333)  (GNAT)

• Universal_Aliasing[242](#part0329.xhtml__bookmark1334)  (GNAT)

• Universal_Data[243](#part0329.xhtml__bookmark1335)  (GNAT)

• Unmodified[244](#part0329.xhtml__bookmark1336) (GNAT)

![](Images/image07348.jpeg)

222 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FStatic_Elaboration_Desired](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FStatic_Elaboration_Desired)

223 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FStream_Convert](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FStream_Convert)

224 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FStyle_Checks](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FStyle_Checks)

225 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSubtitle](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSubtitle)

226 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSuppress_All](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSuppress_All)

227 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSuppress_Elaboration_](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSuppress_Elaboration_Checks)  [Checks](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSuppress_Elaboration_Checks)

228 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSuppress_Exception_](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSuppress_Exception_Locations)

[Locations](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSuppress_Exception_Locations)

229 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSuppress_Initialization](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSuppress_Initialization)

230 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSystem_Table](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FSystem_Table)

231 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FTask_Attributes](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FTask_Attributes)

232 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FTask_Info](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FTask_Info)

233 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FTask_Name](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FTask_Name)

234 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FTask_Storage](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FTask_Storage)

235 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FTest_Case](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FTest_Case)

236 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FThread_Body](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FThread_Body)

237 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FThread_Local_Storage](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FThread_Local_Storage)

238 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FTime_Slice](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FTime_Slice)

239 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FTime_Slice_Attributes](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FTime_Slice_Attributes)

240 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FTitle](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FTitle)

241 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FUnimplemented_Unit](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FUnimplemented_Unit)

242 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FUniversal_Aliasing](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FUniversal_Aliasing)

243 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FUniversal_Data](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FUniversal_Data)

244 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FUnmodified](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FUnmodified)

• Unreferenced[245](#part0330.xhtml__bookmark1338)  (GNAT)

• Unreferenced_Objects[246](#part0330.xhtml__bookmark1339)  (GNAT)

• Unreserve_All_Interrupts[247](#part0330.xhtml__bookmark1340)  (GNAT)

• Unsigned_Literal[248](#part0330.xhtml__bookmark1341)  (ICC)

• Use_VADS_Size[249](#part0330.xhtml__bookmark1342)  (GNAT)

• Validity_Checks[250](#part0330.xhtml__bookmark1343)  (GNAT)

• Warning[251](#part0330.xhtml__bookmark1344)  (SPARCompiler)

• Warnings[252](#part0330.xhtml__bookmark1345)  (GNAT,  SPARCompiler)

• Weak_External[253](#part0330.xhtml__bookmark1346)  (GNAT)

• Wide_Character_Encoding[254](#part0330.xhtml__bookmark1347)  (GNAT)

## 39.4 See  also

See  also

#### 39.4.1  Wikibook

• Ada  Programming[255](#part0330.xhtml__bookmark1348)

• Ada  Programming/Aspects[256](#part0330.xhtml__bookmark1349)

• Ada  Programming/Attributes[257](#part0330.xhtml__bookmark1350)

• Ada  Programming/Keywords[258](#part0330.xhtml__bookmark1351)

#### 39.4.2  Ada  Reference  Manual

###### Ada  83

• Annex  2:  Pragmas  ˆ{[http://archive.adaic.com/standards/83lrm/html/lrm-](http://archive.adaic.com/standards/83lrm/html/lrm-2.html)2.  [html}](http://archive.adaic.com/standards/83lrm/html/lrm-2.html)

• Annex  B:  Predefined  Language  Pragmas  ˆ{[http://archive.adaic.com/standards/](http://archive.adaic.com/standards/83lrm/html/lrm-B.html)  [83lrm/html/lrm-B.html}](http://archive.adaic.com/standards/83lrm/html/lrm-B.html)

###### Ada  95

• 2.8  Pragmas[259](#part0330.xhtml__bookmark1352)

• Annex L:  (informative) Language-Defined  Pragmas[260](#part0330.xhtml__bookmark1353)

![](Images/image07349.jpeg)

245 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FUnreferenced](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FUnreferenced)

246 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FUnreferenced_Objects](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FUnreferenced_Objects)

247 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FUnreserve_All_Interrupts](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FUnreserve_All_Interrupts)

248 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FUnsigned_Literal](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FUnsigned_Literal)

249 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FUse_VADS_Size](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FUse_VADS_Size)

250 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FValidity_Checks](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FValidity_Checks)

251 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FWarning](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FWarning)

252 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FWarnings](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FWarnings)

253 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FWeak_External](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FWeak_External)

254 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FWide_Character_Encoding](http://en.wikibooks.org/wiki/Ada%20Programming%2FPragmas%2FWide_Character_Encoding)

255 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

256 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAspects](http://en.wikibooks.org/wiki/Ada%20Programming%2FAspects)

257 Chapter  [38](#part0307.xhtml__bookmark878)  on  page  [305](#part0307.xhtml__bookmark878)

258 Chapter  [35](#part0295.xhtml__bookmark761)  on  page  [293](#part0295.xhtml__bookmark761)

259 [http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-2-8.html](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-2-8.html)

260 [http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-L.html](http://www.adaic.org/resources/add_content/standards/95lrm/ARM_HTML/RM-L.html)

###### Ada  2005

• 2.8  Pragmas[261](#part0331.xhtml__bookmark1355)

• Annex L:  (informative) Language-Defined  Pragmas[262](#part0331.xhtml__bookmark1356)

###### Ada  2012

• 2.8  Pragmas[263](#part0331.xhtml__bookmark1357)

• Annex L:  (informative) Language-Defined  Pragmas[264](#part0331.xhtml__bookmark1358)

## 39.5 References

References

![](Images/image07350.jpeg)

261 [http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-2-8.html](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-2-8.html)

262 [http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-L.html](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-2-L.html)

263 [http://www.ada-auth.org/standards/12rm/html/RM-2-8.html](http://www.ada-auth.org/standards/12rm/html/RM-2-8.html)

264 [http://www.ada-auth.org/standards/12rm/html/RM-L.html](http://www.ada-auth.org/standards/12rm/html/RM-L.html)

# 40 Libraries

## 40.1 Predefined  Language  Libraries

Predefined  Language  Libraries

The  library  which  comes  with  Ada  in  general  and  GNAT[1](#part0333.xhtml__bookmark1363)  in  particular.  Ada's  built  in  library  is  quite  extensive  and  well  structured.  These chapters  too  are  more  reference  like.

• Standard[2](#part0333.xhtml__bookmark1364)

• Ada[3](#part0333.xhtml__bookmark1365)

• Interfaces[4](#part0333.xhtml__bookmark1366)

• System[5](#part0333.xhtml__bookmark1367)

• GNAT[6](#part0333.xhtml__bookmark1368)

## 40.2 Other  Language Libraries

Other  Language  Libraries

Other  libraries  which  are  not  part  of  the  standard  but  freely  available.

• Multi  Purpose[7](#part0333.xhtml__bookmark1369)

• Container  Libraries[8](#part0333.xhtml__bookmark1370)

• GUI  Libraries[9](#part0333.xhtml__bookmark1371)

• Distributed  Objects[10](#part0333.xhtml__bookmark1372)

• Database[11](#part0333.xhtml__bookmark1373)

• Web  Programming[12](#part0333.xhtml__bookmark1374)

• Input/Output[13](#part0333.xhtml__bookmark1375)

## 40.3 See  also

![](Images/image07351.jpeg)

1 [http://en.wikipedia.org/wiki/GNAT](http://en.wikipedia.org/wiki/GNAT)

2 Chapter  [41](#part0335.xhtml__bookmark1379)  on  page  [333](#part0335.xhtml__bookmark1379)

3 Chapter  [42](#part0339.xhtml__bookmark1395)  on  page  [337](#part0339.xhtml__bookmark1395)

4 Chapter  [43](#part0351.xhtml__bookmark1593)  on  page  [349](#part0351.xhtml__bookmark1593)

5 Chapter  [44](#part0353.xhtml__bookmark1621)  on  page  [351](#part0353.xhtml__bookmark1621)

6 Chapter  [45](#part0355.xhtml__bookmark1622)  on  page  [353](#part0355.xhtml__bookmark1622)

7 Chapter  [46](#part0359.xhtml__bookmark1696)  on  page  [357](#part0359.xhtml__bookmark1696)

8 Chapter  [47](#part0361.xhtml__bookmark1704)  on  page  [359](#part0361.xhtml__bookmark1704)

9 Chapter  [48](#part0363.xhtml__bookmark1717)  on  page  [361](#part0363.xhtml__bookmark1717)

10 Chapter  [49](#part0365.xhtml__bookmark1734)  on  page  [363](#part0365.xhtml__bookmark1734)

11 Chapter  [50](#part0367.xhtml__bookmark1744)  on  page  [365](#part0367.xhtml__bookmark1744)

12 Chapter  [51](#part0373.xhtml__bookmark1745)  on  page  [371](#part0373.xhtml__bookmark1745)

13 Chapter  [52](#part0375.xhtml__bookmark1753)  on  page  [373](#part0375.xhtml__bookmark1753)

Libraries

See  also

#### 40.3.1  Wikibook

• Ada  Programming[14](#part0334.xhtml__bookmark1376)

#### 40.3.2  Ada  Reference  Manual

• Annex  A  (normative)  Predefined  Language  Environment  ˆ{[http://www.adaic.org/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A.html)  [resources/add_content/standards/05rm/html/RM-A.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A.html)

#### 40.3.3  Resources

• A  collection  of  Tools  and  Libraries[15](#part0334.xhtml__bookmark1377)  maintained  by  the  Ada  Resource  Association.  es:Programación  en  Ada/Unidades  predefinidas[16](#part0334.xhtml__bookmark1378)

![](Images/image07352.jpeg)

14 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

15 [http://www.adaic.org/ada-resources/tools-libraries/](http://www.adaic.org/ada-resources/tools-libraries/)

16 [http://es.wikibooks.org/wiki/Programaci%F3n%20en%20Ada%2FUnidades%20predefinidas](http://es.wikibooks.org/wiki/Programaci%F3n%20en%20Ada%2FUnidades%20predefinidas)

# 41Libraries: Standard

The  Standard  package  is  implicit.  This  means  two  things:

1. You  do  not  need  to  with  or  use  the  package,  in  fact  you  cannot  (see  below).  It's  always  available  (except  where  hidden  by  a  homograph,  RM  8.3  (8)  ˆ{[http://www.](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-8-3.html)  [adaic.org/resources/add_content/standards/05rm/html/RM-8-3.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-8-3.html) ).

2. Standard  may  contain  constructs  which  are  not  quite  legal  Ada  (like  the  definitions  of  Character  and  Wide_Character).

A with clause mentioning Standard references a user-defined package Standard that  hides the predefined one.  So do not do this.  However any library unit hidden by a  homograph can be made visible again by qualifying its name with Standard, like e.g.  Standard.My_Unit.

## 41.1 Implementation

Implementation

Since  the  package  Standard  is  very  important  for  portability,  here  are  some  examples  for  various  compilers:

• The package  Standard[1](#part0335.xhtml__bookmark1382)  from ISO  8652[2](#part0335.xhtml__bookmark1383).

• The  package  Standard[3](#part0335.xhtml__bookmark1384)  from  GNAT[4](#part0335.xhtml__bookmark1385).

• The  package  Standard[5](#part0335.xhtml__bookmark1386)  from  Rational  Apex[6](#part0335.xhtml__bookmark1387).

• The  package  Standard[7](#part0335.xhtml__bookmark1388)  from  ObjectAda[8](#part0335.xhtml__bookmark1389)

• The  Standard[9](#part0335.xhtml__bookmark1390)  definitions  for  AppletMagic[10](#part0335.xhtml__bookmark1391)

## 41.2 Portability

Portability

The only mandatory types in Standard are Boolean, Integer and its subtypes, Float,  Character,  Wide_Character,  Wide_Wide_Character,  String,  Wide_String,  Wide_-  Wide_String,  Duration.  There  is  an  implementation  permission  in  RM  A.1  (51)  ˆ{[http://](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-1.html)  [www.adaic.org/resources/add_content/standards/05rm/html/RM-A-1.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-1.html)  that  there  may  be  more  integer  and  floating  point  types  and  an  implementation  advice  RM

A.1  (52) ˆ{[http://www.adaic.org/resources/add_content/standards/05rm/html/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-1.html)

![](Images/image07353.jpeg)

1 [http://en.wikibooks.org/wiki/%2FRM](http://en.wikibooks.org/wiki/%2FRM)

2 [http://en.wikipedia.org/wiki/ISO%208652](http://en.wikipedia.org/wiki/ISO%208652)

3 [http://en.wikibooks.org/wiki/%2FGNAT](http://en.wikibooks.org/wiki/%2FGNAT)

4 [http://en.wikipedia.org/wiki/GNAT](http://en.wikipedia.org/wiki/GNAT)

5 [http://en.wikibooks.org/wiki/%2FApex](http://en.wikibooks.org/wiki/%2FApex)

6 [http://www-306.ibm.com/software/awdtools/developer/ada](http://www-306.ibm.com/software/awdtools/developer/ada)

7 [http://en.wikibooks.org/wiki/%2FObjectAda](http://en.wikibooks.org/wiki/%2FObjectAda)

8 [http://www.aonix.com/objectada.html](http://www.aonix.com/objectada.html)

9 [http://en.wikibooks.org/wiki/%2FAppletMagic](http://en.wikibooks.org/wiki/%2FAppletMagic)

10 [http://www.sofcheck.com/products/adamagic.html#appletmagic](http://www.sofcheck.com/products/adamagic.html#appletmagic)

[Libraries:  Standard](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-1.html)

[RM-A-1.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-1.html)  about the names to be chosen. There even is no requirement that those  additional types must have different sizes.  So it is e.g.  legal for an implementation to  provide  two  types  Long_Integer  and  Long_Long_Integer  which  both  have  the  same  range  and  size.

Note that the ranges and sizes of these types can be different in every platform (except of  course for Boolean and [[Wide_]Wide_]Character). There is an implementation requirement  that  the  size  of  type  Integer  is  at  least  16  bits,  and  that  of  Long_Integer  at  least  32  bits  (if  present)  RM  3.5.4  (21..22)  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-5-4.html)  [standards/05rm/html/RM-3-5-4.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-5-4.html) .  So  if  you  want  full  portability  of  your  types,  do not use types from Standard (except where you must, see below), rather define you own  types.  A  compiler  will  reject  any  type  declaration  whose  range  it  cannot  satisfy.

This means e.g. if you need a 64-bit type and find that with your current implemen-  tation Standard.Long_Long_Integer is such a type, when porting your program to  another  implementation,  this  type  may  be  shorter,  but  the  compiler  will  not  tell  you

-  and  your  program  will  most  probably  crash.  However,  when  you  define  your  own  type  like

![](Images/image07354.jpeg)

then,  when porting to an implementation that cannot satisfy this range,  the compiler  will  reject  your  program.

The type Integer is mandatory when you use [[wide] wide] strings or exponentiation x**i.  This is why some projects even define their own strings, but this means throwing out the  child with the bath tub. Using Integer with strings and exponentiation will normally not  lead  to  portability  issues.

## 41.3 See  also

See  also

#### 41.3.1  Wikibook

• Ada  Programming[11](#part0336.xhtml__bookmark1393)

• Ada  Programming/Libraries#Predefined  Language  Libraries[12](#part0336.xhtml__bookmark1394)

#### 41.3.2  Ada  Reference  Manual

• A.1  The  Package  Standard  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-1.html)  [standards/05rm/html/RM-A-1.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-1.html)

• 3.5.4 Integer Types ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-5-4.html)  [05rm/html/RM-3-5-4.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-5-4.html)

• 3.5.7  Floating  Point  Types  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-5-7.html)  [standards/05rm/html/RM-3-5-7.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-3-5-7.html)

![](Images/image07355.jpeg)

11 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

12 Chapter  [40.1](#part0333.xhtml__bookmark1360)  on  page  [331](#part0333.xhtml__bookmark1360)

#### 41.3.3 Ada  Quality  and  Style  Guide

• 7.1.1  Obsolescent  Features  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/7-1-1.html)  [docs/95style/html/sec_7/7-1-1.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/7-1-1.html)  −  Avoid  using  the  package  ASCII

• 7.2.1  Predefined  Numeric  Types  ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/7-2-1.html)  [content/docs/95style/html/sec_7/7-2-1.html}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/7-2-1.html)  −  Avoid the predefined numeric  types

# 42 Libraries:  Ada

The  Ada  package  is  only  an  anchor  or  namespace  for  Ada's  standard  library.  Most  compilers will not allow you to add new packages to the Ada hierarchy and even if your  compiler allows it you should not do so since all package names starting with Ada. are  reserved  for  future  extensions.

## 42.1 List  of  language  defined  child  units

List  of  language  defined  child  units

The  following  library  units  (packages  and  generic  subprograms)  are  descendents  of  the  package  Ada.

###### Ada  2005

This  package  is  available  since  Ada  2005[1](#part0339.xhtml__bookmark1397).

42.1.1 A  −  C

• Ada.Assertions[2](#part0339.xhtml__bookmark1398)  (Ada  2005)

• Ada.Asynchronous_Task_Control[3](#part0339.xhtml__bookmark1399)

• Ada.Calendar[4](#part0339.xhtml__bookmark1400)

• Ada.Calendar.Arithmetic[5](#part0339.xhtml__bookmark1401)  (Ada  2005)

• Ada.Calendar.Formatting[6](#part0339.xhtml__bookmark1402)  (Ada  2005)

• Ada.Calendar.Time_Zones[7](#part0339.xhtml__bookmark1403)  (Ada  2005)

• Ada.Characters[8](#part0339.xhtml__bookmark1404)

• Ada.Characters.Conversions[9](#part0339.xhtml__bookmark1405)  (Ada  2005)

• Ada.Characters.Handling[10](#part0339.xhtml__bookmark1406)

• Ada.Characters.Latin_1[11](#part0339.xhtml__bookmark1407)

• Ada.Command_Line[12](#part0339.xhtml__bookmark1408)

• Ada.Complex_Text_IO[13](#part0339.xhtml__bookmark1409)  (Ada  2005)

![](Images/image07356.jpeg)

1 Chapter  [23](#part0221.xhtml__bookmark541)  on  page  [219](#part0221.xhtml__bookmark541)

2 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Assertions](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Assertions)

3 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Asynchronous_Task_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Asynchronous_Task_Control)  [Control](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Asynchronous_Task_Control)

4 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Calendar](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Calendar)

5 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Calendar.Arithmetic](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Calendar.Arithmetic)

6 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Calendar.Formatting](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Calendar.Formatting)

7 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Calendar.Time_Zones](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Calendar.Time_Zones)

8 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Characters](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Characters)

9 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Characters.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Characters.Conversions)  [Conversions](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Characters.Conversions)

10 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Characters.Handling](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Characters.Handling)

11 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Characters.Latin_1](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Characters.Latin_1)

12 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Command_Line](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Command_Line)

13 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Complex_Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Complex_Text_IO)

• Ada.Containers[14](#part0340.xhtml__bookmark1410)  (Ada  2005)

• Ada.Containers.Doubly_Linked_Lists[15](#part0340.xhtml__bookmark1411)  (Ada  2005)

• Ada.Containers.Generic_Array_Sort[16](#part0340.xhtml__bookmark1412)   (Ada  2005  generic  procedure)

• Ada.Containers.Generic_Constrained_Array_Sort[17](#part0340.xhtml__bookmark1413)   (Ada 2005 generic procedure)

• Ada.Containers.Hashed_Maps[18](#part0340.xhtml__bookmark1414)  (Ada  2005)

• Ada.Containers.Hashed_Sets[19](#part0340.xhtml__bookmark1415)  (Ada  2005)

• Ada.Containers.Indefinite_Doubly_Linked_Lists[20](#part0340.xhtml__bookmark1416)  (Ada  2005)

• Ada.Containers.Indefinite_Hashed_Maps[21](#part0340.xhtml__bookmark1417)  (Ada  2005)

• Ada.Containers.Indefinite_Hashed_Sets[22](#part0340.xhtml__bookmark1418) (Ada  2005)

• Ada.Containers.Indefinite_Ordered_Maps[23](#part0340.xhtml__bookmark1419)  (Ada  2005)

• Ada.Containers.Indefinite_Ordered_Sets[24](#part0340.xhtml__bookmark1420)  (Ada  2005)

• Ada.Containers.Indefinite_Vectors[25](#part0340.xhtml__bookmark1421)  (Ada  2005)

• Ada.Containers.Ordered_Maps[26](#part0340.xhtml__bookmark1422)  (Ada  2005)

• Ada.Containers.Ordered_Sets[27](#part0340.xhtml__bookmark1423)  (Ada  2005)

• Ada.Containers.Vectors[28](#part0340.xhtml__bookmark1424) (Ada  2005)

42.1.2  D  −  F

• Ada.Decimal[29](#part0340.xhtml__bookmark1425)

• Ada.Direct_IO[30](#part0340.xhtml__bookmark1426)

• Ada.Directories[31](#part0340.xhtml__bookmark1427)  (Ada  2005)

• Ada.Directories.Information[32](#part0340.xhtml__bookmark1428)  (Ada  2005)

• Ada.Dispatching[33](#part0340.xhtml__bookmark1429)  (Ada  2005)

![](Images/image07357.jpeg)

14 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers)

15 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Doubly_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Doubly_Linked_Lists)  [Linked_Lists](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Doubly_Linked_Lists)

16 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Generic_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Generic_Array_Sort)

[Array_Sort](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Generic_Array_Sort)

17 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Generic_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Generic_Constrained_Array_Sort)  [Constrained_Array_Sort](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Generic_Constrained_Array_Sort)

18 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Hashed_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Hashed_Maps)

[Maps](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Hashed_Maps)

19 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Hashed_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Hashed_Sets)  [Sets](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Hashed_Sets)

20 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Indefinite_Doubly_Linked_Lists)

[Indefinite_Doubly_Linked_Lists](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Indefinite_Doubly_Linked_Lists)

21 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Indefinite_Hashed_Maps)  [Indefinite_Hashed_Maps](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Indefinite_Hashed_Maps)

22 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Indefinite_Hashed_Sets)

[Indefinite_Hashed_Sets](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Indefinite_Hashed_Sets)

23 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Indefinite_Ordered_Maps)

[Indefinite_Ordered_Maps](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Indefinite_Ordered_Maps)

24 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Indefinite_Ordered_Sets)  [Indefinite_Ordered_Sets](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Indefinite_Ordered_Sets)

25 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Indefinite_Vectors)

[Indefinite_Vectors](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Indefinite_Vectors)

26 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Ordered_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Ordered_Maps)

[Maps](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Ordered_Maps)

27 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Ordered_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Ordered_Sets)  [Sets](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Ordered_Sets)

28 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Vectors](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers.Vectors)

29 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Decimal](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Decimal)

30 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Direct_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Direct_IO)

31 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Directories](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Directories)

32 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Directories.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Directories.Information)  [Information](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Directories.Information)

33 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Dispatching](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Dispatching)

• Ada.Dispatching.EDF[34](#part0341.xhtml__bookmark1430)  (Ada  2005)

• Ada.Dispatching.Round_Robin[35](#part0341.xhtml__bookmark1431)  (Ada  2005)

• Ada.Dynamic_Priorities[36](#part0341.xhtml__bookmark1432)

• Ada.Environment_Variables[37](#part0341.xhtml__bookmark1433)  (Ada  2005)

• Ada.Exceptions[38](#part0341.xhtml__bookmark1434)

• Ada.Execution_Time[39](#part0341.xhtml__bookmark1435)  (Ada  2005)

• Ada.Execution_Time.Timers[40](#part0341.xhtml__bookmark1436)  (Ada  2005)

• Ada.Execution_Time.Group_Budgets[41](#part0341.xhtml__bookmark1437)  (Ada  2005)

• Ada.Finalization[42](#part0341.xhtml__bookmark1438)

• Ada.Float_Text_IO[43](#part0341.xhtml__bookmark1439)

• Ada.Float_Wide_Text_IO[44](#part0341.xhtml__bookmark1440)

• Ada.Float_Wide_Wide_Text_IO[45](#part0341.xhtml__bookmark1441)  (Ada  2005)

42.1.3 G  −  R

• Ada.Integer_Text_IO[46](#part0341.xhtml__bookmark1442)

• Ada.Integer_Wide_Text_IO[47](#part0341.xhtml__bookmark1443)

• Ada.Integer_Wide_Wide_Text_IO[48](#part0341.xhtml__bookmark1444)  (Ada 2005)

• Ada.Interrupts[49](#part0341.xhtml__bookmark1445)

• Ada.Interrupts.Names[50](#part0341.xhtml__bookmark1446)

• Ada.IO_Exceptions[51](#part0341.xhtml__bookmark1447)

• Ada.Numerics[52](#part0341.xhtml__bookmark1448)

• Ada.Numerics.Complex_Arrays[53](#part0341.xhtml__bookmark1449)  (Ada  2005)

• Ada.Numerics.Complex_Elementary_Functions[54](#part0341.xhtml__bookmark1450)

![](Images/image07358.jpeg)

34 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Dispatching.EDF](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Dispatching.EDF)

35 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Dispatching.Round_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Dispatching.Round_Robin)  [Robin](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Dispatching.Round_Robin)

36 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Dynamic_Priorities](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Dynamic_Priorities)

37 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Environment_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Environment_Variables)  [Variables](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Environment_Variables)

38 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Exceptions](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Exceptions)

39 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Execution_Time](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Execution_Time)

40 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Execution_Time.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Execution_Time.Timers)  [Timers](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Execution_Time.Timers)

41 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Execution_Time.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Execution_Time.Group_Budgets)

[Group_Budgets](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Execution_Time.Group_Budgets)

42 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Finalization](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Finalization)

43 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Float_Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Float_Text_IO)

44 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Float_Wide_Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Float_Wide_Text_IO)

45 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Float_Wide_Wide_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Float_Wide_Wide_Text_IO)  [Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Float_Wide_Wide_Text_IO)

46 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Integer_Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Integer_Text_IO)

47 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Integer_Wide_Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Integer_Wide_Text_IO)

48 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Integer_Wide_Wide_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Integer_Wide_Wide_Text_IO)  [Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Integer_Wide_Wide_Text_IO)

49 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Interrupts](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Interrupts)

50 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Interrupts.Names](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Interrupts.Names)

51 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.IO_Exceptions](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.IO_Exceptions)

52 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics)

53 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Complex_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Complex_Arrays)  [Arrays](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Complex_Arrays)

54 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Complex_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Complex_Elementary_Functions)

[Elementary_Functions](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Complex_Elementary_Functions)

• Ada.Numerics.Complex_Types[55](#part0342.xhtml__bookmark1451)

• Ada.Numerics.Discrete_Random[56](#part0342.xhtml__bookmark1452)

• Ada.Numerics.Elementary_Functions[57](#part0342.xhtml__bookmark1453)

• Ada.Numerics.Float_Random[58](#part0342.xhtml__bookmark1454)

• Ada.Numerics.Generic_Complex_Arrays[59](#part0342.xhtml__bookmark1455)  (Ada  2005)

• Ada.Numerics.Generic_Complex_Elementary_Functions[60](#part0342.xhtml__bookmark1456)

• Ada.Numerics.Generic_Complex_Types[61](#part0342.xhtml__bookmark1457)

• Ada.Numerics.Generic_Elementary_Functions[62](#part0342.xhtml__bookmark1458)

• Ada.Numerics.Generic_Real_Arrays[63](#part0342.xhtml__bookmark1459)  (Ada  2005)

• Ada.Numerics.Real_Arrays[64](#part0342.xhtml__bookmark1460)  (Ada  2005)

42.1.4  R  −  S

• Ada.Real_Time[65](#part0342.xhtml__bookmark1461)

• Ada.Real_Time.Timing_Events[66](#part0342.xhtml__bookmark1462)  (Ada  2005)

• Ada.Sequential_IO[67](#part0342.xhtml__bookmark1463)

• Ada.Storage_IO[68](#part0342.xhtml__bookmark1464)

• Ada.Streams[69](#part0342.xhtml__bookmark1465)

• Ada.Streams.Stream_IO[70](#part0342.xhtml__bookmark1466)

• Ada.Strings[71](#part0342.xhtml__bookmark1467)

• Ada.Strings.Bounded[72](#part0342.xhtml__bookmark1468)

• Ada.Strings.Bounded.Hash[73](#part0342.xhtml__bookmark1469)  (Ada  2005  generic  function)

• Ada.Strings.Fixed[74](#part0342.xhtml__bookmark1470)

• Ada.Strings.Fixed.Hash[75](#part0342.xhtml__bookmark1471)  (Ada  2005  generic  function)

![](Images/image07359.jpeg)

55 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Complex_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Complex_Types)  [Types](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Complex_Types)

56 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Discrete_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Discrete_Random)

[Random](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Discrete_Random)

57 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Elementary_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Elementary_Functions)

[Functions](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Elementary_Functions)

58 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Float_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Float_Random)

[Random](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Float_Random)

59 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Generic_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Generic_Complex_Arrays)

[Complex_Arrays](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Generic_Complex_Arrays)

60 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Generic_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Generic_Complex_Elementary_Functions)  [Complex_Elementary_Functions](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Generic_Complex_Elementary_Functions)

61 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Generic_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Generic_Complex_Types)

[Complex_Types](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Generic_Complex_Types)

62 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Generic_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Generic_Elementary_Functions)  [Elementary_Functions](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Generic_Elementary_Functions)

63 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Generic_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Generic_Real_Arrays)

[Real_Arrays](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Generic_Real_Arrays)

64 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Real_Arrays](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Real_Arrays)

65 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Real_Time](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Real_Time)

66 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Real_Time.Timing_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Real_Time.Timing_Events)  [Events](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Real_Time.Timing_Events)

67 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Sequential_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Sequential_IO)

68 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Storage_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Storage_IO)

69 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Streams](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Streams)

70 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Streams.Stream_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Streams.Stream_IO)

71 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings)

72 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Bounded](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Bounded)

73 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Bounded.Hash](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Bounded.Hash)

74 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Fixed](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Fixed)

75 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Fixed.Hash](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Fixed.Hash)

• Ada.Strings.Hash[76](#part0343.xhtml__bookmark1472)  (Ada  2005  generic  function)

• Ada.Strings.Maps[77](#part0343.xhtml__bookmark1473)

• Ada.Strings.Maps.Constants[78](#part0343.xhtml__bookmark1474)

• Ada.Strings.Unbounded[79](#part0343.xhtml__bookmark1475)

• Ada.Strings.Unbounded.Hash[80](#part0343.xhtml__bookmark1476)  (Ada  2005  generic  function)

• Ada.Strings.Wide_Bounded[81](#part0343.xhtml__bookmark1477)

• Ada.Strings.Wide_Bounded.Wide_Hash[82](#part0343.xhtml__bookmark1478)  (Ada  2005  generic  function)

• Ada.Strings.Wide_Fixed[83](#part0343.xhtml__bookmark1479)

• Ada.Strings.Wide_Fixed.Wide_Hash[84](#part0343.xhtml__bookmark1480)  (Ada  2005  generic  function)

• Ada.Strings.Wide_Hash[85](#part0343.xhtml__bookmark1481)  (Ada  2005  generic  function)

• Ada.Strings.Wide_Maps[86](#part0343.xhtml__bookmark1482)

• Ada.Strings.Wide_Maps.Wide_Constants[87](#part0343.xhtml__bookmark1483)

• Ada.Strings.Wide_Unbounded[88](#part0343.xhtml__bookmark1484)

• Ada.Strings.Wide_Unbounded.Wide_Hash[89](#part0343.xhtml__bookmark1485)  (Ada  2005  generic  function)

• Ada.Strings.Wide_Wide_Bounded[90](#part0343.xhtml__bookmark1486)  (Ada  2005)

• Ada.Strings.Wide_Wide_Bounded.Wide_Wide_Hash[91](#part0343.xhtml__bookmark1487)  (Ada  2005  generic  function)

• Ada.Strings.Wide_Wide_Fixed[92](#part0343.xhtml__bookmark1488)  (Ada  2005)

• Ada.Strings.Wide_Wide_Fixed.Wide_Wide_Hash[93](#part0343.xhtml__bookmark1489)  (Ada  2005  generic  function)

• Ada.Strings.Wide_Wide_Hash[94](#part0343.xhtml__bookmark1490)  (Ada  2005  generic  function)

• Ada.Strings.Wide_Wide_Maps[95](#part0343.xhtml__bookmark1491)  (Ada  2005)

• Ada.Strings.Wide_Wide_Maps.Wide_Wide_Constants[96](#part0343.xhtml__bookmark1492)  (Ada  2005)

![](Images/image07360.jpeg)

76 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Hash](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Hash)

77 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Maps](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Maps)

78 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Maps.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Maps.Constants)  [Constants](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Maps.Constants)

79 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Unbounded](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Unbounded)

80 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Unbounded.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Unbounded.Hash)  [Hash](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Unbounded.Hash)

81 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Bounded](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Bounded)

82 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Bounded.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Bounded.Wide_Hash)  [Wide_Hash](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Bounded.Wide_Hash)

83 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Fixed](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Fixed)

84 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Fixed.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Fixed.Wide_Hash)  [Wide_Hash](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Fixed.Wide_Hash)

85 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Hash](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Hash)

86 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Maps](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Maps)

87 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Maps.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Maps.Wide_Constants)  [Wide_Constants](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Maps.Wide_Constants)

88 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Unbounded)

[Unbounded](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Unbounded)

89 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Unbounded.Wide_Hash)

[Unbounded.Wide_Hash](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Unbounded.Wide_Hash)

90 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_Bounded)  [Bounded](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_Bounded)

91 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_Bounded.Wide_Wide_Hash)

[Bounded.Wide_Wide_Hash](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_Bounded.Wide_Wide_Hash)

92 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_Fixed)  [Fixed](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_Fixed)

93 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_Fixed.Wide_Wide_Hash)

[Fixed.Wide_Wide_Hash](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_Fixed.Wide_Wide_Hash)

94 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_Hash)  [Hash](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_Hash)

95 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_Maps)

[Maps](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_Maps)

96 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_Maps.Wide_Wide_Constants)  [Maps.Wide_Wide_Constants](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_Maps.Wide_Wide_Constants)

• Ada.Strings.Wide_Wide_Unbounded[97](#part0344.xhtml__bookmark1493)  (Ada  2005)

• Ada.Strings.Wide_Wide_Unbounded.Wide_Wide_Hash[98](#part0344.xhtml__bookmark1494)  (Ada  2005  generic  func-  tion)

• Ada.Synchronous_Task_Control[99](#part0344.xhtml__bookmark1495)

42.1.5  T  −  U

• Ada.Tags[100](#part0344.xhtml__bookmark1496)

• Ada.Tags.Generic_Dispatching_Constructor[101](#part0344.xhtml__bookmark1497)  (generic  function)

• Ada.Task_Attributes[102](#part0344.xhtml__bookmark1498)

• Ada.Task_Identification[103](#part0344.xhtml__bookmark1499)

• Ada.Task_Termination[104](#part0344.xhtml__bookmark1500)  (Ada  2005)

• Ada.Text_IO[105](#part0344.xhtml__bookmark1501)

• Ada.Text_IO.Bounded_IO[106](#part0344.xhtml__bookmark1502)  (Ada  2005)

• Ada.Text_IO.Complex_IO[107](#part0344.xhtml__bookmark1503)

• Ada.Text_IO.Decimal_IO[108](#part0344.xhtml__bookmark1504)  (Nested  package  of  Ada.Text_IO  )

• Ada.Text_IO.Editing[109](#part0344.xhtml__bookmark1505)

• Ada.Text_IO.Enumeration_IO[110](#part0344.xhtml__bookmark1506)   (Nested  package  of  Ada.Text_IO[111](#part0344.xhtml__bookmark1507))

• Ada.Text_IO.Fixed_IO[112](#part0344.xhtml__bookmark1508)  (Nested  package  of  Ada.Text_IO  )

• Ada.Text_IO.Float_IO[113](#part0344.xhtml__bookmark1509)  (Nested  package  of  Ada.Text_IO  )

• Ada.Text_IO.Integer_IO[114](#part0344.xhtml__bookmark1510)  (Nested  package  of  Ada.Text_IO  )

• Ada.Text_IO.Modular_IO[115](#part0344.xhtml__bookmark1511)  (Nested  package  of  Ada.Text_IO  )

• Ada.Text_IO.Text_Streams[116](#part0344.xhtml__bookmark1512)

• Ada.Text_IO.Unbounded_IO[117](#part0344.xhtml__bookmark1513)  (Ada  2005)

• Ada.Unchecked_Conversion[118](#part0344.xhtml__bookmark1514)  (generic  function)

![](Images/image07361.jpeg)

97 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_Unbounded)  [Unbounded](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_Unbounded)

98 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_Unbounded.Wide_Wide_Hash)

[Unbounded.Wide_Wide_Hash](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_Unbounded.Wide_Wide_Hash)

99 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Synchronous_Task_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Synchronous_Task_Control)  [Control](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Synchronous_Task_Control)

100 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Tags](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Tags)

101 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Tags.Generic_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Tags.Generic_Dispatching_Constructor)  [Dispatching_Constructor](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Tags.Generic_Dispatching_Constructor)

102 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Task_Attributes](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Task_Attributes)

103 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Task_Identification](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Task_Identification)

104 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Task_Termination](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Task_Termination)

105 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO)

106 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Bounded_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Bounded_IO)

107 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Complex_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Complex_IO)

108 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Decimal_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Decimal_IO)

109 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Editing](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Editing)

110 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Enumeration_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Enumeration_IO) [IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Enumeration_IO)

111 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO)

112 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Fixed_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Fixed_IO)

113 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Float_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Float_IO)

114 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Integer_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Integer_IO)

115 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Modular_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Modular_IO)

116 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Text_Streams](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Text_Streams)

117 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Unbounded_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.Unbounded_IO)

118 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Unchecked_Conversion](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Unchecked_Conversion)

• Ada.Unchecked_Deallocation[119](#part0345.xhtml__bookmark1515)  (generic  procedure)

42.1.6 W  −  Z

• Ada.Wide_Characters[120](#part0345.xhtml__bookmark1516)  (Ada  2005)

• Ada.Wide_Text_IO[121](#part0345.xhtml__bookmark1517)

• Ada.Wide_Text_IO.Bounded_IO[122](#part0345.xhtml__bookmark1518)  (Ada  2005)

• Ada.Wide_Text_IO.Complex_IO[123](#part0345.xhtml__bookmark1519)

• Ada.Wide_Text_IO.Decimal_IO[124](#part0345.xhtml__bookmark1520)   (Nested  package  of  Ada.Wide_Text_IO  )

• Ada.Wide_Text_IO.Editing[125](#part0345.xhtml__bookmark1521)

• Ada.Wide_Text_IO.Enumeration_IO[126](#part0345.xhtml__bookmark1522)   (Nested  package  of  Ada.Wide_Text_IO  )

• Ada.Wide_Text_IO.Fixed_IO[127](#part0345.xhtml__bookmark1523)  (Nested  package  of  Ada.Wide_Text_IO  )

• Ada.Wide_Text_IO.Float_IO[128](#part0345.xhtml__bookmark1524)  (Nested  package  of  Ada.Wide_Text_IO  )

• Ada.Wide_Text_IO.Integer_IO[129](#part0345.xhtml__bookmark1525)   (Nested  package  of  Ada.Wide_Text_IO  )

• Ada.Wide_Text_IO.Modular_IO[130](#part0345.xhtml__bookmark1526)   (Nested  package  of  Ada.Wide_Text_IO  )

• Ada.Wide_Text_IO.Text_Streams[131](#part0345.xhtml__bookmark1527)

• Ada.Wide_Text_IO.Unbounded_IO[132](#part0345.xhtml__bookmark1528)  (Ada  2005)

• Ada.Wide_Wide_Characters[133](#part0345.xhtml__bookmark1529)  (Ada  2005)

• Ada.Wide_Wide_Text_IO[134](#part0345.xhtml__bookmark1530)  (Ada  2005)

• Ada.Wide_Wide_Text_IO.Bounded_IO[135](#part0345.xhtml__bookmark1531)  (Ada  2005)

• Ada.Wide_Wide_Text_IO.Complex_IO[136](#part0345.xhtml__bookmark1532) (Ada  2005)

• Ada.Wide_Wide_Text_IO.Decimal_IO[137](#part0345.xhtml__bookmark1533)  (Nested  package  of  Ada.Wide_Wide_-  Text_IO  )

![](Images/image07362.jpeg)

119 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Unchecked_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Unchecked_Deallocation)  [Deallocation](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Unchecked_Deallocation)

120 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Characters](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Characters)

121 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO)

122 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Bounded_IO)  [Bounded_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Bounded_IO)

123 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Complex_IO)

[Complex_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Complex_IO)

124 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Decimal_IO)  [Decimal_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Decimal_IO)

125 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Editing](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Editing)

126 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Enumeration_IO)  [Enumeration_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Enumeration_IO)

127 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Fixed_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Fixed_IO)

[IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Fixed_IO)

128 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Float_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Float_IO)

[IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Float_IO)

129 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Integer_IO)

[Integer_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Integer_IO)

130 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Modular_IO)  [Modular_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Modular_IO)

131 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Text_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Text_Streams)

[Streams](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Text_Streams)

132 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Unbounded_IO)

[Unbounded_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.Unbounded_IO)

133 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Characters](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Characters)

134 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO)

135 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.Bounded_IO)  [Bounded_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.Bounded_IO)

136 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.Complex_IO)

[Complex_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.Complex_IO)

137 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.Decimal_IO)  [Decimal_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.Decimal_IO)

• Ada.Wide_Wide_Text_IO.Editing[138](#part0346.xhtml__bookmark1535)  (Ada  2005)

• Ada.Wide_Wide_Text_IO.Enumeration_IO[139](#part0346.xhtml__bookmark1536)  (Nested  package  of  Ada.Wide_-  Wide_Text_IO  )

• Ada.Wide_Wide_Text_IO.Fixed_IO[140](#part0346.xhtml__bookmark1537) (Nested  package  of  Ada.Wide_Wide_Text_-  IO  )

• Ada.Wide_Wide_Text_IO.Float_IO[141](#part0346.xhtml__bookmark1538)  (Nested  package  of  Ada.Wide_Wide_Text_-  IO  )

• Ada.Wide_Wide_Text_IO.Integer_IO[142](#part0346.xhtml__bookmark1539)  (Nested  package  of  Ada.Wide_Wide_-  Text_IO  )

• Ada.Wide_Wide_Text_IO.Modular_IO[143](#part0346.xhtml__bookmark1540) (Nested package of Ada.Wide_Wide_-  Text_IO  )

• Ada.Wide_Wide_Text_IO.Text_Streams[144](#part0346.xhtml__bookmark1541)  (Ada  2005)

• Ada.Wide_Wide_Text_IO.Unbounded_IO[145](#part0346.xhtml__bookmark1542)  (Ada  2005)

## 42.2 List  of  implementation  defined  child  units

List  of  implementation  defined  child  units

The  Reference  Manual  allows  compiler  vendors  to  add  extensions  to  the  Standard  Libraries.  However,  these extensions cannot  be directly childs  of the package  Ada, only grandchilds

--  for  example  Ada.Characters.Latin_9  .

Currently, only the implementation defined library units of the GNAT[146](#part0346.xhtml__bookmark1543)  compiler are  listed here.  You can help Wikibooks by  adding[147](#part0346.xhtml__bookmark1544) implementation dependent packages  of  other  compilers:

###### GNAT

Extended  package  implemented  by  GNAT[148](#part0346.xhtml__bookmark1545).

###### ObjectAda

Extended  package  implemented  by  ObjectAda.

###### APEX

Extended  package  implemented  by  IBM/Rational  APEX.

![](Images/image07363.jpeg)

138 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.Editing)  [Editing](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.Editing)

139 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.Enumeration_IO)

[Enumeration_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.Enumeration_IO)

140 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.Fixed_IO)

[Fixed_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.Fixed_IO)

141 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.Float_IO)

[Float_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.Float_IO)

142 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.Integer_IO)

[Integer_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.Integer_IO)

143 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.Modular_IO)  [Modular_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.Modular_IO)

144 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.Text_Streams)

[Text_Streams](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.Text_Streams)

145 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.Unbounded_IO)

[Unbounded_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.Unbounded_IO)

146 [http://en.wikipedia.org/wiki/GNAT](http://en.wikipedia.org/wiki/GNAT)

147 http://en.wikibooks.org/w/index.php?title=Ada_Programming/Libraries/Ada&action=edit

148 [http://gcc.gnu.org/onlinedocs/gnat_rm/The-GNAT-Library.html](http://gcc.gnu.org/onlinedocs/gnat_rm/The-GNAT-Library.html)

42.2.1 A  −  K

• Ada.Characters.Latin_9[149](#part0347.xhtml__bookmark1546)  (GNAT)

• Ada.Characters.Wide_Latin_1[150](#part0347.xhtml__bookmark1547)  (GNAT)

• Ada.Characters.Wide_Latin_9[151](#part0347.xhtml__bookmark1548)  (GNAT)

• Ada.Characters.Wide_Wide_Latin_1[152](#part0347.xhtml__bookmark1549)  (GNAT)

• Ada.Characters.Wide_Wide_Latin_9[153](#part0347.xhtml__bookmark1550)  (GNAT)

• Ada.Command_Line.Environment[154](#part0347.xhtml__bookmark1551)  (GNAT)

• Ada.Command_Line.Remove[155](#part0347.xhtml__bookmark1552)  (GNAT)

• Ada.Direct_IO.C_Streams[156](#part0347.xhtml__bookmark1553)  (GNAT)

• Ada.Exceptions.Is_Null_Occurrence[157](#part0347.xhtml__bookmark1554)  (GNAT  child  function)

• Ada.Exceptions.Traceback[158](#part0347.xhtml__bookmark1555)  (GNAT)

42.2.2 L  −  Q

• Ada.Long_Float_Text_IO[159](#part0347.xhtml__bookmark1556)  (GNAT)

• Ada.Long_Float_Wide_Text_IO[160](#part0347.xhtml__bookmark1557)  (GNAT)

• Ada.Long_Integer_Text_IO[161](#part0347.xhtml__bookmark1558)  (GNAT)

• Ada.Long_Integer_Wide_Text_IO[162](#part0347.xhtml__bookmark1559)  (GNAT)

• Ada.Long_Long_Float_Text_IO[163](#part0347.xhtml__bookmark1560)  (GNAT)

• Ada.Long_Long_Float_Wide_Text_IO[164](#part0347.xhtml__bookmark1561) (GNAT)

• Ada.Long_Long_Integer_Text_IO[165](#part0347.xhtml__bookmark1562)  (GNAT)

• Ada.Long_Long_Integer_Wide_Text_IO[166](#part0347.xhtml__bookmark1563)  (GNAT)

• Ada.Numerics.Long_Complex_Elementary_Functions[167](#part0347.xhtml__bookmark1564)   (GNAT)

![](Images/image07364.jpeg)

149 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Characters.Latin_9](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Characters.Latin_9)

150 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Characters.Wide_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Characters.Wide_Latin_1)  [Latin_1](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Characters.Wide_Latin_1)

151 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Characters.Wide_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Characters.Wide_Latin_9)

[Latin_9](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Characters.Wide_Latin_9)

152 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Characters.Wide_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Characters.Wide_Wide_Latin_1)

[Wide_Latin_1](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Characters.Wide_Wide_Latin_1)

153 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Characters.Wide_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Characters.Wide_Wide_Latin_9)

[Wide_Latin_9](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Characters.Wide_Wide_Latin_9)

154 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Command_Line.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Command_Line.Environment)  [Environment](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Command_Line.Environment)

155 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Command_Line.Remove](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Command_Line.Remove)

156 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Direct_IO.C_Streams](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Direct_IO.C_Streams)

157 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Exceptions.Is_Null_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Exceptions.Is_Null_Occurrence)  [Occurrence](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Exceptions.Is_Null_Occurrence)

158 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Exceptions.Traceback](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Exceptions.Traceback)

159 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Long_Float_Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Long_Float_Text_IO)

160 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Long_Float_Wide_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Long_Float_Wide_Text_IO)  [Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Long_Float_Wide_Text_IO)

161 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Long_Integer_Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Long_Integer_Text_IO)

162 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Long_Integer_Wide_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Long_Integer_Wide_Text_IO)  [Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Long_Integer_Wide_Text_IO)

163 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Long_Long_Float_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Long_Long_Float_Text_IO)

[Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Long_Long_Float_Text_IO)

164 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Long_Long_Float_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Long_Long_Float_Wide_Text_IO)

[Wide_Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Long_Long_Float_Wide_Text_IO)

165 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Long_Long_Integer_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Long_Long_Integer_Text_IO)

[Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Long_Long_Integer_Text_IO)

166 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Long_Long_Integer_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Long_Long_Integer_Wide_Text_IO)

[Wide_Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Long_Long_Integer_Wide_Text_IO)

167 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Long_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Long_Complex_Elementary_Functions)

[Complex_Elementary_Functions](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Long_Complex_Elementary_Functions)

• Ada.Numerics.Long_Complex_Types[168](#part0348.xhtml__bookmark1565)  (GNAT)

• Ada.Numerics.Long_Elementary_Functions[169](#part0348.xhtml__bookmark1566)   (GNAT)

• Ada.Numerics.Long_Long_Complex_Elementary_Functions[170](#part0348.xhtml__bookmark1567) (GNAT)

• Ada.Numerics.Long_Long_Complex_Types[171](#part0348.xhtml__bookmark1568)  (GNAT)

• Ada.Numerics.Long_Long_Elementary_Functions[172](#part0348.xhtml__bookmark1569)  (GNAT)

• Ada.Numerics.Short_Complex_Elementary_Functions[173](#part0348.xhtml__bookmark1570)   (GNAT)

• Ada.Numerics.Short_Complex_Types[174](#part0348.xhtml__bookmark1571)  (GNAT)

• Ada.Numerics.Short_Elementary_Functions[175](#part0348.xhtml__bookmark1572)   (GNAT)

42.2.3  R  −  Z

• Ada.Sequential_IO.C_Streams[176](#part0348.xhtml__bookmark1573)  (GNAT)

• Ada.Short_Float_Text_IO[177](#part0348.xhtml__bookmark1574)  (GNAT)

• Ada.Short_Float_Wide_Text_IO[178](#part0348.xhtml__bookmark1575)  (GNAT)

• Ada.Short_Integer_Text_IO[179](#part0348.xhtml__bookmark1576)  (GNAT)

• Ada.Short_Integer_Wide_Text_IO[180](#part0348.xhtml__bookmark1577)   (GNAT)

• Ada.Short_Short_Integer_Text_IO[181](#part0348.xhtml__bookmark1578)   (GNAT)

• Ada.Short_Short_Integer_Wide_Text_IO[182](#part0348.xhtml__bookmark1579)   (GNAT)

• Ada.Streams.Stream_IO.C_Streams[183](#part0348.xhtml__bookmark1580) (GNAT)

• Ada.Strings.Unbounded.Text_IO[184](#part0348.xhtml__bookmark1581)  (GNAT)

• Ada.Strings.Wide_Unbounded.Wide_Text_IO[185](#part0348.xhtml__bookmark1582)  (GNAT)

![](Images/image07365.jpeg)

168 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Long_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Long_Complex_Types)  [Complex_Types](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Long_Complex_Types)

169 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Long_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Long_Elementary_Functions)

[Elementary_Functions](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Long_Elementary_Functions)

170 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Long_Long_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Long_Long_Complex_Elementary_Functions)  [Complex_Elementary_Functions](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Long_Long_Complex_Elementary_Functions)

171 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Long_Long_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Long_Long_Complex_Types)

[Complex_Types](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Long_Long_Complex_Types)

172 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Long_Long_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Long_Long_Elementary_Functions)  [Elementary_Functions](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Long_Long_Elementary_Functions)

173 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Short_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Short_Complex_Elementary_Functions)

[Complex_Elementary_Functions](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Short_Complex_Elementary_Functions)

174 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Short_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Short_Complex_Types)  [Complex_Types](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Short_Complex_Types)

175 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Short_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Short_Elementary_Functions)

[Elementary_Functions](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Numerics.Short_Elementary_Functions)

176 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Sequential_IO.C_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Sequential_IO.C_Streams)  [Streams](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Sequential_IO.C_Streams)

177 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Short_Float_Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Short_Float_Text_IO)

178 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Short_Float_Wide_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Short_Float_Wide_Text_IO)  [Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Short_Float_Wide_Text_IO)

179 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Short_Integer_Text_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Short_Integer_Text_IO)

[IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Short_Integer_Text_IO)

180 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Short_Integer_Wide_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Short_Integer_Wide_Text_IO)

[Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Short_Integer_Wide_Text_IO)

181 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Short_Short_Integer_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Short_Short_Integer_Text_IO)

[Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Short_Short_Integer_Text_IO)

182 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Short_Short_Integer_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Short_Short_Integer_Wide_Text_IO)

[Wide_Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Short_Short_Integer_Wide_Text_IO)

183 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Streams.Stream_IO.C_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Streams.Stream_IO.C_Streams)  [Streams](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Streams.Stream_IO.C_Streams)

184 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Unbounded.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Unbounded.Text_IO)

[Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Unbounded.Text_IO)

185 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Unbounded.Wide_Text_IO)

[Unbounded.Wide_Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Unbounded.Wide_Text_IO)

• Ada.Strings.Wide_Wide_Unbounded.Wide_Wide_Text_IO[186](#part0349.xhtml__bookmark1584)  (GNAT)

• Ada.Text_IO.C_Streams[187](#part0349.xhtml__bookmark1585)  (GNAT)

• Ada.Wide_Text_IO.C_Streams[188](#part0349.xhtml__bookmark1586)  (GNAT)

• Ada.Wide_Wide_Text_IO.C_Streams[189](#part0349.xhtml__bookmark1587)   (GNAT)

## 42.3 See  also

See  also

#### 42.3.1 Wikibook

• Ada  Programming[190](#part0349.xhtml__bookmark1588)

• Ada  Programming/Libraries[191](#part0349.xhtml__bookmark1589)

• Ada  Programming/Libraries/Standard[192](#part0349.xhtml__bookmark1590)

• Ada  Programming/Libraries/System[193](#part0349.xhtml__bookmark1591)

• Ada  Programming/Libraries/Interfaces[194](#part0349.xhtml__bookmark1592)

#### 42.3.2 Ada  Reference  Manual

A.2  The  Package  Ada  ˆ{[http://www.adaic.org/resources/add_content/standards/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-2.html)  [05rm/html/RM-A-2.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-2.html)

![](Images/image07366.jpeg)

186 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_Unbounded.Wide_Wide_Text_IO)  [Unbounded.Wide_Wide_Text_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Strings.Wide_Wide_Unbounded.Wide_Wide_Text_IO)

187 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.C_Streams](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Text_IO.C_Streams)

188 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.C_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.C_Streams)  [Streams](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Text_IO.C_Streams)

189 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.C_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.C_Streams)

[Streams](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Wide_Wide_Text_IO.C_Streams)

190 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

191 Chapter  [40](#part0333.xhtml__bookmark1359)  on  page  [331](#part0333.xhtml__bookmark1359)

192 Chapter  [41](#part0335.xhtml__bookmark1379)  on  page  [333](#part0335.xhtml__bookmark1379)

193 Chapter  [44](#part0353.xhtml__bookmark1621)  on  page  [351](#part0353.xhtml__bookmark1621)

194 Chapter  [43](#part0351.xhtml__bookmark1593)  on  page  [349](#part0351.xhtml__bookmark1593)

# 43 Libraries:  Interfaces

The  Interfaces  package  helps  in  interfacing  with  other  programming  languages.  Ada  is  one of the few languages where interfacing with other languages is part of the language  standard.  The  language  standard  defines  the  interfaces  for  C[1](#part0351.xhtml__bookmark1595),  Cobol[2](#part0351.xhtml__bookmark1596)  and  Fortran[3](#part0351.xhtml__bookmark1597).  Of  course  any  implementation  might  define  further  interfaces  —  GNAT[4](#part0351.xhtml__bookmark1598)  for  example  defines  an  interface  to  C++[5](#part0351.xhtml__bookmark1599).

Interfacing  with  other  languages  is  actually  provided  by  pragma  ,  pragma  and  pragma

## 43.1 Child  Packages

Child  Packages

• Interfaces.C[6](#part0351.xhtml__bookmark1600)

• Interfaces.C.Extensions[7](#part0351.xhtml__bookmark1601)  (GNAT)

• Interfaces.C.Pointers[8](#part0351.xhtml__bookmark1602)

• Interfaces.C.Streams[9](#part0351.xhtml__bookmark1603)  (GNAT)

• Interfaces.C.Strings[10](#part0351.xhtml__bookmark1604)

• Interfaces.CPP[11](#part0351.xhtml__bookmark1605)  (GNAT)

• Interfaces.COBOL[12](#part0351.xhtml__bookmark1606)

• Interfaces.Fortran[13](#part0351.xhtml__bookmark1607)

• Interfaces.OS2Lib[14](#part0351.xhtml__bookmark1608)  (GNAT, OS/2)

• Interfaces.OS2Lib.Errors[15](#part0351.xhtml__bookmark1609)  (GNAT,  OS/2)

• Interfaces.OS2Lib.Synchronization[16](#part0351.xhtml__bookmark1610)  (GNAT,  OS/2)

• Interfaces.OS2Lib.Threads[17](#part0351.xhtml__bookmark1611) (GNAT,  OS/2)

• Interfaces.Packed_Decimal[18](#part0351.xhtml__bookmark1612)  (GNAT)

![](Images/image07367.jpeg)

1 [http://en.wikibooks.org/wiki/C%20Programming](http://en.wikibooks.org/wiki/C%20Programming)

2 [http://en.wikibooks.org/wiki/COBOL](http://en.wikibooks.org/wiki/COBOL)

3 [http://en.wikibooks.org/wiki/Programming%3AFortran](http://en.wikibooks.org/wiki/Programming%3AFortran)

4 [http://en.wikibooks.org/wiki/Ada%20Programming%2FGNAT](http://en.wikibooks.org/wiki/Ada%20Programming%2FGNAT)

5 [http://en.wikibooks.org/wiki/C%2B%2B%20Programming](http://en.wikibooks.org/wiki/C%2B%2B%20Programming)

6 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.C](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.C)

7 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.C.Extensions](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.C.Extensions)

8 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.C.Pointers](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.C.Pointers)

9 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.C.Streams](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.C.Streams)

10 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.C.Strings](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.C.Strings)

11 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.CPP](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.CPP)

12 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.COBOL](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.COBOL)

13 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.Fortran](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.Fortran)

14 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.OS2Lib](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.OS2Lib)

15 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.OS2Lib.Errors](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.OS2Lib.Errors)

16 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.OS2Lib.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.OS2Lib.Synchronization)  [Synchronization](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.OS2Lib.Synchronization)

17 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.OS2Lib.](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.OS2Lib.Threads)

[Threads](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.OS2Lib.Threads)

18 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.Packed_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.Packed_Decimal)

[Decimal](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.Packed_Decimal)

Libraries:  Interfaces

• Interfaces.VxWorks[19](#part0352.xhtml__bookmark1614)  (GNAT,  VxWorks)

• Interfaces.VxWorks.IO[20](#part0352.xhtml__bookmark1615)  (GNAT,  VxWorks)

## 43.2 See  also

See  also

#### 43.2.1  Wikibook

• Ada  Programming[21](#part0352.xhtml__bookmark1616)

• Ada  Programming/Libraries[22](#part0352.xhtml__bookmark1617)

• Ada  Programming/Libraries/Standard[23](#part0352.xhtml__bookmark1618)

• Ada  Programming/Libraries/Ada[24](#part0352.xhtml__bookmark1619)

• Ada  Programming/Libraries/System[25](#part0352.xhtml__bookmark1620)

#### 43.2.2  Ada  Reference  Manual

###### Ada  95

• Annex B Interface to Other Languages ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-B.html)  [content/standards/05rm/html/RM-B.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-B.html)

• B.2  The  Package  Interfaces  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-B-2.html)  [standards/05rm/html/RM-B-2.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-B-2.html)

###### Ada  2005

• Annex B Interface to Other Languages ˆ{[http://www.adaic.org/resources/add_](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-B.html)  [content/standards/05rm/html/RM-B.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-B.html)

• B.2  The  Package  Interfaces  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-B-2.html)  [standards/05rm/html/RM-B-2.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-B-2.html)

![](Images/image07368.jpeg)

19 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.VxWorks](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.VxWorks)

20 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.VxWorks.IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FInterfaces.VxWorks.IO)

21 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

22 Chapter  [40](#part0333.xhtml__bookmark1359)  on  page  [331](#part0333.xhtml__bookmark1359)

23 Chapter  [41](#part0335.xhtml__bookmark1379)  on  page  [333](#part0335.xhtml__bookmark1379)

24 Chapter  [42](#part0339.xhtml__bookmark1395)  on  page  [337](#part0339.xhtml__bookmark1395)

25 Chapter  [44](#part0353.xhtml__bookmark1621)  on  page  [351](#part0353.xhtml__bookmark1621)

# 44 Libraries: System

# 45 Libraries:  GNAT

The GNAT package hierarchy defines several units for general purpose programming  provided  by  the  GNAT  compiler.  It  is  distributed  along  with  the  compiler  and  uses  the  same  license.

GNAT-4-ObjectAda[1](#part0355.xhtml__bookmark1624) is  a  project  for  porting  the  GNAT  library  to  the  ObjectAda  compiler.

## 45.1 Child  packages

Child  packages

• GNAT.Array_Split[2](#part0355.xhtml__bookmark1625)

• GNAT.AWK[3](#part0355.xhtml__bookmark1626)

• GNAT.Bounded_Buffers[4](#part0355.xhtml__bookmark1627)

• GNAT.Bounded_Mailboxes[5](#part0355.xhtml__bookmark1628)

• GNAT.Bubble_Sort[6](#part0355.xhtml__bookmark1629)

• GNAT.Bubble_Sort_A[7](#part0355.xhtml__bookmark1630)

• GNAT.Bubble_Sort_G[8](#part0355.xhtml__bookmark1631)

• GNAT.Calendar[9](#part0355.xhtml__bookmark1632)

• GNAT.Calendar.Time_IO[10](#part0355.xhtml__bookmark1633)

• GNAT.Case_Util[11](#part0355.xhtml__bookmark1634)

• GNAT.CGI[12](#part0355.xhtml__bookmark1635)

• GNAT.CGI.Cookie[13](#part0355.xhtml__bookmark1636)

• GNAT.CGI.Debug[14](#part0355.xhtml__bookmark1637)

• GNAT.Command_Line[15](#part0355.xhtml__bookmark1638)

• GNAT.Compiler_Version[16](#part0355.xhtml__bookmark1639)

• GNAT.CRC32[17](#part0355.xhtml__bookmark1640)

• GNAT.Ctrl_C[18](#part0355.xhtml__bookmark1641)

![](Images/image07369.jpeg)

1 [http://sourceforge.net/projects/gnat4oa](http://sourceforge.net/projects/gnat4oa)

2 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Array_Split](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Array_Split)

3 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.AWK](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.AWK)

4 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Bounded_Buffers](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Bounded_Buffers)

5 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Bounded_Mailboxes](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Bounded_Mailboxes)

6 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Bubble_Sort](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Bubble_Sort)

7 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Bubble_Sort_A](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Bubble_Sort_A)

8 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Bubble_Sort_G](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Bubble_Sort_G)

9 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Calendar](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Calendar)

10 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Calendar.Time_IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Calendar.Time_IO)

11 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Case_Util](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Case_Util)

12 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.CGI](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.CGI)

13 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.CGI.Cookie](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.CGI.Cookie)

14 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.CGI.Debug](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.CGI.Debug)

15 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Command_Line](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Command_Line)

16 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Compiler_Version](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Compiler_Version)

17 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.CRC32](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.CRC32)

18 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Ctrl_C](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Ctrl_C)

• GNAT.Current_Exception[19](#part0356.xhtml__bookmark1642)

• GNAT.Debug_Pools[20](#part0356.xhtml__bookmark1643)

• GNAT.Debug_Utilities[21](#part0356.xhtml__bookmark1644)

• GNAT.Directory_Operations[22](#part0356.xhtml__bookmark1645)

• GNAT.Directory_Operations.Iteration[23](#part0356.xhtml__bookmark1646)

• GNAT.Dynamic_HTables[24](#part0356.xhtml__bookmark1647)

• GNAT.Dynamic_Tables[25](#part0356.xhtml__bookmark1648)

• GNAT.Exception_Actions[26](#part0356.xhtml__bookmark1649)

• GNAT.Exceptions[27](#part0356.xhtml__bookmark1650)

• GNAT.Exception_Traces[28](#part0356.xhtml__bookmark1651)

• GNAT.Expect[29](#part0356.xhtml__bookmark1652)

• GNAT.Float_Control[30](#part0356.xhtml__bookmark1653)

• GNAT.Heap_Sort[31](#part0356.xhtml__bookmark1654)

• GNAT.Heap_Sort_A[32](#part0356.xhtml__bookmark1655)

• GNAT.Heap_Sort_G[33](#part0356.xhtml__bookmark1656)

• GNAT.HTable[34](#part0356.xhtml__bookmark1657)

• GNAT.IO[35](#part0356.xhtml__bookmark1658)

• GNAT.IO_Aux[36](#part0356.xhtml__bookmark1659)

• GNAT.Lock_Files[37](#part0356.xhtml__bookmark1660)

• GNAT.MD5[38](#part0356.xhtml__bookmark1661)

• GNAT.Memory_Dump[39](#part0356.xhtml__bookmark1662)

• GNAT.Most_Recent_Exception[40](#part0356.xhtml__bookmark1663)

• GNAT.OS_Lib[41](#part0356.xhtml__bookmark1664)

• GNAT.Perfect_Hash_Generators[42](#part0356.xhtml__bookmark1665)

![](Images/image07370.jpeg)

19 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Current_Exception](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Current_Exception)

20 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Debug_Pools](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Debug_Pools)

21 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Debug_Utilities](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Debug_Utilities)

22 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Directory_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Directory_Operations)  [Operations](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Directory_Operations)

23 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Directory_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Directory_Operations.Iteration)

[Operations.Iteration](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Directory_Operations.Iteration)

24 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Dynamic_HTables](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Dynamic_HTables)

25 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Dynamic_Tables](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Dynamic_Tables)

26 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Exception_Actions](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Exception_Actions)

27 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Exceptions](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Exceptions)

28 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Exception_Traces](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Exception_Traces)

29 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Expect](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Expect)

30 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Float_Control](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Float_Control)

31 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Heap_Sort](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Heap_Sort)

32 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Heap_Sort_A](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Heap_Sort_A)

33 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Heap_Sort_G](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Heap_Sort_G)

34 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.HTable](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.HTable)

35 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.IO](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.IO)

36 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.IO_Aux](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.IO_Aux)

37 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Lock_Files](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Lock_Files)

38 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.MD5](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.MD5)

39 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Memory_Dump](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Memory_Dump)

40 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Most_Recent_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Most_Recent_Exception)  [Exception](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Most_Recent_Exception)

41 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.OS_Lib](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.OS_Lib)

42 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Perfect_Hash_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Perfect_Hash_Generators)  [Generators](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Perfect_Hash_Generators)

• GNAT.Regexp[43](#part0357.xhtml__bookmark1666)

• GNAT.Registry[44](#part0357.xhtml__bookmark1667)

• GNAT.Regpat[45](#part0357.xhtml__bookmark1668)

• GNAT.Secondary_Stack_Info[46](#part0357.xhtml__bookmark1669)

• GNAT.Semaphores[47](#part0357.xhtml__bookmark1670)

• GNAT.Signals[48](#part0357.xhtml__bookmark1671)

• GNAT.Sockets[49](#part0357.xhtml__bookmark1672) (GNAT.Sockets  examples[50](#part0357.xhtml__bookmark1673))

• GNAT.Sockets.Constants[51](#part0357.xhtml__bookmark1674)

• GNAT.Sockets.Linker_Options[52](#part0357.xhtml__bookmark1675)

• GNAT.Sockets.Thin[53](#part0357.xhtml__bookmark1676)

• GNAT.Source_Info[54](#part0357.xhtml__bookmark1677)

• GNAT.Spelling_Checker[55](#part0357.xhtml__bookmark1678)

• GNAT.Spitbol[56](#part0357.xhtml__bookmark1679)

• GNAT.Spitbol.Patterns[57](#part0357.xhtml__bookmark1680)

• GNAT.Spitbol.Table_Boolean  new[58](#part0357.xhtml__bookmark1681)

• GNAT.Spitbol.Table_Integer[59](#part0357.xhtml__bookmark1682)

• GNAT.Spitbol.Table_VString  new[60](#part0357.xhtml__bookmark1683)

• GNAT.Strings[61](#part0357.xhtml__bookmark1684)

• GNAT.String_Split[62](#part0357.xhtml__bookmark1685)

• GNAT.Table[63](#part0357.xhtml__bookmark1686)

• GNAT.Task_Lock[64](#part0357.xhtml__bookmark1687)

• GNAT.Threads[65](#part0357.xhtml__bookmark1688)

• GNAT.Traceback[66](#part0357.xhtml__bookmark1689)

![](Images/image07371.jpeg)

43 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Regexp](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Regexp)

44 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Registry](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Registry)

45 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Regpat](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Regpat)

46 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Secondary_Stack_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Secondary_Stack_Info)  [Info](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Secondary_Stack_Info)

47 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Semaphores](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Semaphores)

48 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Signals](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Signals)

49 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Sockets](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Sockets)

50 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Sockets_examples](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Sockets_examples)

51 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Sockets.Constants](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Sockets.Constants)

52 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Sockets.Linker_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Sockets.Linker_Options)  [Options](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Sockets.Linker_Options)

53 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Sockets.Thin](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Sockets.Thin)

54 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Source_Info](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Source_Info)

55 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Spelling_Checker](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Spelling_Checker)

56 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Spitbol](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Spitbol)

57 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Spitbol.Patterns](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Spitbol.Patterns)

58 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Spitbol.Table_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Spitbol.Table_Boolean%20new)  [Boolean%20new](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Spitbol.Table_Boolean%20new)

59 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Spitbol.Table_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Spitbol.Table_Integer)

[Integer](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Spitbol.Table_Integer)

60 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Spitbol.Table_](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Spitbol.Table_VString%20new)  [VString%20new](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Spitbol.Table_VString%20new)

61 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Strings](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Strings)

62 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.String_Split](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.String_Split)

63 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Table](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Table)

64 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Task_Lock](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Task_Lock)

65 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Threads](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Threads)

66 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Traceback](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Traceback)

• GNAT.Traceback.Symbolic[67](#part0358.xhtml__bookmark1691)

• GNAT.Wide_String_Split[68](#part0358.xhtml__bookmark1692)

## 45.2 See  also

See  also

#### 45.2.1  External  links

• The  GNAT  Library[69](#part0358.xhtml__bookmark1693)

#### 45.2.2  Wikibook

• Ada  Programming[70](#part0358.xhtml__bookmark1694)

• Ada  Programming/Libraries[71](#part0358.xhtml__bookmark1695)

![](Images/image07372.jpeg)

67 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Traceback.Symbolic](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Traceback.Symbolic)

68 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Wide_String_Split](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGNAT.Wide_String_Split)

69 [http://gcc.gnu.org/onlinedocs/gnat_rm/The-GNAT-Library.html](http://gcc.gnu.org/onlinedocs/gnat_rm/The-GNAT-Library.html)

70 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

71 Chapter  [40](#part0333.xhtml__bookmark1359)  on  page  [331](#part0333.xhtml__bookmark1359)

# 46 Libraries: Multi-Purpose

###### AdaCL,  Ada  Class  Library[1](#part0359.xhtml__bookmark1698)

Filtering of text files, string tools, process control, command line parsing, CGI, garbage  collector,  components.

###### Matreshka[2](#part0359.xhtml__bookmark1699)

Core components for information system development: Unicode support (case conver-  sions and folding, collation, normalization); regular expression engine; XML processor;  FastCGI,  SQL  database  access.

###### paraffin[3](#part0359.xhtml__bookmark1700)

"A suite of Ada 2005 generics to facilitate iterative and recursive parallelism".[4](#part0359.xhtml__bookmark1701) Features  include  load-balancing  and  monitoring  of  stacks.

## 46.1 See  also

See  also

#### 46.1.1 Wikibook

• Ada  Programming[6](#part0359.xhtml__bookmark1702)

• Ada  Programming/Libraries[7](#part0359.xhtml__bookmark1703)

#### 46.1.2 Ada  Reference  Manual

--  does  not  apply  --

#### 46.1.3 References

![](Images/image07373.jpeg)

1 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FMultiPurpose%2FAdaCL](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FMultiPurpose%2FAdaCL)

2 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FMultiPurpose%2FMatreshka](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FMultiPurpose%2FMatreshka)

3 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FMultiPurpose%2FParaffin](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FMultiPurpose%2FParaffin)

4 Iterative  and  recursive  parallelism  generics  for  Ada  2005  [5](#part0000.xhtml__bookmark0).  .  Retrieved  2012-08-28

6 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

7 Chapter  [40](#part0333.xhtml__bookmark1359)  on  page  [331](#part0333.xhtml__bookmark1359)

# 47 Libraries: Container

The  following  Libraries  help  you  store  and  manage  objects  inside  container  classes:

###### Booch  Components[1](#part0361.xhtml__bookmark1706)

the  most  complete  of  all  container  class  libraries  (at  least  when  used  with  AdaCL,  Ada  Class  Library[2](#part0361.xhtml__bookmark1707)).

###### AdaCL,  Ada  Class  Library[3](#part0361.xhtml__bookmark1708)

A  Booch  Components[4](#part0361.xhtml__bookmark1709)  extension  pack  for  storing  indefinite  objects.

###### Charles[5](#part0361.xhtml__bookmark1710)

Build  on  the  C++  STL  and  therefore  very  easy  to  learn  for  C++  developers.

###### AI302[6](#part0361.xhtml__bookmark1711)

Proof  of  concept  for  Ada.Containers[7](#part0361.xhtml__bookmark1712)

###### Ada.Containers[8](#part0361.xhtml__bookmark1713)

This  language  feature  is  only  available  in  Ada  2005

###### Stephe's  Ada  Library[9](#part0361.xhtml__bookmark1714)

dynamic  arrays,  lists,  trees

## 47.1 See  also

See  also

#### 47.1.1 Wikibook

• Ada  Programming[10](#part0361.xhtml__bookmark1715)

• Ada  Programming/Libraries[11](#part0361.xhtml__bookmark1716)

#### 47.1.2 Ada  Reference  Manual

• A.18.1  The  Package  Containers  ˆ{[http://www.adaic.org/resources/add_content/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-18-1.html)  [standards/05rm/html/RM-A-18-1.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-A-18-1.html)

![](Images/image07374.jpeg)

1 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FContainer%2FBooch](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FContainer%2FBooch)

2 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FMultiPurpose%2FAdaCL](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FMultiPurpose%2FAdaCL)

3 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FMultiPurpose%2FAdaCL](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FMultiPurpose%2FAdaCL)

4 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FContainer%2FBooch](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FContainer%2FBooch)

5 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FContainer%2FCharles](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FContainer%2FCharles)

6 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FContainer%2FAI302](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FContainer%2FAI302)

7 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers)

8 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FAda.Containers)

9 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FSAL](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FSAL)

10 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

11 Chapter  [40](#part0333.xhtml__bookmark1359)  on  page  [331](#part0333.xhtml__bookmark1359)

# 48 Libraries:  GUI

The  following  libraries  can  be  used  to  make  Graphical  User  Interfaces:

###### CLAW[1](#part0363.xhtml__bookmark1719)

Commercial  GUI  toolkit  for  Windows.Introductory  Edition[2](#part0363.xhtml__bookmark1720)  is  distributed  under  GMGPL[3](#part0363.xhtml__bookmark1721).

###### GtkAda[4](#part0363.xhtml__bookmark1722)

Binding  to the  popular  GTK+  toolkit.

###### GWindows[5](#part0363.xhtml__bookmark1723)

RAD  GUI  Development  Framework  for  Windows.

###### Qt4Ada[6](#part0363.xhtml__bookmark1724)

An  Ada2005  binding  to  Qt4.  Under  CeCILL  license  V2.

###### QtAda[7](#part0363.xhtml__bookmark1725)

An  Ada2005  binding  to  the  Qt  libraries  and  associated  tools.  Under  GPL  and  GMGPL[8](#part0363.xhtml__bookmark1726)  (commercially  supported)  licenses.

###### libAgar[9](#part0363.xhtml__bookmark1727)

Ada  bindings  for  the  libagar[10](#part0363.xhtml__bookmark1728)  OpenGL  GUI  library  (BSD  license).

###### TASH[11](#part0363.xhtml__bookmark1729)

TclAdaSHell,  An  Ada  binding  to  Tcl/Tk.  GPL  with  "Linking  Exception".

## 48.1 See  also

See  also

#### 48.1.1 Wikibook

• Ada  Programming[12](#part0363.xhtml__bookmark1730)

• Ada  Programming/Libraries[13](#part0363.xhtml__bookmark1731)

#### 48.1.2 Ada  Reference  Manual

--  does  not  apply  --

![](Images/image07375.jpeg)

1 [http://www.rrsoftware.com/html/prodinf/claw/claw.htm](http://www.rrsoftware.com/html/prodinf/claw/claw.htm)

2 [http://www.adapower.com/adapower1/claw/](http://www.adapower.com/adapower1/claw/)

3 [http://en.wikipedia.org/wiki/GMGPL](http://en.wikipedia.org/wiki/GMGPL)

4 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGUI%2FGtkAda](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGUI%2FGtkAda)

5 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGUI%2FGWindows](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGUI%2FGWindows)

6 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGUI%2FQt4Ada](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGUI%2FQt4Ada)

7 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGUI%2FQtAda](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGUI%2FQtAda)

8 [http://en.wikipedia.org/wiki/GMGPL](http://en.wikipedia.org/wiki/GMGPL)

9 [http://wiki.libagar.org/wiki/Ada_bindings](http://wiki.libagar.org/wiki/Ada_bindings)

10 [http://libagar.org/](http://libagar.org/)

11 [http://sourceforge.net/projects/tcladashell/](http://sourceforge.net/projects/tcladashell/)

12 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

13 Chapter  [40](#part0333.xhtml__bookmark1359)  on  page  [331](#part0333.xhtml__bookmark1359)

Libraries:  GUI

#### 48.1.3  External  Links

• adapower.com  -  Links  to  tools  and  Bindings  for  GUI  Applications[14](#part0364.xhtml__bookmark1732)

• adapower.com  -  Examples  of  programming  GUIs  in  Ada[15](#part0364.xhtml__bookmark1733)

![](Images/image07376.jpeg)

14 [http://www.adapower.com/index.php?Command=Class&ClassID=AdaGUI&Title=Ada+GUI](http://www.adapower.com/index.php?Command=Class&ClassID=AdaGUI&Title=Ada%2BGUI)

15 [http://www.adapower.com/index.php?Command=Class&ClassID=GUIExamples&Title=GUI+](http://www.adapower.com/index.php?Command=Class&ClassID=GUIExamples&Title=GUI%2BExamples)  [Examples](http://www.adapower.com/index.php?Command=Class&ClassID=GUIExamples&Title=GUI%2BExamples)

362

# 49 Libraries: Distributed  Systems

The  following  Libraries  help  you  in  Distributed  programming:

###### GLADE[1](#part0365.xhtml__bookmark1736)

A  full  implementation  of  the  Ada  Annex  E:  Distributed  Systems[2](#part0365.xhtml__bookmark1737)

###### PolyORB[3](#part0365.xhtml__bookmark1738)

A  CORBA[4](#part0365.xhtml__bookmark1739)  and  Annex  E:  Distributed  Systems[5](#part0365.xhtml__bookmark1740)  implementation.

## 49.1 See  also

See  also

#### 49.1.1 Wikibook

• Ada  Programming[6](#part0365.xhtml__bookmark1741)

• Ada  Programming/Libraries[7](#part0365.xhtml__bookmark1742)

• Programming:CORBA[8](#part0365.xhtml__bookmark1743)

#### 49.1.2 Ada  Reference  Manual

• Annex  E  (normative)  Distributed  Systems  ˆ{[http://www.adaic.org/resources/](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-E.html)  [add_content/standards/05rm/html/RM-E.html}](http://www.adaic.org/resources/add_content/standards/05rm/html/RM-E.html)

![](Images/image07377.jpeg)

1 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FDistributed%2FGLADE](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FDistributed%2FGLADE)

2 [http://www.adaic.org/standards/95lrm/html/RM-E.html](http://www.adaic.org/standards/95lrm/html/RM-E.html)

3 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FDistributed%2FPolyORB](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FDistributed%2FPolyORB)

4 [http://en.wikibooks.org/wiki/Programming%3ACORBA](http://en.wikibooks.org/wiki/Programming%3ACORBA)

5 [http://www.adaic.org/standards/95lrm/html/RM-E.html](http://www.adaic.org/standards/95lrm/html/RM-E.html)

6 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

7 Chapter  [40](#part0333.xhtml__bookmark1359)  on  page  [331](#part0333.xhtml__bookmark1359)

8 [http://en.wikibooks.org/wiki/Programming%3ACORBA](http://en.wikibooks.org/wiki/Programming%3ACORBA)

# 50Libraries: Databases

The  following  libraries  help  you  in  Database  programming:

![](Images/image07378.jpeg)![](Images/image07379.jpeg)

| Li-brary | Li-cense | Inter-base  Fire-  bird | MySQL | ODBC | Ora-cle | Post-greSQL | SQLite3 | Sybase | Otherdatabase | Bi-nary  pack-  ages | Notes |
| APQ[1](#part0000.xhtml__bookmark0) | GMGPL | — | Yes | Yes | — | Yes | — | Yes | — | De-bian[2](#part0000.xhtml__bookmark0) | Thread-safe  connec-  tion  pools |
| GNADE(GNuAda  Database  Envi-  ron-  ment)[3](#part0000.xhtml__bookmark0) | GMGPL | — | 3.x,4.x | Yes | — | Yes | Yes | — | — | De-bian[4](#part0000.xhtml__bookmark0) | Em-bedded  SQLprepro-  cessor |
| gnadelite | [5](#part0000.xhtml__bookmark0)? | ? | ? | ? | ? | ? | Yes | ? | ? | ? |  |

![](Images/image07380.jpeg)

1 [http://framework.kow.com.br](http://framework.kow.com.br/)

2 [http://packages.qa.debian.org/a/apq.html](http://packages.qa.debian.org/a/apq.html)

3 [http://gnade.sourceforge.net](http://gnade.sourceforge.net/)

4 [http://packages.qa.debian.org/g/gnade.html](http://packages.qa.debian.org/g/gnade.html)

5 [http://repo.or.cz/w/gnadelite.git](http://repo.or.cz/w/gnadelite.git)

![](Images/image07381.jpeg)

![](Images/image07382.jpeg)<map name="awmap8"><area shape="rect" href="_bookmark0" coords="668, 523, 681, 540"><area shape="rect" href="_bookmark0" coords="668, 469, 677, 486"><area shape="rect" href="_bookmark0" coords="46, 486, 54, 503"><area shape="rect" href="_bookmark0" coords="50, 379, 56, 396"><area shape="rect" href="_bookmark0" coords="40, 155, 46, 172"></map>-

![](Images/image07383.jpeg)

6 [http://www.adacore.com/wp-content/files/auto_update/gnatcoll-docs/gnatcoll.html#](http://www.adacore.com/wp-content/files/auto_update/gnatcoll-docs/gnatcoll.html#Database-interface)  [Database-interface](http://www.adacore.com/wp-content/files/auto_update/gnatcoll-docs/gnatcoll.html#Database-interface)

7 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FDatabase%2FGWindows](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FDatabase%2FGWindows)

8 [http://adaforge.qtada.com/cgi-bin/tracker.fcgi/matreshka/wiki](http://adaforge.qtada.com/cgi-bin/tracker.fcgi/matreshka/wiki)

9 [http://www.opensuse.org](http://www.opensuse.org/)

10 [http://www.fedoraproject.org](http://www.fedoraproject.org/)

![](Images/image07384.jpeg)![](Images/image07385.jpeg)

![](Images/image07386.jpeg)<map name="awmap9"><area shape="rect" href="_bookmark0" coords="10, 294, 17, 311"><area shape="rect" href="_bookmark0" coords="41, 277, 48, 294"><area shape="rect" href="_bookmark0" coords="33, 18, 50, 35"></map>a.

![](Images/image07387.jpeg)

11 [http://pobry.blogspot.fr/p/ada-contributions.html](http://pobry.blogspot.fr/p/ada-contributions.html)

12 [http://www.qtada.com/](http://www.qtada.com/)

![](Images/image07388.jpeg)

| Sim-ple  Compo-  nents  for  Ada[13](#part0000.xhtml__bookmark0) | GMGPL | — | — | Yes | — | — | Yes | — | — | Fe-dora,  Debian | SQLitebind-  ings  are  in-  tended  for  static  linking  with  theSQLite3  amal-  gation.  ODBCbind-  ings  support  32-  and  64-bit  plat-forms |
| SOCI-Ada[14](#part0000.xhtml__bookmark0) | Boost | — | Yes | — | Yes | Yes | — | — | — | ? | Re-quires  C++. |
| SQLite3-Ada[15](#part0000.xhtml__bookmark0) | Publicdomain | — | — | — | — | — | Yes | — | — | ? |  |

![](Images/image07389.jpeg)

13 [http://www.dmitry-kazakov.de/ada/components.htm#SQLite](http://www.dmitry-kazakov.de/ada/components.htm#SQLite)

14 [http://www.inspirel.com/soci-ada/](http://www.inspirel.com/soci-ada/)

15 [http://coreland.ath.cx/code/sqlite3-ada](http://coreland.ath.cx/code/sqlite3-ada)

# 51 Libraries:  Web

The  following  libraries  help  you  in  Internet  or  Web  programming:

AdaCL, Ada Class Library[1](#part0373.xhtml__bookmark1747)  Powerful CGI implementation.  XML/Ada[2](#part0373.xhtml__bookmark1748)

XML  and  Unicode  support.

###### AWS[3](#part0373.xhtml__bookmark1749)

A  full-featured  Web-Server.

###### Matreshka[4](#part0373.xhtml__bookmark1750)

FastCGI,  XML,  Unicode  and  localization  support.

## 51.1 See  also

See  also

#### 51.1.1 Wikibook

• Ada  Programming[5](#part0373.xhtml__bookmark1752)

• Ada  Programming/Libraries[6](#part0373.xhtml__bookmark1751)

#### 51.1.2 Ada  Reference  Manual

--  does  not  apply  --

![](Images/image07390.jpeg)

1 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FMultiPurpose%2FAdaCL](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FMultiPurpose%2FAdaCL)

2 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FIO%2FXML%2FAda](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FIO%2FXML%2FAda)

3 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FWeb%2FAWS](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FWeb%2FAWS)

# 52 Libraries:  Input  Output

The  following  libraries  help  you  when  doing  input/output[1](#part0375.xhtml__bookmark1755):

###### AdaCL,  Ada  Class  Library[2](#part0375.xhtml__bookmark1756)

A multipurpose library featuring filtering of text files, string I/O, command line parsing,  etc.

###### XML/Ada[3](#part0375.xhtml__bookmark1757)

XML  and  Unicode  support.

###### Matreshka[4](#part0375.xhtml__bookmark1758)

SAX-style XML reader and writer. Supports XML1.0 (Fifth Edition), XML1.1 (Second  Edition), Namespaces in XML and XML Base Specifications. Strings, files and sockets  can be used as input source in both blocking and non-blocking modes. Full Unicode  support  and  many  text  codecs  is  provided  also.

## 52.1 See  also

See  also

#### 52.1.1 Wikibook

• Ada  Programming[5](#part0375.xhtml__bookmark1760)

• Ada  Programming/Libraries[6](#part0375.xhtml__bookmark1759)

#### 52.1.2 Ada  Reference  Manual

--  does  not  apply  --

1 Chapter  [18](#part0149.xhtml__bookmark416)  on  page  [147](#part0149.xhtml__bookmark416)

2 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FMultiPurpose%2FAdaCL](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FMultiPurpose%2FAdaCL)

3 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FIO%2FXML%2FAda](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FIO%2FXML%2FAda)

# 53Platform  Support

Ada  is  known  to  be  very  portable,  but  there  is  sometimes  a  necessity  of  using  a  specific  platform  feature.  For  that  matter,  there  are  some  non-standard  libraries.

• Linux[1](#part0377.xhtml__bookmark1763)

• Windows[2](#part0377.xhtml__bookmark1764)

• POSIX  systems[3](#part0377.xhtml__bookmark1765)

• Virtual  machines[4](#part0377.xhtml__bookmark1766)

• Java[5](#part0377.xhtml__bookmark1767)

• .NET[6](#part0377.xhtml__bookmark1768)

## 53.1 See  also

See  also

#### 53.1.1 Wikibook

• Ada  Programming[7](#part0377.xhtml__bookmark1769)

#### 53.1.2 Ada  Reference  Manual

--  does  not  apply  --

#### 53.1.3 Ada  Quality  and  Style  Guide

• Chapter  7:  Portability  ˆ{[http://www.adaic.org/resources/add_content/docs/](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/)  [95style/html/sec_7/}](http://www.adaic.org/resources/add_content/docs/95style/html/sec_7/)

![](Images/image07391.jpeg)

1 Chapter  [54](#part0379.xhtml__bookmark1770)  on  page  [377](#part0379.xhtml__bookmark1770)

2 Chapter  [55](#part0381.xhtml__bookmark1781)  on  page  [379](#part0381.xhtml__bookmark1781)

3 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FPOSIX](http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FPOSIX)

4 Chapter  [56](#part0383.xhtml__bookmark1793)  on  page  [381](#part0383.xhtml__bookmark1793)

5 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FVM%2FJava](http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FVM%2FJava)

6 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FVM%2FdotNET](http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FVM%2FdotNET)

7 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

# 54 Platform:  Linux

The  following  libraries  help  you  when  you  target  the  Linux  Platform.

###### Florist[1](#part0379.xhtml__bookmark1772)

POSIX.5  binding.  It  will  let  you  perform  Linux  system  calls  in  the  POSIX  subset.

###### Ncurses[2](#part0379.xhtml__bookmark1773)

text  terminal library.

###### Texttools[3](#part0379.xhtml__bookmark1774)

ncurses-based  library  for  the  Linux  console.

###### GtkAda[4](#part0379.xhtml__bookmark1775)

GUI  library  (actually  multiplatform).

## 54.1 See  also

See  also

#### 54.1.1 Wikibook

• Ada  Programming[5](#part0379.xhtml__bookmark1776)

• Ada  Programming/Libraries[6](#part0379.xhtml__bookmark1777)

#### 54.1.2 Ada  Reference  Manual

--  does  not  apply  --

#### 54.1.3 External  resources

• The  Big  Online  Book  of  Linux  Ada  Programming[7](#part0379.xhtml__bookmark1778)

• Ada  in  Debian  GNU/Linux[8](#part0379.xhtml__bookmark1779),  slides  suitable  for  a  50minute  presentation,  by  Ludovic  Brenta[9](#part0379.xhtml__bookmark1780).

![](Images/image07392.jpeg)

1 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FPOSIX](http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FPOSIX)

2 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FNcurses](http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FNcurses)

3 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FTexttools](http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FTexttools)

4 [http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGUI%2FGtkAda](http://en.wikibooks.org/wiki/Ada%20Programming%2FLibraries%2FGUI%2FGtkAda)

5 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

6 Chapter  [40](#part0333.xhtml__bookmark1359)  on  page  [331](#part0333.xhtml__bookmark1359)

7 [http://www.pegasoft.ca/resources/boblap/book.html](http://www.pegasoft.ca/resources/boblap/book.html)

8 [http://www.cs.kuleuven.be/~dirk/ada-belgium/events/06/060226-fosdem-4-ada-in-debian.](http://www.cs.kuleuven.be/~dirk/ada-belgium/events/06/060226-fosdem-4-ada-in-debian.pdf)  [pdf](http://www.cs.kuleuven.be/~dirk/ada-belgium/events/06/060226-fosdem-4-ada-in-debian.pdf)

9 [http://en.wikibooks.org/wiki/User%3ALudovic%20Brenta](http://en.wikibooks.org/wiki/User%3ALudovic%20Brenta)

# 55 Platform:  Windows

The  following  Libraries  and  Tools  help  you  when  you  target  the  MS-Windows  Platform.

GWindows[1](#part0381.xhtml__bookmark1783)  Win32  binding  CLAW[2](#part0381.xhtml__bookmark1784)

Another  Win32  binding  that  works  with  any  Ada  95  compiler.  An  introductory  edition  is  available  free  of  charge  for  non-commercial  use.

###### GNATCOM[3](#part0381.xhtml__bookmark1785)

COM/DCOM/ActiveX  binding

###### GNAVI[4](#part0381.xhtml__bookmark1786)

Visual  RAD[5](#part0381.xhtml__bookmark1787)  (Rapid  application  development[6](#part0381.xhtml__bookmark1788))  Development  environment

###### /Console/[7](#part0381.xhtml__bookmark1789)

Libraries  for  console  I/O.

###### /Visual  C++ -  GNAT  interface/[8](#part0381.xhtml__bookmark1790)

Guide  for calling  Ada functions  from  C++  using  GNAT  and Visual  C++.

## 55.1 See  also

See  also

#### 55.1.1 Wikibook

• Ada  Programming[9](#part0381.xhtml__bookmark1791)

• Ada  Programming/Libraries[10](#part0381.xhtml__bookmark1792)

#### 55.1.2 Ada  Reference  Manual

--  does  not  apply  --

1 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FWindows%2Fwin32binding](http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FWindows%2Fwin32binding)

2 [http://www.rrsoftware.com/html/prodinf/claw/claw.htm](http://www.rrsoftware.com/html/prodinf/claw/claw.htm)

3 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FWindows%2Fwin32binding](http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FWindows%2Fwin32binding)

4 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FWindows%2Fwin32binding](http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FWindows%2Fwin32binding)

5 [http://en.wikipedia.org/wiki/Rapid_application_development](http://en.wikipedia.org/wiki/Rapid_application_development)

6 [http://en.wikipedia.org/wiki/Rapid%20application%20development](http://en.wikipedia.org/wiki/Rapid%20application%20development)

7 [http://en.wikibooks.org/wiki/%2FConsole%2F](http://en.wikibooks.org/wiki/%2FConsole%2F)

8 [http://en.wikibooks.org/wiki/%2FVisual%20C%2B%2B%20-%20GNAT%20interface%2F](http://en.wikibooks.org/wiki/%2FVisual%20C%2B%2B%20-%20GNAT%20interface%2F)

9 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

10 Chapter  [40](#part0333.xhtml__bookmark1359)  on  page  [331](#part0333.xhtml__bookmark1359)

# 56 Platform:  Virtual  Machines

The  following  tools  help  you  when  you  target  a  virtual  machine.

###### Java[1](#part0383.xhtml__bookmark1795)

Programming  Ada  95  for  Java's  JVM  (JGnat,  AppletMagic)

###### .NET[2](#part0383.xhtml__bookmark1796)

Programming  Ada  for  the  .NET  Platform  (GNAT  Pro  .NET,  A#)

## 56.1 See  also

See  also

#### 56.1.1 Wikibook

• Ada  Programming[3](#part0383.xhtml__bookmark1797)

• Ada  Programming/Libraries[4](#part0383.xhtml__bookmark1798)

#### 56.1.2 Ada  Reference  Manual

--  does  not  apply  --

![](Images/image07393.jpeg)

1 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FVM%2FJava](http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FVM%2FJava)

2 [http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FVM%2FdotNET](http://en.wikibooks.org/wiki/Ada%20Programming%2FPlatform%2FVM%2FdotNET)

3 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

4 Chapter  [40](#part0333.xhtml__bookmark1359)  on  page  [331](#part0333.xhtml__bookmark1359)

# 57 Portals

## 57.1 Forges  of  open-source  projects

Forges  of  open-source  projects

###### SourceForge[1](#part0385.xhtml__bookmark1803)

Currently there are 200 Ada projects hosted at SourceForge — including the example  programs  for  Ada  Programming[2](#part0385.xhtml__bookmark1804)  wikibook.

###### GitHub[3](#part0385.xhtml__bookmark1805)

A  source  code  repository  based  on  Git  with  many  recent  developments.

###### Ada-centric  forges

There  are  some  Ada-centric  forges  hosted  by  Ada  associations  and  individuals:

• [http://forge.ada-ru.org](http://forge.ada-ru.org/)

• http://www.ada-france.org:8081

• [http://codelabs.ch](http://codelabs.ch/)

• [http://scm.ada.cx](http://scm.ada.cx/)

BerliOS[4](#part0385.xhtml__bookmark1806)

## 57.2 Directories  of  freely  available  tools  and  libraries

Directories  of  freely  available  tools  and  libraries

###### Ada  Information  Clearinghouse  —  Free  Tools  and  Libraries[5](#part0385.xhtml__bookmark1807)  Oloh  (  language  summary[6](#part0385.xhtml__bookmark1808),  ada  tag[7](#part0385.xhtml__bookmark1809),  language  search[8](#part0385.xhtml__bookmark1810))

Oloh  is  a  directory  of  Open  Source  projects.  Its  main  features  are  source  code  analysis  of  public  repositories  and  public  reviews  of  projects.

###### Freecode[9](#part0385.xhtml__bookmark1811)

Freecode,  formerly  Freshmeat.net,  is  a  software  directory  where  developers  can  register  their projects and users find interesting software.  Although the content is somewhat  redundant  to  other  portals,  some  projects  are  exclusively  listed  here.

## 57.3 Collections  of  Ada  source  code

![](Images/image07394.jpeg)

1 http://sourceforge.net/directory/language:ada/

2 [https://sourceforge.net/projects/wikibook-ada](https://sourceforge.net/projects/wikibook-ada)

3 [https://github.com/languages/Ada](https://github.com/languages/Ada)

4 [http://developer.berlios.de/softwaremap/trove_list.php?form_cat=52](http://developer.berlios.de/softwaremap/trove_list.php?form_cat=52)

5 [http://www.adaic.org/ada-resources/tools-libraries/](http://www.adaic.org/ada-resources/tools-libraries/)

6 [http://www.ohloh.net/languages/21](http://www.ohloh.net/languages/21)

7 [http://www.ohloh.net/tags/ada](http://www.ohloh.net/tags/ada)

8 [http://www.ohloh.net/p?page=3&q=language%3Aada&sort=relevance](http://www.ohloh.net/p?page=3&q=language%3Aada&sort=relevance)

9 [http://freecode.com/tags/ada?sort=vitality&with=&without=](http://freecode.com/tags/ada?sort=vitality&with&without)

Portals

Collections  of  Ada  source  code

###### AdaBasis[10](#part0386.xhtml__bookmark1813)

AdaBasis  consists  of  about  560  MB  of  public  domain  source  code  and  documents,  mainly  taken from the Public Ada Library (PAL). The software has been classified and is  presented in a hierarchical manner, separated in different application domains, and, for  some  domains,  with  an  additional  multi-faceted  searching  facility.

The intent is to provide students, teachers and researchers with a large collection of  reusable Ada components and systems for use in language and software engineering  courses.

AdaBasis was set up by the Programming Languages Group of the Institut für Informatik  at the University of Stuttgart, Germany. They plan to enlarge the library in the future,  and welcome free public domain contributions.  For more informations or to make  suggestions  please  contact  [adabasis@informatik.uni-stuttgart.de](mailto:adabasis@informatik.uni-stuttgart.de11)[11](#part0386.xhtml__bookmark1814)

###### The  Public  Ada  Library  (PAL)[12](#part0386.xhtml__bookmark1815)

The PAL is a library of Ada and VHDL software, information, and courseware that  contains  over  1  BILLION  bytes  of  material  (mainly  in  compressed  form).  All  items  in  the PAL have been released to the public with unlimited distribution, and, in most cases  (the  exceptions  are  shareware),  the  items  are  freeware.

###### [ftp

//ftp.cs.kuleuven.ac.be/pub/Ada-Belgium/cdrom/index.html Ada and Software Engi-  neering Library Version 2 (ASE2)] : The ASE2 Library contains over 1.1GB of material  on Ada and Software Engineering assembled through a collaboration with over 60 orga-  nizations. Walnut Creek CDROM once sold copies of this library. Nowadays it is no  longer maintained but is still hosted in the Ada Belgium FTP server. It may contain  useful  resources,  but  it  is  highly  redundant  with  other  libraries.

###### AdaPower[13](#part0386.xhtml__bookmark1816)

A  directory  and  collection  of  Ada  tools  and  resources.

## 57.4 See  also

See  also

#### 57.4.1 Wikibook

• Ada  Programming[14](#part0386.xhtml__bookmark1817)

• Ada  Programming/Tutorials[15](#part0386.xhtml__bookmark1818)

• Ada  Programming/Wikis[16](#part0386.xhtml__bookmark1819)

#### 57.4.2 Ada  Reference  Manual

--  does  not  apply  --

![](Images/image07395.jpeg)

10 [http://www.iste.uni-stuttgart.de/ps/adabasis.html](http://www.iste.uni-stuttgart.de/ps/adabasis.html)

11 [mailto:adabasis@informatik.uni-stuttgart.de](mailto:adabasis@informatik.uni-stuttgart.de)

12 [http://www2.informatik.uni-stuttgart.de/iste/ps/ada-software/html/PAL.html](http://www2.informatik.uni-stuttgart.de/iste/ps/ada-software/html/PAL.html)

13 [http://www.adapower.com/index.php?Command=Packages&Title=Packages+for+Reuse](http://www.adapower.com/index.php?Command=Packages&Title=Packages%2Bfor%2BReuse)

14 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

15 Chapter  [58](#part0389.xhtml__bookmark1820)  on  page  [387](#part0389.xhtml__bookmark1820)

16 [http://en.wikibooks.org/wiki/Ada%20Programming%2FWikis](http://en.wikibooks.org/wiki/Ada%20Programming%2FWikis)

384

#### 57.4.3 Ada  Quality  and  Style  Guide

--  does  not  apply  --

# 58Tutorials

This  page  contains  a  list  of  other  Ada  tutorials  on  the  Net.

1.  Ada Programming[1](#part0389.xhtml__bookmark1821), available on Wikibooks, is currently the only tutorial based on  the  Ada  2005[2](#part0389.xhtml__bookmark1822)  standard  and  currently  being  updated  to  Ada  2012[3](#part0389.xhtml__bookmark1823).
2.  Lovelace[4](#part0389.xhtml__bookmark1824) is a free (no-charge), self-directed Ada 95 tutorial available on the World  Wide Web (WWW). Lovelace assumes that the user already knows another algo-  rithmic  programming  language,  such  as  C,  C++,  or  Pascal.  Lovelace  is  interactive  and contains many short sections, most of which end with a question to help ensure  that users understand the material. Lovelace can be used directly from the WWW,  downloaded,  or  run  from  CD-ROM.  Lovelace  was  developed  by  David  A.  Wheeler.
3.  AdaTutor[5](#part0389.xhtml__bookmark1825) is an interactive Ada 95 tutorial distributed as a public-domain Ada  program.  A  web  edition[6](#part0389.xhtml__bookmark1826)  of  the  tutorial  is  also  available.
4.  The  Ada-95: A guide for C and C++ programmers[7](#part0389.xhtml__bookmark1827) is a short hypertext tutorial  for programmers who have a C or C++ style programming language background. It  was written by Simon Johnston, with some additional text by Tucker Taft.  PDF  edition[8](#part0389.xhtml__bookmark1828).
5.  Dale Stanbrough's Introduction[9](#part0389.xhtml__bookmark1829) is a set of notes that provide a simple introduction  to Ada. This material has been used for a few years as a simple introduction to the  language.
6.  Coronado  Enterprises  Ada  95  Tutorial: shareware  edition[10](#part0389.xhtml__bookmark1830), commercial  edition[11](#part0389.xhtml__bookmark1831).

![](Images/image07396.jpeg)

1 [http://en.wikibooks.org/wiki/Ada%20Programming](http://en.wikibooks.org/wiki/Ada%20Programming)

2 Chapter  [23](#part0221.xhtml__bookmark541)  on  page  [219](#part0221.xhtml__bookmark541)

3 [http://en.wikibooks.org/wiki/Ada%20Programming%2FAda%202012](http://en.wikibooks.org/wiki/Ada%20Programming%2FAda%202012)

4 [http://www.dwheeler.com/lovelace/](http://www.dwheeler.com/lovelace/)

5 [http://www.adatutor.com/](http://www.adatutor.com/)

6 [http://zhu-qy.blogspot.com.es/2012/08/adatutor.html](http://zhu-qy.blogspot.com.es/2012/08/adatutor.html)

7 [http://www.adahome.com/Ammo/Cplpl2Ada.html](http://www.adahome.com/Ammo/Cplpl2Ada.html)

8 [http://home.agh.edu.pl/~jpi/download/ada/guide-c2ada.pdf](http://home.agh.edu.pl/~jpi/download/ada/guide-c2ada.pdf)

9 [http://goanna.cs.rmit.edu.au/~dale/ada/aln.html](http://goanna.cs.rmit.edu.au/~dale/ada/aln.html)

10 [http://www.infres.enst.fr/~pautet/Ada95/a95list.htm](http://www.infres.enst.fr/~pautet/Ada95/a95list.htm)

11 [http://www.coronadoenterprises.com/tutorials/ada95/index.html](http://www.coronadoenterprises.com/tutorials/ada95/index.html)

# 59Web  2.0

Here  is  a  list  of  Web  2.0[1](#part0391.xhtml__bookmark1833)  resources  about  Ada:

#### 59.0.4 News  &  Blogs

• reddit.com  —  Ada[2](#part0391.xhtml__bookmark1834)  [  RSS[3](#part0391.xhtml__bookmark1835)],  social  news  website  on  which  users  can  post  links  to  content  on  the  web

• Ada  Gems[4](#part0391.xhtml__bookmark1836)  [  RSS[5](#part0391.xhtml__bookmark1837)],  programming  tips  and  articles  about  specific  language  features

• Planet  Ada[6](#part0391.xhtml__bookmark1838)  [  RSS[7](#part0391.xhtml__bookmark1839)],  an  aggregate  feed  of  mostly  Ada-related  blogs.

• Ada  Programming  blog[8](#part0391.xhtml__bookmark1840)  [  RSS[9](#part0391.xhtml__bookmark1841)],  by  Martin  Krischik  and  other  authors

• Kickin'  the  Darkness[10](#part0391.xhtml__bookmark1842)  [  RSS[11](#part0391.xhtml__bookmark1843)],  by  Marc  A.  Criley

• Archeia[12](#part0391.xhtml__bookmark1844)  [  RSS[13](#part0391.xhtml__bookmark1845)],  by  Lucretia

• Pragmatic  Revelations[14](#part0391.xhtml__bookmark1846)  [  RSS[15](#part0391.xhtml__bookmark1847)]

#### 59.0.5 Forums  &  developer  rings

• Stack  Overflow  —  Ada  questions[16](#part0391.xhtml__bookmark1848)

• Linked  In  —  Ada  developers  group[17](#part0391.xhtml__bookmark1849)  (free  register  needed)

• Tek-Tips  —  Ada  Forum[18](#part0391.xhtml__bookmark1850)

![](Images/image07397.jpeg)

1 [http://en.wikipedia.org/wiki/Web%202.0](http://en.wikipedia.org/wiki/Web%202.0)

2 [http://www.reddit.com/r/ada/](http://www.reddit.com/r/ada/)

3 [http://www.reddit.com/r/ada/.rss](http://www.reddit.com/r/ada/.rss)

4 [http://www.adacore.com/category/developers-center/gems/](http://www.adacore.com/category/developers-center/gems/)

5 [http://www.adacore.com/rss/gems](http://www.adacore.com/rss/gems)

6 [http://planet.ada.cx/](http://planet.ada.cx/)

7 [http://planet.ada.cx/rss20.xml](http://planet.ada.cx/rss20.xml)

8 [http://ada-programming.blogspot.com/](http://ada-programming.blogspot.com/)

9 [http://ada-programming.blogspot.com/feeds/posts/default](http://ada-programming.blogspot.com/feeds/posts/default)

10 [http://blog.kickin-the-darkness.com/search/label/Ada](http://blog.kickin-the-darkness.com/search/label/Ada)

11 [http://blog.kickin-the-darkness.com/feeds/posts/default](http://blog.kickin-the-darkness.com/feeds/posts/default)

12 [http://www.archeia.com/](http://www.archeia.com/)

13 [http://www.archeia.com/rss_feed.html](http://www.archeia.com/rss_feed.html)

14 [http://adrianhoe.com/adrianhoe/category/software_development/ada/](http://adrianhoe.com/adrianhoe/category/software_development/ada/)

15 [http://adrianhoe.com/adrianhoe/feed/rss/](http://adrianhoe.com/adrianhoe/feed/rss/)

16 [http://stackoverflow.com/questions/tagged/ada](http://stackoverflow.com/questions/tagged/ada)

17 [http://www.linkedin.com/groups?gid=114211](http://www.linkedin.com/groups?gid=114211)

18 [http://www.tek-tips.com/threadminder.cfm?pid=199](http://www.tek-tips.com/threadminder.cfm?pid=199)

Web  2.0

#### 59.0.6 General  Info

• SlideShare[19](#part0392.xhtml__bookmark1851),  presentations  about  Ada[20](#part0392.xhtml__bookmark1852).  See  also: Ada  programming[21](#part0392.xhtml__bookmark1853), Ada  95[22](#part0392.xhtml__bookmark1854),  Ada  2005[23](#part0392.xhtml__bookmark1855),  Ada  2012[24](#part0392.xhtml__bookmark1856)  tag  pages.

• Ohloh[25](#part0392.xhtml__bookmark1857),  a  directory  of  Open  Source  projects. Its  main  features  are  source  code  analysis[26](#part0392.xhtml__bookmark1858)  of  public  repositories  and  public  reviews  of  projects

• Ada  Commons[27](#part0392.xhtml__bookmark1859),  wiki  for  Ada  developers

• Ada@Krischik[28](#part0392.xhtml__bookmark1860),  Ada  homepage  of  Martin  Krischik

• WikiCFP  —  Calls  For  Papers  on  Ada[29](#part0392.xhtml__bookmark1861)  [  RSS[30](#part0392.xhtml__bookmark1862)]

• AdaCore  channel  on  youtube.com[31](#part0392.xhtml__bookmark1863),  Ada  related  videos.

#### 59.0.7 Wikimedia  projects

• Wikipedia  articles  (Ada  category[32](#part0392.xhtml__bookmark1864)):

• Ada[33](#part0392.xhtml__bookmark1865)

• Jean  Ichbiah[34](#part0392.xhtml__bookmark1866)

• Beaujolais  effect[35](#part0392.xhtml__bookmark1867)

• ISO  8652[36](#part0392.xhtml__bookmark1868)

• Ada  Semantic  Interface  Specification[37](#part0392.xhtml__bookmark1869)

• ...

###### • Wiktionary  entries:

• ACATS[38](#part0392.xhtml__bookmark1870)

• Ada[39](#part0392.xhtml__bookmark1871)

• ASIS[40](#part0392.xhtml__bookmark1872)

###### • Wikisource  documents:

• Steelman language  requirements[41](#part0392.xhtml__bookmark1873)

• Stoneman  requirements[42](#part0392.xhtml__bookmark1874)

###### • Wikibooks  tutorials:

![](Images/image07398.jpeg)

19 [http://www.slideshare.net/](http://www.slideshare.net/)

20 [http://www.slideshare.net/group/ada-programming/slideshows](http://www.slideshare.net/group/ada-programming/slideshows)

21 [http://www.slideshare.net/tag/ada-programming](http://www.slideshare.net/tag/ada-programming)

22 [http://www.slideshare.net/tag/ada-95](http://www.slideshare.net/tag/ada-95)

23 [http://www.slideshare.net/tag/ada-2005](http://www.slideshare.net/tag/ada-2005)

24 [http://www.slideshare.net/tag/ada-2012](http://www.slideshare.net/tag/ada-2012)

25 [http://www.ohloh.net/tags/ada](http://www.ohloh.net/tags/ada)

26 [http://www.ohloh.net/languages/21](http://www.ohloh.net/languages/21)

27 [http://commons.ada.cx](http://commons.ada.cx/)

28 [http://ada.krischik.com](http://ada.krischik.com/)

29 [http://www.wikicfp.com/cfp/call?conference=ada](http://www.wikicfp.com/cfp/call?conference=ada)

30 [http://www.wikicfp.com/cfp/rss?cat=ada](http://www.wikicfp.com/cfp/rss?cat=ada)

31 [http://www.youtube.com/user/AdaCore05](http://www.youtube.com/user/AdaCore05)

32 [http://en.wikipedia.org/wiki/Category%3AAda%20programming%20language](http://en.wikipedia.org/wiki/Category%3AAda%20programming%20language)

33 [http://en.wikipedia.org/wiki/Ada%20%28programming%20language%29](http://en.wikipedia.org/wiki/Ada%20%28programming%20language%29)

34 [http://en.wikipedia.org/wiki/Jean%20Ichbiah](http://en.wikipedia.org/wiki/Jean%20Ichbiah)

35 [http://en.wikipedia.org/wiki/Beaujolais%20effect](http://en.wikipedia.org/wiki/Beaujolais%20effect)

36 [http://en.wikipedia.org/wiki/ISO%208652](http://en.wikipedia.org/wiki/ISO%208652)

37 [http://en.wikipedia.org/wiki/Ada%20Semantic%20Interface%20Specification](http://en.wikipedia.org/wiki/Ada%20Semantic%20Interface%20Specification)

38 [http://en.wiktionary.org/wiki/ACATS](http://en.wiktionary.org/wiki/ACATS)

39 [http://en.wiktionary.org/wiki/Ada](http://en.wiktionary.org/wiki/Ada)

40 [http://en.wiktionary.org/wiki/ASIS](http://en.wiktionary.org/wiki/ASIS)

41 [http://en.wikisource.org/wiki/Steelman%20language%20requirements](http://en.wikisource.org/wiki/Steelman%20language%20requirements)

42 [http://en.wikisource.org/wiki/Stoneman%20requirements](http://en.wikisource.org/wiki/Stoneman%20requirements)

• Programación  en  Ada[43](#part0393.xhtml__bookmark1875),  in  Spanish

• Programmation Ada[44](#part0393.xhtml__bookmark1876),  in  French

• Ada[45](#part0393.xhtml__bookmark1877),  in  Italian

###### • Wikiquote:

• Programming  languages  —  Ada[46](#part0393.xhtml__bookmark1878)

###### • Wikiversity:

• Ada  course[47](#part0393.xhtml__bookmark1879)  (you  can  enroll!)

#### 59.0.8 Source  code

• Examples  Ada  Programming  wikibook[48](#part0393.xhtml__bookmark1880)

• Rosetta  Code  —  Ada  Category[49](#part0393.xhtml__bookmark1881),  programming  examples  in  multiple  languages

• literateprograms.org  —  Ada  Category[50](#part0393.xhtml__bookmark1882),  examples  of  literate  programming[51](#part0393.xhtml__bookmark1883)  in  multi-  ple  languages

#### 59.0.9 Projects

• AdaCL[52](#part0393.xhtml__bookmark1884)

• The  Ada  95  Booch  Components[53](#part0393.xhtml__bookmark1885)

• The  GNU  Ada  Compiler[54](#part0393.xhtml__bookmark1886)

• ASIS[55](#part0393.xhtml__bookmark1887)

• GLADE[56](#part0393.xhtml__bookmark1888)

• Florist[57](#part0393.xhtml__bookmark1889)

• GNAT  —  GCC  Wiki[58](#part0393.xhtml__bookmark1890)

• RTEMSAda[59](#part0393.xhtml__bookmark1891)

• AVR-Ada[60](#part0393.xhtml__bookmark1892)  -  Ada  compiler  for  Atmel  microcontrollers  (Arduinos)  Web  2.0[61](#part0393.xhtml__bookmark1893)

![](Images/image07399.jpeg)

43 [http://en.wikibooks.org/wiki/%3Aes%3AProgramaci%F3n_en_Ada](http://en.wikibooks.org/wiki/%3Aes%3AProgramaci%F3n_en_Ada)

44 [http://en.wikibooks.org/wiki/%3Afr%3AProgrammation_Ada](http://en.wikibooks.org/wiki/%3Afr%3AProgrammation_Ada)

45 [http://en.wikibooks.org/wiki/%3Ait%3AAda](http://en.wikibooks.org/wiki/%3Ait%3AAda)

46 [http://en.wikiquote.org/wiki/Programming_languages#Ada](http://en.wikiquote.org/wiki/Programming_languages#Ada)

47 [http://en.wikiversity.org/wiki/Ada](http://en.wikiversity.org/wiki/Ada)

48 [http://wikibook-ada.sourceforge.net](http://wikibook-ada.sourceforge.net/)

49 [http://www.rosettacode.org/wiki/Ada](http://www.rosettacode.org/wiki/Ada)

50 http://en.literateprograms.org/Category:Programming_language:Ada

51 [http://en.wikipedia.org/wiki/literate%20programming](http://en.wikipedia.org/wiki/literate%20programming)

52 [http://adacl.sourceforge.net/index.php](http://adacl.sourceforge.net/index.php)

53 [http://booch95.sourceforge.net/pmwiki.php](http://booch95.sourceforge.net/pmwiki.php)

54 [http://gnuada.sourceforge.net](http://gnuada.sourceforge.net/)

55 [http://gnat-asis.sourceforge.net](http://gnat-asis.sourceforge.net/)

56 [http://gnat-glade.sourceforge.net](http://gnat-glade.sourceforge.net/)

57 [http://gnat-florist.sourceforge.net](http://gnat-florist.sourceforge.net/)

58 [http://gcc.gnu.org/wiki/GNAT](http://gcc.gnu.org/wiki/GNAT)

59 [http://www.rtems.com/wiki/index.php/RTEMSAda](http://www.rtems.com/wiki/index.php/RTEMSAda)

60 [http://avr-ada.sourceforge.net/](http://avr-ada.sourceforge.net/)

61 [http://en.wikibooks.org/wiki/Category%3AAda%20Programming](http://en.wikibooks.org/wiki/Category%3AAda%20Programming)

# 60Contributors

###### EditsUser

1A10112[1](#part0000.xhtml__bookmark0)

1ALK[2](#part0000.xhtml__bookmark0)

1AdRiley[3](#part0000.xhtml__bookmark0)

64Adrignola[4](#part0000.xhtml__bookmark0)

1 Alan.poindexter[5](#part0000.xhtml__bookmark0)

2 Alisonken1[6](#part0000.xhtml__bookmark0)

1Ammon[7](#part0000.xhtml__bookmark0)

1Andreas  Ipp[8](#part0000.xhtml__bookmark0)

1Aramael[9](#part0000.xhtml__bookmark0)

1Arny[10](#part0000.xhtml__bookmark0)

1Arthurvogel[11](#part0000.xhtml__bookmark0)

7Avicennasis[12](#part0000.xhtml__bookmark0)

1Benjstarratt[13](#part0000.xhtml__bookmark0)

14Carsrac[14](#part0000.xhtml__bookmark0)

56CarsracBot[15](#part0000.xhtml__bookmark0)

1 Chouclac[16](#part0000.xhtml__bookmark0)

2 Cspurrier[17](#part0000.xhtml__bookmark0)

44Darklama[18](#part0000.xhtml__bookmark0)

3David  Hoos[19](#part0000.xhtml__bookmark0)

3Derbeth[20](#part0000.xhtml__bookmark0)

1Dhenry[21](#part0000.xhtml__bookmark0)

![](Images/image07400.jpeg)

1 [http://en.wikibooks.org/w/index.php?title=User:A10112](http://en.wikibooks.org/w/index.php?title=User%3AA10112)

2 [http://en.wikibooks.org/w/index.php?title=User:ALK](http://en.wikibooks.org/w/index.php?title=User%3AALK)

3 [http://en.wikibooks.org/w/index.php?title=User:AdRiley](http://en.wikibooks.org/w/index.php?title=User%3AAdRiley)

4 [http://en.wikibooks.org/w/index.php?title=User:Adrignola](http://en.wikibooks.org/w/index.php?title=User%3AAdrignola)

5 [http://en.wikibooks.org/w/index.php?title=User:Alan.poindexter](http://en.wikibooks.org/w/index.php?title=User%3AAlan.poindexter)

6 [http://en.wikibooks.org/w/index.php?title=User:Alisonken1](http://en.wikibooks.org/w/index.php?title=User%3AAlisonken1)

7 [http://en.wikibooks.org/w/index.php?title=User:Ammon](http://en.wikibooks.org/w/index.php?title=User%3AAmmon)

8 [http://en.wikibooks.org/w/index.php?title=User:Andreas_Ipp](http://en.wikibooks.org/w/index.php?title=User%3AAndreas_Ipp)

9 [http://en.wikibooks.org/w/index.php?title=User:Aramael](http://en.wikibooks.org/w/index.php?title=User%3AAramael)

10 [http://en.wikibooks.org/w/index.php?title=User:Arny](http://en.wikibooks.org/w/index.php?title=User%3AArny)

11 [http://en.wikibooks.org/w/index.php?title=User:Arthurvogel](http://en.wikibooks.org/w/index.php?title=User%3AArthurvogel)

12 [http://en.wikibooks.org/w/index.php?title=User:Avicennasis](http://en.wikibooks.org/w/index.php?title=User%3AAvicennasis)

13 [http://en.wikibooks.org/w/index.php?title=User:Benjstarratt](http://en.wikibooks.org/w/index.php?title=User%3ABenjstarratt)

14 [http://en.wikibooks.org/w/index.php?title=User:Carsrac](http://en.wikibooks.org/w/index.php?title=User%3ACarsrac)

15 [http://en.wikibooks.org/w/index.php?title=User:CarsracBot](http://en.wikibooks.org/w/index.php?title=User%3ACarsracBot)

16 [http://en.wikibooks.org/w/index.php?title=User:Chouclac](http://en.wikibooks.org/w/index.php?title=User%3AChouclac)

17 [http://en.wikibooks.org/w/index.php?title=User:Cspurrier](http://en.wikibooks.org/w/index.php?title=User%3ACspurrier)

18 [http://en.wikibooks.org/w/index.php?title=User:Darklama](http://en.wikibooks.org/w/index.php?title=User%3ADarklama)

19 [http://en.wikibooks.org/w/index.php?title=User:David_Hoos](http://en.wikibooks.org/w/index.php?title=User%3ADavid_Hoos)

20 [http://en.wikibooks.org/w/index.php?title=User:Derbeth](http://en.wikibooks.org/w/index.php?title=User%3ADerbeth)

21 [http://en.wikibooks.org/w/index.php?title=User:Dhenry](http://en.wikibooks.org/w/index.php?title=User%3ADhenry)

12Dirk  Hünniger[22](#part0000.xhtml__bookmark0)

2Dmitry-kazakov[23](#part0000.xhtml__bookmark0)

1 Doug[24](#part0000.xhtml__bookmark0)

2 DougP[25](#part0000.xhtml__bookmark0)

17Dragontamer[26](#part0000.xhtml__bookmark0)

1Fraterm[27](#part0000.xhtml__bookmark0)

1Friess[28](#part0000.xhtml__bookmark0)

1Frikk[29](#part0000.xhtml__bookmark0)

1 Frodet[30](#part0000.xhtml__bookmark0)

2 Geocachernemesis[31](#part0000.xhtml__bookmark0)

97GeorgBauhaus[32](#part0000.xhtml__bookmark0)

8Godunko[33](#part0000.xhtml__bookmark0)

1Hagindaz[34](#part0000.xhtml__bookmark0)

1 Herbythyme[35](#part0000.xhtml__bookmark0)

2 JMatthews[36](#part0000.xhtml__bookmark0)

3 James  Dennett[37](#part0000.xhtml__bookmark0)

1Jclee[38](#part0000.xhtml__bookmark0)

1Jcreem[39](#part0000.xhtml__bookmark0)

1Jeffinous[40](#part0000.xhtml__bookmark0)

5Jesselang[41](#part0000.xhtml__bookmark0)

34Jguk[42](#part0000.xhtml__bookmark0)

1 Jlaire[43](#part0000.xhtml__bookmark0)

2 Jlenthe[44](#part0000.xhtml__bookmark0)

4Jomegat[45](#part0000.xhtml__bookmark0)

1Kayau[46](#part0000.xhtml__bookmark0)

![](Images/image07401.jpeg)

22 [http://en.wikibooks.org/w/index.php?title=User:Dirk_H%C3%BCnniger](http://en.wikibooks.org/w/index.php?title=User%3ADirk_H%C3%BCnniger)

23 [http://en.wikibooks.org/w/index.php?title=User:Dmitry-kazakov](http://en.wikibooks.org/w/index.php?title=User%3ADmitry-kazakov)

24 [http://en.wikibooks.org/w/index.php?title=User:Doug](http://en.wikibooks.org/w/index.php?title=User%3ADoug)

25 [http://en.wikibooks.org/w/index.php?title=User:DougP](http://en.wikibooks.org/w/index.php?title=User%3ADougP)

26 [http://en.wikibooks.org/w/index.php?title=User:Dragontamer](http://en.wikibooks.org/w/index.php?title=User%3ADragontamer)

27 [http://en.wikibooks.org/w/index.php?title=User:Fraterm](http://en.wikibooks.org/w/index.php?title=User%3AFraterm)

28 [http://en.wikibooks.org/w/index.php?title=User:Friess](http://en.wikibooks.org/w/index.php?title=User%3AFriess)

29 [http://en.wikibooks.org/w/index.php?title=User:Frikk](http://en.wikibooks.org/w/index.php?title=User%3AFrikk)

30 [http://en.wikibooks.org/w/index.php?title=User:Frodet](http://en.wikibooks.org/w/index.php?title=User%3AFrodet)

31 [http://en.wikibooks.org/w/index.php?title=User:Geocachernemesis](http://en.wikibooks.org/w/index.php?title=User%3AGeocachernemesis)

32 [http://en.wikibooks.org/w/index.php?title=User:GeorgBauhaus](http://en.wikibooks.org/w/index.php?title=User%3AGeorgBauhaus)

33 [http://en.wikibooks.org/w/index.php?title=User:Godunko](http://en.wikibooks.org/w/index.php?title=User%3AGodunko)

34 [http://en.wikibooks.org/w/index.php?title=User:Hagindaz](http://en.wikibooks.org/w/index.php?title=User%3AHagindaz)

35 [http://en.wikibooks.org/w/index.php?title=User:Herbythyme](http://en.wikibooks.org/w/index.php?title=User%3AHerbythyme)

36 [http://en.wikibooks.org/w/index.php?title=User:JMatthews](http://en.wikibooks.org/w/index.php?title=User%3AJMatthews)

37 [http://en.wikibooks.org/w/index.php?title=User:James_Dennett](http://en.wikibooks.org/w/index.php?title=User%3AJames_Dennett)

38 [http://en.wikibooks.org/w/index.php?title=User:Jclee](http://en.wikibooks.org/w/index.php?title=User%3AJclee)

39 [http://en.wikibooks.org/w/index.php?title=User:Jcreem](http://en.wikibooks.org/w/index.php?title=User%3AJcreem)

40 [http://en.wikibooks.org/w/index.php?title=User:Jeffinous](http://en.wikibooks.org/w/index.php?title=User%3AJeffinous)

41 [http://en.wikibooks.org/w/index.php?title=User:Jesselang](http://en.wikibooks.org/w/index.php?title=User%3AJesselang)

42 [http://en.wikibooks.org/w/index.php?title=User:Jguk](http://en.wikibooks.org/w/index.php?title=User%3AJguk)

43 [http://en.wikibooks.org/w/index.php?title=User:Jlaire](http://en.wikibooks.org/w/index.php?title=User%3AJlaire)

44 [http://en.wikibooks.org/w/index.php?title=User:Jlenthe](http://en.wikibooks.org/w/index.php?title=User%3AJlenthe)

45 [http://en.wikibooks.org/w/index.php?title=User:Jomegat](http://en.wikibooks.org/w/index.php?title=User%3AJomegat)

46 [http://en.wikibooks.org/w/index.php?title=User:Kayau](http://en.wikibooks.org/w/index.php?title=User%3AKayau)

1102Krischik[47](#part0000.xhtml__bookmark0)

1Kwhitefoot[48](#part0000.xhtml__bookmark0)

16Larry  Luther[49](#part0000.xhtml__bookmark0)

3LesmanaZimmer[50](#part0000.xhtml__bookmark0)

1Lincher[51](#part0000.xhtml__bookmark0)

1Lodacom[52](#part0000.xhtml__bookmark0)

118Ludovic  Brenta[53](#part0000.xhtml__bookmark0)

1 Maciej Sobczak[54](#part0000.xhtml__bookmark0)

2 Mahanga[55](#part0000.xhtml__bookmark0)

463ManuelGR[56](#part0000.xhtml__bookmark0)

4Mike.lifeguard[57](#part0000.xhtml__bookmark0)

2Moskvax[58](#part0000.xhtml__bookmark0)

5Nikai[59](#part0000.xhtml__bookmark0)

2Okellogg[60](#part0000.xhtml__bookmark0)

6Oleszkie[61](#part0000.xhtml__bookmark0)

8Panic2k4[62](#part0000.xhtml__bookmark0)

1Panzon[63](#part0000.xhtml__bookmark0)

1 Parallelized[64](#part0000.xhtml__bookmark0)

2 Paxton[65](#part0000.xhtml__bookmark0)

1Per.sandberg[66](#part0000.xhtml__bookmark0)

1QuiteUnusual[67](#part0000.xhtml__bookmark0)

1 RamaccoloBot[68](#part0000.xhtml__bookmark0)

2 Randhol[69](#part0000.xhtml__bookmark0)

1Recent  Runes[70](#part0000.xhtml__bookmark0)

1Red4tribe[71](#part0000.xhtml__bookmark0)

![](Images/image07402.jpeg)

47 [http://en.wikibooks.org/w/index.php?title=User:Krischik](http://en.wikibooks.org/w/index.php?title=User%3AKrischik)

48 [http://en.wikibooks.org/w/index.php?title=User:Kwhitefoot](http://en.wikibooks.org/w/index.php?title=User%3AKwhitefoot)

49 [http://en.wikibooks.org/w/index.php?title=User:Larry_Luther](http://en.wikibooks.org/w/index.php?title=User%3ALarry_Luther)

50 [http://en.wikibooks.org/w/index.php?title=User:LesmanaZimmer](http://en.wikibooks.org/w/index.php?title=User%3ALesmanaZimmer)

51 [http://en.wikibooks.org/w/index.php?title=User:Lincher](http://en.wikibooks.org/w/index.php?title=User%3ALincher)

52 [http://en.wikibooks.org/w/index.php?title=User:Lodacom](http://en.wikibooks.org/w/index.php?title=User%3ALodacom)

53 [http://en.wikibooks.org/w/index.php?title=User:Ludovic_Brenta](http://en.wikibooks.org/w/index.php?title=User%3ALudovic_Brenta)

54 [http://en.wikibooks.org/w/index.php?title=User:Maciej_Sobczak](http://en.wikibooks.org/w/index.php?title=User%3AMaciej_Sobczak)

55 [http://en.wikibooks.org/w/index.php?title=User:Mahanga](http://en.wikibooks.org/w/index.php?title=User%3AMahanga)

56 [http://en.wikibooks.org/w/index.php?title=User:ManuelGR](http://en.wikibooks.org/w/index.php?title=User%3AManuelGR)

57 [http://en.wikibooks.org/w/index.php?title=User:Mike.lifeguard](http://en.wikibooks.org/w/index.php?title=User%3AMike.lifeguard)

58 [http://en.wikibooks.org/w/index.php?title=User:Moskvax](http://en.wikibooks.org/w/index.php?title=User%3AMoskvax)

59 [http://en.wikibooks.org/w/index.php?title=User:Nikai](http://en.wikibooks.org/w/index.php?title=User%3ANikai)

60 [http://en.wikibooks.org/w/index.php?title=User:Okellogg](http://en.wikibooks.org/w/index.php?title=User%3AOkellogg)

61 [http://en.wikibooks.org/w/index.php?title=User:Oleszkie](http://en.wikibooks.org/w/index.php?title=User%3AOleszkie)

62 [http://en.wikibooks.org/w/index.php?title=User:Panic2k4](http://en.wikibooks.org/w/index.php?title=User%3APanic2k4)

63 [http://en.wikibooks.org/w/index.php?title=User:Panzon](http://en.wikibooks.org/w/index.php?title=User%3APanzon)

64 [http://en.wikibooks.org/w/index.php?title=User:Parallelized](http://en.wikibooks.org/w/index.php?title=User%3AParallelized)

65 [http://en.wikibooks.org/w/index.php?title=User:Paxton](http://en.wikibooks.org/w/index.php?title=User%3APaxton)

66 [http://en.wikibooks.org/w/index.php?title=User:Per.sandberg](http://en.wikibooks.org/w/index.php?title=User%3APer.sandberg)

67 [http://en.wikibooks.org/w/index.php?title=User:QuiteUnusual](http://en.wikibooks.org/w/index.php?title=User%3AQuiteUnusual)

68 [http://en.wikibooks.org/w/index.php?title=User:RamaccoloBot](http://en.wikibooks.org/w/index.php?title=User%3ARamaccoloBot)

69 [http://en.wikibooks.org/w/index.php?title=User:Randhol](http://en.wikibooks.org/w/index.php?title=User%3ARandhol)

70 [http://en.wikibooks.org/w/index.php?title=User:Recent_Runes](http://en.wikibooks.org/w/index.php?title=User%3ARecent_Runes)

71 [http://en.wikibooks.org/w/index.php?title=User:Red4tribe](http://en.wikibooks.org/w/index.php?title=User%3ARed4tribe)

5Robert  Horning[72](#part0000.xhtml__bookmark0)

1Rosen[73](#part0000.xhtml__bookmark0)

1Rursus[74](#part0000.xhtml__bookmark0)

3SQL[75](#part0000.xhtml__bookmark0)

2Sam[76](#part0000.xhtml__bookmark0)

5Sjw[77](#part0000.xhtml__bookmark0)

1Sparre[78](#part0000.xhtml__bookmark0)

5Spongebob88[79](#part0000.xhtml__bookmark0)

1 Stephen leake[80](#part0000.xhtml__bookmark0)  711Suruena[81](#part0000.xhtml__bookmark0)

2 Swhalen[82](#part0000.xhtml__bookmark0)

2 The  bellman[83](#part0000.xhtml__bookmark0)

3 Thenub314[84](#part0000.xhtml__bookmark0)

3Tkoskine[85](#part0000.xhtml__bookmark0)

1Tobias  Bergemann[86](#part0000.xhtml__bookmark0)

1Van  der  Hoorn[87](#part0000.xhtml__bookmark0)

3Venullian[88](#part0000.xhtml__bookmark0)

5VillemtheVillain![89](#part0000.xhtml__bookmark0)

1Vito  Genovese[90](#part0000.xhtml__bookmark0)

1Warinthepocket[91](#part0000.xhtml__bookmark0)

3WhirlWind[92](#part0000.xhtml__bookmark0)

1Wikibob[93](#part0000.xhtml__bookmark0)

1Xania[94](#part0000.xhtml__bookmark0)

1robot[95](#part0000.xhtml__bookmark0)

![](Images/image07403.jpeg)

72 [http://en.wikibooks.org/w/index.php?title=User:Robert_Horning](http://en.wikibooks.org/w/index.php?title=User%3ARobert_Horning)

73 [http://en.wikibooks.org/w/index.php?title=User:Rosen](http://en.wikibooks.org/w/index.php?title=User%3ARosen)

74 [http://en.wikibooks.org/w/index.php?title=User:Rursus](http://en.wikibooks.org/w/index.php?title=User%3ARursus)

75 [http://en.wikibooks.org/w/index.php?title=User:SQL](http://en.wikibooks.org/w/index.php?title=User%3ASQL)

76 [http://en.wikibooks.org/w/index.php?title=User:Sam](http://en.wikibooks.org/w/index.php?title=User%3ASam)

77 [http://en.wikibooks.org/w/index.php?title=User:Sjw](http://en.wikibooks.org/w/index.php?title=User%3ASjw)

78 [http://en.wikibooks.org/w/index.php?title=User:Sparre](http://en.wikibooks.org/w/index.php?title=User%3ASparre)

79 [http://en.wikibooks.org/w/index.php?title=User:Spongebob88](http://en.wikibooks.org/w/index.php?title=User%3ASpongebob88)

80 [http://en.wikibooks.org/w/index.php?title=User:Stephen_leake](http://en.wikibooks.org/w/index.php?title=User%3AStephen_leake)

81 [http://en.wikibooks.org/w/index.php?title=User:Suruena](http://en.wikibooks.org/w/index.php?title=User%3ASuruena)

82 [http://en.wikibooks.org/w/index.php?title=User:Swhalen](http://en.wikibooks.org/w/index.php?title=User%3ASwhalen)

83 [http://en.wikibooks.org/w/index.php?title=User:The_bellman](http://en.wikibooks.org/w/index.php?title=User%3AThe_bellman)

84 [http://en.wikibooks.org/w/index.php?title=User:Thenub314](http://en.wikibooks.org/w/index.php?title=User%3AThenub314)

85 [http://en.wikibooks.org/w/index.php?title=User:Tkoskine](http://en.wikibooks.org/w/index.php?title=User%3ATkoskine)

86 [http://en.wikibooks.org/w/index.php?title=User:Tobias_Bergemann](http://en.wikibooks.org/w/index.php?title=User%3ATobias_Bergemann)

87 [http://en.wikibooks.org/w/index.php?title=User:Van_der_Hoorn](http://en.wikibooks.org/w/index.php?title=User%3AVan_der_Hoorn)

88 [http://en.wikibooks.org/w/index.php?title=User:Venullian](http://en.wikibooks.org/w/index.php?title=User%3AVenullian)

89 [http://en.wikibooks.org/w/index.php?title=User:VillemtheVillain%21](http://en.wikibooks.org/w/index.php?title=User%3AVillemtheVillain%21)

90 [http://en.wikibooks.org/w/index.php?title=User:Vito_Genovese](http://en.wikibooks.org/w/index.php?title=User%3AVito_Genovese)

91 [http://en.wikibooks.org/w/index.php?title=User:Warinthepocket](http://en.wikibooks.org/w/index.php?title=User%3AWarinthepocket)

92 [http://en.wikibooks.org/w/index.php?title=User:WhirlWind](http://en.wikibooks.org/w/index.php?title=User%3AWhirlWind)

93 [http://en.wikibooks.org/w/index.php?title=User:Wikibob](http://en.wikibooks.org/w/index.php?title=User%3AWikibob)

94 [http://en.wikibooks.org/w/index.php?title=User:Xania](http://en.wikibooks.org/w/index.php?title=User%3AXania)

95 [http://en.wikibooks.org/w/index.php?title=User:%E3%82%BF%E3%83%81%E3%82%B3%E3%83%9E_](http://en.wikibooks.org/w/index.php?title=User%3A%E3%82%BF%E3%83%81%E3%82%B3%E3%83%9E_robot)  [robot](http://en.wikibooks.org/w/index.php?title=User%3A%E3%82%BF%E3%83%81%E3%82%B3%E3%83%9E_robot)

# List  of  Figures

– GFDL:  Gnu  Free  Documentation  License.  [http://www.gnu.org/licenses/fdl.](http://www.gnu.org/licenses/fdl.html)  [html](http://www.gnu.org/licenses/fdl.html)

– cc-by-sa-3.0:  Creative  Commons  Attribution  ShareAlike  3.0  License.  [http://](http://creativecommons.org/licenses/by-sa/3.0/)  [creativecommons.org/licenses/by-sa/3.0/](http://creativecommons.org/licenses/by-sa/3.0/)

– cc-by-sa-2.5:  Creative  Commons  Attribution  ShareAlike  2.5  License.  [http://](http://creativecommons.org/licenses/by-sa/2.5/)  [creativecommons.org/licenses/by-sa/2.5/](http://creativecommons.org/licenses/by-sa/2.5/)

– cc-by-sa-2.0:  Creative  Commons  Attribution  ShareAlike  2.0  License.  [http://](http://creativecommons.org/licenses/by-sa/2.0/)  [creativecommons.org/licenses/by-sa/2.0/](http://creativecommons.org/licenses/by-sa/2.0/)

– cc-by-sa-1.0:  Creative  Commons  Attribution  ShareAlike  1.0  License.  [http://](http://creativecommons.org/licenses/by-sa/1.0/)  [creativecommons.org/licenses/by-sa/1.0/](http://creativecommons.org/licenses/by-sa/1.0/)

– cc-by-2.0:  Creative  Commons  Attribution  2.0  License.  [http://creativecommons.](http://creativecommons.org/licenses/by/2.0/)  [org/licenses/by/2.0/](http://creativecommons.org/licenses/by/2.0/)

– cc-by-2.0:  Creative  Commons  Attribution  2.0  License.  [http://creativecommons.](http://creativecommons.org/licenses/by/2.0/deed.en)  [org/licenses/by/2.0/deed.en](http://creativecommons.org/licenses/by/2.0/deed.en)

– cc-by-2.5:  Creative  Commons  Attribution  2.5  License.  [http://creativecommons.](http://creativecommons.org/licenses/by/2.5/deed.en)  [org/licenses/by/2.5/deed.en](http://creativecommons.org/licenses/by/2.5/deed.en)

– cc-by-3.0:  Creative  Commons  Attribution  3.0  License.  [http://creativecommons.](http://creativecommons.org/licenses/by/3.0/deed.en)  [org/licenses/by/3.0/deed.en](http://creativecommons.org/licenses/by/3.0/deed.en)

– GPL:  GNU  General  Public  License. [http://www.gnu.org/licenses/gpl-2.0.txt](http://www.gnu.org/licenses/gpl-2.0.txt)

– LGPL:  GNU  Lesser  General  Public  License.  [http://www.gnu.org/licenses/lgpl.](http://www.gnu.org/licenses/lgpl.html)  [html](http://www.gnu.org/licenses/lgpl.html)

– PD:  This  image  is  in  the  public  domain.

– ATTR:  The  copyright  holder  of  this  file  allows  anyone  to  use  it  for  any  purpose,  provided that the copyright holder is properly attributed. Redistribution, derivative  work,  commercial  use,  and  all  other  use  is  permitted.

– EURO: This  is the  common (reverse) face  of a  euro coin.  The  copyright  on the  design of the common face of the euro coins belongs to the European Commission.  Authorised is reproduction in a format without relief (drawings, paintings, films)  provided  they  are  not  detrimental  to  the  image  of  the  euro.

– LFK: Lizenz Freie Kunst. [http://artlibre.org/licence/lal/de](http://artlibre.org/licence/lal/de)

– CFR:  Copyright  free  use.

– EPL: Eclipse Public License. [http://www.eclipse.org/org/documents/epl-v10.](http://www.eclipse.org/org/documents/epl-v10.php)  [php](http://www.eclipse.org/org/documents/epl-v10.php)

Copies  of  the  GPL, the  LGPL as  well  as  a  GFDL are  included  in  chapter  Licenses[96](#part0399.xhtml__bookmark1896).  Please  note  that  images  in  the  public  domain  do  not  require  attribution.  You  may  click  on the image numbers in the following table to open the webpage of the images in your  webbrower.

![](Images/image07404.jpeg)

96 Chapter  [61](#part0400.xhtml__bookmark1897)  on  page  [399](#part0400.xhtml__bookmark1897)

List  of  Figures

| 1 | ManuelGR[97](#part0000.xhtml__bookmark0) | GFDL |

![](Images/image07405.jpeg)

97 [http://en.wikibooks.org/wiki/User%3AManuelGR](http://en.wikibooks.org/wiki/User%3AManuelGR)

choose  that  version  for  the  Library.