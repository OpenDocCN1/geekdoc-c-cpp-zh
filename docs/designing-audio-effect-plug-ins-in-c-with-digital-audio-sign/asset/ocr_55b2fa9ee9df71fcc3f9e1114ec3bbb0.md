# # Writing Plug-Ins with RackAFX

The RackAFX plug-in designer will help you write your plug-in. When you create a new RackAFX project, it will set up a new Visual C++ project folder for you and populate your project with all the files you will need. It will automatically create a new derived class based on the name of your project. When you set up graphical user interface (GUI) controls like sliders and buttons, it will write and maintain the code for you. You will be switching back and forth between RackAFX and your C++ compiler. There are buttons on the RackAFX GUI that will let you jump to the compiler as well as launch compiler functions like rebuilding and debugging. You will use RackAFX to maintain your GUI and your compiler to write the signal processing code.

# ## 3.1 Building the DLL

RackAFX sets up your compiler to deliver your freshly built dynamic link libraries (DLL) to the /PlugIns folder in the RackAFX application directory. If you ever want to see, move, or delete your DLL you can find this folder by using the menu item PlugIn > Open PlugIns Folder. Each time you create a new project, RackAFX creates a pass-through plug-in by default; you are urged to build and test the DLL right after creating the new project to check your audio input/output (I/O) and any other connections. You then write over the pass-through code with your own processing algorithm.

After a successful build, you use RackAFX to test and debug the plug-in. You tell RackAFX to load the DLL and create your plug-in. The client needs to handle four basic operations during the lifecycle of your component:

+   1. Creation of the plug-in
+   2. Maintaining the UI
+   3. Playing and processing audio through the plug-in
+   4. Destruction of the plug-in

![](bbox=[0.2, 0.75, 0.8, 0.98])