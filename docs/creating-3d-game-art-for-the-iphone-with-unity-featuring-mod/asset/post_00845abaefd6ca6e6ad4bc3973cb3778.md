
triangles to reduce the amount of geometry at the elbow joint and hand as outlined in red.

Taking a look at Tater's torso, you can also see how terminating edge loops with triangles as shown in Fig. 2.19 controlled resolution differences from the pants to the torso. Adding edge loops to your mesh can be vital to adding detail. For instance, as shown in Fig. 2.19, Tater's pants needed an extra edge loop to keep the roundest form, however, I would have wasted vertices if I would have continued that loop up the torso and through the head.

![](img/d3e3fa4010906e98ec76be003a6e31c2_55_0.png)

FIG 2.19 You Need to Try and Terminate Edge Loops so that They Only Remain Detail in the Areas of the Mesh in Which They're Needed. Don't Allow Edge Loops to Carry Across the Entire Mesh.

Building on the concept of terminating edge loops, in Fig. 2.20, you can see how I handled a five-point polygon on Thumper's barrel. Instead of continuing the edge loop down the barrel of the gun, which is represented by the dashed blue line, I carried it up over the top and back around as shown by the yellow line. By doing this, I split the five-point polygon into a triangle and a quad polygon.

![](img/d3e3fa4010906e98ec76be003a6e31c2_55_1.png)

FIG 2.20 Here I Choose to Split a Five-Point Polygon to Create a Triangle and Quad Polygon while Terminating an Edge Loop.

In Fig. 2.21, you can see Tater with the edge loops selected that I determined to be the most important areas of the mesh. These selected areas are the parts that will be deformed the most when Tater is rigged and animated and are the areas that I paid particular attention to.

![](img/d3e3fa4010906e98ec76be003a6e31c2_56_0.png)

Fig 2.21: The Selected Edge Loops Are the Areas of Most Importance in Terms of where the Mesh Will Be Deformed During Animation.

## Reducing Geometry

Thus far, we've discussed creating geometry in the sense of how to control resolution by placing detail only in the important parts of the model. We talked about reducing geometry by terminating edge loops and using triangles to move from higher to lower resolutions. In this section, we'll take a look at some techniques that can be used to reduce geometry when optimizing your models.

### Polygon Flow and Spin Quads

It is very important to pay close attention to polygon flow on your model. It's particularly important when your model will be animated as a skinned mesh.

### Topology Is Key

The topology of your mesh will give you clues as to where you need to concentrate a bulk of your vertex count. You need to be sure to provide enough resolution in the areas of your mesh that will be deformed when animated.

You need to be sure that the topology of your mesh is designed to handle the animation. In Fig. 2.22, you can see how the polygons were arranged to flow from the top of the shoulders across the chest and around the shoulders and biceps. The topology of the chest and shoulders allows for smooth movement in these areas and will deform well when Tater is animated.

![](img/d3e3fa4010906e98ec76be003a6e31c2_57_0.png)

FIG 2.22 The Topology of Your Meshes Are Very Important, and You Need to Be Sure to Add Enough Detail to Allow the Area to Deform Well when Animated.

I use the Spin Quads tool often when working out my topology for my mesh. The Spin Quads tool is great for changing the flow of polygons. For example, in Fig. 2.23, you can see how I used Spin Quads to change the topology of Tater's shoulder and neck.

![](img/d3e3fa4010906e98ec76be003a6e31c2_57_1.png)

FIG 2.23 Spin Quads Was Used to Change the Topology of the Mesh

them to create a single quad. This isn't so much of a reducing technique as quad polygons are made from two triangles, but it makes the mesh much cleaner and easier to work with.

## Summary

In this chapter, we discussed the principles behind creating optimized geometry for the iDevices. The real trick to creating optimized geometry is deciding how to utilize the amount of vertices you have in your budget. You have to decide where important parts of the model are to place resolution and then reduce these polygons to be able to connect them to areas with less resolution. By understanding how the vertex count is interpreted by the GPU, you can properly gauge the amount of vertices your mesh contains. As we've discussed, mesh seams and UV borders will cause the GPU to split vertices and thus increase vertex count, and by understanding this principle, you'll be able to optimize these discontinuities in your mesh. In Chapter 3, "Understanding Textures and UV Maps," we'll take a look at texturing Tater and Thumper and continue to discuss how UV seams affect the true vertex count of your game objects.

## Planning Your UV Maps

Depending on your object, you are going to have to create a few UV seams, and as I stated above, the trick is to minimize these seams to as few as possible, yet still have the layout make sense for texturing. Let's look at an example. In the top half of Fig. 3.1, you can see a default model box with the UV seams highlighted. As you can see, the UV layout from the default box allows you to easily texture the sides of the box. In the lower half of Fig. 3.1, you can see that the UV layout has overlapping UVs in such a way that there are no seams. Now, the difference between these UV layouts besides ease of texturing and texture distortion is increased vertex count due to UV seams.

**FIG 3.1** Here You Can See the Default Model Box with Two Different UV Layouts. The First UV Map Has UV Seams, and the Second UV Map Has No Seams.

![](img/d3e3fa4010906e98ec76be003a6e31c2_61_0.png)

In Fig. 3.2, you can see how these UV layouts affect the vertex count in Unity iOS. Notice that the UV map without seams coupled with the object having no hard edges due to an increased smoothing angle yields the same vertex count of eight vertices between both Unity iOS and Modo. Although the default UV layout increases the vertex count from 8 to 14 as shown in the first half of Fig. 3.2, it still provides the better solution in that the object can be properly textured without distortion. Yes, it is possible to use an increased smoothing angle and eliminate all UV seams, which will not cause the GPU to split vertices as shown in the second half of Fig. 3.2, but this is not always a practical solution in terms of texturing.

![](img/d3e3fa4010906e98ec76be003a6e31c2_62_0.png)

**FIG 3.2** By creating UVs without seams, you can stop the GPU from splitting vertices, yet this may not be the best solution.

![](img/d3e3fa4010906e98ec76be003a6e31c2_62_1.png)

**FIG 3.3** When creating UVs for safety, my goal was to minimize seams as much as possible while removing texture distortion and creating a UV map that was best suited for texturing.

With this in mind, you have to be aware of each UV seam that you place in your map since it will cause an increase in vertex count. UV seams are inevitable, but you can control and limit them in your UV layout by combining UVs. It's vital to plan your UV layouts to accomplish this task. You not only have to be aware of UV seams, but you must also work to maximize the UV space. You need to arrange the most important areas of your mesh to utilize most of the 0-1 UV space, which in turn allocates more pixels in the texture map. For example, with a character, you might decide that the head is more important in terms of pixel resolution than say the character's hands. This decision would lead you to lay out the head UVs to take up more of the 0-1 UV space and thus allocate more texture resolution in the map. It also helps to keep in mind areas of your object that may not be easily seen by the camera. If you can't really see it, then there's no reason to waste UV space on it. Let's look at some examples using Tater and Thumper.

### Creating UVs for Tater

Once the Tater model was complete, I took a survey of the mesh and made notes on the areas that I wanted to be sure to give the most precedence in terms of texture resolution. In Fig. 3.3, you can see the completed UV layout for Tater.

In Tater's case, I felt that most of the model was equally important. However, I decided that I would give the head, arms, and torso a little more UV space than the pants, legs, and shoes. The legs and shoes received the least amount of UV space since I decided that they wouldn't be as visible in game as the rest of the model. These decisions concluded my first steps in planning my UV map for Tater. By breaking the model down into sections of importance, I determined how to divide the UVs into separate UV shells or islands.

Let's take a look at creating UVs for the shirt. I needed to create a UV layout for the shirt that would allow me to easily create a texture map, and at the same time, minimize any texture distortion. First, I created an initial projection, by using the Project from View tool with the viewport set to Front view as shown in Fig. 3.4.

FIG 3.4 In the Case of the Shirt, I Created an Initial Planar Projection to Get Me in the "ballpark" for My Planned UV Layout.

![](img/d3e3fa4010906e98ec76be003a6e31c2_63_0.png)
