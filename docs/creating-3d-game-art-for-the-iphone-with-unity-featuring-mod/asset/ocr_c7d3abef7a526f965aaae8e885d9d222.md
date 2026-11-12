it above the run cycle, that is at zero since it wasn't assigned a layer. Now, the shoot animation will receive the blend weights before the run, and the run will only receive weights if the shoot animation doesn't use all 100% of the blend weights. When CrossFading the shoot animation by using animation.CrossFade("shoot"), the weights for the shoot animation will start from zero and increase to 100%. It's much like fading in an animation over top of another. The run animation will gradually decrease as the shoot animation is "faded in".

However, this isn't what I'm particularly looking to do, as I want the shoot animation to play as the character is running. This is where additive blending comes into play.

# ### Additive Blending

In order to have the shoot animation play on top of and along with the run animation, we need to set the blend mode to additive for the AnimationState as shown in Fig. 7.17.

Now, when the player hits the fire button or, in this basic example, touches the screen, I can simply play the shoot animation, and it will be added on top of the run animation as shown in Fig. 7.18.

In Fig. 7.19, you can see both animations playing as they are added together via layering and additive blending. On the left side of the image, you can see the animations playing from Unity iOS and on the right, the same animations being added together in Blender. Notice through Unity's Animation System, we were able to produce the exact shooting while running animation in Unity iOS as was produced in Blender using the NLA Editor.

As you can see, this is a very powerful workflow as the shoot animation can now be added to any other animations such as a walk cycle. I no

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
```
```

FIG 7.17 The blendMode for the Shoot Variable Is Set to Be Additive.