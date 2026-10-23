
```
contents = swing.Button("Click Me")(Thread.sleep(10000))
}
frame.visible = true
readLine
```

If you click the button, it blocks the event thread from doing anything else for ten seconds. If you run this program you can click the button and see the effects. One effect is that the button will “stay down”. More interesting is seeing what happens if you try to close or resize the window. The close will not take effect until the end of the ten seconds. The window will not repaint itself during that time either.

To see this same effect on a larger scale, add the following line into the commands map in the Commands object in the project code.

```
"freeze" -> ((rest,d) => Thread.sleep(rest.trim.toInt*1000))
```

Now you can run the drawing program, add a drawing, and enter the command “freeze 10”. After doing this, nothing you do in the GUI will take effect for ten seconds. This command will be useful in the next section as well to see how blocking the event thread impacts other things that happen in the GUI.

Much of this chapter has focused on the challenges associated with using threads. Those challenges remain for the threads associated with a GUI. As you just saw, keeping the event thread busy too long can lead to an unresponsive GUI. It is also risky to have other threads altering mutable data that is used by the event thread as that can lead to race conditions. This combination makes things a bit tricky because you need to have any significant workload happen in a separate thread, but you should not have that other thread mutate values that are used for painting or event handling. Instead, you should have the other thread notify the GUI using events. This is what happens with calls to repaint. Instead of doing the paint in the thread that makes the call, it fires off an event that tells the GUI to do a paint.

All of the different GUI components are Publishers so they have a method called publish that takes an event. To see how we can use this, we can make the command processing in Drawing so that it does the work in a separate thread and notified the GUI using an event. Consider the following alteration to the commandField declaration in Drawing.

```
val commandField = new TextField() {
  listenTo(this)
  reactions += {
    case e:EditDone =>
      if(!text.isEmpty) {
        val t = text
        Actor.actor {
          publish(new ResultEvent(t,Commands(t,Drawing.this)))
        }
        text=""
      }
    case e:ResultEvent =>
      commandArea append "> "+e.text+"\n"+e.result+"\n"
  }
}
```

This code uses Actor.actor to start the command executing in a separate thread. When the command is finished, the result is bundled into a ResultEvent along with the text that was executed and that is published. The commandArea is updated when the ResultEvent

is received. To make this work, the following declaration of ResultEvent was added above the propertiesPanel method.

```
private class ResultEvent(val text:String,val result:Any) extends Event
```

The use of publish and having the change to commandArea happen in the event thread means that we can not have the thread created by actor put the GUI in an inconsistent state at a significant time, such as a redraw.

To really see the impact of this code you need to run DrawingMain and add a drawing, then try using the “freeze” command again. What you will find is that the GUI no longer freezes up. If you do “freeze 10” you can keep using the GUI and nothing will happen for ten seconds. At the end of the ten seconds, the output area will show the proper feedback to indicate that the command completed. You can even type in other commands while a freeze command is working. If the other commands finish before the end of the freeze time, their feedback in the output panel will come before that of freeze.

The other place where threading is significant for GUIs is during animation. The easiest, safe approach to doing animation in a GUI was introduced in chapter 12 where we created a javax.swing.Timer and gave it an ActionListener. The ActionListener is a type from the Java event handling libraries so this code will run the timed code in the GUI event thread and not cause any threading problems. We will use this approach again in the following section.

## 21.8 Animated Bouncing Balls (Project Integration)

To illustrate the use of a javax.swing.Timer in the drawing program we will make a new Drawable that shows balls bouncing around inside of a little box. While it is not really needed at this point, we will also make the code that moves the balls around execute in parallel using parallel collection functionality. Here is the code for this new class.

```
package scalabook.drawing
```

```
import java.awt.{Graphics2D,Color}
import java.awt.geom._
import swing._
import event._
```

```
class DrawBouncingBalls(p:DrawTransform,drawing:Drawing) extends DrawLeaf {
  val parent = p
  private var propPanel:Component = null
  private var (minSize, maxSize) = (0.01, 0.05)
  private var balls = Vector.fill(20){
    val size = minSize+math.random*(maxSize-minSize)
    new Ball(size+math.random*(1-2*size),size+math.random*(1-2*size),
      (math.random-0.5)*0.02,(math.random-0.5)*0.02,size)
  }
}
```

```
private case class Ball(x:Double,y:Double,vx:Double,vy:Double,size:Double)
```

```
private val timer = new javax.swing.Timer(100,Swing.ActionListener(e => {
  balls = (for(Ball(x,y,vx,vy,s) <- balls par) yield {
```

for running a piece of code. There are some useful methods in **Executors** that will provide **ExecutorService** objects which behave in generally useful ways. Many of these allow for the reuse of threads as there is significant overhead in creating **Thread** objects.

- The **Callable** type allows you to run a task on an **ExecutorService** that gives you back a value. When such a task is submitted, you are given a **Future** object that will provide the result.
- The concurrency library includes a number of parallel data structures as well.
  * The **CyclicBarrier** and **CountDownLatch** classes make it easy to have multiple threads pause at a point in the code until all threads have gotten there.
  * An **Exchanger** can be used to pass a value between threads at some particular point.
  * The **BlockingQueue** is a data structure that lets one group of threads exchange objects with another group of threads and blocks in situations when there is not space to put something or nothing is available.
  * A **Semaphore** provides a way to control how many threads are working in a particular part of the code at any given time.
- The *java.util.concurrent.atomic* package provides classes for basic types that have operations which can not be interrupted. These often provide a simpler and more efficient approach to preventing race conditions than synchronization.
- The *java.util.concurrent.locks* package defines locks that can be used for synchronization type behaviors that can span beyond a single method call or code block.

- Scala makes certain types of parallelism simple with parallel collections. These collections have methods that automatically split the work across multiple threads. Calling **par** on a regular collection gives you a parallel version. Calling **seq** on the parallel version gives you back a sequential one.
- There is another parallel library in Scala for Actor-based parallelism. For our current purposes, it provides easy, Scala-style methods for creating threads using **Actor.actor** and **Futures.future**.

## 21.9.2 Exercises

- 1. In the discussion of the parallel factorial and Amdahl's law we concluded that the primary limitation in the code we had written for scaling was the final product. Using techniques from *java.util.concurrent*, write code to make that operation happen in parallel.

- 2. A good way to make sure you understand parallelism is to work on implementing a number of different simple problems using each of the different techniques that were presented in this chapter. The problems you should solve are listed below. For each of them, try to write a solution using the following methods.
  * Normal *java.lang.Threads* or calls to **Actor.actor** with **synchronized** and **wait/notifyAll**.
  * Elements from *java.util.concurrent* such as **ExecutorServices**, thread-safe data structures, and atomic values.
