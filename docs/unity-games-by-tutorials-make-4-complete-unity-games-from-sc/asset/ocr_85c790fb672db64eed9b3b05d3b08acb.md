# Unity Games by Tutorials

To do this, add this to Start():

```
GameObject arena = transform.parent.gameObject;
renaAnimator = arena.GetComponent<Animator>();
```

First, gets the parent GameObject by accessing the parent property on the transform. Once it has a reference to the arena GameObject, it calls GetComponent for a reference to the animator.

The above code works because it assumes the caller is a child of BobbleArena. It would fail if the caller were moved to a different GameObject.

Next add the following before the closing brace:

```
void OnTriggerEnter(Collider other)
{
    renaAnimator.SetBool("IsLowered", true);
}
```

When the trigger is activated, the code sets IsLowered to true. You do do this by calling SetBool().

> Note: There are similar methods for other types. For example, for a float, you'd use SetFloat().

Now you need to logic raise the walls. Add the following:

```
void OnTriggerExit(Collider other)
{
    renaAnimator.SetBool("IsLowered", false);
}
```

When the hero leaves the trigger, this code tells the Animator to set IsLowered to false to raise the walls.

There's one outstanding detail for this script. Currently, any GameObject that enters the trigger lowers the walls. You need a filter so it only applies to the space marine.

Save the file and go back to Unity. With WallTrigger still selected, assign it the Wall layer. Navigate to Edit -> Project -> Settings -> Physics.

Uncheck all the checkboxes in the Wall row. In the Wall column, uncheck Alien Head, Bullet, Column and Floor.