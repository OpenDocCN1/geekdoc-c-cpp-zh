```
// Iterate through them
foreach (GameObject go in gos)
{
```

Of course, it makes no sense for this gameObject to chase itself, and to avoid this,
is is a quick check to see whether go!=myGO:

```
if(go!=myGO) // make sure we're not comparing
    // ourselves to ourselves
{
```

To see whether this is a viable target, the process is a simple distance check with
Vector3.Distance(myGO's transform position (this player) and go's transform.
position (the most recent GameObject picked up by the foreach loop):

```
float aDist =
Vector3.Distance(myGO.transform.position,
go.transform.position);
if(checkForWalls)
{
    // wall check required
    if(CanSee(go.transform)==true)
    {
        AIControlComponent;
        SetChaseTarget(go.transform);
        foundTarget=true;
    }
} else {
```

When no wall check is required, aDist is compared to chaseDistance to see whether
the target set by the loop is close enough to be chased:

```
// no wall check required! go ahead
// and find something to chase!
if(aDist< chaseDistance)
{
```

The AI controller now needs to target the current GameObject from the foreach loop,
which is passed to it via BaseAuthController.SetChaseTarget():

```
// tell our AI controller to
// chase this target
AIControlComponent;
SetChaseTarget(go.transform);
```

We need to track whether or not a target has been found, so that if no suitable target
turns up, we can adapt the AI behavior:

```
foundTarget=true;

\}
```