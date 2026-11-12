![](bbox=[0.09, 0.11, 0.49, 0.36])

![](bbox=[0.52, 0.1, 0.94, 0.31])

be very accurate for collisions, but also very expensive depending on the mesh. In Fig. 9.8, you can see that a Mesh Collider is added to the level sections.

In my case, the Mesh Collider will work fine since the level sections are very basic with a lower poly count. However, on a more complex level model with a higher poly count, you'll want to use a more optimized Collider such as the Box Collider. Physics runs on the CPU so you'll need to

![](bbox=[0.09, 0.57, 0.51, 0.9])

use the Internal Profiler as we'll discuss later, to find possible bottlenecks and to see if the game is CPU bound, meaning expensive on the CPU. However, you can't just add a Box Collider to the section as it won't compensate for the ground and walls, but instead just make the entire section a Collider as shown in Fig. 9.9.

Instead, in your 3D program, you can create a collision object that fits the area your level occupies, but it is much lower in resolution in which you can then safely apply the Mesh Collider. Again, this wasn't needed in my case, so we'll take a look at one of the Penelope tutorial assets that is available in the Resources section at Unity3d. com. In Fig. 9.10, you can see that the level mesh for the Penelope game is more complex and just using a Mesh Collider on this geometry could cause an unnecessary performance hit. Instead, a lower resolution collision object was created in order to optimize the performance of the Mesh Collider.