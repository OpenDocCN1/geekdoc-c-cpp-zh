FIGURE 18.13  Banner as anticipated.

![](bbox=[0.33, 0.116, 0.741, 0.402])

The result will be a cleaner image that actually fills the space of the Dialog Banner as anticipated (Figure 18.13).

# Outputting the Final Build

Once the Player Settings have been configured to your taste, to create the build, choose File>Build Settings. Here, double-check that all the Scene files for the game are included in the Scenes In-Build section. If you've been testing the complete game in Unity this will already be populated.

Then, pick the Platform (in this case PC and Mac Standalone) and choose Windows or Mac in the Target Platform drop-down menu (Figure 18.14). Then click the Build button (or Build and Run if you want Unity to automatically open the .exe or .app it creates).

Now, to be honest, there's a bit of marketing going on in this window. The Platform area shows all sorts of target platforms (Web Player, iOS, Android, Xbox 360, PS3, and Wii). With standard Unity and even with Unity Pro, the only builds you can actually create and use are Web Player and PC and Mac Standalone. The rest of those platforms listed is Unity's way of saying, “You could build for these if you were a licensed developer with those platforms, and if you owned the additional licenses we sell to develop on those platforms.” So don't let that fool you—just because there are options doesn't mean they can actually be used.

However, having griped about that, after making a Windows build (for instance) simply change the Target Platform to Mac OS X Universal (if you've got people on legacy Macs who might be playing the game) or Mac OS X Intel Only if you're sure all the Mac users will be on reasonably recent hardware, and press the Build button. Just like that you've created a cross-platform application.