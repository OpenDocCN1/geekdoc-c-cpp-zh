At the end of 500 ms, if the resource is still owned, the executive attempts to prevent CPU starvation by acquiring the dispatcher lock, boosting the owning thread or threads to 15 (if the original owner priority is less than the waiter's and not 15), resetting their quantums, and performing another await.

Because resources can be either shared or exclusive, the kernel boosts the exclusive owner and checks for shared owners and boosts all of them. When the waiting thread enters the wait state again, the hope is that the scheduler will schedule one of the owners, which will have enough time to complete its work and release the resource. Note that this boosting mechanism is used only if the resource doesn't have the Boost flag, developers can choose to set if the priority-in mechanism described here works well with their usage of the resource.

Additionally, this mechanism isn't perfect. For example, if the resource has multiple shared owners, the execute boosts all threads to priority 15. This results in a surge of high-priority threads on the system, with all full quantums. Although the initial owner will run first (because it was the first to be boosted and therefore is first on the ready list), the other shared owners will run next because the waiting's priority was not boosted. After all the shared owners have had a chance to acquire it and their priority has been decreased while waiting the waiting will finally get to acquire the resource. Because shared owners can promote or convert their ownership from shared to exclusive as soon as the exclusive releases the resource, it's possible for this mechanism not to work as intended.

# Priority boosts for foreground threads awaits

As will be described shortly, whenever a thread in the foreground process completes a wait operation on a kernel object, the kernel boosts its current (not base) priority by the current value of PrioritySepar (The winding system is responsible for determining which process is considered to be in the foreground.) As described earlier in this chapter in the section "Controlling the quantum," Priorityation reflects the quantum-table index used to select quantums for the threads of foreground applications. However, in this case, it is being used as a priority boost.

The reason for this boost is to improve the responsiveness of interactive applications. By giving the foreground application a small boost when it completes a wait, it has a better chance of running right away, especially when other processes at the same base priority might be running in the background.

EXPERIMENT: Watching foreground priority boosts and decays
Using the CPU tool, you can watch priority boosts in action. Take the following steps:

+   1. Open the System utility in Control Panel or right-click the This Computer icon on the desktop and choose Properties.
2. Click the Advanced System Settings, click the Advanced tab, click the Settings button in the Performance section, and click the Advanced tab.
3. Select the Programs option. This gives PrioritySeparation a value of 2.