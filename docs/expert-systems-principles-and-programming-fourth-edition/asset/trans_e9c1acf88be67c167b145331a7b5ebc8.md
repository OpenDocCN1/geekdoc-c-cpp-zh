

如果为通配符参数指定了类型限制，则 preview-generic 仅显示符号 $? 来表示它。

给定通用函数的两个方法，CLIPS 使用以下步骤来确定哪个方法具有更高优先级：

- 1. 比较两个方法中最左侧未检查的参数限制。如果只有一个方法还有参数，则转到步骤 6。如果两个方法都没有剩余参数，则转到步骤 7。否则，转到步骤 2。
- 2. 如果一个参数是常规参数，而另一个参数是通配符参数，则带有常规参数的方法具有优先权。否则，转到步骤 3。
- 3. 如果一个参数有类型限制，而另一个参数没有，则带有类型限制的方法具有优先权。否则，转到步骤 4。
- 4. 比较两个参数中最左侧未检查的类型限制。如果一个参数的类型限制比另一个参数的类型限制更具体，则带有更具体类型限制的方法具有优先权。例如，类型限制 INTEGER 比 NUMBER 更具体。如果两个类型限制都不更具体（例如，INTEGER 不比 LEXEME 更具体），并且两个参数都有剩余类型限制，则重复步骤 4。如果一个参数有剩余类型限制，而另一个参数没有，则没有其他类型限制的方法具有优先权。否则，转到步骤 5。
- 5. 如果一个参数有查询限制，而另一个参数没有，则带有查询限制的方法具有优先权。否则返回步骤 1 并比较下一组参数。
- 6. 如果带有剩余参数的方法的下一个参数是常规参数，则该方法具有优先权。否则，另一个方法具有优先权。
- 7. 先定义的方法具有优先权。

图 10.1 显示了一个流程图，其结果与步骤 1 到 7 等效。步骤 1 从图中左上角的框开始。图 10.2 显示了一个流程图，用于确定一个参数是否比另一个参数具有更具体的类型限制，其结果与步骤 3 和 4 等效。

使用这些步骤，我们可以确定为什么通用函数 check-input 的方法 #2 比方法 #1 具有更高优先级。从步骤 1 开始，我们比较两个方法中最左侧未检查的参数。方法 #1 的参数限制为 ( )，方法 #2 的参数限制为 (STRING)。由于两个方法都有参数，我们转到步骤 2。由于两个参数都是常规参数，我们转到步骤 3。

### 图 10.1 方法优先级确定

- 比较每个方法中最左侧未检查的参数。
- 没有可比较参数的方法具有优先权。
- 是否只有一个方法有可比较的参数？
- 此参数是否是常规参数？
- 有可比较参数的方法具有优先权。
- 两个方法是否都有可比较的参数？
- 先定义的方法具有优先权。
- 参数中是否只有一个是常规参数？
- 带有常规参数的方法具有优先权。
- 参数中是否有一个具有更具体的类型限制？
- 带有更具体类型限制的方法具有优先权。
- 参数中是否只有一个具有查询限制？
- 带有查询限制的方法具有优先权。

### 图 10.2 方法类型特异性确定

![](img/2c460d4de56b7ffaad3834eee20beaa0_615_0.png)

由于只有方法 #2 有类型限制，因此方法 #2 优先于方法 #1。

由于 check-input 方法 #2 只允许输入整数值，让我们创建另一个方法，允许在指定范围内输入浮点值：

```lisp
(defmethod check-input ((?question STRING)
                             (?value1 NUMBER)
                             (?value2 NUMBER))
  (printout t ?question " (" (float ?value1)
           "--" (float ?value2) ") ")
  (bind ?answer (read))
  (while (or (not (numberp ?answer))
             (< ?answer ?value1)
             (> ?answer ?value2))
    (printout t ?question " (" (float ?value1)
             "--" (float ?value2) ") ")
    (bind ?answer (read)))
  (return ?answer))
```

此方法与我们之前的整数范围检查方法类似，只是在参数限制中用 NUMBER 替换了 INTEGER，在显示有效范围时将任何整数范围值强制转换为浮点数，并且使用 `numberp` 而不是 `integerp` 来检查无效类型。定义此附加方法后，示例运行表明两个范围检查方法都能正常工作：

```
CLIPS> (check-input "Pick a number" 1 3.5)_
Pick a number (1.0-3.5) 6.
Pick a number (1.0-3.5) 2.7.
2.7
CLIPS> (check-input "Pick a number" 1 3)_
Pick a number (1-3) 2.7.
Pick a number (1-3) 2
2
CLIPS>
```

preview-generic 命令显示，对于第二次 check-input 通用调用，所有三个方法都适用：

```
CLIPS>
(preview-generic check-input "Pick a number" 1 3)_
check-input #2 (STRING) (INTEGER) (INTEGER)
check-input #3 (STRING) (NUMBER) (NUMBER)
check-input #1 ( ) $?
CLIPS>
```

带有两个 INTEGER 限制的方法比带有两个 NUMBER 限制的方法具有更高优先级。使用优先级确定步骤，我们可以确定原因。从步骤 1 开始，我们比较两个方法中最左侧未检查的参数。方法 #2 和方法 #3 的参数限制均为 (STRING)。由于两个方法都有参数，我们转到步骤 2。由于两个参数都是常规参数，我们转到步骤 3。由于两个参数都有类型限制，我们转到步骤 4。由于两个类型限制相同，我们转到步骤 5。由于两个参数都没有查询限制，我们返回步骤 1。方法 #2 中最左侧未检查的参数限制为 (INTEGER)，方法 #3 中最左侧未检查的参数限制为 (NUMBER)。由于两个方法都有参数，我们转到步骤 2。由于两个参数都是常规参数，我们转到步骤 3。由于两个参数都有类型限制，我们转到步骤 4。由于方法 #2 上的 INTEGER 类型限制比方法 #3 上的 NUMBER 类型限制更具体，因此方法 #2 具有优先权。

让我们再看一个优先级示例。在此示例中，我们将定义一个与最后定义的方法基本相同的方法，只是不使用 NUMBER 作为类型限制，而是指定两种类型 INTEGER 和 FLOAT：

```lisp
(defmethod check-input ((?question STRING)
 (?value1 INTEGER FLOAT)
 (?value2 INTEGER FLOAT))
 (printout t ?question " (" (float ?value1)
 "-" (float ?value2) ") ")
 (bind ?answer (read))
 (while (or (not (numberp ?answer))
 (< ?answer ?value1)
 (> ?answer ?value2))
 (printout t ?question " (" (float ?value1)
 "-" (float ?value2) ") ")
 (bind ?answer (read)))
 (return ?answer))
```

如果查看 preview-generic 调用的结果，我们将看到新方法 #4 夹在方法 #2 和方法 #3 之间：

```
CLIPS>
(preview-generic check-input "Pick a number" 1 3)_
check-input #2 (STRING) (INTEGER) (INTEGER)
check-input #4 (STRING) (INTEGER FLOAT) (INTEGER FLOAT)
check-input #3 (STRING) (NUMBER) (NUMBER)
check-input #1 () $?
CLIPS>
```

这种安排是方法第二个参数上步骤 #4 的结果。比较方法 #3 和 #4 时，方法 #4 的第一个类型限制 INTEGER 比方法 #3 的第一个类型限制 NUMBER 更具体，因此方法 #4 具有更高优先级。比较方法 #2 和 #4 时，方法 #2 的第一个类型限制 INTEGER 与方法 #4 的第一个类型限制相同，因此我们继续比较每个方法的第二个类型限制。由于方法 #2 没有第二个类型限制，但方法 #4 有，因此方法 #2 具有更高优先级。

