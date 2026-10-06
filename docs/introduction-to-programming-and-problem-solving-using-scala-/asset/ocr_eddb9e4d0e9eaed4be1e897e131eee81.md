# 464 Introduction to Programming and Problem-Solving Using Scala

```
r.stroke = Color.Black
content += r
{}
```

```
val num = if (args.length>0) args(0).toInt else 7
val pegs = Array(List.tabulate(num)(i => makeDisk(0, num-i, i+2)),
List[Rectangle](), List[Rectangle]())

ndef moveDisk(to:Int,from:Int) {
  require(to.isEmpty || pegs(from).head.width <
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

```
ndef moveDisks(n:Int,from:Int,to:Int) {
  val other = 3-from-to
  if (n==1) {
    moveDisk(from, to)
  } else {
    moveNDisks(n-1, from, other)
    moveDisk(from, to)
    moveNDisks(n-1, other, to)
  }
}
```

```
val button = new Button("Start")
content += button
button.onClick = (e:ActionEvent) => Future {
  moveNDisks(pegs(0).size, 0, 2)
}
```

main so that you can watch the animation, it is a Button, that when clicked makes a call to moveNDisks. This happens in a Future so Inside the moveNDisks function, code was added that changes the location of the disk that was moved, and pauses the world for a short period so that you can see it. Now the rectangles simply disappear from their old position and appear in the new one. It is left as an exercise for the student to use Transitions to animate this process.

If you play with this code you will notice that many stacks of disks take a very long time to move. This leads to the question of how many disks does it take to get N disks from one peg to another? The recursive code makes this question fairly easily to answer