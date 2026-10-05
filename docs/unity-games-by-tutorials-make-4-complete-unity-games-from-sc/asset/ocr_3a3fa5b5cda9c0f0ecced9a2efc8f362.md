```
return;
}
// 3
transform.LookAt(player);

// 4
agent.SetDestination(player.position);

// 5
if (Vector3.Distance(transform.position, player.position) < range
&& Time.time - timeLastFired > fireRate)
{
    // 6
    timeLastFired = Time.time;
    fire();
}

private void fire()
{
    Debug.Log("Fire");
}
```

Step-by-step, here's what this code is doing:

+   1. By default, all robots are alive. You set the agent and player values to the NavMesh Agent and Player components respectively.
2. Check if the robot is dead before continuing. There are no zombie robots in this game!
3. Make the robot face the player.
4. Tell the robot to use the NavMesh to find the player.
5. Check to see if the robot is within firing range and if's even enough time between shots to fire again.
6. Update timeLastFired to the current time and call Fire(), which simply logs a message to the console for the time.

You need to assign an appropriate tag to the Player GameObject so the robots can find it.

Save your script and switch back to Unity. Click the Player GameObject, and as you did before with the guns, click the Tag drop-down and select the Player tag.

Click Play; you'll see the robots move towards the player and the “Fire” log appear in the console.