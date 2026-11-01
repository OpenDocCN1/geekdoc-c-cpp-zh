

```csharp
{
    int randomIncrement = UnityEngine.Random.Range(1, 5);
    score = score + randomIncrement;
    print(score);
    GameObject.Find("scoreText").GetComponent<Text>().text = "Score: " + score;
    Destroy(collision.collider.gameObject);
}
if (objectTag == "red_monster")
{
    int randomDecrement = UnityEngine.Random.Range(1, 10);
    score = score - randomDecrement;
    print(score);
    GameObject.Find("scoreText").GetComponent<Text>().text = "Score: " + score;
    Destroy(collision.collider.gameObject);
}
if (objectTag == "ground")
{
    SceneManager.LoadScene(SceneManager.GetActiveScene().name);
}
if (objectTag == "finish")
{
    GetComponent<Rigidbody2D>().gravityScale = 0.0f;
    GameObject.Find("levelCompleteText").GetComponent<Text>().text = "Level Complete!";
    StartCoroutine(restartLevel());
}
public IEnumerator restartLevel()
{
    yield return new WaitForSeconds(5f);
    SceneManager.LoadScene(SceneManager.GetActiveScene().name);
}
```

代码 16.14（续）

现在，我们可以在 Unity 中点击 Play 按钮来运行完成的游戏。虽然目前这个游戏还很简单，但我们可以运用本章学到的概念，为游戏添加新的关卡，从而获得更好的游戏体验。

## 16.5. 将游戏导出为独立程序

我们已经开发出了随机平台游戏，并且可以在 Unity 中运行它。不过，我们还需要能够将游戏作为可执行文件进行分发，这样任何玩家都可以运行它。在 Unity 中导出游戏非常简单。为此，请点击 File → Build Settings：

![](img/41d82527c4e41cdb7e56259564306ddc_435_0.png)

图 16.86。启动“Build Settings”对话框

在对话框中，将平台选择为 PC, Mac, Linux Standalone，并将目标平台设置为 Windows。然后，点击 Build 按钮：

![](img/41d82527c4e41cdb7e56259564306ddc_435_1.png)

图 16.87。构建设置

## 第 16 章：使用 C# 在 Unity 中开发 2D 游戏

点击 Build 按钮后，Unity 会显示文件保存对话框。在该对话框中，指定要将可执行游戏保存到计算机上的位置，并为文件命名。我将游戏保存为桌面上的 Random Platformer.exe。双击游戏可执行文件后，会显示一个对话框，我们可以在其中调整图形和输入设置：

![](img/41d82527c4e41cdb7e56259564306ddc_436_0.png)

图 16.88。配置设置

我在 Windows 模式下设置了 800x600 的分辨率：

![](img/41d82527c4e41cdb7e56259564306ddc_436_1.png)

图 16.89。图形设置

点击 Play! 按钮后，很快就会出现“Made with Unity”动画，随后游戏将开始运行：

![](img/41d82527c4e41cdb7e56259564306ddc_437_0.png)

图 16.90。独立游戏

现在是时候运行游戏，看看我们能否获得尽可能高的分数了，最高分为 15 分（你能看出为什么最高分是 15 分吗？）。

本章中，我们学习了使用 C# 编程在 Unity 中进行游戏开发的基础知识。我们可以添加新的关卡并扩展随机平台游戏，使其成为一个完整的游戏；也可以利用当前掌握的 Unity 和 C# 知识开发类似的 2D 游戏。请记住，在编程世界中，我们唯一受到的限制就是自己的想象力！

## 后记

感谢你使用我的书开启 C# 编程之旅！我真心希望你喜欢本书，并在使用 C# 开发程序方面获得了一些信心。如果你想分享意见和建议，欢迎随时发送电子邮件至 syamacli@gmail.com；或者，你也可以在本书网站 www.yamaclis.com/csharp 的评论区公开发表。

本书旨在成为一本初学者指南。如果你认真学习了本书的全部内容，那么你应该已经准备好进一步学习 C# 应用程序开发，而这方面的首要资料来源当然是互联网。我推荐以下网站来学习高级主题：

- https://www.tutorialspoint.com/csharp/
- http://www.completecsharptutorial.com/
- http://www.c-sharpcorner.com/beginners/

我想用下面这些引语结束本书，我认为它们蕴含着深刻的含义：

> “信息是不确定性的消解。”
>
> 克劳德·香农

> “时间就是一切；五分钟之差可能决定胜负。”
>
> 霍雷肖·纳尔逊

> “我的原则始终是：当天的事情当天完成。”
>
> 威灵顿第一公爵

下一页将列出参考资料和密码

## 参考资料

- 1. https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/
- 2. https://msdn.microsoft.com/en-us/library/aa288463(v=vs.71).aspx
- 3. http://www.tiobe.com/tiobe-index/
- 4. https://www.tutorialspoint.com/csharp/
- 5. Rod Stephens，《C# 24 小时培训教程》，Wrox，2015 年。
- 6. Benjamin Perkins、Jacob Vibe Hammer 和 Jon D. Reid，《Beginning C# 6 Programming with Visual Studio 2015》，Wrox，2016 年。
- 7. Joseph Albahari 和 Ben Albahari，《C# 6.0 Pocket Reference: Instant Help for C# 6.0 Programmers》，O’Reilly Media，2015 年。

你可能会对我在“Yamacli 初学者指南系列”中的其他编程书籍感兴趣：

- 1. S. Yamacli，《使用 Swift 3 开发 iOS 10 应用程序初学者指南：Xcode、Swift 与应用程序设计基础》，ISBN-13：978-1540452153，2017 年。
- 2. S. Yamacli，《Android 应用程序开发初学者指南：面向初学者的实用方法》，ISBN-13：978-1548088163，2017 年。

**可从本书网站** www.yamaclis.com/csharp **下载的压缩项目文件和图片的密码是：**27A56。

