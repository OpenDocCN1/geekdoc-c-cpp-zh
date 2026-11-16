
## Chapter 3: Volumetric Representation of Virtual Environments

*David Williams*
**Thermite3D**

### 3.1 Introduction

The use of height maps as a mechanism for representing terrains is well established within computer graphics and gaming. Height maps are a conceptually simple representation, easy to visualize, and simple to create. Furthermore, there is a large body of research [19] into the manipulation and rendering of such data. However, there are also serious limitations that result from this rather simplistic representation, such as the inability to support caves and overhangs.

In this article, we take the concept of two-dimensional height maps and show how they can be extended to fully three-dimensional volumes. This is a representation that naturally and consistently handles the kind of geological structures mentioned previously. It also allows easy real-time modification, and as such can be used to create powerful terrain editors or unique game play opportunities.

To this end, the concept of volumetric environments has been successfully employed in several commercial games to date. The game Worms 3D found it to be an appropriate way to bring the highly destructive but two-dimensional levels from the earlier Worms games into the third dimension [1]. The Crysis sandbox editor utilized voxels during terrain modeling, and these were turned into traditional static meshes for runtime use. And the upcoming game MinerWars uses the concept to allow players to dig through asteroids in real time.

Throughout this article we will consider the modeling and rendering of complex terrains to be the main application of the described technology. Nevertheless, we do believe the technology can have direct application to manmade or otherwise artificial environments if appropriate game play mechanics and artistic styles are in place. In fact, the use of voxels for non-terrain environments has been a core research area of our own experimental Thermite3D game engine [15], upon which this gem is largely based.

Figure 3.1 shows a variety of environments that are represented using the volumetric approach described in this article.

![](img/7ba1225bb0e5a87be0fd35866408ffa7_81_0.png)

**Figure 3.1:** Volumetric representations can be used for many different types of environments. In (a) we see a complex terrain with two primary levels and numerous overhangs [5]. (_Image courtesy of Thomas Schöps._) The Earth in (b) has been cut away to illustrate that the interior is also modeled [15]. Manmade structures with many different materials (c) can also be represented [15], while (d) shows a mining ship inside an asteroid, destroying it in real time [8]. (_Image courtesy of Keen Software House._)

[1] Although based on the concepts described in this article, _Worms_ actually uses a much lower resolution volume than that which we present here but allows for lattice deformations to achieve their desired artistic style.

### 3.2 Overview

The core data structure within our system is that of the volume. A volume is a regular three-dimensional grid of values, each of which is known as a voxel. Conceptually, this is analogous to the way a bitmap image is a regular two-dimensional grid of pixels. It is also possible to think of a volume as consisting of a number of two-dimensional slices stacked on top of each other. This is shown in Figure 3.2(a). We define the concept of a cell as being a group of eight neighboring voxels that form a cube, again as illustrated in Figure 3.2(b).

![](img/7ba1225bb0e5a87be0fd35866408ffa7_82_0.png)

**Figure 3.2:** (a) This volume consists of an 8x8x8 grid of voxels, though real volumes are considerably larger. The corner is cut away to show how voxels also model the interior of an object. (b) Each group of 2x2x2 voxels forms a cell. Note that voxels and volumes are the only types that are stored explicitly within our system, as edges and cells are implicit constructs that we build by looking at a voxel's neighbors.

The volume is sized and positioned so as to cover the entire virtual environment that we wish to represent. Each voxel then encodes a representation of what exists at its location. The exact data that constitutes a voxel will be discussed shortly, but for now it can be considered to be a single bit indicating whether that location is solid material or empty space. Naturally this representation is very easy to modify in real time, because adding or removing material simply becomes a case of setting the values of the voxels. This is significantly easier than the complex CSG operations that might be required for other representations.

While the direct rendering of such volumes is an active research area [12], modern GPU hardware is highly tuned to the efficient rendering of triangle meshes. Therefore, although the volumetric representation is very useful for editing and deforming the environment, it is desirable to transform it into a triangle mesh for the purpose of visualization.

This process is known as surface extraction, and there are a number of algorithms that are able to perform it. The Marching Cubes algorithm [7] is one of the earliest and most widely used—it is popular due to its simplicity, speed of execution, and good locality of reference. Further developments have addressed ambiguities in the original algorithm, worked around (now expired) patent issues, or provided adaptive triangulation.

The Marching Cubes algorithm operates on a single cell at a time. For each corner of the cell, it classifies the voxel as being either inside or outside of the surface according to its value. This gives 256 possible combinations which can be grouped into the 18 equivalence classes illustrated in Figure 3.3. Each class represents the set of rotationally symmetric cases, and some classes include inverses as well. The last three classes in Figure 3.3 are additions to the original Marching Cubes algorithm that must be used instead of the inverted triangles in order to avoid holes.

![](img/7ba1225bb0e5a87be0fd35866408ffa7_83_0.png)

**Figure 3.3:** The set of triangles generated by the Marching Cubes algorithm for each of the 18 possible cell configurations. The numbers indicate how many times each configuration occurs. Solid circles represent voxels containing solid material, while hollow circles represent voxels containing empty space. In most cases the inverse configuration generates the same set of triangles, with the exception of the last three cases (which are inverses of earlier cases but with different triangles to avoid holes).

A lookup table is used to map the combination of voxels to a particular set of triangles that locally represents the surface. This process is applied to every cell in the volume (though cells with identical voxel values generate no triangles and can be trivially skipped) in order to reconstruct the complete surface. We will not be describing this process in much detail as it is already well covered by existing literature and numerous implementations are available online.

### 3.3 Data Structures

Having developed an understanding of the core principles, it is now possible to think carefully about the data structures involved in our volumetric representation.

Although each voxel can be represented by a simple inside/outside bit as described previously, in practice this does not provide much flexibility. Instead, our engine stores an 8-bit *material ID* for each voxel. A value of 0 represents empty space, while each of the 255 non-zero values represents a different material (rock, soil, wood, etc.). Naturally each of these materials will have a different visual appearance, but it is possible to attach different physical properties to them as well (perhaps some cannot be destroyed in-game, for example). This material ID will later be passed down the graphics pipeline for use in shading calculations.

Additionally, the use of a simple in/out decision when classifying the corners of a cell tends to lead to a mesh with a very jagged appearance. Depending on the application (and certainly in the case of terrain) it can be useful to replace this binary volume with a *density field*. In this case we assign each voxel a numerical value and we define the surface of our environment to be the set of all points that have a particular *isovalue*. When running the Marching Cubes algorithm on a given cell we classify each corner as being above or below the isovalue, and use linear interpolation to position any resulting vertices at the correct location along the edge. [2]

Using a density field rather than a binary volume means more control is afforded over the shape of the mesh. By modifying the voxel values such that the isovalue is not exactly halfway between them, the resulting vertex can be pushed closer to one voxel or the other. The consequence of this is that the resulting mesh tends to be a lot smoother.
