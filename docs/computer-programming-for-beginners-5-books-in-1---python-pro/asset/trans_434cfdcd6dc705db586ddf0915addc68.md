
这与列表的处理方式类似，通过使用“sorted”方法。

本质上，字典是一种重要的数据结构，因为任何需要存储大量属性和值的程序都需要它。例如，你甚至可以定义一个字典来简单统计某个对象的不同状态。之所以可行，是因为每个键实际上都是唯一的，因此你不会为同一个键得到重复的值。这意味着键可以用来存储输入数据，而值则用来存储我们执行任何操作后的结果。例如，如果你想了解某个字母在某个句子中出现的频率，可以遍历所有字符，并将每个字符分配给一个键。

## 创建基础游戏

正如本章开头所述，我们将创建一个非常基础的游戏，在游戏中你将运用之前学到的关于序列的所有知识。这实际上是我们之前编写的简易角色生成器的延续。现在，在开始编码之前，让我们从设计的最初阶段开始。

代码将分为三大块。你需要能够生成角色属性、购买装备并进入战斗。让我们进一步展开这些想法：

- 1. 首先，我们需要存储角色属性。由于需要一个容器，字典可能是理想的选择。玩家将能够决定自己的角色名称、描述、性别和种族。而角色属性，即力量、敏捷、魅力和金币，则将是随机的。我们还会引入一些次要属性，如生命值、法力和护甲。为了生成这些数值，我们将使用 random 模块。我们还没有讨论过这个话题，但你只需要知道，模块是可供调用以执行特定任务的函数集合。Python 模块在使用之前必须先导入到程序中。不过，一旦导入，它们的使用方式与普通方法和函数完全相同。你可以把它们看作是 Python 能力的扩展。

- 2. 在代码的下一个部分，我们将定义“商人”，玩家将在这里花费金币购买各种物品。同样，理想的容器是字典。商人提供的物品会有各自的键，我们将价格（值）与这些键关联起来。

- 3. 最后但同样重要的是，我们将实现战斗系统。角色可以在轮到自己时选择武器并攻击对手。此外，我们不想只看到一些数字，因此还会添加文本来描述造成的伤害量。为此，我们需要使用多个元组。下一个问题是如何处理武器伤害计算。我们在这里稍微“取巧”，为“商人”引入两个额外元素。一个是“攻击伤害”，另一个是“攻击速度”。此外，我们将有一个包含价格、攻击伤害和攻击速度的元组。请记住，这些元素的数值不会改变，因此我们会在程序开头就把它们定义好，尽快解决掉这个麻烦。最后，我们需要让战斗阶段进入循环，直到其中一个角色死亡。

现在我们已经有了程序的总体设计，开始进入开发阶段 2：伪代码！

```text
# declare the constant variables that don’t change their values

# define the trader = {}

#1 while characters < 2

#1.1 declare character profile dictionary

#1.2 Ask the user to insert the following information about their character
# ('Name', 'Description', 'Sex', 'Race')

#1.3 Confirm data

#1.4 Implement random stats generation
# ('Strength', 'Intellect', 'Dexterity', 'Charisma')

#1.5 Implement secondary character stats
# ('health', 'mana', 'armor', 'gold')

# Allow the user to modify certain stats

#1.6 Confirm the character stats

#1.7 Display character stats document

#1.8 Ask the player to buy some gear from the trader

#1.9 loop while purchase not equal to 'no'.

#1.9.1 Display trader’s item list with prices.

#1.9.2 Ask the user to buy items.

#1.9.3 If the player has enough gold and
# the trader has the item available, buy the item.

#1.10 Introduce another player

# Combat section

# Prepare the lists with descriptive text.

# hits = (), misses = (), damage_taken = (), health_update = ()

#2 Player enters battle.

# Player decides which weapon to use.

# As long as the weapon is in his inventory.

# If selected weapon doesn’t exist, player will use his fists.

#3 Loop while opponent [health] > 0 and target[health] > 0:

#3.1 for player in battle:

#3.1.1 Calculate the attack speed

#3.1.2 Calculate the attack damage

#3.1.3 Print damage taken

#3.1.4 if opponent [health] > 0 and target [health] > 0: break

#3.2 Print player progress

#4 Print winner
```

如你所见，这个程序比我们目前设计过的都要复杂一些。在继续之前，请务必注意伪代码的结构和缩进。设计越复杂，你就越应该投入时间做准备。不要把一个应用程序看作是一项需要不知道多少工时才能完成的艰巨任务。相反，把它拆分成更小的任务，整理好代码块和需要解决的问题，然后你可以逐一着手处理。

话虽如此，我们目前拥有的伪代码可以轻松地翻译成 Python 代码。首先有常量变量，然后是 import random 语句。我们将使用 random 的方法。接下来是第一部分，我们在名为“trader”的字典中确定物品。每个元素包含三个元组，分别表示价格、攻击伤害和攻击速度。然后是一组元素，即角色可以购买的物品，如护甲和武器，之后还有额外的四个元组。它们将存放描述武器命中、未命中、伤害报告和生命值更新的文本。毕竟这是一款游戏，你应该花点时间设计描述性文本。它需要符合你的游戏氛围以及你为角色设定的任何目标。

接下来，我们有一个空列表，用于保存玩家档案，它被直观地命名为“players”。这些档案中的每一个随后都会临时存放在一个 character_profile 字典中。其中有四个独立的字段，用户可以在这些字段中输入关于其角色的一些信息。然后我们开始使用 random 模块中的“random.randint(start, end)”来自动生成玩家属性。这本质上是一个随机数生成器，相当于掷骰子。然后根据这些数字生成次要属性，并进行校验，确保它们的值位于 1 到 100 之间，以保持简单和可读性。如果数字不在此范围内，我们就再次掷骰子，直到获得有效结果。在此代码块的末尾，我们打印玩家的角色属性表。

接下来是购买物品的部分，我们实际上可以把它附加到角色生成器上。这样能在一定程度上简化编码，并让设计更加紧凑。此外，我们可以使用“for”循环来遍历玩家可以购买的物品列表。然后通过索引从元组中获取价格。此时，玩家可以做出决定，并将所选物品添加到自己的背包中，同时扣除相应数量的金币作为交换。接着，玩家会被要求选择一件武器；如果角色的背包中没有武器，则默认使用拳头。在幕后实际发生的是，玩家从 trader 字典中访问元组，并将其转换为武器数值。角色的护甲值也采用同样方式处理。根据所有这些数据，构建出一份角色档案。最后，战斗发生在一个 while 循环中，该循环会持续执行，直到其中一方失去全部生命值。循环内部还有另一个循环，用于交换每位玩家的回合。请记住，这个示例中的战斗机制是基于回合制的。概念很简单：嵌套循环借助“enumerate”函数访问玩家索引，然后将其转换为布尔值。一位玩家行动后，“not”运算符会反转该值。这意味着我们有一个攻击者索引和一个目标索引，它们在两名玩家之间互换。

接下来是攻击速度的计算。只要玩家掷出的数字为正数，就能命中目标；负数则视为未命中。我们将数值设置在 0 到 7 之间，但必须加以限制，否则会出现一些意想不到的行为。然后，该数值会在 misses 和 hits 元组中进行校验，并根据结果显示相应的描述文本。消息取决于攻击是成功命中对手还是落空了。该数值也用于伤害计算。请记住，这些数值是在一定限制范围内随机设定的，目的是为游戏提供趣味性，而不是死板的结果。

在最后一部分，我们根据目标受到的伤害，定义从目标生命池中扣除多少生命值。然后更新目标的生命值。只要生命值不等于零或负数，游戏就会继续。当生命值降到零时，我们跳出循环，并判定获胜者。程序在达到最终结果后结束运行。

## 编程练习

至此，你已经学到了大量关于 Python 和编程本身的知识。我们已经为游戏制定了计划，编写了伪代码，并对其进行了详细解释。现在，剩下的事情就交给你了！你已拥有自己编写代码所需的一切。你不需要使用到目前为止所学之外的内容。尤其是，在本次练习中，你应该把重点放在本章所学的内容上。
