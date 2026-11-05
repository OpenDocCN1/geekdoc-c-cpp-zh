
```
[System.NonSerialized]
public float steer = 0f;
[System.NonSerialized]
public float motor = 0f;
[System.NonSerialized]
public float brake = 0f;

[Space]
public float wheelToGroundCheckHeight = 0.5f;

[Space]
public bool fakeBrake;
public float fakeBrakeDivider = 0.95f;

[Space]
public bool turnHelp;
public float turnHelpAmount = 10f;

public bool isGrounded;

[System.NonSerialized]
public float mySpeed;

[System.NonSerialized]
public Vector3 velo;

[Header("Audio Settings")]
public AudioSource _engineSoundSource;
public float audioPitchOffset = 0.5f;
```

这里的大部分其他变量将在脚本后续部分进行讲解，随着我们逐步拆解，因此我们直接跳到 Start() 函数。Start() 会由引擎自动调用。它调用 Init() 函数，该函数首先缓存常用对象的引用：

```
public virtual void Start ()
{
    Init ();
}
```

```
public virtual void Init ()
{
    // cache the usual suspects
    _RB = GetComponent<Rigidbody>();
    _GO = gameObject;
    _TR = transform;
}
```

接下来，我们获取附加到此 GameObject 上的输入控制器组件的引用，然后设置我们的 Rigidbody 的质心：

```
_inputController = GetComponent<BaseInputController>();
_RB.centerOfMass = new Vector3(0,-0.1f,0);
```

可以在刚体上设置质心以改变其在物理模拟中的行为方式。质心距离刚体中心越远，对物理行为的影响越大。将质心向下设置到 -1 有助于使车辆保持稳定，并在转弯时防止车辆翻倒。

```
// see if we can find an engine sound source, if we need to
if (_engineSoundSource == null)
{
    _engineSoundSource = _GO.GetComponent<AudioSource>();
}
```

上面，如果未通过 Unity 编辑器的 Inspector 窗口设置引擎音源，脚本会尝试通过调用 GameObject.GetComponent() 来查找它。音源将被存储在 engineSoundSource 中，并仅用于引擎音效。

与所有移动控制器一样，SetUserInput（见下文）设置一个标志来决定是否使用输入来驱动车辆：

```
public void SetUserInput( bool setInput )
{
    canControl = setInput;
}
```

与本书中的其他移动控制器不同，这个控制器引入了锁定状态：

```
public void SetLock(bool lockState)
{
    isLocked = lockState;
}
```

锁定状态用于固定车辆位置而不影响其 y 轴。这与仅仅禁用用户输入不同，因为它为物理对象添加了物理约束以使其保持静止（其目的是在比赛开始前的倒计时或其他类似场景中固定车辆）。

```
public virtual void LateUpdate()
{
    if(canControl)
        GetInput();
    UpdateEngineAudio();
}
```

上面，LateUpdate() 首先在 canControl 设置为 true 时通过 GetInput() 函数检查输入。接下来，调用 UpdateEngineAudio() 来根据引擎速度更新引擎声音的音高。

```
public virtual void FixedUpdate()
{
    UpdatePhysics();
    DoFakeBrake();
    CheckGround();
}
```

上面，所有的物理代码都通过 FixedUpdate() 中的 UpdatePhysics() 调用执行。我们调用制动函数 DoFakeBrake() 以及 CheckGround() 来检查车辆是否在地面上。

```
public virtual void UpdatePhysics()
{
    CheckLock();
}
```

首先调用 CheckLock()，当锁定开启时（isLocked 为 true 时）它会固定车辆位置——非常适合在比赛开始时固定车辆！

// work out a flat velocity
velo = _RB.velocity;
velo = transform.InverseTransformDirection(_RB.velocity);

// work out our current forward speed
mySpeed = velo.z;
```

上面，变量 velo 被设置为保存我们车辆刚体的速度。下一行将该速度转换为局部坐标空间，以便我们获得车辆沿各轴移动速度的值。我们的车辆向前速度沿 z 轴，侧向沿 x 轴。我们取该 z 轴速度并放入变量 mySpeed 中，以便知道车辆移动的速度，mySpeed 在下一节中使用，在那里当车辆移动速度低于任意速度时我们模拟倒档：

```
// if we're moving slow, we reverse motorTorque and remove brakeTorque so that the car will reverse
if( mySpeed<2 )
{
    // that is, if we're pressing down the brake key
    // (making brake>0)
    if( brake>0 )
    {
        rearWheelLeft.motorTorque = -brakeMax * brake;
        rearWheelRight.motorTorque = -brakeMax * brake;
    }
```

上面，请注意这段代码是为了模拟倒档。会检查 mySpeed 的值是否小于 2。当速度如此缓慢且刹车键被按住时，轮子上不再施加 brakeTorque，而是施加最大刹车扭矩（brakeMax）的一部分的反向扭矩，使车辆向后移动。

```
rearWheelLeft.brakeTorque = 0;
rearWheelRight.brakeTorque = 0;
```

在倒档模式下，WheelColliders 上将不施加 brakeTorque（由上面的代码实现），以便车辆可以自由向后移动。虽然制动在上面已处理，但我们在脚本后面进一步处理倒档电机。

```
frontWheelLeft.steerAngle = steerMax * steer;
frontWheelRight.steerAngle = steerMax * steer;
```

当车辆倒车时，转向也会反向，就像真正的汽车一样。

```
// drop out of this function before applying the
// 'regular' non-reversed values to the wheels
return;
}
```

```
if (turnHelp)
    _RB.AddTorque(Vector3.up * steer * turnHelpAmount * _RB.mass);
```

仅使用车轮来转向汽车有时足够，但如果你正在制作更偏向街机的内容，你可能需要施加额外的转向力，使汽车感觉更不真实、更有趣。turnHelp 布尔变量可以在 Inspector 中打开或关闭，你可以调整 turnHelpAmount 以获得酷炫的效果。

在上面的代码中，Unity 的 AddTorque 函数用于将上方向向量乘以 steer、turnHelpAmount 和刚体的质量。在本书的示例赛车游戏中，turnHelpAmount 为 2 是街机物理的一个不错值。

接下来，我们将常规（向前）值应用到 WheelColliders：

// apply regular movement values to the wheels
rearWheelLeft.motorTorque = accelMax * motor;
rearWheelRight.motorTorque = accelMax * motor;
rearWheelLeft.brakeTorque = brakeMax * brake;
rearWheelRight.brakeTorque = brakeMax * brake;
frontWheelLeft.steerAngle = steerMax * steer;
frontWheelRight.steerAngle = steerMax * steer;
}
```

上面，我们告诉 WheelColliders 如何移动。motor、brake 和 steer 值将由本脚本后面的 GetInput() 函数设置。

```
public void DoFakeBrake()
{
    if (isGrounded && brake > 0 && fakeBrake && mySpeed > 0)
    {
        tempVEC = _RB.velocity;
        tempVEC.x = tempVEC.x * fakeBrakeDivider;
        tempVEC.z = tempVEC.z * fakeBrakeDivider;
        _RB.velocity = tempVEC;
    }
}
```

使用 WheelColliders 制动依赖于摩擦以及车轮与其下方地面的关系。主要问题是——如果不做大量工作——牵引力很容易丧失，很难使车辆停止。如果你在制作街机赛车而不是真实模拟，情况更是如此。为了解决这个问题，该脚本包含上面的 DoFakeBrake() 函数，它会降低车辆的速度值以更快地减速。要调整效果，你可以在 GameObject 的 Inspector 中更改 fakeBrakeDivider 的值，或通过 fakeBrake 布尔值的设置将其打开或关闭。

这种增强的制动系统仅在车辆在地面上时应用，因此它依赖于接下来 CheckGround() 函数设置的 isGrounded 布尔值：

```
public void CheckGround()
{
    bool FLGrounded = false;
    bool FRGrounded = false;
    bool RLGrounded = false;
    bool RRGrounded = false;

    if (Physics.Raycast(transform.position, Vector3.down, wheelToGroundCheckHeight))
        FLGrounded = true;
```
