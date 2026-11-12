# # UV Mapping

UV mapping characters can be a daunting task. When UV mapping the level, we were generally working with fairly simple shapes that lent themselves easily to planar maps and cylindrical maps. The human form really is much more complex than that at first blush.

Fortunately, there have been some important tools that have emerged in the last few years that can assist in efficient and quickly created UV maps. Maya actually has some of my favorite UV editing tools; however applications like Modo have emerged with some really powerful UV tools that are much more efficient than Maya's. To make matters even more complicated, there are free tools like RoadKill (http://www.pullin-shapes.co.uk/page8.htm) that integrate fairly seamlessly with Maya that allow for some extraordinarily fast UV mapping using all the latest pelt/LCSM mapping technologies. If you do a lot of UV mapping, or plan to, learning one of these two tools may be in your best interest.

With all that said, Maya's UV mapping tools have done some catching up in recent versions, and many of the tools and techniques available in Modo and Roadkill are available in Maya as well. There are enough available that we will stick to Maya's tool set for this chapter's tutorials. Many of the techniques used for UV mapping the human form are similar to those used for mapping the level, so building upon the toolset you are already familiar with will move us along quickest.

# ## Tutorial 9.1: Character UV Mapping

In this tutorial we will be doing several things. First, Maya's UV tools are powerful, but sometimes require some very specifically created polygonal structure. Before we even start building UV maps, we will take a moment to make sure that the geometry built in the last chapter does indeed fit into these Maya-imposed requirements. The requirements actually are good to keep our eye out for (they are mostly concerned with the problems that arise from nonfour-sided polygons) since identifying and fixing them at this state will ultimately save time within Unity.

# ### Mesh Inspection and Cleanup

+   1. **Step 1:** Open Maya and set the project to Incursion-Maya.
+   2. **Step 2:** Open AegisChung.mb.
+   3. **Step 3:** Turn on Backface Culling. In the persp view panel, choose Shading>Backface Culling (Figure 9.1).

> > **Why?**
> >
> > Figure 9.1 shows the results of the last chapter with backface culling activated. It appears that the entire body has the normals facing the wrong way. If you are using the version of Aegis Chung that is included