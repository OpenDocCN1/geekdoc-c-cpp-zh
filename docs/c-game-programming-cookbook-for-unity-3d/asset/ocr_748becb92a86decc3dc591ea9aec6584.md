```
void resetRespawn()
{
    canRespawn=true;
}
ublic void GetAIInput (float amount)
{
    // calculate steering
    steer= Mathf.Clamp( AIController.GetHorizontal(), -1, 1 );

    // how much accelerator?
    motor= Mathf.Clamp( AIController.GetVertical() , 0, 1 );
}
public void FinishedRace()
{
    // stop allowing control for the vehicle
    canControl = false;
    brake = 1;
    motor = 0;

    // set a flag so it's easy to tell when we are done
    raceControl.RaceFinished();
}
public void SetAIInput (bool aiFlag)
{
    isAIntrolled = aiFlag;
}
public bool IsFinished ()
{
    return raceControl.GetFinished();
}
public int GetCurrentLap ()
{
    return raceControl.GetCurrentLap();
}
public int GetCurrentWaypointNum ()
{
    return raceControl.GetCurrentWaypointNum();
}
public float GetCurrentWaypointDist ()
{
    return raceControl.GetCurrentWaypointDist();
}
public bool IsLapDone ()
{
    return raceControl.GetIsLapDone();
}
public void SetWayController( Waypoints_Controller aControl )
{
    raceControl.SetWayController(aControl);
}
```