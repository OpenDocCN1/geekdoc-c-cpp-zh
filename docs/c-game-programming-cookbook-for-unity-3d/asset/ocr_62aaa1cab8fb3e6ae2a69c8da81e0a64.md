```
public virtual void Init ()
{
    // cache the usual suspects
    myBody= rigidbody;
    myGO= gameObject;
    myTransform= transform;

    // add default keyboard input
    default_input= myGO.AddComponent<Keyboard_Input>();

    // cache a reference to the player controller
    myPlayerController= myGO.GetComponent<BasePlayerManager>();

    if (myPlayerController==null)
        myPlayerController.Init();
}

public virtual void SetUserInput (bool setInput)
{
    canControl= setInput;
}

public virtual void GetInput()
{
    horiz= Mathf.Clamp(default_input.GetHorizontal(), -1, 1 );
    vert= Mathf.Clamp(default_input.GetVertical(), -1, 1 );
}

public void LateUpdate()
{
    // we check for input in LateUpdate because Unity recommends
    // this
    if(canControl)
        GetInput();
}

public bool moveDirectionally;

private Vector3 targetDirection;
private float curSmooth;
private float targetSpeed;
private float curSpeed;
private Vector3 forward;
private Vector3 right;

void UpdateSmoothedMovementDirection ()
{
    if (moveDirectionally)
    {
        UpdateDirectionalMovement();
    } else 
{
        UpdateRotationMovement();
    }
}

void UpdateDirectionalMovement()
{
    // find target direction
    targetDirection= horiz * Vector3.right;
```