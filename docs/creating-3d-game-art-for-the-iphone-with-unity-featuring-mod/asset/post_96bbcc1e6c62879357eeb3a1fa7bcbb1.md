
optimization is to run smoothly, and the only way to achieve this is to make sure your content is optimized enough to maintain a constant frame rate. It is very detrimental for a game to constantly drop frame rate. The main area you'll focus on optimizing your game in terms of game art is through the following:

- 1. Lowering draw calls through batching objects.
- 2. Keeping the vertex count down per frame.
- 3. Compressing textures and reducing memory bandwidth through shared materials and texture atlases.
- 4. Using optimized shaders and not using alpha testing.

### Summary

This concludes our overall discussion of the iPhone and iPad hardware and how it relates to Unity iOS. I can't stress enough how vital it is to understand the platform you are working on. Now that we've discussed the hardware specifications and determined a game budget, we can begin actually building content and getting to work on a game. In Chapter 2, we'll begin taking a look at modeling Tater for the iPhone and iPad and Unity iOS.

![](img/d3e3fa4010906e98ec76be003a6e31c2_38_0.png)

## Creating Game Objects Using modo

### Tater and Thumper

In this chapter, we're going to take an in-depth look at creating a "hero" character and his main weapon. Now, I say the word "hero," but I don't mean it in the sense of the character having a heroic trait. Instead, what I am referring to is a game's main character or asset. It's the "hero" object that gets most of the attention in regards to polygon count and system resources. As we discussed in Chapter 1, "Getting to Know the iDevice Hardware and Unity iOS," when dealing with a mobile device such as the iPhone and iPad, you must always be aware of the limited resources available. Like an old miser, constantly counting every penny, you must watch over each vertex and make sure not a one goes to waste. Throughout this chapter, I'll be discussing techniques and principles behind creating optimized game models for the iDevices. To illustrate the concepts, we'll be looking at the process behind creating Tater and his trusty sidekick of mass destruction, Thumper, as shown in Fig. 2.1. We'll begin by discussing how to determine the project's polygon budget.

![](img/d3e3fa4010906e98ec76be003a6e31c2_39_0.png)

*FIG 2.1 Here You Can See Tater and Thumper, the Main Assets We'll Be Focusing on Throughout This Chapter.*

### Planning the Vertex Budget

**Tater's Weapon Load Out**

Go to the resource site to view the video walkthrough for this chapter.

We talked a lot in Chapter 1, “Getting to Know the iDevice Hardware and Unity iOS,” about the game budget. Part of working out a game budget is to come up with a budget for the amount of vertices your models will be made up of. The vertex budget is the process of deciding exactly how many vertices the objects that make up your scene contain and is shown per frame of the game loop, while still maintaining your game budget's frame rate. This is key to the modeling process because you can't model anything without knowing the limitations of the targeted device, your game's target frame rate and your overall vertex budget. You need to have a vertex count worked out before a single polygon is created in your 3D application. In Chapter 1, “Getting to Know the iDevice Hardware and Unity iOS,” we filled in the first piece of this puzzle by discussing the various hardware components found in the different iDevices in order to gain an understanding of its limitations and thus establish a baseline to follow in order to create optimized geometry for the iPhone and iPad. In the next section, we'll take a look at how you can go about determining your vertex budget.

### Testing Performance

So we've determined that planning the vertex budget is the first step before creating any actual geometry, but how is this budget actually determined? In game development, you'll hear the phrase, “it depends” quite often. Although it may sound like a quick answer to a complicated question, however, it's actually the truth. Determining a vertex budget or any budget in game development depends solely on your game. The type of game you're looking to create bears a lot of weight in regards to how you determine your vertex budget. For instance, if your game is heavy on rendering such as by utilizing lots of objects in the scene, then you'll need to cut back on physics simulations. But by that same token, a heavy physics-based game will demand more resources from CPU and thus call for smaller vertex counts and less objects in your scene in order to balance the overall performance of the game. It's a give and take, and the type of game you're creating will dictate this balance. This is why Chapter 1, “Getting to Know the iDevice Hardware and Unity iOS,” was dedicated to the iDevice hardware as understanding what the hardware is capable of and its limitations are vital when building your content.

#### Creating a Performance Test Scene

When you're in the early stages of developing your game, it can be extremely helpful to create a performance scene to test the capabilities of the hardware. For instance, for the book's game demo and coming from the perspective of a 3D artist, I wanted to concentrate on rendering the 3D assets. This was my primary goal, and I established early on that I wanted to spend the bulk of my timeframe spent rendering. I also decided that I wanted my game to maintain a frame rate of 30 fps. With this goal set, I created a demo scene that I could install on the iPhone and iPad in order to test the performance and see how far I could push the hardware.

The demo scene doesn't need to be complicated or doesn't need to look good. The purpose of this scene is to purely gauge performance. To save time, I went to the Unity iOS web site and downloaded the Penelope tutorial, which can be found at http://unity3d.com/support/resources/tutorials/penelope. The Penelope model looked close to the level of detail I was looking to create for Tater and would make for a good test model. I then opened up the Penelope completed project and deleted all of the assets except the model and the “PlayerRelativeSetup” scene. With this simple scene, I have a skinned mesh with animations and a default control setup to move the character around the scene as shown in Fig. 2.2.

Finally, I created a simple button and added a script that would instantiate a new instance of the Penelope model in the scene at the position of the playable character as well as display the overall vertex count for Penelope and her clones. By using the Penelope assets, I was able to quickly create a prototype scene for testing hardware performance without having to spend time creating objects. Once the game was compiled to an Xcode project, I could then run the game on a device while running the Internal Profiler to check performance as shown in Fig. 2.3.

While monitoring the Internal Profiler's frametime variable in Xcode's Console, I continued to press the “Add” button in the game to create more instances of the Penelope game object and thus increasing vertex count and skinned meshes. The vertex count is only accounting for the Penelope character and her instantiated clones. Also, the vertex count display is not accounting for

The Internal Profiler will show frame performance information every 30 frames with the frametime variable describing how long it took to render a frame measured in milliseconds. This means that if you take 1000 and divide it by your desired frame rate, which is 30, you get 33.3 ms. When testing performance, I would watch the frametime variable to see what value in milliseconds it was outputting. For example, if the frametime were indicating a value of 37 ms, I would then take 1000 and divide that by 37 to get 27.02 or 27 fps.

By knowing the vertex count of the Penelope model and making note of how many instances of Penelope I was able to add to the scene before it began to choke, I was able to get a good estimate of what the hardware could handle. This demo scene allowed me to see how many skinned meshes I could run at the same time as well as how many vertices I could render in the scene, which can be referred to as vertex throughput. Now, this is only a rough estimate of the scene's performance since I'm not taking into account script performance or physics used in an entire game. This performance scene can be used to derive a basic idea of what can be accomplished with the hardware in terms of vertex count.

In FIG 2.4, you can see the results I got from running my performance scene on an iPod Touch third generation.

![](img/d3e3fa4010906e98ec76be003a6e31c2_42_0.png)

FIGURE 2.4 I used the Internal Profiler to Monitor the Performance of the Demo Scene as I Continued to Add Game Objects in the Game. I Was Checking the frametime Variable to See If It Went Beyond 33.3 ms.
