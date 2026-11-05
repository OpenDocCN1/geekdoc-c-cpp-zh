```
the ground    // cast a ray down from the waypoint to try to find
RaycastHit hit;
if (Physics.Raycast(tempVEC + (Vector3.up * 10), -Vector3.up, out hit))
{
    tempVEC.y = hit.point.y + 2.5f;
}
```

As it is quite common for the waypoints to be either off the ground or too close to the ground for our respawn to work correctly, the code above deals with ray casting down to find the ground Collider. We project a ray from tempVEC (the waypoint's position) add 10 units upward. The ray goes straight down at -Vector3.up and we put raycast hit information into the locally scoped variable, hit.

If the raycast was successful, it will return true, and we run the code between the graphics. What happens there is that tempVEC has its y position set to the ground position we just found through the raycast (hit.point) add 2.5 units. This number (2.5f) may be adjusted to respawn the vehicle closer or further from the ground as required. By the way, tempVEC will be used as the final position for the vehicle during repositioning:

```
_myController._TR.rotation = _tempTR.rotation;
_myController._TR.position = tempVEC;
blockRespawn = true;
Invoke("ResetRespawnBlock", 5f);
}
```

Above, Respawn() ends by setting our vehicles rotation to that of the waypoint Transform in _tempTR. Then on the next line, its position is set to the Vector3 in tempVEC. We then set blockRespawn to true and in the last line of the function, a call to ResetRespawnBlock() is scheduled for 5 seconds' time. This means that the respawn function will be disabled for 5 seconds after a respawn.

```
void ResetRespawnBlock()
{
    blockRespawn = false;
}
```

ResetRespawnBlock sets blockRespawn to false, allowing respawns again after a delay.

```
public override void PlayerFinishedRace()
{
```

When a player has completed all of the laps in the race, GlobalRaceManager calls the PlayerFinishedRace() function in the RaceController class. Above, we override RaceController's version of PlayerFinishedRace() to do something specific to this game. When our player has finished all of their race laps, we have the AI take control of the vehicle and drive it around until the entire race finishes when all players have completed their laps, too.

```
if (!AIControlled)
{
    // make sure we give control over to AI if it's not already
    AIControlled = true;
```