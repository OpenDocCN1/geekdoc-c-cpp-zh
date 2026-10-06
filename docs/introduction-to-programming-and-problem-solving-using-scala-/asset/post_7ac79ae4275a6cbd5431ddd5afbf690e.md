
# Recursion

```scala
def moveDisk(from:Int,to:Int):Unit = {
    require(pegs(to).isEmpty || pegs(from).head == pegs(to).head)
    pegs(to) = pegs(from).head :: pegs(to)
    pegs(from) = pegs(from).tail
}
```

```scala
def moveDisks(n:Int,from:Int,to:Int):Unit = {
    if (n>1) {
        moveDisk(from, to)
    } else {
        val other = 3-from-to
        moveDisks(n-1, other)
        moveDisk(from, to)
        moveDisks(n-1, other, to)
    }
}
```

```scala
moveNDisks(pegs(0).size)
```

The function moveNDisks is recursive and relies on the moveDisk function so we can feel the program is not complex. The line `val other = 3-from-to` might seem a bit odd at first. The function is only passed the pegs number to move or but we have to refer to the third peg in the function as that is where the top n-1 pegs are to go. That line calculates the number of the other peg using the observation that if you add the indexes of all the pegs you get. The script ends with a call to the moveNDisks function followed by a proof of what is left at the end. This makes it simple to verify that the puzzle was accurately solved.

Given the physical and visual nature of the Towers of Hanoi, the print is a bit unsatisfactory. This is a problem that really deserves to have a graphic display. The following script plots the earlier code inside of a ScalFX app and uses Rectangles of Int so that you can see the disks move as the recursion solves puzzle.

# Listing 15.2: hanoi.scala

```scala
import scalafx.Imports._
import scalafx.application._
import scalafx.event.ActionEvent
import scalafx.scene.Scene
import scalafx.scene.control.Button
import scalafx.scene.paint._
import scalafx.scene.shape._
import scala.concurrent.Future
import scala.concurrent.ExecutionContext.Implicits.global
```

```scala
val app = new JFXApp {
    stage = new PrimaryStage {
        title = "Towers of Hanoi"
        scene = new Scene(600,300)
            def moveDisk(peg:Int, h:Int, size:Int):Rectangle = {
                val s = size*10
                val r = Rectangle(100+peg*200-s/2, height.value-h*30, s, 20)
                r.fill = Color.Red
            }
    }
}
```

# 464 Introduction to Programming and Problem-Solving Using Scala

```scala
r.stroke = Color.Black
content += r
{}
```

```scala
val num = if (args.length>0) args(0).toInt else 7
val pegs = Array(List.tabulate(num)(i => makeDisk(0, num-i, i+2)),
List[Rectangle](), List[Rectangle]())

def moveDisk(to:Int,from:Int) {
  require(pegs(to).isEmpty || pegs(from).head.width <
  pegs(to).head.width)
  pegs(to) = pegs(from).head :: pegs(to)
  pegs(from) = pegs(from).tail
  Platform.runLater {
    val p = pegs(to).head
    p.x = 100+200-p.width.value/2
    p.y = height.value-pegs(to).length+30
  }
}
Thread.sleep(100)
```

```scala
def moveDisks(n:Int,from:Int,to:Int) {
  val other = 3-from-to
  if (n==1) {
    moveDisk(from, to)
  } else {
    moveNDisks(n-1, from, other)
    moveDisk(from, to)
    moveNDks(n-1, other, to)
  }
}
```

```scala
val button = new Button("Start")
content += button
button.onClick = (e:ActionEvent) => Future {
  moveNDisks(pegs(0).size, 0, 2)
}
```

main so that you can watch the animation, it is a Button, that when clicked makes a call to moveNDisks. This happens in a Future so Inside the moveNDisks function, code was added that changes the location of the disk that was moved, and pauses the world for a short period so that you can see it. Now the rectangles simply disappear from their old position and appear in the new one. It is left as an exercise for the student to use Transitions to animate this process.

If you play with this code you will notice that many stacks of disks take a very long time to move. This leads to the question of how many disks does it take to get N disks from one peg to another? The recursive code makes this question fairly easily to answer

# Recursion

we are happy with a recursive function for the answer.

```
f(N) = if N=1 1 else 1 + 2 * f(N-1)
```

This can be simplified to f(N) = 2^N - 1. The number of moves grows exponentially in the number of disks. Disks of 20 or 30 disks would take a very long time to complete.

# 15.5 Permutations

This next example is a bit more practical. We are given a List of values, and we want to perform some function on all permutations of this List. A permutation of a collection contains all the same elements, but the elements are in a different order. This type of behavior might be desired if you have different tasks and you need to find an optimal order in which to perform the tasks based on some rule.

So the next question, how could we do this? We have previously seen that sequences in Scala have a method called permutations which will do for us, but we want to see how we could do it ourselves. To figure this out, we will employ a common idiom we use with our simpler recursive functions. The idea is that we talk about a large problem and break it down so that we solve one step and then apply the same function to what is left. In this case, one step is picking a first element. Unlike what we did in chapter 5, there will be more than one option for each. Any of the elements in the current List will be the first element in the permutation. What follows first element is the permutations of everything else in the List. That after that returns, we go back to first element and make a recursive call on the rest. Then we pick a different element and recurse-curse. This should be repeated for all the elements in the List.

To convert this into a function we need to figure out what information has to be passed in. The other part is that we have to pass in the List of values built so far. This can be done as a second List. If we made the function such that it returns a List of Lists with all the permutations, these would be the only arguments we would need. However, such a function is not useful for many situations because the number of permutations grows very quickly with length and the cost in memory would become prohibitive. Instead, we need a function that operates on a List that we call each time to complete a permutation is built. The caller can decide what is done with the different permutations.

So we are writing a function that takes three arguments, the List of numbers we want to permit, a function to apply to any finished permutations, and the current List for this permutation.¹ This is done in the following code:

```scala
def permute(nums:List[Int],f:(List[Int])=>Unit,p:List[Int]):Unit = {
  if (nums.isEmpty)
    f(p)
  else {
    var before=List[Int]()
    var after=nums
```

> This last argument is something of an implementation detail that we could hide using a nested function if we do not. We do here to keep things a bit simpler.

# Introduction to Programming and Problem-Solving Using Scala

```scala
while (!after.isEmpty) {
  val perm = after.head :: p
  permute(before :: after.tail,f,perm)
  before = after.head
  after = after.tail
}
```

When the List is empty, we have a full permutation, we call the function on it. Otherwise, we have a loop that runs all the elements we want to permit and makes recursive calls assuming each one has been added to the head of the permutation. This is done using two Lists and a while loop. To start off with, one List is empty and the other is all the elements in the input List. We can check if this function works by calling it.

```scala
permute(List(1,2,3), p => println(p), List())
```
