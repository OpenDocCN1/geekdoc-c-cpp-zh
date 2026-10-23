
```scala
private class BallBallColl(val time: Double, val b1: Int, val b2: Int) extends CollEvent {
    def handle {
        val ball1 = workCopy(b1).advanceTo(time)
        val ball2 = workCopy(b2).advanceTo(time)
        val m1 = ball1.size * ball1.size * ball1.size
        val m2 = ball2.size * ball2.size * ball2.size
        val cmvx = (ball1.vx * m1 + ball2.vx * m2) / (m1 + m2)
        val cmvy = (ball1.vy * m1 + ball2.vy * m2) / (m1 + m2)
        val dx = ball1.x - ball2.x
        val dy = ball1.y - ball2.y
        val dist = math.sqrt(dx * dx + dy * dy)
        if (dist > 1.01 * (ball1.size + ball2.size)) {
            println("Warning: collision with big separation. " + b1 + " " + b2 + " " + dist)
        }
        if (dist < 0.99 * (ball1.size + ball2.size)) {
            println("Warning: collision with little separation. " + b1 + " " + b2 + " " + dist)
        }
        val vx1 = ball1.vx - cmvx
        val vy1 = ball1.vy - cmvy
        val nx = dx / dist
        val ny = dy / dist
        val mag = nx * vx1 + ny * vy1
        workCopy(b1) = ball1.copy(vx = ball1.vx - 1.9 * mag * nx, vy = ball1.vy - 1.9 * mag * ny)
        workCopy(b2) = ball2.copy(vx = ball2.vx + 1.9 * mag * nx * m1 / m2, vy = ball2.vy + 1.9 * mag * ny * m1 / m2)
        pq.removeMatches {
            case bbc: BallBallColl => bbc.b1 == b1 || bbc.b2 == b1 || bbc.b1 == b2 || bbc.b2 == b2
            case bwc: BallWallColl => bwc.b == b1 || bwc.b == b2
            case _ => false
        }
        val others = workCopy.indices.filter(b => b != b1 && b != b2)
        findEventsFor(b1, others, time)
        findEventsFor(b2, others, time)
    }
}

private class BallWallColl(val time: Double, val b: Int, val newDir: (Double, Double, Double, Double) => (Double, Double)) extends CollEvent {
    def handle {
        val ball = workCopy(b)
        val nx = ball.x + (time - ball.time) * ball.vx
        val ny = ball.y + (time - ball.time) * ball.vy
        val (nxv, nyv) = newDir(ball.x, ball.y, ball.vx, ball.vy)
        workCopy(b) = DrawBouncingBalls.Ball(nx, ny, nxv, nyv, ball.size, time)
        pq.removeMatches {
            case bbc: BallBallColl => bbc.b1 == b || bbc.b2 == b
            case bwc: BallWallColl => bwc.b == b
            case _ => false
        }
        findEventsFor(b, workCopy.indices.filter(_ != b), time)
    }
}

object DrawBouncingBalls {
    def apply(p: DrawTransform, data: xml.Node) = {
        new DrawBouncingBalls(p, Vector((data \ "ball").map(bxml => {
            val x = (bxml \ "@x").text.toDouble
            val y = (bxml \ "@y").text.toDouble
            val vx = (bxml \ "@vx").text.toDouble
            val vy = (bxml \ "@vy").text.toDouble
            val size = (bxml \ "@size").text.toDouble
            Ball(x, y, vx, vy, size, 0.0)
        })): _*)
    }

    def apply(p: DrawTransform, minSize: Double = 0.01, maxSize: Double = 0.05) = {
        new DrawBouncingBalls(p, Vector.fill(20) {
            val size = minSize + math.random * (maxSize - minSize)
            Ball(size + math.random * (1 - 2 * size), size + math.random * (1 - 2 * size),
                (math.random - 0.5) * 0.02, (math.random - 0.5) * 0.02, size, 0.0)
        })
    }

    case class Ball(x: Double, y: Double, vx: Double, vy: Double, size: Double, time: Double) {
        def toXML = <ball x={x.toString} y={y.toString}
            vx={vx.toString} vy={vy.toString} size={size.toString}/>

        def advanceTo(t: Double) = {
            val dt = t - time
            copy(x = x + vx * dt, y = y + vy * dt, time = t)
        }
    }

    private val wallInfo = Seq[(Ball => Double, (Double, Double, Double, Double) => (Double, Double))](
        (b => if (b.vx < 0) b.time - (b.x - b.size) / b.vx else -1, (x, y, vx, vy) => (vx.abs, vy)),
        (b => if (b.vx > 0) b.time + (1 - b.x - b.size) / b.vx else -1, (x, y, vx, vy) => (-vx.abs, vy)),
        (b => if (b.vy < 0) b.time - (b.y - b.size) / b.vy else -1, (x, y, vx, vy) => (vx, vy.abs)),
        (b => if (b.vy > 0) b.time + (1 - b.y - b.size) / b.vy else -1, (x, y, vx, vy) => (vx, -vy.abs))
    )
}
```

最显著的变更体现在顶部：新增了两个类级变量，并修改了定时器中的代码。新的类级变量是一个数组，用于在处理过程中镜像向量；以及一个优先队列，其元素类型为 CollEvent，CollEvent 是稍后在代码中声明的特质。

定时器代码会检查这两个变量是否为空，如果是则创建它们。这是出于序列化的需要而必须做的。逻辑上的主要变化发生在定时器的 action 中。workCopy 变量被初始化为应用了重力后的球的副本。然后，对于每个球，找出在下一个时间单位内相对于数组中位于它之后的所有球可能发生的所有事件。只检查列表中位于该球之后的粒子，可以避免我们重复发现碰撞。然后，只要优先队列非空，我们就取出下一个事件并处理它。接着，将球复制到一个用于绘图的 Vector 中。绘图、生成属性和生成 XML 的代码保持不变。

在 toXML 方法之后，主类中新增了许多方法和类。其中第一个方法接受两个 Ball 对象，并返回两者之间的碰撞时间。该方法假设球沿直线运动，因此两球之间距离的平方是关于时间的二次函数。我们只需解出它们之间的距离等于两球半径之和的时刻。每个粒子在一步中会记录它所处的“时间”，因此计算时必须考虑这一点。如果没有碰撞，该方法返回 -1.0。否则，它返回较小的根，因为那是粒子相撞的时刻。另一个根则是粒子如果相互穿过时彼此分离的时刻。下面是求二次方程系数的数学推导。

d²(t) = ((x₁ + vx₁ * t) − (x₂ + vx₂ * t))² + ((y₁ + vy₁ * t) − (y₂ + vy₂ * t))²
= (Δx + Δvx * t)² + (Δy + Δvy * t)²
= Δx² + Δy² + 2(ΔxΔvx + ΔyΔvy)t + (Δvx² + Δvy²)t²

当粒子运动比直线更复杂时，求碰撞时间就需要更复杂的代码，因为通常情况下不存在像本例这样有闭式解的情况。

在求碰撞时间的方法之后，还有一个方法，用于查找某个特定粒子在当前时间之后，与某些其他粒子以及墙壁之间发生的所有事件。由于代码的组织方式，处理粒子和墙壁的结构非常相似。我们遍历希望检查的对象，计算事件时间；如果该事件时间落在当前步骤的有效范围内，就将其加入队列。稍后我们会说明墙壁代码是如何按这种方式工作的。

该模拟包含两种碰撞类型，它们都是 CollEvent 特质的子类型，即 BallBallColl 和 BallWallColl。每个类型都知道事件发生的时间，并包含处理事件的代码。墙壁类比较简单，或许值得看一下，弄清它的工作原理。首先，求出球在事件发生时的位置。然后，调用一个在事件构造时传入的函数，该函数接收球的位置和速度，并返回一个新的速度。用新的速度和位置构建一个新的球对象，并将其存储在数组中，替换原来的对象。然后，删除涉及该球的未来事件，并查找新的事件。

球与球碰撞的代码做的事情相同，但涉及两个球，处理这种碰撞需要更多数学计算。除非你想了解，否则理解这些数学并不重要。它首先计算两个球的相对质量，然后求出两个球的质心速度。² 这段代码会将距离与半径之和进行比较，如果距离与期望值不够接近，就打印一条错误信息。这段代码对于确保一切正常运转非常有帮助；虽然最终代码在技术上并不需要它，但保留它可以防止将来修改时出现问题。每个粒子的速度变化量是按速度在分离两粒子的连线方向上的投影的倍数计算的。这段代码中使用了常量 1.9，以便产生一些能量损失。完美的碰撞会使用 2.0。遗憾的是，这段代码的重力积分并不守恒能量，因此让碰撞对系统稍作阻尼会很有帮助。³

² 在质心参考系中计算碰撞要容易得多。在这个运动的参考系中，每个球都像是撞上了一堵静止的墙。

³ 这段代码在步长开始时对每个粒子施加一个完整的向下加速度。如果粒子在步长中途垂直方向反向，重力的影响也应当是反向的。但这里并没有这样做，因此粒子每次从底部反弹时都可能获得能量。
