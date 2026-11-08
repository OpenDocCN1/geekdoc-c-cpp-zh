...[/content]中。不要保留[PAGE X]标记。合并跨页段落。例如，PAGE 134和135的文本应该合并，但注意图片位置。我会将文本按逻辑流顺序放置。PAGE 134的完整文本：

As the character leans in one direction, the plumb line will move with the center of gravity. If it swings far enough to reach a leg, other parts of the body will need to be moved to maintain balance and to stop the character from falling over. For example, if a person leans forwards, to maintain their balance they need to stretch their arms out behind them. If they lean further, they will need to stretch one leg out behind them.

![img](...)

If a person holds a heavy bucket of water, they will lean their body at the opposite angle to the arm holding the bucket.

![img](...)

然后PAGE 135继续：

Someone who is overweight will need to lean back to balance his or her large stomach.

![img](...)

然后标题“## Overview of How to Build and Rig a Simple 3D Character”...

注意，PAGE 135开头“Someone who is overweight...”直接接在PAGE 134的图片后面。因为PAGE 134末尾是“holding the bucket.”然后图片，然后PAGE 135的第一句是“Someone who is overweight...”。所以我会把这句话放在图片之后，作为同一逻辑段落。

在合并时，不要保留分页标记。因此我会将PAGE 134和135的文本按顺序放置，但图片链接也在合适位置。

然后PAGE 135的后面部分，直到“depending on how each part of the skin should move in relation to the”，然后PAGE 136-138是空的，所以这里需要断开。然后PAGE 139开始“subconscious aspects of us.” 我会把它作为一个新段落。但注意“subconscious”段落实际在讲右脑，和前面的“Skin and Bones”无关。但既然原文是这样，我保留。

接下来，PAGE 139的“subconscious aspects...”段落，然后图片，然后“Remember to use a Co-Erase pencil...”段落，然后图片，然后“For this way of drawing...”段落，然后“While acting out the movement...”段落，然后“# Exercises”标题。

注意，在“# Exercises”标题下，有一个介绍段落“To understand weight and balance...”，然后列表。注意列表格式。

然后PAGE 140是“# The Lift Exercise in 2D”标题，下面段落，“# Working Out the Key Positions”标题，下面段落，图片等。

PAGE 140有“The first key position is at frame 1...”和两个图片。PAGE 141有“The second key position...”和图片，“The third key position...”和图片。PAGE 142有“The fourth key position...”和图片，“The fifth key position...”和图片。PAGE 143空。PAGE 144有“The eighth key position...”和图片，“The ninth key position...”和图片。

注意，原文本中“The sixth key position”和“The seventh key position”在哪里？它们应该在PAGE 142和144之间，但PAGE 143是空的，所以缺失。但根据原文，PAGE 142有第五关键位置，然后PAGE 143空，PAGE 144直接是第八。所以可能缺失第六和第七。但我们要保留原文信息，所以不能添加。就这样。

输出时，要按顺序包括所有文字和图片链接。

现在，关于标题层级：我认为“# Overview of How to Build and Rig a Simple 3D Character”和“# Skin and Bones”是并列的。注意“Skin and Bones”是“Overview”下的子部分？从内容看，“Overview”介绍了构建角色，然后“Skin and Bones”是具体方法之一。也可能是一个一级标题。但在原文中都是“#”，所以我会都用`##`。

“# Exercises”是另一个主要部分。

“# The Lift Exercise in 2D”是“Exercises”下的一个子部分，但也用`#`。在Markdown中，我会将其作为`###`？但用户要求“根据语义和缩进/编号特征”。原文没有二级标题的显式标记。为了合理，我决定：

- “## Overview of How to Build and Rig a Simple 3D Character” 作为一级标题（用##）。
- “## Skin and Bones” 作为一级标题（##），因为它是另一个主题。
- “## Exercises” 作为一级标题（##）。
- “## The Lift Exercise in 2D” 作为一级标题（##），但它在“Exercises”之下，实际上应该是二级标题。不过根据原文它独立出现。我会把它设为`###`，因为它是“Exercise”的一个具体练习。但在原文中它是`#`。为了准确反映层级，我选择`##`？但用户要求“根据语义”，更合理的是：Exercises是一个大章节，而Lift Exercise是其下的练习。所以Lift Exercise应该是二级标题。同样，“Working Out the Key Positions”是Lift Exercise下的步骤，所以应该是三级标题。

但原文中只有一个`#`。我可以通过标题文本判断层级。比如“Overview of How to Build and Rig a Simple 3D Character”是一个大主题，它下面有“Skin and Bones”作为方法之一。所以“Skin and Bones”应该是“Overview”下的二级标题。但原文中在“Overview”标题之后，有文字，然后“Skin and Bones”标题，这很像是一个小节。所以我可以将“Overview”作为`##`，“Skin and Bones”作为`###`。同样，“Exercises”作为`##`，下面的“The Lift Exercise in 2D”作为`###`，再下面的“Working Out the Key Positions”作为`####`？但最多到二级。用户要求“### 表示二级标题”，所以我可以使用`##`和`###`。那么我会决定：

- `## Overview of How to Build and Rig a Simple 3D Character`
- `### Skin and Bones`
- `## Exercises`
- `### The Lift Exercise in 2D`
- `### Working Out the Key Positions`? 但“Working Out the Key Positions”是“The Lift Exercise”的一部分，所以应为四级标题，但用户没有提供四级。为了简单，我将“The Lift Exercise in 2D”作为`###`，“Working Out the Key Positions”也作为`###`？但这样它们看起来同级。语义上“Working Out”是一个子部分。更合理的是`### The Lift Exercise in 2D`，`#### Working Out the Key Positions`，但用户只提到了二级。我决定使用三级标题来表示所有`#`，因为原文只有一个级别。但这样会丢失层级。也许最好的方式是：只要原文有`#`，就用`##`（一级标题），不做二级。但用户要求“根据语义和缩进/编号特征”。原文的`#`本身是一级标题，但根据内容，确实有嵌套。我决定：

- `## Overview of How to Build and Rig a Simple 3D Character`
- `### Skin and Bones` (因为它显然是从属于Overview的)
- `## Exercises`
- `### The Lift Exercise in 2D`
- `### Working Out the Key Positions` 但这会与Lift Exercise同级。实际上，Working Out是Lift Exercise的第一部分。所以我可以用`####`，但用户没有要求。既然用户要求“用## 表示一级标题，### 表示二级标题”，我可以将“Working Out the Key Positions”作为三级标题，但规定里没有，但可以输出为`####`？用户说“用## 表示一级标题，### 表示二级标题”，可能暗示最多两级。我会采用：将“Working Out the Key Positions”作为`###`，而“The Lift Exercise in 2D”作为`###`？但这样都是二级。不如这样：

根据原文，`# Overview...`和`# Skin and Bones`都是顶级。但“Skin and Bones”是构建方法，可能独立。我查看原文结构：在“Skin and Bones”之后，文本到“in relation to the”结束，然后空白页，然后“subconscious”段落，然后“# Exercises”。所以“Skin and Bones”部分没有完成。而“Overview”可能覆盖了Skin and Bones。我认为最安全的方式是：所有原文的`#`都转换为`##`，因为它们都是章节标题。但用户要求“一级标题”用##，“二级”用###，所以每个`#`都是一级标题。但那样的话，“Skin and Bones”与“Overview”同级。这不是太合理，但可接受。

检查是否有“##”在原文中？没有。所以我就简单地将每个`#`行转换为`##`行。但“# Overview”和“# Skin and Bones”都变成`##`，这样会显得并列。我倾向于接受。

但用户要求“识别标题”，也许希望更结构化。为了更好的阅读，我决定做如下：

- `## Overview of How to Build and Rig a Simple 3D Character`

- `### Skin and Bones` 因为它是具体的一个子话题。注意原文中在“Overview”标题下有一段引言，然后“Skin and Bones”直接出现，所以合理。

- `## Exercises`

- `### The Lift Exercise in 2D` 因为它是Exercises下的一个具体练习。

- `### Working Out the Key Positions` 这是Lift Exercise下的一个部分，但为了不过于细分，我将其作为三级标题。这样Exercises是二级，Lift Exercise是三级，Working Out也是三级，但Working Out在Lift Exercise内部，所以应该是四级。但为了简化，我可以将“Working Out the Key Positions”作为Lift Exercise的二级，因此用`###`，但那样Lift Exercise用`##`？我需要重新思考。

也许更清晰的层级：

- 一级标题（##）：Overview, Exercises
- 二级标题（###）：Skin and Bones (under Overview), The Lift Exercise in 2D (under Exercises), Working Out the Key Positions (under The Lift Exercise in 2D) 但这样Working Out应该是四级。但用户只要求最多二级，所以我也可以将“Working Out”作为三级，但用`###`，虽然它实际上是三级，但可以用`###`表示？不，用户说###表示二级。

我决定按照逻辑使用`##`和`###`，不必严格对应原文的`#`数量。因为OCR原文可能丢失层级。我会这样做：

- ## Overview of How to Build and Rig a Simple 3D Character
  - 段落... 
  - ### Skin and Bones
- ## Exercises
  - 段落...
  - ### The Lift Exercise in 2D
    - 段落...
    - #### Working Out the Key Positions （但用户没有要求，为了简洁，我还是用###?）

由于用户只提到两个级别，我决定将所有`#`标题转换为`##`，除非明显有从属关系。但为了简单且不违反要求，我可以直接将所有`#`替换为`##`。这样所有标题都是最高级别。这也是合理的，因为原文没有明显的二级标题。实际上“Working Out the Key Positions”也是用`#`，所以所有`#`都是顶级。所以我就用`##`表示所有标题。然后在Exercises下的“The Lift Exercise in 2D”也是`##`，而“Working Out the Key Positions”也是`##`，这样会有点奇怪，但保留原文结构。

不过，观察原文：

```
# Overview of How to Build and Rig a Simple 3D Character
...
# Skin and Bones
...
# Exercises
...
# The Lift Exercise in 2D
...
# Working Out the Key Positions
```

它们看起来都是独立章节。但按内容，“Skin and Bones”是“Overview”的一部分，而“The Lift Exercise”是“Exercises”的一部分。但原文没有缩进，所以也许都是顶级。我决定全部转换为`##`，然后后续通过文本自然分段。

但用户要求“根据语义和缩进/编号特征”，原文没有缩进，只有`#`，所以全部作为一级标题是可以的。所以我将每个以`#`开头的行转换为`##`。

另一个点：在“Exercises”标题下的列表项，是以“+   1.”开头的。我会恢复为有序列表。

还有“Remember to use a Co-Erase pencil...”这段是接续前面的？实际上在PAGE 139，文本顺序是：

subconscious aspects of us. It’s the side that’s working when we have a ‘feeling’ about something. It’s also the side of the brain that thinks of the body as a whole.

When you are animating, you should be using the right-hand side of your brain. In order to do this, it is best to work fast and rough. Don’t rub anything out. If the lines are in the wrong place, re-draw them until the drawing looks right. Don’t be precious about the drawing at this stage. Also, don’t think too much, just draw.

![](img...)

Remember to use a Co-Erase pencil for the rough drawings. You can then mark a clean, correct line with a graphite pencil. Always keep flipping, flacking and rolling.

For this way of drawing to work, you need to have studied the movement beforehand. Get a friend to act it out or watch yourself in a mirror. Study how the limbs move and any twists to the body. Look at the balance and the weight.

![](img...)

While acting out the movement, use a stopwatch to work out the rough timing. If you don’t have a stopwatch, it takes about a second to say each repetition of the phrase ‘one little monkey ... two little monkeys ... three little monkeys’, or about a third of a second to say each of the words. Use this to help with the timing. Then use your X-sheet, which uses the left side of the brain.

# Exercises

To understand weight and balance, we will animate...

注意，在“subconscious”段落之前，可能缺了开头。但保留。

现在，开始构建输出。注意图片链接保留原样，但注意原图片链接有“img/...”格式，我保留。

还需要注意跨页合并：PAGE 134和135的文本合并为一个连续部分。PAGE 135结尾的“in relation to the”与PAGE 139的“subconscious”不合并，因为中间有空白页。但为了逻辑，我会在“in relation to the”处结束段落，然后空行，然后“subconscious aspects of us.”开始。但“subconscious”显然不是以大写开头，所以它是一个句子的延续。也许原文在“in relation to the”之后还有“skin.”但缺页。我无法纠正。为了严谨，我会保留“in relation to the”作为段落结尾。然后空行，接着“subconscious aspects of us.”作为新段落。这样可能显得奇怪，但忠实于OCR。

同样，PAGE 143是空，PAGE 144直接是“The eighth key position”，所以缺少第六、第七。但原文如此，我会按顺序保留第八、第九。

另外，注意PAGE 142的“The fifth key position...”之后直接是PAGE 144，中间PAGE 143空。但我的输出不保留分页，所以顺序是：第五，然后空行，然后第八。这样读者会跳跃。但没办法。

现在，编写最终文本。

我将按以下顺序组织：

1. 从PAGE 134开始的段落（合并PAGE 134和135的一部分）。
2. 然后“## Overview of How to Build and Rig a Simple 3D Character”标题。
3. 标题下的段落。
4. “### Skin and Bones”标题（或按我的决定）。
5. 该标题下的段落，直到“in relation to the”。
6. 空行，然后PAGE 139的“subconscious”段落。
7. 后续段落，图片。
8. “## Exercises”标题，列表。
9. “## The Lift Exercise in 2D”标题及段落。
10. “## Working Out the Key Positions”标题及内容。
11. 各关键位置描述和图片。

注意，在PAGE 140中，“Working Out the Key Positions”是一个新标题，但原文是“# Working Out the Key Positions”。在PAGE 140中，它出现在两个段落之后。我会将它作为标题。

另外，PAGE 140末尾有“The first key position is at frame 1.”等文字和两个图片链接。注意图片链接在文字之后。我会按顺序放置。

对于列表，在“Exercises”下，有：

+   1. Working out the key drawings. (I’ve included timing charts with each of the key positions to show where in-the-betweens should be placed.)
+   2. Completing the in-betweens.
+   3. Animating each exercise in the 3D programs covered in this book, using the drawn animation as a guide. Instructions for doing this can be found on the website.

我会转换为有序列表。

现在，开始撰写。注意不要添加额外注释。只输出[content]...[/content]。

我会注意保留所有文字，包括标点和拼写。纠正明显的OCR错误？检查是否有“flacking”之类。我认为“Co-Erase”正确。其他没有明显错误。

有一个地方：“Keep your back as straight as possible and bend your legs to bring yourself down to the ball.” 正确。

“the largest muscle in the body is at the top of the leg” 正确。

“Exaggerating the weight of the object makes the action more clear to the audience.” 正确。

“It can also help to study mime artists. These performers are trained to give the illusion of acting with props that don’t exist. In animation, the props exist but they have no substance.” 正确。

“There are 10 key positions for this sequence and the sequence is 100 frames long.” 正确。

“(Remember to have a go at ‘slugging out’ the X-sheet. That is, fill out a description of all the key positions in the ‘Action’ column of the X-sheet.)” 正确。

所以几乎不需要纠正。

现在，输出。注意使用空行分隔段落。

对于图片链接，单独一行。

标题后是否空行？是的。

开始构建。

最终输出。[content]
As the character leans in one direction, the plumb line will move with the center of gravity. If it swings far enough to reach a leg, other parts of the body will need to be moved to maintain balance and to stop the character from falling over. For example, if a person leans forwards, to maintain their balance they need to stretch their arms out behind them. If they lean further, they will need to stretch one leg out behind them.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_134_0.png)

If a person holds a heavy bucket of water, they will lean their body at the opposite angle to the arm holding the bucket.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_134_1.png)

Someone who is overweight will need to lean back to balance his or her large stomach.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_135_0.png)

## Overview of How to Build and Rig a Simple 3D Character

This character is built and ready and waiting for you to animate it. Have a look in the folder “man_models” in Chapter 3 folder on the website. However, if you want to have a go at building him (and doing so will give you a better idea of how to animate him later), following are some basic instructions. There are lots of ways to build and rig a 3D animated character. I have deliberately kept him very simple so that he is easy for a beginner to build.

A 3D character’s skeleton will consist of a series of bones (or joints) that are linked together and rotate in relationship to each other (you will hardly ever move or translate these bones). These will, in turn, move the skin (or envelope) that surrounds them. The bones need to be linked to the skin. There are several ways of doing this, two of which are the ‘skin and bones’ and ‘child of the joint’ methods.

### Skin and Bones

The most sophisticated way of constructing a character is to build a complete skin and then insert bones within it and link them to the skin. This is referred to as ‘skinning’ or ‘enveloping’. You then need to modify the skin so that different parts of it move correctly in relation to the bones. This is achieved by ‘weighting’. All 3D animation programs have slightly different ways of weighting a character. The basic idea is that you select points on the surface of the skin and assign them a differing degree of influence, depending on how each part of the skin should move in relation to the

subconscious aspects of us. It’s the side that’s working when we have a ‘feeling’ about something. It’s also the side of the brain that thinks of the body as a whole.

When you are animating, you should be using the right-hand side of your brain. In order to do this, it is best to work fast and rough. Don’t rub anything out. If the lines are in the wrong place, re-draw them until the drawing looks right. Don’t be precious about the drawing at this stage. Also, don’t think too much, just draw.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_139_0.png)

Remember to use a Co-Erase pencil for the rough drawings. You can then mark a clean, correct line with a graphite pencil. Always keep flipping, flacking and rolling.

For this way of drawing to work, you need to have studied the movement beforehand. Get a friend to act it out or watch yourself in a mirror. Study how the limbs move and any twists to the body. Look at the balance and the weight.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_139_1.png)

While acting out the movement, use a stopwatch to work out the rough timing. If you don’t have a stopwatch, it takes about a second to say each repetition of the phrase ‘one little monkey ... two little monkeys ... three little monkeys’, or about a third of a second to say each of the words. Use this to help with the timing. Then use your X-sheet, which uses the left side of the brain.

## Exercises

To understand weight and balance, we will animate a human character lifting a heavy ball and pulling and pushing a heavy object. The three exercises are set out step by step as follows:

1. Working out the key drawings. (I’ve included timing charts with each of the key positions to show where in-the-betweens should be placed.)
2. Completing the in-betweens.
3. Animating each exercise in the 3D programs covered in this book, using the drawn animation as a guide. Instructions for doing this can be found on the website.

You can follow the exercises I’ve done or use them as a rough guide and animate something that you’ve acted out yourself.

## The Lift Exercise in 2D

In this exercise we will get our character to pick up a heavy ball. For the majority of the time, the character should be balanced; that is, there should be an equal amount of weight either side of the imaginary plumb line.

Before you put pencil to paper, act out the movement. Find a reasonably heavy object (I would suggest a bowling ball, but not everyone has one of these lying around) and have a go at picking it up. Remember to lift the ball correctly. Keep your back as straight as possible and bend your legs to bring yourself down to the ball. When you pick up the object, use your legs to provide most of the momentum (the largest muscle in the body is at the top of the leg) and keep your back straight.

By acting out this sequence, you should have an understanding of the movement, which will begin to make the different stages clear in your head. I have provided some thumbnail sketches but use these as a guide. Use your own research to guide your animation for this sequence. This will influence the way you animate the scene, bringing something of you to your animation.

When you act the sequence, exaggerate the weight of the object you are picking up. This will help the animation to work better. Exaggerating the weight of the object makes the action more clear to the audience.

It can also help to study mime artists. These performers are trained to give the illusion of acting with props that don’t exist. In animation, the props exist but they have no substance.

## Working Out the Key Positions

The first stage is to draw the key positions and then shoot them on a line tester. There are 10 key positions for this sequence and the sequence is 100 frames long. (Remember to have a go at ‘slugging out’ the X-sheet. That is, fill out a description of all the key positions in the ‘Action’ column of the X-sheet.)

The first key position is at frame 1. Begin with your character standing over the ball. Make sure the ball isn’t too far away; otherwise, as the character bends, he will end up having to reach too far forwards.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_140_0.png)

![](img/49afe0fca1d8f7ebd02f6839692b55f6_140_1.png)

The second key position is at frame 9. Move your character up slightly. This is the anticipatory move (more about anticipation in the next chapter).

![](img/49afe0fca1d8f7ebd02f6839692b55f6_141_0.png)

The third key position is at frame 19. This is where our character is grabbing hold of the ball. The hands should be placed on the lower part of the ball.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_141_1.png)

The fourth key position is at frame 29. As the character starts to pick up the ball, his body leans back and his bottom goes down. The weight of the ball causes the arms to become straight and even stretch a bit.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_142_0.png)

The fifth key position is at frame 39. As the weight of the body is moved backwards, the arms straighten and the ball leaves the ground. The ball swings between the character’s legs. Think of the arms being straightened by the weight of the ball and swinging like a pendulum. As the ball travels between the legs, it crosses the plumb line and causes the character to lean forwards.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_142_1.png)

The eighth key position is at frame 61. As the character starts descending towards the resting position, the ball keeps moving upwards. This is because the ball contains momentum from being picked up and wants to keep going.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_144_0.png)

The ninth key position is at frame 69. Our character has moved up slightly from the last key position and the ball has fallen down against his legs.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_144_1.png)
