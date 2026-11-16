

close 函数被调用以关闭与 file-logical-name 槽关联的文件。sensor 和 value 槽的内容也会被清空，因此不会再从中检索任何传感器值。

与 DATA-SOURCE 的先前子类不同，FILE-DATA-SOURCE 类将重写 next-cycle 消息处理程序，以一次性从文件中检索下一个周期的所有传感器值：

```
(defmessage-handler INPUT::FILE-DATA-SOURCE
  next-cycle (?cycle)
  (if (not ?self:file-logical-name)
    then (send ?self get-file))
  (bind ?name (read ?self:file-logical-name))
  (if (eq ?name EOF)
    then
    (send ?self close-data-source)
    (return))
  (while (and (neq ?name end-of-cycle)
    (neq ?name EOF))
    (bind ?raw-value
      (read ?self:file-logical-name))
    (if (eq ?raw-value EOF)
      then
      (send ?self close-data-source)
      (return))
    (send ?self put-sensor-value
      ?name ?raw-value)
    (bind ?name (read ?self:file-logical-name))
    (if (eq ?name EOF)
      then
      (send ?self close-data-source)
      (return)))))
```

首先，如果 file-logical-name 槽未从其原始默认值 FALSE 更改，则向实例发送 get-file 消息以检索文件名并打开文件。然后，该处理程序从数据文件中读取所有数据值，直到遇到关键字 end-of-cycle。如果到达文件末尾，则向实例发送 close-data-source 消息以关闭文件并移除任何现有的传感器值。否则，在读取数据值时，它们会通过发送 put-sensor-value 消息存储在实例中，以便稍后检索。

还必须重写 get-data 消息处理程序：

```
(defmessage-handler INPUT::FILE-DATA-SOURCE
  get-data (?name)
  (bind ?position (member$ ?name ?self:sensor))
  (if ?position
   then
   (nth$ ?position ?self:value)
   else
   (return nil)))
```

它在 sensor 槽中查找指定传感器的位置，如果存在，则返回 value 槽中存储的相应值。最后，还必须添加一个包含 FILE-DATA-SOURCE 类实例的 definstances：

```
(definstances INPUT::file-data-source
  ([file] of FILE-DATA-SOURCE))
```

有四种不同的数据源共享一组通用的消息处理程序，我们可以使用两条规则和一个 deffacts 从其中任何一个读取数据：

```
(deffacts local-cycle
  (local-cycle 0))
(defrule INPUT::next-cycle
  (cycle ?cycle)
  ?f <- (local-cycle ~?cycle)
  (data-source ?source)
  (object (is-a DATA-SOURCE) (name ?source))
  =>
  (send ?source next-cycle ?cycle)
  (retract ?f)
  (assert (local-cycle ?cycle)))
(defrule INPUT::Get-Sensor-Value-From-Data-Source
  (cycle ?cycle)
  (local-cycle ?cycle)
  (data-source ?source)
  (object (is-a DATA-SOURCE) (name ?source))
  ?s <- (sensor (name ?name)
   (raw-value none)
   (device ?device))
  (device (name ?device) (status on))
  =>
  (bind ?raw-value (send ?source get-data ?name))
  (if (not (numberp ?raw-value))
   then
   (printout t "No data for sensor "
    ?name crlf)
   (printout t "Halting monitoring system"
    crlf)
   (halt)
   else
   (modify ?s (raw-value ?raw-value))))
```

local-cycle 事实用于指示当前监控周期是否已处理 next-cycle 消息。next-cycle 规则检查 cycle 事实指定的周期是否与 local-cycle 事实指定的周期不同。如果存在此情况，则规则左侧（LHS）匹配的 DATA-SOURCE 实例会收到 next-cycle 消息，并且 local-cycle 事实会更新为与 cycle 事实相同的值。对于 DATA-SOURCE、SENSOR-DATA-SOURCE 和 INSTANCE-DATA-SOURCE 实例，next-cycle 消息处理程序不执行任何操作。对于 FILE-DATA-SOURCE 实例，next-cycle 处理程序将当前周期的所有数据值读入实例。一旦 cycle 和 local-cycle 事实匹配，就会使用 Get-Sensor-Value-From-Data-Source 规则检索连接到处于开启状态的设备的每个传感器的原始值。get-data 消息会发送到规则左侧匹配的 DATA-SOURCE 实例，以获取特定传感器的原始值。如果返回非数值，则监控系统将停止，因为非数值用于指示没有更多数据。否则，原始传感器值将存储在传感器事实的 raw-value 槽中。

## 检测趋势

下一阶段活动，即趋势阶段，确定传感器的当前状态并计算可能正在发展的趋势。传感器的当前状态（正常、低或高警戒线、或低或高红线）必须从输入阶段断言的原始传感器值中确定。传感器的当前状态存储在传感器 deftemplate 的 state 槽中。以下规则确定传感器是否处于正常状态：

```
(defrule TRENDS::Normal-State
  ?s <- (sensor (raw-value ?raw-value&~none)
               (low-guard-line ?lgl)
               (high-guard-line ?hgl))
  (test (and (> ?raw-value ?lgl)
             (< ?raw-value ?hgl)))
  =>
  (modify ?s (state normal) (raw-value none))))
```

第一个模式和随后的 test CE 查找处于正常状态的任何传感器。传感器模式中的 raw-value 槽与值 none 进行比较，以确保在规则的 test CE 中不会将符号与数值进行比较。测试传感器是否处于正常状态所需的范围介于低警戒线和高警戒线值之间。test CE 将规则限制在原始传感器值处于正常状态范围内的情况。该规则的唯一操作是断言传感器的推导状态。raw-value 槽也设置为文字 none，以便在下一个输入阶段读取。

还需要四条规则来分析传感器的其余四种可能状态。每条规则都将类似于 Normal-State 规则，区别在于从传感器事实中检索的值以及用于确定当前状态的 test CE。所有五条状态规则都可以写成一条规则，在规则右侧（RHS）使用 if 表达式来确定传感器的适当状态。然而，这种编码方式违背了数据驱动系统的初衷。此外，涉及所有或部分可能状态的操作或条件的进一步修改，如果使用单个笨拙的规则，将变得困难得多。其余四条状态分析规则如下：

```
(defrule TRENDS::High-Guard-Line-State
  ?s <- (sensor (raw-value ?raw-value&~none)
              (high-guard-line ?hgl)
              (high-red-line ?hrl))
  (test (and (>= ?raw-value ?hgl)
             (< ?raw-value ?hrl)))
=>
  (modify ?s (state high-guard-line)
          (raw-value none)))
```

```
(defrule TRENDS::High-Red-Line-State
  ?s <- (sensor (raw-value ?raw-value&~none)
              (high-red-line ?hrl))
  (test (>= ?raw-value ?hrl))
=>
  (modify ?s (state high-red-line)
          (raw-value none)))
```

```
(defrule TRENDS::Low-Guard-Line-State
  ?s <- (sensor (raw-value ?raw-value&~none)
              (low-guard-line ?lgl)
              (low-red-line ?lrl))
  (test (and (>= ?raw-value ?lrl)
             (<= ?raw-value ?lgl)))
=>
  (modify ?s (state low-guard-line)
          (raw-value none)))
```

```
(defrule TRENDS::Low-Red-Line-State
  ?s <- (sensor (raw-value ?raw-value&~none)
              (low-red-line ?lrl))
  (test (<= ?raw-value ?lrl))
=>
  (modify ?s (state low-red-line)
          (raw-value none)))
```

前五条规则确定当前周期传感器的状态。由于检测传感器趋势是 TRENDS 模块的目标之一，因此有必要维护有关传感器过去状态的信息。将使用以下 deftemplate 来存储此信息。由于 TRENDS 和 WARNINGS 模块都将使用此 deftemplate，因此它将放置在 MAIN 模块中。

```
(deftemplate MAIN::sensor-trend
    (slot name)
    (slot state (default normal))
    (slot start (default 0))
    (slot end (default 0))
    (slot shutdown-duration (default 3)))
```

name 槽是传感器的名称，state 槽对应传感器的最新状态，start 槽是传感器处于当前状态的第一个周期，end 槽是当前周期，shutdown-duration 槽是传感器必须处于警戒线区域的时间量，之后其关联设备必须关闭。

更新趋势信息的规则将取决于每个传感器的事实列表中是否存在 sensor-trend 事实。出于此原因，初始传感器趋势将在 defacts 构造中定义：

```
(defacts MAIN::start-trends
    (sensor-trend (name S1) (shutdown-duration 3))
    (sensor-trend (name S2) (shutdown-duration 5))
    (sensor-trend (name S3) (shutdown-duration 4))
    (sensor-trend (name S4) (shutdown-duration 4))
    (sensor-trend (name S5) (shutdown-duration 4))
    (sensor-trend (name S6) (shutdown-duration 2)))
```

有了这些信息，可以定义两条规则来监控传感器的趋势。一条规则将监控自上一个周期以来未发生变化的趋势，另一条规则将监控自上一个周期以来已发生变化的趋势：

```
(defrule TRENDS::State-Has-Not-Changed
    (cycle ?time)
    ?trend <- (sensor-trend
        (name ?sensor) (state ?state)
        (end ?end-cycle&?time))
    (sensor (name ?sensor) (state ?state)
        (raw-value none))
    =>
    (modify ?trend (end ?time)))
```

```
(defrule TRENDS::State-Has-Changed
    (cycle ?time)
```

