
![](img/d3e3fa4010906e98ec76be003a6e31c2_64_0.png)

**FIG 3.5** I needed to Separate the UVs so that they Could be Properly Relaxed.

![](img/d3e3fa4010906e98ec76be003a6e31c2_64_1.png)

**FIG 3.6** Using Lock Boundary Works Well in This Type of Situation. We Don't Want to Relax the Border UVs, But Only the Internal UVs and Lock Boundary Does Just That.

I then selected the front of the shirt and used the Move tool with Tear Off enabled to separate the UVs into separate UV shells for the front and back of the shirt as shown in Fig. 3.5.

From there, I used the UV Relax tool with Lock Boundary enabled and relaxed each UV shell as shown in Fig. 3.6.

At this point, I have two UV shells for the front and back of the shirt, which will allow me to easily texture the shirt. However, I need to do something about the UV seams that I have created so that I don't inadvertently increase the vertex count in my mesh. To eliminate some seams, I need to stitch the two halves of the shirt back together. To accomplish this, I selected the back of the shirt and used the Mirror UVs tool set to V to flip the UV shell in order to better align the two halves for stitching as shown in Fig. 3.7.

I then used the Move and Sew UVs to stitch the two UV shells together and thus eliminate two UV seams as shown in Fig. 3.8.

Once the two halves were stitched together, I did another UV Relax operation and used the Drag tool to fix any overlapping UVs. Looking back to Fig. 3.3, you can see the completed UV shell for the shirt. As you can see, the workflow is to create UVs that allow for ease of texturing, minimize UV seams by sewing edges together, and relax the UVs to remove any possible texture distortion. This is the workflow that I followed for all of the UVs in both the Tater and Thumper models.

![](img/d3e3fa4010906e98ec76be003a6e31c2_65_0.png)

**Fig 3.7** Before You Can Properly Sew the UVs, You'll Need to Align the Seams as Closely as Possible.

![](img/d3e3fa4010906e98ec76be003a6e31c2_65_1.png)

**Fig 3.8** By Sewing the Two Halves Together, I Was Able to Remove Two Seams and Thus Stop the GPU from Having to Split These Vertices.

It can also be very useful to overlap certain UV shells. For instance, with Tater's shoes, I decided that they would barely be visible in the game, so they are the smallest set of UV shells in the UV layout. To further save on space, I went ahead and overlapped both of the shoe's UV shells so they occupied the same UV coordinates. This allowed me to save a lot of space in the UV map as shown in Fig. 3.9.

![](img/d3e3fa4010906e98ec76be003a6e31c2_66_0.png)

**FIG 3.9** I Didn't Mind to Use a Repeating Texture for the Shoes, so in order to Save Space in the UV Map, I Overlapped Their UV Shells

For both Tater and Thumper, I didn't have a need for repeating textures. I think of these types of objects as having self-contained UVs, which is to say their UVs are meant to target specific parts on a single contained mesh. However, in contrast, a wall object will need to have its UVs repeat so that the object can represent many walls in a tiled fashion.

## Creating UVs for Thumper

The UVs for the Thumper model were created in a very similar fashion to Tater. In Fig. 3.10, you can see the complete UV layout.

![](img/d3e3fa4010906e98ec76be003a6e31c2_66_1.png)

**FIG 3.10** The UVs for Thumper Were Created in a Similar Fashion to Tater

The UVs for Thumper were meant to occupy targeted areas on a specific mesh, so there were no repeating UVs to be concerned with. Again, I started with surveying the model and determining which areas are the most important and thus need to occupy the most UV space. Areas of the gun that are located underneath the object would definitely require less of the 0–1 space. I did follow the basic workflow of breaking apart areas of the mesh into separate UV shells, relaxing and optimizing these areas and then sewing UV borders to minimize UV seams. However, instead of just relying on planar maps and then manually stitching borders together, I first used the Unwrap tool to unwrap the bulk of the gun. In Fig. 3.11, you can see the edges that were selected and the result from the Unwrap tool.

![](img/d3e3fa4010906e98ec76be003a6e31c2_67_0.png)

**FIG 3.11** I Used the Unwrap Tool to Quickly Get the UVs Created for the Bulk of the Gun.

Notice that with the Unwrap tool, I was able to unwrap tough areas such as where the gun handle attaches to the barrel by carefully selecting the UV edges that would create the UV seams. Also take note that the handle is unwrapped, but it's still connected as much as possible to the base UV shell of the gun as shown in Fig. 3.12. My goal for this UV unwrap was to keep as many UVs continuous as possible while still being able to maintain a UV layout that makes sense when it comes to texturing.

![](img/d3e3fa4010906e98ec76be003a6e31c2_68_0.png)

**FIG 3.12** The Handle Is Neatly Unwrapped and It's Also Still Connected to the Gun, Which Keeps More UVs Continuous.

Of course, you can't just use the Unwrap tool and have everything perfectly unwrapped. Once I had the base unwrapped, I then went and relaxed the UVs and arranged the UV shells into their final positions for the map. I also had to do a few manual projections, relax the UVs using the Relax tool, and sew the shells together to eliminate seams. In Fig. 3.13, you can see the polygons that I manually unwrapped.

![](img/d3e3fa4010906e98ec76be003a6e31c2_68_1.png)

**FIG 3.13** These Selected Polygons Were Manually Unwrapped.

### Use Unwrap Tool or Manual Projections

The Unwrap tool can be very helpful for quickly unwrapping a mesh. However, there are times with a complicated mesh that it can be difficult to figure out exactly how to select seams in order to get a clean unwrap. Also, you may find that when using the Unwrap tool, your UVs aren't being unwrapped in the most optimal way in regards to how you will be texturing in Photoshop. When I get into situations like this, I will create several smaller planar projections of the object and then manually stitch them together using the Move and Sew tools as we've discussed throughout this chapter. Sometimes, it's just easier to get your head around unwrapping the mesh so to speak by manually flattening the UVs via planar projections and then stitching them back manually.

In this section, we discussed creating UV maps. I'd like to reiterate that just as we found in Chapter 2 with modeling, there isn't a magic trick to optimizing your UVs. By understanding the important role UV seams play toward increasing vertex count when the mesh is rendered by the GPU, you can understand how and when to minimize the seams. Again, I have to bring up the common game industry phrase, "it depends." How you decide to optimize your UVs depends on your game content and the type of game you're creating. The workflow that I stick to in creating content always begins with surveying the mesh and planning a UV layout. From there, I begin basic unwraps and then minimize UV seams. Rinse and repeat. In the next section, we’ll take a practical look at the process behind creating the texture map for the Tater game object.

## Fundamentals of Game Textures

In the following sections, we are going to discuss the creation of the fundamentals of creating textures for the iDevice hardware. In regards to building content for the iPhone and iPad, I rely on the texture maps to bring detail to my objects. As we’ve discussed, the iDevice hardware, though powerful, can be somewhat limited in terms of game development, and you’ll find that the best performance can be gained by using only a combination of color and lightmaps. Before we take a look at the textures for Tater and Thumper, we first need to look at some fundamentals in regards to textures and the iPhone and iPad.

### Texture Formats

In this section, we are going to discuss texture formats as they relate to the iDevice hardware. These formats pertain to the formatting of the texture in system memory. There are several formats that are supported across the SGX GPU found in both the iPhone and iPad devices such as 32 bit, 16 bit, and PVRTC-compressed formats. In Fig. 3.14, you can see a list of available formats as found in the Importing Assets Settings dialog in Unity iOS.

### Texture Size

When creating my textures, I typically work in a much higher resolution than will be used in my actual Unity iOS project. This essentially helps to future proof my textures when new devices are released with higher resolution capabilities as well as making it easier to support multiresolutions across

![](img/d3e3fa4010906e98ec76be003a6e31c2_69_0.png)

**FIG 3.14** You Can Set a Texture Format in the Importing Assets Dialog within Unity iOS.
