
![](img/d3e3fa4010906e98ec76be003a6e31c2_87_0.png)

**FIG 4.2** Fence Areas Are Closed off to Player but Give the Illusion There's More to the Level.

I was a bit cautious of this because I know that the iPad and iPhone 4 can suffer from fill-rate issues, especially when filling the screen with a transparent polygon. So, I asked the question, “Can this reasonably be accomplished?” Later in this chapter, we’ll talk about how I tested this scenario, but for now, you can see the situations like this you need to address up front. It’s much easier to decide to drop the fences in the design phase and go another route versus having to scrap a model and start over due to performance issues. Always address the style issues up-front, in the design phase of your level, by asking the important question, “Can this reasonably be accomplished?”

## Breaking Down into Sections

So, we’ve talked about style, and in this section, we’ll start to really address the design of the level in terms of optimization. It’s always a good idea to break your level down into sections as shown in Fig. 4.3.

There are several advantages to breaking the level geometry down into sections, which I’ve organized into three categories: Puzzle Building, Lazy Loading, and Optimize Batching.

### Puzzle Building

Breaking the level design into sections gives us the opportunity to create seamless tiles or puzzle-like pieces of geometry that can be used to build a level in any number of configurations as shown in Fig. 4.4.

![](img/d3e3fa4010906e98ec76be003a6e31c2_88_0.png)

**FIG 4.3** Here the Level Is Divided into Sections.

Now, for the level showcased in this book, I didn't go as far with the level tiles as to make them totally seamless, as it wasn't necessary for my overall design, but it's an important technique to mention. However, the sections of levels I did create can be configured somewhat differently than my original layout. With Unity iOS, we now have the ability to work with mesh tiles from within the application. By using the new Vertex Snapping feature, we can simply and accurately snap tiles together by holding down the V key, hovering the mouse pointer over a desired vertex, and left-click and drag to snap the mesh to a vertex on another tile as shown in Fig. 4.5. Vertex Snapping in Unity iOS ensures that both meshes are "snapped" precisely together and can be used to quickly connect several mesh tiles to create a level within the application.

As you can see, creating mesh tiles and using Vertex Snapping in Unity iOS is a very effective way to build a level. We'll discuss the entire process later in the "Building on the Grid" section.

### Lazy Loading

Breaking the level down into sections also gives us the ability to optimize large levels by using what is referred to as lazy loading, which is the process of deferring the initialization of an object until it's absolutely needed. For instance, let's say we have a large level broken into four sections. In your game logic, you can create a methodology for loading one of the next sections when the player has reached a goal position. By the same token, you can unload a section once the player has also reached a goal position.

![](img/d3e3fa4010906e98ec76be003a6e31c2_89_0.png)

**FIG 4.4** The Level Can Be Broken Down into Smaller Tileable Elements.

For instance, you could set up a blockade, which controls how much the player is allowed to backtrack in a level. Once the player has reached a certain position, you can safely unload the section. Now, discussing the implementation of this procedure is beyond the scope of this book, but it's important to understand the advantages to breaking the level down into sections in terms of loading. For this method, each section is saved as a separate FBX file that can be loaded when needed. Also, with each section exported as a separate file, you can implement an asset downloading mechanism to your game so that the player can use in-app purchases.

### Optimize Batching and Rendering

As we discussed in Chapter 1, batching is extremely important for optimizing your game's performance, and special care needs to be taken to make sure that your meshes can and will be able to batch. By breaking the level into sections, you gain two advantages in terms of rendering vertices. First, it will be easier to stay within the 300-vertex limit that is a restriction of Dynamic Batching, and second, you further optimize the amount of vertices sent to the GPU in regards to the camera's view frustum.

![](img/d3e3fa4010906e98ec76be003a6e31c2_90_0.png)

**FIG 4.5** Vertex Snapping is Great for Ensuring Meshes Are Perfectly Aligned.

## Batching Revisited

In Chapter 1, we took a technical look at both Dynamic and Static Batching. Let's now take a more practical look at Static Batching as it pertains to creating a level. I mentioned earlier that creating our level in sections would further optimize the amount of vertices sent to the GPU. As we mentioned in Chapter 1, with Static Batching, vertices are stored in an indexed vertex buffer, which contains less data for the CPU to deal with and is thus faster than Dynamic Batching. However, we then have the caveat of not being able to transform the vertices. Static Batching creates a shared mesh. These items are not combined. They remain separate, but all of the vertices are added to an indexed vertex buffer, which is the vital aspect of Static Batching in terms of how you create your objects. Let's take a look at an example. In Fig. 4.6, I combined two sections from a level into one in modo and added a third section to the scene in Unity iOS so that we have two meshes to be rendered. You can also see that the camera's view is only showing half of the level. Because I've marked all of the meshes as Static and adhered to the rules of creating a batch, the meshes will be batched into one draw call. However, our job toward optimization isn't done. We not only have to think about the draw call, but the camera view frustum and how it relates to the amount of vertices being stored in the indexed vertex buffer for Static Batching as well.

![](img/d3e3fa4010906e98ec76be003a6e31c2_91_0.png)

**FIG 4.6** This Image Shows that even though the Camera Doesn't See the Mesh Behind it, the Verts Are Still Sent to the GPU.

I mentioned that only half of the level is being viewed. However, since the meshes for sections 1 and 2 have been combined in modo, the camera's view frustum is still within the bounding box for that mesh, and all of the vertices are being sent to the GPU even though most of them aren't being rendered, i.e., everything behind the camera. Now, in Fig. 4.7, I have properly divided the level into sections, and now, the camera's view frustum isn't overlapping the bounding box for section 1 and thus those vertices aren't being sent to the GPU. As you can see in Fig. 4.7, the vertex count has been drastically lowered to 96 verts down from 144. By breaking the level into sections, we were not only able to batch the meshes but also further minimize the amount of vertices sent to the GPU.

![](img/d3e3fa4010906e98ec76be003a6e31c2_92_0.png)

**FIG 4.7** Using Sections, the Vertex Count Is Dramatically Reduced.

The question now becomes, "How do you know where to divide up the level?" Well, in terms of optimization, it's quite simple. All you need to do is think about the widest area of the level that's going to be seen by the player at a given time. For instance, in Fig. 4.8, you can see how I decided on a proper division for sections 1 and 2 of the level due to the player having to move down the hall and turn left in order to see more of the level. The goal is to visualize your level and decide what areas will be visible to the camera's view frustum at a given time. The Occlusion Culling tools in Unity iOS will provide a similar optimization, but it's an Advanced License feature. Also, in order to properly use Occlusion Culling, you'll need to have your geometry broken into sensibly sized pieces as we've discussed in this chapter. So by following these principles of dividing up the level, you'll also be creating the correct geometry for using Occlusion Culling if you upgrade to or already have the Advanced License.

When building any objects for Unity iOS and the iDevices, I adopt the mantra, "Build to Batch." When creating your own content, you should always stick to this important concept in order to keep your mind focused on building optimized content.

> *The goal is to visualize your level and decide what areas will be visible to the camera's view frustum at a given time.*
