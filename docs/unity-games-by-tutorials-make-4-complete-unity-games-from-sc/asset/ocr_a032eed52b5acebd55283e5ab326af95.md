Here you check isAlive first.

Finally, in Update(), surround the existing navigation code with a similar check to see if the alien is alive.

```
```
if (isAlive)
{
...
}
```
```

Save and switch to Unity. In the Project view, click the disclosure triangle next to the Alien prefab to reveal its children, and select BobbleEnemy-Head. Click the Add Component button and select Rigidbody from the physics category. Uncheck the Use Gravity option and check the Is Kinematic option.

Click Add Component once again, and select Sphere Collider from the physics category. Set Center to (0, 0, 0.02) and Radius to 0.03. Disable the component by unchecking the component checkbox.

Finally, assign to the layer Alien Head and select Yes, change children when prompted.

Select the Alien prefab in the Project view. In the Inspector, drag the BobbleEnemy-Head to the head property.

Play the game.

![](bbox=[0.282, 0.55, 0.712, 0.813])

It won't take long to accumulate an excess of disembodied alien heads. After a while, the space marine will struggle to differentiate the dead aliens from the living.