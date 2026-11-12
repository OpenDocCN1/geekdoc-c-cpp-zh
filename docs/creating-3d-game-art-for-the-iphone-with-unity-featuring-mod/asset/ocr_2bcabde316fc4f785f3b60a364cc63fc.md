```
```javascript
private var shoot : AnimationState;

function Start()
{
    animation.Play("run");

    //Set the Shoot Clip
    shoot = animation["shoot"];
    //Place the Shoot Clip on layer above run clip
    shoot.layer = 1;
    //Set the blend mode to additive
    shoot.blendMode = AnimationBlendMode.Additive;
    //Enable shoot
    shoot.enabled = true;
}


function Update ()
{
    for (var i:int =0; i < Input.touchCount; i++){
        //Store touch
        var touch: Touch = Input.GetTouch(i);
        //Check to see if finger moved
        if (touch.phase == TouchPhase.Began) {
            print("Touch: First Began");
            animation.Play("shoot");
        } else if (touch.phase == TouchPhase.Ended){
            print("Touch Ended");
        }
    }

}
```
```

**FIG 7.18** Here You Can See the Script That Plays the Shoot Animation When the User Touches the Screen. Notice the Shoot Animation Is Placed on Layer 1 and That the AnimationBlendMode Is Set to Additive.

longer have to worry about creating different walk and run animations to encompass shooting, as I can easily layer it over any animations I create. Also, using this method, I could easily adapt new shooting animations for different weapon types knowing that these animations can be added to my existing walk, run, and strafing actions with ease. This makes adding new animations simple, as I don't need to create a set of special run and walk cycles for each new shooting animation. Think about creating sequels to your game, where new weapon animations can be created while allowing you to reuse some of your animations from the first game. Productivity is key when it comes to game development, and any time you can find a way to save yourself from re-creating something, you need to take it.

> *Productivity is key when it comes to game development, and any time you can find a way to save yourself from re-creating something, you need to take it.*