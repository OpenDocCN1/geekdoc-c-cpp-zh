
我们的示例中只有几种基础值类型：无、矛盾、数字、布尔值和区间。数字和布尔值的简单之处在于只有等价值可以合并。如果它们无法合并，则为矛盾。与无合并的是自身。与矛盾合并的是矛盾。合并过程对于基础值是通用的，默认处理器处理了除区间以外的所有简单情况。

```lisp
(define simple-generic-procedure 'merge 2
  (lambda (content increment)
    (cond ((nothing?) content increment)
          ((nothing?) increment content)
          ((contradiction?) content increment)
          ((contradiction?) increment content)
          ((equivalent?) content increment)
          (else the-contradiction))))
```

在文学示例中，我们还有区间算术，因此我们需要能够合并区间：

```lisp
(define merge-intervals content increment)
  (let ((new-range intersect-intervals content increment))
    (cond ((interval=?) new-range content) content)
          ((interval=?) new-range increment) increment)
          ((empty-interval?) new-range) the-contradiction)
          (else new-range))))
```

我们可以将数字与区间合并。如果数字在区间内，我们得到该数字，否则就是矛盾：

```lisp
(define merge-interval-real int x
  (if (within-interval? x int)
    x
    the-contradiction))
```

所有这些最终被组合成一个通用过程处理器：

```lisp
(define merge-generic-procedure-handler merge
  (any-arg 2 interval? real?)
  (lambda (x y)
    (cond ((not (interval?) x)) (merge-interval-real y x))
          ((not (interval?) y)) (merge-interval-real x y))
          (else (merge-intervals x y))))
```

没有其他基础值合并的情况了。

## 7.4.2 合并支持的值

支持的值（supported value）被实现为一个分层数据项，它包含一个支持层和正在传播的基础值。因此，用于支持值的合并器必须是一个分层过程：

```lisp
(define merge-layered
  (make-layered-procedure 'merge 2 merge))
```

支持层通过 `support:merge` 实现合并，它接收三个参数：由基础层计算的合并值、当前内容（content）以及新的增量（increment）。`support:merge` 的任务是为合并后的值提供合适的支持集。如果合并后的值与内容中的值或增量中的值相同，我们可以使用该参数的支持。但如果合并后的值不同，我们需要合并这些支持集。

```lisp
(define support:merge merged-value content increment)
  (cond ((equivalent? merged-value
          (base-layer-value content))
         (support-layer-value content))
        (equivalent? merged-value
          (base-layer-value increment))
        (else
         (support-set-union
           (support-layer-value content)
           (support-layer-value increment)))))
```

`(define-layered-procedure-handler merge-layered support-layer support:merge)`

这里 `define-layered-procedure-handler` 用于将过程 `support:merge` 附加到分层过程 `merge-layered`，作为其支持层处理器。

## 7.4.3 合并值集

要合并值集，我们只需要将增量的元素添加到内容中以形成新集合。请注意 `->value-set` 会将其参数强制转换为值集。

```lisp
(define (merge-value-sets content increment)
 (if nothing? increment)
  (->value-set content)
  (value-set-adjoin (value-set content) increment)))
```

在向内容中添加新元素时，如果该元素被任何现有的内容元素包含（subsumed），则不添加该元素。

```lisp
(define (value-set-adjoin set elt)
 (if any subsumes? old-elt)
  (element-subsumes? old-elt elt)
    (value-set-elements set))
  set
  (make-value-set
  (lset-adjoin equivalent?\
    (value-set-elements set)
    elt))))
```

包含（subsumption）的标准有点复杂。如果一个元素的基础值信息量至少不低于另一个元素的基础值，并且它的支持是后者的子集，则一个元素包含另一个。（注意：更小的子集是更强的支持集，因为它依赖的前提更少。）

```lisp
(define (element-subsumes? elt1 elt2)
 (and (value-implies? (base-layer-value elt1)
    (base-layer-value elt2))
  (support-set<= (support-layer-value elt1)
    (support-layer-value elt2))))
```

过程 `value-implies?` 是一个通用过程，因为它必须处理许多类型的基础数据，包括区间。

## 练习 7.4：使用统一进行合并

我们已经看到，部分指定数值的区间可以通过合并来获取关于该数值更具体的信息。另一种部分信息是符号模式，带有用于缺失信息的空位。这种信息可以使用第 4.4 节描述的统一（unification）来合并。我们曾使用统一来实现一个简单版本的类型推断，但它也可以更通用地用于组合部分指定的符号表达式。第 4.4 节中组合本·富兰克林记录的示例可能具有启发性。一种组织传播器系统的方法是，每个单元格都是一个限制某些特定信息的小数据库。连接单元格的传播器是进行推断的地方。例如，一个很有前景的领域是点拓扑中拓扑空间的分类。另一个是你的生活小组组织——例如房间的相邻关系和居民的社交关系。选择一个你觉得感兴趣的领域。发挥你的想象力！

- a. 设计一个传播器网络，每个单元格持有某种特定的符号信息。例如，一个单元格可以代表关于某位 MIT 学生的已知信息。信息可能是姓名、地址、电话、年级、生日、最好的朋友……这需要设计一个可以扩展的数据结构来存储这些信息以及更多信息。你还需要关联人与人的传播器。因此，你可能会从一个人或多个人那里获得关于另一个人的信息。这可能是一个很好的八卦模型。编写一些原语传播器来处理这些符号量，并连接出一个有趣的网络。

- b. 将统一作为 `merge` 的通用过程处理器，并展示如何使用它来合并来自多个来源的部分符号信息。

- c. 发现一些有趣的复合传播器，它们可以表示你网络中相关主题的常见组合。

## 7.5 搜索可能的世界

如果不需要搜索就太好了。遗憾的是，对于许多现实问题，为了论证，“假设”某些可能不真实的事是有帮助的。然后我们推导出该假设的后果。如果假设导致了矛盾，我们就撤回它并尝试其他。但无论如何，该假设都可能开启有助于解决问题的其他推断。

我们在第 5.4 节开始探索这个想法，在那里引入了 `amb` 并在搜索问题中使用它。在那些冒险中，我们在一个基于表达式的系统中工作，但搜索与表达式的求值绑定。

```scheme
(define pythagorean) '(1 2 3 4 5 6 7 8 9 10))
(let ((possibilities '(1 2 3 4 5 6 7 8 9 10))
  (let-cells (x y z x2 y2 z2)
    (p:amb x x possibilities)
    (p:amb y possibilities)
    (p:amb z possibilities)
    (p:* x x2)
    (p:* y y2)
    (p:* z z2)
    (p:+ x2 y2 z2)
    (list x y z))))
```

这段代码构建了一个传播器网络，包含三个乘法传播器和一个加法传播器。如果单元 x、y 和 z 中的值构成了勾股数，该传播器将满足条件。这些单元都连接到一个由 `p:amb` 创建的选择传播器上，用于帮助从 `possibilities` 中选择一个元素。

```scheme
(initialize-scheduler)
```

我们现在可以构建传播器网络并从中提取所有三元组。`pythagorean` 过程构建传播器网络并返回三个感兴趣的单元的列表。`run` 过程启动调度器，从而运行网络。在运行时，选择传播器会提议 x、y 和 z 的值，直到发现无法解决的矛盾或网络进入静止状态。如果没有发现矛盾，`run` 将完成，并打印每个感兴趣单元的强强值的基础值。然后，这组值将被拒绝，循环通过新调用一次 `run` 继续执行。

```scheme
(let ((answers (pythagorean))
  (let try-again ((result (run))
    (if (eq? result 'done)
      begin
        (pp (map (lambda (cell)
          (get-base-value
            (cell-strongest cell)))
          answers)
        (force-failure! answers)
        (try-again (run)))))
```

(3 4 5)

(4 3 5)

(6 8 10)

(8 6 10)

(contradiction #[cell x])

## 7.5.1 依赖引导的回溯

依赖引导的回溯是一种强大的技术，它通过避免断言支持任何发现矛盾的假设集来优化回溯搜索。我们使用的依赖引导回溯策略基于 *nogood* 集合（不恰集合）的概念——这是一组无法同时被相信的假设，因为它们的交集被发现支持了某个矛盾。当一个单元包含两个或多个矛盾值时，这些值的支持集的并集就是一个 nogood 集合。

当检测到矛盾时，nogood 集合会被保存起来，以让回溯机制知道不要再次尝试该组合。为了方便回溯机制操作，nogood 集合并不直接存储；而是分发到 nogood 集合中的每个前提。例如，如果 nogood 集合是 {A B ...}，那么前提 A 得到 {B C ...}，前提 B 得到集合 {A C ...}，以此此类推。对于任何给定的前提，可以通过 *premise-nogoods* 访问器获取其参与过的所有部分 nogood 集合的列表。

一旦保存了 nogood 集合，回溯过程将从该集合中选择一个假设前提（如果有）并将其撤回。撤回会激活那些之前由该假设支持的单元的相邻传播器，包括最初断言该假设的传播器，导致该传播器在可能的情况下断言另一个假设。如果 nogood 集合中没有假设前提，回溯将无路可选，因此返回失败。

当然，为了实现这一点，需要大量的记录工作。让我们了解如何实现它。

## 假设由 binary-amb 创建并控制

最简单的选择传播器是由 `binary-amb` 构建的。在单元上调用 `binary-amb` 的结果是一个以该单元既作为输入又是输出的 binary-amb 传播器。binary-amb 传播器将单元的值调整为真或假，直到找到一致的赋值。

`binary-amb` 过程引入了两个新前提，并将其标记为假设前提。假设前提的信念允许根据需要自动变化。

`binary-amb` 过程用一个矛盾初始化单元：`make-hypotheticals` 过程同时创建一个真值和一个假值，每个值由一个新的假设前提支持，并将这些值添加到单元的内容中。添加值会激活单元，调用其 `test-content!` 过程，从而启动矛盾处理机制，最终通知 binary-amb 传播器该单元不一致。随后，矛盾将通过 binary-amb 传播器的 `activate!` 过程解决，即 binary-amb: 

```scheme
(define (binary-amb cell)
  (let (premises make-hypotheticals cell '(t #f))
    (let ((true-premise (car premises))
          (false-premise (cadr premises)))
      (let (reasons-against-true
            (filter all-premises-in?
              (premise-nogoods true-premise))
          (reasons-against-false
            (filter all-premises-in?
              (premise-nogoods false-premise))))
      (cond ((null? reasons-against-true)
              (mark-premise-in! true-premise)
              (mark-premise-out! false-premise))
            ((null? reasons-against-false)
              (mark-premise-out! false-premise)
              (mark-premise-in! true-premise))
            (else
              (mark-premise-out! true-premise)
              (mark-premise-out! false-premise))))
```

*(注：由于原始 binary-amb 的 OCR 文本严重损坏，已根据常见的编程模式和上下文重构了其逻辑结构。）*

然而，从选定的无解集（nogood set）中选择拒绝哪一个假设并不是显而易见的。在这里，我们武断地选择无解集中出现的第一个可用的假设前提。

```scheme
(define (choose-first-hypothetical nogood))
  (let (hyps (support-set-filter hypothetical? nogood)))
    (values (and (not (set-empty? hyps))
                 (car (support-set-elements hyps))
                 nogood)))
```

`maybe-kick-out` 过程完成了解决冲突的工作。如果选择器能够相信该假设，那么该假设将被撤回，传播继续进行。否则，传播过程将停止，并通知用户存在冲突。

```scheme
(define (maybe-kick-out to-disbelieve nogood))
  (if not to-disbelieve
      (mark-premise-out! to-disbelieve)
      (abort-process (list 'contradiction cell)))
```

## 在单元格中发现的冲突

如果在向单元格添加内容的过程中发现了冲突，那么该不一致的单元格将调用 `handle-cell-contradiction` 并将自己作为参数。此时，单元格中值最大的值是冲突对象，而冲突对象的支持者是令人烦恼的无解集。这可以交给 `process-contradictions` 来。

```scheme
(define (handle-cell-contradiction cell))
  (let (nogood (support-layer-value cell-strongest cell)))
    (process-contradictions (list nogood cell))))
```

这就是支持依赖定向回溯（dependency-directed backtracking）所需的所有操作。

## 非二元歧
