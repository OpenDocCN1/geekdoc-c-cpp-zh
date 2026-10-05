# Unity Games by Tutorials

# Chapter 10: Adding Enemies

![](bbox=[0.292, 0.091, 0.706, 0.273])

Click Play and you'll see the robot's ball spin:

![](bbox=[0.346, 0.346, 0.653, 0.48])

Now, to add the firing animation. Select all three **RobotRampage_Bot** GameObjects and set their **Animator's** **Controller** to **Robot** by clicking the circle beside the **Controller** field and selecting **Robot:**

![](bbox=[0.346, 0.56, 0.653, 0.683])

Select each **RobotRampage_Bot** individually and click **Apply** on each one to apply the changes to the prefabs. Now, open the **Robot** script. Add the following instance:

```
public Animator robot;
```

Then update Fire() to the following:

```
private void fire()
{
    robot.Play("Fire");
}
```

raywenderlich.com

274