
槽和 <upper-limit> 术语表示槽的最大值。?VARIABLE 表示没有最小值或没有最大值（取决于它是第一个还是第二个）。例如，person deftemplate 中的 age 槽可以修改为防止将负值放入槽：

```
(deftemplate person
    (multislot name (type SYMBOL))
    (slot age (type INTEGER) (range 0 ?VARIABLE)))
```

如果我们愿意假设没有人活过125岁，那么 range 属性可以更改为 (range 0 125)。与允许值属性一样，range 属性并不将槽值的类型限制为数值。它仅在槽的值为数值时，才将槽允许的数值限制在指定范围内。槽的默认 range 属性是 (range ?VARIABLE ?VARIABLE)。

## 基数属性

基数属性允许指定可以存储在多字段槽中的值的最小数量和最大数量。基数属性的一般格式是 (cardinality <lower-limit> <upper-limit>)，其中 <lower-limit> 和 <upper-limit> 可以是 ?VARIABLE 或正整数。<lower-limit> 术语表示槽可以包含的最小值数量，<upper-limit> 术语表示槽可以包含的最大值数量。?VARIABLE 表示没有最小值数量或没有最大值数量（取决于它是第一个还是第二个）。多字段槽的默认基数属性是 (cardinality ?VARIABLE ?VARIABLE)。以下 deftemplate 可用于表示公司排球队，该队必须有六名队员，最多可有两名替补队员。请注意，type、允许值和 range 属性应用于多字段槽包含的每个值。

```
(deftemplate volleyball-team
    (slot name (type STRING))
    (multislot players (type STRING)
                 (cardinality 6 6))
    (multislot alternates (type STRING)
                 (cardinality 0 2)))
```

## 默认属性

在前面的章节中，每个被断言的 deftemplate 事实始终为每个槽都明确指定了值。如果在 assert 命令中没有明确指定值，自动将指定值存储在槽中通常很方便。default 属性允许指定这样的默认值。default 属性的一般格式是 (default <default-specification>)，其中 <default-specification> 可以是 ?DERIVE、?NONE、单个表达式（用于单字段槽），或零个或多个表达式（用于多字段槽）。

如果在 default 属性中指定了 ?DERIVE，则会为槽推导出满足所有槽属性的值。如果未为槽指定 default 属性，则假设为 (default ?DERIVE)。对于单字段槽，这意味着选择满足槽的 type、range 和 allowed values 属性的值。多字段槽的推导默认值将是一组相同值的列表，这些值是槽的最小允许基数（默认为零）。如果多字段槽的默认值中包含一个或多个值，则每个值都将满足槽的 type、range 和 allowed values 属性。推导值的示例如下：

```
CLIPS> (clear.)
CLIPS>
(deftemplate example
   (slot a)
   (slot b (type INTEGER))
   (slot c (allowed-values red green blue))
   (multislot d)
   (multislot e (cardinality 2 2)
                (type FLOAT)
                (range 3.5 10.0))))
CLIPS> (assert (example))
<Fact-0>
CLIPS> (facts)
f-0     (example (a nil)
         (b 0)
         (c red)
         (d)
         (e 3.5 3.5))
For a total of 1 fact.
CLIPS>
```

CLIPS 仅保证槽的推导默认值满足槽的约束属性。换句话说，您的程序不应依赖于将特定推导值（例如前面示例中槽 a 的符号 nil 或槽 b 的整数 0）放入槽。如果您的程序依赖于特定默认值，则应将表达式与 default 属性一起使用（将在稍后说明）。

如果在 default 属性中指定了 ?NONE，则在断言事实时必须为槽提供值。也就是说，没有默认值。例如，

```
CLIPS> (clear.)
CLIPS>
(deftemplate example
   (slot a)
   (slot b (default ?NONE))))
CLIPS> (assert (example))
```

```
[TMPLTRHS1] Slot b requires a value because of its
(default ?NONE) attribute.
CLIPS> (assert (example (b 1)))
<Fact-0>
CLIPS> (facts.)
f-0     (example (a nil) (b 1))
For a total of 1 fact.
CLIPS>
```

如果将一个或多个表达式与 default 属性一起使用，则在解析槽时对表达式进行求值，并且每当 assert 命令中未指定槽的值时，此值将存储在槽中。单字段槽的 default 属性必须恰好包含一个表达式。如果多字段槽的 default 属性中未指定表达式，则长度为零的多字段用作默认值。否则，所有表达式的返回值将被分组在一起以形成一个多字段值。以下是将表达式与 default 属性一起使用的示例：

```
CLIPS> (clear.)
CLIPS>
(deftemplate example
   (slot a (default 3))
   (slot b (default (+ 3 4)))
   (multislot c (default a b c))
   (multislot d (default (+ 1 2) (+ 3 4))))
CLIPS> (assert (example))
<Fact-0>
CLIPS> (facts.)
f-0     (example (a 3) (b 7) (c a b c) (d 3 7))
For a total of 1 fact.
CLIPS>
```

## 默认动态属性

使用 default 属性时，槽的默认值在解析槽定义时确定。也可以在将使用默认值的事实断言时生成默认值。这是通过 default-dynamic 属性完成的。当使用 default-dynamic 属性的槽的值在 assert 命令中未指定时，将对使用 default-dynamic 属性指定的表达式进行求值，并将其用作槽的值。

例如，让我们考虑在经过一定时间后删除事实的问题。首先，我们需要知道事实何时被断言。将使用 CLIPS 提供的 time 函数以创建时间标记事实。它返回自系统相关参考时间以来经过的秒数。time 函数的返回值本身没有意义。只有与该函数返回的其他值进行比较时才有用。以下 deftemplate 将用于此示例。它包含一个 creation-time 槽，用于存储创建时间，以及一个 value 槽，用于存储与事实关联的值。

```
(deftemplate data
   (slot creation-time (default-dynamic (time)))
   (slot value))
```

每次创建 data 事实且 creation-time 槽未指定时，将调用 time 函数并将值存储在 creation-time 槽中：

```
CLIPS> (watch facts.)
CLIPS> (assert (data (value 3)))
==> f-0     (data (creation-time 12002.45)
                      (value 3))
<Fact-0>
CLIPS> (assert (data (value b)))
==> f-1     (data (creation-time 12010.25)
                      (value b))
<Fact-1>
CLIPS> (assert (data (value c)))
==> f-2     (data (creation-time 12018.65)
                      (value c))
<Fact-2>
CLIPS>
```

假设 current-time 事实被断言并由其他规则更新以包含当前系统时间，则以下规则将撤销一分钟前断言的 data 事实：

```
(defrule retract-data-facts-after-one-minute
   ?f <- (data (creation-time ?t1))
   (current-time ?t2)
   (test (> (- ?t2 ?t1) 60))
   =>
   (retract ?f))
```

请注意，将 retract-data-facts-after-one-minute 规则更改为以下内容不会产生相同的结果：

```
(defrule retract-data-facts-after-one-minute
   ?f <- (data (creation-time ?t1))
   (test (> (- (time) ?t1) 60))
   =>
   (retract ?f))
```
