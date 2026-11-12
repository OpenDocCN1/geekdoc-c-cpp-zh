"Understanding Textures and UV Maps," we'll continue this discussion with a look at creating UV maps and texturing.

# ## My Workflow

I stated earlier that I wanted to keep the vertex count for Tater to less than 800 vertices. For Thumper, I wanted to keep its vertex count below 300 vertices. In the end, I was able to get Tater to 659 vertices and Thumper to 224 vertices. This gives me a combined count for the "hero" character and his weapon at 883 vertices. For this character, I didn't create a high-resolution mesh and then build a low-resolution version cage from it. This is a typical workflow in games as you can extrapolate a normal map from the high-resolution mesh. Instead, I went with a modified approach in that I began creating a low-resolution polygon cage and then optimized the mesh by adding geometry to detail areas of detail and reducing geometry once the base mesh was completed. As I worked on the base mesh, I used a combination of the Loop Slice and Edge Slice tools to quickly add and control edge loops on the mesh. I also tried to use quad polygons as much as possible and use triangles only in certain areas where I wanted to reduce geometry. For instance, in Fig. 2.15, I used a triangle in Tater's forearm to go from higher resolution level around the bicep to a lower resolution level around the wrist.

![](bbox=[0.035, 0.512, 0.653, 0.813])

**FIG 2.15** Here a Triangle Was Used to Reduce the Level of Detail from the Bicep to the Wrist.

When Unity iOS imports the FBX file, it will automatically be tripled, so there's no need to triple the polygons within modo.