```
void OnDrawGizmos()
{
    // we only want to draw the waypoints when we're editing,
    // not when we are playing the game
    if ( Application.isPlaying )
        return;
}
```

Application.Playing can be checked to find out whether not Unity is in edit mode or playing your game. There is no point in wasting time or CPU cycles drawing waypoints when the game is running, so we did a quick check to drop whenever we are not in edit mode.

The next steps are to keep the transforms up to date (just in case they are moved or new ones added in the editor). Also, when you build a path, obviously it will start with a single waypoint. With only one point, there is no end point for rendering a line in the editor, so this function checks that there are enough waypoints to actually draw a line and drops out when totalTransforms is less than 2.

```
GetTransforms();
```

```
// make sure we have more than one transform in the
// the list, otherwise we can't draw lines between them
if (totalTransforms < 2)
    return;
```

```
// draw our path first, we grab the position of the very
// first waypoint so that our line has a start point
TEMTRans = (Transform)transforms[0];nlastPos = TEMTRans.position;
```

```
// we point each waypoint at the next, so that we can use
// the wrong way or to find out where the player is going
// after a reset
// facing the correct direction. So first we need to hold a
pointT = (Transform)transforms[0];
// also, as this is the first point we store it to use for
// closing the path later
firstPos = lastPos;
```

```
// now we loop through all of the waypoints drawing lines
// between them
for (int i = 1; i < totalTransforms; i++)
{
    TEMTRans = (Transform)transforms[i];
    if (TEMTRans==null)
    {
        GetTransforms();
        return;
    }
}
```

```
// grab the current waypoint position
currentPos = TEMptrans.position;
```