
- **Step 20:** Save and return to Unity. Fix syntax.
- **Step 21:** Attach this new DamagePlayerScript to the Trigger-WaterKiller GameObject in the Hierarchy.
- **Step 22:** Select Trigger-WaterKiller and in the Inspector under the Damage Player Script component, define the Damage Amount as 10.
- **Step 23:** Test and play. Jump in the water and stay there. Watch the Health meter at the top and see how it drops by 10 every 2 seconds. Eventually, the Console will throw an error because you'll be dead, but Unity won't know of any Scene-ClosingFall scene.
- **Step 24:** Save Scene-EntryWay.
- **Step 25:** Open Scene-Hallway.
- **Step 26:** Deactivate Hallway_Unbaked and activate Hallway_BakedGroup.

## Why?

I know, you're probably sick of turning these off and on, and it would have been great if the tutorials were set up so we never had to do that but alas, with the concepts we're exploring this little annoyance is necessary to allow ideas to build upon each other.

- **Step 27:** Create a new trigger that fits into the area between all the stairs (Figure 17.8). This needs to be very accurate because if it's too big the player will hit it running down the stairs and die, but if it's too small, he might be able to fall all the way to the ground without hitting the trigger. Name the trigger Trigger-FallDeath.

**FIGURE 17.8** Trigger-FallDeath.

![](img/0285f88bc840f313779e011725b623a5_507_0.png)

## Why?

There are different ways to handle a character falling to his death. Some are more interesting than this one and can include timing how long a character is not grounded and is falling. Others simply measure whether a component Emit is turned off (a script activates it). This script is called SteamEmitters and it simply turns the emitters on and off based upon the distance the emitters are from the player:

``` 
private var fpcAegis : GameObject;

function Start () {
    fpcAegis = GameObject.Find("FPC_AegisChurch");
}

function Update () {
    var dist = Vector3.Distance (fpcAegis.transform.position, transform.position);
    if (dist <25) {
        particleEmitter.emit = true;
    } else {
        particleEmitter.emit = false;
    }
}
```

This is so that when walking through the dark version of the model, the steam for the entire level isn't visible (the shaders for particles are light independent). So as the player gets closer, the emitter emits.

The version of steam included in the Steam Unity package also includes an Audio Source component (Component>Audio>Audio Source) with a looping steam sound. Importantly, it contains a Box Collider component (Component>Physics>Box Collider) that is set to be a trigger. Finally, the Steam GameObject has attached to it the DamagePlayerScript with a Damage Amount set to 2 (Figure 17.9).

![](img/0285f88bc840f313779e011725b623a5_509_0.png)

Figure 17.9 Steam prefab.

If you understand how this was all put together, don’t worry about assembling your own; just use the provided prefab.

- **Step 30:** Either create your own steam prefab with these directions or import Steam.unitypackage from the supporting web site (http://www.Creating3DGames.com).

- **Step 31:** Place a bunch of Steam prefabs into the scene. Stick them inside the pipes that run through the hallways. Be sure to vary the rotations (some pointing straight down, some at an angle), so they don’t all appear quite as much like copies of themselves (Figure 17.10).

![](img/0285f88bc840f313779e011725b623a5_510_0.png)

*Figure 17.10*  Placed Steam prefabs

- **Step 32:** Group the Steam objects by creating an empty GameObject, labeling it SteamEmitters, and placing all the Steam objects as children of it.

- **Step 33:** Play and test (Figure 17.11). As the player hangs out in the steam, their Health should decrease by 2 units every 2 seconds.

![](img/0285f88bc840f313779e011725b623a5_510_1.png)

*Figure 17.11*  Working steam and damage being done as we hang out in it

- **Step 34:** Save Scene–Hallway.

## Timers on Cameras

Getting closer. We now have all sorts of ways to die. In a few pages, we will keep track of health from level to level (right now he miraculously is healed when he moves from the EntryWay to the Hallway). We just need to do a little bit of cleaning up.

Currently, if the CCTV camera sees you they throw up an awful racket, but there are no consequences. We need to add a mechanism to the cameras so that once they see the player, a countdown begins where if it reaches 0, the player loses the game.

Luckily, much of the mechanism already exists within the CCTV-CameraSearchingScript. We simply need to add a CountDown function that ends the game if the player doesn't destroy the camera.

- **Step 35:** Open CCTV-CameraSearchingScript.

- **Step 36:** Tell the script that when the raycast hits the object with the tag Player, to not only fire the PulseLight function, but to also fire a new function called CountDown:

``` 
var seenSomething : boolean;

function Update () {
    var hit : RaycastHit;
    if (Physics.Raycast (transform.position, transform.forward, hit, 100)) {
        Debug.DrawLine (transform.position, hit.point, Color.yellow);
        if (hit.collider.gameObject.tag == "Player") {
            seenSomething = true;
            PulseLight();
            CountDown();
        }
    }
}

function PulseLight() {
    audio.enabled = true;
    while (seenSomething) {
        var textureColor : Color;
        textureColor.r = Mathf.Sin (Time.time * 10.0);
        renderer.material.color = textureColor;
        yield;
    }
}
```

- **Step 37:** Create a simple function that tells Unity to wait for 10 seconds, and then launch the level Scene-ClosingFail:

``` 
var seenSomething : boolean;

function Update () {
    var hit : RaycastHit;
    if (Physics.Raycast (transform.position, transform.forward, hit, 100)) {
        Debug.DrawLine (transform.position, hit.point, Color.yellow);
        if (hit.collider.gameObject.tag == "Player") {
            seenSomething = true;
            PulseLight();
            CountDown();
        }
    }
}

function PulseLight() {
    audio.enabled = true;
    while (seenSomething) {
        var textureColor : Color;
        textureColor.r = Mathf.Sin (Time.time * 10.0);
        renderer.material.color = textureColor;
        yield;
    }
}

function CountDown() {
    yield WaitForSeconds (10);
    Application.LoadLevel("Scene-ClosingFail");
}
```

### Why?

Remember that this script is attached to the camera itself, and when the camera is shot it's destroyed and the broken version is instantiated in its place. Because the camera itself gets destroyed, the scripts attached to it destroy as well. So, if the player does indeed find the alerting camera and shoots it, this function (CountDown) never gets to its 10 seconds and therefore never launches Scene-ClosingFail.

- **Step 38:** Save and return to Unity. Fix syntax problems.

## Scene-ClosingFail

- **Step 39:** Duplicate Scene-Closing (select it in the Project panel and choose Edit>Duplicate). Rename the duplicate Scene-ClosingFail. Open this new Scene-ClosingFail.
- **Step 40:** Rename the Congratulations GUITexture to Fail and replace its texture with the DataPanel-Failed texture from the Project panel's 2D Assets.
- **Step 41:** Adjust lighting or other visual elements to give this version a darker feeling of failure. The image shown in Figure 17.12 simply turns the color balance of all the lights toward red.
- **Step 42:** Save Scene-ClosingFail.
- **Step 43:** Add Scene-ClosingFail to the Build Settings' (File>Build Settings) Scenes in Build.

FIGURE 17.12 Scene-ClosingFail.

![](img/0285f88bc840f313779e011725b623a5_513_0.png)

## Global Variables

We've created all sorts of variables at this point. We've created public variables (var nameOfVariable) that create a variable that can be populated within Unity's editor. We've created private variables (private var nameOfVariable) that store data, but usually are controlled and populated within the script. We've created local variables whose scope is limited to just a particular function.

The last type of variable we're going to cover is called a global variable. Global variables actually do just what the name implies—they are variables that are accessible globally. Importantly, a global variable remains constant between scenes. This becomes ideal for something like health.

- **Step 44:** Open the script HealthEngineScript.
- **Step 45:** Convert the variable “health” from a private to global variable and give it an initial value. Because we're defining an initial value in the declaration, remove the line `health = 100;` from the Start function:

``` 
static var health : int = 100;
private var healthLevel : GameObject;

function Awake ()
{
    healthLevel = GameObject.Find("HealthLevel");
}

function Start()
{
    healthLevel.guiText.text = health.ToString();
}

function ApplyDamage (damage : int){
    health -= damage;
    healthLevel.guiText.text = health.ToString();
    if (health <=0){
        KillPlayer();
    }
}
```
