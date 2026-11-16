
## 18.7 Results

The proposed methods have been implemented in DirectX/HLSL environment, and their performance has been measured on an Nvidia GeForce 8800 GTX GPU at 800×600 resolution. The rendering results of the harbor scene are shown in Figure 18.3. This scene can be rendered at 170 FPS if only directional light is computed. Taking 16 samples per pixel, the ambient occlusion and indirect lighting computation runs over 100 FPS. With 32 samples per pixel, the rendering speed drops to 60 FPS.

![](img/7ba1225bb0e5a87be0fd35866408ffa7_415_0.png)

**Figure 18.3:** (See also Color Plates.) Rendering results of the harbor scene— (First column) direct lighting, (second column) direct lighting plus ambient occlusion, and (third column) direct lighting plus ambient occlusion and indirect lighting.

## References

- [1] H. Landis."Production-ready global illumination". SIGGRAPH Course notes 16, 2002.
http://www.debevec.org/HDRI2004/landis-S2002-course16-proreadyGI.pdf

- [2] A. Iones, A. Krupkin, M. Sbert, and S. Zhukov."Fast realistic lighting for video games". IEEE Computer Graphics and Applications, Volume 23, Number 3 (May 2003), pp. 54–64.

- [3] A. Keller and W. Heidrich."Interleaved sampling". Rendering Techniques 2001 (Proceedings of the 12th Eurographics Workshop on Rendering), 2001, pp. 269–276.

- [4] A. Méndez, M. Sbert, and J. Catá."Real-time obscurances with color bleeding". SCCG ’03: Proceedings of the 19th Spring Conference on Computer Graphics, ACM, 2003, pp. 171–176.

- [5] M. Mittring."Finding next gen — CryEngine 2". Advanced Real-Time Rendering in 3D Graphics and Games course, SIGGRAPH 2007, pp. 97–121.

- [6] M. Pharr and S. Green."Ambient occlusion". GPU Gems, Addison-Wesley, 2004.

- [7] M. Powell and J. Swann."Weighted Uniform Sampling—a Monte-Carlo Technique for Reducing Variance". Applied Mathematics, Volume 2, Number 3 (September 1966), pp. 228–236.

- [8] T. Ritschel, T. Grosch, and H.-P. Seidel."Approximating Dynamic Global Illumination in Image Space". Proceedings ACM SIGGRAPH Symposium on Interactive 3D Graphics and Games (I3D), 2009, pp. 75–82.

- [9] P. Shanmugam and O. Arikan."Hardware accelerated ambient occlusion techniques on GPUs". Proceedings of the 2007 Symposium on Interactive 3D Graphics, 2007, pp. 73–80.

- [10] T. Umenhoffer, B. Tóth, and L. Szirmay-Kalos."Efficient Methods for Ambient Lighting". Spring Conference on Computer Graphics, 2009, pp. 99–106.

- [11] S. Zhukov, A. Iones, and G. Kronin."An ambient light illumination model". Proceedings of the Eurographics Rendering Workshop, 1998, pp. 45–56.

## Chapter 19: Real-Time Character Dismemberment

Aurelio Reis
id Software

### Overview

Modern games utilize a number of tricks to convey a realistic and intriguing world. In only a few years, realistic physics and destructible environments have garnered widespread industry adoption, yet despite this, few games attempt to model heavy damage on game characters. One of the main reasons for this is the complexity of decomposing the topology of a 3D mesh dynamically with real-time performance.

In this gem, we introduce an efficient general-use technique for character dismemberment that can be easily incorporated into an existing skeletal animation system. This implementation is perfectly suitable for games, real-time applications like military simulations, and other "serious games" where the accuracy of the damage modeling does not need to be precise (as in medical simulations).

While many games don't have the subject matter appropriate for dismemberment, when presented in a cartoonish way it's possible to approach gore and dismemberment such that it is relevant to the gameplay experience as opposed to being used purely for shock value or gimmick. Movies such as Evil Dead 2 and Kill Bill have approached gore in a comedic way that rivets audiences. As zombie and monster games gain popularity, it's likely that they will have the most to gain from character dismemberment.

### 19.1 What is Character Damage Modeling?

A character in this context is roughly defined as any animated figure in the shape of a creature using a bipedal skeleton and keyframed animations for its motion. In the game world, a character is represented as an entity that is capable of moving around using some scripted or autonomous behaviors with animations that coincide with this motion. As the character moves throughout the world, it may come in contact with a number of interactive elements that can affect the character in one way or another. In a first-person shooter, for instance, a character may move about, be influenced in some way by the environment (like when riding an elevator), and may shoot or be shot by other characters (player or non-player).

When a character is killed, the results are usually presented using some kind of pre-canned animation sequence with special effects like blood and gore strewn about. In most modern games, it is common practice to use "ragdoll" physics once the character is completely dead to add an additional sense of realism. In addition, some games go so far as to create bloody chunks and body parts, so-called "gibs" (for giblets). Combined, these elements result in character damage modeling that makes the game world more believable to the player. Games, after all, are about consequences, and realistic character deaths add to that realism.

While most games are able to get away with this degree of damage modeling, some games require more precise detail. Additional elements like projected decals and character scarring adds a lot, but the most dramatic change would be in the shape of the character itself. The effects of severe blunt force or impact trauma on a humanoid is enough to dismember most major limbs with ease, and it is this particular subset of damage modeling on which this gem focuses.

### 19.2 Methods of Mutilation

There are a number of ways to approach character dismemberment. The easiest and most straightforward solution would be to explicitly model the character as an articulated collection of body parts. Whenever a limb's bounding volume is hit, everything below that body part in the hierarchy can be manually detached. This technique, while incredibly simple, can be difficult to tune because model seams become prominent at the body part boundaries. Aesthetically, the quality is quite poor, although it can be hidden by clever modeling tricks (e.g., placing a gorget at the character's neck seam). In addition, this technique would require a large number of body parts to work well, which means additional draw calls that can result in reduced performance.

The extreme opposite of this would be to use computational geometry. Constructive solid geometry (CSG) boolean operations can be used to remove chunks of a character by dynamically splitting and removing polygons from the mesh. The uniform character mesh is a great advantage, but unfortunately this technique requires heavy CPU processing both in pre-transforming the animated mesh to the proper pose and in the required geometric operations. This technique can also result in a highly triangulated mesh with an unpredictable number of polygons that can become both a memory and performance concern.

Another possible method would be similar to the one used in the Soldier of Fortune series of games made by Raven Software. In their approach, they used what they called "gore zones" to represent up to 26 areas that can be toggled off on a given animated biped. The character models were created in such a way that every gore zone was completely capped, sealed and internally textured. This allowed them the flexibility to represent internal cavities such as the skull where the brain could become detached due to heavy trauma. The obvious downsides are a heavily triangulated model and a draw call for each gore zone—26 draw calls per character model. This can be avoided by consolidating gore zone geometry into a massive draw batch, but since this requires touching GPU memory, it can come at an expensive cost.

It's also possible to remove limbs by using geometry morphing. In this method, a blend shape is used to move the vertices of the limb to a desired final position, i.e., a stump or cap. This technique is easily hardware accelerated, although older hardware is only able to handle a few blend shapes. Because of this, dismembering multiple limbs at the same time requires modifying a vertex buffer where a morph scale is specified. In order to determine whether to apply the vertex position deltas to get the dismembered geometry location, this scale is modified at run time. Like the previous technique, this method suffers from having to modify a buffer in GPU memory.

Ultimately, each of these techniques has its own set of potential benefits and pitfalls. Ideally, what we want is a system that works with a uniform mesh because of the inherent performance benefits of a single draw call. In addition, our solution should be able to take advantage of commodity graphics hardware like that in the current generation of game consoles. This system also needs to be flexible enough to allow for any number of user-defined body parts (within reason) to be severed, generating a new and separate object that is able to coexist with the original model. Finally, it should require as little artist intervention as possible, allowing for arbitrary break points based on user-defined data that is easily modifiable.
