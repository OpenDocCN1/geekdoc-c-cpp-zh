# Chapter 31

# Spatial Trees

+   31.1  Spatial Data and Grids ......................................................... 777
+   31.2  Quadtrees and Octrees ........................................................... 782
+   31.3  kD-Trees ....................................................................... 785
+   31.4  Efficient Bouncing Balls ....................................................... 789
+   31.5  End of Chapter Material ....................................................... 789
+       31.5.1  Summary of Concepts ...................................................... 789
+       31.5.2  Exercises ................................................................ 790
+       31.5.3  Projects ................................................................. 790

A lot of the data that you deal with in certain fields of computing is spatial. There are certain data structures that you can use to make the process of finding elements in certain parts of space more efficient. These spatial data structures can increase the speed of certain operations dramatically, especially when there are large numbers of elements involved. This chapter will consider a few of the many options for doing this.

# 31.1  Spatial Data and Grids

Examples of spatial data can be bodies in a physics simulation or characters spread out across a large world in a game. The way these bodies or agents behave is generally influenced by the other things that are near them. This makes the problem of finding nearby neighbors an important one. To illustrate the nature of this problem, let us consider a simplified example. You are given N points in some M dimensional space. For visualization purposes, we will typically treat M = 2, but it could be higher. We want to find all pairs of points (p1, p2) such that the distance between them is less than a given threshold, |p2 − p1| < T.

The easiest-to-write solution to this problem is a brute force approach that runs through all particles in one loop, with a nested loop that runs through all the particles after that one in the sequence and calculates and compares distances. If we model the points as anything that can be converted to Int => Double we can write a class that serves as the interface for all the approaches to basic neighbor visits that we will write.

```
package scalabook.adt
```

```
abstract class NeighborVisitor[A <% Int => Double](val dim:Int) {
  def visitAllNeighbors(tDist:Double, visit:(A,A) => Unit)
  def visitNeighbors(i:Int, tDist:Double, visit:(A,A) => Unit)
```

1 This is written as a class instead of a trait to keep the code simpler. The <% symbol gets expanded out to include an implicit argument. As traits can not take arguments, we would have to get into the more complex details of this in order to use a trait. See appendix B for details.