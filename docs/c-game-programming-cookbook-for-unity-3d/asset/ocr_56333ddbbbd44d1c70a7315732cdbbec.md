```
}
void FinishGame ()
{
    Application.LoadLevel( mainMenuSceneName );
}
The Timer is started at the end of the countdown, with a call toTimer():
void FinishedCount ()
{
    HideCount ();
    // let the timer begin!
    theTimer.StartTimer();
}
```

# 13.5 Battle Controller

The battle controller is Tank Battle's equivalent to Metal Vehicle Doom's race controller. It is applied to all players to be tracked as members of the battle, and the global battle manager will talk to these script components to keep an overall picture of the battle (managing the score board, etc.). The full script looks like this:

```
using UnityEngine;
using System.Collections;
public class BattleController : MonoBehaviour
{
    private bool isFinished;

    private Vector3 myPosition;

    private Transform myTransform;
    public int howmany_frags;
    public int howMany_fraggedOthers;

    public bool battleRunning;

    private bool doneInit();

    // we default myID to -1 so that we will know if the script hasn't
    // finished initializing when another script tries to GetID
    private int myID = -1;

    public BattleController ()
    {
        myID= GlobalBattleManager.Instance.GetUniqueID( this );
        Debug.Log("ID assigned is "+myID);
    }

    public void void Init()
```