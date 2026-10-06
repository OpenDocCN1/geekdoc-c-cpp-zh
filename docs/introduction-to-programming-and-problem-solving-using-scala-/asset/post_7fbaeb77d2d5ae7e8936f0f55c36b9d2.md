
## Introduction to Programming and Problem-Solving Using Scala

The meat of the Maze class is the updateAll method that calls lines 64-114. This gets called by the timer in Game roughly every 0.1 seconds. It takes no arguments, and returns in Int that is the number of points scored by the player in tick. The method begins by calling update on the player. After this, it checks to see if the player is in the process of dying or not. If so, it checks if that has been happening for 10 ticks yet. If it has, it initContents to reset the board. Either way, it returns 0. The more interesting branch is when the player is not dying. Each of the ghosts are updated, and the count variable is incremented. You then see sections that have comments for eating pellets, running into ghosts, running into fruit, and replenishing fruit. The value that is returned is the sum of points the player got eating fruit, ghosts, and fruit.

The ghost interactions are one subsection that needs more explanation, because it uses a foldLeft operation. This code runs through the ghosts and maps each to one tuple. The tuple has the number of players gets that ghost in the first element and which ghost killed the player. If it is on line 86 if they are close enough to interact. If they are and the ghost is scored, we tell that ghost that it has been eaten and returns points and the player was not killed. If the ghost was not scored, then there are no points, and the player was not killed. If they are not close enough to interact then are are put through a foldLeft operation that combines them.

The results of that map are the first elements, which are the scores, are added up, while the second elements, whether or not the player died, are or together. If any ghost killed the player, the player is dead. This logic could be done with a for loop and two vars for ghostScore and dying. That code would look like the following.

```scala
var ghostScore = 0
var dying = false
for (g <- ghosts) {
  if (g.player.x).abs < 0.8 && (g.player.y).abs < 0.8) {
    if (g.scared) {
      g.eating()
      ghostScore += 200
    } else {
      dying = true
    }
  }
}
```

123-128 in the companion object declare a number of constants that are used in other classes to support navigation around the maze.

Next is the PacMan class. This class is true to the initial design. The data from our design is split between arguments that are passed from outside code and some values are always set to defaults. There is also a number of accessor methods.

## Listing 16.7: PacMan.scala

```scala
class PacMan(
  private var _x:Double,
  private var _y:Double,
  private var _dir:Int
) {
  private var _animationCount = 0
  private var keyDir = -1
  private var _dying = false
```

## Object-Orientation

```scala
Game.newLife()
def x = _x
def y = _y
def dir = _dir
def animationCount = _animationCount
def dying = _dying
def setDying(Unit):Unit = {
    _dying = true
    _animationCount = 0
}
def update(maze:Unit) = {
    if (dying) {
        _animationCount += 1
    } else {
        if ((x == x.toInt()) && y == y.toInt()) {
            allowed = (0 to 3).filter(d => 
                maze.cell((x+Maze.XOffset(d)).toInt(), y+Maze.YOffset(d)).toInt()) > 0
            )
            if (allowed.contains(keyDir)) _dir = keyDir
            if (!allowed.contains(keyDir)) _dir = -1
        } else if ((keyDir+2)*4 == dir) {
            _dir = keyDir
        }
        if (dir > 0) {
            _x += Maze.XOffset(dir)/4.0
            _y += Maze.YOffset(dir)/4.0
            if (x < -1) _x = maze.columns
        } else if (x > maze.columns) _x = -1
            _animationCount += 1
        }
    }
}
def goLeft:Unit = keyDir = Maze.Left
def goRight:Unit = keyDir = Maze.Right
def goUp:Unit = keyDir = Maze.Up
def goDown:Unit = keyDir = Maze.Down
```

The first thing that stands out here is line 10, which calls Game.newLife(). With this line of code we are creating a PacMan instance automatically reduces the number of lives the player has. Lines 18-21 add that what was not in the design is called by the Maze when the player runs into a ghost that is not scared.

As with Maze, the main logic of this class is contained in the update method lines 23-44. If the player is dying, it only increments the animation count. Otherwise, it checks if the position of the player is a whole number in both x and y. The reason for this check is that the player can only turn at an intersection, which means that the fractional parts are zero. If they are at whole numbers, the filter on lines 28-30 checks which directions are safe for the player to turn. This code uses the XOffset and YOffset arrays that are defined in the Maze object. You should spend a few minutes looking at those values to understand how they work. Up is 0, and if you look at the offsets, the values at index 0 is 0 for x and -1 for y, which is the combination you need for moving up.

After the valid directions have been determined, line 31 checks if the direction the player has pressed is allowed. If it is, it becomes the new direction for movement. This style of handling input gives the game a feel that is typical for Pac-Man, where you can select a direction before you go to turn, and the character will go in that direction when it gets line 32 checks if the current direction is allowed. This line is critical; without it, the PacMan will go through walls when it runs into them. The else if on line 33-35 allows the player to turn around if they are located at a fractional block.

Lines 36-42 check if the player is moving and, if so, it moves and updates the animation count. The movement includes checks that wrap the player from one side to the other. The ghost interactions are one subsection that needs more explanation, because it uses a foldLeft operation. This code runs through the ghosts and maps each to one tuple. The tuple has the number of players gets that ghost in the first element and which ghost killed the player. If it is on line 86 if they are close enough to interact. If they are and the ghost is scored, we tell that ghost that it has been eaten and returns points and the player was not killed. If the ghost was not scored, then there are no points, and the player was not killed. If they are not close enough to interact then are are put through a foldLeft operation that combines them.

The results of that map are the first elements, which are the scores, are added up, while the second elements, whether or not the player died, are or together. If any ghost killed the player, the player is dead. This logic could be done with a for loop and two vars for ghostScore and dying. That code would look like the following.

```scala
var ghostScore = 0
var dying = false
for (g <- ghosts) {
  if (g.player.x).abs < 0.8 && (g.player.y).abs < 0.8) {
    if (g.scared) {
      g.eating()
      ghostScore += 200
    } else {
      dying = true
    }
  }
}
```

123-128 in the companion object declare a number of constants that are used in other classes to support navigation around the maze.

Next is the PacMan class. This class is true to the initial design. The data from our design is split between arguments that are passed from outside code and some values are always set to defaults. There is also a number of accessor methods.

## Listing 16.7: PacMan.scala

```scala
class PacMan(
  private var _x:Double,
  private var _y:Double,
  private var _dir:Int
) {
  private var _animationCount = 0
  private var keyDir = -1
  private var _dying = false
```

## Listing 16.8: Ghost.scala

```scala
import scalafx.paint.Color

class Ghost(
    private var _x:Double,
    private var _y:Double,
    private var _dir:Int,
    private var _animationCount:Int,
    val color:Color) {
    private var _scared = false

    def x = _x
    def y = _y
    def dir = _dir
    def animationCount = _animationCount
    def scared = _scared

    def scare():Unit = {
        _scared = true
        _animationCount = 0
    }

    def eat():Unit = {
        x = 9
        y = 9
        _scared = false
    }

    def update(maze:Maze) = {
        if (dying) {
            _animationCount += 1
        } else {
            if ((x == x.toInt()) && y == y.toInt()) {
                val allowed = (0 to 3).filter(d => 
                    maze.cell((x+Maze.XOffset(d)).toInt(), y+Maze.YOffset(d)).toInt()) > 0
                )
                if (allowed.contains(keyDir)) _dir = keyDir
                if (!allowed.contains(keyDir)) _dir = -1
            } else if ((keyDir+2)*4 == dir) {
                _dir = keyDir
            }
            if (dir > 0) {
                _x += Maze.XOffset(dir)/4.0
                _y += Maze.YOffset(dir)/4.0
                if (x < -1) _x = maze.columns
            } else if (x > maze.columns) _x = -1
                _animationCount += 1
        }
    }
    def goLeft:Unit = keyDir = Maze.Left
    def goRight:Unit = keyDir = Maze.Right
    def goUp:Unit = keyDir = Maze.Up
    def goDown:Unit = keyDir = Maze.Down
}

object Ghost {
    val scaredTime = 100
}
```

## Introduction to Programming and Problem-Solving Using Scala

The meat of the Maze class is the updateAll method that calls lines 64-114. This gets called by the timer in Game roughly every 0.1 seconds. It takes no arguments, and returns in Int that is the number of points scored by the player in tick. The method begins by calling update on the player. After this, it checks to see if the player is in the process of dying or not. If so, it checks if that has been happening for 10 ticks yet. If it has, it initContents to reset the board. Either way, it returns 0. The more interesting branch is when the player is not dying. Each of the ghosts are updated, and the count variable is incremented. You then see sections that have comments for eating pellets, running into ghosts, running into fruit, and replenishing fruit. The value that is returned is the sum of points the player got eating fruit, ghosts, and fruit.

The ghost interactions are one subsection that needs more explanation, because it uses a foldLeft operation. This code runs through the ghosts and maps each to one tuple. The tuple has the number of players gets that ghost in the first element and which ghost killed the player. If it is on line 86 if they are close enough to interact. If they are and the ghost is scored, we tell that ghost that it has been eaten and returns points and the player was not killed. If the ghost was not scored, then there are no points, and the player was not killed. If they are not close enough to interact then are are put through a foldLeft operation that combines them.

The results of that map are the first elements, which are the scores, are added up, while the second elements, whether or not the player died, are or together. If any ghost killed the player, the player is dead. This logic could be done with a for loop and two vars for ghostScore and dying. That code would look like the following.

```scala
var ghostScore = 0
var dying = false
for (g <- ghosts) {
  if (g.player.x).abs < 0.8 && (g.player.y).abs < 0.8) {
    if (g.scared) {
      g.eating()
      ghostScore += 200
    } else {
      dying = true
    }
  }
}
```

123-128 in the companion object declare a number of constants that are used in other classes to support navigation around the maze.

Next is the PacMan class. This class is true to the initial design. The data from our design is split between arguments that are passed from outside code and some values are always set to defaults. There is also a number of accessor methods.

## Listing 16.7: PacMan.scala

```scala
class PacMan(
  private var _x:Double,
  private var _y:Double,
  private var _dir:Int
) {
  private var _animationCount = 0
  private var keyDir = -1
  private var _dying = false
```

## Object-Orientation

```scala
Game.newLife()
def x = _x
def y = _y
def dir = _dir
def animationCount = _animationCount
def dying = _dying
def setDying(Unit):Unit = {
    _dying = true
    _animationCount = 0
}
def update(maze:Unit) = {
    if (dying) {
        _animationCount += 1
    } else {
        if ((x == x.toInt()) && y == y.toInt()) {
            allowed = (0 to 3).filter(d => 
                maze.cell((x+Maze.XOffset(d)).toInt(), y+Maze.YOffset(d)).toInt()) > 0
            )
            if (allowed.contains(keyDir)) _dir = keyDir
            if (!allowed.contains(keyDir)) _dir = -1
        } else if ((keyDir+2)*4 == dir) {
            _dir = keyDir
        }
        if (dir > 0) {
            _x += Maze.XOffset(dir)/4.0
            _y += Maze.YOffset(dir)/4.0
            if (x < -1) _x = maze.columns
        } else if (x > maze.columns) _x = -1
            _animationCount += 1
        }
    }
}
def goLeft:Unit = keyDir = Maze.Left
def goRight:Unit = keyDir = Maze.Right
def goUp:Unit = keyDir = Maze.Up
def goDown:Unit = keyDir = Maze.Down
```

The first thing that stands out here is line 10, which calls Game.newLife(). With this line of code we are creating a PacMan instance automatically reduces the number of lives the player has. Lines 18-21 add that what was not in the design is called by the Maze when the player runs into a ghost that is not scared.

As with Maze, the main logic of this class is contained in the update method lines 23-44. If the player is dying, it only increments the animation count. Otherwise, it checks if the position of the player is a whole number in both x and y. The reason for this check is that the player can only turn at an intersection, which means that the fractional parts are zero. If they are at whole numbers, the filter on lines 28-30 checks which directions are safe for the player to turn. This code uses the XOffset and YOffset arrays that are defined in the Maze object. You should spend a few minutes looking at those values to understand how they work. Up is 0, and if you look at the offsets, the values at index 0 is 0 for x and -1 for y, which is the combination you need for moving up.

After the valid directions have been determined, line 31 checks if the direction the player has pressed is allowed. If it is, it becomes the new direction for movement. This style of handling input gives the game a feel that is typical for Pac-Man, where you can select a direction before you go to turn, and the character will go in that direction when it gets line 32 checks if the current direction is allowed. This line is critical; without it, the PacMan will go through walls when it runs into them. The else if on line 33-35 allows the player to turn around if they are located at a fractional block.

Lines 36-42 check if the player is moving and, if so, it moves and updates the animation count. The movement includes checks that wrap the player from one side to the other.

## Listing 16.8: Ghost.scala

```scala
import scalafx.paint.Color

class Ghost(
    private var _x:Double,
    private var _y:Double,
    private var _dir:Int,
    private var _animationCount:Int,
    val color:Color) {
    private var _scared = false

    def x = _x
    def y = _y
    def dir = _dir
    def animationCount = _animationCount
    def scared = _scared

    def scare():Unit = {
        _scared = true
        _animationCount = 0
    }

    def eat():Unit = {
        x = 9
        y = 9
        _scared = false
    }

    def update(maze:Maze) = {
        if (dying) {
            _animationCount += 1
        } else {
            if ((x == x.toInt()) && y == y.toInt()) {
                val allowed = (0 to 3).filter(d => 
                    maze.cell((x+Maze.XOffset(d)).toInt(), y+Maze.YOffset(d)).toInt()) > 0
                )
                if (allowed.contains(keyDir)) _dir = keyDir
                if (!allowed.contains(keyDir)) _dir = -1
            } else if ((keyDir+2)*4 == dir) {
                _dir = keyDir
            }
            if (dir > 0) {
                _x += Maze.XOffset(dir)/4.0
                _y += Maze.YOffset(dir)/4.0
                if (x < -1) _x = maze.columns
            } else if (x > maze.columns) _x = -1
                _animationCount += 1
        }
    }
    def goLeft:Unit = keyDir = Maze.Left
    def goRight:Unit = keyDir = Maze.Right
    def goUp:Unit = keyDir = Maze.Up
    def goDown:Unit = keyDir = Maze.Down
}

object Ghost {
    val scaredTime = 100
}
```
