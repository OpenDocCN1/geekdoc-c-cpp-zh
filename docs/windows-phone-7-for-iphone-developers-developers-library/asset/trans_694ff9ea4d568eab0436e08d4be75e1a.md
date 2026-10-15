
几个非常重要（且通常是底层）的事件通过通知中心发布。例如，当 iPhone 旋转时，当前运行应用的默认通知中心会发布一个通知。你的应用可以直接监听该通知（不推荐），也可以让 UIKit 框架替你监听，并围绕 UI 旋转的概念提供更高层次的抽象，以处理方向变化。

如果你想在 C# 中实现类似的功能，其实非常简单。此外，一些辅助工具包和框架（例如我们将在本书后面讨论的一些 MVVM 实现）已经包含了发布和订阅全局通知的功能。

在 C# 应用程序中实现全局通知的一种超快速且简单的方法是使用公开静态事件的静态类。为此，我们将向 GameEngine 对象添加几个静态事件，用于指示游戏开始、暂停和结束的时间。任何对象，无论其生命周期或作用域如何，都可以订阅这些事件并执行响应的代码。修改后的 GameEngine 对象如代码清单 4.3 所示。

### 代码清单 4.3 GameEngine.cs（包含静态事件）

```csharp
using System;
using System.Net;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Documents;
using System.Windows.Ink;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Animation;
using System.Windows.Shapes;
using System.Diagnostics;

namespace WindowsPhoneApplication1
{
    public delegate void OnGameStartedDelegate(DateTime startTime);
    public delegate void OnGamePausedDelegate();
    public delegate void OnGameFinishedDelegate();

    public static class GameEngine
    {
        public static void Start()
        {
            if (OnGameStarted != null)
                OnGameStarted(DateTime.Now);
        }

        public static void Stop()
        {
            if (OnGameFinished != null)
                OnGameFinished();
        }

        public static void Pause()
        {
            if (OnGamePaused != null)
                OnGamePaused();
        }

        public static void Resume()
        {
            if (OnGameResumed != null)
                OnGameResumed(DateTime.Now);
        }

        public static Combatant CreateCombatant()
        {
            Combatant c = new Combatant();
            c.OnGotKilled += new DidGetKilledDelegate(c_OnGotKilled);
            c.OnHitByCombatant +=
                new DidHitTargetDelegate(c_OnHitByCombatant);
            c.OnHitCombatant +=
                new DidHitTargetDelegate(c_OnHitCombatant);

            return c;
        }

        static void c_OnHitCombatant(
            Combatant attacker, Combatant target, int hitPoints)
        {
            BroadCast(attacker.Name + " hit " + target.Name +
                " for " + hitPoints.ToString() + " hitpoints.");
        }

        static void c_OnHitByCombatant(Combatant attacker,
            Combatant target, int hitPoints)
        {
            BroadCast(target.Name + " was hit for " +
                hitPoints.ToString() + " by " + attacker.Name);
        }

        static void c_OnGotKilled(Combatant killer, Combatant target)
        {
            BroadCast(killer.Name + " killed " + target.Name +
                "! OH NOEZ!!1ONE");
        }

        static void BroadCast(string msg)
        {
            // ordinarily there would be network code here
            // to broadcast to the entire game

            Debug.WriteLine("[Game]: " + msg);
        }

        public static event OnGameStartedDelegate OnGameStarted;
        public static event OnGameFinishedDelegate OnGameFinished;
        public static event OnGamePausedDelegate OnGamePaused;
        public static event Action<DateTime> OnGameResumed;
    }
}
```

此时，代码清单 4.3 中的代码看起来应该相当直观。游戏引擎上新增了一些方法，用于触发各种事件，如 Start、Stop、Pause 和 Resume。在清单末尾，你可以看到我声明的四个新事件。

如果你仔细看，会注意到我声明 OnGameResumed 事件的方式有些不同。我没有像之前的代码清单那样使用在命名空间顶部声明的强类型委托，而是利用了 C# 中的一些简写特性，例如泛型和称为 `Action<T>` 的泛型类型。

泛型允许类由创建实例的代码与特定类型关联，而不是由类本身关联。例如，我不使用 List 类的实例来创建可为任意类型的对象列表，而是通过创建 `List<Combatant>` 实例来创建战斗者列表。泛型允许我在实例化类时向类提供一个或多个类型参数。如果你想了解更多关于泛型以及 C# 语言本身的其他底层细节，不妨阅读 Bart De Smet 所著的《C# 4.0 Unleashed》。

最后这个事件声明的第二个改动是使用了 `Action<DateTime>`。`Action<T>` 类是一个泛型类，为具有 void 返回类型的委托提供了一种简写方式。如你所见，在事件声明前写一次 `Action<DateTime>`，比创建自定义委托类型然后使用它来声明事件要易读得多。每当你看到 `Action<T>`，你都可以在脑海中将它理解为“一个接受类型为 T 的参数并返回 void 的委托”。此外，Action 还有接受多个参数的变体，以适应事件处理程序中更多的参数。

## 警惕静态类和属性

尽管我向你展示了使用静态类和事件属性是在应用程序中提供全局事件通知系统的一种方式，但你对这个建议必须持保留态度。

C# 应用程序使用垃圾回收机制。这意味着有一个后台进程会随着你制造垃圾而清理它们，释放分配给孤立或不再处于作用域内的对象的内存。静态类及其公开的属性永远不会离开作用域。这意味着它们永远不会成为孤立对象，分配给它们的内存也永远不会被回收。

简而言之，如果可以为任何目的（事件或其他）避免使用静态类和属性，那就尽量避免。在为类创建一堆用于全局通知的静态事件之前，请确保这样做是必要的。如果你可以使用局部作用域的事件处理，那就改用局部方式；这样内存占用会更小，垃圾回收周期也会更快。

## 小结

在本章中，你从 iOS 和 Windows Phone 7 两个角度简要了解了事件驱动编程。

在 iOS（以及 Mac 上的 Cocoa）开发中，委托模式被广泛使用，允许对象通过称为协议的已知且约定的契约相互通信。委托模式用于各种场景，从响应用户事件调用方法到向不同类型的控件提供数据，开发者在构建自己的自定义框架时也可以使用它。委托模式的典型特征是被动性：不是将数据和功能推送给控件，而是控件在需要时被动地请求数据和功能。即使你在 WP7 开发中从不使用这种模式，你也应该了解并尊重它，因为它支持了众多开发特性，使 iPhone 编程如此引人注目且强大。

随后，本章从讨论委托模式转向讨论 C# 中如何处理事件。你了解了如何公开事件属性、如何发布事件以及如何订阅这些事件。最后，你看到了如何利用静态类和事件属性来公开全局事件。

凭借你在上一章学到的面向对象编程知识，加上本章的事件编程知识，你应该已经准备好开始编写你的第一个 WP7 应用程序了。

## 渲染与视图系统基础

> 绘画是供人观看而非感受的诗，而诗歌是供人感受而非观看的画。
>
> 列奥纳多·达·芬奇

本章概述了 iOS 和 Windows Phone 7 平台上底层控件渲染系统的工作方式。本章不是关于控件本身（本书后面会有大量章节介绍控件）。相反，本章回顾了 UIKit 视图系统，包括对坐标系、点与像素等内容的简要讨论。

接下来，本章从底层视角向你介绍 Silverlight。你将看到 Silverlight 如何组合声明性 UI 元素，然后将它们渲染到屏幕上，并允许用户与这些控件交互。

拥有这种视图渲染系统内部机制的底层知识现在可能看起来并不那么有用，但当你真正开始撸起袖子编写一些严肃的 WP7 应用程序和控件时，你会庆幸自己对这些幕后机制及其与典型 iOS 应用程序运行方式的关系有基本的了解。

如果你做过任何 iPhone 编程，你就会知道用户看到的一切都是分层处理的。可以把它想象成一叠牌。牌堆的最底部是桌面。这就是 UIWindow。虽然从技术上讲你可以拥有多个 UIWindow，但在任何给定时间，只有一个窗口会显示给用户。
