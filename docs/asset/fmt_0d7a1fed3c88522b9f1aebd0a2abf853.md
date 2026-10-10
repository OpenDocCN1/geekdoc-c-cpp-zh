
```
alyssa-hacker enters lobby-7
alyssa-hacker says: Hi gjs
ben-bittiddle enters lobby-7
ben-bittiddle says: Hi alyssa-hacker gjs
registrar enters lobby-7
registrar says: Hi ben-bittiddle alyssa-hacker gjs
```

# 真难过-gjs 喜欢黑板。让我们继续在四处看看。

`(go up)`

`gjs` 通过 `up` 出口离开

`gjs` 进入了 `barker-library`

你处于 `barker-library`

你看到这里：`engineering-book`

你可以离开：`up`（向上）`down`（向下）

听到了一声惊天动地、刺心肺的尖叫……

显然，一个巨魔（可能是注册员）吃掉了某人。

然而，这里有一本可以拿走的书，我们拿了它并回到了教室。

`(take-thing 'engineering-book)`

`gjs` 捡起了 `engineering-book`

`(down)`

`gjs` 通过 `down` 出口离开

`gjs` 进入了 `10-250`

你处于 `10-250`

你的包里装有：`engineering-book`

你看到出口：`blackboard`（黑板）

你可以离开：`up`（向上）`down`（向下）

我们从教室回到 `lobby-10`，在那里我们遇到了 `lambda-10`，他立刻地偷走了我们的书。

`(down)`

`gjs` 通过 `down` 出口离开

`gjs` 进入了 `lobby-10`

`gjs` 说：Hi lambda-man

你处于 `lobby-10`

你的包里装有：`engineering-book`

你看到这里：`lambda-man`

你可以离开：`lobby-7` `infinite-corridor`（无限走廊）`great-court`（大庭院）

你可以离开：`east`（东）`south`（南）`west`（西）`up`（上）

`alyssa-hacker` 进入 `lobby-10`

`alyssa-hacker` 说：Hi gjs lambda-man

`lambda-man` 从 `gjs` 手里拿走了 `engineering-book`

`gjs` 说：Yaaah!我不开心了！

## 对象类型

在我们的游戏中创建一个对象，我们使用 `make-property` 定义一些属性，使用 `make-type` 定义一个谓词，通过 `type-instantiator` 获取谓词关联的实例化器，并用适当参数调用该实例化器。

我们如何创建一个巨魔？巨魔的 `make-troll` 构造函数接受参数，用于指定特定正在构建的巨魔的特定属性值。巨魔将在给定位置创建，并具有躁动（移动的倾向）、贪婪（拿走东西的倾向）和饥饿（咬他人的倾向）。

```
(define (create-troll name place restlessness hunger)
  'name name
  'location place
  'restlessness restlessness
  'acquisitiveness 1/10
  'hunger))
```

我们创建了两个巨魔：`grendel` 和 `registrar`。它们最初被放在随机的位置，具有某些随机倾向。

```
(define (create-trolls places)
  (map (lambda name)
    (create-troll name
      (random-choice places)
      (random-bias 3)
      (random-bias 3)))
'(grendel registrar)))
```

`random-choice` 过程从提供的列表中随机选择一个项目。`random-bias` 过程选择一个数字（在此情况下为 1、2 或 3）并返回它的倒数。

巨魔被定义为一个谓词，仅对巨魔时为真。`make-type` 过程接收类型名称以及对巨魔特有属性的描述符。（只有巨魔拥有饥饿属性）。

```
(define troll:hunger)
  (make-property 'hunger predicate bias))
```

```
(define troll?)
  (make-type 'troll (list troll:hunger))
```

巨魔是一种特定类型的自主代理。因此，巨魔集合是自主代理集合的子集 `(<=)`。

```
(set-predicate!= troll? autonomous-agent?)
```

巨魔的构造函数直接派生自定义类型的谓词，饥饿属性的访问器也是如此。

```
(define make-troll
(type-instantiator troll?))
```

```
(define get-hunger
(property-getter troll:hunger?))
```

自主代理偶尔会受到“时钟”`clock`的刺激以采取某些动作。巨魔的独特动作是咬其他人。

```
(define-clock-handler troll? eat-people!)
```

通过掷偏向硬币来决定巨魔此时是否饥饿。如果饥饿了，它会寻找其他人（巨魔也是人！），如果有，它会选择一个咬，导致受害者遭受伤害。叙述者会描述发生的事情。

```
(define (eat-people troll!)
  (if (flip-coin (get-hunger troll))
  (let ((people (here troll)))
    (if null people)
      (narrate! (list troll "belly rumbles"))
      (let ((victim (random-choice people)))
        (narrate! (list troll "takes a bite out of" victim))
        (suffer! (random-number 3)))))
```

`flip-coin` 过程生成 0 到 1 之间的随机分数。如果该分数大于参数，则返回真。`random-number` 过程返回一个小于或等于其参数的正数。`narrator!` 过程用于为故事添加旁白。`narrator!` 的第二个参数（上面的 troll）可以是任何具有位置的对象。叙述者会宣布它的第一个参数。

我们说巨魔是一种自主代理。自主代理类型由其谓词定义，该谓词指定了此类代理所需的属性。我们还规定了自主代理集合是所有对象的子集。

```
(define autonomous-agent:restlessness
  (make-property 'restlessness predicate bias?))
```

```
(define autonomous-agent:acquisitiveness
  (make-property 'acquisitiveness predicate bias?))
```

```
(define autonomous-agent?
  (make-type 'autonomous-agent (list autonomous-agent:restlessness autonomous-agent:acquisitiveness)))
```

```
(set-predicate!= autonomous-agent? person?)
```

巨魔的构造函数指定了 `restlessness` 和 `acquisitiveness` 属性的值，除了饥饿属性外还需要制作自主代理。由于巨魔是自主代理，它们还必须具有 `person` 属性及其所有超集属性的值。在这个系统中，所有属性都有默认值，如果未指定，则会自动填充。例如，所有对象都需要一个名称；名称是未指定的。巨魔的构造函数指定了制作一个自主代理所需的 `restlessness` 和 `acquisitiveness` 属性值，以及饥饿属性。由于巨魔是自主代理的属性值。

## 通用过程

现在我们看到通用过程是如何构建的，我们将看到如何实现它们。具体来说，我们将看到通用过程是描述行为的有效工具。`eat-hunger` 是通过 `property-getter` 实现的，它接收一个参数。

```
(define move! destination actor)
  (generic-move! thing
    (get-location)
    destination
    actor))
```

`move!` 是用更通用的过程 `generic-move!` 实现的，该过程接收四个参数：要移动的物体、物体的位置以及移动过程的执行者。这个过程是通用的，因为移动行为可能取决于所有参数的类型。当我们创建 `generic-move!` 时，还指定了一个非常通用的处理器来捕获未被更具体的处理器覆盖的情况（针对特定的参数类型）。

```
(define generic-move!
  (most-specific-procedure-handler 'generic-move! 4 #f))
```

```
(define-generic-generic-procedure generic-move!
  (match-args thing? container? container? person?)
  (lambda (thing from to actor)
    (tell! (list "is not movable"))))
```

通用过程的真正威力通过移动物品的机制得到了阐明。例如，当我们捡起工程书时，我们将它从房间移动到包里。这是通过 `move` 过程实现的：

```
(define move! thing destination actor)
  (generic-move! thing
    (get-location thing)
    destination
    actor))
```

`clock-tick!` 过程被用来触发动作，而不是计算值。注意，我们指定的 `action-handler` 将在超集的动作之后执行。我们可以通过更改调用的顺序来先执行给定的动作，后执行其他的。

```
(define (define-clock-handler type)
  (define-generic-procedure clock-tick)
  (match-args type)
  (lambda (super) (action))))
```

这种通用过程支持“链式调用”，每个处理器在调用时都会接收一个额外的参数（在本例中为 super）。这与 Java 等语言中使用的机制基本相同，尽管在那里它是通过关键字而不是参数完成的。

```scheme
(define (take-thing name)
  (let ((thing (find-thing name (here))))
    (if thing
        (take-thing! thing my-avatar)
        'done))
```

```scheme
(define (take-thing! thing person)
  (move! thing (get-bag person) person))
```

这里有两个过程。第一个是用户界面过程，它为玩家提供了一种方便的方式，通过提供名称来描述要取走的物品。它调用了第二个过程，这是一个内部过程，该过程也被其他地方使用。

为了使这个功能工作，我们为 `generic-move!` 提供了一个处理程序，它专门用于从某个位置移动可移动物体：

```scheme
(define-generic-procedure-handler generic-move!
  (match-args mobile-thing? place? bag? person?)
  (lambda (mobile-thing from to actor)
    (let ((new-holder (get-holder to)))
      (cond (eqv? actor new-holder)
            (narrate! list actor
                  "picks up" mobile-thing
                  actor)
            else
            (narrate! list actor
                  "picks up" mobile-thing
                  "and gives it to" new-holder)
            actor))
      (if (not eqv? actor new-holder)
        (say! new-holder (list "Whoa!, dude!"))
      (move-internal! mobile-thing from to))))
```

执行者 `actor` 正在拿物品，执行者是新的持有者。

但执行者可能在某个位置拿起物品并将其放入某人的包中！

`say!` 过程用于表示某人说了一些话。它的第一个参数是说话的人，第二个参数是所说的内容。`move-internal` 过程实际上将对象从一个地方移动到另一个地方。

要丢弃物品，我们使用 `drop-thing` 过程将其从我们的包移动到当前位置：

```scheme
(define drop-thing name)
  (let ((thing (find-thing name my-avatar)))
    (if thing
        (drop-thing! my-avatar)
        'done))
```

```scheme
(define drop-thing! thing person)
  (move! thing (get-location person) person)
```

以下 `generic-move!` 的处理程序允许丢弃物品。执行者可能从它自己的包中丢弃物品，也可能从另一个人的包中拿起某物并丢弃。

```scheme
(define-generic-procedure-handler generic-move!)
  (match-args mobile-thing? bag? place? person?)
  (lambda (mobile-thing from actor)
    (let ((former-holder (get-holder from)))
      (cond ((eqv? actor former-holder))
            (narrate! list actor)
                  "drops" mobile-thing
              actor)
            else (narrate! list actor)
                  "takes" mobile-thing
                  "from" former-holder
                  "and drops it"
                  actor)))
      (if (not eqv? actor former-holder)
        (say! former-holder)
        (list "What did you do that for?" from to)))
    (move-internal! mobile-thing from to))))
```

另一个 `generic-move!` 处理程序通过将物品从一个包移动到另一个包来实现礼物或偷取。在这里，行为取决于执行者、物品的原持有者和最终持有者之间的关系。

```scheme
(define-generic-procedure-handler generic-move!)
  (match-args mobile-thing? bag? bag? person?)
  (lambda (mobile-thing from actor)
    (let ((former-holder (get-holder from)))
          (new-holder (get-holder to)))
      (cond ((eqv? (list new-holder "is already carrying"
                    mobile-thing)
            (tell! actor))))
```
