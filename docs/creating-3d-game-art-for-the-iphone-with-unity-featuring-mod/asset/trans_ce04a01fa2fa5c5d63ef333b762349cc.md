

![](img/d3e3fa4010906e98ec76be003a6e31c2_183_0.png)

**图 7.13** 片段在轨道“属性”面板中的混合模式设置为“添加”。

现在，射击动画以叠加方式混合在奔跑动画之上。这也是你在 Unity 的动画系统中处理动画混合时发生的情况。仅使用 Blender 的 NLA 编辑器，你就能拥有更加精细的工作流，因为你可以构建动作（Actions）并将它们分层放入 NLA 中。NLA 还允许你对动画进行一些交互式调整，例如通过调整“播放设置”来加快或减慢动画速度，如图 7.14 所示。

![](img/d3e3fa4010906e98ec76be003a6e31c2_183_1.png)

**图 7.14** 你可以通过更改“缩放”属性，在“播放设置”中调整片段的速度。

此时，通过 NLA 编辑器混合射击和奔跑动作后，你可以将此动画导出到 Unity iOS，从而得到可直接使用的“边跑边射击”动画。然而，正如我们之前讨论的，这并不是最佳方案，因为那样我们还得为“边走边射击”或“向左平移时射击”等等创建另一个动画。如你所见，你的项目可能很快就会产生大量动画文件。相反，让我们看看如何在 Unity iOS 中混合这些动画，并减少项目所需的 FBX 文件数量。

## 在 Unity iOS 中混合动画

继续我们的射击与奔跑示例，现在来看看如何在 Unity iOS 中混合这些动画。我们一直使用 Blender 中的 NLA 编辑器创建动画，为了只导出奔跑动画，你需要通过单击轨道的“播放设置”中的“静音”（Muted）来禁用射击轨道，如图 7.15 所示。

![](img/d3e3fa4010906e98ec76be003a6e31c2_184_0.png)

**图 7.15** 射击轨道已被静音，因此它不会包含在 FBX 导出中。

它位于奔跑循环之上，由于未分配层，所以该值为零。现在，射击动画会先于奔跑动画接收混合权重，而只有当射击动画没有占用全部 100% 的混合权重时，奔跑动画才会接收权重。当使用 animation.CrossFade("shoot") 对射击动画进行交叉淡化时，射击动画的权重将从零开始并增加到 100%。这很像在一个动画之上淡入另一个动画。随着射击动画“淡入”，奔跑动画会逐渐减弱。

然而，这并不是我特别想要做的，因为我希望射击动画在角色奔跑时播放。这正是叠加混合（additive blending）发挥作用的地方。

### 叠加混合

为了让射击动画在奔跑动画之上并与其同时播放，我们需要将 AnimationState 的混合模式设置为叠加（additive），如图 7.17 所示。

现在，当玩家按下开火按钮，或者在这个基础示例中触摸屏幕时，我只需播放射击动画，它就会叠加到奔跑动画之上，如图 7.18 所示。

在图 7.19 中，你可以看到两个动画在播放，它们通过分层和叠加混合相加在一起。图像左侧显示的是在 Unity iOS 中播放的动画，右侧显示的是在 Blender 中相加在一起的相同动画。请注意，通过 Unity 的动画系统，我们能够在 Unity iOS 中制作出与 Blender 中使用 NLA 编辑器制作的完全相同的“边跑边射击”动画。

如你所见，这是一个非常强大的工作流，因为现在可以将射击动画添加到任何其他动画（例如行走循环）上。我不再需要担心创建不同的行走和奔跑动画来包含射击，因为我可以轻松地将其叠加到我创建的任何动画之上。此外，使用这种方法，我可以轻松地为不同武器类型适配新的射击动画，因为我知道这些动画可以轻松添加到现有的行走、奔跑和横移动作上。这使得添加新动画变得简单，因为我不需要为每个新的射击动画创建一组特殊的奔跑和行走循环。想一想为游戏制作续作的情况：你可以在创建新武器动画的同时，复用第一部游戏中的一些动画。在游戏开发中，生产力至关重要；任何时候只要你能找到避免重新创建某些内容的方法，就应该采用它。

> *在游戏开发中，生产力至关重要；任何时候只要你能找到避免重新创建某些内容的方法，就应该采用它。*

```javascript
private var shoot : AnimationState;

function Start()
{
    animation.Play("run");

    //Set the Shoot Clip
    shoot = animation["shoot"];
    //Place the Shoot Clip on layer above run clip
    shoot.layer = 1;
    //Set the blend mode to additive
    shoot.blendMode = AnimationBlendMode.Additive;
    //Enable shoot
    shoot.enabled = true;

}
```

**图 7.17** 将 shoot 变量的 blendMode 设置为叠加。

```javascript
private var shoot : AnimationState;

function Start()
{
    animation.Play("run");

    //Set the Shoot Clip
    shoot = animation["shoot"];
    //Place the Shoot Clip on layer above run clip
    shoot.layer = 1;
    //Set the blend mode to additive
    shoot.blendMode = AnimationBlendMode.Additive;
    //Enable shoot
    shoot.enabled = true;

}


function Update ()
{
    for (var i:int =0; i < Input.touchCount; i++){
        //Store touch
        var touch: Touch = Input.GetTouch(i);
        //Check to see if finger moved
        if (touch.phase == TouchPhase.Began) {
            print("Touch: First Began");
            animation.Play("shoot");
        } else if (touch.phase == TouchPhase.Ended){
            print("Touch Ended");
        }
    }

}
```

**图 7.18** 这里你可以看到当用户触摸屏幕时播放射击动画的脚本。请注意，射击动画被放在第 1 层，并且 AnimationBlendMode 被设置为叠加。

![](img/d3e3fa4010906e98ec76be003a6e31c2_188_0.png)

**图 7.19** 在这张图中，你可以看到 Blender 中的分层动画已在 Unity iOS 中使用动画混合复现出来，就像之前在 Blender 的 NLA 编辑器中所做的一样。

## 在 Blender 中使用动力学为对象制作动画

在本节中，我们将了解使用 Bullet 物理引擎创建一些程序化动画的过程。在本书的演示应用中，你将扮演 Tater，跑过他的训练设施并射击目标。如图 7.20 所示，目标是一块简单的木板，上面喷绘着僵尸脸。请注意 Tater 使用喷漆罐的艺术才能！此对象的动画目标是：当它被 Thumper 的爆炸击中时，炸成碎片，如图 7.21 所示。

将物理用于此类效果可能非常合适。本章介绍的过程会将 Blender 中的物理模拟“烘焙”为关键帧，然后这些关键帧将通过 FBX 文件在 Unity iOS 中播放。然而，需要注意的是，使用这种方法可能会给 GPU 端带来较大负担。这并不一定是坏事，正如我们在本书中一直讨论的那样，你需要对游戏进行性能分析，以找出潜在的瓶颈。对于较新的硬件，iDevice 上的 CPU 正变得比 GPU 更强大，这意味着如果你的游戏已经渲染负担很重，这种方法可能不是最佳解决方案。作为本节的补充，在第 9 章中，我们将讨论在 Unity iOS 中使用物理模拟创建相同的爆炸效果，这会将该效果所需的资源转移到 CPU 上。理解这两种方法背后的过程很重要，因为每种方法都可能以不同方式影响游戏的性能。

**图 7.20** 在这里你可以看到 Lazer 将在游戏中射击的目标游戏对象。该游戏对象将在 Blender 中使用刚体动力学制作动画。

![](img/d3e3fa4010906e98ec76be003a6e31c2_189_0.png)

**图 7.21** 在 Blender 中创建的动力学模拟将被烘焙并导出到 Unity iOS，以便它可以在游戏中使用，如此处所示。

![](img/d3e3fa4010906e98ec76be003a6e31c2_189_1.png)

让我们先来看看如何在 Blender 中设置刚体动力学。

### 在 Blender 中设置刚体动力学

目标游戏对象是在 modo 中创建的。将这个对象导入 Blender 比之前通过 FBX 将 Tater 和 Thumper 模型传输到 Blender 时更棘手一些。在我们进入实际的动力学设置之前，先来看看如何将目标对象导入 Blender。

> **锁定目标……**
>
> 目标对象是在 modo 中创建的。你可以在资源网站上找到本章视频，了解目标对象是如何创建的。

