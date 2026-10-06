
## 512 Introduction to Programming and Problem-Solving Using Scala

The end of update checks if the Ghost has reached its maximum time being scared and sets that to false if it has reached its max. The companion object defines the constant for how long the ghosts remain scared.

The main thing missing from this Ghost implementation is that they always turn randomly, no matter where the player is. In reality, they should generally head toward the player when they are not scared, and they should head away from the player when they are scared. In the actual game, they also move slightly faster than the player when they are not scared and slightly slower. The intelligent direction selection can be implemented with the recursive shortest path algorithm introduced in chapter 15. Making these enhancements is left as an exercise for the reader.

The simplest class is Fruit. It does nothing more than store a location and a type. There is also a companion object that stores information related to Fruit.

## Listing 16.9: Fruit.scala

```scala
import scalafx.scene.paint.Color
class Fruit(
    val x:Double,
    val y:Double,
    val fruitType:Int) {

  object Fruit {
    val Cherry = 0
    val Strawberry = 1
    val Orange = 2
    val Scores = List(100, 300, 500)
    val Colors = List(Color.Red, Color.Fuchsia, Color.Orange)
  }
}
```

The last file to part of the Pac-Man™ implementation is the Renderer. Because this singleton implementation allows only one of them at a time, it has been declared as a singleton object. The fact that there are no data members in this tells us that it should probably be an object instead of a class. A class would allow us to create multiple instances, but why should we make multiple instances of a type that does not have any data in it? Generally, the answer is that we should not; so, in that situation, an object declaration is the better choice.

The object has a single method called renderer that takes a GraphicsContext and a Maze. It draws everything in it to the GraphicsContext.

## Listing 16.10: Renderer.scala

```scala
import scalafx.scene.canvas._
import scalafx.scene.paint._
import scalafx.scene.shape.ArcType

object Renderer {
    def renderer(gc:GraphicsContext, maze:Maze):Unit = {
        gc.fill = Color.Black
        gc.fillRect(0, 0, maze.Width, maze.Height)
        val cellWidth = maze.Width/maze.columns
        val cellSize = maze.Height/maze.rows
        for (i <- 0 until maze.rows; j <- 0 until maze.columns) {
            maze.cell(j, i) match {
              case Maze.Wall =>
                gc.fill = Color.Blue
                gc.fillRect(j*cellWidth, i*cellHeight, cellWidth, cellHeight)
              case Maze.Pellet =>
                gc.fill = Color.White
                gc.fillOval(j*cellWidth+3*cellWidth/8, i*cellHeight+3*cellHeight/8, cellWidth/4, cellHeight/4)
              case Maze.PowerPellet =>
                gc.fill = Color.White
                gc.fillOval(j*cellWidth+cellWidth/4, i*cellHeight+cellHeight/4, cellWidth/2, cellHeight/2)
              case Maze.Open =>
              case Maze.Door =>
                gc.fill = Color.LightGray
                gc.fillRect(j*cellWidth, i*cellHeight+cellHeight/4, cellWidth, cellHeight/2)
            }
        }
        maze.ghosts.foreach(g => drawGhost(gc, g, cellWidth, cellHeight))
        drawPacMan(gc, maze.player, cellWidth, cellHeight)
        maze.fruit.foreach(f => {
            gc.fill = Fruit.Colors(f.type)
            gc.fillOval(f*cellWidth+cellWidth/4, f*cellHeight+cellHeight/4, cellWidth/2, cellHeight/2)
        })
        gc.fill = Color.White
        gc.fillText(Game.score.toString, 10, 20)
        for (i <- 0 until Game.lives) {
            gc.fill = Color.Yellow
            gc.fillArc(400+i*cellWidth, 0, cellHeight, 45, 270, ArcType.Round)
        }

        private def drawPacMan(gc:GraphicsContext, pm:PacMan, cellWidth:Double, cellHeight:Double):Unit = {
            gc.fill = Color.Yellow
            if (pm.dy) {
                val center = 90
                val openAngle = pm.animationCount*18
                gc.fillArc(pm.x*cellWidth, pm.y*cellHeight, cellWidth, cellHeight, center+openAngle, 360-2*openAngle, ArcType.Round)
            } else {
                val openAngle = 45+math.sin(pm.animationCount/2.0)*math.sin(pm.animationCount/2.0)
                val center = pm.dir match {
                    case Maze.Up => 90
                    case Maze.Right => 0
                    case Maze.Down => 270
                    case Maze.Left => 180
                    case _ => 0
                }
                gc.fillArc(pm.x*cellWidth, pm.y*cellHeight, cellWidth, cellHeight, center+openAngle, 360-2*openAngle, ArcType.Round)
            }
        }

        private def drawGhost(gc:GraphicsContext, ghost:Ghost, cellWidth:Double, cellHeight:Double):Unit = {
            if (ghost.scared) {
                gc.fill = Color.DarkBlue
            } else {
                gc.fill = Color.Blue
            }
            if (ghost.animationCount < Ghost.ScaredTime || ghost.animationCount > 20) {
                gc.fillArc(ghost.x*cellWidth, ghost.y*cellHeight, cellWidth, cellHeight, 0, 180, ArcType.Round)
            }
            gc.fillRect(ghost.x*cellWidth, ghost.y*cellHeight+cellHeight/2, cellWidth, cellHeight)
        }
    }
}
```

Lines 12-27 draw the grid of the Maze, with pellets. There are separate methods that handle the drawing of the PacMan and after those are called, the Fruit is then drawn out however many lives the player has. The result produced by this looks like figure 16.2. The Renderer could be enhanced in a number of ways, especially the representations of the ghosts and the fruit, making the game playable. Hopefully these different examples give you a feel for the concepts of object orientation and how to think about programs using it. There is a lot more to explore, but that is left for Object-Orientation, Abstraction, and Data Structures Using Scala.

## 16.6 End of Chapter

### 16.6.1 Summary of Concepts

- Objects are constructs that combine data and functionality that operates on data. The standard way of making objects in Scala is to define a class and instantiate objects from it. You can think of a class as a blueprint for making objects.
- A def declaration in a class defines a method. A val or var defines member data.
- Classes can take parameters. By default they are not members. Adding val or var in front of the name makes it member data.
- By default, constructs inside of a class are public and can be seen by any code. Part of the power of object orientation comes from the ability to hide things so that other code cannot get to them. The private modifier makes it so no code outside of the class can see it. There is also a protected modifier that makes declarations visible only to subtypes.
- Scala allows declarations which create singleton objects. These cannot take arguments and are not instantiated with new. A single instance just exists for the ability to use it.

![](img/06d4e84f27a8884ea40ba6182ec7c78_539_0.png)16.2: This figure shows the window created by running the Pac-Man™ game.

- Scripts are good for small programs, but larger programs are written and run as applications. The entry point to an application is defined by a main method in an object. Top level declarations are split to different files. Code is compiled with scalac and run with scala.
- An object with the same name as a class can be declared in the same file and it becomes a companion object. Companions have access to private declarations.

### 16.6.2 Exercises

1. Alter the Ghost class to make intelligent direction choices to head toward or away from the player. Note that without always making the best choice the game becomes impossible.
2. Alter the Ghost class so that they move faster than the player when they are not scared and slower when they are.
3. You can turn any script that you wrote previously into an application by embedding everything into an object in the main method. The results of this should compile with scalac and run with scala.

The result of this simple conversion is not generally ideal. Any method or case declarations should generally be pulled out of main. The methods likely go inside object but outside of main. If these methods are not generally useful, they should be private. The classes could be inside of the object where they might not be private depending on how they are used. If they truly stand on their own and have meaning, they should go outside the object and into a separate file bearing their name.

The results of modification might not compile. That will depend on the quality of the original code and whether variables are declared outside of the methods. If you use variables outside of the methods in the body, you have one of two choices. Generally your first choice should be to pass these variables by adding extra parameters to the method. If a variable is a data member/property of the object, it can be moved to a level up so it too is in object, but not in main.

Your goal for this is to run through this process on a number of scripts that you wrote in the book. When you do this, it is recommended that you use a subdirectory for each script you are converting, copy files into there. This way you not only preserve the original script, but make it easier to compile that single application. Doing this on a number of scripts will really help to build your feel for how this new approach differs from what we have done previously.
