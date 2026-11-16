

其中，$k_p$ 和 $k_d$ 是比例增益和微分增益，$\theta$ 和 $\theta_{des}$ 是当前关节角度和期望关节角度，$\dot{\theta}$ 是关节的当前速度（在其连接的物体上产生角速度）。将力矩限制在合理的最大值是一个好主意，以保持稳定的仿真。以下代码片段实现了 PD 控制器所做的计算：

```
void ApplyPDControlTorques(Vec3 *Kp, Vec3 *Kd, Vec3 *des,
                           int numJoints)
{
    for(int i = 0 ; i < numJoints ; i++)
    {
        Vec3 torque;
        Vec3 vel = GetJointVelocity(i);
        Vec3 cur = GetCurrentAngleForJoint(i);
        torque[0] = Kp[i][0]*(des[0] - cur[0]) - Kd[i][0]*vel[0];
        torque[1] = Kp[i][1]*(des[1] - cur[1]) - Kd[i][1]*vel[1];
        torque[2] = Kp[i][2]*(des[2] - cur[2]) - Kd[i][2]*vel[2];
        if(torque.length() > MAX_TORQUE)
            torque = MAX_TORQUE*torque.normalize();
        ApplyTorqueAtJoint(i, torque);
    }
}
```

## 调整控制器增益

PD 控制器的行为类似于弹簧和阻尼器，比例增益和微分增益参数 $k_p$ 和 $k_d$ 控制生成的响应曲线。调整这些参数对于实现自然的运动至关重要。比例（刚度）增益控制弹簧的强度，而微分（阻尼）增益调整关节到达期望值的平滑程度。阻尼不足会导致关节超过期望值时出现振荡响应，而过度阻尼则会导致向期望值过渡过于缓慢。在中间某个位置，你将实现临界阻尼，即完美的平衡点，关节能快速到达期望值，且几乎没有或没有超调。传统上，增益值是手动调整的，这个过程可能相当耗时。如果你打算手动调整增益，一个好的经验法则是从比例增益和微分增益之间 10:1 的比例开始。

一种可以大幅减少手动调整参数数量的技术是，按每个关节所影响的身体链的有效转动惯量来缩放计算出的力矩（Zordan02）。例如，肩部会受到上臂、下臂和手的相对转动惯量的影响，如图 4.5.2 所示。使用此技术，调整参数的数量可以减少到整个身体的一个刚度和阻尼参数，因为最终增益将由每个关节所影响的身体链进行调整。按关节收集受影响的身体，并根据以下公式计算相对转动惯量：

\( H = \sum_i (m_i r_i \times v_i + I_{CM_i} \omega_i) \)

其中，$m_i$ 是物体的质量；$r_i$ 是物体相对于链的质心（CM）的相对质心，$v_i$ 是物体质心相对于链的质心的相对速度，$I_{CM_i}$ 是物体关于其质心的惯性张量，$\omega_i$ 是物体的角速度（参见 [Kwon98]）。除了此技术之外，你还可以尝试使用模拟退火或遗传算法等优化技术来学习特定行为的适当增益；参见 [Sims94]。

![](img/672fe9a2d008ba627b1991e15d70f43e_502_0.png)

**图 4.5.2** 影响肩关节运动的身体链示例。通过估计这些身体相对于肩部的相对转动惯量，可以高效地调整其控制器增益。

## 构建行为

既然你已经拥有控制模拟角色关节的底层机制，就可以开始开发特定行为了。有限状态机是管理运动控制状态之间转换的常见表示。状态之间的转换通常基于时间或事件，并可能导致针对状态目标定制的新控制器增益或期望值。例如，跌倒控制器可能有多个状态，将一只或两只手臂抛向跌倒方向，需要增益使身体保持一定的刚性，但仍能让手臂快速响应。当手臂接触地面时，会转换到一个控制器状态，该状态将吸收冲击并降低臀部和上半身的速度。图 4.5.3 演示了一个模拟向后跌倒的跌倒控制器示例。

![](img/672fe9a2d008ba627b1991e15d70f43e_503_0.png)

**图 4.5.3** 跌倒控制器示例。预测的肩部着陆位置（用球体指示）用作参考点，以计算期望的手臂位置。前向速度和朝向方向（用矢量指示）用于根据跌倒方向确定当前状态。© 2004 转载，经 Ilkka Kerenius & Rich Carlson 许可。

观察仿真的原始状态可能无法为控制器状态提供最有用的信息。实现向控制器提供信息的传感器很有帮助，例如支撑多边形、质心、身体部位接触和朝向方向。利用这些信息、个人直觉以及可能的一些生物力学知识，你可以将行为分解为基本控制状态。提前规划，以确保你的控制器能够稳健地响应游戏过程中可能出现的各种输入。保持目标可控；构建一个生成稳定跑步步态的控制器比构建一个只需确保身体最终落地的控制器要困难得多。构建模拟行为很困难，但作为游戏开发者，这是你的创造力和独创性对结果产生重大影响的地方。

## 结论

本文介绍了为现有布娃娃角色增加更有趣行为的技术。PD 控制器允许你以物理为基础的方式驱动角色的肢体。虽然计算期望的关节值和调整控制器增益可能很棘手，但所述方法可以降低手动调整参数的数量。如何创造性地使用这项技术取决于你，但随着我们发现更好的方式来模拟人类行为，可能性是无限的。

## 致谢

感谢 David Cherry、Ilkka Kerenius 和 Rich Carlson 提供部分图中出现的世界几何。

## 参考文献

- [Dorf89] Dorf, R. C. Modern Control Systems. Addison-Wesley, 1989.
- [Faloutsos01] Faloutsos, Petros, et al. “The Virtual Stuntman: Dynamic Characters with a Repertoire of Autonomous Motor Skills.” In Computer Graphics, Vol. 25, no. 6: pp. 933–953.
- [Hodgins95] Hodgins, Jessica, et al. “Animating Human Athletics.” In Computer Graphics, Vol 29, Annual Conference Series: pp. 71–78.
- [Kwon98] Kwon, Young-Hoo. “Mechanical Basis of Motion Analysis.” SIGGRAPH 2000, Computer Graphics Processing: pp. 201–208. Available online at http://kwon3d.com/theories.html.
- [Mandel04] Michael, Mandel. “Versatile and Interactive Virtual Humans: Hybrid use of Kinematic and Dynamic Motion Synthesis.” Master’s thesis, Carnegie Mellon University, available online at http://www.city-net.com/~amandel/portfolio/masters.html.
- [Shapiro03] Shapiro, Ari, et al. “Hybrid Control for Interactive Character Animation.” In Pacific Graphics 2003: pp. 455–461.
- [Sims94] Sims, Karl. “Evolving Virtual Creatures.” SIGGRAPH 1994, Computer Graphics Proceedings: pp. 15–22.
- [Smith04] Smith, Russell. “The Open Dynamics Engine.” Available online at http://ode.org/.
- [Wooten96] Wooten, Wayne, et al. “Animation of Human Diving.” Computer Graphics Forum, Vol 15, no. 1: pp. 3–14.
- [Zordan02] Zordan, Victor, et al. “Motion capture-driven simulations that hit and react.” In ACM SIGGRAPH Symposium on Computer Animation: pp. 89–96.

## 设计预定物理系统

Daniel F. Higgins
webmaster@programming.org

游戏开发无疑是一项高强度、高耐力的运动。其领先的开发者拥有经验丰富的团队，凭借令人难以置信的专注力、创新精神和强烈的热情主导各个类别。就像在玩高风险扑克游戏一样，开发者倾向于聚集在同一张无限注牌桌周围，不断将筹码推向天空。我们紧握手中的牌，寄望于新游戏的技术、“趣味性”以及粉丝的热爱来赢得这一局。因此，当竞争对手亮出赢牌时，我们目瞪口呆地看着自己的筹码转瞬之间消失，这也不足为奇。

为了增强我们的牌力，我们必须到处寻找灵感。灵感可以在 _《双塔奇兵》_ 中对圣盔谷的战斗、滑板公园里滑稽的滑板技巧，或是边境牧羊犬为黏糊糊的网球跳跃的瞬间中找到。

本文介绍了一款源于灵感的引擎。这一灵感成为设计一个系统的挑战，该系统能够产生大预算物理引擎的错觉，允许快速开发，并避免高昂的开发成本。此外，它应设计为新手和专家程序员都能使用，同时保持足够的灵活性以集成到游戏外的物理工具中。最终，该系统被创建出来，其名为 _预定物理_。

### 什么是预定物理？

在典型的一天里，与游戏开发者讨论物理时，会涉及速度、摩擦力、刚体、重力和加速度等词汇。你可能还会听到“布娃娃”这一术语。在过去，游戏物理主要作为一种载体，乏味地将物体从 A 点沿路径移动到 B 点，就像一趟痛苦乏味的旋转木马。在当今竞争激烈的游戏开发领域，儿童游乐设施已经不再够用。今天的引擎不仅沿路径移动物体，还将它们抛向空中，撞穿墙壁，并导致砖块脱落并最终堆积成动态形成的瓦砾。我们的竞争对手，配备大预算引擎，在近身格斗中面对他们可能令人生畏，在 the

