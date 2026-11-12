
![](img/0285f88bc840f313779e011725b623a5_528_0.png)

FIGURE 18.14 Creating a build.

### A Few Notes on the Output Files

When creating a Windows build, do note that there are actually two files. The first is the .exe file—the actual executable that the player launches to play the game. The second is a folder that is called NameOfYourGame_Data. To play the game, both must be present and in the same folder. When distributing the build, I find it helpful to take both files (the executable and the data folder) and zipping them into one archive and sending that off. We have had occasion here where we sent off a project to a client, who then tried to show it to someone else by just sending the .exe—it doesn't work.

On the Mac side, things are a little more elegant for the final user. An .app in Mac OS X looks to the user like a simple icon in their Finder. However, in reality it's really a folder (that OS X calls a Package) that contains a bunch of things. When Unity creates a Mac build, it creates an .app folder. On a PC, this will appear as a folder (which I usually compress into a zip archive before sending it off to someone), but when a Mac user unzips it to his machine, it will appear as a single icon that will contain all the assets he needs. The user just double-clicks to launch it.

Finally, note that when creating a Web Player build, Unity won't ask for a simple location to save the build—it will ask specifically for a Folder. The reason for this is that there are some very closely linked files that Unity will output. One will be the .html file that presents the Unity content (a .unity3d file). The specifics of this .html file can be controlled in a general way via the Player Settings in the Per-Platform Setting section. Specifically, the look of this html file can be altered and customized manually via your favorite HTML editor.

When creating this build, Unity puts an extra layer of compression on assets (LZMA) to try and help the player actually get to play the game faster; so the build can take a little bit longer to output.

## Conclusion

And with that we end. By this point, you should have a build that you can pass on to most any of your friends with Windows or Mac machines. It's a functioning game, but just a start.

Through many years of teaching 3D and game design in semester-long formats and one week seminars and writing many books, I've seen a lot of students create a lot of projects. Often these projects are of dazzling complexity, and sometimes they were more of the stuff of very solid foundational understanding. But in all cases, the nature of books or classes can yield a kind of dependency on the information deliverer (either the instructor or the book).

What this means is that the learners think they've got it all under control and that they've learned lots—and they have. But usually this new knowledge is right on the edge of their memory, and without immediate further application, it slides out of their memory banks.

So here's my plea. If you have not been doing the Homework and Challenges, go back and hit a few of them to expand on the game we've just built together. And go back and do this soon (as in today or tomorrow). Then, start a new project from scratch within the week. Being able to access skills and techniques and apply them to your unique situation is when a book or class has really been worth the money and time you've invested in learning it.

We've covered a lot in the pages of this book. Now go make the leap from tutorial follower to game creator and be brilliant!

- Animations area, defining multiple animations, 316
- Animator, 3
- AO, see ambient occlusion (AO)
- app folder, for a Mac build, 501, 507
- Append to Polygon tool, 211–22, 196f, 200
  - adding a string, 226, 226f
  - closing final knot, 187
  - connecting chest flap to back flap, 211, 211f
  - using, 22
- Append to Polygon Tool option, 187, 187f
- Application.LoadLevel function, 353
- Apply Button, collision detection checkers, 256, 257
- ApplyDamage function, 481
- arch, projecting bottom polygons of, 55
- arch edges, sewing up, 56–57, 56f
- areas, carving out, 128
- arm hole, selecting ring of edges around, 213
- arm position, as continuous, 181
- arm shape, extruding out, 213, 214f
- arms
  - adjusting, 416
  - closing off bottom of, 218, 218f
  - creating, 213–216
  - edges around, 209
  - extruding to create polygons for palm, 217, 217f
  - fixing disappearing, 416–417
  - joint layout for simplified, 215f
  - joints for, 291–296
  - rigged, 322f
- art assets, 5
  - bringing in, 32
  - created outside of Unity, 4
  - creating first, 6
- art team, 4
- artifacts, 33, 138
- assets
  - assembling in a package, 113
  - categories of, 5
  - creating, 5, 139, 329
  - deleting or reorganizing within Unity, 93
  - described, 5
  - for the game produced in this book, 5
  - importing into Unity, 4, 89, 92–93
  - inspecting, 95–96
  - keeping track of, 16
  - manually exporting for game characters, 314
  - organizing, 102
  - treating with reverence, 92–93
- Assets folder, 92–93, 96
- Assign New Material from the hotbox menu, 238
- Assign New Material window, 41, 238
- asymmetrical details, for Aegis Chung, 231–232
- atlassing, 48–49
- attenuation, of sound, 332
- Attribute Editor
  - bringing up, 53, 286
  - bringing up Create Render Node, 41
  - Drawing Overrides section, 300
  - in Maya compared to inspector in Unity, 95–96
  - opening, 298
  - opening texture node in, 72
  - Placement Extras section, 183–184
  - renaming node, 82–83
- attributes, of an animation, 449
- Audacity audio editing tool, 324
- Audio Clip, defining, 326
- Audio Clip input field, 211, 424
- audio clips, importing in Unity, 325
- audio editing tools, on the market, 324
- Audio Listener, 325
- Audio Reverb Zones, 327–328
- Audio Source, 325, 329, 330
- Audio Source components
  - adding, 326, 424
  - adding to any GameObject, 325
  - adding to CCTV Camera prefab, 211
  - with a looping steam sound, 488
- AutoDestruct for PistolSpark option, 419f
- automatic door openers, triggers as, 364
- Automatic Mapping
  - beginning mapping with, 42–45
  - creating UVs, 42–43, 43f
  - manipulators for, 60
- Awake function, 351–352, 361
  - finding mainCamera, 447
  - populating private variables in, 454
- Axis Divisions, creating a cylinder with, 60, 29f
- axis of rotation, rotating a collection of points, 22f
- axis of rotation, moving, 22
- B
- back (spine), see also spine
  - few joints in, 291
  - selecting edges across, 209, 210f
- back of the neck, rough outline of, 206, 206f
- back wall, creating, 317, 317f
- Backface Culling
  - excluding back faces, 25–26
  - in the Persp view panel, 25–33
  - turning on, 234–235, 235f
- background color
  - affecting cameras, 120
  - attribute of a camera, 120
  - attribute of Camera component, 119–120
  - tweaking, 121
- backpack, assigning vertices, 305
- Bake button, pressing, 147, 170, 314–315
- Bake Simulation Options window, 314–315
- baked animated character, exporting as, 276
- baked light, as .fbx, 276
- baked light, game screenshots of, 177f
- baked lighting, setting just right, 174
- Baked Shadows settings, 168–169, 175, 176f
- baked solutions, adjusting in Photoshop, 177–178
- baking
  - at 208, 266
  - in 3D, 146–147
  - animation, 276
  - taking a while in Unity, 147
  - terrain, 175
  - in Unity, 146–147, 160, 168–171
- Balaklava, Ukraine
  - abandoned Soviet nuclear submarine base, 7–8
  - facility entry, 174
- ball joint, centering circle on, 288f
- banner image, leaving at non-power-of-two settings, 505, 505f
- base textures
  - for everything but the head, 263, 263f
  - without added dirt or grime, 151f
