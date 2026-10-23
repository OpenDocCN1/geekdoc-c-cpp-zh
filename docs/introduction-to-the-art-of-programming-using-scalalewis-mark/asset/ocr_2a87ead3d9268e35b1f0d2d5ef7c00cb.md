To make this more concrete, picture yourself at a four-way intersection. You ask the oracle about each direction and get values of 7, 13, 4, and 19. So the shortest path lies in the direction that gave you back 4. However, that was the distance from one step in that direction. The minimum distance from where you are is one greater than that, or 5 steps. It is the minimum of the four, plus one step to get to that other location. The solution of taking the minimum also points us in the proper direction for the base case of hitting a wall or going out of bounds. If the best solution is the minimum, we should return a number that can not possibly be the minimum for a bad path. A large number such as one billion will suffice for virtually any maze. You might be tempted to use Int.MaxValue, but remember that we are adding 1 to it. Try doing Int.MaxValue+1 in the REPL and you will see why that is not an ideal choice.

That defines our recursive case. There is only one other factor that needs to be considered. If you have ever been in a hedge maze or some other maze where you can not see over the walls, it can be quite difficult to tell one location from another, and unless you do something to mark your previous locations you can wind up running in circles and never finding your way out. A rather famous solution to this problem was described by the Brothers Grimm in Hansel and Gretel who left breadcrumbs to mark their path. We will choose the same approach. Assuming you have no birds in your computer this should work better for you than it did for the children. If you do have birds in your computer, you should probably deal with that before reading on.

So the last facet that we need for our algorithm is the ability to drop down breadcrumbs to mark our path. If we ever come back upon our breadcrumbs we will treat it just like being in a wall or out of bounds. We will also sweep up our breadcrumbs before we return from a path. This was not required by Hansel and Gretel who simply wanted to be able to find their path. We, however, want to find an optimal path and leaving breadcrumbs all over the place would often cause us to miss such a path. Converting this all to code produces the following.

```
```scala
def shortestPath(maze:Array[Array[Int]],x:Int,y:Int,endX:Int,endY:Int):Int = {
  if(x<0 || y<0 || y>=maze.length || x>=maze(y).length || maze(y)(x)!=0) {
    1000000000
  } else if (x==endX \&\& y==endY) {
    0
  } else {
    maze(y)(x)=1
    val dist=(shortestPath(maze,x+1,y,endX,endY) min
      shortestPath(maze,x-1,y,endX,endY) min
      shortestPath(maze,x,y+1,endX,endY) min
      shortestPath(maze,x,y-1,endX,endY)) + 1
    maze(y)(x)=0
    dist
  }
}
```
```

The whole function is built from if expressions. The first option is for going out of bounds, hitting a wall, or coming across one of our breadcrumbs, and it returns one billion, a number so large it can not possibly be a valid path, but one small enough that we also will not overflow it by adding 1 for other steps through the maze. The second case is where we have reached the end. These two can be reversed and would need to be if the exit were outside of the bounds or marked by a special value in the array. The last case is the recursive case which drops a breadcrumb, makes four recursive calls and combines them with min, then picks up the breadcrumb and returns. This code could be invoked with this call.