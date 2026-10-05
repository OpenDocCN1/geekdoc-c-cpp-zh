
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

## 非二元歧（Non-binary amb）

虽然 `binary-amb` 可以用于许多问题的表述，但大多数选择并不是二元的。可以通过构建一个由条件传播器组成的电路从 `binary-amb` 构建出 n 元选择机制，这些传播器由单元格真真值受 `binary-amb` 传播器的调制，但这种方法非常低效，并且引入了大量的额外机制。因此，我们通过 `p:amb` 提供了一种原生的 n 元选择机制。`p:amb` 过程类似于 `binary-amb`。对于 `binary-amb`，单元格的值恰好有两个选择（#t 或 #f），每个选择由一个假设前提支持。当 `p:amb` 应用于单元格和可能值的列表时，`make-hypotheticals` 过程会将值添加到单元格中，每个值都由一个新的假设前提支持。

当由 `p:amb` 构建的传播器被激活时，会调用 `amb-choose` 过程。它首先尝试在其假设中寻找一个未被其前提无解集（premise-nogoods）排除的假设前提。如果有，它会将该前提标记为有效（in），并将所有其他前提标记为无效（out），从而选择与单元格该前提关联的值。如果没有任何假设前提可以被相信，它将将其所有前提标记为无效，并创建一个新的无解集传递给 `process-contradictions`，后者可能会从这些无解集中的撤回一个假设前提。`pairwise-union` 过程的泛化在处理两个两个集合时是 `cross-product-union`（笛卡尔积并）。和之前一样，这是一个解析步骤。

```scheme
(define (p:amb cell values)
  (let ((premises make-hypotheticals cell values))
    (define amb-choose
      (let ((to-choose
             (find (lambda premise)
               (not any all-premises-in?
                     (premise-nogoods premise))))
           premises)))
      (for-each (lambda premise)
        (if eq? to-choose
            (mark-premise-in! premise)
            (mark-premise-out! premise)))))
    premises)
  (let ((nogoods
         (cross-product-union
           (map (lambda
                 (filter all-premises-in?
                   (premise-nogoods premise))))
             premises))))
    (for-each mark-premise-out! nogoods)
    (process-contradictions cell)))
  (let ((atorator cell)
        (list cell)
        (amb-choose 'amb'))
    (set! all-amb-propagators))))```

使用 `p:amb` 构建的传播器引入的假设前提数量与选择数量相等。而使用 `binary-amb` 构建的传播器则引入两倍数量的假设。

## 5.7.2 解决组合问题

为了演示使用依赖定向回溯解决组合问题的方法，考虑著名的“住址”问题：Baker、Cooper、Fletcher、Miller 和 Smith 住在一个五层公寓的不同楼层。Baker 不在顶层。Cooper 不在底层。Miller 住在 Cooper 更高的楼层。Smith 不住在 Fletcher 的相邻楼层。我们可以将其设定为传播器问题。这里有一个简单的表述：

```scheme
(define (multiple-dwelling)
  (let-cells (baker cooper fletcher miller smith)
    let ((floors '1 2 3 4 5))
      (p:amb baker floors) (p:amb cooper floors)
      (p:amb fletcher floors) (p:amb miller floors)
      (p:amb smith floors)
      (require-distinct)
      (list baker cooper fletcher miller smith))
    (let-cells ((b=5 #f) (c=1 #f))
      (require-not baker 5)
      (require-not cooper 1)
      (require-not fletcher 1)
      (require-not fletcher 5)
      (require-higher miller cooper)
      (require-not-adjacent smith fletcher)
      (require-not-adjacent fletcher))))
```

（注：上述代码块的 OCR 文本源码较为混乱，我根据问题描述和标准的约束编程进行了重建以确保可读性。）

## 练习 7.5：游艇命名题

使用传播器表述并解决以下问题。

Mary Ann Moore 的父亲有一艘游艇，他的四位朋友也有：Colonel Downing、Mr. Hall、Sir Barnacle Hood 和 Dr. Parker。这五个人每个人都有一个女儿，并且都用其他人的女儿的名字命名了自己的游艇。Sir Barnacle 的游艇是 Gabrielle，Mr. Moore 拥有 Lorna，Mr. Hall 拥有 Rosalind。Colonel Downing 拥 Melissa 是以 Sir Barnacle 的女儿命名的。Gabrielle 的父亲拥有一艘以 Dr. Parker 的女儿命名的游艇。Lorna 的父亲是谁？
