

如果答案为否，则当前位置设置为当前位置连接到否（或右）分支的子节点。如果在任何时刻答案节点成为当前位置，则答案节点的值是通过咨询决策树得出的答案。否则，处理决策节点的过程将重复，直到到达答案节点。此算法的伪代码如下：

```
procedure Solve_Binary_Tree
Set the current location in the tree
to the root node.
while the current location is a decision node do
Ask the question at the current node.
if the reply to the question is yes
Set the current node to the yes branch.
else
Set the current node to the no branch.
end if
end do
Return the answer at the current node.
end procedure
```

## 具有多分支的决策树

仅允许从决策节点产生二元分支的决策树，难以表示允许一组响应或一系列案例的决策。为葡萄酒示例构建的二元决策树很好地说明了这种低效性。如果主菜是鱼，在确定最佳颜色为白色之前，必须做出三个决策：必须全部询问“主菜是红肉吗？”、“主菜是家禽吗？”和“主菜是鱼吗？”这些问题。一个更直接的问题，可以使决策节点简洁地表达，是“主菜是什么？”能够处理此问题的决策节点必须允许多个分支，给定一系列可能的决策（在此例中为红肉、家禽、鱼和其他）。图 12.2 显示了图 12.1 的修改版决策树，现在通过对 Solve_Binary_Tree 算法进行简单修改来允许多个分支：

```
procedure Solve_Tree
Set the current tree location to the root node.
while the current location is a decision node do
Ask the question at the current node until
an answer in the set of valid choices
for this node has been provided.
Set the current node to the child node of
the branch associated with the choice
selected.
end do
Return the answer at the current node.
end procedure
```

### 图 12.2 具有多分支的决策树

![](img/2c460d4de56b7ffaad3834eee20beaa0_730_0.png)

## 能够学习的决策树

在学习过程中向决策树添加新知识有时很有用，如常用的动物识别决策树示例所示。一旦决策树到达一个答案，它会询问答案是否正确，如果正确，则不再执行其他操作。但是，如果答案不正确，则会修改决策树以容纳正确答案。答案节点将被替换为一个决策节点，该节点包含一个问题，用于区分节点中的旧答案和未被正确猜出的答案。图 12.3 显示了一个按特征对动物进行分类的决策树。这个决策树有些天真（它只知道三种动物），需要学习。

### 图 12.3 动物识别决策树

![](img/2c460d4de56b7ffaad3834eee20beaa0_730_1.png)

使用该树的示例猜测会话可能如下进行：

```
Is the animal warm-blooded? (yes or no) yes.
Does the animal purr? (yes or no) no.
I guess it is a dog
Am I correct? (yes or no) no.
What is the animal? bird.
What question when answered yes will distinguish
a bird from a dog? Does the animal fly?
Now I can guess bird
Try again? (yes or no) no.
```

会话可以持续下去，决策树将学习越来越多的信息。图 12.4 显示了上述会话后的决策树表示。以这种方式学习的一个缺点是，决策树可能最终既不是非常层级化的结构，也不是在猜测合适动物时非常高效。高效的决策树应使从根到所有路径的答案节点的分支数量大致相同。

### 图 12.4 学习鸟类后的动物识别决策树

![](img/2c460d4de56b7ffaad3834eee20beaa0_731_0.png)

修改 Solve_Tree 算法以加入学习功能的伪代码如下：

```
procedure Solve_Tree_and_Learn
Set the current location in the tree
to the root node
while the current location is a decision node do
  Ask the question at the current node.
  if the reply to the question is yes
    Set the current node to the yes branch.
  else
    Set the current node to the no branch.
  end if
end do
Ask if the answer at the current node is
correct.
if
  if the answer is correct
    Return the correct answer.
  else
    Determine the correct answer.
    Determine a question which when answered yes
    will distinguish the answer at the current
    node from the correct answer.
    Replace the answer node with a decision node
    that has as its no branch the current
    answer node and as its yes branch an
    answer node with the correct answer.
    The decision node's question should be
    the question which distinguishes the
    two answer nodes.
  end if
end if
end procedure
```

## 基于规则的决策树程序

确定如何在 CLIPS 中实现学习决策树的第一步是决定知识应如何表示。由于决策树必须学习，将树表示为事实而不是规则可能很有价值，因为事实可以轻松添加和删除，以便在学习过程中更新树。一组 CLIPS 规则可用于通过使用基于规则的方法实现 Solve_Tree_And_Learn 算法来遍历决策树。决策树的每个节点将表示为一个事实。以下 deftemplate 将用于表示答案节点和决策节点：

```
(deftemplate node
  (slot name)
  (slot type)
  (slot question)
  (slot yes-node)
  (slot no-node)
  (slot answer))
```

其中，*名称* 槽是节点的唯一名称，*类型* 槽是节点的类型，包含值 *答案* 或 *决策*。*问题*、*是节点* 和 *否节点* 槽仅用于决策节点。*问题* 槽是在遍历问题节点时提出的问题。*是节点* 槽是问题得到肯定回答时应转到的节点，*否节点* 槽是问题得到否定回答时应转到的节点。*答案* 槽仅由答案节点使用，是在遍历答案节点时决策树的答案。

由于动物程序将学习，因此有必要存储一个运行到下一个运行中所学到的信息。由于决策树将结构化为一组事实，将它们以 *加载事实* 命令格式存储在文件中，并在程序开始时使用 *加载事实* 命令断言它们，在程序结束时使用 *保存事实* 命令保存它们将很有用。对于此程序，事实将存储在名为 animal.dat 的文件中。如果使用图 12.3 作为初始决策树，则文件 animal.dat 应包含以下文本。请注意，根节点已被命名为 root，其他每个节点都已赋予唯一名称。还请注意，某些槽（例如答案节点的 *决策*、*是节点* 和 *否节点* 槽）保持未指定，因为这些将被赋予默认值（我们的程序不会在意槽中放置什么值）：

```
(node (name root) (type decision)
   (question "Is the animal warm-blooded?")
   (yes-node node1) (no-node node2))
(node (name node1) (type decision)
   (question "Does the animal purr?")
   (yes-node node3) (no-node node4))
(node (name node2) (type answer) (answer snake))
(node (name node3) (type answer) (answer cat))
(node (name node4) (type answer) (answer dog))
```

现在必须编写遍历决策树的规则。以下规则将初始化学习决策树程序：

```
(defrule initialize
   (not (node (name root)))
   =>
   (load-facts "animal.dat")
   (assert (current-node root)))
```

此 *初始化* 规则将在根节点不在事实列表中时触发。*初始化* 规则的操作将决策树表示加载到事实列表中，并断言一个事实，指示当前感兴趣的节点是根节点。

下一个 deffunction 和规则会询问与决策节点关联的问题，然后断言一个包含问题答案的事实：

```
(deffunction ask-yes-or-no (?question)
   (printout t ?question " (yes or no) ")
```

