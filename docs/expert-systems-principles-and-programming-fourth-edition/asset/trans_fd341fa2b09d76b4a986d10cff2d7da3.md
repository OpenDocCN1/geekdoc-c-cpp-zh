

来自多个类。其次，对对象模式中未指定的槽值的更改不会重新触发模式所属的规则。第三，对逻辑条件元素中对象模式内未指定的槽值的更改不会移除关联规则提供的逻辑支持。对象模式的一般形式是：

```
(object <attribute-constraint>*)
```

其中 <attribute-constraint> 是：

```
(is-a <constraint>) |
(name <constraint>) |
(<slot-name> <constraint>*)
```

并且 <constraint> 与 deftemplate 模式中使用的模式槽约束相同。is-a 和 name 关键字的含义将在稍后讨论。让我们先从对象模式匹配的简单示例开始：

```
CLIPS> (clear)
CLIPS>
(defclass ID-POINT
  (is-a USER)
  (slot x))
CLIPS>
(defrule Example-1
  (object (x ?x))
  =>
  (printout t "Value of x slot is " ?x crlf))
CLIPS> (make-instance p1 of ID-POINT (x 3))
[p1]
CLIPS> (agenda):
0 Example-1: [p1]
For a total of 1 activation.
CLIPS> (run)
Value of x slot is 3
CLIPS>
```

首先，我们定义具有单个属性 x 的类 ID-POINT。然后定义 defrule Example-1。请注意，此规则仅匹配槽 x，未提及 ID-POINT 类。创建规则时，CLIPS 会自动确定 ID-POINT 类能够匹配该模式。创建 ID-POINT 类的实例后，Example-1 规则已正确激活，运行程序将输出实例的 x 槽值的正确结果。

让我们看看如果定义另一个包含 x 槽的类会发生什么：

```
CLIPS>
(defclass 2D-POINT
  (is-a USER)
  (slot x)
  (slot y))
CLIPS> (make-instance p2 of 2D-POINT (x 4) (y 2))
[p2]
CLIPS> (agenda)
CLIPS>
```

也许出乎意料的是，Example-1 规则不会被实例 [p2] 激活。这是因为判断某个类是否能匹配对象模式是在定义规则时做出的。在定义规则后定义的类的实例不会匹配规则使用的对象模式。如果重新定义 Example-1 规则，我们将看到原本期望的行为：

```
CLIPS>
(defrule Example-1
    (object (x ?x))
    =>
    (printout t "Value of x slot is " ?x crlf))
CLIPS> (agenda)
0      Example-1: [p2]
0      Example-1: [p1]
For a total of 2 activations.
CLIPS> (run)
Value of x slot is 4
Value of x slot is 3
CLIPS>
```

请注意，Example-1 规则现在对来自不同类的包含 x 槽的 [p1] 和 [p2] 实例都已激活。

## 对象模式匹配与继承

对象模式也可以匹配继承的槽：

```
CLIPS> (clear)
CLIPS>
(defclass 1D-POINT
    (is-a USER)
    (slot x))
CLIPS>
(defclass 2D-POINT
    (is-a 1D-POINT)
    (slot y))
CLIPS>
(defclass 3D-POINT
    (is-a 2D-POINT)
    (slot z))
CLIPS>
(defrule Example-2
    (object (y ?y))
    =>
    (printout t "Value of y slot is " ?y crlf))
CLIPS> (make-instance p1 of 1D-POINT (x 3))
[p1]
CLIPS> (make-instance p2 of 2D-POINT (x 1) (y 2))
[p2]
CLIPS> (make-instance p3 of 3D-POINT (x 2) (y 4) (z 3))
[p3]
CLIPS> (agenda)
0      Example-2: [p3]
0      Example-2: [p2]
For a total of 2 activations.
CLIPS> (run)
Value of y slot is 4
Value of y slot is 2
CLIPS>
```

请注意，Example-2 规则被实例 [p2] 和 [p3] 激活，但 [p1] 除外。实例 [p2] 是类 2D-POINT 的实例，该类定义了规则引用的 y 槽。实例 [p3] 是类 3D-POINT 的成员，该类从类 2D-POINT 继承了 y 槽。类 ID-POINT 的实例 [p1] 只有 x 槽，因此无法匹配规则 Example-2 的对象模式。

## is-a 和 name 关键字

is-a 关键字在对象模式中像槽名一样使用时具有特殊含义。它将匹配模式的实例限制为满足 is-a 约束的类。例如：

```
CLIPS>
(defrule Example-3
    (object (is-a 2D-POINT) (x ?x))
    =>
    (printout t "Value of x slot is " ?x crlf))
CLIPS> (agenda)
0      Example-3: [p3]
0      Example-3: [p2]
For a total of 2 activations.
CLIPS> (run)
Value of x slot is 2
Value of x slot is 1
CLIPS>
```

请注意，尽管实例 [p1] 也有 x 槽属性，但只有实例 [p2] 和 [p3] 激活了 Example-3 规则。这是因为 [p1] 既不是 2D-POINT 类的实例，也不是其子类。然而，实例 [p3] 确实满足对象模式，因为它通过继承是 2D-POINT 类的成员。可以通过显式禁止 3D-POINT 类来阻止实例 [p3] 匹配对象模式：

```
CLIPS>
(defrule Example-4
   (object (is-a 2D-POINT&~3D-POINT) (x ?x))
   =>
   (printout t "Value of x slot is " ?x crlf))
CLIPS> (agenda)
0      Example-4: [p2]
For a total of 1 activation.
CLIPS> (run)
Value of x slot is 1
CLIPS>
```

对象模式引用的任何类都必须已经定义；否则将导致错误：

```
CLIPS>
(defrule Example-5
   (object (is-a 4D-POINT) (x ?x))
   =>
   (printout t "Value of x slot is " ?x crlf))
[OBJRTBLDS] Undefined class in object pattern.

ERROR:
(defrule MAIN::Example-5
   (object (is-a 4D-POINT)
CLIPS>
```

对象模式引用的槽也是如此。必须至少有一个类包含对象模式中引用的所有槽属性，否则将导致错误：

```
CLIPS>
(defrule Example-6
   (object (w ?w))
   =>
   (printout t "Value of w slot is " ?w crlf))
[OBJRTBLDS] No objects of existing classes can
satisfy w restriction in object pattern.

ERROR:
(defrule MAIN::Example-6
(object (w
CLIPS>
```

由于现有类（ID-POINT、2D-POINT 和 3D-POINT）都没有 w 槽属性，规则 Example-6 中的对象模式无法满足，因此会生成错误。

name 关键字可用于匹配特定实例。例如：

```
CLIPS>
(defrule Example-7
(object (name [p1] | [p3]) (x ?x))
=>
(printout t "Value of x slot is " ?x crlf))
CLIPS> (agenda)
0 Example-7: [p3]
0 Example-7: [p1]
For a total of 2 activations.
CLIPS> (run)
Value of x slot is 2
Value of x slot is 3
CLIPS>
```

规则 Example-7 使用 name 关键字将能够匹配对象模式的实例限制为 [p1] 和 [p3]。实例 [p2] 虽然有 x 槽值，但由于其名称不满足 name 限制，因此不会匹配该模式。由于 is-a 和 name 关键字在对象模式中具有特殊含义，因此不能在 defclass 定义中将其用作槽名。

## 触发对象模式

对象模式与事实模式之间一个非常重要的区别是，只有在更改实例的槽值时，那些显式匹配槽的对象模式才会受到影响。为了说明这一点，让我们重新审视第 8.10 节中 sum-rectangles 规则的初始尝试：

```
(defrule sum-rectangles
(rectangle (height ?height) (width ?width))
?sum <- (sum ?total)
=>
(retract ?sum)
(assert (sum (+ ?total (* ?height ?width)))))
```

此规则的问题是，任何尝试修改 sum 事实都会导致规则对刚刚处理的 rectangle 事实重新触发，从而造成无限循环。将 sum 事实从有序事实转换为 deftemplate 事实并使用 modify 命令无法解决问题。第 8.4 节中提出的解决方案使用多个规则来计算总和。更好的解决方案是适当地使用对象模式。以下是将第 8.4 节中的 sum-rectangles 代码重写为使用对象的初步尝试：

```
(defclass RECTANGLE
  (is-a USER)
  (slot height)
  (slot width))
(defclass SUM
  (is-a USER)
  (slot total))
(definstances initial-information
  (of RECTANGLE (height 10) (width 6))
  (of RECTANGLE (height 7) (width 5))
  (of RECTANGLE (height 6) (width 8))
  (of RECTANGLE (height 2) (width 5))
  ([sum] of SUM (total 0)))
(defrule sum-rectangles
  (object (is-a RECTANGLE)
    (height ?height) (width ?width))
  ?sum <- (object (is-a SUM) (total ?total))
  =>
  (send ?sum put-total
    (+ ?total (* ?height ?width))))
```

关于新的 sum-rectangles 规则有几点需要注意。首先，与事实模式一样，我们可以使用 <- 模式绑定操作符将匹配模式的实例绑定到变量。在此示例中，匹配 SUM 对象模式的实例地址绑定到 ?sum 变量。然后可以将此变量作为参数传递给 send 函数，向实例发送消息。然而，运行此代码会演示与事实模式相同的问题：无限循环。这是因为使用 put-total 消息从规则右侧更改 total 槽的值会重新触发 SUM 对象模式，因为它匹配 total 槽。

我们不需要在规则左侧匹配 total 槽，因为绑定到 ?total 的值在任何左侧模式中都不会再次被引用。通过在规则右侧使用消息传递检索值，得到以下规则：

```
(defrule sum-rectangles
  (object (is-a RECTANGLE)
    (height ?height) (width ?width))
  ?sum <- (object (is-a SUM))
```

