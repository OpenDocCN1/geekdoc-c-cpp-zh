

test CE 中的时间函数仅在第一个模式被数据事实匹配时才会被检查。由于返回的值将与创建时间槽中的值大致相同，因此规则不会被满足。CLIPS 不会不断重新检查 test CE 以确定其是否评估为不同的值；它们仅在前面的 CEs 发生变化时才会被检查。这就是为什么规则原始版本中的 current-time 事实必须被更新，以便 test CE 会被定期重新检查。

## 冲突的槽属性

CLIPS 不允许为槽指定冲突的属性。例如，槽的默认值必须满足槽的类型、allowed-...、范围和基数属性。如果指定了 allowed-... 属性，则与该属性关联的类型必须满足槽的类型属性。allowed-numbers、allowed-integers 和 allowed-floats 属性不能与 range 属性一起使用。

## 9.3 显著性

到目前为止，控制事实已被用于间接控制程序的执行。CLIPS 提供了两种控制规则执行的显式技术：显著性和模块。使用模块控制规则执行将在本章后面讨论。使用关键字 salience 允许显式指定规则的优先级。通常，议程像堆栈一样工作，即最近放置在议程上的激活将首先触发。显著性允许更重要的规则保持在议程顶部，无论规则是什么时候添加的。较低显著性的规则会被推到议程中较高显著性规则的下方。

显著性使用数值设置，范围从最小值 -10,000 到最高值 10,000。如果程序员没有为规则显式分配显著性，CLIPS 假设显著性为 0。请注意，显著性为 0 介于最大和最小显著性值之间。显著性为 0 并不意味着规则没有显著性，而是表示它具有中间优先级。新激活的规则会放置在议程上，位于所有显著性相等或较低的规则之前，以及所有显著性更高的规则之后。

显著性的一个用途是强制规则按顺序触发。请考虑以下一组规则，其中未声明显著性值：

```
(defrule fire-first
   (priority first)
   =>
   (printout t "Print first" crlf))
```

```
(defrule fire-third
   (priority third)
   =>
   (printout t "Print third" crlf))
```

规则触发的顺序取决于满足规则左侧 CEs 的事实被断言的顺序。例如，如果输入了规则，以下命令将产生如下所示的输出：

```
CLIPS> (unwatch all.)
CLIPS> (reset.)
CLIPS> (assert (priority first))
<Fact-1>
CLIPS> (assert (priority second))
<Fact-2>
CLIPS> (assert (priority third))
<Fact-3>
CLIPS> (run.)
Print third
Print second
Print first
CLIPS>
```

请注意输出语句的顺序。首先打印“Print third”，然后打印“Print second”，最后打印“Print first”。第一个事实（priority first）激活规则 fire-first。当第二个事实被断言时，它激活规则 fire-second，该规则堆叠在规则 fire-first 的激活之上。最后，第三个事实被断言，其激活的规则 fire-third 堆叠在规则 fire-second 的激活之上。

在 CLIPS 中，由不同模式激活的同等显著性规则根据事实的堆栈顺序进行优先级排序。规则从议程的堆栈顶部向下触发。因此，规则 fire-third 会首先被触发，因为它位于堆栈顶部，然后是规则 fire-second，最后是规则 fire-first。如果断言事实的顺序被反转，那么规则触发的顺序也将被反转。以下输出中可以看到这一点：

```
CLIPS> (reset.)
CLIPS> (assert (priority third))
<Fact-1>
CLIPS> (assert (priority second))
<Fact-2>
CLIPS> (assert (priority first))
<Fact-3>
CLIPS> (run.)
Print first
Print second
Print third
CLIPS>
```

一个重要的一点是，如果两个或多个具有相同显著性的规则由同一个事实激活，则无法保证规则放置在议程上的顺序。

可以使用显著性来强制规则按 fire-first、fire-second、fire-third 的顺序触发，而不考虑激活事实被断言的顺序。这可以通过声明显著性值来实现：

```
(defrule fire-first
   (declare (salience 30))
   (priority first)
   =>
   (printout t "Print first" crlf))

(defrule fire-second
   (declare (salience 20))
   (priority second)
   =>
   (printout t "Print second" crlf))

(defrule fire-third
   (declare (salience 10))
   (priority third)
   =>
   (printout t "Print third" crlf))
```

无论断言优先级事实的顺序如何，议程的顺序始终相同。在断言优先级事实后执行 agenda 命令将产生以下输出：

```
CLIPS> (reset.)
CLIPS> (assert (priority second)
             (priority first)
             (priority third))
<Fact-3>
CLIPS> (agenda.)
30   fire-first: f-2
20   fire-second: f-1
10   fire-third: f-3
For a total of 3 activations.
CLIPS>
```

请注意显著性值如何重新排列了议程中规则的优先级。运行程序时，规则触发的顺序始终是 fire-first、fire-second、fire-third。

## 9.4 阶段和控制事实

基于规则的专家系统最纯粹的概念是规则在适用时机会性地行动。然而，大多数专家系统都具有一定的过程性方面。例如，Sticks 程序有不同的规则，适用性取决于轮到人类还是计算机移动。这个问题的控制是通过指示轮到谁的事实来处理的。这些控制事实允许将有关程序控制结构的信息嵌入到领域知识的规则中。这确实有一个缺点：有关规则控制的知识与有关如何玩游戏的知识混合在一起。对于 Sticks 程序来说，这不是一个主要缺点，因为它很小。然而，对于涉及数百或数千条规则的程序，领域知识和控制知识的混合使得开发和维护成为一大问题。

例如，考虑执行电子设备等系统的故障检测、隔离和恢复的问题。故障检测是识别电子设备工作不正常的过程。隔离是确定导致故障的设备组件的过程。恢复是确定纠正故障所需步骤的过程（如果可能的话）。通常，针对这类问题，专家系统将具有确定是否发生故障的规则、其他用于隔离故障原因的规则，以及用于确定如何从故障中恢复的更多规则。然后循环将返回。图 9.1 显示了此类系统中控制流的示例。

**图 9.1 故障检测、隔离和恢复问题的不同阶段**

![](img/2c460d4de56b7ffaad3834eee20beaa0_524_0.png)

在此系统中实现控制流至少有四种方法。前三种方法使用显著性，将在本节中讨论。第四种方法使用模块，将在本章后面讨论。实现控制流的第一种方法是将控制知识直接嵌入到规则中。例如，检测规则将包括指示何时应进入隔离阶段的规则。每组

