

CLIPS> (reset)
CLIPS> (assert (emergency (type fire)))
<Fact-1>
CLIPS> (assert (emergency (type flood)))
<Fact-2>
CLIPS> (run)
Emergency: Operator Alert
Emergency: Operator Alert
CLIPS>

可以按以下方式修改 operator-alert-for-emergency 规则，以防止针对额外紧急情况重新触发该规则：

```
(defrule operator-alert-for-emergency
(emergency)
(not (operator-alert))
=>
(printout t "Emergency: Operator Alert" crlf)
(assert (operator-alert)))
```

(not (operator-alert)) CE 防止规则被重新触发；但是，以这种方式修改规则假设如果已经存在操作员警报，则它是由 operator-alert-for-emergency 规则触发的。操作员可能因紧急演习而被置于警戒状态，如下面的规则所示：

```
(defrule operator-alert-for-drill
(operator-drill)
(not (operator-alert))
=>
(printout t "Drill: Operator Alert" crlf)
(assert (operator-alert)))
```

请注意，如果演习警报规则先触发，则紧急警报规则将无法在以后触发，因为 operator-alert 事实将已被断言。为纠正此问题，可以修改 operator-alert 事实以存储警报原因；但是，过度使用控制事实来防止规则触发会增加规则的复杂性，并通过在规则之间添加控制依赖关系来降低规则的可维护性。

幸运的是，可以修改 operator-alert-for-emergency 规则以使用 exists CE，这将消除对控制事实的需求。无论 exists CE 内部的 CEs 有多少个事实匹配，exists CE 都只会生成一个部分匹配。因此，如果 exists CE 是规则的第 N 个 CE，且前 N - 1 个 CE 已生成 M 个部分匹配，那么前 N 个 CE 能生成的部分匹配的最大数量是 M。重写为使用 exists CE 的 operator-alert-for-emergency 规则如下：

```
(defrule operator-alert-for-emergency
 (exists (emergency))
 =>
 (printout t "Emergency: Operator Alert" crlf)
 (assert (operator-alert)))
```

该规则只会生成一个激活，因此操作员警报消息只会打印一次，如下面的对话所示：

```
CLIPS> (reset)
CLIPS> (assert (emergency (type fire)))
<Fact-1>
CLIPS> (assert (emergency (type flood)))
<Fact-2>
CLIPS> (agenda)
0 operator-alert-for-emergency: f-0,
For a total of 1 activation.
CLIPS> (run)
Emergency: Operator Alert
CLIPS>
```

exists CE 是通过组合 and CE 和 not CE 来实现的。exists CE 内部的 CEs 被包含在一个 and CE 中，然后再包含在两个 not CE 中。因此，通过将整个 LHS 用 and CE 包围，然后按说明替换 exists CE，将 operator-alert-for-emergency 规则转换为如下形式：

```
(defrule operator-alert-for-emergency
 (and (not (not (and (emergency)))))
 =>
 (printout t "Emergency: Operator Alert" crlf)
 (assert (operator-alert)))
```

由于围绕规则 LHS 的 and CE 的第一个 CE 是 not CE，因此在开头添加了 (the initial-fact) 模式 CE。进行此添加并删除 emergency 模式周围多余的 and CE 后，得到以下规则：

```
(defrule operator-alert-for-emergency
 (and (initial-fact)
 (not (not (emergency))))
 =>
 (printout t "Emergency: Operator Alert" crlf)
 (assert (operator-alert)))
```

规则开头的 (initial-fact) 模式解释了在前面的对话中发出 agenda 命令时为该规则显示的 f-0 事实索引。如果没有 emergency 事实，则最内层的 not CE 将被满足。如果此 CE 被满足，则最外层的 not CE 将不被满足，规则也不会被激活。反之，如果存在 emergency 事实，则最内层的 not CE 将不被满足。由于此 CE 不被满足，最外层的 not CE 将被满足，规则将被激活。

## 8.17 FORALL 条件元素

forall 条件元素允许您基于一组对另一个 CE 的每次出现都满足的 CEs 进行模式匹配。例如，假设工业厂区有多个地点（例如建筑物）可能起火，我们想确定每个起火的建筑物是否已疏散并有消防队试图扑灭火灾。可以使用 forall CE 来检查这一点。如下所示，emergency 事实将被修改为除了紧急类型外还包含紧急位置。将使用另外两个 deftemplates 来指示消防队的位置以及建筑物是否已疏散。all-fires-being-handled 规则使用这些 deftemplates 来确定适当条件是否已满足。

```
(deftemplate emergency
  (slot type)
  (slot location))

(deftemplate fire-squad
  (slot name)
  (slot location))

(deftemplate evacuated
  (slot building))

(defrule all-fires-being-handled
  (forall (emergency (type fire)
         (location ?where))
         (fire-squad (location ?where))
         (evacuated (building ?where)))
=>
(printout t
  "All buildings that are on fire " crlf
  "have been evacuated and" crlf
  "have firefighters on location" crlf))
```

对于匹配 (emergency (type fire) (location ?where)) 模式的每个事实，也必须存在匹配 (fire-squad (location ?where)) 模式和 (evacuated (building ?where)) 模式的事实。在首次加载 deftemplates 和 defrule 并发出 reset 命令时，由于没有火灾紧急情况，规则应被满足：

```
CLIPS> (watch activations)
CLIPS> (reset)
==> Activation 0      all-fires-being-handled:
    f-0,
CLIPS>
```

一旦断言 emergency 事实，规则将被停用，直到断言适当的 fire-squad 和 evacuated 事实：

```
CLIPS>
(assert (emergency (type fire)
        (location building-11)))
==> Activation 0      all-fires-being-handled: f-0,
<Fact-1>
CLIPS>
(assert (evacuated (building building-11)))
<Fact-2>
CLIPS>
(assert (fire-squad (name A)
        (location building-11)))
==> Activation 0      all-fires-being-handled: f-0,
<Fact-3>
CLIPS>
(assert (fire-squad (name B)
        (location building-1)))
<Fact-4>
CLIPS>
(assert (emergency (type fire)
        (location building-1)))
==> Activation 0      all-fires-being-handled: f-0,
<Fact-5>
CLIPS> (assert (evacuated (building building-1)))
==> Activation 0      all-fires-being-handled:
f-0,
<Fact-6>
CLIPS>
```

如果删除 building-1 的 fire-squad 事实，则规则将被停用。删除该建筑物的 emergency 事实将重新激活规则：

```
CLIPS> (retract 4)
==> Activation 0      all-fires-being-handled: f-0,
CLIPS> (retract 5)
==> Activation 0      all-fires-being-handled: f-0,
CLIPS> (run)
All buildings that are on fire
have been evacuated and
have firefighters on location
CLIPS>
```

forall CE 的一般格式如下：

```
(forall <first-CE>
<remaining-CEs>+)
```

为使 forall CE 得以满足，匹配 <first-CE> 的每个事实也必须具有匹配所有 <remaining-CEs> 的事实。forall CE 的一般格式将使用以下格式替换为 and 和 not CEs 的组合：

```
(not (and <first-CE>
(not (and <remaining-CEs>+))))
```

## 8.18 LOGICAL 条件元素

逻辑条件元素允许您指定事实的存在取决于另一个事实或一组事实的存在。逻辑 CE 是 CLIPS 提供的真值维护功能。例如，考虑以下规则，该规则指示当火灾散发有害烟雾时，消防员应使用氧气面罩：

```
(defrule noxious-fumes-present
(emergency (type fire))
(noxious-fumes-present)
=>
(assert (use-oxygen-masks)))
```

如下面的对话所示，前面的规则将在每次发生此类火灾紧急情况时断言 use-oxygen-masks 事实：

```
CLIPS> (unwatch all)
CLIPS> (reset)
CLIPS> (watch facts)
CLIPS> (assert (emergency (type fire)) (noxious-fumes-present))
==> f-1 (emergency (type fire))
==> f-2 (noxious-fumes-present)
<Fact-2>
CLIPS> (run)
==> f-3 (use-oxygen-masks)
CLIPS>

