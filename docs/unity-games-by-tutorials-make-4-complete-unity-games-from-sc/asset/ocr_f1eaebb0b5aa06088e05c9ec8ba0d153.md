The hero will now react to each hit until the maximum number of hits. At that point, nothing will happen — but you'll fix that, next, in a dramatic way!

# Removing the bobblehead

There's nothing more terrifying to a bobblehead than losing its precious head. Your space marine is no different. It's only fitting that the head rolls off the body to make the game's end spectacular and undeniable.

Time for a little more scripting. Open PlayerController in your editor and add the following instances variable:

```
public RigidBody marineBody;
private bool isDead = false;
```

marineBody is, well, the marine's body. You're adding this because you'll make some physics alterations when the hero dies. And, of course, isDead keeps track of the player's current death state.

Together, they let the script know if the marine is dead.

Now you need a method that manages the death, so add the following:

```
public void Die() {
    bodyAnimator.SetBool("IsMoving", false);
    marineBody.transform.parent = null;
    marineBody.isKinematic = false;
    marineBody.useGravity = true;
    marineBody.gameObject.GetComponent<CapsuleCollider>().enabled = true;
    marineBody.gameObject.GetComponent<Gun>().enabled = false;
}
```

You set IsMoving to false since the marine is dead and you don't want a zombie running around. Next, set the parent to null to remove the current GameObject from its parent. Then, by enabling Use Gravity and disabling IsKinematic, the body will drop and roll, and you enable a collider to make this all work. The gun prevents the player from firing after death.

At this point, the head and body share a joint. You need to destroy the hinge joint to enable the hero's inevitable dismemberment.

Add the following code before the previous block:

```
Destroy(head.gameObject.GetComponent<HingeJoint>());
head.transform.parent = null;
```