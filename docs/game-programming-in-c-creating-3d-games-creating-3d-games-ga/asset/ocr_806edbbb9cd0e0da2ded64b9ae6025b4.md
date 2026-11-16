![](bbox=[0.196, 0.086, 0.679, 0.386])

# Figure 10.13 AABB intervals along the x-axis

Listing 10.17 gives the code for the sweep-and-prune method along the x-axis. You first sort the vector of boxes by their minimum x-value. Then, for every box, you grab the maximum x value and save it in max. In the inner loop, you only consider boxes whose min.x is less than max. Once the inner loop hits the first box with a min.x greater than max, there are no other boxes that overlap along the x-axis with the outer loop box. This means there are no other possible intersections against the outer loop box, so you break to the next iteration of the outer loop.

# Listing 10.17 PhysWorld::TestSweepAndPrune Implementation

Click here to view code image

```
void PhysWorld::TestSweepAndPrune(std::function<void
```