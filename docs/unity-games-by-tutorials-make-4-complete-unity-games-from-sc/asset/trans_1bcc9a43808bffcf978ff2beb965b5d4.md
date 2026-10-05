
```cs
public AudioClip hurt;
public AudioClip alienDeath;
public AudioClip marineDeath;
public AudioClip victory;
public AudioClip elevatorArrived;
public AudioClip powerupPickup;
public AudioClip powerupAppear;
```

这些变量代表了游戏中每个音效片段。你已将它们全部设置为 `public`，以便在 Unity 编辑器中为它们设置片段。

**保存**并返回 Unity。在层级面板（Hierarchy）中选择 **SoundManager**，打开 **Sounds** 文件夹，并将以下声音分配给 SoundManager：

- 射击：**bw_shoot**
- 升级后射击：**bw_triple_shot**
- 受伤：**bw_marine_death**
- 外星人死亡：**bw_alien_death**
- 陆陆死亡：**bw_marine_death**
- 胜利：**bw_victory**
- 电梯到达：**bw_elevator**
- 强化拾取：**bw_powerup_pickup**
- 强化出现：**bw_powerup_appear**

该组件看起来如下：

| SoundManager | |
|---|---|
| 射击 | bw_shoot |
| 升级后射击 | bw_triple_shot |
| 受伤 | bw_marine_death |
| 外星人死亡 | bw_alien_death |
| 陆陆死亡 | bw_marine_death |
| 胜利 | bw_victory |
| 电梯到达 | bw_elevator |
| 强化拾取 | bw_powerup_pickup |
| 强化出现 | bw_powerup_appear |

干得好！你已经将音效库很好地组织在了一个地方，并准备好将其余音频集成到游戏中。

## 播放声音

在层级面板（Hierarchy）中，展开 SpaceMarine 并选择 BobbleMarine-Body。在检器（Inspector）中，点击添加组件（Add Component）按钮，并在 Audio 中选择 Audio Source。

接下来，双击 Gun 脚本进行编辑，并添加以下实例变量：

```cs
private AudioSource audioSource;
```

在 Start() 中添加以下内容：

```cs
audioSource = GetComponent<AudioSource>();
```

这只是获取了已挂载 AudioSource 的引用——你稍后会用到它。在 fireBullet() 中，在结束大括号之前添加以下 PlayOneShot：

```cs
audioSource.PlayOneShot(SoundManager.Instance.gunFire);
```

这段代码播放了射击声。

注意，在 Unity 中通过代码播放音效有两种方法：

- PlayOneShot()，正如你在这里使用的，它允许同一个声音同时播放多次，产生重叠效果。例如，陆战队员可以发射一颗子弹，在该音效仍在播放时，陆战队员可以快速发射另一颗子弹，你会同时听到两个音效。陆战队员射击速度快，这正是我们在这里需要的。
- Play() 只允许音效同时播放一次。如果你播放了一个音效，然后再次调用 Play()，它将重新开始声音，导致第一个效果听起来被切断了。Play() 相比 PlayOneShot() 的优势在于 Play() 可以途中停止，而 PlayOneShot() 则不能。

保存文件并返回 Unity。运行游戏并射击，来听听射击声。

听起来棒极了，但有点遗憾的是，当你炸飞外星人时并听不到它们死亡的声音。因此，你将在下一个阶段添加死亡声音。

注意，你不能让外星人像你处理子弹那样播放自己的声音，因为当外星人死亡时，你会销毁 Alien GameObject。当你销毁 GameObject 时，任何在 AudioSource 上播放的声音都会立即停止。

因此，你将让 GameManager 来播放死亡声音。虽然使用 SoundManager 处理所有声音很有吸引力，但这样做会缩小你的选择。当你深入研究混音器（mixer）时，你会学到更多。

在代码编辑器中打开 SoundManager 脚本，添加以下方法：

```cs
public void PlayOneShot(AudioClip clip)
{
    soundEffectAudio.PlayOneShot(clip);
}
```

这是对 PlayOneShot() 的简单封装。

保存并关闭 SoundManager 脚本，然后打开 Alien 脚本。在 OnTriggerEnter() 中，在结束大括号之前添加以下内容：

```cs
SoundManager.Instance.PlayOneShot(SoundManager.Instance.alienDeath);
```

保存脚本并返回 Unity。运行游戏并消灭所有外星人。

## 添加强化

你为陆战队员制造了相当困难的环境。在第 4 章“物理”中，你加入了大量的外星人。在第 5 章“寻路”中，你教了外星人如何追捕陆战队员，它们正血脉疯狂。

最糟糕的是，你一直让他们在没有音乐的情况下工作。谁会这样做？这太残忍了！

现在是给我们的英雄加加油的好时机——某种能平衡局面的东西。你将创建一个听起来很酷且能临时将射速提高三倍强化。

首先，你需要创建一个三发枪。打开 Gun 脚本，在实例变量下方添加以下内容：

```cs
public bool isUpgraded;
public float upgradeTime = 10.0f;
private float currentTime;
```

- isUpgraded 是一个标记，让脚本知道是发射一颗子弹还是三颗。
- upgradeTime 是升级持续的时间（秒）。
- currentTime 跟踪自枪支升级以来已经过去了多久。

（注：原文中存在大量重复的变量说明，已根据文档工程师要求去重并保留核心逻辑）

