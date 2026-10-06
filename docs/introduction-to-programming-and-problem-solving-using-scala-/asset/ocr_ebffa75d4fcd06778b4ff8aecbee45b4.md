```
def dir = _dir
def animationCount = _animationCount
def scared = _scared

def scare():Unit = {
    _scared = true
    _animationCount = 0
}
```

```
def eat():Unit = {
    x = 9
    y = 9
    _scared = false
}
```

```
def update(maze:Maze):Unit = {
    if (animationCount >= 0) {
        if ((x == x.toPoint()) && y == y.toInt()) == Maze.Door {
            maze.cell(x.toInt,y.toInt-1)
            _dir = 0
        }
    } else {
        val allowed = (0 to 3).filter(d => {
            val cell = maze.cell(x+Maze.XOffset(d)).toInt,
            (y+Maze.YOffset(d)).toInt()
            cell > 0 && (d+2)*4 != 1
        })
        _dir = allowed.random().nextInt(allowed.length)
    }

    if (dir > 0) {
        x += Maze.XOffset(dir)/4.0
        y -= Maze.YOffset(dir)/4.0
    }
    if (x < -1) _x = maze.columns
    else if (x >= maze.columns) _x = -1
    }

    animationCount += 1
    if (_scared && animationCount > Ghost.ScaredTime) {
        _scared = false
    }
}
```

```
object Ghost {
    val scaredTime = 100
}
```

Again, the main logic is in the update method. The Ghost does not anything unless the animation count is non-negative. This allows us to easily get the ghosts to leave their home base one at a time. The logic for turning is like that for PacMan in that they can only turn when x and y have no fractional part, and finds the allowed directions using a filter. One difference is that the random selection is not allowed to send the Ghost back in the opposite direction it is currently heading. The Ghost picks randomly from those allowed directions. Lines 32-33 is a special case to the Ghost to come out of their home area as soon as they move below the Door cell.