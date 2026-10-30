![](bbox=[0.22, 0.12, 0.78, 0.55])

Figure 26.3: Traffic deadlock in a city

of them to become empty. This will happen if the cars in the right road can move down. But these can move down if the cars in the bottom road can move left. These in turn will move left only if the cars in the left road can move. But these are blocked because of the cars in the top row. The net result: no one can move. Deadlock.

A deadlock is possible on a circular taxiway if every segment contains a plane which wants to move forward. In our airport it would seem that the taxiways do not form a circular path. However we have to be careful in implementing the half-runway-exclusion rule.

It turns out that deadlocks will not arise because we observe the following discipline in reserving halfRW. A landing aircraft must first reserve the landing runway and only then halfRW. Similarly a plane taking off must first reserve the takeoff runway and only then halfRW. You can see that this is a good strategy: halfRW being a precious resource must be reserved last. If a plane reserves halfRW and cannot reserve the landing runway, then it prevents take offs unnecessarily until such time as it reserves the landing runway. More formally, as the exercise asks you, you should be able to prove that if this policy is used there can be no deadlock. On the other hand, if landing planes as well as planes taking off reserve halfRW first, then it is possible to create a deadlock by carefully constructing the arrival sequence of the planes. The exercises invite you to explore this possibility.

# 26.8 Concluding remarks

There are many ways in which we could have designed this program. For example, note that the class ATC does not contain any interesting data members. Thus you might choose not