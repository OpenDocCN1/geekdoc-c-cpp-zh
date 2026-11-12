FIGURE 2.2 More polygons means more places to bend. This allows for more rounded forms, but it requires a bigger data set.

![](bbox=[0.321, 0.107, 0.899, 0.341])

constructing forms of assembling polygons. Some methods are derived from curves; others work along the line of creating polygons directly. But at the end of the process, all the methods' results are turned into triangles by a process called **tessellation**, so that the engine can see them and the video card can draw them.

# Rendering

This drawing of polygons and the textures and lighting associated with them is called **rendering**. There are two kinds of rendering: software and hardware rendering. Software rendering is what is commonly used in television and film projects. The scene is built within a 3D application including lights and textures, and then the CPU is engaged to draw the complex interaction of the objects, colors, and lights in the scene. Because the results are displayed later (not in real time), if it takes a second for a frame to be rendered, or a minute, or even an hour per frame, this is acceptable. The sequential stills that are the output of this process are put together via a video editing package, and watched as a moving image.

Hardware rendering is much different. Games are in this category because the video card renders the polygons within the digital space to represent 3D space. The hardware draws what is on the screen (including all the objects, textures, and light) and needs to do so at as many times per second. Generally, if players are getting much below 30 frames per second, they notice the choppiness of the game.

So how does a computer draw 30 frames per second of one project, but one frame every 30 minutes of another? The answer is simply the size of the data set and the hardware dedicated to handle that set. For projects that will not be rendered in real time, the amount of data can be much higher. The number of polygons can be much more, the size and number of textures bigger, and the complex calculations of light more sophisticated. In real-time situations (hardware rendering, with dedicated hardware chugging away on this data set), the amount of data the video card deals with is much, much smaller.