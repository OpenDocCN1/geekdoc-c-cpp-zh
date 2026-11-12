![](bbox=[0.02, 0.11, 0.88, 0.44])

FIG 4.3 Here the Level Is Divided into Sections.

Now, for the level showcased in this book, I didn't go as far with the level tiles as to make them totally seamless, as it wasn't necessary for my overall design, but it's an important technique to mention. However, the sections of levels I did create can be configured somewhat differently than my original layout. With Unity iOS, we now have the ability to work with mesh tiles from within the application. By using the new Vertex Snapping feature, we can simply and accurately snap tiles together by holding down the V key, hovering the mouse pointer over a desired vertex, and left-click and dragging to snap the mesh to a vertex on another tile as shown in Fig. 4.5. Vertex Snapping in Unity iOS ensures that both meshes are "snapped" precisely together and can be used to quickly connect several mesh tiles to create a level within the application.

As you can see, creating mesh tiles and using Vertex Snapping in Unity iOS is a very effective way to build a level. We'll discuss the entire process later in the "Building on the Grid" section.

# Lazy Loading

Breaking the level down into sections also gives us the ability to optimize large levels by using what is referred to as lazy loading, which is the process of deferring the initialization of an object until it's absolutely needed. For instance, let's say we have a large level broken into four sections. In your game logic, you can create a methodology for loading one of the next sections when the player has reached a goal position. With that same token, you can unload a section once the player has also reached a goal position.