of each node’s geometry. Adding actual geometry falls into two categories. Static geometry includes augmentations to the level geometry such as pillars or statues. These are items we may want to weld to the existing cell geometry. If so, we need to make sure the cell geometry is not being instanced by more than one node in the graph. If it is, we will need to create a separate version of the cell geometry before we weld any new geometry to the cell. Welding new geometric features also requires an update to the cell’s AABB tree and possibly the recalculation of portals. Nonstatic geometry can simply be added at the node level without welding.

# Conclusion

We have presented a process for generating procedural game levels to address the large amount of content required by growing game genres such as massively multiplayer online games. Given an appropriate set of rules, our algorithm provides amplification of a simple data structure into a complex geometric game level [Roden04]. Our process begins by generating a 3D graph with appropriate rules. Prefabricated 3D geometric level pieces are then mapped to nodes of our graph. Identical geometry is instanced instead of being copied, taking care to weld sub-cell prefabs into a single model to reduce the number of redundant vertices and save on rendering time. We then compute visibility and collision detection information for later use by our portal algorithm. Finally, we add level content such as static geometry and environmental audio.

The method presented should be considered as a foundation for the reader in building their own level generator. One important issue we have not touched upon is lighting. A procedure for adding realistic lighting would depend not only on the design but also on how the level generator is used. If levels are generated as a pre-process, lighting can be computed using pre-processing techniques, whereas for dynamically generated levels, a different set of lighting techniques would be employed.

# References

+   [Luebke95] Luebke, David and Chris Georges. “Portals and Mirrors: Simple, Fast Evaluation of Potentially Visible Sets.” In (Pat Hanrahan and Jim Winget, editors) ACM Symposium on Interactive 3D Graphics (April 1995): pp. 105–106.

+   [Perry02] Perry, Lee. “Modular Level and Component Design.” In Game Developer Magazine (November 2002): pp. 30–35.

+   [Roden04] Roden, Timothy, and Ian Parberry. “From Artistry to Automation: A Structured Methodology for Procedural Content Creation.” 3rd International Conference on Entertainment Computing (September 2004).

+   [Schroeder01] Schroeder, Tim. “Collision Detection Using Ray Casting.” In Game Developer Magazine (August 2001): pp. 50–56.