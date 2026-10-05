

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

## 7.5.1 依赖引导的回溯 (Dependency-directed backtracking)

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

