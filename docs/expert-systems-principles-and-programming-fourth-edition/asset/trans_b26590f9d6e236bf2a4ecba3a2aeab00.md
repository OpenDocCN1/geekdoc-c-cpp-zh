

(bind ?answer (read))
(while (and (neq ?answer yes) (neq ?answer no))
  (printout t ?question " (yes or no) ")
  (bind ?answer (read)))
(return ?answer))

(defrule ask-decision-node-question
  ?node <- (current-node ?name)
  (node (name ?name)
        (type decision)
        (question ?question))
  (not (answer ?))
  =>
  (assert (answer (ask-yes-or-no ?question)))))

第二个模式仅在当前节点为决策节点时才匹配。第三个模式检查问题是否已被回答。在规则的右侧（RHS）中，ask-yes-or-no 函数会反复提问，直到提供 yes 或 no 答案为止。根据答案，将触发以下两条规则之一：

(defrule proceed-to-yes-branch
  ?node <- (current-node ?name)
  (node (name ?name)
        (type decision)
        (yes-node ?yes-branch))
  ?answer <- (answer yes)
  =>
  (retract ?node ?answer)
  (assert (current-node ?yes-branch))))

(defrule proceed-to-no-branch
  ?node <- (current-node ?name)
  (node (name ?name)
        (type decision)
        (no-node ?no-branch))
  ?answer <- (answer no)
  =>
  (retract ?node ?answer)
  (assert (current-node ?no-branch))))

在两条规则中，current-node 事实会被撤销，然后根据问题的答案用新的断言进行更新。answer 事实会被撤销，以便 ask-decision-node-question 规则再次被激活。

下一条规则询问答案节点是否做出了正确的猜测。它与 ask-decision-node-question 规则的作用类似：

(defrule ask-if-answer-node-is-correct
  ?node <- (current-node ?name)
  (node (name ?name) (type answer)
       (answer ?value))
  (not (answer ?))
  =>
  (printout t "I guess it is a " ?value crlf)
  (assert
  (answer (ask-yes-or-no "Am I correct?"))))

如果答案不是 yes 或 no，则 bad-answer 规则会导致 ask-if-answer-node-is-correct 规则再次被激活。如果答案是 yes 或 no，则将触发以下两条规则之一。如果答案节点的值得到验证，则会断言 ask-try-again 事实，以指示应询问用户是否继续。如果答案错误，则会发生学习，并断言 replace-answer-node 事实以指示要替换的节点名称。在任一情况下，current-node 和 answer 事实都会被撤销：

(defrule answer-node-guess-is-correct
?node <- (current-node ?name)
(node (name ?name) (type answer))
?answer <- (answer yes)
=>
(assert (ask-try-again))
(retract ?node ?answer))

(defrule answer-node-guess-is-incorrect
?node <- (current-node ?name)
(node (name ?name) (type answer))
?answer <- (answer no)
=>
(assert (replace-answer-node ?name))
(retract ?node ?answer))

以下三条规则用于确定用户是否想要继续。ask-try-again 规则会询问“再试一次？”问题。同样，如果给出的答案不是 yes 或 no，则 bad-answer 规则会触发。如果答案是 yes，one-more-time 规则会将 current-node 事实重置为根节点，以重新开始猜测过程。如果答案是 no，则表示决策树的事实将使用 save-facts 命令保存到 animal.dat 文件中：

(defrule ask-try-again
(ask-try-again)
(not (answer ?))
=>
(assert (answer (ask-yes-or-no "Try again?"))))

(defrule one-more-time
?phase <- (ask-try-again)
?answer <- (answer yes)
=>
(retract ?phase ?answer)
(assert (current-node root)))

(defrule no-more
?phase <- (ask-try-again)
?answer <- (answer no)
=>
(retract ?phase ?answer)
(save-facts "animal.dat" local node))

最后，如果答案错误，以下规则将添加一个新的决策节点，使决策树能够学习：

(defrule replace-answer-node
?phase <- (replace-answer-node ?name)
?data <- (node (name ?name)
(type answer)
(answer ?value))
=>
(retract ?phase)
; Determine what the guess should have been
(printout t "What is the animal? ")
(bind ?new-animal (read))
; Get the question for the guess
(printout t "What question when answered yes ")
(printout t "will distinguish " crlf " a ")
(printout t ?new-animal " from a " ?value)
(printout t "Now I can guess " ?new-animal crlf)
; Create the new learned nodes
(bind ?newmodel (gensym*))
(bind ?newnode2 (gensym*))
(modify ?data (question ?question)
(yes-node ?newmodel)
(no-node ?newnode2))
(assert (node (name ?newmodel)
(type answer)
(answer ?new-animal)))
(assert (node (name ?newnode2)
(type answer)
(answer ?value)))
; Determine if the player wants to try again
(assert (ask-try-again)))

replace-answer-node 规则会要求正确识别该动物，并提供一个能将该动物与决策树之前识别为正确答案的动物区分开来的问题。旧的答案节点将被替换为决策节点，并创建两个答案节点作为新学习问题的答案。gensym* 函数（每次调用时生成一个唯一符号）用于为两个新答案节点各提供一个名称。然后会断言 ask-try-again 事实，以确定是否应再次运行程序。

## 决策树程序的逐步跟踪

可以通过观察决策树程序的执行来了解其行为。假设决策树规则已加载，且包含表示初始决策树事实的文件 animal.dat 已创建，则以下对话显示了执行 reset 命令后系统的状态：

CLIPS> (watch facts.)
CLIPS> (watch rules.)
CLIPS> (reset.)
==> f-0 (initial-fact)
CLIPS> (agenda.)
0 initialize: f=0,
For a total of 1 activation.
CLIPS>

initialize 规则因缺少根节点事实而被激活。允许 initialize 规则触发将进入决策树。请注意，以下跟踪中的一些输出已缩进以提高可读性：

CLIPS> (run 1.)
FIRE 1 initialize: f=0,
==> f-1 (node (name root) (type decision)
(question "Is the animal warm-blooded?")
(yes-node node1) (no-node node2)
(answer nil))
==> f-2 (node (name node1) (type decision)
(question "Does the animal purr?")
(yes-node node3) (no-node node4)
(answer nil))
==> f-3 (node (name node2) (type answer)
(question nil) (yes-node nil)
(no-node nil) (answer snake))
==> f-4 (node (name node3) (type answer)
(question nil) (yes-node nil)
(no-node nil) (answer cat))
==> f-5 (node (name node4) (type answer)
(question nil) (yes-node nil)
(no-node nil) (answer dog))
==> f-6 (current-node root)
CLIPS> (agenda.)
0
ask-decision-node-question: f-6,f-1,
For a total of 1 activation.
CLIPS>

initialize 规则使用 load-facts 函数加载决策树。current-node 事实被设置为根节点事实。由于根节点是决策节点，因此激活了 ask-decision-node-question 规则。允许此规则及关联的 proceed-to-yes-branch 规则触发，会产生以下对话：

CLIPS> (run 2.)
FIRE 1 ask-decision-node-question: f-6,f-1,
Is the animal warm-blooded? (yes or no) yes.
==> f-7 (answer yes)
FIRE 2 proceed-to-yes-branch: f-6,f-1,f-7
<== f-6 (current-node root)
<== f-7 (answer yes)
<== f-8 (current-node node1)
CLIPS> (agenda.)
ask-decision-node-question: f-8,f-2,
For a total of 1 activation.
CLIPS>

与根决策节点关联的问题是“该动物是温血动物吗？”由于对问题的回答是 yes，proceed-to-yes-branch 规则将决策节点的左侧节点（node1）设置为当前节点。由于 node1 也是决策节点，因此规则 ask-decision-node-question 再次被激活。允许接下来的两条规则再次触发，会产生以下对话：

CLIPS> (run 2.)
FIRE 1 ask-decision-node-question: f-8,f-2,
Does the animal purr? (yes or no) no.
==> f-9 (answer no)
FIRE 2 proceed-to-no-branch: f-8,f-2,f-9
<== f-8 (current-node node1)
<== f-9 (answer no)
<== f-10 (current-node node4)
CLIPS> (agenda.)
0
ask-if-answer-node-is-correct: f-10,f-5,
For a total of 1 activation.
CLIPS>

