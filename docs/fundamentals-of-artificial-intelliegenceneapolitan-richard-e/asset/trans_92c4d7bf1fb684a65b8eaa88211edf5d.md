

```
(frame-name
slot-name1: filler1;
slot-name2: filler2;
:
)
```

### 示例 4.1 表示图 4.1 中语义网的帧的前两个帧如下：

```
(animal
SupersetOf: bird;
SupersetOf: fish;
skin: has;
mobile: yes;
eats: yes;
breathes: yes;
)
```

```
(bird
SubsetOf: animal;
SupersetOf: canary;
SupersetOf: ostrich;
wings: has;
flies: yes;
feathers: has;
)
```

请注意，在前面的示例中，我们将帧名称设置为粗体。

## 4.2.2 使用帧规划行程

假设一名旅行推销员正在规划一个访问多个城市的往返行程。行程有多个组成部分，例如出行方式、访问的城市和住宿。我们开发帧来表示这些组件，并展示如何使用它们来表示行程计划。

我们有以下用于开发行程的通用帧：

```
(Trip
FirstStep: TravelStep;
Traveler: human;
BeginDate: date;
EndDate: date;
TotalCost: price;
)
```

```
(TripPart
SupersetOf: TravelStep;
SupersetOf: LodgingStay;
BeginDate: date;
EndDate: date;
Cost: price;
PaymentMethod: method;
)
```

```
(TravelStep
SubsetOf: TripPart;
Origin: city;
Destination: city;
OriginLodgingStay: LodgingStay;
DestinationLodgingStay: LodgingStay;
FormofTransportation: travelmeans;
NextStep: TravelStep;
PreviousStep: TravelStep;
)
```

```
(LodgingStay
SubsetOf: TripPart;
Place: city;
Lodging: hotel;
ArrivingTravelStep: TravelStep;
DepartingTravelStep: TravelStep;
)
```

请注意，TravelStep 和 LodgingStay 都是 TripPart 的子集。因此，它们继承 TripPart 中的属性，即 BeginDate、EndDate、Cost 和 PaymentMethod。接下来，我们开发一个简单的行程，从本地城市芝加哥出发，访问墨尔本，然后返回芝加哥。

```
(trip1
MemberOf: Trip;
FirstStep: TravelStep1;
Traveler: Amit Patel;
BeginDate: 06/22/2011;
EndDate: 06/28/2011;
TotalCost: $6000;
)
```

```
(TravelStep1
    MemberOf: TravelStep;
    BeginDate: 6/22/2011;
    EndDate: 6/23/2011;
    Cost: $1500;
    PaymentMethod: visa;
    Origin: Chicago;
    Destination: Melbourne;
    OriginLodgingStay: Null;
    DestinationLodgingStay: LodgingStay1;
    FormofTransportation: plane;
    NextStep: TravelStep2;
    PreviousStep: Null;
)
```

```
(TravelStep2
    MemberOf: TravelStep;
    BeginDate: 6/27/2011;
    EndDate: 6/28/2011;
    Cost: $2000;
    PaymentMethod: master card;
    Origin: Melbourne;
    Destination: Chicago;
    OriginLodgingStay: LodgingStay1;
    DestinationLodgingStay: Null;
    FormofTransportation: plane;
    NextStep: Null;
    PreviousStep: TravelStep1;
)
```

```
(LodgingStay1
    MemberOf: LodgingStay;
    BeginDate: 6/23/2011;
    EndDate: 6/27/2011;
    Cost: $2500;
    PaymentMethod: american express;
    Place: Melbourne;
    Lodging: Best Western;
    ArrivingTravelStep: TravelStep1;
    DepartingTravelStep: TravelStep2;
)
```

图 4.3 显示了帧中的填充值如何将帧链接成一个有组织的行程计划。前面关于规划行程的示例基于出现在 [布雷赫曼和莱夫斯克，2004] 中的更复杂的示例。

![](img/67fa924962ee21b3590be9f3b10d9fe7_109_0.png)

图 4.3 构成芝加哥和墨尔本之间行程的帧之间的链接。

## 4.3 非单调逻辑

命题逻辑和一阶逻辑会得出某些结论，且没有撤销或覆盖结论的机制。这是**单调性**属性。然而，人类得出的结论往往只是暂时的，基于部分信息，并在新证据出现时被撤销。例如，如果我们得知一个实体是鸟，我们会得出它能飞的结论。当我们后来得知该实体是鸵鸟时，我们会撤销之前的结论并推断该实体不能飞。能够系统化这种推理的逻辑称为**非单调**。我们接下来讨论这种逻辑。处理不确定推理的另一种方法是使用概率论，这是本文第二部分的重点。

### 4.3.1 圈定

圈定由麦卡锡 [1980] 开发，用于形式化这样一种假设：除非我们另有说明，否则一切都按预期进行。他通过讨论**食人族-传教士**问题来引入这一概念，问题如下。假设一条河岸上有三位传教士和三个食人族，他们需要使用一艘两人座的船过河。然而，每条河岸上食人族的人数永远不能多于传教士的人数。麦卡锡关注的不是获得问题的解决方案，而是以下观察。即，有许多未陈述的细节。例如，船是否有漏水可能导致其沉没，或者更相关的是，是否有一座桥，一些人可以走过桥过河。可能存在许多未陈述的情况，这些情况可能影响问题的解决方案。**圈定假设**是：除非明确说明，否则没有条件会改变或与预期不同。在当前示例中，我们假设过河的唯一方式是乘坐两人座的船，并且它总能可靠地到达对岸。

### 示例 4.2 圈定的逻辑语句示例如下：

\(\forall x \, \text{bird}(x) \land \neg \text{abnormal}(x) \Rightarrow \text{flies}(x).\)

推理者对谓词 *异常* 进行圈定，这意味着除非另有说明，否则假设其为假。因此，如果我们只知道 bird(Tweety)，我们推断 Tweety 能飞。然而，假设我们包含以下语句：

\(\forall x \, \text{ostrich}(x) \Rightarrow \text{abnormal}(x).\)

如果我们同时知道 ostrich(Ralph) 和 bird(Ralph)，我们就不能得出 Ralph 能飞的结论。

### 示例 4.3 假设我们有以下语句：

\(\forall x \, \text{Quaker}(x) \land \neg \text{abnormal}_1(x) \Rightarrow \text{pacifist}(x)\)

\(\forall x \, \text{Republican}(x) \land \neg \text{abnormal}_2(x) \Rightarrow \neg \text{pacifist}(x)\)

Republican(Nixon) \(\land\) Quaker(Nixon).

在不知道 abnormal_1(Nixon) 或 abnormal_2(Nixon) 是否为真的情况下，我们会得出他是和平主义者且他不是和平主义者的结论。在这种情况下，我们可以让推理者对和平主义不得出任何结论，或者我们可以采用**优先圈定**，在其中我们给予贵格会党员或共和党党员优先权。如果我们给后者优先权，我们得出结论尼克松不是和平主义者。

圈定的正式描述出现在 [利夫希茨，1994]。

### 4.3.2 默认逻辑

**默认逻辑**采用形式为“在没有相反信息的情况下，假设...”的规则。Reiter [1980] 对默认逻辑进行了形式化，并认为默认推理对知识表示和推理至关重要。我们接下来提供一个非正式的介绍。

默认逻辑在结论与知识库当前状态一致时得出结论。默认逻辑中的典型规则如下：

```
bird(x): flies(x)
-----------------
flies(x)
.
```

此规则表示，如果对于特定实体 x，bird(x) 为真，那么只要知识库中没有与 flies(x) 矛盾的内容，我们就可以得出该实体 flies(x) 的结论。例如，如果我们得知 bird(Tweety)，那么只要知识库中没有陈述 flies(Tweety) 不为真，我们就可以得出 flies(Tweety) 的结论。然而，如果 ¬flies(Tweety) 在知识库中，那么我们就不能得出这个结论。

以下是默认规则的一般形式：

```
A: B1, B2, ..., Bn
-----------------
C
,
```

其中 A、Bi 和 C 是一阶逻辑公式。A 称为**先决条件**；B1、B2、... 和 Bn 称为**一致性条件**；C 称为**后继**。如果任何 Bi 可以被证明为假，那么我们不能从 A 得出 C；否则我们可以。

一个**默认理论**是一对 (D, W)，其中 D 是默认规则的集合，W 是一阶逻辑句子的集合。

### 示例 4.4 以下是一个默认理论。令 D 如下：

```
bird(x): flies(x)
-----------------
flies(x)
.
```

和

```
W = {bird(Tweety)}.
```

默认理论的一个**扩展**是该理论的极大后果集。也就是说，扩展由 W 中的语句以及可以使用规则得出的一组结论组成，使得无法再得出额外的结论。示例 4.4 中理论的唯一扩展如下：

```
{bird(Tweety), flies(Tweety)}.
```

### 示例 4.5 令 D 如下：

```
Quaker(x): pacifist(x)
-----------------
pacifist(x)
```

```
Republican(x): ¬pacifist(x)
-----------------
¬pacifist(x)
```

和

