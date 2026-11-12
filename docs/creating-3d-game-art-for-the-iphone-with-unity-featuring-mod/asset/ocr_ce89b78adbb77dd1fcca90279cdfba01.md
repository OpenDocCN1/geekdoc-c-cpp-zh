![](bbox=[0.04, 0.1, 0.67, 0.52])

FIG 4.20 This Is the Final Map I Created for the Sky, Which Doesn't Waste Any Texture Space.

# Creating the Trash Heap

Next, I'd like to talk about the heaps of trash surrounding the level. The trash heap is also very basic in terms of modeling. The process for creating the geometry was to simply create a mountain from as few polygons as possible. Again, I will use a max-smoothing angle to remove the facets in the polygons. This item will target a different texture atlas than the level. For this model, the UV layout was the key to creating a successful look. To create the UV map, I cut the UVs down into sections. I made sure that each section was proportional to each other so the texture would be a consistent size across the mesh. The UVs were overlapped and placed in the upper area of the 0-1 space. The bottom half is reserved for the target object that will be discussed in Chapter 7.

I used Luxology's ImageSynth 2.0 program to create all of the seamless textures for my maps. I went to CG Textures and downloaded several junk and trash yard photos, and using ImageSynth, I compiled a seamless texture that was used for mapping the geometry.

In Fig. 4.21, you can see the completed trash heap model. Notice that the trash heap texture uses a seamless texture in the top half of the texture atlas.