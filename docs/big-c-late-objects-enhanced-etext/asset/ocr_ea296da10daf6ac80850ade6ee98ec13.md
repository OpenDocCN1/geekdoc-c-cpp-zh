# WORKED EXAMPLE 2.1

# Computing Travel Time

In this example, we develop a hand calculation to compute the time that a robot requires to retrieve an item from rocky terrain.

# Problem Statement

A robot needs to retrieve an item that is located in rocky terrain adjacent to a road. The robot can travel at a faster speed on the road than on the rocky terrain, so it will want to do so for a certain distance before moving on a straight line to the item.

Your task is to compute the total time taken by the robot to reach its goal, given the following inputs:

+   - The distance between the robot and the item in the x- and y-direction (dx and dy)
+   - The speed of the robot on the road and the rocky terrain (s₁ and s₂)
+   - The length l₁ of the first segment (on the road)

![](bbox=[0.15, 0.15, 0.25, 0.25])

![](bbox=[0.8, 0.22, 0.95, 0.38])

Courtesy of NASA.

![](bbox=[0.7, 0.4, 0.95, 0.7])

To make the problem more concrete, let's assume the following dimensions:

![](bbox=[0.3, 0.7, 0.6, 0.95])

The total time is the time for traversing both segments. The time to traverse the first segment is simply the length of the segment divided by the speed: 6 km divided by 5 km/h, or 1.2 hours.