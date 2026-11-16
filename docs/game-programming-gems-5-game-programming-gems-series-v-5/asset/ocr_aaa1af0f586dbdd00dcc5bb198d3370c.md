# # 2.5 Dimensional Impostors for Realistic Trees and Forests

Gábor Szíjártó, Technical University of Budapest
szijarto.gabor@freemail.hu

One of the major challenges in developing techniques for realistic and high-performance visualization of outdoor environments is the rendering of vegetation. Convincing modeling of trees and bushes requires a very large number of polygons that exceed the limits posed by the current rendering hardware. A number of methods have been proposed in the past to address the issue, most of which are variants of multiresolution modeling and level-of-detail algorithms.

In this gem, a 2.5 dimension impostor based method [Szijarto03] is developed for high-resolution tree rendering, which uses the structure of conventional trees. Moreover, it takes advantage of the programmable rendering pipelines available on the recent video cards. The algorithm uses view-dependent 2.5 dimensional impostors to visualize convincing trees in most levels of detail. Due to the use of impostors, the performance depends heavily on the fill rate of the video card.

# ## Introduction

It is often useful to define specific scales of simulation at which a vegetation-rendering algorithm should provide the required level of realism. Most applications can be assigned to one or more of the following categories:

+   - Insect scale: The level of simulation where a consistent, realistic depiction of individual branches and leaves is expected. (The avatar can climb the tree.)
+   - Human scale: Scenes must look realistic at distances ranging from an arm’s reach to some tens of meters away. Consistency is desired but not required. (The avatar can bump into trees, even dash through bushes, but does not focus on specific details.)